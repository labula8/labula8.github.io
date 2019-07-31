# go-micro


## 简单介绍

Micro是一个用来简化微服务开发的框架，提供了如下功能：

Go Micro - 基于Golang的插件式RPC框架，提供服务发现，客户端负载均衡，编码，同步和异步通讯功能。
API - API Gateway(API 网关)， 用来提供处理http请求。可以作为一个http的反向代理或者翻译相关的http请求到RPC服务。
Sidecar - 用来接入其他语言编写的应用到Micro中。
Web - 提供一个web dashboard，并且可以为Micro应用提供反向代理。
CLI - 用来跟Micro服务交互的命令行工具。
Bot - 用它我们可以在我们的服务中与Slack, HipChat, XMPP通讯。

Go-micro拥有很多特性：

服务注册、发现
负载均衡
消息解码，并默认支持json以及protobuf
基于rpc的请求响应
异步的消息通讯
接口可插拔

## 主要interface

整个Go Micro 都是有这8个interface构成的，换而言之只要理解了这8个接口，
并仔细研究其中一个实现基本就能了解整个框架的实现和架构。
下面先来看看这8个接口

### Transort

服务之间通信的接口。也就是服务发送和接收的最终实现方式，是由这些接口定制的。

type Socket interface {
    Recv(*Message) error
    Send(*Message) error
    Close() error
}

type Client interface {
    Socket
}

type Listener interface {
    Addr() string
    Close() error
    Accept(func(Socket)) error
}

type Transport interface {
    Dial(addr string, opts ...DialOption) (Client, error)
    Listen(addr string, opts ...ListenOption) (Listener, error)
    String() string
}

### Codec

有了传输方式，下面要解决的就是传输编码和解码问题，go-micro有很多种编码解码方式，
默认的实现方式是protobuf,当然也有其他的实现方式，json、protobuf、jsonrpc、mercury等等。

源码


type Codec interface {
    ReadHeader(*Message, MessageType) error
    ReadBody(interface{}) error
    Write(*Message, interface{}) error
    Close() error
    String() string
}

type Message struct {
    Id     uint64
    Type   MessageType
    Target string
    Method string
    Error  string
    Header map[string]string
}
Codec接口的Write方法就是编码过程，两个Read是解码过程。

### Registry

服务的注册和发现，目前实现的consul,mdns, etcd,etcdv3,zookeeper,kubernetes.等等，

type Registry interface {
    Register(*Service, ...RegisterOption) error
    Deregister(*Service) error
    GetService(string) ([]*Service, error)
    ListServices() ([]*Service, error)
    Watch(...WatchOption) (Watcher, error)
    String() string
    Options() Options
}

### Selector

以Registry为基础，Selector 是客户端级别的负载均衡，当有客户端向服务发送请求时， 
selector根据不同的算法从Registery中的主机列表，得到可用的Service节点，进行通信。
目前实现的有循环算法和随机算法，默认的是随机算法。

type Selector interface {
    Init(opts ...Option) error
    Options() Options
    // Select returns a function which should return the next node
    
    Select(service string, opts ...SelectOption) (Next, error)
    // Mark sets the success/error against a node
    
    Mark(service string, node *registry.Node, err error)
    // Reset returns state back to zero for a service
    
    Reset(service string)
    // Close renders the selector unusable
    
    Close() error
    // Name of the selector
    
    String() string
}
默认的是实现是本地缓存，当前实现的有blacklist,label,named等方式。

### Broker

Broker是消息发布和订阅的接口。很简单的一个例子，因为服务的节点是不固定的，
如果有需要修改所有服务行为的需求，可以使服务订阅某个主题，当有信息发布时，
所有的监听服务都会收到信息，根据你的需要做相应的行为。

type Broker interface {
    Options() Options
    Address() string
    Connect() error
    Disconnect() error
    Init(...Option) error
    Publish(string, *Message, ...PublishOption) error
    Subscribe(string, Handler, ...SubscribeOption) (Subscriber, error)
    String() string
}
Broker默认的实现方式是http方式，但是这种方式不要在生产环境用。go-plugins里有很多成熟的消息队列实现方式，有kafka、nsq、rabbitmq、redis，等等。

### Client

Client是请求服务的接口，他封装Transport和Codec进行rpc调用，也封装了Brocker进行信息的发布。

type Client interface {
    Init(...Option) error
    Options() Options
    NewMessage(topic string, msg interface{}, opts ...MessageOption) Message
    NewRequest(service, method string, req interface{}, reqOpts ...RequestOption) Request
    Call(ctx context.Context, req Request, rsp interface{}, opts ...CallOption) error
    Stream(ctx context.Context, req Request, opts ...CallOption) (Stream, error)
    Publish(ctx context.Context, msg Message, opts ...PublishOption) error
    String() string
}
当然他也支持双工通信 Stream 这些具体的实现方式和使用方式，以后会详细解说。
默认的是rpc实现方式，他还有grpc和http方式，在go-plugins里可以找到

### Server

Server看名字大家也知道是做什么的了。监听等待rpc请求。监听broker的订阅信息，等待信息队列的推送等。

type Server interface {
    Options() Options
    Init(...Option) error
    Handle(Handler) error
    NewHandler(interface{}, ...HandlerOption) Handler
    NewSubscriber(string, interface{}, ...SubscriberOption) Subscriber
    Subscribe(Subscriber) error
    Register() error
    Deregister() error
    Start() error
    Stop() error
    String() string
}

### Service

Service是Client和Server的封装，他包含了一系列的方法使用初始值去初始化Service和Client，
使我们可以很简单的创建一个rpc服务。

type Service interface {
    Init(...Option)
    Options() Options
    Client() client.Client
    Server() server.Server
    Run() error
    String() string
}

## 安装

由于Micro的服务发现并没有自己实现，仅仅是提供Plugin来接入第三方服务发现(consul, etcd), 默认使用的是consule
安装参考: consul installation doc
安装protobuf

## 参考

https://github.com/micro/go-micro

https://studygolang.com/articles/11520
https://studygolang.com/articles/21803

https://studygolang.com/search?q=micro
