---
title: 阿里云OSS乌龙
date: 2019-09-27 12:32:15
categories:
tags:
---
昨天，突然接到阿里云的短信，我前天才开的阿里云oss欠费停机了？？？![IMG_EAB4A9A03E8D-1](http://gray.oss-cn-beijing.aliyuncs.com/2019/09/27/imgeab4a9a03e8d1.jpeg?image/auto-orient,1/resize,p_89/quality,q_90)
<center>停机短信</center>
excuse me？ 我才开通一天啊喂！后来我迅速查看了使用详情，![使用明细](http://gray.oss-cn-beijing.aliyuncs.com/2019/09/27/shi-yong-ming-xi.png?image/auto-orient,1/resize,p_89/quality,q_90)
看到了**云服务器ECS-快照**的字样，我立马想到自己的ECS，是不是设置了自动快照？？因为前面的流量情况是一样的，是不是它自己一直在自动备份？？可是我查看了自己所有的服务器，并没有开快照啊。![服务器没有开通快照](http://gray.oss-cn-beijing.aliyuncs.com/2019/09/27/fu-wu-qi-mei-you-kai-tong-kuai-zhao.png?image/auto-orient,1/resize,p_89/quality,q_90)
无奈之下，我只能联系客服（不得不说阿里爸爸服务是真棒！）晚上十一点多还有在线客服也是感动了一把。最终在与客服耐心的沟通后，仍然没有找到问题所在。直到最后，我忽然想起新建bucket时候的两个条件：![](http://gray.oss-cn-beijing.aliyuncs.com/2019/09/27/15695594696934.jpg?image/auto-orient,1/resize,p_89/quality,q_90)
**存储包**和**流量包**！！！我购买的是存储包而欠费的原因竟然是流量包……这一发现让我哭笑不得，原来问题它就不出在那40G的存储包上面，而所谓的快照原来就是我已经使用的空间，最终，当我交上欠费的¥0.1以后，终于又能打开markdown图片了。

## 反思

经过这一次的事件，我越发明白了阅读官方文档的重要性，其实这些内容在官方给的QA里一般能找到，但是习惯互联网捷径的我更愿意直接google，这不失为解决方法的一种途径，但是，有时候可能官方给出的文档更加注重问题本身，更加明了，前提是你能够静下心来仔细阅读一下。包括昨天我还没有解决的GitHub密匙问题（当初搭建博客时候，把密匙配置在了graylogo/gray.github.io仓库下，导致其他仓库push时候失败了，官方文档提供的ssh连接很详细，但可惜的是全是英文……纵使如此，一些词汇还是相对简单的，加上Google翻译，还是能看懂的。所以，啥也不说了，读文档，解决问题去吧。
