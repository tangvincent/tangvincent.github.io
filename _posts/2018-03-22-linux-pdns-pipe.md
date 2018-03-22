---
layout: post
title:  "linux 搭建pdns"
categories: Linux
tags:  devops pdns
author: Vincent
---

* content
{:toc}


参考资料 [http://xip.io/](http://xip.io/)

## 打开防火墙
```
iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 53 -j ACCEPT
iptables -A INPUT -m state --state NEW -m udp -p udp --dport 53 -j ACCEPT
/etc/init.d/iptables save

cat /etc/sysconfig/iptables
```

## 安装epel
>yum repolist

## 查看centos版本
```
lsb_release -a
cat /etc/issue
wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
rpm -ivh epel-release-6-8.noarch.rpm
yum repolist
```

## 安装pdns
```
yum install epel-release yum-plugin-priorities && curl -o /etc/yum.repos.d/powerdns-auth-40.repo https://repo.powerdns.com/repo-files/centos-auth-40.repo && yum install pdns

```

## 下载xip-pdns
```
cd /hy/install
wget https://github.com/basecamp/xip-pdns/archive/master.zip
mv master.zip xip-pdns-master.zip
unzip xip-pdns-master.zip
cp xip-pdns.conf.example xip-pdns.conf
cd xip-pdns-master/etc
cp xip-pdns.conf.example xip-pdns.conf

cd /etc/pdns

vi pdns.conf
launch=pipe
pipe-command=/hy/install/xip-pdns-master/bin/xip-pdns /hy/install/xip-pdns-master/etc/xip-pdns.conf
```

## 安装pipe backend
```
cd /usr/lib64/pdns/
yum install pdns-backend-pipe
service pdns start
vi /var/log/messages
```
