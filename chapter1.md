# 使用python建造一个简单的debugger

Use this simple code:
    
    def tracefunc(frame, event, arg):
        print("%s on #%d" % (event, frame.f_lineno))
        return tracefunc
        
    import sys
    sys.set_trace(tracefunc)
    
    def foo():
        for i in range(1, 4):
            print(1/(3.0 - i))
            
    foo()
