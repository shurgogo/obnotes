# 拉取镜像
```bash
docker pull hello-world
```

# 镜像转化为 tar
```
docker save -o hello-world > hello-world.tar
```
or
```
docker save hello-world > hello-world.tar
```

# 构建基础镜像
```
docker load -i hello-world.tar
```
or
```
docker load < hello-world.tar
```

# 构建普通镜像
```
docker build -t test:v1 .
```
注意最后的`.`

# 显示已有镜像
```bash
docker images
```

# 删除镜像
```bash
docker image rm $image_name:version
```
