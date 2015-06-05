# 使用Twisted建立服务
Game Server Requirements
* High scale
* Low latency(~200ms)

方案
* Python
* Twisted Asynchronous HTTP server for "slow" request
  - Reading/writing Amazon S3 on login/logout
  - Querying Facebook API
  - Top Scores database query

* Twisted Synchronous HTTP server for "fast" request
* Cluster of processes
* Support ~100 online players per CPU core

## Synchronous版本
```
from twisted.web import server, resource
from twisted.internet import reactor

class MyResource(resource.Resource):
    def render(self, request):
        name = request.args['name'][0]
        return "Hello %s!\n" % name

reactor.listenTCP(8080, server.Site(MyResource()))
reactor.run()
```

## Asynchronous版本
```
from twisted.web import server, resource
from twisted.internet import reactor

class MyResource(resource.Resource):
    def render(self, request):
        name = request.args['name'][0]
        # ... start working ...
        return twisted.web.NOT_DONE_YET

# later, when work is done ...
request.write("Hello")
request.finish()
```

When Asynchronous, how to connect "Before" and "After"?

```
def render(self, request):
    name = request.args['name'][0]
    d = defer.Deferred()
    d.addBoth(self.complete_deferred_request, request)
    my_async_function(d)
    return twisted.web.NOT_DONE_YET
    
def complete_deferred_request(self, body, request):
    if body == twisted.web.NOT_DONE_YET:
        return body # still asynchronous
    request.write(body)
    request.finish()
    
def my_async_function(d):
    result = # ... do something
    d.callback(result)
```

Another Option: @inlineCallbacks
```
def render(self, request):
    result = yield my)_async_function()
    returnValue(result)
    
```
* Simulates "stackless" threads
* Suspends code execution, then resumes later




