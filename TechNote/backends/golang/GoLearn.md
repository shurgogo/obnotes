# 类型

## 引用类型
- slice
```go
s2 := s1[2:3:3]
```
定义 s2 长度为 j-i=3-2=1, 定义容量为 k-i=3-2=1, 当 s2 增长时，会生成新切片，可以防止老切片被修改
- map
- channel
- interface
- fucntion

## 结构类型
这个 File 类型的本质时非原始（基础类型）的，这个类型的值实际上不能安全复制，对内部未公开的类型的注释，解释了不安全的原因。
因为没有方法阻止程序员进行复制，所以 File 类型的实现使用了一个嵌入的指针，指向一个未公开的类型，正是这层额外的内嵌类型阻止了复制。不是所有的结构类型都需要或者应该实现类似的额外保护。**程序员需要能识别出每个类型的本质，并使用这个本质来决定如何组织类型**。
因为 File 类型的值具备非原始的本质，所以总是应该被共享，而不是被复制。
```go
// File represents an open file descriptor.
type File struct {  
   *file // os specific  
}
// file is the real representation of *File.  
// The extra level of indirection ensures that no clients of os  
// can overwrite this data, which could cause the finalizer  
// to close the wrong file descriptor.
type file struct {  
   pfd         poll.FD  
   name        string  
   dirinfo     *dirInfo // nil unless directory being read  
   nonblock    bool     // whether we set nonblocking mode  
   stdoutOrErr bool     // whether this is stdout or stderr  
   appendMode  bool     // whether file is opened for appending}
```

# 序列化和反序列化
## json.Decoder 和 json.Unmarshall 的区别
- 当数据来源为 stream，使用json.Decoder。例如打开一个大文件，需要逐行读取；或者从 http 的 response 中读取数据时，用 json.Decoder流式解析。
```go
file, _ := os.Open(filePath)
_ := json.NewDecoder(file).Decode(&entity)
```

- 当数据来源已经保存在 memory 中时，用json.Unmarshall。例如已经将小文件的内容全部保存至某个变量后，直接用 json.Unmarshall 解析。
```go
content, _ := ioutil.ReadAll(filePath)
_ := json.Unmarshall(&entity, content)
```
