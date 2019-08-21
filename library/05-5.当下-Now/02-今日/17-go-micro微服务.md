# go-micro


## 简单介绍

```
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
```

### 特性

```
Go Micro把分布式系统的各种细节抽象出来。下面是它的主要特性。

服务发现（Service Discovery） - 自动服务注册与名称解析。
    服务发现是微服务开发中的核心。当服务A要与服务B协作时，它得知道B在哪里。
    默认的服务发现系统是Consul，而multicast DNS (mdns，组播)机制作为本地解决方案，
    或者零依赖的P2P网络中的SWIM协议（gossip）。

负载均衡（Load Balancing） - 在服务发现之上构建了负载均衡机制。
    当我们得到一个服务的任意多个的实例节点时，我们要一个机制去决定要路由到哪一个节点。
    我们使用随机处理过的哈希负载均衡机制来保证对服务请求颁发的均匀分布，并且在发生问题时进行重试。

消息编码（Message Encoding） - 支持基于内容类型（content-type）动态编码消息。
    客户端和服务端会一起使用content-type的格式来对Go进行无缝编/解码。
    各种各样的消息被编码会发送到不同的客户端，客户端服服务端默认会处理这些消息。
    content-type默认包含proto-rpc和json-rpc。

Request/Response - RPC通信基于支持双向流的请求/响应方式，我们提供有抽象的同步通信机制。
    请求发送到服务时，会自动解析、负载均衡、拨号、转成字节流。
    默认的传输协议是http/1.1，而tls下使用http2协议。

异步消息（Async Messaging） - 发布订阅（PubSub）头等功能内置在异步通信与事件驱动架构中。
    事件通知在微服务开发中处于核心位置。默认的消息传送使用点到点http/1.1，激活tls时则使用http2。

可插拔接口（Pluggable Interfaces） - Go Micro为每个分布式系统抽象出接口。
    因此，Go Micro的接口都是可插拔的，允许其在运行时不可知的情况下仍可支持。
    所以只要实现接口，可以在内部使用任何的技术。更多插件请参考：github.com/micro/go-plugins。
```

## 主要interface

整个Go Micro 都是有这8个interface构成的，换而言之只要理解了这8个接口，
并仔细研究其中一个实现基本就能了解整个框架的实现和架构。
下面先来看看这8个接口

### Transort

服务之间通信的接口。也就是服务发送和接收的最终实现方式，是由这些接口定制的。

```
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
```

### Codec

有了传输方式，下面要解决的就是传输编码和解码问题，go-micro有很多种编码解码方式，
默认的实现方式是protobuf,当然也有其他的实现方式，json、protobuf、jsonrpc、mercury等等。

源码
```

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
```

Codec接口的Write方法就是编码过程，两个Read是解码过程。

### Registry

服务的注册和发现，目前实现的consul,mdns, etcd,etcdv3,zookeeper,kubernetes.等等，
```
type Registry interface {
    Register(*Service, ...RegisterOption) error
    Deregister(*Service) error
    GetService(string) ([]*Service, error)
    ListServices() ([]*Service, error)
    Watch(...WatchOption) (Watcher, error)
    String() string
    Options() Options
}
```
### Selector

以Registry为基础，Selector 是客户端级别的负载均衡，当有客户端向服务发送请求时，
selector根据不同的算法从Registery中的主机列表，得到可用的Service节点，进行通信。
目前实现的有循环算法和随机算法，默认的是随机算法。
```
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
```
默认的是实现是本地缓存，当前实现的有blacklist,label,named等方式。

### Broker

Broker是消息发布和订阅的接口。很简单的一个例子，因为服务的节点是不固定的，
如果有需要修改所有服务行为的需求，可以使服务订阅某个主题，当有信息发布时，
所有的监听服务都会收到信息，根据你的需要做相应的行为。
```
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
```
Broker默认的实现方式是http方式，但是这种方式不要在生产环境用。go-plugins里有很多成熟的消息队列实现方式，有kafka、nsq、rabbitmq、redis，等等。

### Client

