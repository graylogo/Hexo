---
title: 通过Hexo + Github 搭建博客
date: 2019-05-25 13:30:06
categories: 思考
tags: 感悟
---
>最近学习压力很大，想起了这个被搁置一年的博客计划，正好看到了Hexo搭建的[萤火之森](http://frankorz.com/archives/)页面，真的很漂亮，于是决定动手自己搭建一个。这篇文章正好记录一下搭建过程中遇到的问题，方便以后学习。
> 
<!-- more -->
## hexo 基础命令

```bash
hexo g == hexo generate  生成
hexo d == hexo deploy 部署
hexo s == hexo server
hexo n == hexo new
```
## 遇到的问题
### 1. Github密匙只读

### 2. hexo s 显示4000端口不能用
解决方法：在Blog的根目录下，修改_config.ynl文件，在最后加上：
```c
server:
    port: 4001  #注意port前有Tab键 冒号后有空格
    compress: true
    header: true
```

## 花费的时间
总的算下来，总共花了我四个小时左右的时间来搭建这个博客，当然，这仅仅是搭建了基础的框架，后期还需要大量的时间来美化，不过鉴于最近考试太忙，估计得延期一段时间了。

## 为什么要需要这个博客？
一年前，我用阿里云镜像一键搭建了基于Wordpress的个人博客，但是由于拖更，导致兴趣越来越少，最后也就不了了之了。从这段历程中，我感受到了，不是自己努力来的结果自己真是不懂得珍惜，这一个花费我一晚上心血建立的Blog，我可要好好监督自己，不要荒废了。
其实，挺羡慕那些能在各种论坛分享自己知识的人，帮助别人的同时也能留下自己的足迹，最重要的是，在这个过程中，能找到归属感与成就感，这就是分享的意义吧。
很大一部分人，写的都是技术博客，但是我知道自己现在能力有限，输出不了太多的干货，所以，现在这个阶段，更多的是记录一些学习笔记，当然，我也想穿插一些自己的心里话，写一下每个阶段的感悟。
## 搭建过程让我学到了什么
搭建过程虽然烦琐，但我确乐在其中，兴趣是最好的老师，在搭建过程中，我看到了很多感兴趣的技术，比如GitHub的代码托管（很早以前我就注册了GitHub账号，但是一直没有项目来练习），比如Node.js，看到漂亮的网页，不眠不免对前端心生向往，再比如最近一直在学习的Linux命令行，现我已经迫不及待想要用shell自己写一个一键部署脚本了。
## 给自己立下Flag
我的脑海里会迸发出很多新计划，但是最后很多都是不了了之，因为没有去实现，所以，在这里，我要给自己定几个目标：
1. 每个月至少来更新一篇博客，不管是什么类型的。
2. 尽快掌握MarkDown与法，写出排版漂亮的文章。
3. 将我的小站好好维护下去，做一些优化。
4. 开始GitHub的学习

## 关于我
我觉得我很有想法，但是想到和做到之间，有一块透明的玻璃挡在我的面前，它看不见，但是它真实存在，而现在我要做的，就是想办法用行动突破它！
在脑海里的话语，写在纸面上就是另外一番模样，说白了，我需要练习自己的写作能力了，多年后，看到这青涩的文字，嘴角应该会有一丝微笑吧。
