## 安装升级
-----------
### 环境检查
* 当前golang项目统一使用 go mod为依赖管理，请先按文档安装或对照相应版本
* 调试项目请在linux系统中编译打包，windows不保证可正常运行

### 安装脚手架
通过 [rigger](http://github.com/tal-tech/rigger)脚手架可一键创建odin模板的rpcx项目

### 生成框架

此处以"rpcproject"为项目名称
```shell
$ rigger new rpc rpcproject
正克隆到 '/winshare/go/src/rpcproject'...
rpcprojec项目已创建完成, 使用:
cd /winshare/go/src/rpcproject && rigger build 
开始你的微服务之旅！

```