Client是请求服务的接口，他封装Transport和Codec进行rpc调用，也封装了Brocker进行信息的发布。
```
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
```
当然他也支持双工通信 Stream 这些具体的实现方式和使用方式，以后会详细解说。
默认的是rpc实现方式，他还有grpc和http方式，在go-plugins里可以找到

### Server

Server看名字大家也知道是做什么的了。监听等待rpc请求。监听broker的订阅信息，等待信息队列的推送等。
```
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
```
### Service

Service是Client和Server的封装，他包含了一系列的方法使用初始值去初始化Service和Client，
使我们可以很简单的创建一个rpc服务。
```
type Service interface {
    Init(...Option)
    Options() Options
    Client() client.Client
    Server() server.Server
    Run() error
    String() string
}
```
## 安装

由于Micro的服务发现并没有自己实现，仅仅是提供Plugin来接入第三方服务发现(consul, etcd), 默认使用的是consule
安装参考: consul installation doc
安装protobuf

```
./consul --help agent

部署启动
下载consul文件，consul download：

wget https://releases.hashicorp.com/consul/1.2.2/consul_1.2.2_linux_amd64.zip
unzip consul_1.2.2_linux_amd64.zip
解压后就是一个consul文件。

启动第一个consul server，注意-bootstrap：

# cat start.sh
#!/bin/bash
nohup ./consul agent  -bootstrap -bind=10.10.199.154 -server -data-dir=./data/ 2>&1 1>consul.log  &
启动后，可以直接通过网址http://127.0.0.1:8500/ui打开consul的网页。

查看组成consul服务的node：

$ ./consul catalog nodes
Node           ID        Address        DC
10-10-199-154  3f33abc5  10.10.199.154  dc1

$ curl 127.0.0.1:8500/v1/catalog/nodes 2>/dev/null |python -m json.tool
[
    {
        "Address": "10.10.199.154",
        "CreateIndex": 5,
        "Datacenter": "dc1",
        "ID": "3f33abc5-a8b1-8dfc-d553-051ea2be6750",
        "Meta": {
            "consul-network-segment": ""
        },
        "ModifyIndex": 6,
        "Node": "10-10-199-154",
        "TaggedAddresses": {
            "lan": "10.10.199.154",
            "wan": "10.10.199.154"
        }
    }
]
还可以通过dns查询成员node的地址，默认后缀为node.consul：

$ dig @127.0.0.1 -p 8600 10-10-199-154.node.consul

dig @127.0.0.1 -p 8600 192-168-56-102.node.consul

; <<>> DiG 9.9.4-RedHat-9.9.4-61.el7 <<>> @127.0.0.1 -p 8600 10-10-199-154.node.consul
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 35964
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;10-10-199-154.node.consul.	IN	A

;; ANSWER SECTION:
10-10-199-154.node.consul. 0	IN	A	10.10.199.154

;; ADDITIONAL SECTION:
10-10-199-154.node.consul. 0	IN	TXT	"consul-network-segment="

;; Query time: 0 msec
;; SERVER: 127.0.0.1#8600(127.0.0.1)
;; WHEN: Tue Aug 21 17:55:03 CST 2018
;; MSG SIZE  rcvd: 106
服务操作
服务是consul管理的基本单元之一。

注册服务
要注册的服务可以直接做成本地配置文件：

sudo mkdir /etc/consul.d
echo '{"service": {"name": "web", "tags": ["rails"], "port": 80}}'  | sudo tee /etc/consul.d/web.json
或者通过api注册，注意api是agent/service：

$ cat web2.json
{
    "Name": "web2",
    "Tags": [
        "rails"
    ],
    "Address": "",
    "Port": 81,
    "ServiceEnableTagOverride": false
}
$ curl --request PUT --data @web2.json  http://127.0.0.1:8500/v1/agent/service/register
查询服务地址
命令行查看所有服务：

$ ./consul catalog services
consul
web
web1
dns查询指定服务地址，默认后缀为service.consul，注意查询类型要指定为为srv，才能看到服务端口：

$ dig @127.0.0.1 -p 8600 web.service.consul srv
 dig @127.0.0.1 -p 8600 web2.service.consul srv

; <<>> DiG 9.9.4-RedHat-9.9.4-61.el7 <<>> @127.0.0.1 -p 8600 web.service.consul srv
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 28545
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 3
;; WARNING: recursion requested but not available

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
;; QUESTION SECTION:
;web.service.consul.		IN	SRV

;; ANSWER SECTION:
web.service.consul.	0	IN	SRV	1 1 80 10-10-199-154.node.dc1.consul.

;; ADDITIONAL SECTION:
10-10-199-154.node.dc1.consul. 0 IN	A	10.10.199.154
10-10-199-154.node.dc1.consul. 0 IN	TXT	"consul-network-segment="

;; Query time: 0 msec
;; SERVER: 127.0.0.1#8600(127.0.0.1)
;; WHEN: Tue Aug 21 18:54:22 CST 2018
;; MSG SIZE  rcvd: 148
http api查询：

$ curl http://10.10.199.154:8500/v1/catalog/service/web |python -m json.tool
[
    {
        "ID": "3f33abc5-a8b1-8dfc-d553-051ea2be6750",
        "Node": "10-10-199-154",
        "Address": "10.10.199.154",
        "Datacenter": "dc1",
        "TaggedAddresses": {
            "lan": "10.10.199.154",
            "wan": "10.10.199.154"
        },
        "NodeMeta": {
            "consul-network-segment": ""
        },
        "ServiceKind": "",
        "ServiceID": "web",
        "ServiceName": "web",
        "ServiceTags": [
            "rails"
        ],
        "ServiceAddress": "",
        "ServiceMeta": {},
        "ServicePort": 80,
        "ServiceEnableTagOverride": false,
        "ServiceProxyDestination": "",
        "ServiceConnect": {
            "Native": false,
            "Proxy": null
        },
        "CreateIndex": 10,
        "ModifyIndex": 10
    }
]
查看agent上的所有服务：

curl http://10.10.199.154:8500/v1/agent/services 2>/dev/null |python -m json.tool
删除服务
curl --request PUT  http://127.0.0.1:8500/v1/agent/service/deregister/web1
Connect配置
Connect是consul的重要特性，简单说就是，consul可以为服务配置访问代理，并且负责中间的认证和加密。

Consul Connect中有详细说明，这里使用的也是其中的例子。

在本地启动一个echo服务：

$ yum install -y socat
$ socat -v tcp-l:8181,fork exec:"/bin/cat"
注册到consul中，注意connect字段不为空，表示consul需要为socat服务准备代理:

$ cat <<EOF | sudo tee /etc/consul.d/socat.json
{
  "service": {
    "name": "socat",
    "port": 8181,
    "connect": { "proxy": {} }
  }
}
EOF
重启consul，或者给consul发送SIGHUB信号，重新加载配置。

用下面的命令，手动在本地启动一个proxy：

./consul connect proxy -service web -upstream socat:9191
然后就可以通过9191端口访问8181端口的服务：

$ nc 127.0.0.1 9191
helo
操作到这里的时候报错，通过9191无法联通，consul日志显示：

2018/08/21 19:31:44 [WARN] agent: Check "service:socat-proxy" socket connection failed: dial tcp 10.10.199.154:20233: connect: connection refused
Key操作
更详细的文档位于：Consul Key 操作。

需要注意的是consul支持多数据中心，key-value存储不在多个数据中心之间同步。见：What data is replicated between Consul datacenters?

写入一个名为”k1”的key，value为”hello”:

curl -X PUT --data "hello" 127.0.0.1:8500/v1/kv/k1
读取k1:

$ curl 127.0.0.1:8500/v1/kv/k1
[
    {
        "LockIndex": 0,
        "Key": "k1",
        "Flags": 0,
        "Value": "aGVsbG8=",      //base64编码
        "CreateIndex": 20077,
        "ModifyIndex": 20077
    }
]
key的读取接口支持6个参数：

key (string: "")         - Specifies the path of the key to read.
dc (string: "")          - Specifies the datacenter to query.
                           This will default to the datacenter of the agent being queried.
                           This is specified as part of the URL as a query parameter.
recurse (bool: false)    - Specifies if the lookup should be recursive and key treated as a prefix instead of a literal match.
                           This is specified as part of the URL as a query parameter.
raw (bool: false)        - Specifies the response is just the raw value of the key, without any encoding or metadata.
                           This is specified as part of the URL as a query parameter.
keys (bool: false)       - Specifies to return only keys (no values or metadata). Specifying this implies recurse.
                           This is specified as part of the URL as a query parameter.
separator (string: '/')  - Specifies the character to use as a separator for recursive lookups.
                           This is specified as part of the URL as a query parameter.
例如查看指定路径下的所有key：

$ curl 127.0.0.1:8500/v1/kv/k1?keys
[
    "k1",
    "k1/k11"
]
删除key:

curl -X DELETE 127.0.0.1:8500/v1/kv/k1
consul-template
consul-template是一个根据consul中的数据自动渲染配置文件的工具，和confd很类似，虽然consul-template自称：

Q: How is this different than confd?
A: The answer is simple: Service Discovery as a first class citizen. You are
also encouraged to read this Pull Request on the project for more background
information. We think confd is a great project, but Consul Template fills a
missing gap. Additionally, Consul Template has first class integration with
Vault, making it easy to incorporate secret material like database credentials
or API tokens into configuration files.
不过我感觉没有什么太大的区别，confd支持的后端还更丰富：

etcd
consul
vault
environment variables
file
redis
zookeeper
dynamodb
rancher
ssm (AWS Simple Systems Manager Parameter Store)
这里简单了解一下consul-template，没准以后会用到。

在consul tools download页面中可以找到下载地址：

wget https://releases.hashicorp.com/consul-template/0.19.5/consul-template_0.19.5_linux_amd64.tgz
tar -xvf consul-template_0.19.5_linux_amd64.tgz
解压后得到一个二进制文件consul-template。
```

