# php-docker

## 简介

docker版的lnmp环境

开发通常需要在本地进行开发，而为了跟测试环境保持一致，如果单独部署服务，需要部署nginx,php-fpm等，php-docker就是为了解决这个问题，只需简单配置即可完成nginx,php-fpm,redis,mysql等部署

都改为了使用国内镜像

用 Docker 容器服务的方式搭建环境，易于维护、升级。使用前需了解 Docker 的基本概念，常用基本命令

使用前需了解 Docker 的基本概念，常用基本命令

相关软件版本：

- PHP 7.0/7.3
- MySQL 5.7
- Nginx 1.12
- Redis 3.2

已经有的 PHP 拓展

- redis 3.1.4
- mongodb 1.5.3
更多拓展可以自己修改Dockfile

## 使用

### 1.安装 Docker，Docker-compose  

- Docker，详见官方文档：<https://docs.docker.com/engine/installation/linux/docker-ce/centos/>
- docker-compose，文档：<https://docs.docker.com/compose/install/>

记得修改配置docker镜像地址为国内镜像

### 2. clone项目到本地

### 3. 修改配置文件

将files文件夹中的.env.example复制一份为.env，修改HOST_APP_CODE_PATH配置为本地代码目录，这样会将本地目录挂载到容器中，这样容器可以访问本地文件

如果HOST_APP_CODE_PATH对应的目录不在docker的file sharing中，需要将目录配置到docker中，文档：<https://docs.docker.com/docker-for-mac/#file-sharing>

### 4.docker-compose 构建项目

进入 docker-compose.yml 所在目录：
执行命令：

```
docker-compose up
```

如果没问题，下次启动时可以以守护模式启用，所有容器将后台运行：  

```
docker-compose up -d
```

使用 docker-compose 基本上就这么简单，Docker 就跑起来了，用 stop，start 关闭开启容器服务。  
更多的是在于编写 dockerfile 和 docker-compose.yml 文件。

可以这样关闭容器并删除服务：

```
docker-compose down
```

## 项目结构

- data
    用了保存mysql和reids的数据文件
- files
    docker环境的配置文件
- logs
    运行的日志文件

## 怎么运行php cli命令

需要进入到镜像中去执行php cli命令
查看docker进程

```
docker ps
```

找到对应的容器id，比如：de814907a269，进入容器

```
docker exec -it de814907a269 /bin/bash
```

这样就类似进入了一个linux系统，可以执行命令
