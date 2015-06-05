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



