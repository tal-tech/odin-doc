## 断路器
---------------
断路功能通过插件在服务端实现，并通过可视化管理平台进行动态修改配置
### 错误熔断(circuitBreakerOption)
根据一短时间内错误比率熔断
```
"circuitbreaker": {
    "failureRatio": 0,
    "closed": false
}
```
* 配置说明，failureRatio字段为容忍失败比例，默认判断时间段为10s

