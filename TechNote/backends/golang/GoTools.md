1. golangci-lint: 搭配 goland 的 go-linter 插件使用，写出符合 google style 的代码
2. go vet ./...: 检查常见错误，如闭包中使用函数循环变量，deadlock 等
3. go tool compile
4. go tool objdump
5. go tool link
6. go tool pprof
7. go tool trace
8. go build
	8.1 go build --race: 可以检测出数据竞争
9. godoc --http=6060: go 文档工具