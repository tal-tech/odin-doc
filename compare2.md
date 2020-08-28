## 性能对比
---------
### rpcx压测

rpcx框架作者已对多种rpc框架进行压测，具体压测过程及结果如下

#### 协议
所有的测试都是基于相同的数据，统一采用protobuffer进行序列化和反序列化

#### 测试指标
* 吞吐率: 每秒完成的请求量
* 平均延迟: 服务发出到收到response所需的时间
* P99延迟：99%的调用的延迟时间

#### 测试环境
cpu cores为 32, Intel Xeon E5-2630 V3 @2.4GHz

#### 测试结果
测试结果分别为模拟不同服务端处理耗时情况下


0ms处理耗时


![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p0-throughput.png?api=v2&nonce=1579610488346)![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p0-latency.png?api=v2&nonce=1579610502916)![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p0-p99.png?api=v2&nonce=1579610518862)


10ms处理耗时


![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p10-throughput.png?api=v2&nonce=1579610386426)![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p10-latency.png?api=v2&nonce=1579610403798)![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p10-p99.png?api=v2&nonce=1579610418165)


30ms处理耗时


![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p30-throughput000.png?api=v2&nonce=1579610077861)![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p30-latency000.png?api=v2&nonce=1579609980693)![pic](https://wiki.zhiyinlou.com/download/thumbnails/31521190/p30-p99000.png?api=v2&nonce=1579610057400)


整体来看，rpcx从吞吐、平均延迟、P99延迟等方面，仅在对比go原生rpc时，处于劣势，优于其他框架。


### odin压测

#### 测试指标
* 吞吐率: 每秒完成的请求量

#### 测试环境
* OS：CentOS Linux release 7.4.1708 (Core)
* CPU：4
* Memory：8G

#### 测试结果
测试结果分别为odin框架打开不同中间件情况下，整体QPS

![pic](https://wiki.zhiyinlou.com/download/attachments/31521190/image2020-1-22_17-15-59.png?version=1&modificationDate=1579684561140&api=v2)


从图中可以明显看出：

* odin框架打开默认中间件会带来一定的性能损耗，大约16%左右
* 其中LogWarn中间件对性能影响最大，达到10%

Recovery和Context转化中间件对性能影响几乎可以忽略，且rpcx调用件传递context和panic恢复比较关键，强烈建议默认打开，其他中间件可根据项目实际需要添加。

client端同样对上述功能进行了封装，对性能影响类似，记录Log影响最大，自行选择使用，或通过Log级别控制
