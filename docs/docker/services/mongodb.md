# MongoDB

MongoDB 是一款较为常用的NOSQL 数据库，结合 Docker 使用，能实现轻松配置部署、迁移，本文以下为简要介绍如何在 Docker 中部署并使用 MongoDB。下文主要分为几个部分，内容如下：

MongoDB 镜像安装
MongoDB 容器创建
MongoDB 容器数据目录挂载
MongoDB 数据迁移
MongoDB 常用 Docker 命令

## MongoDB Docker 镜像安装

MongoDB 提供官方镜像，下载安装镜像方法如下：

```
$ docker pull mongo
```

以上命令为安装 MongoDB 最新版本的镜像。

## MongoDB Docker 容器创建

MongoDB Docker 容器创建有以下几个问题：
1. MongoDB 容器基本创建方法和数据目录挂载
2. MongoDB 容器的数据迁移
3. MongoDB 设置登录权限问题

## MongoDB 容器基本创建方法和数据目录挂载

MongoDB 容器基本创建命令如下：

```
$ docker run -p 27017:27017 -v <LocalDirectoryPath>:/data/db --name docker_mongodb -d mongo
```

在上面的命令中，几个命令参数的详细解释如下：

- ``-p`` 指定容器的端口映射，mongodb 默认端口为 27017
- ``-v`` 为设置容器的挂载目录，这里是将<LocalDirectoryPath>即本机中的目录挂载到容器中的/data/db中，作为 mongodb 的存储目录
- ``--name`` 为设置该容器的名称
- ``-d`` 设置容器以守护进程方式运行

## 容器数据迁移

接下来，我们先停止刚才创建的 docker_mongodb 容器，命令如下：

```
$ docker stop docker_mongodb
```

然后我们再创建一个新的 MongoDB 容器，挂载刚才刚刚的数据目录，命令如下：

```
$ docker run -p 27017:27017 -v <LocalDirectoryPath>:/data/db --name docker_mongodb_migration -d mongo
```

我们可以容器查询命令，查看当前 Docker 的容器状态，命令如下：

```
$ docker container ls -a
```

这里的 ``-a`` 参数是查看所有的容器，包括已经停止的容器。

## 用 Docker Compose 快速搭建mongo+管理系统

新建一个 ``stack.yml`` 文件，内容如下：

```
version: '3.1'

services:

  mongo:
    image: mongo
    ports:
      - 27017:27017
    restart: always
    environment:
      MONGO_INITDB_ROOT_USERNAME: mongoadmin
      MONGO_INITDB_ROOT_PASSWORD: mongoadmin

  mongo-express:
    links:
      - mongo
    image: mongo-express
    restart: always
    ports:
      - 8081:8081
    environment:
      ME_CONFIG_OPTIONS_EDITORTHEME: 3024-night
      ME_CONFIG_BASICAUTH_USERNAME: mongoexpress
      ME_CONFIG_BASICAUTH_PASSWORD: mongoexpress
      ME_CONFIG_MONGODB_ADMINUSERNAME: mongoadmin
      ME_CONFIG_MONGODB_ADMINPASSWORD: mongoadmin
```

启动：

```
$ docker-compose -f stack.yml up
```
