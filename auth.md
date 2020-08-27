## 鉴权
----------
### 服务端
* 初始化鉴权（main.go）
```go
    s.AddBeforeServerStartFunc(bs.InitLoggerWithConf(),
        bs.InitTraceLogger("HS-Golang", "0.1"),
        bs.InitPerfutil(),
        bs.InitPprof(),
        s.InitConfig(),
        s.InitRegistry(),
        s.InitRpcxPlugin(rpcxplugin.RatelimitOption(), rpcxplugin.MetricsOption(), rpcxplugin.TraceOption(), rpcxplugin.ContextOption(), rpcxplugin.RecoveryOption(), rpcxplugin.CostWarnOption()),
        s.DisableHTTPGateway(),
        //新增下一行，初始化服务鉴权功能
        s.InitRpcxAuth(),
        s.RegisterServiceWithPlugin("Xes-Micro", app.NewService(), ""))
    s.AddAfterServerStopFunc(bs.CloseLogger())
    err = s.Serve()
    if err != nil {
        panic(err)
    }
```

* 配置文件
```
[ValidRpcxAuth]
2010101=fe02fnelfn92rnknl
1203434=jeofnen823rubkj2j
```
格式为：appId=appKey

* 自定义appId管理

若不希望通过配置管理，而通过其他存储管理appId和appKey方式，可通过以下方式处理

```go
    s.AddBeforeServerStartFunc(bs.InitLoggerWithConf(),
        bs.InitTraceLogger("HS-Golang", "0.1"),
        bs.InitPerfutil(),
        bs.InitPprof(),
        s.InitConfig(),
        s.InitRegistry(),
        s.InitRpcxPlugin(rpcxplugin.RatelimitOption(), rpcxplugin.MetricsOption(), rpcxplugin.TraceOption(), rpcxplugin.ContextOption(), rpcxplugin.RecoveryOption(), rpcxplugin.CostWarnOption()),
        s.DisableHTTPGateway(),
        //新增下一行，初始化服务鉴权功能
        s.InitRpcxAuth(authAccess),
        s.RegisterServiceWithPlugin("Xes-Micro", app.NewService(), ""))
    s.AddAfterServerStopFunc(bs.CloseLogger())
    err = s.Serve()
    if err != nil {
        panic(err)
    }

func authAccess(in string) (string, bool) {
    //自定义逻辑 一定要使用内存缓存
    return "", false                         
}
```
实现func(string) (string, bool)类型方法，方法传入s.InitRpcxAuth()中，入参为appId。返回结果为appKey和ok

### 客户端
* 配置文件
```
[RpcxAuth]
appId=2010101
appKey=fe02fnelfn92rnknl 
```
appId、appKey对应服务端有效id和key

* 通过ctx传入appId、appKey

如客户端不使用配置管理appId和appKey，或使用多个appId和appKey，可以自行管理，但需通过context进行传递
```go
    ctx = context.WithValue(ctx, "RPCX_APPID", "2010101")
    ctx = context.WithValue(ctx, "RPCX_APPKEY", "fe02fnelfn92rnknl")
    err := client.SayHello(ctx, req, resp)
```
