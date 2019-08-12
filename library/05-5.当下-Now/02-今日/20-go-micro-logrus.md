# logrus

```
go get github.com/sirupsen/logrus

[root@localhost]/data/git/labula8/test/goTest/work/src/github.com# echo $GOPATH
/data/git/labula8/test/goTest/work
[root@localhost]/data/git/labula8/test/goTest/work/src/github.com# echo $GOROOT
/data/git/labula8/test/goTest/go
[root@localhost]/data/git/labula8/test/goTest/work/src/github.com# echo $GOBIN 
/data/git/labula8/test/goTest/go/bin

[root@localhost]/data/git/labula8/test/goTest/work/logrus_test# go get github.com/sirupsen/logrus
package golang.org/x/sys/unix: unrecognized import path "golang.org/x/sys/unix" 
(https fetch: Get https://golang.org/x/sys/unix?go-get=1: dial tcp 74.125.68.141:443: i/o timeout)

[root@localhost]/data/git/labula8/test/goTest/work/src/golang.org/x# git clone https://github.com/golang/text.git

git clone https://github.com/golang/sys.git

Logrus的使用
１、安装
go get github.com/sirupsen/logrus

２、Logrus特性
六种日志级别：
logrus.Debug("Useful debugging information.")
logrus.Info("Something noteworthy happened!")
logrus.Warn("You should probably take a look at this.")
logrus.Error("Something failed but I'm not quitting.")
logrus.Fatal("Bye.")   //log之后会调用os.Exit(1)
logrus.Panic("I'm bailing.")   //log之后会panic()

３、log参数配置，定义输出、格式或者日志级别等
func init() {
    // 设置日志格式为json格式　自带的只有两种样式logrus.JSONFormatter{}和logrus.TextFormatter{}
    log.SetFormatter(&log.JSONFormatter{})

    // 设置将日志输出到标准输出（默认的输出为stderr，标准错误）
    // 日志消息输出可以是任意的io.writer类型
    log.SetOutput(os.Stdout)

    // 设置日志级别为warn以上
    log.SetLevel(log.WarnLevel)
}

４、常规使用
package main

import (
  log "github.com/sirupsen/logrus"
)

func main() {
  log.WithFields(log.Fields{
    "animal": "walrus",
  }).Info("A walrus appears")
}

５、logrus实例
package main
import (
    "github.com/sirupsen/logrus"
    "os"
)

// logrus提供了New()函数来创建一个logrus的实例。
// 项目中，可以创建任意数量的logrus实例。
var log = logrus.New()

func main() {
    // 为当前logrus实例设置消息的输出，同样地，
    // 可以设置logrus实例的输出到任意io.writer
    log.Out = os.Stdout

    // 为当前logrus实例设置消息输出格式为json格式。
    // 同样地，也可以单独为某个logrus实例设置日志级别和hook，这里不详细叙述。
    log.Formatter = &logrus.JSONFormatter{}

    log.WithFields(logrus.Fields{
    "animal": "walrus",
    "size":   10,
    }).Info("A group of walrus emerges from the ocean")
}

６、Fields
entry := logrus.WithFields(log.Fields{"request_id": request_id, "user_ip": user_ip})
entry.Info("something happened on that request") 
entry.Warn("something not great happened")

7、Entry
logrus.WithFields会自动返回一个 *Entry，Entry里面的有些变量会被自动加上
time:entry被创建时的时间戳
msg:在调用.Info()等方法时被添加
level

作者：yongfutian
链接：https://www.jianshu.com/p/752d712f70ce
来源：简书
简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。

```

```

../gitlab-pt.ztgame.com/Microservice/common/redis/redis.go:4:2: cannot find package "github.com/go-redis/redis" in any of:
	/data/git/labula8/test/goTest/go/src/github.com/go-redis/redis (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/github.com/go-redis/redis (from $GOPATH)
../gitlab-pt.ztgame.com/Microservice/common/middleware/go2sky.go:9:2: cannot find package "github.com/tetratelabs/go2sky" in any of:
	/data/git/labula8/test/goTest/go/src/github.com/tetratelabs/go2sky (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/github.com/tetratelabs/go2sky (from $GOPATH)
../gitlab-pt.ztgame.com/Microservice/common/middleware/go2sky.go:10:2: cannot find package "github.com/tetratelabs/go2sky/reporter" in any of:
	/data/git/labula8/test/goTest/go/src/github.com/tetratelabs/go2sky/reporter (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/github.com/tetratelabs/go2sky/reporter (from $GOPATH)
../github.com/micro/go-micro/broker/http_broker.go:27:2: cannot find package "golang.org/x/net/http2" in any of:
	/data/git/labula8/test/goTest/go/src/golang.org/x/net/http2 (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/golang.org/x/net/http2 (from $GOPATH)
../github.com/micro/go-micro/transport/http_transport.go:20:2: cannot find package "golang.org/x/net/http2/h2c" in any of:
	/data/git/labula8/test/goTest/go/src/golang.org/x/net/http2/h2c (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/golang.org/x/net/http2/h2c (from $GOPATH)
../github.com/micro/mdns/client.go:13:2: cannot find package "golang.org/x/net/ipv4" in any of:
	/data/git/labula8/test/goTest/go/src/golang.org/x/net/ipv4 (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/golang.org/x/net/ipv4 (from $GOPATH)
../github.com/micro/mdns/client.go:14:2: cannot find package "golang.org/x/net/ipv6" in any of:
	/data/git/labula8/test/goTest/go/src/golang.org/x/net/ipv6 (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/golang.org/x/net/ipv6 (from $GOPATH)
../github.com/snowzach/rotatefilehook/rotatefilehook.go:7:2: cannot find package "gopkg.in/natefinch/lumberjack.v2" in any of:
	/data/git/labula8/test/goTest/go/src/gopkg.in/natefinch/lumberjack.v2 (from $GOROOT)
	/data/git/labula8/test/goTest/work/src/gopkg.in/natefinch/lumberjack.v2 (from $GOPATH)
    
    go get github.com/go-redis/redis
    go get github.com/tetratelabs/go2sky
    go get golang.org/x/net/http2/h2c
    
    https://github.com/ably-forks/google.golang.org_grpc.git
```

## 参考

logrus

https:://github.com/sirupsen/logrus

Logrus的使用

https://www.jianshu.com/p/752d712f70ce

一键解决 go get golang.org/x 包失败
https://www.jianshu.com/p/a537ee63d606