go run main.go 
==== Main Begin ====
serviceName=test.server
2019/08/12 12:22:33 get consul config fail: error loading source consul: source not found: test/server
exit status 1


git clone https://github.com/golang/sys.git

../github.com/nats-io/nkeys/keypair.go:21:2: cannot find package "golang.org/x/crypto/ed25519" in any of:
	/data/git/labula8/test/goTest/go/src/golang.org/x/crypto/ed25519 (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/golang.org/x/crypto/ed25519 (from $GOPATH)
[root@localhost]/data/git/labula8/test/goTest/work/src/hello_world# go get golang.org/x/crypto
package golang.org/x/crypto: unrecognized import path "golang.org/x/crypto" (https fetch: Get https://golang.org/x/crypto?go-get=1: dial tcp 216.239.37.1:443: i/o timeout)

git clone https://github.com/golang/crypto.git

# github.com/micro/go-micro/client/grpc
../github.com/micro/go-micro/client/grpc/codec.go:23:24: undefined: encoding.Codec
# github.com/micro/go-micro/server/grpc
../github.com/micro/go-micro/server/grpc/codec.go:24:24: undefined: encoding.Codec

```
  1 package grpc
  2 
  3 import (
  4     "encoding/json"
  5     "fmt"
  6     "strings"
  7 
  8     b "bytes"
  9 
 10     "github.com/golang/protobuf/jsonpb"
 11     "github.com/golang/protobuf/proto"
 12     "github.com/micro/go-micro/codec"
 13     "github.com/micro/go-micro/codec/bytes"
 14     "github.com/micro/go-micro/codec/jsonrpc"
 15     "github.com/micro/go-micro/codec/protorpc"
 16     "google.golang.org/grpc"
 17     "google.golang.org/grpc/encoding"
 18     "google.golang.org/grpc/metadata"
 19 )
 20 
 21 type jsonCodec struct{}
 22 type bytesCodec struct{}
 23 type protoCodec struct{}
 24 type wrapCodec struct{ encoding.Codec }
```

go get github.com/lucas-clemente/quic-go

go get github.com/micro/protobuf/protoc-gen-go

protoc --go_out=plugins=micro:. hello_world.proto

curl http://localhost:8500/v1/agent/service/register -X PUT -i -H "Content-Type:application/json" -d '{"ID":"kv", "Name":"kv", "Address":"127.0.0.1", "port":8000}'

curl http://localhost:8500/v1/agent/service/register -X PUT -i -H "Content-Type:application/json" -d '{"ID":"register", "Name":"register", "Address":"127.0.0.1", "port":8100}'

curl http://localhost:8500/v1/catalog/service/kv | python -m json.tool

./consul agent -server -ui -bootstrap-expect=1 -data-dir=./data/ -node=devmaster -advertise=192.168.56.102 -bind=0.0.0.0 -client=0.0.0.0

curl http://localhost:8500/v1/catalog/service/yutest | python -m json.tool
[
    {
        "Address": "192.168.56.102",
        "CreateIndex": 32422,
        "Datacenter": "dc1",
        "ID": "849a6ad1-79c7-c5d0-b7fb-ce36c9167df2",
        "ModifyIndex": 32422,
        "Node": "devmaster",
        "NodeMeta": {
            "consul-network-segment": ""
        },
        "ServiceAddress": "10.10.10.129",
        "ServiceConnect": {},
        "ServiceEnableTagOverride": false,
        "ServiceID": "yutest-6990e32b-96fc-4dfa-be8e-31e44d8c6155",
        "ServiceKind": "",
        "ServiceMeta": {},
        "ServiceName": "yutest",
        "ServicePort": 28596,
        "ServiceProxy": {},
        "ServiceProxyDestination": "",
        "ServiceTags": [
            "t-789caa562a294acc2b2ec82f2a51b252ca28292950aa05040000ffff4f930768",
            "t-789caa564a2acacf4e2d52b252ca28292950aa05040000ffff364d0600",
            "t-789caa562a4e2d2a4b2d52b252ca2d4d2e50aa05040000ffff37200607",
            "t-789caa562a4a4dcf2c2e29aa54b2524acecf2b2ecd51aa05040000ffff560f07c8",
            "t-789caa562a28ca2fc94fcecf51b252ca2d4d2e50aa05040000ffff46a906e2",
            "e-789c9490c1cac2301084df65cfe53ffd78c8432888371159e928856453b31b4125ef2e85125bb0a0e7ef9b619827090790a35d8cfe6f23be13ac733821514309d70c3572d59a0adb913664f77e19ded86728b97d2db970c0b16bdfc1dc89adfe27ae64ef4b53036a9cec7b1df243f723ca7ccc47ff508637b48fa258bc63c40b7f543a1f4201c62d1b0fb56a091cc8d199bd824a79050000ffff207b8e6d",
            "e-789c7ccebdaac24010c5f1773975b8d5c5625fc04610d44e44067294c0ee24666605917d770984f8516cff9b33ff2754121170e8fbf8b71da86b49dc74cabd8ba3c1c85ba639c2227fd16e160dfc31d4c15d62a6211c97b1ab249ebbf67d9c3bf5d5ff87d51c633995a9c4865e8dd59499545a16f1f5a041a24b2b2ed3bcf9484908b84834a29457000000ffff7f25677d",
            "e-789c8ccd4d0ac2400cc5f1bbbc75f1003985883b7111308a90f9689311a4ccdd652a161d37dde6fdc96f46e420201c53d2ddfe1e6f1830c958c41cb4ae6d38c88801feccbf87076b11039dd6f82b339fde2f3f552caaf55c9b613945931eb1dc21cbe11fb9b0f3162788f3d2d2dc2ae100c295d504b5be020000ffffbef454e3",
            "e-789c8ccd3d0ac24014c4f1bb4c1dacc462cf6025568ac8838c12d88f98f75610d9bb4b20ae825b58ff67f83d1125100efb94fcea9022b7831a3a4cbc65aac1d5c53bee96d2c11e633bdcc5672adcb19eaf12781efacf290fd136ebaf6dccde975399651d535436e92535ec5a7e713531fe43079af46232d36a1325c0e1225e89525e010000ffff419666ed",
            "v-789cca492c492d2e01040000ffff08cc028e"
        ],
        "ServiceWeights": {
            "Passing": 1,
            "Warning": 1
        },
        "TaggedAddresses": {
            "lan": "192.168.56.102",
            "wan": "192.168.56.102"
        }
    }
]

## 参考

https://github.com/micro/go-micro

https://gitee.com/mirrors/go-micro

https://studygolang.com/articles/11520
https://studygolang.com/articles/21803

https://studygolang.com/search?q=micro

https://micro.mu/docs/go-micro.html
https://micro.mu/docs/cn/index.html

https://github.com/micro/protoc-gen-micro
https://github.com/micro/examples/tree/master/greeter

https://github.com/micro-in-cn/tutorials/tree/master/examples/basic-practices

https://micro.mu/blog/2016/04/18/micro-architecture.html

https://github.com/micro/go-micro#getting-started

https://godoc.org/github.com/micro/go-micro#Option

Micro的架构与微服务的设计模式
http://btfak.com/%E5%BE%AE%E6%9C%8D%E5%8A%A1/2016/04/18/micro-architecture/

http://btfak.com/%E5%BE%AE%E6%9C%8D%E5%8A%A1/2016/03/28/go-micro/

https://www.cnblogs.com/li-peng/p/9598879.html
https://www.cnblogs.com/li-peng/p/9689786.html

http://gorm.book.jasperxu.com/

https://www.consul.io/downloads.html

https://github.com/golang/crypto

https://github.com/micro/go-plugins

http://gorm.book.jasperxu.com/development.html#a

https://github.com/prometheus/client_golang

https://github.com/spf13/viper

https://github.com/uber-go/zap

http://btfak.com/%E5%BE%AE%E6%9C%8D%E5%8A%A1/2016/03/28/go-micro/
https://micro.mu/docs/cn/index.html

https://www.cnblogs.com/li-peng/p/9558421.html
https://www.cnblogs.com/li-peng/p/9598879.html

https://studygolang.com/articles/11520

iris-go
https://learnku.com/docs/iris-go/10/why/3759

gorm

https://cloud.tencent.com/developer/article/1193786

micro installation

https://www.jianshu.com/p/0ff8c0923950


https://www.jianshu.com/p/4ed1010b4c22

https://segmentfault.com/a/1190000017572032

consul

https://www.consul.io/api/agent/service.html

https://releases.hashicorp.com/consul/1.5.3/

http://blog.cxiangnet.cn/2018/04/10/consul-%E4%BB%8B%E7%BB%8D/

https://www.cnblogs.com/acm-bingzi/p/consul_ip.html

https://www.lijiaocn.com/%E9%A1%B9%E7%9B%AE/2018/08/17/consul-usage.html

https://segmentfault.com/a/1190000018731395?utm_source=tag-newest

https://segmentfault.com/a/1190000018731395

https://www.cnblogs.com/xiaohanlin/p/8016803.html

https://www.cnblogs.com/williamjie/p/9369713.html

https://www.cnblogs.com/bossma/p/9756809.html

https://www.jianshu.com/p/2fa8f33fa1dd

https://www.cnblogs.com/lori/p/8391351.html

https://www.cnblogs.com/ASPNET2008/p/6892137.html

https://www.jianshu.com/p/92955eeb4c41

zookeeper vs consul

https://mp.weixin.qq.com/s?__biz=MzA5OTAyNzQ2OA==&mid=208173179&idx=1&sn=392c17b136c2bf570429785702d98353&scene=0&key=dffc561732c226516d4dccb1f165c5b24e823a11384b262d55dc20e3bd0d4cd21c219e8fc2bb2817fd3ccd46f36db04a&ascene=14&uin=ODY5ODkzMzQw&devicetype=iPhone+OS8.4.1&version=16020610&nettype=WIFI&fontScale=100&pass_ticket=yxu6Cmc0yX5TWpekVDtFbQhGNYo%2BPbTVmjkpYiq2xiXv6Mbhq3rZUqZkbefMNm11

logrus

https://www.jianshu.com/p/752d712f70ce
