## 开发目录
----------
业务代码开发全部在app目录下，以下为app目录结构及详细说明
```
├── common                     #公用方法、变量、常量等
│   ├── Const.go
│   ├── util.go
│   └── var.go
├── entity                    #实体层
│   └── user.go
├── repository                #仓库层
│   ├── memoryDao
│   │   └── user.go
│   ├── pikaDao
│   │   └── user.go
│   ├── redisDao
│   │   └── user.go
│   └── repository.go
├── service                   #service定义，由rigger自动生成       
│   ├── serviceBridge.go
│   └── service.go
├── serviceImpl               #service具体实现，开发业务逻辑目录
│   ├── HelloService.go
│   └── UserService.go
├── serviceInit.go            #service初始化，由rigger自动生成
└── serviceInterface          #service接口定义，定义服务所有对外提供方法，由业务开发定义，是所有自动生成代码的模板
    └── interface.go 
```
