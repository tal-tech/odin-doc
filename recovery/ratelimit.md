## 限流
-----------
限流功能通过插件在服务端实现，并通过可视化管理平台进行动态修改配置
### 限流插件(RatelimitOption())
```
"ratelimit": [
    {
        "path": "MethodName",
        "limit": 2000,
        "burst": 100,
        "closed": false,
        "maxDelayTime": 0
    }
],
```
* 配置说明，path为限流节点，limit为每秒限流请求量，burst为令牌桶最大令牌数量，maxDelayTime配置为获取预定令牌等待最长时间，超过则进行限流
