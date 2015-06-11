# Global Interpreter Lock: Episode I - Break the Seal

问题： 多通道但前方有红绿灯
红灯->全部通道停止

How to live along with GIL well.

Brainless Solution
------------------------
multi-process
* multiprocessing
* pp (Parallel Python)
* pyCSP


pp remote node

Release the GIL
* Especially suitable for processor-bound tasks
* Examples:
  * ctypes
  * Python/C extension
  * Cython
  * Pyrex

Cooperative Multitasking
* Executing the code when exactly needed
* Examples
  * generator
  * pyev
  * gevent

pyev code:
```
import pyev
import signal
import sys

def alarm_handler(watcher, revents):
    sys.stdout.write('.')
    sys.stdout.flush()
    
def timeout_handler(watcher, revents):
    loop = watcher.loop
    loop.stop()
    
def int_handler(watcher, revents):
    loop = watcher.loop
    loop.stop()
    
if __name__ == '__main__':
    loop = pyev.Loop()
    
    alarm = loop.timer(0.0, 1.0, alarm_handler)
    alarm.start()
    
    timeout = loop.timer(10.0, 0.0, timeout_handler)
    timeout.start()
    
    sigint = loop.signal(sinal.SIGINT, int_handler)
    sigint.start()
    
    loop.start()
```

gevent code:
```
import gevent
from gevent import signal
import signal as o_signal
import sys

if __name__ == '__main__':
    ctx = dict(stop_flag=False)
    
    def int_handler():
        ctx['stop_flag'] = True
    gevent.signal(o_signal.SIGINT, int_handler)
    
    count = 0
    while not ctx['stop_flag']:
        sys.stdout.write('.')
        sys.stdout.flush()
        
        gevent.sleep(1)
        
        count += 1
        if count > 10:
            break
```

Interpreter as an Instance?
-------------------------------
* Rough idea, not a concrete solution yet
* C program, single process, multi-thread
  * still can share states with relatively low penaly
* Allocate memory space for interpreter context
  * that is, accept an address to put instance context in Py_Initialize()