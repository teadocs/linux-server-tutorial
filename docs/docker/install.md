# docker安装

## Mac

mac安装程序下载链接 

1. [Stable](https://download.docker.com/mac/stable/Docker.dmg)
2. [Edge](https://download.docker.com/mac/edge/Docker.dmg) 版本的 Docker for Mac。

如同 macOS 其它软件一样，安装也非常简单，双击下载的 .dmg 文件，然后将鲸鱼图标拖拽到 Application 文件夹即可。

![mac 1](/static/images/docker_install_mac_1.png)

从应用中找到 Docker 图标并点击运行。可能会询问 macOS 的登陆密码，输入即可。

![mac 2](/static/images/docker_install_mac_2.png)

点击顶部状态栏中的鲸鱼图标会弹出操作菜单。

![mac 3](/static/images/docker_install_mac_3.png)

![mac 4](/static/images/docker_install_mac_4.png)

第一次点击图标，可能会看到这个安装成功的界面，点击 "Got it!" 可以关闭这个窗口。

![mac 5](/static/images/docker_install_mac_5.png)

启动终端后，通过命令可以检查安装后的 Docker 版本。

```bash
$ docker --version
Docker version 17.09.1-ce, build 19e2cf6
```

### 镜像加速

鉴于国内网络问题，后续拉取 Docker 镜像十分缓慢，我们可以需要配置加速器来解决，我使用的是网易的镜像地址：http://hub-mirror.c.163.com。

在任务栏点击 Docker for mac 应用图标 -> Perferences... -> Daemon -> Registry mirrors。在列表中填写加速器地址即可。修改完成之后，点击 Apply & Restart 按钮，Docker 就会重启并应用配置的镜像地址了。

![mac 6](/static/images/docker_install_mac_6.png)

之后我们可以通过 docker info 来查看是否配置成功。

```bash
$ docker info
...
Registry Mirrors:
 http://hub-mirror.c.163.com
Live Restore Enabled: false
```

参考文章[MacOS Docker 安装 | 菜鸟教程](http://www.runoob.com/docker/macos-docker-install.html)

## Centos7

Docker从1.13版本之后采用时间线的方式作为版本号，分为社区版CE和企业版EE。

社区版是免费提供给个人开发者和小型团体使用的，企业版会提供额外的收费服务，比如经过官方测试认证过的基础设施、容器、插件等。

社区版按照stable和edge两种方式发布，每个季度更新stable版本，如17.06，17.09；每个月份更新edge版本，如17.09，17.10。

### 安装docker

1、Docker 要求 CentOS 系统的内核版本高于 3.10 ，查看本页面的前提条件来验证你的CentOS 版本是否支持 Docker 。

通过 **uname -r** 命令查看你当前的内核版本

```bash
$ uname -r
```

2、使用 root 权限登录 Centos。确保 yum 包更新到最新。

```bash
$ sudo yum update
```

3、卸载旧版本(如果安装过旧版本的话)

```bash
$ sudo yum remove docker  docker-common docker-selinux docker-engine
```

4、安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的

```bash
$ sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

5、设置yum源

```bash
$ sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

6、可以查看所有仓库中所有docker版本，并选择特定版本安装

```bash
$ yum list docker-ce --showduplicates | sort -r
```

7、安装docker

```bash
$ sudo yum install docker-ce  #由于repo中默认只开启stable仓库，故这里安装的是最新稳定版17.12.0
$ sudo yum install <FQPN>  # 例如：sudo yum install docker-ce-17.12.0.ce
```

8、启动并加入开机启动

```bash
$ sudo systemctl start docker
$ sudo systemctl enable docker
```

9、验证安装是否成功(有client和service两部分表示docker安装启动都成功了)

```bash
$ docker version
```

## Window

