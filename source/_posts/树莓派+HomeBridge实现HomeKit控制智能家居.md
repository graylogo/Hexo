---
title: 树莓派+HomeBridge实现HomeKit控制智能家居
date: 2019-09-25 18:41:45
categories:
tags: 树莓派
---
米家app发展的很快，短短几年，已经日趋完善，得益于其高性价比，用户也越来越多，反观HomeKit在国内的表现，也仅仅是同“**电视.app**“一样，躺在每个ios用户的手机里。后来，在GitHub上开源了一个[HomeBridge](https://github.com/nfarina/homebridge)项目，通过树莓派做桥接，实现Siri控制米家智能设备。
<!-- more -->
##一、需要准备的东西
* 支持 iOS10 的苹果设备（ iPhone 5 以上、 iPad mini 2 以上、 iPod 第六代以上）

* 小米多功能网关**二代**（ 注意：一定要二代！）

* 任意一个或多个支持 HomeKit 的设备：小米智能插座 ZigBee 版、小米人体传感器、小米门窗传感器、小米温湿度传感器、Yeelight智能灯泡、 Aqara墙壁开关等
* 树莓派 Raspberry Pi 3B+ （包含读卡器 & 8 Gb 以上 TF 内存卡一张）
* Mac Book一台（当然，win也可以） <br>
![树莓派](http://gray.oss-cn-beijing.aliyuncs.com/2019/09/25/4518047ab0da64eede17368.gif?image/auto-orient,1/resize,p_89/quality,q_90)<center>树莓派3B+</center>

##二、GitHub项目地址
* [HomeBridge](https://github.com/nfarina/homebridge)
* [homebridge-mi-aqara](https://github.com/YinHangCode/homebridge-mi-aqara)

##三、开始吧
1. 关于树莓派的安装和打开ssh可以先移步[系统烧录](https://blog.csdn.net/u012313335/article/details/53405734)和[打开ssh](https://blog.csdn.net/u012313335/article/details/73920256)；
2. 跟新gcc（可以使用pi用户也可以使用root用户，使用pi用户涉及权限问题请加sudo）<br>
``
sudo apt-get install gcc
``
1. 接下来依次安装，如果你发现速度很慢，你可能需要更改中国软件源，参考文章：Raspbian [中国软件源](http://shumeipai.nxez.com/2013/08/31/raspbian-chinese-software-source.html),阿里云各个地方速度都不错。
<br>**a. 安装nodejs：**<br>
`sudo apt-get update`
`curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`
`sudo apt-get install -y nodejs`
`sudo apt-get install -y build-essential`
<br>**b. 安装avahi：**<br>
`sudo apt-get install libavahi-compat-libdnssd-dev`
<br>**c. 安装HomeBridge：**<br>
`sudo npm install -g --unsafe-perm homebridge`
<br>**d. 安装homebridge-aqara：**<br>
`sudo npm install -g homebridge-aqara`
<br>安装部分完成！
1. 新建和配置config.json文件
返回主目录→创建" .homebridge "文件夹→进入" config.json "文件）
```
cd ~ 
mkdir .homebridge
vim .homebridge/config.json
```
    <br>复制以下代码稍作修改：
```
{

    "bridge": {

        "name": "Homebridge",

        "username": "CC:22:3D:E3:CE:30",

        "port": 51826,

        "pin": "031-45-154"

    }, 

    "platforms": [{

        "platform": "AqaraPlatform",

        "sid": ["【（密码A）网关MAC地址，去掉冒号，全部小写】"],

        "password": ["【（密码B）网关局域网密码】"]

    }]
}
```
<br>其中 name 是你在 iOS 家庭 App 上可以看到的桥接器的名字，建议就叫 Homebridge，username 需要是类似 MAC 的格式，是可以随意填写，只要符合格式，建议不需要更改了。port 随意，确保不要被占用。pin 随意，为密码，需要是 8 位数字，格式为 xxx-xx-xxx，比如 123-45-678。下面的 platform 也是无所谓修改不修改，关键是**sid**和**password**，这就需要在手机上操作了。
在手机上打开米家 App，点击你的网关，右上角三个 ···，并狂按底部空白区域，直到出现局域网通信协议和网管信息为止。
![](http://gray.oss-cn-beijing.aliyuncs.com/2019-09-25%2F1569411561.png)
点击局域网通信协议，打开，并刷新一个密码，改为全部小写，（安卓手机刷出来是小写），记录这段文字（密码 A ）。<br>
点击网关信息，找到 mac: 后的文字，如本截图中的 28:6C:07:85:B3:0E，去掉 : 并全部改为小写，也记录这段文字（密码 B ），如本截图中的文字处理后的结果就是 f0b429cc6168。
![](http://gray.oss-cn-beijing.aliyuncs.com/2019/09/25/15694117001892.jpg?image/auto-orient,1/resize,p_89/quality,q_90)
第一个密码 A 就是你的 sid，第二个密码 B 就是 password。如果你有多个网关用逗号链接，比如 cb30a01c1bcc4b3c, dc41b12d2cdd5c4d, password 同理。在刚刚树莓派编辑的 config.json 输入上面获得的密码，保存退出。（vim的使用自行Google）
1. 运行homebridge
直接在命令行输入`homebridge`就能运行；有时出现错误会自动关闭，错误原因有很多，一般就是端口占用，或者mac地址和密码填写错误，仔细检查，如果不行的话，清除缓存，删除连接信息重新运行homebridge： 
**操作方法**
a. 结束HomeBridge进程，如下：
`pkill -9 homebridge`
b. 进入config.json所在的文件夹，例如：
`cd /root/.homebridge`
c. 删除文件夹下persist文件夹，例如：
`rm -rf persist`
d. 重启Homebridge进程，例如：
`homebridge`
掏出iPhone，打开家庭app，点击添加配件，扫描二维码或者手动输入你设置的八位密码就可以配对成功，操作完成。
1. 最后的最后，你会发现，HomeBridge 停止运行了。我们不可能在电脑上挂着终端使树莓派一直运行这个服务，因此还有最后一步，把 HomeBridge 服务加入到树莓派的系统服务里。事实上, 树莓派文档 Scheduling tasks with Cron 给出的方法是最简单并且方便以后配置别的程序。
先安装 cron
`sudo apt-get install gnome-schedule`
然后配置 cron.
`crontab -e`
在最下方添加` @reboot homebridge & `即可完成开机启动 homebridge 的配置。
现在，你可以重启一下树莓派，运行`ps -ef | grep homebridge`看看 HomeBridge 服务是否正常运行.

最后来感叹一下apple的生态系统，当我成功配置后，我能够在iPhone、ipad、mac、甚至是Apple Watch上控制小米家居，实在激动。

**注意**：树莓派必须通过网线连接，不能通过Wi-Fi连接！

## 参考：
[树莓派进阶（一）：借助树莓派与 HomeBridge，从米家到 HomeKit](https://www.jianshu.com/p/ec79b2711bd5)
[从米家到 HomeKit，你只需要一个树莓派](https://sspai.com/post/38358)
[HomeBridge教程 ](https://homekit.loli.ren/docs/show/3)

