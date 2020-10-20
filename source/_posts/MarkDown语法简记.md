---
title: MarkDown语法简记
date: 2019-07-18 16:09:06
categories: 笔记
tags: 笔记
---
常用的MarkDown语法
<!-- more-->
## 初识MarkDown
作为一个未来的码农，越早接触这一语法越好。毕竟我是拿来来练习打字速度的（手动滑稽）。

## 列表（注意中间需要空格）
```bash
1. 这是第一点
2. 这是第二点
-  前面一个点
```
显示效果：
1. 这是第一点
2. 这是第二点
-  前面一个点

## 重点
```bash
**加粗**
*斜体*
~~删除线~~ (注意这是英文键盘下的~)
**注意**：当需要打出*时，在前面加入\即可
>这是用来  \*演示\* 的 \_文本\_
```
效果：
**加粗**
*斜体*
~~删除线~~ (注意这是英文键盘下的~)
**注意**：当需要打出*时，在前面加入\即可
>这是用来  \*演示\* 的 \_文本\_

## 代码片段
或者使用\`代码片段`

`if(a=b)`
## 分隔符

```bash
***
---
___
```
效果：
***
---
___

## 超链接(需要用英文括号)
[Google](http://www.google.com/)
*以下是中文括号显示效果：*
[Google]（http://www.google.com/）

## 图片
插入图片的格式和插入**超链接**语法基本一致，只不过需要在前面加一个英文！
```bash
![GitHub](https://avatars2.githubusercontent.com/u/3265208?v=3&s=100 "GitHub,Social Coding")
```
![GitHub](https://avatars2.githubusercontent.com/u/3265208?v=3&s=100 "GitHub,Social Coding")

## 代码块
用前后各三个点来包含多行代码，在第一个三点后面加入代码的语言就可以高亮显示关键词：
```c
#include<stdio.h>
int main()
{
print("a\n");
return 0;
}
```
## 表格
```
使用  |   来分隔不同的单元格，使用 ---来分隔表头和其它行
```

```md
name | age
--- | ---
LearnShare | 12
Mike |  32
```
效果：

name | age
--- | ---
LearnShare | 12
Mike |  32
