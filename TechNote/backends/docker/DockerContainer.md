# 重启容器
```bash
docker restart $docker_id
```

# 启动容器
```bash
docker start $docker_id
```

# 暂停容器
```bash
docker stop $docker_id
```

# 删除容器
```bash
docker rm $docker_id
```

# 防止容器直接退出
```bash
docker run --name "test" --network=host -itd test:v2
```
## 参数解释
> -p 绑定端口
> -t 启用伪终端
> -d 后台运行
> -i 起来后返回docker id

# 观察容器