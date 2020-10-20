---
title: Mac安装Redis5.0.8
date: 2020-05-16 12:38:27
categories:
tags:
---

在用SpeingBoot做邮箱验证的时候，需要用到`Redis`，所以在Mac和CentOs中都安装了`redis5.0.8`：

<!-- more -->

#### 1. 下载

redis[下载地址](https://redis.io )，选择download，然后可以看到5.0.8的安装包：

![Screen Shot 2020-05-16 at 12.49.14](http://gray.oss-cn-beijing.aliyuncs.com/2020-05-16-045020.png)

或者，可以通过wget安装`wget http://download.redis.io/releases/redis-5.0.8.tar.gz`

#### 2. 安装

- 解压到安装目录`tar zxvf redis-5.0.8.tar.gz /usr/local`

  > 注意，如果没有权限请加上sudo

- 切换到解压好的目录`cd /usr/local/redis-5.0.8`，执行make命令，大概两分钟后安装完成

- 执行`make install`，作用是在`/usr/local/bi`n里产生一些文件(命令)，比如`redis-server`、`redis-cli`等，如果不执行make install，那么键入启动服务命令redis-server时会提示“该命令不存在”，redis服务就无法启动。我们查看一下：

  ![image-20200516125715391](http://gray.oss-cn-beijing.aliyuncs.com/2020-05-16-045716.png)

#### 3. 修改配置文件redis.conf

修改redis.conf，将GENERAL里的no改成yes（默认redis.conf里守护进程没有被开启）

(注：这个配置文件可能在 /usr/redis/redis-5.0.8/redis.conf，或者/etc/redis.conf)

![image-20200516125936103](http://gray.oss-cn-beijing.aliyuncs.com/2020-05-16-045936.png)

#### 4. 启动服务

执行`to redis-server /usr/local/redis-5.0.8/redis.conf`加载配置文件，可以在bash配置文件里重命名一下，`alias redis='redis-server /usr/local/redis-5.0.8/redis.conf'`，查看结果：配置文件已经加载；

![image-20200516130301891](http://gray.oss-cn-beijing.aliyuncs.com/2020-05-16-050301.png)

加载配置文件后，启动客户端`redis-cli` 

退出的话先执行shutdown再exit即可

#### 5. /uer/local权限问题

默认安装以后，在Mac系统中就算是sudo用户也没有访问redis权限，退出的时候提示没有权限保存`saving: Permission denied`，手动修改一下文件夹权限`sudo chown -R $(whoami) /usr/local/redis-5.0.8`，👌