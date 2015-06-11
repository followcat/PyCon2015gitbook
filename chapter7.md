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