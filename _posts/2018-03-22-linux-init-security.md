---
layout: post
title:  "如何安全地初始化一台linux服务器"
categories: Linux
tags:  devops
author: Vincent
---

* content
{:toc}

## 关闭DenyHosts
```md
/etc/init.d/daemon-control stop
```

## 改root密码，建议一年一改
```md
passwd
```
>如果改其它用户的密码，例如user1, 则 passwd user1

## 添加普通用户并授权
创建一个shell脚本 x.sh
```
export LANG=en_US.UTF-8
group=devops
users=(user1 user2)
pwd=changeit
if [ $(awk -F ':' '{print $1}' /etc/group |grep "$group" |wc -l) -eq 0 ];then
groupadd $group
fi
[ -d /home/users ] || mkdir -p /home/users

for user in ${users[@]}
do
if [ $(cat /etc/passwd |grep $user|wc -l) -ne 0 ] ;then
echo $pwd | passwd --stdin $user
usermod -a -G $group $user
else
useradd -d /home/users/$user -g $group $user
echo "$pwd" | passwd --stdin $user
usermod -a -G $group $user
fi
done
if [ $(cat /etc/sudoers |grep "$group" |wc -l) -eq 0 ];then
echo "%"$group" ALL=(ALL) ALL" >> /etc/sudoers
echo "sudoers $group create OK"
else
echo "sudoers $group have existed"
fi
```
## 如果有必须，则可以为某个用户设置单独的acl权限
例如
>setfacl -m user:user1:rwx -R /data/files

## 修复ssh端口
修改前建议先备份
>cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak20171127

```
vi /etc/ssh/sshd_config

Port 60006
PermitRootLogin no
GSSAPIAuthentication no
UseDNS no
```

## 改iptable
>iptables -I INPUT -p tcp -m state --state NEW -m tcp --dport 60006 -j ACCEPT

## 重启sshd服务
>service sshd restart

## 删除22端口
```
iptables -L INPUT --line-numbers
要查看要删除的原来的22端口的是数字是哪一条
iptables -D INPUT 数字
/etc/init.d/iptables save

cat /etc/sysconfig/iptables
```

## 删除x.sh