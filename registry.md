## 服务注册
--------
rpcx框架支持zookeeper、etcd、consul多种服务注册方式

odin框架封装了服务注册细节，目前只实现zookeeper、etcd两种注册方式，提供选择

### 配置
使用odin框架，只需引入服务注册配置即可：
```
[Registry]
;是否启用注册中心 on:启用   off:不启用
status=on
;注册中心地址，多个地址以空格分割，zk、etcd地址均可
addrs=10.90.70.56:2181 10.90.70.49:2181 10.90.70.59:2181
;注册服务根路径，可用于服务分组，区分不同业务组等
basePath=/xes_xueyan_hudong
;注册检查更新时间 1m表示一分钟，为rpcx原默认值
updateInterval=1m
```
### 注册方式
注册方式选择通过go build tags区分，默认zookeeper，改变需修改Makefile REGISTRY变量：
```
SERVICE := rpcproject
MAIN := cmd/rpcproject
#REGISTRY := etcd
REGISTRY := zookeeper
build:
    go build -tags "$(REGISTRY)" -ldflags $(LD_FLAGS) -gcflags "-N" -i -o ./bin/$(SERVICE) ./$(MAIN)
```

