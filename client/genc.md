## 生成SDK代码
----------

使用rigger genc go [servicename]生成客户端代码

生成代码为
```go
package rpcproject

import (
    "odin/proto"      //项目SDK统一存放位置
    "github.com/tal-tech/xtools/rpcxutil"
    "context"
    "sync"
)

const (
    ServiceName = "Rpcproject"
    BasePath    = "/odin_demo"
)

// NewClient 只是获取一个client对象，此时并没有连接服务发现中心，调用时才会去连接服务发现中心
// 不需传入注册中心addr，默认读取ini配置
//[Registration]
//addrs=127.0.0.1:2379 127.0.0.1:2379
//group=online/gray/release/dev
func NewClient() (*Client,error) {
    if client != nil {
        return client, nil
    }
    client = &Client{}
    return client, nil
}

func (c *Client) SayHello(ctx context.Context, req *proto.SayHelloRequest, resp *proto.SayHelloResponse) error{
    wrapclient := c.getRpcxClient()
    return wrapclient.WrapCall(ctx, "SayHello", req, resp)
}

func (c *Client) UserInfo(ctx context.Context, req *proto.UserInfoRequest, resp *proto.UserInfoResponse) error{
    wrapclient := c.getRpcxClient()
    return wrapclient.WrapCall(ctx, "UserInfo", req, resp)
}
//other methods
```

### 说明
* import路径：每个服务分组的服务proto、SDK最好都放在同一项目下
* BasePath：不同服务分组BasePath不同，需生成时指定-b参数
* 使用：声明Client后，调用client对应方法即可，client为全局唯一变量，多次NewClient不会创建多个client

