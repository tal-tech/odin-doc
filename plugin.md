### 插件化管理
------------
框架支持的一些可选功能，可以自行选择添加

插件包括：
* Pprof golang性能分析工具
* Expvr 内存使用分析工具
* Trace zipkin链路追踪工具

#### 启动项配置
```
//main函数
   s := rpcxserver.NewServer(rpcxserver.Addr(addr))
 
   s.AddBeforeServerStartFunc(bs.InitXesLogger("XueYan", "0.1"))
   //Optional Plugin(可选Pprof/Expvar/MaxFd，使用rigger frame命令添加插件)

    s.AddBeforeServerStartFunc(s.InitConfig(),
       s.InitRegistry(),
       s.InitRpcxPlugin(rpcxplugin.RatelimitOption(), rpcxplugin.MetricsOption(), rpcxplugin.TraceOption(), rpcxplugin.ContextOption(), rpcxplugin.RecoveryOption(), rpcxplugin.CostWarnOption()),
       s.DisableHTTPGateway(),
       s.RegisterServiceWithPlugin("Odin", app.NewService(), ""))
    s.AddAfterServerStopFunc(bs.CloseLogger())
```

#### 一键添加

使用方式：
```
rigger frame Plugin Pprof
```
