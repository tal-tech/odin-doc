## 运行
-----------
### 编译
```
$ rigger build
go build -tags "zookeeper" -ldflags '-X "rpcproject/version.TAG=" -X "rpcproject/version.VERSION=" -X "rpcproject/version.AUTHOR=" -X "rpcproject/version.BUILD_INFO=" -X "rpcproject/version.BUILD_DATE=2019-11-13 16:17:28"' -gcflags "-N" -i -o ./bin/rpcproject ./cmd/rpcproject
```
### 发布系统编译
```
$ make TAG=$cur_tag
go build -tags "zookeeper" -ldflags '-X "rpcproject/version.TAG=v1.0.1" -X "rpcproject/version.VERSION=" -X "rpcproject/version.AUTHOR=" -X "rpcproject/version.BUILD_INFO=" -X "rpcproject/version.BUILD_DATE=2019-1116:17:28"' -gcflags "-N" -i -o ./bin/rpcproject ./cmd/rpcproject
```
### 打印help
```
$ ./bin/rpcproject --help
Usage of ./bin/rpcproject:
  -c string
        指定ini配置文件，以程序的二进制文件(myproject)为相对目录，正确的相对目录加载方式： -c ../conf/conf_xxx.ini； 默认为加载 ../conf/conf.ini
  -p string
        配置文件的前缀设置，用于以绝对路径形式加载，如  -c conf.ini -p /usr/pathto/myproject/conf
  -cfg string
        json config path (default "conf/config.json")
  -extended string
        扩展参数，程序未定义使用用途，用户可自行处理
  -f    foreground
  -m    mock 开关
  -mode int
        进程模型，取值：2 [gracehttp](github.com/facebookgo/grace/gracehttp), 默认为：[oversee](github.com/jpillora/overseer)
  -s string
        start or stop
  -usr1 string
        user defined flag -usr1
  -usr2 string
        user defined flag -usr2
  -usr3 string
        user defined flag -usr3
  -usr4 string
        user defined flag -usr4
  -usr5 string
        user defined flag -usr5
  -v    version
```

### 部署环境中启动
```
$ bin/rpcproject 
2019/11/13 16:23:32 CONF INIT,path:../conf/conf.ini
2019/11/13 16:23:32 [expvarutil] Expvar not enabled
2019/11/13 16:23:32 service.go:264: INFO : methodDoReregister has wrong number of ins:1
2019/11/13 16:23:32 service.go:264: INFO : methodGetMetadata has wrong number of ins:1
2019/11/13 16:23:32 service.go:264: INFO : methodSetReregister has wrong number of ins:2
2019/11/13 16:23:32 service.go:264: INFO : methodUpdate has wrong number of ins:1
2019/11/13 16:23:32 service.go:289: INFO : methodWrapcall reply type not a pointer:wrap.EndPoint
2019/11/13 16:23:32 server.go:174: INFO : server pid:19212
2019/11/13 16:23:32 server.go:174: INFO : server pid:19212
```
### 开发测试中启动
```
$ rigger start
2019/11/13 16:24:15 CONF INIT,path:conf/conf.ini
2019/11/13 16:24:15 [expvarutil] Expvar not enabled
2019/11/13 16:24:15 service.go:264: INFO : methodDoReregister has wrong number of ins:1
2019/11/13 16:24:15 service.go:264: INFO : methodGetMetadata has wrong number of ins:1
2019/11/13 16:24:15 service.go:264: INFO : methodSetReregister has wrong number of ins:2
2019/11/13 16:24:15 service.go:264: INFO : methodUpdate has wrong number of ins:1
2019/11/13 16:24:15 service.go:289: INFO : methodWrapcall reply type not a pointer:wrap.EndPoint
2019/11/13 16:24:15 server.go:174: INFO : server pid:19247
2019/11/13 16:24:15 server.go:174: INFO : server pid:19247
启动成功pid:19247
```

### 验证
```
$ rigger example zookeeper
2019/11/13 16:25:15 server.go:358: INFO : client has closed this connection: 10.90.101.139:27065
SayHello: i'm hello service,recv greeting:hello, i'm rpcproject client
AddUser: &{Id:2}
UserInfo: &{学而思 %!s(int=10) beijing}
UpdateUser: &{}
UserInfo: &{网校 %!s(int=20) beijing}
```

----------
至此，我们已经通过odin搭建并跑通了一个rpc服务！
