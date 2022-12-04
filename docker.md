# docker

## install

1. uninstall old versions

```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```

2. install by scripts

```sh
curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

## image

1. 拉取镜像，[docker hub](https://hub.docker.com/search?q=&type=image)上面有很多现成的镜像可以用

```sh
docker pull [选项] [Docker Registry 地址[:端口号]/]仓库名[:标签]
# 举例: 拉取arch linux
docker pull archlinux:latest
# 举例: 拉取ubuntu
docker pull ubuntu:latest
```

2. 列出镜像

```sh
docker image ls
# 或
docker images
```

3. 删除镜像

```sh
docker image rm [选项] <镜像1> [<镜像2> ...]
# 或
docker rmi IMAGE_NAME:TAG
```

4. 创建新的镜像

```sh
docker [container] commit CONTAINER IMAGE_NAME:TAG
# 举例: 保存当前叫做webserver的容器到新的镜像nginx:v2
docker commit webserver nginx:v2
```

5. 保存镜像到本地文件

```sh
docker save -o IMAGE_NAME.tar IMAGE_NAME:TAG
```

6. 从本地文件导出镜像

```
docker load -i IMAGE_NAME.tar
```

## container

1. 新建并启动

```sh
# 输出一个 "Hello World"，之后终止容器
docker run ubuntu:18.04 /bin/echo 'Hello world'
# 启动一个 bash 终端，允许用户进行交互
docker run -t -i ubuntu:18.04 /bin/bash
# -t 选项让Docker分配一个伪终端（pseudo-tty）并绑定到容器的标准输入上
# -i 则让容器的标准输入保持打开
```

2. 启动终止的容器

```sh
docker start CONTAINER
```

3. 停止容器

```sh
docker stop CONTAINER
```

4. 重启容器

```sh
docker restart CONTAINER
```

5. 进入容器

```sh
docker attach CONTAINER
```

6. 删除容器

```sh
docker rm CONTAINER
```

7. 容器重命名

```sh
docker rename CONTAINER1 CONTAINER2
```

8. 容器限制修改

```sh
docker update CONTAINER --memory 500MB
```

9. 本地文件和容器互传
```sh
docker cp xxx CONTAINER:xxx
docker cp CONTAINER:xxx xxx
```

10. 查看某个容器中的所有进程
```sh
docker top CONTAINER
```

11. 导出容器到本地文件

```sh
docker export CONTAINER_ID > IMAGE_NAME.tar
```

12. 导入容器快照
```sh
# 和load区别在于使用import会丢弃所有历史记录和元数据信息
docker import IMAGE_NAME.tar
```

13. 挂起当前容器

```sh
# 在容器内
ctrl + p; ctrl + q
```

14. 创建容器时指定ip映射

```sh
# 指定容器的80端口映射到宿主机器的8000端口
docker run -p 8000:80 -it ubuntu /bin/bash
# 将容器的ip192.168.0.100和80端口，映射到宿主机的8000端口
docker run -p 192.168.0.100:8000:80 -it ubuntu /bin/bash
```

15. 查看端口映射
```sh
docker port container_ID
```


## Dockerfile 定制镜像

> 在空白目录中创建文本文件，命名为 Dockerfile:

```sh
mkdir  my_image
cd my_image
touch Dockerfile
```

> Dockerfile 中只有两种命令 FROM [基础镜像] 以及 RUN + shell 命令

> 构建镜像

```sh
docker build -t [image-name]:[version] <路径>
```