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

Pyev code:
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