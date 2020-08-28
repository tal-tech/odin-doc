## SDK存放规范
---------
rpcx客户端和服务端都需要引用request、response结构，分开放置可能造成版本不一致，故放在统一项目内管理，客户端和服务端都引用相同代码可避免这个问题

rigger生成好的rpcx客户端代码，存在多个不同服务都要引用的情况，更新后统一放在一个位置，不需多次生成且版本可以保持一致

这样就需要创建一个公共项目，保存同一个服务组内的所有proto定义、client代码

以大班整合项目为例：

```
├── barrage
│   ├── proto
│   │   └── proto.go
│   └── rpc
│       └── barrage.go
├── classroom
│   ├── proto
│   │   └── proto.go
│   └── rpc
│       └── classroom.go
├── duration
│   ├── proto
│   │   └── proto.go
│   └── rpc
│       └── duration.go
├── edc
│   ├── proto
│   │   └── proto.go
│   └── rpc
│       └── edc.go
```

### 说明
* 创建一个common项目，项目内包括所有服务proto定义和client代码
* 项目内以服务名为文件夹名
* proto.go的package名为proto
