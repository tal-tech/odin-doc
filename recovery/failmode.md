## FailMode
----------
rpcx框架支持以下FailMode
```go
//FailMode decides how clients action when clients fail to invoke services
type FailMode int

const (
    //Failover selects another server automaticaly
    Failover FailMode = iota
    //Failfast returns error immediately
    Failfast
    //Failtry use current client again
    Failtry
    //Failbackup select another server if the first server doesn't respon in specified time and use the fast response.
    Failbackup
)
```

目前客户端调用使用固定配置
* FailMode为Failover模式，失败选择其他server重试
* 重试次数为2次
