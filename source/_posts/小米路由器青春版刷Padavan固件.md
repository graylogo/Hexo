---
title: 小米路由器青春版刷Padavan固件
date: 2019-01-26 22:59:05
categories:
tags: 路由器
---
>刷机是一种乐趣，大学宿舍晚上断电，正好手上有一个**小米路由器青春版**，USB充电宝供电，巴掌大小，放在宿舍简直合适不过了。最最最厉害的是可以刷潘多拉固件，简直不要太好！
>（这篇文章是以前Wordpress上写的，后来荒废了，但是这篇文章留在了MWeb的文件夹里，**感谢MarkDown！**）
<!-- more -->


## 准备：
* 小米路由器青春版 *1
* 网线 *1
* 电脑(Mac 或 Windows) *1
* 刷机所需的固件，软件（Putty和WINSCP自行百度下载）

****

## 基本思路：
>1. 首先确保路由器ROM版本为2.0，如果不是，降级到2.0或刷入开发版miwifi_r1cl_all_59371_2.1.26.bin版本([点击下载](http://bigota.miwifi.com/xiaoqiang/rom/r1cl/miwifi_r1cl_all_59371_2.1.26.bin)这个开发版）

>2. 修改网页地址的方式来篡改web管理密码和root密码

>3. 使用telnet命令进去备份各个分区(非必须)

>4. 刷入breed

>5. 刷入固件（潘多拉或梅林）

## 步骤：
1. 小米路由器青春版是没有官方通道开启ssh的，其它版本路由器可以在[miwifi开放平台](http://www1.miwifi.com/miwifi_open.html)查看。
在网友的帖子里，我们可以直接修改路由器的请求地址的特定参数，改变系统参数，从而开启ssh。
> 首先确保路由器ROM版本为2.0，如果不是，降级到2.0或刷入开发版miwifi_r1cl_all_59371_2.1.26.bin版本([点击下载](http://bigota.miwifi.com/xiaoqiang/rom/r1cl/miwifi_r1cl_all_59371_2.1.26.bin)这个开发版）
>降级方法：由官方的路由管理界面，上传本ROM包，自动升级即可

2. 在浏览器地址栏输入192.168.31.1，输入管理员密码（如果忘记了的话按住路由器的reset键10s以上重置系统，设置账户密码再做上面的操作），地址栏会多出一部分参数，比如我的是：
```
http://192.168.31.1/cgi-bin/luci/;stok=6bb3936a88b4df625ded00d17be3911a/web/home#router
```
3. 更改管理员密码和root密码
将上面的地址中的 **/web/home#router** 改为 **/api/xqsystem/set_name_password?oldPwd=旧密码&newPwd=新密码**  ，然后确定，看网页的返回值，如果是**{"code":0}**就表示修改成功，可以接着下一步。

4. 把 **/web/home#router** 改为 **/api/xqnetwork/set_wifi_ap?ssid=xiaomi&encryption=NONE&enctype=NONE&channel=1%3B%2Fusr%2Fsbin%2Ftelnetd** ，然后查看返回的JSON数据 **{"msg":"未能连接到指定WiFi(Probe timeout)","code":1616}** ，就可以用telnet方式登录路由器。

5. 用telnet方式登录路由器
下载一个Putty 。然后打开选填以下参数，连接类型：telnet;主机名称：192.168.31.1.点击连接。可以看到看到login，账户输入root，密码则为以上第二步中修改的新密码。然后依次执行下面的三条指令：
```
	sed -i ":x;N;s/if \[.*\; then\n.*return 0\n.*fi/#tb/;b x" /etc/init.d/dropbear 
    /etc/init.d/dropbear start 
    nvram set ssh_en=1; nvram commit  
```
此时我们已经开放ssh，可以用ssh方式登录路由器了。

6. 刷入breed
WINSCP 选择SCP协议 复制breed.bin 到/tmp
输入以下命令刷入，刷入后，机器会自动重启：
```
    mtd -r write /tmp/breed.bin Bootloader
```
7. 进入breed控制台
先给路由器断电，再按住路由器reset键，再给路由器送电，等到路由器灯闪的时候，松开reset键，用一根网线将路由器的WAN口和电脑相连，在电脑上在浏览器中输入192.168.1.1，进入breed控制台了。

8. 刷入固件
可供选择的固件还是很多的，在这里我找了一个[padavan](http://www.right.com.cn/forum/thread-161324-1-1.html),这固件是从Padavan固件源码搬运源码汉化后编译出来的。选择[MI-NANO_3.4.3.9-099.trx](http://opt.cn2qq.com/padavan/)这个版本，青春版专供直接在控制台选择上固件，然后点击更新，等待路由器自动重启，万事大吉！

9. 修改灯光颜色
开机灯颜色蓝色橙色混合
使用下面的命令关闭橙色灯变成纯正蓝色
```
    mtk_gpio -d 44 0
```
10. 管理路由器
刷入成功后，默认创建了名字为PCDN的无线网络，默认的密码为1234567890
后台网址为192.168.123.1，账号密码都为admin。（登录后可自行修改）
另外，可以配置ss，开启广告屏蔽插件等操做。

参考文章：
[小米路由器青春版刷Padavan固件](https://blog.csdn.net/qq_29109181/article/details/77727328)
[小米路由器青春版刷潘多拉、华硕固件](https://blog.csdn.net/qq_19666821/article/details/69948930)
[小米路由器青春版开启SSH刷入Padavan固件](https://www.b612.me/code/80.html)
[小米路由器青春版刷Padavan以及修改灯光颜色](http://right.com.cn/forum/thread-196864-1-1.html)


