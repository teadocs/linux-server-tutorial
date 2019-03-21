# Redis

Redis是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。

Redis是一个key-value存储系统。和Memcached类似，它支持存储的value类型相对更多，包括string(字符串)、list(链表)、set(集合)、zset(sorted set --有序集合)和hash（哈希类型）。这些数据类型都支持push/pop、add/remove及取交集并集和差集及更丰富的操作，而且这些操作都是原子性的。在此基础上，redis支持各种不同方式的排序。与memcached一样，为了保证效率，数据都是缓存在内存中。区别的是redis会周期性的把更新的数据写入磁盘或者把修改操作写入追加的记录文件，并且在此基础上实现了master-slave(主从)同步。

## Redis Docker 镜像安装

Redis 提供官方镜像，下载安装镜像方法如下：

```
$ docker pull redis
```

以上命令为安装 Redis 最新版本的镜像。

国内镜像安装方法

```
$ docker pull registry.docker-cn.com/library/redis
```

## 启动 Redis

```
$ docker run -d -p 6379:6379 --name myredis redis
```

## 查看 Redis 

```
$ docker ps
```
