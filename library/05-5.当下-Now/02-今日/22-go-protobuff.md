# go-protobuff

* 安装go-protobuff

* 编辑proto文件
```
syntax = "proto3";

package proto;

message Person {
    int64 id = 1;
    int32 age = 2;
    string name = 3;
    string sex = 4;
}
```

* 生成protobuff

```
$ protoc --version
libprotoc 3.9.1

protoc --go_out=. person.proto


```

* 调用编码

* 调用解码

```
package main

import (
	"fmt"
	stProto "t_protobuf/proto"
	"github.com/golang/protobuf/proto"
	"reflect"
)

func t_test() {
	stPerson := &stProto.Person{
		Id: 1,
		Age: 20,
		Name: "dada",
		Sex: "male",
	}
	fmt.Println("send#", stPerson)
	
	//编码protobuf
	pData, err := proto.Marshal(stPerson)
	if err != nil {
		panic(err)
	}
	
	fmt.Printf("pData=%s\n", pData)
	
	for pos, ch := range pData {
		fmt.Printf("[%d], 0x %x\t %d\t %c\n", pos, ch, ch, ch)
	}
	
	//解码protobuf
	stReceive := &stProto.Person{}
	err = proto.Unmarshal(pData, stReceive)
	
	if err != nil {
		panic(err)
	}
	fmt.Println("recieve#", stReceive)
	fmt.Printf("Id=%d, Age=%d\n", stReceive.GetId(), stReceive.GetAge())
	
	fmt.Println(reflect.TypeOf(stReceive))
	
	sType := reflect.TypeOf(stReceive)
	fmt.Println(reflect.TypeOf(sType))
}

func main() {
	fmt.Println("==== Begin Main t_proto1 ====\n")
	t_test()
	fmt.Println("==== End Main ====\n")
}

```

## 参考

https://studygolang.com/articles/14054
https://segmentfault.com/a/1190000009277748

https://www.jianshu.com/p/419efe983cb2

golang gRPC示例
https://studygolang.com/articles/4370
https://github.com/grpc/grpc-go

