---
title: 解决Mac中Terminal无法访问github
date: 2020-07-18 14:33:04
categories: 问题
tags: Mac
---
 
 在Terminal中，`git clone` 和 `git push`无法使用，ping了一下github，发现连接不通，但是Chrome中却能打开，在此记录一下解决的办法。
 <!-- more -->
### 通过ping命令查看当前的github的ip地址
 ![](http://gray.oss-cn-beijing.aliyuncs.com/2020/07/18/15950551780422.jpg?image/auto-orient,1/resize,p_89/quality,q_90)

 如图： 可以看到地址为13.250.177.223，这是ping不通的
### 查看自己的hosts文件
通过`cat /etc/hosts`命令查看host文件，查找是否有github相关的映射，比如我的映射关系就是13.250.177.223，如果没有，看下一步。
### 获取github的ip地址
在[IPAdress](https://www.ipaddress.com)网站上，输入github.com查询ip地址，可以看到，当前最新的ip地址是140.82.113.4，记录这个ip地址。
![](http://gray.oss-cn-beijing.aliyuncs.com/2020/07/18/15950555144253.jpg?image/auto-orient,1/resize,p_89/quality,q_90)
### 修改hosts文件
terminal打开命令：`sudo vi /etc/hosts`，输入密码，选择“e(edit anyway)”,然后添加记录：（此处涉及到vi编辑器的用法，不会用的自行百度or谷歌）
```bash
# github
 140.82.113.4 www.github.com
```
最后保存并退出，修改hosts文件保存后我自动刷新DNS，再ping就没问题啦！
![](http://gray.oss-cn-beijing.aliyuncs.com/2020/07/18/15950558068128.jpg?image/auto-orient,1/resize,p_89/quality,q_90)
可以看到连接不怎么稳定，此时就需要小飞机来帮忙了。
### 配置代理提高速度
因为如果挂了全局代理，这样如果需要克隆coding之类的国内仓库，会奇慢无比所以我建议使用这条命令，只对github进行代理，对国内的仓库不影响
```bash
git config --global http.https://github.com.proxy https://127.0.0.1:1080
git config --global https.https://github.com.proxy https://127.0.0.1:1080
```
同时，如果在输入这条命令之前，已经输入全局代理的话，可以输入进行取消
```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```
其中端口在小飞机的设置里查看，比如当前我的代理端口就是1087
![](http://gray.oss-cn-beijing.aliyuncs.com/2020/07/18/15950560453819.jpg?image/auto-orient,1/resize,p_89/quality,q_90)
注意：这歌方法仅限于https协议下载，对于SSH协议是无效的。