---
layout: post
title:  "Linux 查询、创建和删除用户"
categories: Linux
tags:  linux
author: Vincent
---

* content
{:toc}

## 查询用户
1. [参考](https://www.cnblogs.com/xiohao/p/5877256.html)
2. 但是，你会发现，在使用上面的 cat 命令所打印出来的东西太杂乱了，于是网上找到下面的这个命令：
```md
#对于 cat /etc/passwd 的替换
cat /etc/passwd|grep -v nologin|grep -v halt|grep -v shutdown|awk -F":" '{ print $1"|"$3"|"$4 }'|more
```


## 创建用户：

useradd



## 删除用户

userdelete
