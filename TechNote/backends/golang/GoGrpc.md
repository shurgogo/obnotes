1. 安装 protoc-gen-go
```bash
go install github.com/golang/protobuf/protoc-gen-go@latest
```
2. 写 .proto 文件
```go
syntax = "proto3";  
  
package grpc;  
  
option go_package="./gogrpc"; //输出的pb.go所在的包（自动填写为gogrpc）  
  
service Greeter {  
  rpc SayHello(Hreq) returns (Hresp);  
}  
  
message Hreq {  
  string name = 1;  
}  
  
message Hresp {  
  string msg = 1;  
}  
```
3. 生成 go 语言的 pb 文件，格式为 .pb.go
在 gogrpc 目录下执行命令：
```bash
protoc -I . --go_out=plugins=grpc:.. ./*.proto
```
其中 `I` 后面是输入文件目录，`go_out` 后面是输出的包，`./*.proto` 表示当前目录下所有的 proto 文件