# go bible

测试环境

```
$ go version
go version go1.10.3 windows/amd64

$ echo $GOROOT
D:\Go\

$ echo $GOPATH
D:\Work\GoWorks

echo $GOBIN


go run t01.go

go build t01.go

```

go 标准库

```
输入，输出，排序，文本处理

os包，跨平台，操作系统接口（函数，变量）
```

```
入口
func main() {}

打印
fmt.Printf("Hello\n")

包
package main

包引入
import (
    "fmt"
)

格式化工具: gofmt
引入包：go get golang.org/x/tools/cmd/goimports

程序:

函数，变量，常量，类型声明
(func, var, const, type)

函数：关键字，函数名，参数列表，返回值列表

行尾：省略 ";"

语句块： {}
左括号{，不能独占一行


切片 arry[3] = {1, 2, 3}

    arry[m:n] === [m:n) 左闭右开，范围 0 <= m <= n <= len(array)

    arry[0:0] nil
    arry[0:1] 1
    arry[1:1] nil
    arry[1:2] 2
    arry[2:1] err
    arry[:1] 1
    arry[:3] {1, 2, 3}

注释
    单行  // xx
    多行  /* xx */
    
循环
for 初始化; 条件判断; 自增语句; {
}

go  不允许使用，未使用的变量，引入空标识符（中间变量，只用作占位符，值丢弃），"_"

for pos, elem := range 容器 {}
for _, elem := range 容器 {}

```


## 参考

http://www.gopl.io/

https://github.com/adonovan/gopl.io/

https://golang.org/

https://blog.golang.org

http://talks.golang.org/

https://play.golang.org

https://tour.golang.org

https://golang.org/pkg

gopl.io/ch1/helloworld

Golang--不定参数类型
https://www.cnblogs.com/zhangmingcheng/p/10148408.html