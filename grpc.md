介绍一下你是如何使用grpc的：

grpc意思为远程过程调用。使得在客户端可以像调用本地对象一样直接调用另一台不同机器上服务端应用的方法。gRPC 也是基于以下理念：定义一个服务，指定其能够被远程调用的方法（包含参数和返回类型）。在服务端实现这个接口，并运行一个 gRPC 服务器来处理客户端调用。在客户端拥有一个存根能够像服务端一样的方法。gRPC 提供了一种简单的方法来定义服务，同时客户端可以充分利用 HTTP2 stream 的特性，从而有助于节省带宽、降低 TCP 的连接次数、节省CPU的使用等。


特性
基于HTTP/2
HTTP/2 提供了连接多路复用、双向流、服务器推送、请求优先级、首部压缩等机制。可以节省带宽、降低TCP链接次数、节省CPU，帮助移动设备延长电池寿命等。gRPC 的协议设计上使用了HTTP2 现有的语义，请求和响应的数据使用HTTP Body 发送，其他的控制信息则用Header 表示。

IDL使用ProtoBuf
gRPC使用ProtoBuf来定义服务，ProtoBuf是由Google开发的一种数据序列化协议（类似于XML、JSON、hessian）。ProtoBuf能够将数据进行序列化，并广泛应用在数据存储、通信协议等方面。压缩和传输效率高，语法简单，表达力强。

多语言支持 （ C, C++, Python, PHP, Nodejs, C#, Objective-C、Golang、Java）
gRPC支持多种语言，并能够基于语言自动生成客户端和服务端功能库。目前已提供了C版本grpc、Java版本grpc-java 和 Go版本grpc-go，其它语言的版本正在积极开发中，其中，grpc支持C、C++、Node.js、Python、Ruby、Objective-C、PHP和C#等语言，grpc-java已经支持Android开发。

gRPC已经应用在Google的云服务和对外提供的API中，其主要应用场景如下：

低延迟、高扩展性、分布式的系统
同云服务器进行通信的移动应用客户端
设计语言独立、高效、精确的新协议
便于各方面扩展的分层设计，如认证、负载均衡、日志记录、监控等

**使用过程**

编写一个proto协议，然后生成对应python或者其他语言文件。

文件中包含了proto协议中定义的内容，比如提供的服务等。

```protobuf
service Decode {
    rpc DecodeRequest(request) returns (Response) {}
}
```

**服务端**

在服务端编写代码，根据标准库中提供的函数新建服务器，然后将添加接口服务，给服务器添加监听端口。

**接口服务可以重写**

**客户端**

```python
channel = grpc.insecure_channel('%s:%s' % (ip, port))
stub = decodereq_pb2_grpc.DecodeStub(channel)
resp = stub.DecodeReq(decodereq_pb2.PortraitDecodeReq(**data), timeout=2.0) 
```

客户端根据生成的文件和标准库中提供的函数来请求调用，需要传入参数。根据上面的proto文件，python中生成了DecodeStub类供客户端使用，传入channel进行初始化，初始化对象有一个，就是与proto中请求名同名的一个对象，即上面的DecodeReq，该对象被初始化为_UnaryUnaryMultiCallable类的一个实例。然后对其进行调用，调用该类中的call函数。传入参数，需要用proto中定义后生成的函数来传，其中包括了序列化方式。

到此结束等待返回结果。

使用stub.DecodeReq()就是调用_UnaryUnaryMultiCallable这个类的call函数。

https://blog.csdn.net/weixin_42589052/article/details/109653659

然后就可以在