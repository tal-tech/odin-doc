## 目录结构
---------
项目目录结构如下，分别为开发目录app、main文件目录cmd、版本管理目录version、编译二进制目录bin、配置目录conf，其他为编译部署调试等脚本
```
├── app                            #项目工程目录
│   ├── common                     #公用代码目录
│   │   ├── Const.go               #常量
│   │   ├── util.go                #工具方法
│   │   └── var.go                 #公共变量
│   ├── entity                     #实体定义目录
│   │   └── user.go                #用户实体
│   ├── repository                 #实体仓库目录
│   │   ├── memoryDao              #内存仓库目录
│   │   │   └── user.go            #用户实体仓库实现
│   │   ├── pikaDao                #pika仓库目录
│   │   │   └── user.go            #用户实体仓库实现
│   │   ├── redisDao               #redis仓库目录
│   │   │   └── user.go            #用户实体仓库实现
│   │   └── repository.go          #仓库选择实现
│   ├── service                    #服务代码目录
│   │   ├── serviceBridge.go       #服务组合
│   │   └── service.go             #服务结构体
│   ├── serviceImpl                #服务实现目录
│   │   ├── HelloService.go        #hello服务实现
│   │   └── UserService.go         #用户服务实现
│   ├── serviceInit.go             #服务初始化
│   └── serviceInterface           #服务接口目录
│       └── interface.go           #服务接口定义
├── bin                            #可执行文件目录
│   └── odin                       #可执行文件
├── cmd                            #命令代码目录
│   └── odin
│       └── main.go                #main.go
├── conf                           #配置文件目录
│   ├── conf_dev.ini               #开发配置文件
│   ├── conf.ini                   #配置文件
│   ├── conf_release.ini           #测试线配置文件
│   ├── conf_online.ini            #线上配置文件
│   └── odin.ini                   #supervisor 配置文件 
├── examples                       #示例代码目录
│   └── main.go
├── go.mod                     
├── Makefile
├── README.md
└── version                       #版本目录
    └── version.go                #版本文件

```

