title: CentOS7-我的系统设置
author: 胖娃娃树下
date: 2017/06/23
---

这篇文章汇集系统配置方面的知识，既有CLI下的又有GUI下的，此外有一篇文章专讲GUI桌面环境。系统配置主要分为以下几类：  
1. 启动初始化
2. 网络
3. 本地化配置（中文配置）

## 1. 启动初始化
   - 开机打开网络
   `/etc/sysconfig/network-scripts/ifcfg-enp7s0`修改`ONBOOT=NO`->`ONBOOT=YES`
   - 开机关闭飞行模式

## 2. 网络
   - vsftpd configuration
   To add user who can connect to the server, we need to modify three config files. `/etc/vsftpd/vsftpd.conf` If `userlist_enable=YES`, then the users in /etc/user_list and /etc/ftpusers will be denied to make connections.Otherwise, only users in these two files will be permitted to connect to .  

## 3. 本地化
