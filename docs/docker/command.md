# docker常用命令

```
#查看当前docker版本
docker -v
#查看当前本地所有镜像
docker images
#构造镜像,用法docker build -t 镜像名称 .
docker build -t docker_demo .
#用于容器与主机之间的数据拷贝。用法docker cp 主机文件地址 容器内地址。12d7f14v45cv为容器id。
docker cp /www/runoob 12d7f14v45cv:/www/
#创建一个新的容器并运行，-d为后台执行，-p 9000:3000前面为主机端口，后面是容器端口。docker_demo镜像名
docker run -d -p 9000:3000 docker_demo
#启动已被停止的容器
docker start docker_demo
#关闭已被启动的容器
docker stop docker_demo
#重新启动容器
docker restart docker_demo
#杀掉一个运行中的容器。
docker kill -s KILL docker_demo
#删除一个或多少容器。-f :通过SIGKILL信号强制删除一个运行中的容器-l :移除容器间的网络连接，而非容器本身-v :-v 删除与容器关联的卷
docker rm -f docker_demo、docker_demo1
#在运行的容器中执行命令。104e28f2f072容器id
sudo docker exec -it 104e28f2f072 /bin/bash 
#列出容器。 -a:所有容器包含没有运行的
docker ps 
#获取容器获取容器的日志 104e28f2f072容器id，-t:显示时间戳
docker logs -f -t 104e28f2f072 
#登陆镜像仓库
docker login
#获取镜像
docker pull 
#上传镜像
docker push
#查看指定镜像的创建历史。
docker history docker_demo
```