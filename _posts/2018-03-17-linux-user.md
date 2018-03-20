---
layout: post
title:  "Linux 查询、创建、删除、注销用户"
categories: Linux
tags:  linux
author: Vincent
---

* content
{:toc}

[linux指令大全](http://man.linuxde.net/)

## 查询用户
1. [参考](https://www.cnblogs.com/xiohao/p/5877256.html)
![]({{ site.imgurl }}/img/linux/user-search.jpg)
2. 但是，你会发现，在使用上面的 cat 命令所打印出来的东西太杂乱了，于是网上找到下面的这个命令：
```md
#对于 cat /etc/passwd 的替换
cat /etc/passwd|grep -v nologin|grep -v halt|grep -v shutdown|awk -F":" '{ print $1"|"$3"|"$4 }'|more
```

## 创建用户组
groupadd [option] (groupname)
>-g：指定新建工作组的id；  
-r：创建系统工作组，系统工作组的组ID小于500；  
-K：覆盖配置文件“/ect/login.defs”；  
-o：允许添加组ID号不唯一的工作组。
  
例如建立一个新组，并设置组ID：
```md
groupadd -g 344 group1
```
>此时在/etc/passwd文件中产生一个组ID（GID）是344的项目。


## 创建用户
[参考](http://man.linuxde.net/useradd)  
useradd(选项)(参数)  
>-c<备注>：加上备注文字。备注文字会保存在passwd的备注栏位中;\   
-d<登入目录>：指定用户登入时的启始目录;\
-D：变更预设值;\
-e<有效期限>：指定帐号的有效期限;\
-f<缓冲天数>：指定在密码过期后多少天即关闭该帐号;\
-g<群组>：指定用户所属的群组;\
-G<群组>：指定用户所属的附加群组;\
-m：自动建立用户的登入目录;\
-M：不要自动建立用户的登入目录;\
-n：取消建立以用户名称为名的群组;\
-r：建立系统帐号;\
-s<shell>：指定用户登入后所使用的shell;\
-u<uid>：指定用户id。\


## 删除用户
  
[参考](http://man.linuxde.net/userdel)  
userdel(选项)(参数)
>-f：强制删除用户，即使用户当前已登录；  
-r：删除用户的同时，删除与用户相关的所有文件。

请不要轻易用-r选项；他会删除用户的同时删除用户所有的文件和目录，切记如果用户目录下有重要的文件，在删除前请备份。


## 注销用户


>用 w 或者 who 查看在线用户，确定用户所在TTY。  
经测试，在CentOS 6.2 下 pkill 或者 skill 都能成功执行。  
例如注销登陆在 pts/2 上的用户：  
pkill -kill -t pts/2  
skill -KILL -t pts/2  
两者都可以，不过注意大小写。  
skill -KILL -u username  
pkill -kill -u username  
能注销所有用 username 登陆的工作台。  
用这个方法注销 root 可能会出现问题。  

[pkill](http://man.linuxde.net/pkill)