## 配置
-----------
配置文件格式为 `.ini`, 按环境划分: `conf_dev.ini`, `conf_release.ini`, `conf_online.ini`, 这样做的目的是根据环境来覆盖 conf.ini，使用服务启动时配置加载统一。


```
[Server]
network=tcp
;服务监听端口
port=11900

[log]
; LogPath : /home/logs/
LogPath=/home/logs/rpcproject/rpcproject.log
; level :DEBUG/INFO/WARNING/ERROR
Level=DEBUG
; RotateLines 1K/1M
RotateLines=0K
; RotateSize 1M/1G
RotateSize=0M
; RotateDaily true/false
RotateHourly=true


[Registry]
;是否启用注册中心 on:启用   off:不启用
status=off
;注册中心地址，多个地址以空格分割
addrs=127.0.0.1:2181
basePath=/odin_demo
;注册更新时间 1m表示一分钟
updateInterval=1m

[Redis]
redis=127.0.0.1:6379
pika=127.0.0.1:6379

```

