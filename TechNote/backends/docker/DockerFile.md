# 基本结构
```bash
# 暴露端口 8888
EXPOSE 8888
# 拷贝文件，src是相对(dockerfile)路径，dest是(inside docker)绝对路径
COPY <src> <dest>
# RUN是在构建镜像时执行
RUN install.sh
# CMD是在容器启动时执行
CMD [myserv]
```

## ADD 和 COPY 的区别和使用场景
- ADD 支持添加远程 url 和自动提取压缩格式的文件，COPY 只允许从本机中复制文件
- COPY 支持从其他构建阶段中复制源文件（--from）
- 根据官方 Dockerfile 最佳实践，除非真的需要从远程 url 添加文件或者自动提取压缩文件才用 ADD，其他情况一律使用 COPY
**注意**
- ADD 从 url 获取文件和复制的效果不理想，因为该文件会增加 Docker Image 最终大小
- 相反，应该使用 curl 或 wget 来获取远程文件，并在不需要时删除