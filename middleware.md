## 插件
--------
rpcx框架支持在一些固定节点添加插件，如下：
```go
type PluginContainer interface {
    DoRegister(name string, rcvr interface{}, metadata string) error
    DoRegisterFunction(name string, fn interface{}, metadata string) error
    DoUnregister(name string) error

    DoPostConnAccept(net.Conn) (net.Conn, bool)
    DoPostConnClose(net.Conn) bool

    DoPreReadRequest(ctx context.Context) error
    DoPostReadRequest(ctx context.Context, r *protocol.Message, e error) error

    DoPreWriteResponse(context.Context, *protocol.Message, *protocol.Message) error                           DoPostWriteResponse(context.Context, *protocol.Message, *protocol.Message, error) error

    DoPreWriteRequest(ctx context.Context) error
    DoPostWriteRequest(ctx context.Context, r *protocol.Message, e error) error
}
```

### 问题
对于请求，只能在读、写两个关键节点中执行插件操作，插件不能获取整个请求处理转态，如耗时等，故参考gin的中间件执行方式，实现新的插件功能

### xesMicroPlugin
目前已实现插件功能包括
```go
func RatelimitOption() Options {}         #限流插件
func TraceOption() Options {}             #zipkin trace插件
func CostWarnOption() Options {}          #耗时报警插件（记录耗时、调用方信息日志）
func ContextOption() Options {}           #context转化插件
func RecoveryOption() Options {}          #recovery捕获panic插件
```

插件支持可插拔式使用，在程序入口处指定。odin框架默认使用限流、trace、context转化
```go
func main() {
    //...
    s := rpcxserver.NewServer(rpcxserver.Addr(addr))
    s.AddBeforeServerStartFunc(bs.InitLoggerWithConf(),
    bs.InitPerfutil(),
    s.InitConfig(),
    s.InitRegistry(),
    //插件注册
    s.InitRpcxPlugin(rpcxplugin.RatelimitOption(), rpcxplugin.TraceOption(), rpcxplugin.ContextOption()),
    s.RegisterServiceWithPlugin("Rpcproject", app.NewRegisterService(), ""))
    s.AddAfterServerStopFunc(bs.CloseLogger())
    err = s.Serve()
    //...
}      
```
