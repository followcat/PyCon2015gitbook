# 使用python建造一个简单的debugger

Use this simple code to make a Trace Function:
    
```
    def tracefunc(frame, event, arg):
        print("%s on #%d" % (event, frame.f_lineno))
        return tracefunc
        
    import sys
    sys.settrace(tracefunc)
    
    def foo():
        for i in range(1, 4):
            print(1/(3.0 - i))
            
    foo()
```
    
Drawbacks of our console debugger
* Only one breakpoint can be set
* Can't set and remove breakpoints during execution
* Unable to present our frame values in a nice view

Then
1. Multiprocess debugging
2. Attach to a running process
3. Django template debugging


[PyDev.Debugger](http://github.com/fabioz/PyDev.Debugger) Github


