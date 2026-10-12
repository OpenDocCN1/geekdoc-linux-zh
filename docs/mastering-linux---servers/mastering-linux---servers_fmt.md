
# Linux 服务器精通指南

## 摘要

本书旨在用于讲师引导的培训。对于自学者，意图是让你在一台运行良好的 Linux 电脑旁阅读本书，以便能够立即操作每个主题，练习每条命令。

本书面向初级 Linux 系统管理员（对于想要进一步了解其 Linux 系统的家庭用户来说，也可能有趣且有用）。然而，本书并非用于介绍文本编辑器、浏览器、邮件客户端、多媒体或办公软件等 Linux 桌面应用程序。

获取更多信息和免费的 `.pdf` 文件请访问：`http://linux-training.be`。

欢迎随时联系作者：

- `Paul Cobbaut`: `paul.cobbaut@gmail.com`, `http://www.linkedin.com/in/cobbaut`

Linux Training 项目的贡献者：

- `Serge Van Ginderacter`: `serge@ginsys.eu`，构建脚本和基础设施搭建
- `Ywein Van den Brauer`: `ywein@crealau.eu`，许可和法律章节
- `Hendrik De Vloed`: `hendrik.devloed@ugent.be`, `builderhead.pl` 脚本

我们还感谢我们的评审员：

- `Wouter Verlhest`: `wo@uter.be`, `http://grep`
- `Geert Goossens`: `mail.goossens.geert@gmail.com`, `http://www.linkedin.com/in/`
- `Elie De Brauer`: `elie@de-brauer.be`, `http://www.de-brauer.be`
- `Christophe Vandeplas`: `christophe@vandeplas.com`, `http://christophe.vandeplas`
- `Bert Desmet`: `bert@devnox.be`, `http://blog.bdesmet.be`
- `Rich Yonts`: `richyonts@gmail.com`,

### 目录片段

- 4.17. 解决方案：`dns` ................................................................................ 88
- 5. 高级 `DNS` ....................................................................................... 89
  - 5.1. 示例：`DNS` 轮询调度 ................................................................................ 90
  - 5.2. `DNS` 代理 .......................................................................................... 91
  - 5.3. 示例：`DNS` 代理 .......................................................................... 92
  - 5.4. 示例：分域解析 `dns` ............................................................ 94
  - 5.5. 旧版 `DNS` 主题 ................................................................................ 96
- IV. `dhcp` 服务器 ..................................................................................... 100
- 6. `dhcp` 简介 ................................................................... 102
  - 6.1. 广播 ............................................................................... 103
  - 6.2. 绘制 `dh` 原图 ............................................................................ 104
  - 6.3. 安装 `dhcp` 服务器 ................................................... 105
  - 6.4. RHEL/CentOS 的 `dhcp` 服务器 ....................................... 105
  - 6.5. 客户端预留 ....................................................... 106
  - 6.6. 示例配置文件 ................................................... 106
  - 6.7. 旧版示例配置文件 ........................................ 107
  - 6.8. 高级 `DNS` ............................................................ 109
  - 6.9. 练习：`dhcp` ........................................................ 110
- V. `iptables` 防火墙 ............................................................ 111
- 7. 规则简介 ................................................ 113
  - 7.1. 路由器或防火墙 ................................................ 114
  - 7.2. 数据包转发 ................................................ 114
  - 7.3. 数据包过滤 ................................................ 114
  - 7.4. 状态检测 ...................................................... 114
  - 7.5. `nat` (网络地址转换) ................ 115
  - 7.6. `pat` (端口地址转换) ...................... 115
  - 7.7. `snat` (源 `nat`) ....................................... 115
  - 7.8. 多数地址 ......................................... 115
  - 7.9. `dnat` (目的 `nat`) ......................... 115
  - 7.10. 端口转发 ................................... 115
  - 7.11. `/proc/sys/net/ipv4/ip_forward` .............. 116
  - 7.12. `/etc/sysctl.conf` ................................. 116
  - 7.13. `syslog` ................................................... 116
  - 7.14. 练习：数据包转发 ................ 117
  - 7.15. 解决方案：数据包转发 ............... 119
- 8. `iptables` 防火墙 .................................... 122
  - 8.1. `iptables` 表 ........................................ 123
  - 8.2. 启动与停止 `iptables` ............... 123
  - 8.3. `filter` 表 ................................... 123
  - 8.4. 练习：数据包过滤 ................ 129
  - 8.5. 解决方案：数据包过滤 ............... 130
  - 8.6. 网络地址转换 ................ 131
- VI. `Samba` 简介 .......................................... 134
- 9. `samba` 简介 .......................... 137



## 9. 精细安装版本

- 9.1. 精细安装版本 ................ 138
- 9.2. 安装 `samba` ................................ 139
- 9.3. 文档 ................................... 140
- 9.4. 启动与停止 `samba` ................ 141
- 9.5. `samba` 进程 ........................ 142
- 9.6. SMB 协议 ........................ 143
- 9.7. 练习：`samba` 简介 .... 144

## 10. Samba 快速上手

- 10.1. `/etc/samba/smb.conf` ................ 146
- 10.2. `/usr/bin/testpam` ................ 147
- 10.3. `/usr/bin/smbclient` ................ 148
- 10.4. `/usr/bin/smbtree` ................ 150
- 10.5. 服务器字符串 ................... 151
- 10.6. Samba 网页管理工具 (SWAT) .. 152

Linux 服务器

- 10.7. 练习：`samba` 快速上手 ................................................................ 153
- 10.8. 解决方案：`samba` 快速上手 ............................................................. 154

## 11. 只读文件服务器

- 11.1. 设置共享目录 ....................................................................... 157
- 11.2. 配置共享 ...................................................................................... 157
- 11.3. 重启服务器 ....................................................................................... 158
- 11.4. 验证共享 ........................................................................................ 158
- 11.5. 关于 `neatat` 的说明 ........................................................................................ 160
- 11.6. 练习：只读服务器 ................................................................. 161

## 12. 可写文件服务器

- 12.1. 设置共享目录 ....................................................................... 163
- 12.2. `smb.conf` 中的配置 ...................................................................... 164
- 12.3. 配置共享 ...................................................................... 164
- 12.4. 使用 Windows 测试访问 ................................................................. 164
- 12.5. 测试连接 ....................................................................... 165
- 12.6. 这是如何实现的？........................................................................... 165
- 12.7. 练习：可写服务器 ................................................................ 166
- 12.8. 解决方案：可写服务器 ................................................................ 167

## 13. Samba 账号

- 13.1. 创建账号 ....................................................................... 169
- 13.2. 文件所有权 ................................................................ 169
- 13.3. `/etc/samba/passwd` ............................................................ 169
- 13.4. 后端 ............................................................................ 170
- 13.5. 强制用户 ....................................................................... 170
- 13.6. 练习：`samba` 账号 ................................................................ 171
- 13.7. 解决方案：`samba` 账号 ................................................ 172

## 14. Samba 身份验证

- 14.1. 在 Linux 上创建账号 ................................................................ 174
- 14.2. 在 Samba 上创建账号 ............................................................ 174
- 14.3. `security = user` ......................................................................... 174
- 14.4. 配置共享 ....................................................................... 175
- 14.5. 使用 `net` 测试访问 ................................................................ 175
- 14.6. 使用 `smbclient` 测试访问 ................................................................ 175
- 14.7. 所有权 ....................................................................... 176
- 14.8. 常见问题 ................................................................ 176
- 14.9. 练习：`samba` 身份验证 ............................................. 178



## 15. Samba 共享安全

- 15.1. 基于用户的安全
- 15.2. 基于 IP 地址的安全
- 15.3. 隐性安全
- 15.4. 文件系统安全
- 15.5. 练习：共享安全
- 15.6. 解决方案：共享安全

## 16. Samba 域成员

- 16.1. `smb.conf` 中的更改
- 16.2. 加入 Active Directory 域
- 16.3. `winbind`
- 16.4. `winbind`
- 16.5. `getent`
- 16.6. 文件所有权
- 16.7. 练习：`samba` 域成员

## 17. Samba 域控制器

- 17.1. 关于域控制器
- 17.2. 关于安全模式
- 17.3. 关于密码后端
- 17.4. `smb.conf` 中的 `[global]` 节
- 17.5. `netlogon` 共享
- 17.6. 其他 `[share]` 节
- 17.7. 用户与组
- 17.8. `tdbsam`
- 17.9. 关于计算机账户
- 17.10. 本地或漫游配置文件
- 17.11. NTFS ACLs 中的组
- 17.12. 登录脚本
- 17.13. 实践：`samba` 域控制器

## 18. Samba 4 简述

- 18.1. Samba 4 alpha 6

## VII. selinux

## 19. SELinux 简介

- 19.1. `selinux` 模式
- 19.2. 日志
- 19.3. 激活 `selinux`
- 19.4. `enforce`
- 19.5. `selenux`
- 19.6. `getatus`
- 19.7. 策略
- 19.8. `/etc/selinux/config`
- 19.9. DAC 或 MAC
- 19.10. `b -Z`
- 19.11. `-Z`



- 19.12. `/selinux` ............................................................ 214
- 19.13. 身份 ............................................................ 214
- 19.14. 角色 ....................................................... 214
- 19.15. 类型（或域） ................................................ 215
- 19.16. 安全上下文 ...................................... 216
- 19.17. 转换 ....................................................... 216
- 19.18. 扩展属性 ................................... 217
- 19.19. 进程安全上下文 ................... 217
- 19.20. `chcon` ....................................................... 217
- 19.21. 示例 ........................................ 218
- 19.22. `setroubleshoot` ................................ 220
- 19.23. 布尔值 ............................................ 222

## VIII. 介绍 `git` ................................................... 222

## 20. `git` ........................................................................ 226

- 20.1. `git` ........................................................ 227
- 20.2. 安装 `git` ................................... 227
- 20.3. 开始项目 ................................ 227
- 20.4. `git` 分支 ....................................... 230
- 20.5. 待续... ............................ 231
- 20.6. `github.com` ....................................... 232
- 20.7. 将你的公钥添加到 `github` ........ 232
- 20.8. 实践：`git` ................................... 233

## IX. `ipv6` .................................................................. 234

## 21. `ipv6` 简介 ................................ 236

- 21.1. 关于 `ipv6` ....................................... 237
- 21.2. 网络 ID 和主机 ID ................... 237
- 21.3. 主机部分生成 ................ 237
- 21.4. `ipv4` 映射 `ipv6` 地址 ................ 238
- 21.5. 链路本地地址 ................ 238
- 21.6. 唯一本地地址 ................ 238
- 21.7. 全局单播地址 ............ 238
- 21.8. 6664 ....................................................... 238
- 21.9. ISP ................................................................ 239
- 21.10. 不可路由地址 ............................................................................ 239
- 21.11. `ping6` ....................................................................................................... 239
- 21.12. 比时与 `ipv6` ................................................................................ 240
- 21.13. 其他网站 ................................................................................... 240
- 21.14. `6to4` ................................................................................ 240
- 21.15. `ping6` 和 `ipv6` ................................................................................ 240
- 21.16. `ipv6` 和 `tcp` ........................................................................ 242
- 21.17. `PTR` 记录 ................................................................................ 242
- 21.18. `6to4` 设置 ................................................................................ 242

## X. 附录 ................................................................. 245

## A. 克隆 ................................................................................ 247

- A.1. 关于克隆 ................................................................. 247
- A.2. 离线克隆 ................................................. 247
- A.3. 示例 ................................................................ 247

## B. 许可证 .......................................................... 249

索引 ....................................................... 256

# 表列表

- 4.1. 顶级域名 ................................................. 65
- 4.2. 新通用 TLD ................................................. 65
- 7.1. 数据转发 ................................................................ 17
- 7.2. 数据转发 ................................................................ 19

# 第一部分. `apache` 和 `squid`

# 目录

## 1. `apache` 服务器 ................................................................ 3

- 1.1. `apache` 简介 ........................................ 4



## 目录

- 1.2. Debian 上的虚拟主机 ................................................. 11
- 1.3. Debian 上的命名虚拟主机 ................................... 15
- 1.4. Debian 上的密码保护网站 .......................... 17
- 1.5. CentOS 上的虚拟主机 ................................................. 18
- 1.6. CentOS 上的命名虚拟主机 ................................... 22
- 1.7. CentOS 上的密码保护网站 .......................... 24
- 1.8. `apache` 故障排除 ........................................ 27
- 1.9. 虚拟主机 .................................................................... 27
- 1.10. 别名与重定向 ....................................................... 27
- 1.11. 关于 `.htaccess` 的更多 ............................................... 27
- 1.12. 流量 ............................................................ 27
- 1.13. Debian 上的自签名证书 ..................................... 28
- 1.14. RHEL/CentOS 上的自签名证书 ............................................... 30
- 1.15. 实践：`apache` ................................................................ 32

## 2. `squid` 简介 ................................................................ 33

- 2.1. 关于代理服务器 ............................................ 34
- 2.2. 安装 `squid` ................................................................................. 34
- 2.3. 端口 3128 ........................................................................ 34
- 2.4. 启动与停止 ........................................................ 34
- 2.5. 客户端代理设置 ........................................................ 35
- 2.6. 倒置图像 ............................................................ 37
- 2.7. `/var/log/squid` ................................................................................ 39
- 2.8. 访问控制 ................................................................................ 39
- 2.9. 测试 `squid` ................................................................................. 39

# 第 1 章 `apache` Web 服务器

在本章中，我们将学习如何使用 `apache` 软件搭建 Web 服务器。

根据 NetCraft (http://news.netcraft.com/archives/web_server_survey.html) 的数据，大约有 70% 的 Web 服务器运行在 Apache 上。该名称源于一个补丁斑斑的（patchy）Web 服务器，因为人们为 NCSA httpd 服务器编写了大量的补丁（patches）。

后续章节将把此 Web 服务器扩展为 LAMP 堆栈（Linux, Apache, Mysql, Perl/PHP/Python）。

## 1.1. `apache` 简介

### 1.1.1. 在 Debian 上安装

此句显示没有安装 `apache` 服务器，`/var/www` 目录也不存在。

```
root@debian:~# ls -l /var/www
ls: cannot access /var/www: No such file or directory
root@debian:~# dpkg -l | grep apache
```

在 Debian 上安装 `apache`：

```
root@debian:~# aptitude install apache2
The following NEW packages will be installed:
apache2-mpn-worker(a) apache2-utils(a) apache2.2-bin(a) apache2.2-com-
mon(a) libapr1(a) libaprutill(a) libaprutill-dbd-sqlite3(a) libaprutill-ldap(a)
ssl(a)
0 packages upgraded, 10 newly installed, 0 to remove and 0 not upgraded.
Need to get 1,487 kB of archives. After unpacking 5,673 kB will be used.
Do you want to continue? [Y/n]
```

安装完成后，上述两个命令将产生不同的结果：

```
root@debian:~# ls -l /var/www
total 4
-rw-r--r-- 1 root 177 Apr 29 11:55 index.html
root@debian:~# dpkg -l | grep apache | tr -s ' '
ii apache2.2.22-13+deb7ul amd64 Apache HTTP Server metapackage
ii apache2-mpn-worker 2.2.22-13+deb7ul amd64 Apache HTTP Server - high speed th
read model
ii apache2-utils 2.2.22-13+deb7ul amd64 utility programs for webservers
ii apache2.2-bin 2.2.22-13+deb7ul amd64 Apache HTTP Server common binary files
ii apache2.2-common 2.2.22-13+deb7ul amd64 Apache HTTP Server common files
```

### 1.1.2. 在 RHEL/CentOS 上安装

注意，红帽发行版使用 `httpd` 作为包名和进程名，而不是 `apache`。

验证 CentOS/RHEL 中是否安装了 `apache`：

```
[root@centos65 ~]# rpm -q httpd
package httpd is not installed
[root@centos65 ~]# ls -l /var/www
ls: cannot access /var/www: No such file or directory
```

在 CentOS 上安装 `apache`：

```
[root@centos65 ~]# yum install httpd
```

运行 `yum install httpd` 命令后，Centos 6.5 服务器已安装 `apache`，且 `/var/www` 目录存在。



```
[root@centos65 ~]# rpm -q httpd
httpd-2.2.15-30.el6.centos.x86_64
[root@centos65 ~]# ls -l /var/www
total 16
drwxr-xr-x 2 root 4096 Apr 29 23:57 cgi-bin
drwxr-xr-x 2 root 4096 May 6 13:08 error
drwxr-xr-x 2 root 4096 Apr 29 23:57 html
drwxr-xr-x 2 root 4096 May 6 13:08 icons
[root@centos65 ~]#
```

### 1.1.3. 在 Debian 上运行 apache

这是在 Debian 上启动 `apache2` 的方法。

```
root@debian7:~# service apache2 status
Apache2 is NOT.
root@debian7:~# service apache2 start
Starting web server: apache2:Could not reliably determine the server's qualified domain name, using 127.0.1 for ServerName
```

验证请运行 `apache2 status` 命令或使用 `ps`。

```
root@debian7:~# service apache2 status
Apache2 is running (pid 3680)
root@debian7:~# ps -C apache2
PID TIME CMD
3680 ? 00:00:00 apache2
3683 ? 00:00:00 apache2
3684 ? 00:00:00 apache2
3685 ? 00:00:00 apache2
root@debian7:~#
```

或者使用 `wget` 和 `file` 验证你的 Web 服务器提供了 html 文档。

```
root@debian7:~# wget 127.0.0.1
--2014-05-06 13:27:02-- http://127.0.0.1/
--Connecting to 127.0.0.1:80... connected.
HTTP request sent, waiting response... 200 OK
Length: 177 [text/html]
Saving to: 'index.html'
```

```
100[=================================>] 177 --K/s in 0s
2014-05-06 13:27:02 'index.html' saved [177/177]
root@debian7:~# file index.html
index.html: HTML document, ASCII text
root@debian7:~#
```

或者通过打开浏览器并访问服务器 IP 地址来验证 apache 是否运行。应该会显示 Apache 测试页面。

你可以通过以下操作在重启 apache 时快速避免“could not reliably determine the fdn”消息。

```
root@debian7:~# echo ServerName Debian7 >> /etc/apache2/apache2.conf
root@debian7:~# service apache2 restart
Restarting web server: apache2 ...
```

### 1.1.4. 在 CentOS 上运行 apache

这是在 CentOS 上启动 `apache2` 的方法。

```
[root@centos65 ~]# service httpd status
httpd is NOT running.
[root@centos65 ~]# service httpd start
Starting web server: httpd:Could not reliably determine the server's qualified domain name, using 127.0.0.1 for ServerName
```

验证请运行 `httpd status` 命令或使用 `ps`。

```
[root@centos65 ~]# service httpd status
httpd is running (pid 1234)
[root@centos65 ~]# ps -C httpd
PID TIME CMD
1234 ? 00:00:00 httpd
1235 ? 00:00:00 httpd
1236 ? 00:00:00 httpd
1237 ? 00:00:00 httpd
[root@centos65 ~]#
```

或者使用 `wget` 和 `file` 验证你的 Web 服务器提供了 html 文档。

```
[root@centos65 ~]# wget 127.0.0.1
--2014-05-06 13:27:02-- http://127.0.0.1/
--Connecting to 127.0.0.1:80... connected.
HTTP request sent, waiting response... 200 OK
Length: 177 [text/html]
Saving to: 'index.html'
```

```
100[=================================>] 177 --K/s in 0s
2014-05-06 13:27:02 'index.html' saved [177/177]
[root@centos65 ~]# file index.html
index.html: HTML document, ASCII text
[root@centos65 ~]#
```

或者通过打开浏览器并访问服务器 IP 地址来验证 apache 是否运行。应该会显示 Apache 测试页面。

你可以通过以下操作在重启 apache 时快速避免“could not reliably determine the fdn”消息。

```
[root@centos65 ~]# echo ServerName localhost >> /etc/httpd/conf/httpd.conf
[root@centos65 ~]# service httpd restart
Restarting web server: httpd ...
```

### 1.1.5. 在 Debian 上运行 apache

这是在 Debian 上启动 `apache2` 的方法。

```
root@debian7:~# service apache2 status
Apache2 is NOT.
root@debian7:~# service apache2 start
Starting web server: apache2:Could not reliably determine the server's qualified domain name, using 127.0.0.1 for ServerName
```

验证请运行 `apache2 status` 命令或使用 `ps`。

```
root@debian7:~# service apache2 status
Apache2 is running (pid 3680)
root@debian7:~# ps -C apache2
PID TIME CMD
3680 ? 00:00:00 apache2
3683 ? 00:00:00 apache2
3684 ? 00:00:00 apache2
3685 ? 00:00:00 apache2
root@debian7:~#
```

或者使用 `wget` 和 `file` 验证你的 Web 服务器提供了 html 文档。

```
root@debian7:~# wget 127.0.0.1
--2014-05-06 13:27:02-- http://127.0.0.1/
--Connecting to 127.0.0.1:80... connected.
HTTP request sent, waiting response... 200 OK
Length: 177 [text/html]
Saving to: 'index.html'
```

```
100[=================================>] 177 --K/s in 0s
2014-05-06 13:27:02 'index.html' saved [177/177]
root@debian7:~# file index.html
index.html: HTML document, ASCII text
root@debian7:~#
```

或者通过打开浏览器并访问服务器 IP 地址来验证 apache 是否运行。应该会显示 Apache 测试页面。



你可以通过以下操作在重启`apache`时快速避免“could not reliably determine the fdn”消息。

```bash
root@debian7:~# echo ServerName Debian7 >> /etc/apache2/apache2.conf
root@debian7:~# service apache2 restart
Restarting web server: apache2 ...
```

### 1.1.6. 默认网站

更改新安装`apache`服务器的默认网站非常简单。你只需要在`DocumentRoot`中创建（或更改）一个`index.html`文件。

在 Debian 上查找`DocumentRoot`：

```bash
root@debian:~# grep DocumentRoot /etc/apache2/sites-available/default
DocumentRoot /var/www
```

这意味着`/var/www/index.html`是默认站点。

```bash
root@debian:~# cat /var/www/index.html
<html><h1>It works!</h1>
<p>This is the default web page for this server.</p>
<p>The web server is running but no content has been added, yet.</p>
</body></html>
root@debian:~#
```

在 RHEL/CentOS 上查找`DocumentRoot`：

```bash
[root@centos65 ~]# grep DocumentRoot /etc/httpd/conf/httpd.conf
DocumentRoot "/var/www/html"
```

RHEL/CentOS 没有默认页面（只有之前提到的`noindex.html`错误页面）。但在`/var/www/html/`中创建的`index.html`文件将自动作为默认页面使用。

### 1.1.7. apache 配置

在 Debian 或 CentOS 上配置`apache`时，有很多相似之处，但也有几处不同。这两个 Linux 家族都有自己的所有者示例。

RHEL/CentOS 上的所有配置都在`/etc/httpd`中完成。

```bash
[root@centos65 ~]# ls -l /etc/httpd/
total 8
drwx-xr-x 2 root root 4096 May 6 13:08 conf
drwx-xr-x 2 root root 4096 May 6 13:08 conf.d
lrwx-xr-wx 1 root root 19 May 6 13:08 logs -> ../var/log/httpd
lrwx-xr-wx 1 root root 29 May 6 13:08 modules -> ../usr/lib64/httpd/modules

drwx-xr-wx 1 root root 19 May 6 13:08 run -> ../var/run/httpd
[root@centos65 ~]#
```

Debian（以及ubuntu/...）使用`/etc/apache2`。

```bash
root@debian7:~# ls -l /etc/apache2/
total 72
-rw-r--r-- 1 root root 9659 May 6 14:23 apache2.conf
drwx-xr-x 2 root root 4096 May 6 13:19 conf.d
-rw-r--r-- 1 root root 1465 Jan 31 18:35 envvars
-rw-r---- 1 root root 31063 Jul 20 2013 magic
drwx-xr-x 2 root root 4096 May 6 13:19 mods-available
drwx-xr-x 2 root root 4096 May 6 13:19 mods-enabled
-rw-r--r-- 1 root root 750 Jan 26 12:13 ports.conf
drwx-xr-x 2 root root 4096 May 6 13:19 sites-available
drwx-xr-x 2 root root 4096 May 6 13:19 sites-enabled
root@debian7:~#
```

## 1.2. 在 Debian 上使用端口虚拟主机

### 1.2.1. 默认虚拟主机

Debian 为其默认网站有一个虚拟主机配置文件，位于`/etc/apache2/sites-available/default`。

```bash
root@debian:~# head -2 /etc/apache2/sites-available/default
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
```

### 1.2.2. 三个额外的虚拟主机

在这种场景下，我们为三个客户创建了三个额外的网站，他们共享一个俱乐部并希望共同聘用你。他们是一个名为 Choo Choo 的模型火车俱乐部、一个名为 Chess Club 42 的象棋俱乐部以及一个名为 hunter2 的黑客空间。

在一个服务器上放置网站的一种方法是将每个网站放在不同的端口上。此截图显示了他们新创建的虚拟主机，每个客户一个。

```bash
root@debian:~# vi /etc/apache2/sites-available/choochoo
root@debian:~# cat /etc/apache2/sites-available/choochoo
<VirtualHost *:7000>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/choochoo
</VirtualHost>
root@debian:~# vi /etc/apache2/sites-available/chessclub42
root@debian:~# cat /etc/apache2/sites-available/chessclub42
<VirtualHost *:8000>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/chessclub42
</VirtualHost>
root@debian:~# vi /etc/apache2/sites-available/hunter2
root@debian:~# cat /etc/apache2/sites-available/hunter2
<VirtualHost *:9000>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/hunter2
</VirtualHost>
```

注意不同的端口`7000`、`8000`和`9000`。注意我们还为每个网站指定了唯一的`DocumentRoot`。如果你使用的是 Ubuntu 或 Mint，这些配置文件需要以`.conf`结尾。

### 1.2.3. 三个额外的端口

我们需要在`ports.conf`中启用这三个端口。用`vi`打开文件并添加三行来监听额外的端口。

```bash
root@debian7:~# vi /etc/apache2/ports.conf
root@debian7:~# grep Listen /etc/apache2/ports.conf
Listen 80
Listen 7000
Listen 8000
Listen 9000
```

### 1.2.4. 三个额外的网站

我们需要创建三个`DocumentRoot`并在这些目录中放置简单的网站。

```bash
root@debian7:~# mkdir /var/www/choochoo
root@debian7:~# mkdir /var/www/chessclub42
root@debian7:~# mkdir /var/www/hunter2
root@debian7:~# echo 'Choo Choo model train Choo Choo' > /var/www/choochoo/index.html
root@debian7:~# echo 'Welcome to chess club 42' > /var/www/chessclub42/index.html
root@debian7:~# echo 'Hacking is fun' > /var/www/hunter2/index.html
```

### 1.2.5. 启用网站

最后一步是使用`a2`命令启用网站。此命令会在`sites-enabled`中创建链接。这些链接还没有……



```bash
root@debian:~# cd /etc/apache2/
root@debian:~# ls sites-available/
chessclub42  choochoo  default
root@debian:~# ls sites-enabled/
```

为所有网站运行 `a2` 命令。为了激活新配置，你需要运行：`service apache2 reload`。

```bash
root@debian:~# a2 choochoo
root@debian:~# a2 chessclub42
root@debian:~# a2 hunter2
root@debian:~# service apache2 reload
```

### 1.2.6. 测试网站

在端口 7000 上测试模型火车 Choo Choo。

```bash
root@debian7:~# wget 127.0.0.1:7000
2014-05-06 21:16:03-- http://127.0.0.1:7000/
Connecting to 127.0.0.1:7000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 32 [text/html]
Saving to: index.html
================> 32 KB/s in 0
2014-05-06 21:16:03 (2.92 MB/s) 'index.html' saved [32/32]
root@debian7:~# cat /var/www/choochoo/index.html
Choo Choo model train Choo Choo
```

在端口 8000 上测试 Chess 42。

```bash
root@debian7:~# wget 127.0.0.1:8000
2014-05-06 21:16:20-- http://127.0.0.1:8000/
Connecting to 127.0.0.1:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 26 [text/html]
Saving to: index.html
================> 25 KB/s in 0
2014-05-06 21:16:20 (2.16 MB/s) 'index.html' saved [25/25]
root@debian7:~# cat /var/www/chessclub42/index.html
Welcome to chess club 42
```

在端口 9000 上测试黑客俱乐部 2。

```bash
root@debian7:~# wget 127.0.0.1:9000
2014-05-06 21:16:30-- http://127.0.0.1:9000/
Connecting to 127.0.0.1:9000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 26 [text/html]
Saving to: index.html
================> 32 KB/s in 0
2014-05-06 21:16:30 (2.0 MB/s) 'index.html' saved [26/26]
root@debian7:~# cat /var/www/hunter2/index.html
Hacking is fun
```

清理临时文件。

```bash
root@debian7:~# rm index.html
```

## 1.3. 在 Debian 上使用命名虚拟主机

### 1.3.1. 命名虚拟主机

象棋俱乐部和模型火车俱乐部的端口号太难记忆了。他们希望通过名称访问网站。

我们继续在具有三个端口网站的同一服务器上工作。我们需要确保这些网站可以通过 `choochoo.local`、`chessclub42.local` 和 `hunter2.local` 访问。

我们首先创建新的虚拟主机。从另一台计算机使用服务器的 IP 地址进行测试。

### 1.3.2. 名称解析

我们需要某种方式解析名称。这可以在另一个章节中讨论。在本示例中，也可以快速地将三个名称添加到 `/etc/hosts` 文件中。

```bash
root@debian?:# grep ^192 /etc/hosts
192.168.42.50 choochoo.local
192.168.42.50 chessclub42.local
192.168.42.50 hunter2.local
```

注意你可能还有另一个 IP 地址...

### 1.3.3. 启用虚拟主机

接下来我们可以使用 `a2ensite` 来启用。

```bash
root@debian7:/etc/apache2/sites-available# a2ensite choochoo.local
Enabling site chesschooo.local.
To activate the new configuration, you need to run:
    service apache2 reload
root@debian7:/etc/apache2/sites-available# a2ensite chessclub42.local
Enabling site chessclub42.local.
To activate the new configuration, you need to run:
    service apache2 reload
root@debian7:/etc/apache2/sites-available# a2ensite hunter2.local
Enabling site hunter2.local.
To activate the new configuration, you need to run:
    service apache2 reload
```

### 1.3.4. 重载与验证

执行 `service apache2 reload` 后，可以通过名称访问网站。

```bash
root@debian7:/etc/apache2/sites-available# service apache2 reload
Reloading web server config. apache2.
root@debian7:/etc/apache2/sites-available# chessclub42.local
--2014-05-06 21:37:13-- http://chessclub42.local/
Resolving chessclub42.local (chessclub42.local)... 192.168.42.50
Connecting to chessclub42.local (chessclub42.local) [192.168.42.50]:80... connected.

HTTP request sent, awaiting response... 200 OK
Length: 25 [index.html]
Saving to: 'index.html'

100%[------------------------------------------------------] 25  --K/s    in 0s

2014-05-06 21:37:13 (2.06 MB/s) - `index.html' saved [25/25]

root@debian7:/etc/apache2/sites-available# cat index.html
Welcome to chess club 42
```

## 4. Debian 上的密码保护网站

你可以使用指向 `.htpasswd` 文件的 `.htaccess` 文件来对网站中的文件和目录进行保护。`htpasswd` 命令可以创建一个包含用户名和（加密）密码的 `.htpasswd` 文件。

此截图为名为 cliff 的黑客创建了用户和密码，并使用 `-e` 标志创建 `.htpasswd` 文件。

```bash
root@debian7:~# htpasswd -c /var/www/.htpasswd cliff
New password:
Re-type new password:
Adding password for user cliff
root@debian7:~# cat /var/www/.htpasswd
cliff:$apr1$vuuj10lLk$SZ49q0swXh93P0QPVP.
```

Cliff 和 Rob 选择了相同的密码（`hunter2`），这展示了如何向 `.htpasswd` 添加第二个用户和密码。



```
root@debian7:~# htpasswd /var/www/.htpasswd rob
New password:
Re-type new password:
Adding password for user rob
root@debian7:~# cat /var/www/.htpasswd
cliff:$apr1$vuuj10lLk$SZ49q0swXh93P0QPVP
rob:$apr1$5Hn1IFFTcNR1HoP.IW11/1DRQ41Q0
```

我们需要在想要保护的网站的 `DocumentRoot` 中创建一个 `.htaccess` 文件。此截图显示了一个示例。

```
root@debian7:~# cd /var/www/hunter2/
root@debian7:/var/www/hunter2# cat .htaccess
AuthUserFile="Members only!"
AuthName
AuthType Basic
require valid-user
```

注意，我们正在保护之前创建的 9000 端口上的网站。

由于我们将网站放在了名为 `hunter2` 的黑客空间中，且它是默认网站的子目录，我们需要如截图所示调整 `/etc/apache2/sites-available/default/default` 中的 `AllowOverride` 参数（Debian 7 上的行号可能会有所不同）。

```
<Directory /var/www//
    Options Indexes FollowSymLinks MultiViews
    AllowOverride Authconfig
    Order allow, deny
    allow from all
</Directory>
```

现在重启 `apache2` 服务器并测试它是否正常工作！

## 1.5. CentOS 上的端口虚拟主机

### 1.5.1. 默认虚拟主机

与 Debian 不同，CentOS 的默认网站没有虚拟主机配置文件。相反，当在默认位置（`/var/www/html`）未找到索引文件时，默认配置将抛出一个标准的错误页。

### 1.5.2. 三个虚拟主机

在这种情况下，我们为三个客户创建了三个额外的网站，他们共享一个俱乐部。它们分别是：名为 `Choo Choo` 的模型火车俱乐部、一个名为 `Chess 42` 的象棋俱乐部以及一个名为 `hunter2` 的黑客空间。

在一个 Web 服务器上运行三个网站的一种方法是让每个网站运行不同的端口。此截图显示了为每个客户新创建的虚拟主机。

```
[root@CentOS65] ~# vi /etc/httpd/conf.d/choochoo.conf
[root@CentOS65] ~# cat /etc/httpd/conf.d/choochoo.conf
<VirtualHost *:7000>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/html/choochoo
</VirtualHost>
[root@CentOS65] ~# vi /etc/httpd/conf.d/chessclub42.conf
[root@CentOS65] ~# cat /etc/httpd/conf.d/chessclub42.conf
<VirtualHost *:8000>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/html/chessclub42
</VirtualHost>
[root@CentOS65] ~# vi /etc/httpd/conf.d/hunter2.conf
[root@CentOS65] ~# cat /etc/httpd/conf.d/hunter2.conf
<VirtualHost *:9000>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/html/hunter2
</VirtualHost>
```

注意不同的端口号 7000、8000 和 9000。注意我们为每个网站指定了唯一的 `DocumentRoot`。

### 1.5.3. 三个额外的端口

我们需要在 `httpd.conf` 文件中启用这三个端口。

```
[root@CentOS65] ~# vi /etc/httpd/conf/httpd.conf
root@debian:-# grep "Listen" /etc/httpd/conf/httpd.conf
Listen 80
Listen 7000
Listen 8000
Listen 9000
```

### 1.5.4. SELinux 守护我们的端口

如果我们尝试重启服务器，将注意到以下错误：

```
[root@CentOS65 #] service httpd restart      [ OK ]
Stopping httpd:
Starting httpd:
(13)Permission denied: make_sock: could not bind to address 0.0.0.0:7000
 listening sockets available, shutting down
                               [FAILED]
```

这是由于 `SELinux` 为其他用户保留了 7000 和 8000 端口。我们需要告诉 `SELinux`

### 1.5.8. 防火墙规则

然而，如果我们尝试从另一台机器访问该站点，仍然无法查看网站。防火墙正在阻止入站连接。我们需要先打开这些入站端口

```bash
[root@CentOS65 ~]# iptables -I INPUT -p tcp --dport 80 -j ACCEPT
[root@CentOS65 ~]# iptables -I INPUT -p tcp --dport 7000 -j ACCEPT
[root@CentOS65 ~]# iptables -I INPUT -p tcp --dport 8000 -j ACCEPT
[root@CentOS65 ~]# iptables -I INPUT -p tcp --dport 9000 -j ACCEPT
```

如果我们希望这些规则在重启后仍然有效，我们需要保存它们。

```bash
[root@CentOS65 ~]# service iptables save
iptables: Saving firewall rules to /etc/sysconfig/iptables:[ OK ]
```

## 1.6. CentOS 上的命名主机

### 1.6.1. named 虚拟主机

象棋俱乐部和模型火车俱乐部觉得端口号太难记了。他们更倾向于通过名称访问网站。

我们继续在同一台服务器上工作，该服务器上有三个网站。我们需要确保这些网站可以通过 `choochoo.local`、`chessclub42.local` 和 `hunter2.local` 的名称访问。

首先，我们需要在配置中启用虚拟主机

```bash
[root@CentOS65 ~#] vi /etc/httpd/conf/httpd.conf
[root@CentOS65 ~#] grep ^VirtualHost /etc/httpd/conf/httpd.conf
NameVirtualHost *:80
[root@CentOS65 ~#]#
```

接下来，我们需要创建三个虚拟主机。



```bash
[root@CentOS65 ~#] vi /etc/httpd/conf/choochoo.local
[root@CentOS65 ~#] cat /etc/httpd/conf/chessclub42.local
[root@CentOS65 ~#] vi /etc/httpd/conf/hunter2.local
[root@CentOS65 ~#] cat /etc/httpd/conf/choochoo.local
<VirtualHost *:80>
ServerAdmin webmaster@localhost
ServerName choochoo.local
DocumentRoot /var/www/html/choochoo
</VirtualHost>
[root@CentOS65 ~#] cat /etc/httpd/conf/chessclub42.local
<VirtualHost *:80>
ServerAdmin webmaster@localhost
ServerName chessclub42.local
DocumentRoot /var/www/html/chessclub42
</VirtualHost>
[root@CentOS65 ~#] cat /etc/httpd/conf/hunter2.local
<VirtualHost *:80>
ServerAdmin webmaster@localhost
ServerName hunter2.local
DocumentRoot /var/www/html/hunter2
</VirtualHost>
[root@CentOS65 ~#]#
```

注意，它们都监听 80 端口，并且有一个额外的 `ServerName` 指令。

### 1.6.2. 域名解析

我们需要一些东西来解析名称。这可以通过 `DNS` 实现，将在另一个章节中讨论。对于本次演示，可以快速将这三个名称添加到 `/etc/hosts` 文件中

```bash
[root@CentOS65 ~#] grep ^192 /etc/hosts
192.168.1.225 choochoo.local
192.168.1.225 chessclub42.local
192.168.1.225 hunter2.local
```

注意，你可能有另一个地址……

### 1.6.3. 重载与验证

在执行 `service httpd reload` 后，网站应该可以通过名称访问了。

```bash
[root@CentOS65 ~]# service httpd reload
Reloading httpd:
[root@CentOS65 ~]# wget http://chessclub42.local/
Resolving chessclub42.local... 192.168.1.225
Connecting to chessclub42.local[192.168.1.225]:80...
HTTP request sent, awaiting response... 200 OK
Length: 1024 bytes
Saving to: index.html
[root@CentOS65 ~]# cat index.html
Welcome to chess club
```

## 1.7. 密码保护的网站

你可以使用 `.htaccess` 文件引用 `.htpasswd` 文件来保护网站中的文件和目录。`htpasswd` 命令可以创建一个包含用户名和（加密）密码的 `.htpasswd` 文件。

此截图为黑客 `cliff` 创建了用户和密码，并使用 `-c` 标志来创建 `.htpasswd` 文件。

```bash
[root@CentOS65 ~]# htpasswd -c /var/www/.htpasswd cliff
New password:
Updating password:
Adding password for user cliff
[root@CentOS65 ~]# cat /var/www/.htpasswd
cliff:$apr
```

`Rob` 也想要你的网站，截图显示了如何向 `.htpasswd` 中添加第二个用户。

```bash
[root@CentOS65 ~]# htpasswd /var/www/.htpasswd rob
New password:
Updating password:
Adding password for user rob
[root@CentOS65 ~]# cat /var/www/.htpasswd
cliff:$apr
rob:$apr
```

`Cliff` 和 `Rob` 选择了相同的密码（`hunter2`），但由于不同的盐（`salts`），这在 `.htpasswd` 文件中是不可见的。我们需要在想要保护的网站的 `DocumentRoot` 中创建一个 `.htaccess` 文件。此截图显示了示例

```bash
[root@CentOS65 ~]# cat /var/www/html/hunter2/.htaccess
AuthName "Members only!"
AuthName Basic
AuthType Basic
require valid-user
```

注意，我们正在保护之前创建的 9000 端口的网站。因为我们之前创建了 9000 端口的网站，我们需要在网站的 `DocumentRoot` 中创建一个 `.htaccess` 文件。此截图显示了示例

```
[root@CentOS65 ~]# cat /var/www/html/hunter2/.htaccess
AuthName "Members only!"
AuthName Basic
AuthType Basic
require valid-user
```

注意，我们在保护之前创建的 9000 端口的网站。并且因为我们之前创建了 9000 端口的网站，我们需要在 `httpd.conf` 中调整某些参数。

```bash
[root@CentOS65 ~]# cat /var/www/html/hunter2/.htaccess
AuthName "Members only!"
AuthName Basic
AuthType Basic
require valid-user
```

## 1.8. Apache 故障排除

当 `Apache` 重启时，它会告诉你哪里出错了。

```bash
[root@CentOS65 ~]# service apache2 restart
Syntax error on /etc/httpd/conf/httpd.conf at line 28: <VirtualHost> not closed.
Syntax error on /etc/httpd/conf/httpd.conf at line 1: <VirtualHost> not closed.
```

## 1.9. 虚拟主机示例

以下是一个虚拟主机配置示例。

```apache
<VirtualHost 83.276.245:80>
ServerName cobbatt.be
ServerAlias www.cbatt.be
DocumentRoot /home/paul/public_html
ErrorLog /home/paul/logs/error_log
CustomLog /home/paul/logs/access_log common
ScriptAlias /cgi-bin/ /home/paul/cgi-bin/
<Directory /home/paul/public_html>
Options IncludesSymLinks
allow from all
</Directory>
ErrorDocument 404 http://www.cbatt.be/cbatt.php
</VirtualHost>
```

## 1.10. 别名与重定向

`Apache` 支持目录的别名，如下所示：

```apache
Alias /paul/ "/home/paul/public_html/"
```

同样，内容可以重定向到另一个网站或 `Web` 服务器

```apache
Redirect permanent foo http://www.foo.com/bar
```

## 1.11. 关于 .htaccess 的更多信息

你可以使用 `.htaccess` 进行更多操作。一个例子是使用 `.htaccess` 防止某些域名访问你的网站。就像在本例中，某些来源被网站阻止了：



```apache
# Options +followsymlinks
RewriteEngine On
RewriteCond %{HTTP_REFERER} ^://(www\.)buy-adipex.fw.nu.*$ [OR]
RewriteCond %{HTTP_REFERER} ^://(www\.)buy-levitra.asso.we.*$ [NC,OR]
RewriteCond %{HTTP_REFERER} ^://(www\.)buy-tramadol.fw.nu.*$ [NC,OR]
RewriteCond %{HTTP_REFERER} ^://(www\.)buy-viagra.lookin.at.*$ [NC,OR]
RewriteCond %{HTTP_REFERER} ^://(www\.)?www.healthinsurancehelp.net.*$ [NC]
RewriteRule .* - [F]
```

## 1.13. Debian 上的自签名证书

以下是关于在 Debian 7 上使用自签名证书设置 `Apache2` 的简快速指南。

这些包可能已经安装了。

```
root@debian:~# aptitude install apache2 openssl
No packages will be installed, upgraded, or removed.
0 packages upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
Need to get 0 B of archives. After unpacking 0 B will be used.
```

创建一个目录来存储证书，并使用 `openssl` 创建一个有效期为 999 天的自签名证书。

```
root@debian:~# mkdir /etc/ssl/localcerts
root@debian:~# openssl req -new -x509 -days 999 -nodes -out /etc/ssl/local/certs/apache.pem -keyout /etc/ssl/localcerts/apache.key
Generating a 2048-bit RSA key
...
writing new private key to '/etc/ssl/localcerts/apache.key'
You are asked to be enter information that will be incorporated
in your certificate request.
What you are asked to enter what is called a Distinguished Name or a DN.
There are a few fields that you can leave blank
For some fields there will be a default value
If you enter ''', the field will be left blank.
```

国家名称（字母代码）`[AU]:BE`

州或省名称（全名）`[Some-State]:Antwerp`

本地名称（例如，城市）：`Antwerp`

组织名称（例如，公司）`[Internet Widg Pty Ltd]:linux-training.be`

组织单位名称（例如，部门）`[]`

通用名称（例如，服务器 FQDN 或您的名称）`[:Paul`

邮箱地址 `[]`

一点点安全性并无害处。

```
root@debian:~# chmod 600 /etc/ssl/localcerts/apache.key
root@debian:~# ls -l /etc/ssl/localcerts
```

## 2.2. 安装 squid

此截图显示了如何使用 `aptitude` 在 Debian 上安装 `squid`。如果你使用的是 Red Hat/CentOS，请使用 `yum`。

```
root@debian:~# aptitude install squid
The following NEW packages will be installed:
squid-common(a) squid-langpack(a)
0 packages upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to to get 1,513 kB of archives. After unpacking 4,540 kB will be used.
Do you want to continue? [Y/n]
... truncated...
Setting up squid-langpack (20160616-1)
Setting up squid-common (2.7.STABLE94.1)
Setting up squid (2.7.STABLE94.1)
Creating squid spool directory structure
2014/08/01 15:19:31 Creating Swap Directories
Restarting Squid HTTP proxy: squid.
```

`squid` 的主配置文件是 `/etc/squid/squid.conf`。该文件详细解释了每一个参数。

```
root@debian:~# wc -l /etc/squid/squid.conf
4948 /etc/squid/squid.conf
```

## 2.3. 端口 3128

默认情况下，`squid` 代理服务器将监听端口 `3128`。

```
root@debian:~# grep "port" /etc/squid/squid.conf
http_port 3128
root@debian:~#
```

## 2.4. 启动与停止

你可以像截图所示，使用标准的服务命令管理 `squid`。

```
root@debian:~# service squid start
Starting Squid HTTP proxy: squid.
root@debian:~# service squid restart
Restarting Squid HTTP proxy: squid.
root@debian:~# service squid status
squid is running.
root@debian:~# service squid stop
Stopping Squid HTTP proxy: squid.
root@debian:~#
```

## 2.5. 客户端代理设置

若要在 `Firefox` 或 `Iceweasel` 中启用代理服务器，请进入“编辑偏好”并如截图所示进行配置（将 `192.168.1.60` 替换为代理服务器的 IP 地址）。

![](img/1d499a6177836f6f088a9e2a53e11a14_42_0.png)

测试开启代理后内部运行正常。同时也测试在代理服务器上执行 `service squid stop` 命令后，是否会收到类似截图所示的消息。

![](img/1d499a6177836f6f088a9e2a53e11a14_42_1.png)

若要用 `Google` `Chrome`（或 Debian `Chromium`）启用代理，请按如下命令行方式启动程序：

```
paul@debian7:~$ chromium --proxy-server='192.168.1.60:3128'
```

使用 `service squid stop` 禁用代理会导致类似此所示的错误信息。

![](img/1d499a6177836f6f088a9e2a53e11a14_43_0.png)

## 2.6. 倒置图像

代理服务器位于你的浏览器和互联网之间。除了缓存互联网数据（代理服务器的原始功能）以及基于网页内容的防火墙限制外，代理服务器处于一个完美的位置，可以允许你访问的网页。

你可以对网页进行更改（或移除某些广告），或者像我们在本例中做的那样：更改所有图像使其倒置。

服务器需要命令行工具来处理图像，以及一个使用这些工具的 `perl` 脚本（使用 `wget` 下载图像并使用 `apache` 服务）。在本例中我们使用了 `imagemagick`（它提供了转换和修改工具）。

```
root@debian:~# aptitude install imagemagick wget apache2
--truncated...
output truncated...
root@debian7:~# dpkg -s $(which mogify)
imagemagick: /usr/bin/mogify
debian7:~#
```

下方显示的 `perl` 脚本可以在多个网站上找到，我没有找到作者。不过它是一个非常简单的脚本，使用 `wget` 和 `mogify` 下载图像（`.jpg` 和 `.png`），将它们翻转并存储在 `/var/www/`。



## 2.6. 图像翻转脚本

```bash
root@debian7:~# cat /usr/local/bin/flip.pl
$count = 0;
$pid = $$;
while (<>) {
	chomp($_);
	if ($1 =~ /\.*jpg$/i) {
		$url = $1;
		system("/usr/bin/wget", "-q", "-O", "/var/www/images/$count.jpg");
		system("/usr/bin/mogify", "-flip", "/var/www/images/$count.jpg");
		print("http://127.0.0.1/images/$count.jpg\n");
	} elsif ($1 =~ /\.*gif$/i) {
		$url = $1;
		system("/usr/bin/wget", "-q", "-O", "/var/www/images/$count.gif");
		system("/usr/bin/mogify", "-flip", "/var/www/images/$count.gif");
		print("http://127.0.0.1/images/$count.gif\n");
	} elsif ($1 =~ /\.*png$/i) {
		$url = $1;
		system("/usr/bin/wget", "-q", "-O", "/var/www/images/$count.png");
		system("/usr/bin/mogify", "-flip", "/var/www/images/$count.png");
		print("http://127.0.0.1/images/$count.png\n");
	} else {
		print("\n");
	}
	$count++;
}
```

在 `/etc/squid/squid.conf` 中更改或添加以下行：

```
http_access allow localnet
http_port 3128 transparent
```

## 2.7. /var/log/squid

`squid` 的标准日志位置是 `/var/log/squid`。

脚本 `/usr/local/bin/flip.pl` 使用 `/var/www/images`，并且应该被 `squid` 服务器（使用用户 `proxy`）和 `apache2` 服务器（使用 `www-data`）访问。截图显示如何创建此目录、设置权限并让用户加入组。

```
root@debian7:~# mkdir /var/www/images
root@debian7:~# chown www-data /var/www/images
root@debian7:~# chmod 755 /var/www/images
root@debian7:~# usermod -aG proxy www-data
root@debian7:~# usermod -aG proxy
```

重启 `squid` 和 `apache2` 后测试运行正常。(img/1d499a6177836f6f088a9e2a53e11a14_45_0.png)

## 2.8. 访问控制

默认 `squid` 设置只允许 `localhost`。要为私网络范围启用访问，请在 `squid.conf` 中查找“INSERT YOUR RULE(S)”句子并添加类似下方所示的两行。

```
# INSERT YOUR RULE(S) TO ALLOW ACCESS FROM CLIENTS
acl company_network src 192.168.1.0/24
http_access allow company_network
```

## 2.9. 测试 squid

首先，确保运行中的 `squid` 可以访问互联网。

```
root@RHEL4 ~ # wget -q http://linux-training.be/index.html
root@RHEL4 ~ # ls -l index.html
-rw-r--r-- 1 root 2269 Sep 18 13:18 index.html
```

然后配置浏览器或客户端使用代理服务器，或者你可以为命令行程序设置 `HTTP_PROXY` 变量指向代理。

```
root@fedora ~ # export HTTP_PROXY=http://192.168.1.39:8080
root@ubuntu ~ # export http_proxy=http://192.168.1.39:8080
```

可以使用 `wget -q` 测试客户端以简化截图。

```
root@RHEL5 ~ # wget > /resolv.conf
root@RHEL5 ~ # wget -q http://www.linux-training.be/index.html
root@RHEL5 ~ # ls -l index.html
-rw-r--r-- 1 root 2269 Sep 18 20:08 index.html
```

## 2.10. 域名解析

你需要在 `squid` 上进行域名解析，但客户端不需要。

```
paul@RHEL5 ~ $ wget http://grep.be
--14:35:44-- grep.be
Resolving grep.be... failed: Temporary failure in name resolution.
paul@RHEL5 ~ $ export http_proxy=http://192.168.1.39:8080
paul@RHEL5 ~ $ wget http://grep.be
--14:35:49-- http://grep.be/
```

Connecting to `192.168.1.39:8080`... connected.

Proxy request sent, awaiting response... `200 OK`

Length: `5390 (5.3K) [text/html]`

Saving to: `'index.html.1'`

```
100%[=================>] 5,390 .-K/s  in 0.1s

14:38:29 (54.8 KB/s)  - 'index.html' saved [5390/5390]

[paul@RHEL5 ~]$
```

## Introduction to Squid

## Part II. MySQL Database

# Table of Contents

*   3. Introduction to SQL using MySQL ................................................................... 43
*   3.1. Installing MySQL ................................................................. 44
*   3.2. Accessing MySQL ................................................................. 45
*   3.3. MySQL Databases ................................................................. 47
*   3.4. MySQL Tables ................................................................. 49
*   3.5. MySQL Records ................................................................. 51
*   3.6. Joining Two Tables ................................................................. 54
*   3.7. MySQL Triggers ................................................................. 55

# 第3章：使用 MySQL 介绍 SQL

`MySQL` 是一个理解结构化查询语言（SQL）的数据库服务器。`MySQL` 由瑞典公司 `MySQL AB` 开发。首次发布于 1995 年。2008 年，`MySQL AB` 被 `Sun Microsystems` 收购（现由 `Oracle` 所有）。

`MySQL` 在结合 `php` 和 `apache` 使用的网站中（LAMP 服务器中的 `m`）非常流行，但 `MySQL` 也被用于拥有巨大数据库的组织，如 `Facebook`、`Flickr`、`Google`、`Nokia`、`Wikipedia` 和 `Youtube`。



本章将通过在本地 `mysql` 服务器上创建和使用小型数据库、表、查询和简单的触发器来教你 `sql`。

## 3.1. 安装 `mysql`

在 Debian/Ubuntu 上，你可以使用 `aptitude install mysql-server` 来安装 `mysql` 服务端和客户端。

```
root@ubuntu204#$ aptitude install mysql-server
The following NEW packages will be installed:
libdcb0-mysql-perl(a) libdcb0-perl(a) libhtmml-template-perl(a)
libnet-daemon-perl(a) libmysqlprpc-perl(a) mysql-client-5.5(a)
mysql-client-core-5.5(a) mysql-server mysql-server-5.5(a)
mysql-server-core-5.5(a)
0 packages upgraded, 10 newly installed, 0 to remove and 1 not upgraded.
Need to get 25.5 MB of archives. After unpacking 84.4 MB will be used.
Do you want to continue? [Y/n]
```

在安装过程中，系统会要求你为 `root` `mysql` 用户提供密码，记住这个密码（或像我一样使用 `hunter2`）。

要验证已安装的版本，在 Debian/Ubuntu 上使用 `dpkg -l`。此截图显示版本为 5.0。

```
root@ubuntu204#$ dpkg -l mysql-server | tail -1 | tr -s ' ' | cut -c-72
i mysql-server 5.5.24-0ubuntu0.12.04.1 MySQL database server (metapacka)
```

在 Red Hat/Fedora/CentOS 上，执行 `rpm -q` 获取 `MySQL` 的版本信息。

```
[paul@RHEL52 ~]$ rpm -q mysql-server
mysql-server-5.0.45-7.el5
```

你需要 5.0 版本来使用触发器。

## 3.2. 访问 `mysql`

### 3.2.1. Linux 用户

`mysql` 的安装会在 `/etc/passwd` 中创建一个用户账户并在 `/etc/group` 中创建一个组账户。

```
kevin@ubul204:~$ tail -1 /etc/passwd
mysql:x:120:131:MySQL Server,,,,nonexistent:/bin/false
kevin@ubul204:~$ tail -1 /etc/group
mysql:x:131:
```

`mysql` 守护进程 `mysql` 将以该用户和组的凭据运行。

```
root@ubul204~$ ps -eo uid,gid,user,group,comm | grep mysql
120 mysql 131 mysqld
```

### 3.2.2. `mysql` 客户端应用程序

你现在只需输入 `mysql -u root -p` 即可在命令行中使用 `mysql`，系统会提示你输入（`mysql` `root` 账户）的密码。在下面的截图中用户退出了 `mysql` 控制台。

```
root@ubul204~$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection is id 43
Server version: 5.5.24-Ubuntu00.12.04.1 (Ubuntu)
```

Copyright (c) 2000, 2011, Oracle and/or its affiliates. 保留所有。

`Oracle` 是 `Oracle` 公司和/或其关联公司的注册商标。其他名称可能是其各自所有者的商标。

输入 `help`; 或 `h` 获取帮助。输入 `\c'` 清空当前输入语句。

```
mysql> exit
Bye
```

你也可以将密码写在命令行中，但那样并不安全。任何可以访问你 `bash` 历史记录的人都能读取你的 `mysql` 密码。

```
root@ubul204~$ mysql -u root -phunter2
Welcome to the MySQL monitor. Commands end with ; or \g.
...
```

### 3.2.3. `~/.my.cnf`

你可以在主目录下的隐藏文件 `.my.cnf` 中保存配置。在截图中，我们将 `root` 用户和密码放在了 `.my.cnf` 中。

```
kevin@ubuntu1204:~$ pwd
/home/kevin
kevin@ubuntu1204:~$ cat .my.cnf
[client]
user=root
password=hunter2
kevin@ubuntu1204:~-$
```

这使得我们只需输入 `mysql` 即可以 `root` 用户身份登录。

```
kevin@ubuntu1204:~$ mysql monitor.
Welcome to the MySQL monitor. Commands end with ; or \ \
Your MySQL connection id is 56
Server version: 5.5.24-Ubuntu00.12.04.1 (Ubuntu)
```

### 3.2.4. `mysql` 命令行客户端

你可以使用 `mysql` 命令查看数据库并在其上执行 `SQL` 查询。截图向你展示了如何操作。

在这里执行 `show databases` 命令。每个命令必须以分隔符结束。默认分隔符是分号。

```
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema|
| test               |
+--------------------+
4 rows in (0.00 sec)
```

## 3.4.3. 描述表

要查看表结构的描述，请执行所示的 `describe $tablename` 命令。

```
mysql> describe country;
+-------------+------+------+------+----------+
| Field        | Type        | Null | Key | Default | Extra |
+-------------+------+------+------+----------+
| countrycode | char(3)     |      | PRI | NULL    |          |
| countryname | varchar(70) | NO   |     | NULL    |          |
| population  | int(11)    | YES |     | NULL    |          |
| countrycapital| varchar(50)| YES |     | NULL    |          |
+-------------+------+------+------+----------+
4 rows in set (0.00 sec)
```

## 3.4.4. 删除表

要从数据库中删除一个表，请执行所示的 `drop table $tablename` 命令。

```
mysql> drop table country;
Query OK, 0 rows affected (0.00 sec)
```

## 3.5. `mysql` 记录

### 3.5.1. 创建记录

使用 `insert` 向表中输入数据。截图显示了几个 `insert` 语句，它们根据数据在语句中的位置插入不同的值。

```
mysql> insert into country values ('BE', 'Belgium', '11000000', 'Brussels');
Query OK, 1 row affected (0.05 sec)
```

```
mysql> insert into country values ('DE', 'Germany', '82000000', 'Berlin');
Query OK, 1 row affected (0.05 sec)
```



```
mysql> insert into country values ('JP', 'Japan', '128000000', 'Tokyo');
Query OK, 1 row affected (0.05 sec)
```

一些管理员倾向于使用大写 `sql` 关键字。`mysql` 客户端接受两种形式。

```
mysql> INSERT INTO COUNTRY VALUES ('FR', 'France', '64000000', 'Paris');
Query OK, 1 row affected (0.00 sec)
```

注意，当使用重复的 `primary key`（主键）时会得到错误。

```
mysql> insert into country values ('DE', 'Germany', '82000000', 'Berlin');
ERROR 1062 (23000): Duplicate entry 'DE' for key 'PRIMARY'
```

### 3.5.2. 查看所有记录

下面是一个通过简单的 `select` 查询查看表内容的示例。

```
mysql> select * from country;
```

| countrycode | countryname | population | countrycapital |
| :--- | :--- | :--- | :--- |
| BE | Belgium | 11000000 | Brussels |
| CN | China | 14000000 | Beijing |
| DE | Germany | 82000000 | Berlin |
| FR | France | 64000000 | Paris |
| IN | India | 130000000 | New Delhi |
| JP | Japan | 128000000 | Tokyo |
| MX | Mexico | 113000000 | Mexico City |
| US | United States | 313000000 | Washington |

```
8 rows in set (0.00 sec)
```

### 3.5.3. 更新记录

考虑以下 `insert` 语句。西班牙的首都是马德里，不是巴塞罗那。

```
mysql> insert into country values ('ES','Spain','48000000','Barcelona');
Query OK, 1 row affected (0.08 sec)
```

使用 `update` 语句可以更新记录。

```
mysql> update country set countrycapital='Madrid' where countrycode='ES';
Query OK, 1 row affected (0.07 sec)
Rows matched: 1 Changed: 0
```

我们可以使用 `select` 语句来验证这一点。

```
mysql> select * from country;
```

| countrycode | country | population | countrycapital |
| :--- | :--- | :--- | :--- |
| BE | Belgium | 11000000 | Brussels |
| CN | China | 14000000 | Beijing |
| DE | Germany | 82000000 | Berlin |
| ES | Spain | 48000000 | Madrid |
| FR | France | 64000000 | Paris |
| IN | India | 130000000 | New Delhi |
| JP | Japan | 128000000 | Tokyo |
| MX | Mexico | 113000000 | Mexico City |
| US | United States | 313000000 | Washington |

```
9 rows in set (0.00 sec)
```

### 3.5.4. 查看选定的记录

通过 `select` 语句中的子句（`clause`），你可以指定想要查看的记录。

```
mysql> SELECT * FROM country WHERE countrycode='ES';
```

| countrycode | country | population | countrycapital |
| :--- | :--- | :--- | :--- |
| ES | Spain | 48000000 | Madrid |

```
1 row in set (0.00 sec)
```

另一个 `where` 子句的示例。

```
mysql> select * from country where country='Spain';
```

| countrycode | country | population | countrycapital |
| :--- | :--- | :--- | :--- |
| ES | Spain | 48000000 | Madrid |

### 3.5.5. where 子句中的主键

表的 `primary key` 唯一标识表中的每一行。在 `where` 子句中使用另一个字段时，可能会获取多行。

```
mysql> insert into country values ('EG','Egypt','820000','Cairo');
Query OK, 1 row affected (0.33 sec)

mysql> select * from country where population='820000';
```

| countrycode | countryname | population | countrycapital |
| :--- | :--- | :--- | :--- |
| DE | Germany | 820000 | Berlin |
| EG | Egypt | 820000 | Cairo |

```
2 rows in set (0.00 sec)
```

### 3.5.6. 记录排序

我们知道 `select` 允许查看表中的所有记录。考虑这个表。

```
mysql> select countryname,population from country;
```

| countryname | population |
| :--- | :--- |
| Belgium | 11000000 |
| China | 14000000 |
| Germany | 8200000 |
| Egypt | 820000 |
| Spain | 48000000 |
| France | 640000 |
| India | 13000000 |
| Japan | 12800000 |
| Mexico | 11300000 |
| United States | 31300000 |

```
10 rows in set (0.00 sec)
```

使用 `order by` 子句，我们可以更改记录呈现的顺序。

```
mysql> select countryname,population from country order by countryname;
```

| countryname | population |
| :--- | :--- |
| Belgium | 11000000 |
| China | 14000000 |
| Germany | 8200000 |
| Egypt | 820000 |
| France | 640000 |
| India | 13000000 |
| Japan | 12800000 |
| Mexico | 11300000 |
| Spain | 48000000 |
| United States | 31300000 |

```
10 rows in set (0.00 sec)
```

### 3.5.7. 记录分组

考虑这张人员表。截图显示了如何使用 `avg` 函数计算平均值。

```
mysql> select * from people;
```



# SQL MySQL 介绍

## 3.5. 查询记录

```
mysql> select * from people;
```

| Name | Field | birthyear | countrycode |
| :--- | :--- | :--- | :--- |
| Barack Obama | politics | 1961 | US |
| Deng Xiaoping | politics | 1904 | CN |
| Guy Verhofstadt | politics | 1953 | BE |
| Justine Henin | tennis | 1982 | BE |
| Kim Clijsters | tennis | 1983 | BE |
| Li Na | tennis | 1982 | CN |
| Liu Yang | astronaut | 1978 | CN |
| Serena Williams | tennis | 1981 | US |
| Venus Williams | tennis | 1980 | US |

```
9 rows in set (0.00 sec)
```

使用 `select` 语句查询特定字段：

```
mysql> select Field, AVG(birthyear) from people;
```

| Field | AVG(birthyear) |
| :--- | :--- |
| politics | 1967.1111111111 |

```
1 row in set (0.00 sec)
```

使用 `group by` 子句，我们可以获得每个字段的平均值。

```
mysql> select Field, AVG(birthyear) from people group by Field;
```

| Field | AVG(birthyear) |
| :--- | :--- |
| astronaut | 1978 |
| politics | 1939.333333333333 |
| tennis | 1981.6 |

```
3 rows in set (0.00 sec)
```

### 3.5.8. 删除记录

你可以使用 `delete` 从表中永久地删除一条记录。

```
mysql> delete from country where countryname='Spain';

Query OK, 1 row affected (0.06 sec)
```

验证删除结果：

```
mysql> select * from country where countryname='Spain';

Empty set (0.00 sec)
```

## 3.6. 连接两个表

### 3.6.1. 内连接 (inner join)

通过 `inner join`，你可以从两个表中提取值并将它们合并为一个结果。在查看此 `inner join` 截图时，考虑上一节中的 `country` 表和 `people` 表。

```
mysql> select Name,Field,countryname
-> from country
-> inner join people on people.countrycode=country.countrycode;
```

| | 宇航员 | 中国 |
|---|---|---|
| Serena Williams | 网球 | 美国 |
| Venus Williams | 网球 | 美国 |

集合包含 9 行 (0.00 秒)

此**内连接（inner join）**将只显示两个表中 `countrycode` 均匹配的记录。

### 3.6.2. 左连接 (left join)

**左连接（left join）**与**内连接**不同，它会提取左表中的所有行，无论右表中是否有匹配项。

| 姓名 (Name) | 字段 (Field) | 国家名称 (countryname) |
|---|---|---|
| Guy Verhofstadt | 政治 | 比利时 |
| Justine Henin | 网球 | 比利时 |
| Kim Clijsters | 网球 | 中国 |
| Deng Xiaoping | 政治 | 中国 |
| Liu Yang | 宇航员 | 中国 |
| NULL | NULL | 德国 |
| NULL | NULL | 埃及 |
| NULL | NULL | 西班牙 |
| NULL | NULL | 日本 |
| NULL | NULL | 墨西哥 |
| Barack Obama | 政治 | 美国 |
| Serena Williams | 网球 | 美国 |
| Venus Williams | 网球 | 美国 |

集合包含 16 行 (0.00 秒)

我们可以看到，即使某些国家在人员表中没有匹配记录，它们仍然存在。

## 3.7. MySQL 触发器 (triggers)

### 3.7.1. 使用之前触发器 (before trigger)

考虑**创建表（create table）**命令。最后一个字段 `(amount)` 是两个字段 `unitprice`（单价）和 `unitcount`（数量）相积。

```
mysql> create table invoices (
  -> id char(8) NOT NULL,
  -> customerid char(8) NOT NULL,
  -> unitprice int,
  -> unitcount smallint,
  -> amount int );

Query OK, 0 rows affected (0.00 sec)
```

我们可以通过使用**之前触发器（before trigger）**让 `mysql` 执行计算。下面的截图显示了触发器的创建，它通过将即将插入的两个字段相乘来计算金额。

```
mysql> create trigger total_amount BEFORE INSERT ON invoices

-- 对于每行设置 new.amount = new.unitprice * new.unitcount ;

Query OK, 0 rows affected (0.02 sec)
```

在这里，我们通过插入一条新记录（不提供总金额）来验证触发器工作。

```
mysql> insert into invoices values ('20090526','ABC','199','10',''');

Query OK, 1 row affected (0.02 sec)
```

查看记录可以证明触发器正在正常工作。

```
mysql> select * from invoices;

+------------------------------------------+
| id | customerid | unitprice | unitcount | amount |
+----+--------------------+------+----------+
| 20090526 | ABC | 199 | 10 | 1990 |
+------------------------------------------+

1 row set (0.00 sec)
```

### 3.7.2. 移除触发器

当不再需要触发器时，可以使用 `drop trigger` 命令将其删除。

```
mysql> drop trigger total_amount;

Query OK, 0 rows affected (0.00 sec)
```



# 第三部分. DNS 服务器

## 目录

- 4. DNS 介绍 ................................................................................ 59
- 4.1. 关于 dns ............................................................................................ 60
- 4.2. dns 命名空间 ....................................................................... 63
- 4.3. 仅缓存服务器 ................................................................... 68
- 4.4. 权威 dns 服务器 ................................................................ 71
- 4.5. 主、从服务器 ................................................................ 71
- 4.6. 区域传输 ................................................................................. 71
- 4.7. 主与从 ..................................................................... 73
- 4.8. SOA 记录 ....................................................................................... 73
- 4.9. 全量或增量区域传输 ................................................... 74
- 4.10. dns 缓存 ...................................................................................... 75
- 4.11. 正向备份区域示例 ................................................ 76
- 4.12. 示例：仅缓存 DNS 服务器 ........................................ 77
- 4.13. 示例：带有转发器的仅缓存 ................................................ 79
- 4.14. 示例：主权威服务器 ................................................ 81
- 4.15. 示例：一个 DNS 服务器 ................................................................. 85
- 4.16. 练习：dns ...................................................................... 87
- 4.17. 解答：dns ...................................................................... 88
- 5. 高级 DNS ................................................................................ 89
- 5.1. 示例：DNS 轮询 (robin) ................................................................ 90
- 5.2. 委托 ................................................................. 91
- 5.3. 示例：DNS 委托 ................................................................. 92
- 5.4. 示例：分区域解析 (split-horizon) ................................................. 94
- 5.5. dns 主题 ................................................................. 96

# 第 4 章 DNS 介绍

DNS（域名命名系统）是互联网的核心组件之一。它将人类易读的域名（如`google.com`）转换为机器易读的 IP 地址。没有 DNS，我们必须记住复杂的数字 IP 才能访问网站。DNS 就像是互联网的电话簿。

DNS 的工作原理：当你在浏览器中输入域名时，计算机会向 DNS 服务器查询该域名对应的 IP 地址。如果本地缓存中没有该记录，它会向本地 DNS 服务器请求。如果本地服务器也没有，它会向递归解析器发送请求，层层向上查找直到找到权威服务器。

## 4.1 关于 DNS (About DNS)

DNS 全称为域名命名系统（Domain Name System）。它。在 DNS 命名空间中，域名被组织成一个层层次的树状结构。

### 4.1.4 `/etc/resolv.conf`

客户端计算机需要知道 DNS 服务器的 IP 地址以便向其发送查询。这可以通过 DHCP 服务器提供，也可以手动输入。

Linux 客户端将此信息存储在`/etc/resolv.conf`文件中。

## 4.2 DNS 命名空间 (DNS Namespace)

DNS 命名空间是一个层次结构。顶层是根区域（用点`.`表示），下面是顶级域名（TLD，如`.com`, `.org`, `.cn`），然后是二级域名（如`example.com`）。

## 4.3 仅缓存服务器 (Caching Only Servers)

仅缓存服务器（通常称为递归解析器）不存储原始记录，它们只存储从其他服务器获取的响应。

## 4.4 权威 DNS 服务器 (Authoritative DNS Servers)

权威 DNS 服务器持有特定区域域名的实际记录。它是 DNS 查询的终点。

## 4.5 主服务器和从服务器 (Primary and Secondary)

主服务器（`Primary`）是区域记录的源头。从服务器（`Secondary`）是主服务器的副本，用于提供冗余和高可用性。

## 4.6 区域传输 (Zone Transfers)

区域传输是将主服务器上的区域数据同步到从服务器的过程，以确保数据一致。

## 4.7 主与从 (Master and Slave)

在旧的术语中，主（`Master`）对应主服务器，从（`Slave`）对应从服务器。现代术语倾向于使用主/从（`Primary`/`Secondary`）。

## 4.8 SOA 记录 (SOA Record)

`SOA`（起始权威机构）记录包含该区域的关键元数据，如管理员邮箱、序列号、刷新和过期时间等。

## 4.9 全量或增量区域传输 (Full or Incremental Zone Transfers)

全量传输发送整个区域文件，而增量传输仅发送自上次传输以来更改的部分。

## 4.10 DNS 缓存 (DNS Cache)

DNS 缓存用于存储最近查询过的域名记录，以减少查询次数并提高访问速度。缓存可以存在于浏览器、操作系统或本地 DNS 服务器中。

## 4.11 正向备份区域示例 (Forward Backup Zone Example)

此处展示了如何配置正向解析区域以作为主服务器的备份。

## 4.12 示例：仅缓存 DNS 服务器 (Example: Caching Only DNS Server)

演示了如何配置一个仅负责缓存查询的 DNS 服务器。

## 4.13 示例：带有转发器的仅缓存 (Example: Caching Only with Forwarder)

展示了如何配置将未命中的请求转发到上游服务器。

## 4.14 示例：主权威服务器 (Example: Primary Authoritative Server)

展示了配置主权威服务器的步骤。

## 4.15 示例：一个 DNS 服务器 (Example: A DNS Server)

提供了一个完整的 DNS 服务器配置示例。

## 4.16 练习：dns (Practice: DNS)

供读者练习的 DNS 配置的练习题。

## 4.17 解答：dns (Solution: DNS)

提供上述练习的详细解答。

# 5 高级 DNS (Advanced DNS)

探讨更复杂的 DNS 策略和技术。

## 5.1 示例：DNS 轮询 (Example: DNS Robin)

展示如何通过 DNS 轮询在多个服务器之间实现负载均衡。

## 5.2 委托 (Delegation)

解释 DNS 如何将特定域名的查询委托给子区域服务器。

## 5.3 示例：DNS 委托 (Example: DNS Delegation)

提供配置 DNS 委托记录的示例。

## 5.4 示例：分区域解析 (Example: Split-horizon)

展示如何根据请求来源（内部或外部）为同一个域名返回不同的 IP 地址。

## 5.5 dns 主题 (DNS Topics)

关于 DNS 相关话题的进一步讨论。



在 `/etc/resolv.conf` 文件中查看 DNS 配置：

```
root@debian7:~# cat /etc/resolv.conf

domain linux-training.be

search linux-training.be

nameserver 192.168.1.42

root@debian7~#
```

你可以手动更改此文件中的 IP 地址以使用另一个 DNS 服务器。例如，Google 在 `8.8.8.8` 和 `8.8.4.4` 提供了公共公共名称服务器。

更改后的配置示例：

```
root@debian7:~# cat /etc/resolv.conf

nameserver 8.8.8.8

root@debian7~#
```

请注意，在 DHCP 客户端上，此值在 DHCP 租约更新时可能会被覆盖。

## 4.2. dns 命名空间

### 4.2.1. 层次结构

**DNS 命名空间**是一个分级的树形结构，**根服务器**（又称点服务器）位于顶端。**根服务器**通常用一个点表示。

![](img/1d499a6177836f6f088a9e2a53e11a14_70_0.png)

**根服务器**下方是**顶级域名**（简称 TLD）。

TLD 的数量比图片显示的要多。目前大约有 200 个国家拥有一个 TLD。还有几个通用的 TLD，如 `.com`、`.edu`、`.org`、`.gov`、`.net`、`.mil`、`.int` 以及最近的 `.aero`、`.info`、`.museum` 等。

### 4.2.2. 根服务器

互联网上有13 台**根服务器**，它们被命名为 A 到 M。记者经常将这些服务器称为**互联网的主服务器**，因为如果这些服务器宕机，就没有人能（使用名称）连接到网站。

根服务器并不是 13 台物理机器，而是要多得多。例如，**F 根服务器**由 46 台物理机器组成，它们都表现得一台机器（使用任播技术）。

```
http://root-servers.org
http://f.root-servers.org
http://en.wikipedia.org/wiki/Root_nameserver
```

### 4.2.3. 根提示 (root hints)

每个 DNS 软件都附带了一份根提示列表，用于定位根服务器。

此截图显示了 bind 9.8.4 自带的根提示文件。

```
root@debian7:~# grep -w 'A' /etc/bind/db.root

A.ROOT-SERVERS.NET.      3600000 A 198.41.0.4
B.ROOT-SERVERS.NET.      3600000 A 192.228.79.201
C.ROOT-SERVERS.NET.      3600000 A 192.33.4.12
D.ROOT-SERVERS.NET.      3600000 A 199.77.91.13
E.ROOT-SERVERS.NET.      3600000 A 192.203.230.10
F.ROOT-SERVERS.NET.      3600000 A 192.5.24.21
G.ROOT-SERVERS.NET.      3600000 A 192.112.96.4
H.ROOT-SERVERS.NET.      3600000 A 128.63.2.53
I.ROOT-SERVERS.NET.      3600000 A 192.36.148.17
J.ROOT-SERVERS.NET.      3600000 A 192.58.128.30
K.ROOT-SERVERS.NET.      3600000 A 193.0.14.129
L.ROOT-SERVERS.NET.      3600000 A 199.78.13.42
M.ROOT-SERVERS.NET.      3600000 A 202.12.27.33

root@debian7:~#
```

### 4.2.4. 域名

顶级域名下方是域名。域名可以有子域名（也称为子域）。

这张图片显示了如 `google.com`、`chess.com`、`linux-training.be` 等 DNS 域名（还有数百万个）。

![](img/1d499a6177836f6f088a9e2a53e11a14_71_0.png)

DNS 域名注册在 TLD 服务器上，而 TLD 服务器注册在根节点。

### 4.2.5. 顶级域名

根级别下方是**顶级域名**或 **TLD**。最初只定义了七个：

表 4.1. 第一批顶级域名

| 年份 | TLD | 用途 |
|---|---|---|
| 1985 | `.arpa` | 通过 `in-addr.arpa` 进行反向查找 |
| 1985 | `.com` | 商业机构 |
| 1985 | `.edu` | 美国教育机构 |
| 1985 | `.gov` | 美国政府机构 |
| 1985 | `.mil` | 美国军事 |
| 1985 | `.net` | 互联网服务提供商、互联网基础设施 |
| 1985 | `.org` | 非营利组织 |
| 1988 | `.int` | 像 `nato` 这样的国际条约 |

为单个国家定义了国家 **tld**，例如 1985 年英国的 `.uk`、1988 年比利时的 `.be` 以及 1986 年法国的 `.fr`。1998 年定义了一些通用用途的 tld。

表 4.2. 新的通用 tld

| 年份 | TLD | 用途 |
|---|---|---|
| 2002 | `.aero` | 航空相关 |
| 2001 | `.biz` | 商业 |
| 2001 | `.coop` | 合作社 |
| 2001 | `.info` | 信息 |
| 2001 | `.museum` | 博物馆 |
| 2001 | `.name` | 名称 |
| 2004 | `.pro` | 专业版 |
| 2011 | `.travel` | 旅游 |
| 2012 | `.tel` | 通信 |
| 2012 | `.jobs` | 工作 |

### 4.2.6. 完全限定域名 (FQDN)

**完全限定域名**或 **fqdn** 是主机名与其域的组合。例如，如果一个系统是 `gwen`，那么它的完全限定域名就是 `gwen.linux-training.be`。在 Linux 系统上，你可以使用 `hostname` 和 `domain` 命令来验证。

```
root@debian7:~# hostname

debian7

root@debian7:~# fqdn

debian7.linux-training.be

.linux-training.be

root@debian7:~# domain
```

## 4.2.7. DNS 区域 (zones)

**DNS 区域**（zone）是 DNS 树的一部分，由某个服务器（也称为根服务器）授权。该区域涵盖了该域名下的所有记录。下图显示了具有授权权限的区域。

![](img/1d499a6177836f6f088a9e2a53e11a14_72_0.png)

一个 DNS 服务器可以委托其他服务器。

## 4.3.2. 带有转发器的仅缓存服务器

带有**转发器**的**仅缓存服务器**是一种 DNS 服务器，它所有的信息都将从**转发器**处获取。该**转发器**必须是一个**dns 服务器**，例如来自**互联网服务提供商**的**dns 服务器**。

![](img/1d499a6177836f6f088a9e2a53e11a14_77_0.png)

这张图片显示了公司局域网上的**dns 服务器**，它将其**isp**的**dns 服务器**设置为转发器。**如果 dns 服务器的 ip 地址是 `212.71.8.10`，那么在公司**dns 服务器**的 `named.conf` 文件中将发生以下情况：**

```
forwarders {
  212.71.8.10;
}
```

你也可以配置你的**dns 服务器**使其与**条件转发器**协同工作。条件转发器的定义如下。

```
zone "someotherdomain.local" {
  type forwarder;
  forward only;
  forwarders { 10.104.42.1; };
}



### 4.3.3. 迭代或递归查询

`递归查询`是一种`DNS`查询，发起查询的客户端期望得到一个完整的答案（如上述从`Macbook`到`DNS`服务器的粗红色箭头所示）。`迭代查询`是一种`DNS`查询，客户端并不期望得到完整的答案（图中从`DNS`服务器发出的三个黑色箭头）。迭代查询通常发生在名称服务器之间。根名称服务器不响应递归查询。

## 4.4. 权威 DNS 服务器

控制某个区域（`zone`）的`DNS`服务器被称为该区域的**权威 DNS 服务器**。请记住，一个**区域**是**资源记录**的集合。

![](img/1d499a6177836f6f088a9e2a53e11a14_78_0.png)

## 4.5. 主与从

当你为一个区域设置第一台**权威 DNS 服务器**时，它被称为**主 DNS 服务器**。该服务器将拥有一份**区域数据库**的可读可写副本。出于容错、性能或负载均衡的考虑，你可能决定设置另一台对该区域具有权威性的**DNS 服务器**。这就是一台**从 DNS 服务器**。

![](img/1d499a6177836f6f088a9e2a53e11a14_78_1.png)

## 4.6. 区域传输

从服务器通过**区域传输**从主服务器接收区域数据库的副本。区域传输由从服务器定期请求。这些时间间隔定义在**SOA 记录**中。

![](img/1d499a6177836f6f088a9e2a53e11a14_78_2.png)

你可以使用`rndc`强制刷新区域。下面的示例强制执行了`fred.local`区域的传输，并显示了来自`/var/log/syslog`的日志。

```text
root@debian7:~/etc/bind# rndc refresh fred.local
```

```text
root@debian7:/etc/bind# grep fred /var/log/syslog | tail -7 | cut -c38-

zone fred.local/IN: sending notifications (serial 1)

received control channel command 'refresh fred.local'

zone fred.local/IN: Transfer started.

transfer of 'fred.local/IN' from 10.104.109#53: connected using 10.104.33.5737

zone fred.local/IN: transferred 2

transfer of 'fred.local/IN' from 10.104.109#53: completed: 10 records,

zone fred.local/IN: sending notifications (serial 2)

root@debian7:/etc/bind#
```

## 4.7. 主从

向区域添加从级`DNS`服务器时，你会将此服务器配置为主服务器的从服务器。主服务器随后成为从服务器的主服务器。通常主服务器是所有从服务器的主服务器。有时从服务器是另一个从服务器的主服务器。图中`ns1`是主服务器，`ns2`和`ns4`是从服务器，而`ns2`和`ns3`是`ns1`的主服务器，`ns4`是`ns2`的主服务器。

![](img/1d499a6177836f6f088a9e2a53e11a14_80.png)

## 4.8. SOA 记录

`SOA`记录包含一个刷新（`refresh`）值。如果设置为 30 分钟，从服务器将每 30 分钟请求一次区域副本。还有一个重试（`retry`）值，当主服务器未响应时使用的重试值。以下是使用`nslookup`查询`(linux-training.be)``SOA`记录的示例。

```text
root@debian6:~ nslookup

> type=SOA

Server: ns1.linux-training.be

Address: 195.47.215.14

origin: linux-training.be

serial: 2321013

refresh: 14400

retry: 3600

expire: 604800

minimum: 3600
```

只有当区域数据库更新（意味着添加或删除了一个或多个资源记录）时发生区域传输。从服务器与其主服务器的`SOA`记录进行序列号比较。如果两个序列号相同，则不需要更新。如果从服务器的序列号小于主服务器，则请求区域传输。下面是在`wireshark`中捕获的区域传输。

| Time | Source | Destination | Protocol | Info |
|---|---|---|---|---|
| 1 | 000000 | 192.168.1.37 | 192.168.1.35 | DNS | Standard query Seq=0 Win=5040 Len=0 |
| 2 | 006805 | 192.168.1.35 | 192.168.1.37 | DNS | Standard query response Seq=0 ns.copy.paul |
| 3 | 0314067 | 192.168.1.37 | 192.168.1.35 | TCP | 33713 > [ACK] [SYN] Win=5850 Len=0 MS=5 |
| 4 | 0315037 | 192.168.1.37 | 192.168.1.35 | TCP | 33713 > [ACK] [SYN] Win=5151 Win=1 MS=5 |
| 5 | 0501907 | 192.168.1.35 | 192.168.1.37 | TCP | 33713 > domain [ACK] Seq=1 Win=5056 |
| 6 | 0619554 | 192.168.1.37 | 192.168.1.35 | TCP | [TCP segment] = segment of reassembled PDU |
| 7 | 0718359 | 192.168.1.35 | 192.168.1.37 | TCP | 33713 > domain [ACK] Seq=1 Win=5792 Len |
| 8 | 0801111 | 192.168.1.37 | 192.168.1.35 | TCP | 33713 > cobbb.paul, ack=31 |
| 9 | 0918283 | 192.168.1.35 | 192.168.1.37 | DNS | 33713 > domain [ACK] Seq=1 Win=5792 Len |
| 10 | 0919784 | 192.168.1.35 | 192.168.1.37 | DNS | Standard query response Seq=0 ns.cobbb.paul |
| 11 | 1102923 | 192.168.1.37 | 192.168.1.35 | TCP | 33713 > [ACK] Seq=1 Win=5027 Ack= |
| 12 | 12026018 | 192.168.1.37 | 192.168.1.35 | TCP | 33713 > [ACK] Seq=77 Win=295 |
| 13 | 13021011 | 192.168.1.35 | 192.168.1.37 | TCP | 33713 > domain Ack=25 |

## 4.9. 增量区域传输

当发生区域传输时，可以是全量传输也可以是增量传输。这取决于传输的大小。当更改的总大小小于区域的大小时，优先选择增量传输。全量传输使用`axfr`协议，增量传输使用`ixfr`协议。

## 4.10. DNS 缓存

`DNS`是一种缓存协议。当客户端查询本地`DNS`服务器时，如果本地服务器不是该查询的权威，它将在`DNS`树中查找权威服务器。本地服务器首先查询根服务器，然后是顶级服务器，最后是域名服务器。当本地服务器解析查询时，它会将这些信息传递给提交查询的客户端，并并在缓存中保留这些查询的副本。因此，当（另一个）客户端向此服务器提交相同的查询时，它将从缓存中检索这些信息。

## 4.11. 正向查找区域示例

在`/etc/bind/named.conf.local`中设置区域的方法是创建一个指向另一个文件的引区域条目（该另一个文件包含区域数据库）。

以下是`/etc/bind/named.conf.local`中每种配置的示例：

```text
root@debian:-# cat /etc/bind/named.conf.local

//

// 在此处进行本地配置

//

// 如果你的组织中没有使用 1918 区域，

// 请在此处添加它们

// include "/etc/bind/zones.rfc1918";

zone "paul.local" IN {

    type master;

    file "/etc/bind/db.paul.local";

    allow-update { none };

}
```



# 创建区域文件

要创建一个区域，简单的方法是复制现有的区域文件（这比从头开始写要简单）。

```
root@debian:/etc/bind# cp db.empty db.paul.local
```

```
root@debian:/etc/bind# vi db.paul.local
```

这是一个区域文件的示例。

```
root@debian:/etc/bind# cat db.paul.local

; 课堂教学区域

TTL 86400 SOA debian.paul.local. root.paul.local (
    2014100100 ; Serial
    1h ; Refresh
    1h ; Retry
    2h ; Expire
    86400 ) Negative Cache TTL

; 名字服务器
    IN NS nsl
    IN NS debianpaul
    IN NS debian7

; 服务器
debian IN A 10.104.33.30
debianpaul IN A 10.104.33.30
debian7 IN A 10.104.33.30
nsl IN A 10.104.33.30
www IN A 10.104.33.30
```

## 4.12. 示例：仅作为缓存的 DNS 服务器

1. 在 Debian 上安装 DNS 软件

```
root@debian7:-# aptitude update aptitude upgrade

...

root@debian7:-# aptitude install bind9

...

root@debian7:-# dpkg -l | grep bind9 | tr -s ' '

ii bind9 1:9.8.4.dfsg.Pi-6+nmu2+deb7u2 amd64 Internet Name Server
ii bind9-host 1:9.8.4.dfsg.Pi-6+nmu2+deb7u2 amd64 Version of 'host' bundled...
ii bindutils 1:9.8.4.dfsg.Pi-6+nmu2+deb7u2 amd64 Utilities for BIND
ii libbind90-1:9.8.4.dfsg.Pi-6+nmu2+deb7u2 amd64 BIND9 Shared Library...

root@debian7:-#
```

2. 发现配置文件。你能找到每个文件的用途吗？

```
root@debian7:-# ls -l /etc/bind

total 52

-rw-r--r-- 1 root 2389 Sep 20:25 bind.keys
-rw-r--r-- 1 root 237 Sep 20:25 db.0
-rw-r--r-- 1 root 271 Sep 20:25 db.12
-rw-r--r-- 1 root 353 Sep 20:25 db.255
-rw-r--r-- 1 root 270 Sep 20:25 db.empty
-rw-r--r-- 1 root 308 Sep 20:25 db.local
-rw-r--r-- 1 root 505 Sep 20:25 named.conf
-rw-r--r-- 1 bind 490 Sep 20:25 named.conf.default-zones
-rw-r--r-- 1 bind 374 Oct 1 20:01 named.conf.local
-rw------- 1 root 1124 Nov 11:14 named.conf.options
-rw------- 1 bind 77 Oct 1 11:14 rndc.conf
-rw-r--r-- 1 root 1317 Sep 20:25 zones.rfc191
```

3. 设置仅作为缓存的 DNS 服务器。这通常是默认设置。仅缓存的服务器会为你查询名称并缓存它们。许多教程会教你如何添加转发器（forwarder），但我们首先尝试在不使用它的情况下运行！

这里没有转发器似乎也能正常工作。使用嗅探器，你可以发现新安装的 DNS 服务器没有使用你的本地 DNS 服务器（从 `/etc/resolv.conf` 查看）。那么，这些信息是从哪里来的？通过嗅探 DNS 流量你可以学到些什么？

4. 详细说明在没有进一步转发器的情况下，仅作为缓存的 DNS 服务器时发生了什么。这个 Wireshark 截图会有帮助，但通过自己嗅探流量你会学到更多。

![](img/1d499a6177836f6f088a9e2a53e11a14_85_0.png)

| No. | 时间 | 源 | 目的 | 协议信息 |
|---|---|---|---|---|
| 205 | 18:35:38 | 192.168.1.37 | 128.8.18.90 | DNS | Standard query A slashdot.org |
| 210 | 18:48:13 | 192.168.1.37 | 192.168.1.37 | DNS | Standard query response |
| 211 | 18:49:38 | 192.168.1.37 | 199.249.112.1 | DNS | Standard query A slashdot.org |
| 212 | 18:52:28 | 192.168.1.37 | 192.168.1.37 | DNS | Standard query response |

- `Transaction ID`: 0x6826
- `Flags`: 0x8000 (Standard query response, No Error)
- `Questions`: 1
- `Answer RRs`: 0
- `Authority RRs`: 9
- `Additional RRs`: 13
- `slashdot.org`: type A, CLASS IN
- `Authoritative nameserver`:
  - type: NS, CLASS IN, `debianpaul`
  - type: NS, CLASS IN, `debian7`
  - type: NS, CLASS IN, `b2.org`
  - type: NS, CLASS IN, `d0.org`
  - type: NS, CLASS IN, `a0.org`
  - type: NS, CLASS IN, `c0.org`
  - type: DS, CLASS IN
  - type: DS, CLASS IN
  - type: RSEC, CLASS IN

## 4.14.1. 使用你的 DNS 服务器

如果你确信你的 `dns` 服务器工作正常，那么请将其设置为 `/etc/resolv.conf` 中的默认且唯一的 DNS 服务器。

```
root@debian7:~# cat /etc/resolv.conf

nameserver 10.104.33.30

root@debian7:~#
```

如果你也使用了 `dhcpclient`，则需要将你的 `dns` 服务器添加到 `/etc/dhcp/dhcpclient.conf` 中。

```
root@debian7:~# diff /etc/dhcp/dhcpclient.conf /etc/dhcp/dhcpclient.conf.original

21c21

< prepend domain-name-servers 10.104.33.30;

> #prepend domain-name-servers 127.0.0.1;

23,24c23

< domain-name, domain-name-servers, domain-search, host-name,
<-\omain-name, domain-name-servers, host-name,

---

> domain-name, domain-name-servers, domain-search, host-name,

root@debian7:~#
```

上面的截图显示 10.104.33.30 现在是一个默认选项，`dhcp` 不再应向 `dhcp` 服务器请求该选项。

调整 `/etc/hosts` 以反映你的域名，并使用 `hostname` 和 `dnsdomainname` 进行验证。

```
root@debian7:~# grep debian7 /etc/hosts

127.0.0.1 debian7.paul.local debian7

root@debian7:~# hostname

debian

root@debian7:~# hostname --fqdn

debian.paul.local

root@debian7:~# dnsdomainname

paul.local
```

## 4.14.2. 使用自己的域名

考虑以下截图：

```
root@debian7b:~# cat /etc/resolv.conf
```



`nameserver 10.104.33.30`

```
root@debian7b:~# ping -cl www

ping: unknown host www

root@debian7b:~# vi /etc/resolv.conf

root@debian7b:~# cat /etc/resolv.conf

nameserver 10.104.33.30

domain paul.local

root@debian7b:~# ping -cl www

PING www.paul.local (10.104.33.31) 56(84) bytes of data.

64 bytes from 10.104.33.31: icmp_req=1 ttl=64 time=0.021 ms

--- www.paul.local ping statistics ---

1 packets transmitted, 1 received, 0% packet loss, time 0ms

rtt/avg/max/mdev = 0.021/0.021/0.021/0.000 ms

root@debian7b:~#
```

在 `/etc/resolv.conf` 中添加 `domain paul.local` 指令，这样在使用主机名时就可以省略域名。

你可以通过调整 `dhclient.conf` 自动实现这一功能。

```
root@debian7~# grep paul.local /etc/dhcp/dhclient.conf

prepend domain-name "paul.local";

prepend domain-search "paul.local";

root@debian7:~#
```

## 4. 启动 DNS 服务器并在错误日志中检查你的区域。

```
root@debian:~# service bind9 restart

Stopping domain name service..., bind9.

Starting domain name service..., bind9.

root@debian:~# grep paul.local /var/log/syslog

Oct 09:22:18 debian[2707]: zone paul.local/IN: loaded sera

Oct 6 09:22:18 debian[2707]: zone paul.local/IN: sending not

2014010
```

## 5. 使用 `dig` 或 `nslookup` 测试你的记录。

```
root@debian:~# ping -c 1 nsl.paul.local

PING paul.local (10.104.33.30) 56(84) bytes of data.

64 bytes from 10.104.33.30: icmp_req=1 ttl=64 time=0.006 ms

--- nsl.paul.local ping statistics ---

1 packets transmitted, 1 received, 0% packet loss, time 0ms

rtt/avg/max/mdev = 0.006/0.006/0.006/0.000 ms

root@debian:~# ping -c 1 www.paul.local

ping: unknown host www.paul.local
```

> 注意被注释掉的记录不应该被找到。

```
root@debian:~# dig debian7.paul.local

;; options: +cmd-answer

;; Got answer:

;; HEADER; opcode: QUERY, status: NOERROR, id: 50491

;; flags: qr aa ra; QUERY: 1, ANSWER: 1, ADDITIONAL: 2

;; QUESTION SECTION:

debian7.paul.local IN A

;; ANSWER SECTION:

debian7.paul.local. 86400 IN A 10.104.33.30

;; AUTHORITY SECTION:

paul.local. 86400 IN NS nsl.paul.local.

paul.local. 86400 IN NS debian7.paul.local.

;; ADDITIONAL SECTION:

nsl.paul.local. 86400 IN A 104.104.33.30

debian7.paul.local. 86400 IN A 104.104.33.30

;; Query time: 4 msec

;; SERVER: 104.104.33.30

;; WHEN: Mon Oct 6 09:35:25 2014

;; MSG rcvd: 14

root@debian:~#
```

## 6. 我们的主服务器似乎正在运行。注意这里的信息：

```
root@debian:~#

ip address : 104.104.33.30

domain name : paul.local
```

## 4.15 示例：DNS 服务器

1. 从服务器通过网络从主服务器传输信息（从服务器也可以是主服务器）。主服务器在本地文件系统中维护记录。作为练习，为了验证所有学生的工作，请设置一个从服务器。
2. 在配置服务器之前，你可能需要允许传输到此服务器。记住这不是安全的，因为传输是明文的并且限制了地址。此示例遵循我们上面的演示。假设一个名为 `Jesse` 的学生已完成设置，域名为 `paul.local`，IP 地址为 `104.104.33.20`。目标是在我的计算机上有一个 `paul.local` 的从服务器。

```
root@debian:/etc/bind# cat named.conf

// Do any local

// 如果组织内未使用区域，请考虑在此处添加

zone "paul.local" IN (

    type master;

    file "/etc/bind/db.local";

    allow-update { none };

    allow-transfer { 104.104.15.20 };

);
```

### DNS 简介

3. 通过以下配置，我可以让我的服务器成为 `jesse.local` 区域的从服务器。

```
root@debian:/etc/bind# tail named.conf

zone jesse.local: IN {

  type slave;

  file "/var/cache/named/db.local";

  masters { 104.104.15.20 };

};
```

```
root@debian:/etc/bind# mkdir /var/cache/named

root@debian:/etc/bind# chown bind /var/cache/named

root@debian:/etc/bind# ls -ld /var/cache/named/

drwxr-xr-x 2 bind 4096 1 20:01 /var/cache/named/
```

注意，我们将从区域放在 `/var/cache/named` 而不是 `/etc/bind`。

4. 在从服务器上重启应该传输数据库文件。在 `/var/syslog` 中验证这一点。时间和日期已从截中截断，且 `Jesse` 没有在名称中使用当前日期。

```
root@debian:/etc/bind# grep jesse /var/syslog

named[2731]: transfer of jesse.local/IN: Transfer started.

named[2731]: transfer of 'jesse.local/IN' from 104.104.15.20: connected to 104.104.33.30

named[2731]: transfer of 'jesse.local/IN': transferred serial 20110516
```

从区域的内容：

```
root@debian:/etc/bind# cat /var/cache/named/db.local

$ORIGIN

TTL 604800

@paul.local. IN SOA ns.paul.local. admin.paul.local. (

            20140101 1 ; 300 600 2419200 604800 )

;

@paul.local. IN NS ns.paul.local.

@paul.local. IN NS debian7.paul.local.

ns.paul.local. IN A 104.104.33.30
```



`debian7.paul.local. IN A 104.104.33.30`

```
## 4.16 练习：dns
- 1. 安装 `bind9` 并使用嗅探器检查其工作原理。
- 2. 添加转发器并验证其工作正常。
- 3. 创建一个名为 `you.local` 的主查找区域，至少包含两个 `NS` 记录和四个 `A` 记录。
- 4. 使用 `dig` 或 `nslookup` 验证你的 `NS` 和 `A` 记录。
- 5. 在另一个服务器上创建主区域的从服务器并验证区域传输。
- 6. 在两个服务器上设置两个主区域并实现条件转发。

## 4.17 解决方案：dns
- 1. 安装 `bind9` 并使用嗅探器检查其工作原理。你应该通过 `tcpdump` 或 `wireshark` 查看向根域名服务器的查询。
- 2. 添加转发器并验证其工作正常。转发器可以添加到 `named.conf.options` 中，如理论所示。
- 3. 创建一个名为 `yourname.local` 的主查找区域，至少包含两个 `NS` 记录和四个 `A` 记录。这在理论中有详细解释。
- 4. 使用 `dig` 或 `nslookup` 验证你的 `NS` 和 `A` 记录。这在理论中有详细解释。
- 5. 在另一个服务器上创建主区域的从服务器并验证区域传输。这在理论中有详细解释。
- 6. 在两个服务器上设置两个主区域并实现条件转发（你可以使用之前的两个服务器）。
```

# 第 5 章 高级 DNS

本章将扩展你的 DNS 服务器功能，主题包括用于服务器负载均衡的 `轮询 DNS (round robin dns)`、将子域名委托给另一个团队的 `DNS 委托 (dns delegation)`，以及能够为客户端提供本地服务位置的 `分区域 DNS (split horizon dns)`。

`DNS` 还有更多内容，很快会添加。

## 5.1. 示例：DNS 轮询

当你为同一个名称创建多个 `A` 记录时，`bind` 会对返回的记录顺序进行轮询。这允许将 DNS 作为主机之间的负载均衡器使用，因为客户端通常会获取第一个解析出的地址。

考虑这个针对 `/etc/bind/db.paul.local` 区域配置文件的示例。`www` 有两个指向不同 IP 地址的 `A` 记录。

```
root@debian:~# grep www /etc/bind/db.paul.local
www       IN      A  10.104.33.30
www       IN      A  10.104.33.31
```

下面是 `nslookup` 查询平衡 `A` 记录的截图。注意返回的 IP 地址的顺序。

```
root@debian:~# nslookup www.paul.local 10.104.33.30
Server:         10.104.33.30
Address:        10.104.33.30#53
Name:           www.paul.local
Address:        10.104.33.31
Name:           www.paul.local
Address:        10.104.33.30

root@debian:~# nslookup www.paul.local 10.104.33.30
Server:         10.104.33.30
Address:        10.104.33.30#53
Name:           www.paul.local
Address:        10.104.33.30
Name:           www.paul.local
Address:        10.104.33.31
```

尝试在两个 Web 服务器上建立网站（带有细微差异以便区分网站）并测试轮询。

## 5.2. DNS 委托

你可以将子域名委托给另一个 DNS 服务器。该子域名将成为一个新的区域，其权威由新的 DNS 服务器维护。

![](img/1d499a6177836f6f088a9e2a53e11a14_98_0.png)

当委托正确设置后，查询父区域的客户端也能解析被委托的子区域。

## 5.3. 示例：DNS 委托

我们有另一台 Linux 服务器 `debian7b`，我们希望让它负责子域名 `test42.paul.local`。

注意截图中的服务器名称要么是 `debian7`（托管父域名），要么是 `debian7b`（托管子域名）。

我们首先调整 `/etc/bind/named.conf.local` 文件（在托管父域名的服务器上），以确保在解析权威名称时不会使用任何转发器。

```
root@debian7:~# grep -A4 paul.local /etc/bind/named.conf.local
zone "paul.local" {
    type master;
    file "etc/bind/db.paul.local";
    allow-update { none };
    allow-transfer { 10.104.15.20 };
    forwarders { };
}
root@debian7:~#
```

技术上，你也可以在排故障时将 `allow-transfer` 设置为 `{ any }` 然后进行细化，但对于委托来说是不需要的。

然后我们向区域数据库中添加委托：

```
root@debian7:~# vi /etc/bind/db.paul.local
ORIGIN test42.paul.local.
@       IN NS ns2.test42.paul.local.
ns2      IN A    10.104.33.31    ; 粘合记录
root@debian7:~#
```

不要忘记重启 `bind` 并验证 `/var/log/syslog`。

```
root@debian7:~# service bind9 restart
Stopping domain name service.... bind9.
Starting domain name service.... bind9.

root@debian7:~# grep paul.local /var/log/syslog | cut -c28- | tail -2
named[3202]: zone paul.local/IN: loaded serial 2014100801
named[3202]: zone paul.local/IN: sending notifications (serial 2014100801)
root@debian7:~#
```

注意在你的终端上你可以输入 `tail -40 /var/log/syslog`，因为我使用 `grep`、`cut` 和 `tail -2` 的唯一原因是限制此书中截图的大小。

接下来我们在第二台服务器上创建一个数据库文件，如所示：

```
root@debian7b:~# cat /etc/bind/db.test42.paul.local
; 教学的子区域
$TTL 8600
$ORIGIN test42.paul.local.
@    SOA    ns2.test42.paul.local. root.test42.paul.local. (
                    2014100800 ; Serial
                            1h; Refresh
                            1h; Retry
                            2h; Expire
                            900 ) ; Negative Cache TTL
; name
IN     NS      ns2.test42.paul.local.
IN     NS      debian7b.test42.paul.local.
; servers
ns2         IN A       10.104.33.31
debian7b     IN A       10.104.33.31
root@debian7b:~#
```

第二台服务器在 `named.conf.local` 中也需要定义，然后重启 `bind`。

```
root@debian7b:~# cat /etc/bind/named.conf.local
// 本地配置
// 如果没有使用，考虑在这里添加 r1918 区域
include "/etc/bind/zones.rfc1918"
zone "test42.paul.local" {
    type master;
    file "/etc/bind/db.test42.paul.local";
    allow-update { none };
    allow-transfer { any };
}
root@debian7b:~#
```



在父服务器上测试：

```
root@debian7:~# dig ns1.paul.local +short
10.104.33.30
root@debian7:~# dig ns2.test42.paul.local +short
10.104.33.31
root@debian7:~# dig debian7b.test42.paul.local +short
10.104.33.31
```

## 5.4. 示例：分区域 (split-horizon)

假设你想根据请求者来回答 `DNS`。例如，当来自 `10.104.15.0/24` (Jesse) 的用户查询 `www.local` `A` 记录时，返回 `10.104.33.30`；但当来自 `10.104.42.0` (Keith) 的用户查询相同的记录将得到 `10.104.33.31`。

分区域设置可以重定向到某些服务的本地。在本示例中，我们想要为两个网络（Jesse 和 Keith）决定答案并防止他们使用我们的 `DNS` 服务器，同时保留解析 `paul.local` 的能力。

我们在 `named.conf.local` 中创建三个视图 (views)：

```
root@debian7:/etc/bind# cat named.conf.local

view "paul" {

    match-clients { 10.104.33.30; localhost; };

    include "/etc/bind/named.zones";

    zone "paul.local" {

        type master;

        file "/etc/bind/db.paul.local";

        allow-update { none };

    } // 结束 view

view "jesse" {

    match-clients { 10.104.15.0/24 };

    zone "paul.local" {

        type master;

        file "/etc/bind/db.paul.local.jesse";

        allow-update { none };

    } // 结束 view 

view "keith" {

    match-clients { 10.104.42.0/24 };

    zone "paul.local" {

        type master;

        file "/etc/bind/db.paul.local.keith";

        allow-update { none };

    }

} // 结束 view
```

注意我们在 `internal` 区域中包含了 `default-zones`。必须使用视图放置所有区域。区域文件是完全相同的，除了 `www` 记录。你可以看到内部用户启用了轮询，来自 `10.104.15.0/24` (Jesse) 的计算机将始终收到 `10.104.33.30`，而来自 `10.104.42.0` (Keith) 的计算机将收到 `10.104.33.31`。

```
root@debian7:/etc/bind# grep www db.paul.local db.paul.local.

db.paul.local:www      IN A 10.104.33.30

db.paul.local:www      IN A 10.104.33.31

db.paul.local:jesse   IN A 10.104.33.30

db.paul.local:keith   IN A 10.104.33.31
```

## 5.5. 旧 DNS 主题

本段下的所有 `DNS` 内容都是旧的，急需审查。

### 5.5.1. 旧示例：反向 DNS

1. 我们可以使用反向 `DNS` 区域为 `DNS` 服务器添加 `IP` 到名称解析。

2. 首先向 `/etc/bind/named.conf.local` 添加一个 `.arpa` 区域如下（我们将 `notify` 设置为 `no` 以避免向其他服务器发送通知消息）：

```
root@ubuntu010srv:/etc/bind# grep -A4 arpa named.conf.local

zone "1.168.192.in-addr.arpa" (

    type master;

    notify no;

    file "/etc/bind/db.192";

);
```

3. 同样为此反向查找区域创建一个数据库文件。

```
root@ubuntu010srv:/etc/bind# cat db.192

;

; BIND 用于 192.168.1.0/24 网络的反向数据文件

;

@ TTL 604800

@ IN SOA ns.cobbaut.paul root.cobbaut.paul. (

2011016 6 ; Serial

604800 ; Refresh

86400 ; Retry

2419200 ; Expire

604800 ) ; Negative Cache TTL

;

@ IN NS ns.

37 IN PTR ns.cobbaut.paul.

1 IN PTR anya.cobbaut.paul.

30 IN PTR mac.cobbaut.paul.

root@ubuntu010srv:/etc/bind#
```

### 5.5.2. 旧版 DNS 负载均衡

与上述不同。当一个区域有多个权威服务器时，你可以将查询分散到所有服务器上。实现此方法的方法是对所有参与外部查询负载均衡的服务器创建 `NS` 记录。

你也可以在内部客户端配置不同的名称服务器。

### 5.5.3. 旧版 DNS notify

`rfc 1034` 和 `rfc 1035` 中 `DNS` 的原始设计在 `SOA` 记录中实现了刷新时间（refresh time），用于为从服务器查询主服务器配置时间循环。这会导致大量的无用的拉取请求（pull requests），或者在更新之间出现显著延迟。

出于因此，设计了 `dns notify` (`rfc 1996`)。每当有更新时，服务器都会通知从服务器。默认情况下，此功能在 `bind` 中是启用的。

可以在此更改中禁用 `notify`：

```
zone "1.168.192.in-addr.arpa" {

  type master;

  notify no;

  file "/etc/bind/db.192";

}
```

### 5.5.4. 旧版 IXFR 和 AXFR

当你重启 `bind` 服务器或直接手动更新区域数据库文件时，会启动全区域传输 (`AXFR`)。使用 `nsupdate`，你可以更新区域数据库并启动增量区域传输。

你需要 `admin` 权限才能让 `nsupdate` 运行。

```
root@ubuntu010srv:/etc/bind#$ nsupdate

> server 127.0.0.1

> update add mac4.1.linux-training.be 86400 A 192.168.1.627

> send

update failed: REFUSED
```



## 5.5.5. 旧版 DNS 与 DHCP 的集成

某些组织喜欢让所有客户端都存在 DNS 中。这维护起来很繁琐。幸运的是，`rfc 2136` 描述了 DHCP 服务器与 DNS 服务器的集成。每当 DHCP 确认客户端 IP 配置时，它就可以通知 DNS 这些客户端的 IP 地址和名称。这被称为动态更新（`dynamic-updates`）或 `DDNS`。

## 5.5.6. 旧版 in-addr.arpa 中的反向即正向

反向查找实际上是在 `in-addr.arpa` 域中作为正向查找实现的。该域有 256 个子域（从 `0.in-addr.arpa` 到 `255.in-addr.arpa`），每个子域又有 256 个子域。这种两次嵌套形成了一个超过四亿（2 的 32 次方）域的结构。

## 5.5.7. 旧版 ipv6

带有 `rfc 3596` 用于 DNS 的 `cam6` 扩展。网络上的 `ipv6` 主机有 `AAAA` 记录，有一个用于反向查找的 `ip6.int` 域（拥有 16 个子域，从 `0.ip6.int` 到 `fip6.int`，每个子域又有 16 个子域……并如此重复 16 次）。

## 5.5.8. 旧版 DNS 安全：文件损坏

为了减轻区域文件和 `bind` 配置文件的损坏，请使用 Unix 权限保护它们，并进行定期备份。

## 5.5.9. 旧版 DNS 安全：区域传输

将区域传输限制在某些特定的 IP 地址，而不是任何地址。尽管 IP 地址可以被伪造，仍请使用此方法。

## 5.5.10. 旧版 DNS 安全：区域传输、IP 伪造

你可以设置 `DNSSEC`（这并不是容易维护的），并结合 `rfc 2845(tsigs)` 和 `rfc 2930(tkey, 但容易受到暴力攻击)`，或者你可以禁用所有区域传输并使用带有 `ssh` 的脚本手动复制它们。

## 5.5.11. 旧版 DNS 安全：查询

仅允许来自本地网络进行递归，仅在需要时允许从外部进行迭代查询。这可以在主服务器和从服务器上配置。

```
view "internal" {
    match-clients { 192.168.42/24; };
    recursion yes;
}

view "external" {
    match-clients { any };
    recursion no;
}
```

或者只允许来自本地区域的查询。

```
options {
    allow-query { 192.168.42.0/24; localhost; };
}

zone "cobbaut.paul" {
    allow-query { any; };
}
```

或者只允许来自内部客户端的递归查询。

```
options {
    allow-recursion { 192.168.42.0/24; localhost; };
}
```

## 5.5.12. 旧版 DNS 安全：chrooted bind

大多数 Linux 发行版都允许在 `chroot` 环境中轻松设置 `bind`。

## 5.5.13. 旧版 DNS 安全：DNSSEC

`DNSSEC` 使用公钥/私钥来保护通信，这在 `rfc: 4033`, `4034` 和 `4035` 中描述。

## 5.5.14. 旧版 DNS 安全：root

不要以 `root` 身份运行 `bind`。不要以 `root` 身份运行任何守护进程。

# 第四部分. dhcp 服务器

# 目录

- 6. dhcp 简介 ............................................................................ 102
- 6.1. 四次广播 ....................................................................................... 103
- 6.2. 图解 dhcp ......................................................................................... 104
- 6.3. 安装 dhcp 服务器 ................................................................................ 105
- 6.4. RHEL/CentOS 的 dhcp 服务器 ................................................................ 105
- 6.5. 客户端保留 ................................................................................ 106
- 6.6. 示例配置文件 ................................................................................ 106
- 6.7. 旧的示例配置文件 ................................................................ 107
- 6.8. 高级 dhcp ................................................................................ 109
- 6.9. 练习：dhcp ................................................................................. 110

# 第 6 章. dhcp 简介

`dhcp` 的替代方案是在每台客户端计算机上手动输入 ip 配置。

## 6.1. 四次广播

`dhcp` 在第 2 层广播上工作。启动的 `dhcp` 客户端将在网络上发送一个 `dhcp discover`。所有（有可用租约）`dhcp` 服务器都将用 `dhcp offer` 响应。客户端将选择这些 `offer` 之一并向所选的 `offer` 发送 `dhcp request`。`dhcp` 服务器响应一个 `dhcp acknowledgment`。

在 `wireshark` 中它看起来像这样。

![](img/1d499a6177836f6f088a9e2a53e11a14_110_0.png)

当此过程完成后，客户端就可以使用其 `ipcp-配置`直到租约结束。

## 6.2. 图解 dhcp

我们有一个小型网络，包含两个名为 `DHCP-SRV1` 和 `DHCP-SRV2` 的 `dhcp` 服务器以及两个客户端（`SunWS1` 和 `Mac42`）。所有计算机都通过集线器或交换机连接（图中所示）。所有四台计算机都有连接到集线器的缆（电缆未画）。

![](img/1d499a6177836f6f088a9e2a53e11a14_111_0.png)

- 1. 客户端 `SunWS1` 在网络上发送一个 `dhcp discover`。所有计算机都接收了这个广播。
- 2. 两个 `dhcp` 服务器都用 `dhcp offer` 回答。
- 3. 客户端选择来自 `DHCP-SRV1` 的 `offer` 并发送 `dhcp request`。
- 4. `DHCP-SRV1` 用 `dhcp acknowledgment` 回答。

四次广播（如果你算上五次的话）都在第 2 层。参考 `rfc 2131`。

## 6.3. 安装 dhcp 服务器

对于 `Debian/Mint`，安装很容易。

```bash
debian5:~ aptitude install dhcp-server
读取软件包列表... 完成
构建依赖树...
读取状态... 完成
读取任务描述... 完成
将安装新软件包：
dhcp-server
```

你得到了一个包含许多示例的配置文件。

```bash
debian5:~# ls -l /etc/dhcp3/conf.conf
-rw-r--r-- 1 root 3551 2011-04-10 21:23 /etc/dhcp3/conf.conf
```

## 6.4. RHEL/CentOS 的 dhcp 服务器

使用 `yum` 安装很简单。

```bash
[root@rhe7]# yum install dhcp
加载插件: product-id, subscription-manager
解析依赖
--> 运行事务检查
--> 软件包 dhcp.x86_64 12:4.2.5-36.e17 将被安装
--> 完成依赖解析
```



# 解析依赖

| 软件包 | 体系 | 版本 | 仓库 | 大小 |
|---|---|---|---|---|
| 安装 `dhcp` | `x86_64` | `12:4.2.5-36.e17` | `rhel-7-server-rpms` | `510 k` |

## 事务摘要
`1` 个软件包
总大小: `510 k`
已安装: `1.4 M`
是否确定 `[y/N]`: `y`
下载包:
`dhcp-4.25-36.e17.x86_64.rpm` | `510 KB` `00:01`
运行事务检查
运行事务测试
事务测试成功
运行事务
安装: `12:dhcp-4.2.5-36.e17.x86_64` | `1/1`
验证: `12:dhcp-4.2.5-36.e17.x86_64` | `1/1` |

已安装：
完成！

安装后我们得到一个 `/etc/dhcp/dhcp.conf`，它指向一个名为 `dhcpd.sample` 的示例文件。

## dhcp 简介

```
[root@rhel71 ~]# # cat /etc/dhcp/dhcpcd.conf
# DHCP Server 配置文件。
#   见 /usr/share/doc/dhcp*/dhcpcd.conf.example
#   参 dhcpcd.conf(5) man page

[root@rhel71 ~]#
```

我们复制示例文件并根据实际情况进行调整。我们将该副本命名为 `/etc/dhcp/dhcpcd.conf`。

```
[root@rhel71 ~]# cp /usr/share/doc/dhcp-4.2.5/dhcpcd.conf /etc/dhcp/dhcp-d.conf
[root@rhel71 ~]# # vi /etc/dhcp/dhcpcd.conf
option domain-name "linux-training.be";
option domain-name-servers 10.42.42.42;
default-lease-time 600;
max-lease-time 720;
log-facility local7;

subnet 10.42.0.0 netmask 255.255.255.0 (
  range 10.42.200.11 10.42.200.120;
  option routers 10.42.200.1;
}

[root@rhel71 ~]#
```

`routers` 选项仅对该子网有效，而 `domain-name` 选项对所有子网有效。

启动服务器。请记住在 RHEL7/CentOS 上使用 `systemctl start dhcpd`，在之前的 RHEL/CentOS 版本上使用 `service dhcpd`。

```
[root@rhel71 ~]# systemctl start dhcpd
[root@rhel71 ~]#
```

## 6.5. 客户端保留

你可以使用 `MAC` 地址为客户端预留 `IP` 配置。

```
host pc42 {
  hardware ethernet 11:22:33:44:55:66;
  fixed-address 192.168.42.42;
}
```

你可以为此保留项添加单独的选项。

```
host pc42 {
  hardware ethernet 11:22:33:44:55:66;
  fixed-address 192.168.42.42;
  option domain-name "linux-training.be";
  option routers 192.168.42.1;
}
```

## 6.6. 示例配置文件

下面你将看到 Debian 6 服务器上 `/etc/dhcp/dhcpcd.conf` 的几个部分。

```
# NetSec Antwerp Network
```

```
subnet 192.168.1.0 netmask 255.255.255.0 (
  range 192.168.1.20 192.168.1.199;
  option domain-nameservers nsl.netsec.local;
  option domain-name "netsec.local";
  option routers 192.168.1.1;
  option broadcast-address 192.168.1.255;
  default-lease-time 7200;
  max-lease-time 7200;
)
```

上述是网络的通用配置，包含一个 `188` 个地址的池。

下面是两个客户端保留项：

```
# laptops
#
host mac {
  hardware ethernet 00:26:bb:xx:xx;
  fixed-address mac.netsec.local;
}

host vmac {
  hardware ethernet 8c7b:9d:xx:xx;
  fixed-address vmac.netsec.local;
}
```

## 6.7. 旧版示例配置文件

用于在 Fedora 上具有 DNS 域动态更新更新的 `dhcpd4`。

```
[root@fedora14 ~]# cat /etc/dhcp/dhcpd.conf
authoritative;
include "/etc/rndc.key";
log-facility local6;
server-identifier fedora4;
dns-domainname "office.linux-training.be";
dns-update-style interim;
dns-updates on;
update-static-leases on;

option domain-name "office.linux-training.be";
option domain-nameservers 192.168.42.100;
option ip-forwarding off;

default-lease-time 1800;
max-lease-time 3600;

zone "office.linux-training.be {
  primary 192.168.42.100;
}
subnet 192.168.4.0 netmask 255.255.255.0
  range 192.168.4.24 192.168.4.40;
}
```

允许在区域数据库中进行任何更新（`named.conf` 配置的一部分）：

```
zone "office.linux-training.be";
type master;
file "/var/named/db.office.linux-training.be";
allow-transfer ( any );
allow-update ( any );
};
```

允许在区域数据库中进行安全的密钥更新（`named.conf` 配置的一部分）：

```
zone "office.linux-training.be" {
type master;
file "/var/named/db.office.linux-training.be";
allow-transfer ( any );
allow-update ( key mykey );
};
```

示例密钥文件内容：

```
[root@fedora4 ~]# cat /etc/rndc.key
key "rndc-key {
alalgorithm hmac-md5;
secret "*4Ykd58UieUr3Ve6ad1qTfQ==";
};
```

使用 `dnssec-keygen` 生成你自己的密钥。

如何在配置文件包含密钥：

```
include "/etc/bind/rndc.key";
```

同时确保 `bind` 能够写入你的 `db.zone` 文件（使用 `chmod`/`chown`）。对于 `Ubuntu`，这可以在 `/etc/bind` 中，对于 `Fedora` 则在 `/var/named` 中。

## 6.8. 高级 dhcp

### 6.8.1. 80/20 原则

`DHCP` 服务器不应是单点故障。让我们讨论冗余的 `DHCP` 服务器设置。

### 6.8.2. 中继代理

为了避免在每个网段都放置 `DHCP` 服务器，我们可以使用 `DHCP` 中继代理。

### 6.8.3. 异常 DHCP 服务器

异常 `DHCP` 服务器是一个没有解决方案的问题。例如，无意中将一个（被认为简单的）集线器/交换机连接到有内部 `DHCP` 服务器的网络中。

### 6.8.4. dhcp 和 ddns

`DHCP` 在配置客户端计算机时动态更新 `DNS`。`DDNS` 可以使用或使用安全密钥。

当配置正确时，记录可以自动添加到区域文件中：

```
root@fedora14~# tail -2 /var/named/db.office.linux-training.be
ubu1010srv A 192.168.42.151
 TXT "0ubu1010"
```

## 6.9. 练习：dhcp

## 7.1. 路由器或防火墙



`路由器`是连接两个网络的设备。`防火墙`是一种除了充当`路由器`之外，还包含（并实现）规则的设备，用于决定是否允许从一个网络传输到另一个网络。防火墙可以根据网络、主机、协议和端口配置阻止访问。防火墙在转发数据包时还可以更改数据包的内容。

![](img/1d499a6177836f6f088a9e2a53e11a14_121_0.png)

## 7.2. 包转发

`包转发`意味着允许数据包从一个网络传输到另一个网络。当一个多宿主机连接到两个不同的网络，并且它允许数据包通过它的两个网络接口从一个网络传输到另一个网络时，就说开启了`包转发`。

## 7.3. 包过滤

`包过滤`与包转发非常相似，但每个数据包都会根据规则进行单独测试，以决定允许或丢弃该包。这些规则由 `iptables` 存储。

## 7.4. 状态型

状态型防火墙是无状态防火墙的进阶，它会检查每一个单独的数据包。状态型防火墙会维护一个活动连接表，并且足够智能，识别新连接何时属于活动会话的一部分。`Linux iptables` 就是一个状态型防火墙。

## 7.5. nat (网络地址翻译)

`nat 设备`是一种路由器，它同时更改数据包中的源和/或目标 IP 地址。它通常用于将连接在私有地址范围（`rfc 1918`）内的多台计算机连接（公共）互联网。`nat` 可以从互联网上隐藏地址。

重要的一点是，人们和供应商在指代特定类型的 `nat` 时并不总是使用正确的术语。请确保你谈论的是同一件事。我们可以区分几种类型的 `nat`。

## 7.6. pat (端口地址翻译)

`nat` 包含 `pat`。`pat 设备`是一种路由器，它同时更改数据包中的源和/或目标 `tcp/udp` 端口。`pat` 是 `Cisco` 的术语，并用于 `Linux` 中的 `snat`、`dnat`、伪装（`masquerading`）和`端口转发`。`RFC 3022` 称为 `NAPT`，并将 `nat/pat` 组合定义为“传统 `nat`”。向你出售的 `nat` 设备可能同时执行 `nat` 和 `pat`。

## 7.7. snat (源地址翻译)

`snat 设备`在数据包通过我们的 `nat` 配置时更改源 IP 地址。带有 `iptables` 的 `snat` 配置包含一个固定的目标源地址。

## 7.8. 伪装 (masquerading)

`伪装` 是 `snat` 的一种形式，它使用公共 IP 地址隐藏你私有网络的（私有）源 IP 地址。伪装在动态互联网接口（宽带调制解调器/路由器）上很常见。`iptables` 的伪装配置使用动态目标源地址。

## 7.9. dnat (目标地址翻译)

`dnat 设备`在数据包通过我们的 `nat` 时更改目标 IP 地址。

## 7.10. 端口转发

当设置静态 `dnat` 以允许外部连接进入我们的私有网络时，我们将其称为`端口转发`。

## 7.11. /proc/sys/net/ipv4/ip_forward

主机是否转发数据包定义在 `/proc/sys/net/ipv4/ip_forward` 中。下面的截图显示了如何在 `Linux` 上启用包转发。

```
root@router-# echo 1 > /proc/sys/net/ipv4/ip_forward
```

下一个命令显示了如何禁用包转发。

```
root@router-# echo 0 > /proc/sys/net/ipv4/ip_forward
```

使用 `cat` 检查是否启用了包转发。

```
root@router-# cat /proc/sys/net/ipv4/ip_forward
```

## 7.12. /etc/sysctl

默认情况下，大多数 `Linux` 计算机都没有配置自动包转发。要在系统每次启动时都启用包转发，请将 `/etc/sysctl.conf` 中的 `net.ipv4.ip_forward` 变量更改为 `1`。

```
root@router-# grep ip_forward /etc/sysctl.conf
net.ipv4.ip_forward = 0
```

## 7.13. sysctl

更多信息，请查看 `sysctl` 的 `man` 页面。

```
root@debian6-# sysctl -a 2>/dev/null | grep ip_forward
```

## 7.14. 练习：包转发

7.14.0 当在 `VirtualBox` 或 `VMware` 中添加网卡时，你可以选择或（创建）内部网络。使用此选项创建两个内部网络。我将它们命名为 `leftmost` 和 `rightnet`，但你可以选择任何名称。

### 网络

| 适配器 | 描述 |
|---|---|
| 适配器 1 | Intel PRO/1000 Desktop (桥接适配器, en1:AirPort) |
| 适配器 2 | Intel PRO/1000 Desktop (内部网络, 'leftnet') |
| 适配器 3 | Intel PRO/1000 Desktop (内部网络, 'rightnet') |

1. 设置两台 `Linux` 机器，一台在 `leftmost`，另一在 `rightnet`。确保它们都在正确的子网中获取 IP 地址。这两台机器将是“路由器”的“左侧”和“右侧”。

![](img/1d499a6177836f6f088a9e2a53e11a14_124_0.png)

2. 设置第三台带有三个网卡的 `Linux` 计算机，一台在 `leftmost`，另一台在 `rightnet`。这台计算机将作为“路由器”。在下表中填写相关的名称、IP 地址和 MAC 地址。

表 7.1. 包转发

| leftmost 计算机 | 路由器 | rightnet 计算机 |
|---|---|---|
| MAC | | |
| IP | | |

3. 你如何验证路由器默认是否允许包转发？测试从路由器 `ping` 到两台机器，以及从那两台机器 `ping` 到路由器。使用 `arp -a` 确保你连接到了正确的 MAC 地址。

4. 从 `leftnet` 计算机 `ping` 到 `rightnet` 计算机。在路由器上启用或禁用包转发，并验证两个网络之间的 `ping` 发生了什么。如果你未能成功 `ping` 通通两个网络（位于不同的子网），请使用 `wireshark` 或 `tcpdump` 等数据嗅探器来发现问题。

5. 使用 `wireshark` 或 `tcpdump` 回答以下问题：当数据包通过时，源 MAC 会变化吗？目标 MAC 呢？源和目标 IP 呢？

6. 路由器上的第三张网卡？将此网卡连接到互联网。

```
rootrouter-# dhclient eth0
```

你现在的设置类似于这张图。给 `leftnet` 和 `rightnet` 提供访问需要做什么？

![](img/1d499a6177836f6f088a9e2a53e11a14_125_0.png)

## 7.15. 解决方案：包转发

```
Adapter 1: Intel PRO/1000 Desktop (bridged AdapterPort)
Adapter 2: Intel PRO/1000 Desktop (Internal Network, 'leftnet')
Adapter 3: Intel PRO/1000 Desktop (Internal Network, 'rightnet')
```

1. 设置两台 `Linux` 机器，一台在 `leftmost`，另一台在 `rightnet`。确保它们都在正确的子网中获取 IP 地址。这两台机器将是“路由器”的“左侧”和“右侧”。

![](img/1d499a6177836f6f088a9e2a53e11a14_126_0.png)

你计算机上的 IP 配置应该类似于这两个截图。两台机器必须位于不同的子网（这里是 `192.168.60.0/24` 和 `192.168.70.0/24`）。我在两台机器上都创建了一个小脚本来配置接口。

```
root@# cat leftnet.sh
pkill dhclient
ifconfig eth0 192.168.60.8 netmask 255.255.255

root@# cat rightnet.sh
pkill dhclient
ifconfig eth0 192.168.70.9 netmask 255.255.255
```

2. 设置第三台带有三个网卡的 `Linux` 计算机，一台在 `leftnet`，另一台在 `rightnet`。这台计算机将作为“路由器”。在下表中填写相关的名称、IP 地址和 MAC 地址。

```
root@# cat router.sh
ifconfig eth1 192.168.60.1 netmask 255.255.255
ifconfig eth2 192.168.70.1 netmask 255.255.255
echo 1 > /proc/sys/net/ipv4/ip_forward
```

你的设置可能使用下表中不同的 IP 和 MAC 地址。



| left 计算机 | 路由器 | rightnet 计算机 |
|---|---|---|
| `08:00:27:f6:ab:b9` | `08:00:27:13:f5:a` | `08:00:27:bc:4a:6b` |
| `192.168.60.8` | `192.168.60.1` | `192.168.70.1` |

### 3. 如何验证路由器默认是否允许数据包转发？

测试从路由器 ping 到另外两台机器，以及从那两台机器到路由器。使用`arp -a`确保你连接的是正确的 MAC 地址。

这可以通过`grep ip_forward /etc/sysctl.conf`（`1`为启用，`0`为禁用）或使用`sysctl -a | grep ip_forward`来完成。

```
root@router-# grep ip_forward /etc/sysctl.conf
net.ipv4.ip_forward = 0
```

### 4. 从左电脑 ping 到右电脑

在路由器上启用/禁用数据包转发，并验证两个网络之间的 ping 发生了什么变化。如果你无法在两个网络（不同子网）之间进行 ping，请使用`wireshark`或`tcpdump`等嗅探器来发现问题。

你是否忘记为局域网机器添加默认网关？使用`route add default gw 'ip-address'`。

```
root@left-# route add default gw 192.168.60.1
root@right-# route add default gw 192.168.70.1
```

当数据包转发启用（且默认网关配置正确）时，你应该能够成功 ping。当数据包转发禁用或网关配置不正确时，ping 将无法工作。

### 5. 使用 wireshark 或 tcpdump 分析数据包

使用`wireshark`或`tcpdump -xx`来回答以下问题。数据包通过过滤器时，源 MAC 会发生变化吗？目的 MAC 呢？源和目的 IP 地址呢？

通过路由器时，两个 MAC 地址都会发生变化。像这样使用`tcpdump -xx`：

```
root@router-# tcpdump -xx -i eth1
root@router-# tcpdump -xx -i eth2
```

## 路由器简介

### 6. 连接互联网

还记得路由器上的第三张网卡吗？将此网卡连接到带有互联网的局域网。在许多局域网中，`dhclient eth0`命令可以直接运行（将`eth0`替换为正确的接口）。

```
root@router~# dhclient eth0
```

你现在有了与图片类似的设置。需要执行什么操作才能为`leftnet`和`rightnet`提供互联网访问。

![](img/1d499a6177836f6f088a9e2a53e11a14_128_0.png)

`leftnet`和`rightnet`上的客户端需要一个工作的`dns server`。我们在这里使用 Google 的 dns 服务器之一。

```
echo nameserver 8.8.8.8 > /etc/resolv.conf
```

# 第 8 章 iptables 防火墙

本章介绍了一些简单的防火墙规则以及如何使用`iptables`配置它们。

`iptables`是一个允许用户配置 Linux 内核内置防火墙功能的应用程序。

## 8.1. iptables

默认情况下，内核中有三张包含一组组规则的表。

`filter`表用于数据包过滤。

```
root@debian6~# iptables -t filter -L
Chain INPUT (policy ACCEPT)
  target     prot source destination
Chain FORWARD (policy ACCEPT)
  target     prot source destination
Chain OUTPUT (policy ACCEPT)
  target     prot source destination
```

`nat`表用于地址转换。

```
root@debian6~# iptables -t nat -L
Chain PRERUTING (policy ACCEPT)
  target     prot source destination
Chain POSTROUTING (policy ACCEPT)
  target     prot source destination
Chain OUTPUT (policy ACCEPT)
  target     prot source destination
```

`mangle`表可用于数据包的特殊处理。

每个表中的规则系列称为`chain`。我们稍后会讨论链。

## 8.2. 启动和停止 iptables

下面的截图显示了如何在 Red Hat/Fedora/CentOS 兼容发行版上启动和停止`iptables`。

```
root@centos6 ~# service iptables stop
root@centos6 ~# service iptables start
iptables: Applying firewall rules  [ ok ]
root@centos6 ~#
```

Debian 和 Ubuntu 没有这个脚本，但可以卸载。

```
root@debian6~# aptitude purge iptables
```

## 8.3. filter 表

### 8.3.1 关于数据包过滤

`数据包过滤`比数据包转发复杂一点。数据包转发仅使用路由表做决策，而数据包过滤使用规则列表。内核将根据这些规则决定对每个数据包进行什么操作。

#### 8.3.2. filter 表

`iptables`中的`filter`表有三个链（规则组）。`INPUT`链用于进入系统的数据包。`OUTPUT`链用于离开系统的数据包。`FORWARD`链用于通过系统转发（路由）的数据包。

![](img/1d499a6177836f6f088a9e2a53e11a14_131_0.png)

截图显示了如何列出`filter`表及其所有规则。

```
[root@RHEL5]# iptables -t filter -nL
Chain INPUT (policy ACCEPT)
  target     prot source destination
Chain FORWARD (policy ACCEPT)
  target     prot source destination
Chain OUTPUT (policy ACCEPT)
  target     prot source destination
[root@RHEL5]#
```

你可以看到，`filter`表中的三个链都设置为`ACCEPT`。`ACCEPT`是默认行为。

#### 8.3.3. 设置默认规则

规则的默认确实是`ACCEPT`所有。这不是最安全的防火墙。更安全的设置是`DROP`所有。被丢弃的数据不会在任何链中继续，也不会向任何地方发送警告或错误。

下面的命令将锁定计算机。不要在`ssh` shell 内部执行这些命令。

```
root@debianpaul:~# iptables -P INPUT DROP
root@debianpaul:~# iptables -P OUTPUT DROP
root@debianpaul:~# iptables -P FORWARD DROP
root@debianpaul:~# iptables -L
```

```
Chain INPUT (policy DROP)
  target     prot source destination

Chain FORWARD (policy DROP)
  target     prot source destination

Chain OUTPUT (policy DROP)
  target     prot source destination
```

#### 8.3.4. 修改策略规则

首先，让我们所有链的默认策略设置为`drop`。注意，输入此命令时可能会丢失连接；

```
[root@RHEL5 ~]# iptables -P INPUT DROP
[root@RHEL5 ~]# iptables -P FORWARD DROP
[root@RHEL5 ~]# iptables -P OUTPUT DROP
```

接下来，我们允许服务器使用自己的回环设备（这允许链访问在`localhost`上运行的服务）。我们首先向`INPUT`链添加规则允许来自`lo`（回环）接口的流量，然后对通过回环接口离开系统的数据包执行相同的操作。

查看`filter`表（省略`-filter`因为它是默认表）：

```
[root@RHEL5 ~]# iptables -nL
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT
```



```
Chain INPUT (policy DROP)
  target     prot source destination
ACCEPT     all

Chain FORWARD (policy DROP)
  target     prot source destination

Chain OUTPUT (policy DROP)
  target     prot source destination
```

### 8.3.5. 允许通过 eth0 使用 ssh

此示例显示了如何添加两条规则允许通过 `eth0` 使用 `ssh`。

```
root@RHEL5 ~]# iptables -A INPUT -i eth0 -j ACCEPT
root@RHEL5 ~]# iptables -A OUTPUT -o eth0 -j ACCEPT
```

`filter` 表看起来像这样 (`-v`)：

```
root@RHEL5 ~]# iptables -nv
Chain INPUT (policy DROP 7 packets, 609 bytes)
pkts bytes target opt in out destination
0 0 ACCEPT all * * lo 0.0.0.0/0 0.0.0/0
0 0 ACCEPT tcp * eth0 0.0.0.0/0 0.0.0/0 tcp dpt:22

Chain FORWARD (policy DROP 0 packets, 0 bytes)
pkts bytes target opt in out destination

Chain OUTPUT (policy DROP 3 packets, 228 bytes)
pkts bytes target opt in out destination
0 0 ACCEPT all * * lo 0.0.0.0/0 0.0.0/0
0 0 ACCEPT tcp * eth0 0.0.0.0/0 0.0.0/0 tcp dpt:22
```

### 8.3.6. 从子网访问任何计算机

此示例显示了如何从 `10.1.1.0/24` 网络访问任何计算机，但仅通过 `eth1`。这不是代理（应用）级别的问题。

```
root@RHEL5 ~]# iptables -A INPUT -i eth1 -s 10.1.1.0/24 -p tcp -j ACCEPT
root@RHEL5 ~]# iptables -A OUTPUT -o eth1 -d 10.1.1.0/24 -p tcp -j ACCEPT
```

结合之前的示例，策略正在扩展：

```
root@RHEL5 ~]# iptables -nv
Chain INPUT (policy DROP 7 packets, 609 bytes)
pkts bytes target opt in out destination
0 0 ACCEPT all * * lo 0.0.0.0/0 0.0.0/0
0 0 ACCEPT tcp * eth0 0.0.0.0/0 0.0.0/0 tcp dpt:22
0 0 ACCEPT tcp * eth1 0.0.0.0/0 10.1.1.0/24

Chain FORWARD (policy DROP 0 packets, 0 bytes)
pkts bytes target opt in out destination

Chain OUTPUT (policy DROP 3 packets, 228 bytes)
pkts bytes target opt in out destination
0 0 ACCEPT all * * lo 0.0.0.0/0 0.0.0/0
0 0 ACCEPT tcp * eth0 0.0.0.0/0 0.0.0/0 tcp dpt:22
0 0 ACCEPT tcp * eth1 0.0.0.0/0 10.1.1.0/24
```

### 8.3.7. iptables 保存

使用 RHEL 的 `iptables` 在防火墙启动（重）启动时自动实现这些规则。

```
[root@RHEL ~]# # /etc/init.d/iptables save
Saving iptables rules to /etc/sysconfig/iptables:
[root@RHEL ~]# #
```

### 8.3.8. 脚本示例

你可以为这些规则编写一个简单的脚本。以下是一个实现了你在之前章节中看到的防火墙规则的示例脚本。

```bash
#!/bin/bash
# 首先清理一切
iptables -t filter -F
iptables -t filter -X
iptables -t nat -F
iptables -t nat -X

# 默认拒绝
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

# 允许回环设备
iptables -A INPUT -o lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# 允许外部通过 eth0  ssh 访问系统
iptables -A INPUT -i eth0 -p tcp --dport 22 -j ACCEPT
iptables -A OUTPUT -o eth0 -p tcp --sport 22 -j ACCEPT

# 允许从 10.1.1.0/24 到系统的任何流量
iptables -A INPUT -i eth -s 10.1.1.0/24 -p tcp -j ACCEPT
iptables -A OUTPUT -o eth -d 10.1.1.0/24 -p tcp -j ACCEPT
```

### 8.3.9. 允许 ICMP(ping)

当你启用 `iptables` 时，在尝试 `ping` 其他主机时会收到“Operation not permitted”（操作不允许）的消息的消息。

```
[root@RHEL5 ~]# ping 192.168.187.130
PING 192.168.187.130 (192.168.187.130) 56(84) bytes of data.
ping: sendmsg: Operation not permitted
ping: sendmsg: Operation not permitted
```

下面的截图显示了如何设置 `iptables` 以允许从或向你的机器进行 `ping`。

```
[root@RHEL5 ~]# iptables -A INPUT -p icmp --icmp-type any -j ACCEPT
[root@RHEL5 ~]# iptables -A OUTPUT -p icmp --icmp-type any -j ACCEPT
```

前两行并不允许其他计算机通过你的路由器路由 `ping` 消息，因为它们只处理了 `INPUT` 和 `OUTPUT`。对于 `ping` 的路由，你需要在 `FORWARD` 链上启用它。以下命令启用了网络间 `icmp` 消息的路由。

```
[root@RHEL5 ~]# iptables -A FORWARD -p icmp --icmp-type any -j ACCEPT
```

## 8.4. 练习：数据包过滤

1. 确保在 `iptables` 激活时，你可以 `ssh` 到你的路由器系统。

2. 确保在 `iptables` 激活时，你可以 `ping` 你的路由器系统。

3. 将你的其中一个网络定义为“内部”(internal)，另一个定义为“外部”(external)。配置路由器允许访问网站 (`http`) 的流量从内部网络到外部网络（但反向方向不行）。

4. 确保内部网络可以 `ssh` 到外部，但反之则不然。

## 8.5. 解决方案：数据包过滤

可能的解决方案，其中 `leftnet` 是内部网络，`rightnet` 是外部网络。



```bash
#!/bin/bash

# 首先清理一切
iptables -t filter -F
iptables -t filter -X
iptables -t nat -F
iptables -t nat -X

# 默认拒绝
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT DROP

# 允许回环
iptables -A INPUT -o lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# 问题 1：通过 eth0 允许 ssh
iptables -A INPUT -i eth0 -p tcp --dport 22 -j ACCEPT
iptables -A OUTPUT -o eth0 -p tcp --sport 22 -j ACCEPT

# 问题 2：允许任何地方 icmp(ping)
iptables -A INPUT -p icmp --icmp-type any -j ACCEPT
iptables -A FORWARD -p icmp --icmp-type any -j ACCEPT
iptables -A OUTPUT -p icmp --icmp-type any -j ACCEPT

# 问题 3：允许内部(leftnet) 到外部(rightnet) 的 http
iptables -A FORWARD -i eth1 -o eth2 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -m state ESTABLISHED,RELATED -j ACCEPT

# 问题 4：允许内部(leftnet) 到外部(rightnet) 的 ssh
iptables -A FORWARD -i eth1 -o eth2 -p tcp --dport 22 -j ACCEPT
iptables -A FORWARD -m state ESTABLISHED,RELATED -j ACCEPT

# 允许外部(rightnet) 到内部(leftnet) 的 http
iptables -A FORWARD -i eth2 -o eth1 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -m state ESTABLISHED,RELATED -j ACCEPT

# 允许外部通过 eth0  rpc
iptables -A INPUT -i eth0 -p tcp --dport 111 -j ACCEPT
iptables -A OUTPUT -o eth0 -p tcp --sport 111 -j ACCEPT
```

## 8.6. 网络转换

NAT 设备是一种同时也更改数据包源地址和目的 IP 地址的路由器。它通常用于将私有地址范围内的多个计算机连接到公共互联网。NAT 的开发是为了从互联网隐藏内部网络，允许私有地址访问互联网。`iptables` 中的 NAT 添加了两个新链：`PREROUTING` 在数据包到达 `INPUT` 链之前修改；`POSTROUTING` 在数据包退出 `OUTPUT` 链之后修改。使用 `iptables -t nat -L` 查看 NAT 表。下面的截图显示了一个空的 NAT 表。

```
[root@RHEL]# iptables -t nat -L
Chain PREROUTING (policy ACCEPT)
  target     prot opt source
Chain POSTROUTING (policy ACCEPT)
  target     prot opt source
Chain OUTPUT (policy ACCEPT)
  target     prot opt source
```

### 8.6.2. SNAT (源 NAT)

源 nat 的目标是在数据包离开系统之前更改其源地址。这意味着 NAT 设备需要在内存中保留所有已更改数据包的表，以便将其交付给原始源。由于 SNAT 针对离开系统的包，我们使用 `POSTROUTING` 链。这是一个 SNAT 规则示例。该规则规定来自 `10.1.1.0/24` 网络并离开 `eth1` 的包将设置为公共 IP。

```bash
iptables -t nat -A POSTROUTING -o eth1 -s 10.1.1.0/24 -j SNAT --to-source 192.168.1.1
```

当然，必须存在正确的 `iptables` 过滤设置允许数据包从一个网络到另一个网络。

### 8.6.3. SNAT 示例

此示例使用了典型的 nat 设置。内部 (`eth0`) 网络通过 SNAT 访问外部 (`eth1`) Web 服务器（端口 80）。

```bash
#!/bin/bash
#  nat 的 iptables 脚本
# eth0 是内部网络，eth1 是互联网
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD DROP
iptables -A FORWARD -i eth0 -o eth1 -s 10.1.1.0/24 -p tcp --dport 80 -j ACCEPT
iptables -A FORWARD -i eth1 -o eth0 -d 10.1.1.0/24 -p tcp --sport 80 -j ACCEPT
iptables -t nat -A POSTROUTING -o eth1 -s 10.1.1.0/24 -j SNAT --to-source 192.168.1.1
```

## 8.6.4. IP 伪装 (Masquerading)

IP 伪装与 SNAT 非常相似，但用于动态接口。典型的示例是连接到互联网的宽带“路由器/调制调器”，它们每次冷启动都会从 ISP 接收不同的 IP。将 SNAT 脚本转换为伪装只需要一行。

```
iptables -t nat -A POSTROUTING -o eth1 -s 10.1.1.0/24 -j MASQUERADE
```

## 8.6.5. DNAT (目的 NAT)

DNAT 通常用于将来自互联网的数据包重定向到内部服务器（位于你的 DMZ 中），位于无法从互联网直接访问的私有地址范围。此示例脚本允许互联网用户通过 `ssh` (端口 22) 访问你的内部 (`192.168.1.99`) 服务器。

```bash
#!/bin/bash
# DNAT 的 iptables 脚本
# eth0 是内部网络，eth1 是外部
echo 0 > /proc/sys/net/ipv4/ip_forward
iptables -P INPUT ACCEPT
iptables -P OUTPUT ACCEPT
iptables -P FORWARD DROP
iptables -A FORWARD -i eth1 -o eth0 -p tcp --dport 22 -j DNAT --to-destination 192.168.1.99
```



# 第 15 章 Samba 安全性

15.1. 基于用户名的安全
15.2. 基于 IP 地址的安全
15.3. 隐性实现安全
15.4. 文件系统安全
15.5. 实践：保护共享
15.6. 解决方案：保护共享

# 第 16 章 Samba 域成员

16.1. `smb.conf` 中的更改
16.2. 加入 Active Directory 域
16.3. `winbind`
16.4. `wbinfo`
16.5. `getent`
16.6. 文件所有权
16.7. 实践：Samba 域成员

# 第 17 章 Samba 域控制器

17.1. 关于域控制器
17.2. 关于安全模式
17.3. 关于密码后端
17.4. `smb.conf` 中的 `[global]` 节
17.5. `netlogon` 共享
17.6. 其他 `[share]` 节
17.7. 用户与组
17.8. `tdsams`
17.9. 关于计算机账户
17.10. 本地或漫游配置文件
17.11. NTFS ACLs 中的组
17.12. 登录脚本
17.13. 实践：Samba 域控制器

# 第 18 章 Samba 4 简览

18.1. Samba 4 alpha 6

# 第 9 章 Samba 简介

本 Samba 服务器简介简单解释了如何安装 Samba 3，并简要提到了 SMB 协议。

## 9.1. 验证已安装的版本

### 9.1.1. 基于 `.rpm` 的发行版

要查看 Red Hat、Fedora 或 CentOS 上安装的 `samba` 版本，请使用 `rpm -q samba`。

```bash
root@RHEL52 ~]# rpm -q samba

samba-3.0.28-1.el5_2.1
```

上面的截图显示 RHEL 已安装 `Samba` 版本 3.0。Samba 版本号中的最后一个数字表示更新或补丁的数量。

下方是在安装了 Samba 3.5 版本的较新 CentOS 上运行相同命令的结果。

```bash
root@centos6 ~]# rpm -q samba

samba-3.5.10-116.el16_2.1686
```

### 9.1.2. 基于 `.deb` 的发行版

在 Debian 或 Ubuntu 上使用 `dpkg -l` 或 `aptitude show`。Debian 7.0 (Whezy) 和 Ubuntu 12.04 (Precise) 都使用 Samba 服务器的 3.6.3 版本。

```bash
root@debian7~# aptitude show samba | grep Version

Version: 2.3.6-1
```

Ubuntu 12.04 目前处于 Samba 版本 3.6.3。

```bash
root@ubuntu1204:~# dpkg -l samba | tail -1

ii samba 2:3.6.3-2ubuntu1 SMB/CIFS 文件、打印和 Unix 登录服务器
```

## 9.2. 安装 `samba`

### 9.2.1. 基于 `.rpm` 的发行版

Red Hat Linux 默认安装 Samba。如果尚未安装 Samba，可以使用图形界面（应用程序--设置--添加/删除应用程序）并选择“Windows 文件服务器”。非图形的方法是使用 `rpm` 或 `yum`。

当你下载了 `.rpm` 文件时，可以这样安装 Samba：

```bash
[paul@RHEL52 ~]$ rpm -i samba-0.0.28-1.el5_2.rpm
```

`yum` 命令在 Fedora 和 CentOS 上默认可用（RHN 网络）。

```bash
root@centos6 ~]# yum install samba
```

### 9.2.2. 基于 `.deb` 的发行版

Ubuntu 和 Debian 用户可以使用 `aptitude` 程序（或 Synaptic 等图形化工具）。

```bash
root@debian7# aptitude install samba

将安装下列软件包：

samba-common(a) samba-common-bin(a) tdb-tools(a)

0 个软件包升级，4 个新安装，0 个删除，1 个未升级。

需要获取 15.1 MB 的存档。解压缩后将使用 42.9 MB。

继续吗？Y/n?
```

## 9.3. 文档

### 9.3.1. Samba

Samba 提供了 `html` 和 `pdf` 格式的优秀文档（也可以从 `samba.org` 免费下载并作为书籍）。文档是一个独立的包，如果你想在服务器本身上使用，请安装它。

```bash
root@centos6 ~]# yum install samba-doc

...

root@centos6 ~]# ls -l /usr/share/doc/samba-doc-3.5.10/

total 10916

drwxr-xr-x. 6 root 4096 May 6 15:50 htmldocs

-rw-r--r-- 1 root 460546 Jun 14 2011 Samba3-Example.pdf

-rw-r--r-- 1 root 608260 Jun 14 2011 Samba3-Developers-Guide.pdf
```

操作适用于 Ubuntu 和 Debian。

## 9.4. 启动与停止

可以通过调用 `/etc/init.d/samba` 来启动守护进程。

```bash
root@centos6 ~]# /etc/init.d/samba stop

  停止 Samba
```



```bash
root@centos6 ~]# /etc/init.d/samba start
```

启动 `Samba`

```bash
root@centos6 ~]# /etc/init.d/samba restart
```

重启 `Samba`

```bash
root@centos6 ~]# /etc/init.d/samba status
```

检查 `Samba`

## 9.5. Samba 守护进程

`Samba 3` 由三个守护进程组成，分别名为 `nmbd`、`smbd` 和 `winbind`。

### 9.5.1. nmbd

`nmbd` 守护进程处理名称。它注册并解析名称。根据文档，它应该是第一个启动的守护进程。

```bash
root@RHEL52 ~]# ps -C nmbd

PID TTY TIME

5681 ? 00:00:00 nmbd
```

### 9.5.2. smbd

`smbd` 守护进程管理文件传输和身份验证。

```bash
root@RHEL52 ~]# ps -C smbd

PID TTY TIME

5678 ? 00:00:00 smbd
5683 ? 00:00:00 smbd
```

### 9.5.3. winbind

`winbind` 守护进程仅用于处理 `Windows` 域成员。注意 `winbind` 是通过 `/etc/init.d/winbind` 启动的。

```bash
root@RHEL52 ~]# ps -C winbind

PID TTY TIME

5752 ? 00:00:00 winbind
5754 ? 00:00:00 winbind
```

## 9.6. SMB 协议

### 9.6.1. 简史

该协议的发展由 `IBM` 在 80 年代初开始。到 80 年代末，大部分开发由 `Microsoft` 完成。`SMB` 是一种运行在 `NetBIOS/NetBEUI` 之上的应用层协议，也可以运行在 `tcp/ip` 之上。

1996 年，`Microsoft` 要求对协议进行记录。他们将 `CIFS`（通用互联网文件系统）作为互联网草案提交，但从未获得 `RFC` 状态。

2004 年，欧盟决定 `Microsoft` 应该对该协议进行记录，以便其他开发者编写兼容软件。2007 年 12 月 20 日，`Microsoft` 达成了协议。`Samba` 团队现在可以访问 `SMB/CIFS`、`Windows` 工作组和 `Active Directory` 文档。

### 9.6.2. 广播协议

`SMB` 使用 `NetBIOS` 服务定位协议，这是一种广播协议。这意味着 `NetBIOS` 名称在网络上必须是唯一的（即使你有不同的 `IP` 地址）。

### 9.6.3. NetBIOS 名称

`NetBIOS` 名称与主机名相似，但始终全大写且长度仅为 15 个字符。`Microsoft Windows` 计算机和 `Samba` 服务器会在网络上广播此名称。

### 9.6.4. 网络带宽

在网络中有许多广播的 `SMB/CIFS` 计算机会导致带宽问题。解决方案可以是使用 `NetBIOS` 名称服务器 (`NBNS`)，例如 `WINS`（`Windows` 互联网命名服务）。

## 9.7. 练习：Samba 简介

- 0. 确保你知道自己的学号，你命名的*任何任何东西*都必须包含你的学号！
- 1. 验证你能够登录 `Linux/Unix` 计算机。记录这台计算机的名称和 `IP` 地址。
- 2. 对你可用的其他所有（虚拟机）也执行相同的操作。
- 3. 通过 `ping` 计算机验证网络连接，编辑相应的 `hosts` 文件以便使用名称。通过 `ping` 这些名称来测试可用性。
- 4. 确保已安装 `Samba`，记录 `Samba` 的版本。
- 5. 打开你电脑上安装的官方 `Samba-3 howto pdf` 文件。该文件有多少页 `A4` 纸？然后查看 `samba.org` 上的同一份 `pdf`，它是定期更新的。
- 6. 停止 `Samba` 服务。

# 第 10 章：开始使用 Samba

## 10.1. /etc/samba/smbd.conf

### 10.1.1. smbd -b

`Samba` 配置在 `smb.conf` 文件中完成。可以手动编辑该文件，也可以使用像 `webmin` 这样的基于 `Web` 的界面进行管理。该文件通常位于 `/etc/samba`。你可以通过 `smbd -b` 找到确位置。

```bash
[root@RHEL4 ~]# ls smbd -b | grep CONFIGFILE

CONFIGFILE:/etc/samba/smbd.conf
```

### 10.1.2. 默认的 smb.conf

默认的 `smb.conf` 文件包含带有解释的示例列表。

```bash
[paul@RHEL4 ~]# ls -l /etc/samba/smbd.conf

-rw-r--r-- 1 root 10386 May 30 23:08 /etc/samba/smbd.conf
```

在 `Ubuntu` 和 `Debian` 上，`smb.conf` 包含了大量的示例和解释。

```bash
[paul@laika:~]# ls -l /etc/samba/smbd.conf

-rw-r--r-- 1 root 10515 2007-05-24 00:21 /etc/samba/smbd.conf
```

### 10.1.3. 极简的 smbd.conf

下面是一个极简 `smbd.conf` 的示例。它允许 `Samba` 进行通信，并对其他计算机可见（`Microsoft` 在“网络邻域”或“我的网络位置”中显示计算机）。

```ini
[paul@RHEL4 ~]# cat /etc/samba/smbd.conf

[global]

group = WORKGROUP

[firstshare]

path = /srv/samba/public
```

### 10.1.4. net view

下面是 `Microsoft Windows Server 2003 sp2` 上 `net view` 命令的截图。它显示了 `Red Enterprise Linux 5.3` 和一台 `Ubuntu 9.04 Samba` 服务器（都使用了极简的 `smbd.conf`）是如何对附近的 `Microsoft` 计算机可见的。

![](img/1d499a6177836f6f088a9e2a53e11a14_153_0.png)

### 10.1.5. smbd.conf 中的长行

`smbd.conf` 中的某些参数后面可以跟一个值列表。你可以通过在行尾添加反斜线 `\` 在下一行继续写（为了清晰）：

```bash
valid users = Serena, Venus, Lindsay \
```

### 10.1.6. smb.conf

虽然很奇怪但确实是：`smb.conf` 接受像 `create mode` 和 `create mask` 这样的同义词，并且（有时）缺失错误是可以被浏览的。在某些情况下你可以切换单词，`guest only` 参数与 `only guest` 是相同的。`Writable = yes` 等同于 `readonly = no`。

### 10.1.7. man smb.conf

执行 `man smb.conf` 时，你可以访问大量的文档。

```bash
[root@RHEL4b samba]# apropos samba

cupsaddmb -8 export printers for samba for windows clients

imhosts -5 The Samba NetBIOS file

net -8 for administration of Samba and remote CIFS servers

-8 manage the SAM database (Database of Samba Users)

pdbdeit -7 Windows Samba/CIFS server for UNIX

samba -5 smb.conf The configuration file for the Samba suite

smbpasswd -5 Samba user and password file

smbstatus -8 report on current Samba connections

swat -8 Samba Tool for backing up .tdb files

[root@RHEL4b samba]#
```

## 10.2. /usr/bin/testpar

### 10.2.1. smb.conf 语法检查

要验证 `smb.conf` 文件的语法，可以使用 `testpar`。

```bash
[paul@RHEL4b]$ testpar

Load smb config files from /etc/samba/smbd.conf

Processing section "[firstshare]"

Loaded services OK.

Server role: ROLE_STANDONE

Press enter to see dump of service definitions
```

### 10.2.2. testpar -v

一个有趣的选项是 `testpar -v`，它会输出所有全局选项及其默认值。

```



### 10.2.2. `testpar` 命令输出示例

`[root@RHEL4b]# testpar -v |`

```
Load smb config files from /etc/samba/smbd.conf

Processing section "[pub]"

Processing section "[global]"

Loaded services OK.

Server role: ROLE_STANDONE

Press enter to see dump of service definitions
```

```
[global]

dos charset = CP85
unix charset = UTF-8
display charset = LOCALE
workgroup = WORK

realm =
netbios name =
netbios scope =
server string = Samba 3.0.2
```

Samba 3.0.x 中的 `smb` 参数大约有 350 个默认值。在 Samba 3.5.x 中，这个数字增加到了近 400 个。

### 10.2.3. `testpar -s`

Samba 守护一直在检查 `smb.conf` 文件，因此保留此文件是一个良好的习惯。但记录你的 Samba 配置并显式设置具有默认值的选项也是一种良好的习惯。`testpar -s` 选项允许你同时完成这两点。它将输出尽可能小的配置，同时保留你的设置。其思想是将你的 Samba 配置放在另一个文件（如 `smb.conf`）中，并让 `testpar` 为你解析。下面显示了设置了 `workgroup` 为 `WORKGROUP` 的第一个 `smb.conf` 文件。

```
@root@RHEL4b samba)# cat smb.conf.full

[global]

workgroup = WORKGROUP

# is a demo of documented smb.conf

# These two lines are removed by testpar -s

server string = Public Server
```

接下来，我们使用 `-s` 选项执行并将标准输出重定向到真实的 `smb.conf` 文件。

```
@root@RHEL4b samba)# testpar -s smb.conf.full > smb.conf

Load smb config files from smb.conf.full

Processing section "[firstshare]"

Loaded services file OK.

[firstshare]

path = /srv/samba/public

[root@RHEL4b samba)# cat smb.conf

[global]

server string = Public Server

[firstshare]

path = /srv/samba/public

[root@RHEL4b samba)#
```

下面是最终结果。那两个注释和默认选项不再存在了。

## 10.3. /usr/bin/smbclient

### 10.3.1. `smbclient` 查看 Samba

通过 `smbclient`，你可以从 SMB 服务器浏览并共享信息。它将显示你所有的共享、工作组以及主浏览器（Master Browser）的名称。添加 `-N` 选项是为了避免输入空密码。`-L` 选项后跟着要检查的主机名称。

```
root@RHEL4b init.d# smbclient -NL rhel4b

Anonymous login successful

Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]
```

| Sharename | Type | Comment |
| --- | --- | --- |
| firstshare | Disk | |
| IPC$ | IPC | IPC Service (Public Test Server) |
| ADMIN$ | IPC | IPC Service (Public Test Server) |
| Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]| | |

| Server | Comment |
| ------ | ----- |
| RHEL4B | Public Test Server WINXP |
| ------ | ---- |
| Workgroup | Master |
| ------ | ---- |
| WORKGROUP | WINXP |

### 10.3.2. `smbclient` 匿名

下面的截图是 Microsoft Windows Server 2003 sp2 上的 `net view` 命令。它显示了 Red Enterprise Linux 5.3 和一台 Ubuntu 9.04 Samba 服务器（都使用了极简的 `smbd.conf`）是如何对附近的微软计算机可见的。

![](img/1d499a6177836f6f088a9e2a53e11a14_153_0.png)

### 10.3.3. `smbclient` 认证

下面的截图使用 `smbclient` 显示关于匿名 Samba 的信息。

```
root@RHEL4b smclient -L 127.0

Anonymous login successful

Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]
```

| Sharename | Type | Comment |
| --- | --- | --- |
| firstshare | Disk | |
| IPC$ | IPC | IPC Service (Public Test Server) |
| ADMIN$ | IPC | IPC Service (Public Test Server) |
| Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0.10-1.4.E]| |

| Server | Comment |
| ------ | ----- |
| RHEL4B | Public Test Server WINXP |
| ------ | ---- |
| Workgroup | Master |
| ------ | ---- |
| WORKGROUP | WINXP |

### 10.3.4. `smbclient` 使用凭据

Windows xp 和 2003 不接受匿名访问（`NT_STATUS_DENIED`）。此示例显示了如何为 `smbclient` 提供凭据。

```
[paul@RHEL5] smbclient -L target -U administrator
```

| Sharename | Type | Comment |
| --- | --- | --- |
| C$ | Disk | Default share |

```
paul@laika:- $ smbtree

Password:

WORKGROUP

\W2000

\W2000\firstshare

\W2000\C$ Default share

\W2000\ADMIN$ Remote Admin

\W2000\IPC$ Remote IPC

PEGAS55

\WINXP

cli_rpc_pipe_open: nt_name_create failed on pipe \srvpc to machine WINXP.

Error was NT_STATUS_ACCESS_DENIED

RHEL4B Pegasus Domain Member Server

\RHEL4B\ADMIN$ IPC Service (Pegasus Domain Member Server)

\RHEL4B\IPC$ IPC Service (Pegasus Domain Member Server)

\RHEL4B\domainata Active Directory users only

HM2003

cli_rpc_pipe_open: nt_name_create failed on pipe \srvpc to machine HM2003.

Error was NT_STATUS_ACCESS_DENIED

paul@laika:- $
```

上一页幻灯片提供了为什么我们无法在 winxp 和 w2003 电脑上看到共享信息的有用原因。让我们在我们的 RHEL 服务器上尝试 `smbtree`，但这次使用管理员凭据（所有电脑上的凭据都是相同的）。

```
[paul@RHELab -]$ smbtree -Uadministrator%Stargatel

WORKGROUP

\W2000

PEG

\WINXP

\WINXP\C$ Default share
```



\WINXP\ADMIN$ Remote Admin

\WINXP\share55

\WINXP\IPC$ Remote IPC

RHEL4B

Pegasus Domain Member Server

\RHEL4B\ADMIN$ IPC Service (Pegasus Domain Member Server)

\RHEL4B\IPC$ IPC Service (Pegasus Domain Member Server)

\RHEL4B\domainata Active Directory users only

HM2003

\HM2003\NETLOGON server share

\HM2003\SYSVOL Logon server share

\HM2003\WUSStemp A network share used by Local Publishing ...

\HM2003\ADMIN$ Remote Admin

\HM2003\tools Remote IPC

\HM2003\IPC$ A network share to be used by Local ...

\HM2003\WaitContent

\HM2003\C$ Default share

`[paul@RHELab -]`

```
```

如你所见，这对所有 SMB 电脑及其共享提供了一个非常好的概览。

## 10.5. server

`net view` 和 `smclient` 客户端看到的注释是 `server` 选项的默认值。只需将此值添加到 `smb.conf` 的全局部分并重启即可更改它。

```
[root@RHEL53 samba]# testparam -s /dev/null | grep server

server string = Red Hair in Paris
```

稍过之后，更改后的选项在微软电脑上将是可见的。

```
C:\Documents and Settings\Administrator>net view

Server Name	Remark

```

```
\\LAIKA		Ubuntu

\\RHEL53		Red Hat

\\W2003		Antwerp

```

## 10.6. Samba 管理工具 (SWAT)

Samba 附带了一个基于 Web 的工具来管理你的配置文件。可以通过宿主机系统的 `901` 端口使用 Web 浏览器访问 SWAT。检查你的系统使用的是 `inetd` 还是 `superdaemon`。

```
[root@RHEL4b]# ps | grep inetd

1502 pts/0	00:00		inetd

2771 7		00:00		inetd -stayalive -pidfile /var/run/inetd.pid
```

然后编辑 `inetd.conf` 或更改 `/etc/inetd.d/swat` 中的 `disable` 为 `disable = no`。

```
[root@RHEL4b samba]# cat /etc/inetd.d/swat

# default: off

# description: SWAT 是 Samba 管理工具。使用 SWAT 配置你的 Samba 服务器。要使用 SWAT，请用你喜欢的浏览器连接到 901 端口

{

	port= 901

	socket_type= stream

	wait= no

	only_from= 127.0.0.1

	user= root

	server= /usr/sbin/swat

	log_failure+=

	disable= no

}
```

更改 `from` 值以启用对子网中所有电脑的访问。使用 SWAT 时要小心，它会删除 `smb.conf` 中所有手动编辑的注释。

```
[root@RHEL53 tied.d]# grep /etc/inetd.d/swat

only_from=192.168.1.0/24
```

## 10.7. 练习：开始使用 samba

1. 备份原始 `smb.conf` 的副本，并将其命名为 `smb.conf.orig`。
2. 启用 SWAT 并查看它。
3. 停止 Samba 服务器。
4. 创建一个极简的 `smb.conf`。
5. 创建一个极简的 `smb.conf`。
6. 启动 Samba。
7. 验证 Samba 运行正常。
8. 验证另一台电脑可以访问。
9. 使用 `net view` 查看网络。
10. 更改 `smb.conf` 中的参数。
11. 重启 Samba 后，更改项会生效吗？
12. 哪台电脑是主节点？
13. 如果时间允许，安装嗅器。

## 10.8. 答案：开始使用 samba

1. 备份原始 `smb.conf` 的副本，并将其命名为 `smb.conf.orig`。
2. 启用 SWAT 并查看它。
3. 停止 Samba 服务器。
4. 创建一个极简的 `smb.conf`。
5. 使用 `testparam` 查看 `smb.conf`。
6. 启动 Samba。
7. 验证 Samba 运行正常。
8. 验证另一台电脑可以访问。
9. 使用 `net view` 查看网络。
10. 更改 `smb.conf` 中的参数。
11. 重启 Samba 后，更改项会生效吗？
12. 哪台电脑是主节点？
13. 如果时间允许，安装嗅器。

# 第11章. 只读文件服务器

## 11.1. 设置共享目录

让我们开始为 Samba 设置一个非常简单的只读文件服务器。所有人（甚至是匿名游客）都可以访问。

第一步是创建一个目录并在其中放入一些测试文件。

```
[root@RHEL52 ~] mkdir -p /srv/samba/readonly

[root@RHEL52 ~] cd /srv/samba/readonly

[root@RHEL52 readonly]# echo "It is cold today." > water.txt

[root@RHEL52 readonly]# echo "It is hot today." > summer.txt

[root@RHEL52 readonly]# ls -l

total 8

-rw-r--r-- 1 root 17 Jan 21 05:49 summer.txt

-rw-r--r-- 1 root 17 Jan 21 05:49 water.txt

[root@RHEL52 readonly]#
```

# 一个只读文件服务器

```
root@ub1110:~# cat /etc/samba/smb.conf

[global]

workgroup = LINUXTR

netbios name = UBI1110

security = share

[ro1]

path = /srv/samba/readonly

read only = yes

guest ok = yes
```

使用哪种 Linux 发行版其实并不重要。在 Debian 6 上使用相同的配置，效果几乎完全一样。

```
root@debian6:~# cat /etc/samba/smb.conf

[global]

workgroup = LINUXTR

netbios name = DEBIAN6

security = share

[ro1]

path = /srv/samba/readonly

read only = yes

guest ok = yes
```

## 11.3. 重启服务器

测试后，重启 `samba` 服务（这样就不用了）。

```
[root@HEL4b readonly]# smb restart

Shutting down SMB services:      [ OK ]

Shutting down NMB services:      [ OK ]

Starting SMB services:           [ OK ]

Starting NMB services:           [ OK ]
```

## 11.4. 验证共享

### 11.4.1. 使用 smclient 验证

你现在可以使用 `smclient` 验证共享的存在。我们的 `pubread` 被列为第四个共享。

```
[root@HEL52]# smclient -L 127.0.0.1

Domain=[WORKGROUP] OS=[Unix] Server=[Samba 3.0-33]



| 共享名称 | 类型 | 注释 |
| --- | --- | --- |
| `IPC$` | IPC | 共享服务（匿名文件服务器） |
| `pub0` | 磁盘 | |
| `pubread` | 磁盘 | 读取文件 |
| `Server` | 注释 | |

| `TEACHERO` | `Samba 3.0-33` | |
| `W2003EE` | `Master` | |
| `Workgroup` | | |
| `WORKGROUP` | `W2003EE` | |

### 11.4.2. 在 Windows 上验证

最后的测试是进入 Windows 计算机并在 Samba 服务器上读取文件。我们首先使用 `net use` 挂载驱动器 `K` 上的 `pubread` 共享。

```
C:\net use K: teacher\pubread
```

命令执行成功。

然后查看共享的内容。

```
C:\dir k:

驱动器 K 为 pubread

卷序列号为 0C82-11F2

目录的 K:\

21/01/2009  05:49  <DIR>

21/01/2009  05:49  <DIR>

21/01/2009  05:49                summer.txt

21/01/2009  05:49                winter.txt

                               2 个文件              35 字节

                               2 个目录          13,496,242,176 字节可用
```

为了安全起见，让我们尝试写入。

```
K:\echo very > winter.txt

拒绝访问。

K:\
```

或者你可以使用 Windows 资源管理器...

![](img/1d49a617783f6f088a9e2a53e11a14_166_0.png)

## 11.5. 关于 netcat 的说明

Windows 命令行是在 Linux 控制台中通过 `netcat` 管道到 Windows 命令 shell 的。

这种方法的原理是让 `netcat` 在 Windows 计算机上监听特定端口，当收到连接时执行 `cmd.exe`。`netcat` 与 `cat` 的相似之处在于 `cat` 在网络上不做任何操作。

要启用此连接，在 Windows 计算机上输入以下命令（先下载 Windows 版 `netcat`）。

```
nc -l -p 23 -e cmd.exe
```

然后从任何 Linux 计算机使用 `netcat` 连接到这台机器。你在 Linux Shell 中得到一个 `cmd.exe` 提示符。

```
paul@blalka:-$ nc 192.168.1.38 23

Microsoft Windows [版本 5.2.3790]

(C) Copyright 1985-2003 Microsoft Corp.

C:\>net use k: /delete

net use k: /delete

k: 已删除。
```

## 11.6. 练习：只读文件服务器

- 1. 在合适的位置（`FHS`）创建一个目录，供所有人读取文件。
- 2. 确保目录所有权正确且所有人可访问。
- 3. 在该目录放置一个文本文件。
- 4. 使用 `Samba` 共享该目录。
- 5. 从你自己和另一台计算机（`smbclient`, `net use`, ...）验证该共享可以读取。
- 6. 为你的 `smb.conf` 创建一个备份，命名为 `smb.conf.ReadOnlyFileServer`。

## 11.7. 解决方案：只读文件服务器

1. 在合适的位置（`FHS`）创建一个目录，供所有人读取文件。

选择其中一个...

```
mkdir -p /srv/samba/readonly

mkdir -p /home/samba/readonly

/home/paul/readonly/samba 是错误的！！

/etc/samba/readonly 是错误的！！

/readonly 是错误的！！
```

2. 确保目录所有权正确且所有人可访问。

```
chown root:root /srv/samba/readonly

chmod 755 /srv/samba/readonly
```

3. 在该目录放置一个文本文件。

```
echo Hello World > hello.txt
```

4. 使用 `Samba` 共享该目录。

```
你的 smb.conf.readonly 看起来可能像这样：

[global]

workgroup = WORKGROUP

server string = Read Only File Server

netbios name = STUDENTx

security = share

[readonly]

path = /srv/samba/readonly
```

# 12. 可写服务器

## 12.1. 设置目录

在这个示例中，我们将创建一个所有人都可以创建文件的目录。

```
root@RHEL52# mkdir -p /srv/samba/writable
```

## 12.2. 共享

在 `smb.conf` 中有两个参数需要更改。

```
[global]

workgroup = WORKGROUP

server string = Public Server

security = share

[pubread]

path = /srv/samba/readonly

comment = files to read

read only = yes

guest ok = yes
```

## 12.3. 配置

我们只需在 `smb.conf` 中添加一个参数。

```
[pubwrite]

path = /srv/samba/writable

comment = files to write

read only = no

guest ok = yes
```

## 12.4. 在 Windows 上验证

现在我们可以在 Windows 上验证连接的可用性。

```
C:\net use K: teacher0\pubwrite

命令执行成功。
```

## 12.5. 测试写入

我们挂载了驱动器 `K` 上的 `pubread` 共享。

```
C:\dir k:

驱动器 K 为 pubread

卷序列号为 0C82-11F2

目录的 K:\

21/01/2009  05:49  <DIR>

21/01/2009  05:49  <DIR>

21/01/2009  05:49                summer.txt

21/01/2009  05:49                winter.txt

                               2 个文件              35 字节

                               2 个目录          13,496,242,176 字节可用
```

## 12.6. 这是如何可能的？

Linux（或任何 Unix）总是需要用户账户来获取访问。Windows 计算机没有为 `Samba` 提供用户账户或密码。相反，通过此共享创建的文件 Linux 所有者是访客账户（通常名为 `nobody`）。

```
root@RHEL52 samba# ls -l /srv/samba/writable/

total 4

-rwxr-xr-- 1 nobody nobody 6 Jan 21 06:16 hoi.txt
```

所以这不是最干净的解决方案。我们需要改进。

## 12.7. 练习：可写服务器

- 1. 使用 `Samba` 共享一个目录。
- 2. 确保所有人都可以读取和写入文件，使用 `smbclient` 和 Microsoft 计算机测试写入。
- 3. 验证由（各种）用户创建的文件的所有权。

## 12.8. 解决方案：可写服务器

- 1. 使用 `Samba` 共享一个目录。

```
mkdir /srv/samba/writable

chmod 777 /srv/samba/writable
```

# 第 13 章 `samba` 第一个用户账户

## 13.1. 创建 `samba` 用户

我们将为 `samba` 服务器创建一个用户，并让该用户成为目录及其所有文件的所有者。这个匿名用户有一个清晰的描述，但没有登录 shell（登录 shell）。

```
[root@RHEL52 samba]# useradd -s /bin/false sambanobody

[root@RHEL52 samba]# usermod -c "Anonymous Samba Access" sambanobody

[root@RHEL52 samba]# password sambanobody

Changing password for user sambanobody.
```



New UNIX password:

Retype new UNIX password:

`passwd: all authentication tokens updated successfully.`

## 13.2. 文件的所有权

我们可以使用此用户作为文件和目录的所有者，而不是使用 `root` 账户。这种方法清晰且安全得多。

```
[root@RHEL52 samba]# chmod -R sambanobody:sambanobody /srv/samba/
```

```
[root@RHEL52 samba]# ls -al /srv/samba/writable/

drwxrxrwx 2 sambanobody 4096 Jan 21 06:01 ..
drwxrxr-x 6 sambanobody 4096 Jan 21 06:01 ..
-rw-r--r-- 1 sambanobody 6 Jan 21 06:16 hoi.txt
```

## 13.3. /usr/bin/smbpasswd

我们在之前的示例中创建的 `nobody` 用户账户尚未用于 `samba`。只需使用我们为共享而创建的文件和目录即可。本节的目标是强制要求通过 `samba` 共享创建的文件所有权属于我们的 `sambanobody` 用户。记住，我们的服务器仍然对所有人开放，没有人需要知道这个账户或密码。我们只是想要一个干净的 `Linux` 服务器。

为了实现这一点，我们首先必须让 `samba` 知道这个用户。我们可以通过将账户添加到 `smbpasswd` 中来实现这一点。

```
[root@RHEL52 samba]# smbpasswd -a sambanobody

New SMB password:

Retype SMB password:

Added user sambanobody.
```

## 13.4. /etc/samba/smbpasswd

要找到 `samba`（目前）存储这些信息的地方，请使用 `smbd -b`。`PRIVATE_DIR` 变量将向你显示 `smpasswd` 数据库的位置。

```
[root@RHEL52 samba]# smbd -b | grep PRIVATE

PRIVATE_DIR:/etc/samba
```

```
[root@RHEL52 samba]# ls -l /etc/samba/smbpasswd

-rw------- 1 root root 110 Jan 21 06:19 smbpasswd
```

你可以使用简单的 `cat` 命令查看 `smbpasswd` 数据库的内容。`sambanobody` 用户有一个密码（它是秘密的）。

```
[root@RHEL52 samba]# cat smbpasswd
```

## 13.5. passdb 后端

注意，最近版本的 `Samba` 将 `tdbsam` 作为 `passdb backend` 参数的默认值。

```
root@ubull110:~# testparam -v 2>/dev/null | grep 'passdb backend'

passdb backend = tdbsam
```

## 13.6. 强制使用此用户

现在 `Samba` 知道了这个用户，我们可以调整我们的可写共享，以强制通过它创建的文件的所有权。为此，我们使用 `force user` 和 `force group` 选项。现在我们可以确保 `Samba` 可写共享中的所有文件都属于同一个 `sambanobody` 用户。

下面是我们在 `smb.conf` 中对共享的更新定义。

```
[pubwrite]

path = /srv/samba/writable

comment = files to write

force user = sambanobody

force group = sambanobody

read only = no

guest ok = yes
```

当你重新连接到共享并写入文件时，这个 `sambanobody` 用户将拥有新创建的文件（并且没有人需要知道密码）。

## 13.7. 练习：第一个 samba 用户账户

- 1. 创建一个用于 `samba` 的用户账户。
- 2. 将此用户添加到 `samba` 的用户数据库中。
- 3. 创建一个可写入的共享目录，并使用 `force user` 和 `force group` 指令强制文件所有权。
- 4. 使用 `smbclient`、`net use` 和 `Windows` 资源管理器测试 `force user` 的功能。

## 13.8. 解决方案：第一个 samba 用户账户

- 1. 创建一个用于 `samba` 的用户账户。
```
useradd -s /bin/false sambanobody

usermod -c "Anonymous Samba Access" sambanobody

password sambanobody
```
- 2. 将此用户添加到 `samba` 的用户数据库中。
```
smbpasswd -a sambanobody
```
- 3. 创建一个可写入的共享目录，并使用 `force user` 和 `force group` 指令强制文件所有权。
```
[userwrite]

path = /srv/samba/writable

comment = files owned by sambanobody

read only = no

guest ok = yes

force user = sambanobody

force group = sambanobody
```
- 4. 使用 `smbclient`、`net use` 和 `Windows` 资源管理器测试 `force user` 的功能。
```
ls -l /srv/samba/writable (并验证所有权)
```

# 第 14 章 samba 认证

## 14.1. 在 Linux 上创建用户

本示例的目标是设置一个多个用户可以访问的共享。用户在访问此共享之前需要使用密码身份验证。我们将创建三个命名的用户，每个都有自己的密码。首先，我们在 `Linux` 上添加这些用户。

```
[root@RHEL52 samba]# useradd -c "Serena" serena

[root@RHEL52 samba]# useradd -c "Justine" justine

[root@RHEL52 samba]# useradd -c "Martina" martina

[root@RHEL52 samba]# password serena

Changing password for user serena.

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully.

[root@RHEL52 samba]# password justine

Changing password for user justine.

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully.

[root@RHEL52 samba]# password martina

Changing password for user martina.

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully.
```

## 14.2. 在 samba 中创建用户

然后我们将相同的密码它们添加到 `smbpasswd` 文件。

```
[root@RHEL52 samba]# smbpasswd -a serena

New SMB password:

Retype SMB password:

Added user serena.

[root@RHEL52 samba]# smbpasswd -a justine

New SMB password:

Retype SMB password:

Added user justine.

[root@RHEL52 samba]# smbpasswd -a martina

New SMB password:

Retype SMB password:

Added user martina.
```

## 14.3. security = user

记住我们在 `[global]` 段中将 `samba` 的安全模式设置为 `share`。由于我们现在要求用户提供用户名和密码才能访问服务器，我们需要更改这一点。设置 `security = user` 后，`[global]` 段如下所示：

```
[global]

workgroup = WORKGROUP

netbios name = TEACHER
```



`server string = Samba Server`

`security = user`

## 14.4. 配置共享

我们在`smb.conf`中添加`[share]`段（并且不要忘记创建`/srv/samba/authwrite`目录）。

```ini
[authwrite]
path = /srv/samba/authwrite
comment = authenticated users
read only = no
guest ok = no
```

## 14.5. 使用 `net use` 测试访问

重启`Samba`后，我们将从微软计算机测试不同的用户。截图显示了从`Windows XP`使用`net use`。

```bash
C:\>net use m: \\teacher0\authwrite /user:serena

The command completed successfully.
```

```bash
C:\>m:echo greetings from Serena > serena.txt
```

下一张截图是`Windows 2000`上的`martina`，她成功写入了文件，但无法覆盖`serena`文件。

```bash
C:\>net use k: \\teacher0\authwrite /user:martina

The command completed successfully.
```

```bash
C:\>k:

k:\echo greetings from martina > Martina.txt

K:\echo overwrite > serena.txt

Access is denied.
```

## 14.6. 使用 `smbclient` 测试访问

你也可以使用`smbclient`测试带身份的连接。

```bash
[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina wrongpass

session setup failed: NT_STATUS_LOGON_FAILURE
```

然后我们使用正确的密码，并验证我们可以访问共享上的文件。

```bash
[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

smb: \> more serena.txt

getting file serena.txt of size 14 as /tmp/smb.XXXX (6.8 kb/s)

one

two

three

smb: \> q
```

## 14.7. 验证所有权

我们现在有一个带认证访问的简单服务器。共享中的文件属于它们相应的所有者。

```bash
[root@RHEL52 samba]# ls -l /srv/samba/authwrite/

total 8

-rw-r--r-- 1 martina martina 0 Jan 21 20:06 martina.txt

-rw-r--r-- 1 serena serena 14 Jan 21 21:25 serena.txt

-rw-r--r-- 1 serena serena 6 Jan 21 20:09 ser.txt
```

## 14.8. 常见问题

### 14.8.1. `NT_STATUS_BAD_NETWORK_NAME`

当你忘记创建目标目录时，会得到`NT_STATUS_BAD_NETWORK_NAME`。

```bash
[root@RHEL52 samba]# rm -rf /srv/samba/authwrite/

[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

tree connected failed: NT_STATUS_BAD_NETWORK_NAME
```

### 14.8.2. `NT_STATUS_LOGON_FAILURE`

输入错误的密码或使用不存在的用户名时，会得到`NT_STATUS_LOGON_FAILURE`。

### 14.8.3. 用户名大小敏感

记住`Linux`上的用户名是大小敏感的。

```bash
[root@RHEL52 samba]# su - MARTINA

su: user MARTINA does not exist
```

# `Samba` 认证

```bash
[root@RHEL52 samba]# su - martina

[martina@RHEL52 ~]#
```

但微软计算机中的用户名是不区分大小写的。

```bash
[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

smb: \> q

[root@RHEL52 samba]# smbclient //teacher0/authwrite -U MARTINA stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

smb: \> q
```

## 14.9. 练习：`Samba` 认证

- 0. 确保你已经为之前的练习中的`smb.conf`做了适当的备份。
- 1. 创建三个用户（在`Linux`和`Samba`上），并记住它们的密码！
- 2. 设置一个仅允许身份验证用户访问的共享目录。
- 3. 使用`smbclient`和`Windows`计算机访问你的共享，使用多个用户账户（`Windows`需要为此进行注销/重新登录）。
- 4. 验证这些用户创建的文件是否属于他们。
- 5. 尝试从另一个用户处更改或删除文件。

## 14.10. 解决方案：`Samba` 认证

- 1. 创建三个用户（在`Linux`和`Samba`上），并记住它们的密码！

```bash
useradd -c 'SMB user1' user
passwd user
```

- 2. 设置一个仅允许身份验证用户访问的共享目录。
`smb.conf`中的共享部分可能如下：

```ini
[authwrite]
path = /srv/samba/authwrite
comment = authenticated users only
read only = no
guest ok = no
```

- 3. 使用`smbclient`和`Windows`计算机访问你的共享，使用多个用户账户（`Windows`需要为此进行注销/重新登录）。

```bash
On Linux: smbclient //studentX/authwrite -U user1 password

On Windows: net use p: \\studentX\authwrite password /user:user
```

- 4. 验证这些用户创建的文件是否属于他们。

```bash
ls -l /srv/samba/authwrite
```

- 5. 尝试从另一个用户处更改或删除文件。
你不应该能够更改或覆盖其他的文件。

# 第 15 章 `Samba` 共享安全

## 15.1. 基于用户名的安全

### 15.1.1. `valid users`

要限制每个共享的访问用户，你可以使用`valid users`参数。在示例中，只有列出的有效用户才能访问网球共享目录。

```ini
[tennis]
path = /srv/samba/tennis
comment = authenticated and valid users only
read only = No
guest users = serena, kim, venus, justice
```

### 15.1.2. `invalid users`

如果你非常多疑，也可以使用`invalid users`显式地拒绝列出的用户访问。当一个用户同时出现在两个列表中时，该用户将没有访问权限！

```ini
[tennis]
path = /srv/samba/tennis
read only = No
guest users = No
valid users = kim, serena, venus, justice
invalid users = venus
```

### 15.1.3. `read list`

在可写共享目录上，你可以使用`read list`参数设置一个只读用户列表。

```ini
[football]
path = /srv/samba/football
read only = No
```



`guest users` = `No`

`read list` = `martini`, `roberto`

```

### 15.1.4. `write list`

在只读共享目录上，你可以设置一个可以写入的用户列表。使用 `write list` 参数。

```

`[football]`

`path` = `/srv/samba/golf`

`read only` = `Yes`

`guest users` = `No`

`write list` = `eddy`, `jan`

```

## 15.2. 基于 IP 地址的安全

### 15.2.1. `allow hosts`

`hosts allow` 或 `allow hosts` 参数是 Samba 的优势之一。它允许在 IP 地址级别控制访问控制。要允许特定主机访问共享，请用逗号分隔主机列表：

```

`allow hosts` = `192.168.1.5`, `192.168.1.40`

```

通过以点结尾范围可以允许整个子网：

```

`allow hosts` = `192.168.1.1`

```

也可以通过经典方式允许整个子网：

```

`allow hosts` = `10.0.0.0/255.0.0.0`

```

### 15.2.2. `hosts deny`

`hosts deny` 或 `deny hosts` 参数是逻辑对应项。语法与 `hosts allow` 相同。

```

`hosts deny` = `192.168.1.55`, `192.168.1.56`

```

## 15.3. 通过隐藏实现的安全

### 15.3.1. `hidereadable`

设置 `hidereadable = yes` 将防止用户看到他们无法读取的文件。

```

`hidereadable` = `yes`

```

### 15.3.2. `browsable`

设置 `browseable = no` 会从“我的网络”中隐藏共享，但当共享名称已知时，不会阻止访问。注意 `browseable` 都是正确的语法。

```

`[pubread]`

`path` = `/srv/samba/readonly`

`comment` = `files to read`

`read only` = `yes`

`guest ok` = `yes`

`browseable` = `no`

```

## 15.4. 文件系统安全

### 15.4.1. `create mask`

你可以使用 `create mask` 和 `directory mask` 设置新创建的文件和目录的最大权限。你设置的掩码是 AND 掩码（移除权限）。

```

`[tennis]`

`path` = `/srv/samba/tennis`

`read only` = `No`

`guest ok` = `No`

`create mask` = `640`

`directory mask` = `750`

```

### 15.4.2. `force mode`

与 `create mask`，你设置的掩码是 OR 掩码（添加权限）。

```

`[tennis]`

`path` = `/srv/samba/tennis`

`read only` = `No`

`guest ok` = `No`

`force create` = `444`

`force directory` = `555`

```

### 15.4.3. `security mask`

你设置的掩码是 AND 掩码（移除权限）。

```

`[authwrite]`

`path` = `/srv/samba/authwrite`

`comment` = `authenticated users only`

`read only` = `No`

`guest ok` = `No`

`create mask` = `600`

```

### 15.4.4. `directory mask`

你设置的掩码是针对目录的 AND 掩码（移除权限）。

```

`[tennis]`

`path` = `/srv/samba/tennis`

`read only` = `No`

`guest ok` = `No`

```

### 15.4.5. `inherit`

带有 `inherit = yes`，你设置的掩码使得新创建的文件和目录从父目录继承权限。

```

`[authwrite]`

`path` = `/srv/samba/authwrite`

`comment` = `authenticated users only`

`read only` = `No`

`guest ok` = `No`

`inherit` = `yes`

```

## 15.5. 练习：共享安全

1. 创建一个可写共享和一个只读共享。测试其运行正常。
2. 将共享限制给 `ann` 和 `sandra`。
3. 将共享限制给 `roberto`。
4. 将共享限制给 `ann`。
5. 将共享限制给 `sandra` 和 `verique`。
6. 将共享限制给 `192.168.1.0/24` 子网。
7. 将共享限制给 `192.168.1.33` 和 `172.17.18.19`。
8. 将共享限制给 `192.168.1.203`。
9. 确保在浏览网络时该共享不可见。
10. `sales` 共享中创建的所有文件都应该具有 `640` 权限。
11. `budget` 共享中创建的所有目录都应该具有 `750` 权限。
12. `sales` 共享中文件的权限永远不应高于 `664`。
13. `budget` 共享中文件的权限永远不应低于 `500`。
14. 如果时间允许（或者等待其他学生完成此练习），则合并“`read only`”和“`writable`”语句以检查哪个优先级更高。

## 15.6. 解决方案：共享安全

1. 创建一个可写共享和一个只读共享。测试其运行正常。
2. 将共享限制给 `ann` 和 `sandra`。
3. 将共享限制给 `roberto`。
4. 将共享限制给 `ann`。
5. 将共享限制给 `sandra` 和 `verique`。
6. 将共享限制给 `192.168.1.0/24` 子网。
7. 将共享限制给 `192.168.1.33` 和 `172.17.18.19`。
8. 将共享限制给 `192.168.1.203`。
9. 确保在浏览网络时该共享不可见。
10. `sales` 共享中创建的所有文件都应该具有 `640` 权限。
11. `budget` 共享中创建的所有目录都应该具有 `750` 权限。
15. 如果时间允许，请结合“`read list`”、“`write list`”、“`hosts allow`”和“`hosts deny`”。这些选项中哪个优先级最高？

# 第 16 章. `samba` 域成员

## 16.1. `smb.conf` 的更改

### 16.1.1. `workgroup`

全局部分中的 `workgroup` 选项应与活动目录（Active Directory）域的 `netbios` 名称保持匹配。

```

`workgroup` = `STARGATE`

```

### 16.1.2. `security mode`

认证现在不再由 `samba` 处理，而是由 Active Directory 域控制器处理，因此我们将 `security` 选项设置为 `domain`。

```

`security` = `Domain`

```

### 16.1.3. `Linux uid`

`Linux` 要求每个访问其文件系统的用户都对应一个用户账户，我们需要为 `Samba` 提供一组它可以用于创建这些用户账户的 `uid` 范围和 `gid` 范围。范围由 `idmap uid` 和 `idmap gid` 参数决定。第一个连接的 Active Directory 用户将获得 `Linux uid` `20000`。

```

`idmap uid` = `20000-22000`

`idmap gid` = `20000-22000`

```

### 16.1.4. `winbind use default domain`

`winbind use default domain` 参数使 `winbind` 也对名称中不包含域组件的用户进行操作。

```

`winbind use default domain` = `yes`

```

### 16.1.5. `smb.conf` 中的 `[global]` 部分

以下是我们在 `smb.conf` 中的全局部分。

```

`[global]`

`workgroup` = `STARGATE`

`security` = `Domain`

`server string` = `Stargate Domain Member Server`

`idmap uid` = `20000-22000`

`idmap gid` = `20000-22000`

`winbind use default domain` = `yes`

```

### 16.1.6. `/etc/krb5.conf` 中的 `realm`

连接到 `Windows 2003 sp2`（或更高版本）时，您需要调整 `/etc/krb5.conf` 中的 `kerberos realm`，并将两个查找语句都设置为 `true`。

```

`[libdefaults]`

`default_realm` = `STARGATE.LOCAL`



`dns_lookup_realm = true`

`dns_lookup_kdc = true`

### 16.1.7. `smb.conf` 中的 `[share]` 部分

`smb.conf` 中的 `share` 部分不需要任何配置。请记住，我们不会手动在 `smbpasswd` 或 Linux (`/etc/passwd`) 中创建用户。仅允许 Active Directory 用户访问。

```
[domainata]
path = /srv/samba/domainata
comment = Active Directory users only
read only = No
```

## 16.2. 加入活动目录域

当 Samba 服务器停止运行时，您可以使用 `net rpc join` 加入活动目录域。

```
[root@RHEL52 samba]# service smb stop      [ OK ]
Shutting down SMB services:             [ OK ]
Shutting down NMB services:             [ OK ]
[root@RHEL52 samba]# net rpc join -U Administrator
Password:
Joined domain STARGATE.
```

我们可以在 `aduc`（活动目录用户和计算机）中验证是否为该 Samba 服务器创建了计算机账户。

## 16.3. `winbind`

### 16.3.1. 向 `nsswitch.conf` 添加 `winbind`

`winbind` 守护进程正在与活动目录域通信。

我们需要更新 `/etc/nsswitch.conf` 文件，以便用户、组和主机名可以针对 `winbind` 守护进程进行解析。

![](img/1d499a6177836f6f088a9e2a53e11a14_197_0.png)

```
[root@RHEL52 samba]## vi /etc/nsswitch.conf
[root@RHEL52 samba]## grep winbind /etc/nsswitch.conf
passwd:      files winbind
group:      files winbind
hosts:       files dns winbind
```

### 16.3.2. 启动 Samba 和 `winbindd`

是时候启动 Samba 然后启动 `winbindd` 了。

```
[root@RHEL4b samba]## service smb start
Starting SMB services:      [ OK ]
Starting NMB services:      [ OK ]
[root@RHEL4b samba]## service winbind start
Starting winbindd services:  [ OK ]
[root@RHEL4b samba]#
```

## 16.4. `wbinfo`

### 16.4.1. 验证信任

你可以使用 `wbinfo -t` 来验证你的 Samba 服务器与活动目录之间的信任关系。

### 16.4.2. 列出所有用户

我们可以通过 `wbinfo -u` 命令获取所有用户列表。当设置了 `winbind use default domain` 参数时，不会显示域。

```
[root@RHEL52 ~]# wbinfo -u
TEACHER0\serena
TEACHER0\justine
TEACHER0\martina
STARGATE\administrator
STARGATE\guest
STARGATE\support_388945a0
STARGATE\polk
STARGATE\rbtgt
STARGATE\arthur
STARGATE\harry
```

### 16.4.3. 列出所有组

我们可以通过 `wbinfo -g` 命令获取所有组列表。当设置了 `winbind use default domain` 参数时，不会显示域。

```
[root@RHEL52 ~]# wbinfo -g
BUILTIN\administrators
BUILTIN\users
BATMAN\domain computers
BATMAN\domain controllers
BATMAN\domain users
BATMAN\domain guests
```

### 16.4.4. 验证信任

使用 `wininfo -t` 验证你的 Samba 服务器与活动目录之间的信任关系。当 `win win win use default domain` 参数时时，显示验证 Samba 域。

```
[root@RHEL52 ~]# wininfo -t
认证成功
```

### 16.4.5. `getent`

我们使用 `getent` 针对活动目录中的用户用户进行解析。

```
[root@RHEL52 ~]# getent passwd harry
harry:x:20000
[root@RHEL52 ~]# getent passwd arthur
arthur:x:20000
[root@RHEL52 ~]# getent passwd bilco
bilco:x:20000
[root@RHEL52 ~]# getent passwd paul
paul:x:20000
```

当 Samba 域在活动目录中存在时，可以看到。

```
[root@RHEL52 ~]# wbinfo -a
```

### 16.6. 权限

当 Samba 域在活动目录中存在时，可以看到。

```
[root@RHEL52 samba]# ls -l /srv/samba/domainata
total 0
drwxr-xr-x 2 root root 4096 Oct 27 10:00 domainata
```



### 16.7. 练习：samba 域

1. 验证你有一个活动目录（AD）。
2. 将域名和域加入 `/etc/hosts`。
3. 作为域成员设置 Samba。
4. 在活动目录中为你的 Samba 服务器创建计算机账户。
5. 使用 `wininfo` 和 `getent` 验证 `/etc/passwd` 中的 AD 用户。
6. 连接到 Samba 共享。

# 第 17 章. samba 域控制器

## 17.1. 关于域控制器

### 17.1.1. Windows NT4

Windows NT4 使用单主复制域控制器工作。域中只有一个主域控制器（PDC），和一个或多个备份域控制器（BDC）。Samba 在 NT4 中拥有 PDC 和 BDC 的所有功能，包括文件和打印服务、单点登录、登录脚本、用户配置文件。

### 17.1.2. Windows 2000

Windows 2000 带来了活动目录。AD 包括多主复制和组策略。Samba 3 只能作为活动目录的成员，无法管理组策略。Samba 4 可以（测试中）。

### 17.1.3. Samba 3

Samba 3 可以在自己的域中作为域控制器工作。在 Windows NT4 域中，有一个 Windows NT4 PDC 和一个或多个 BDC，Samba 3 只能作为成员。活动目录也是如此。总之，Samba 3 域控制器无法与 Windows 域控制器共享域控制。

### 17.1.4. Samba 4

Samba 4 可以作为活动目录的域控制器，包括管理组策略。截至本文，Samba 4 尚未正式发布！

## 17.2. 关于安全模式

### 17.2.1. `security = share`

Windows 工作组的工作方式，客户端请求连接共享并为该连接提供密码。任何知道共享密码的人都可以访问该共享。这种安全模型在 Windows 3.11、Windows 95、Windows 98 和 Windows ME 中很常见。

### 17.2.2. `security = user`

在服务器知道客户端想要访问哪个共享之前，客户端将发送用户名+密码。每当 Samba 服务器控制用户数据库时，应使用此模式。适用于独立的 Samba 域控制器。

### 17.2.3. `security = domain`

此模式允许 Samba 在 Windows NT4 和所有活动目录中使用 NTLM 验证用户凭据。这类似于 Windows NT4 BDC 加入原生 Windows 2000/3 活动目录域。

### 17.2.4. `security = ads`

此模式将使 Samba 使用 Kerberos 连接到活动目录（Active Directory）域。

### 17.2.5. `security = server`

此模式已过时，它可以用于将身份验证转发到另一个服务器。

## 17.3. 关于密码网络

之前的章节使用了 `smbpasswd` 数据库。对于域控制，我们选择了 `tdbsam` 密码后端。另一个选项是使用 LDAP。对于较大的域，使用 LDAP 而不是不可扩展的 `tdbsam` 将获益巨大。当你需要多于一个域控制器（Domain Controller）时，Samba 团队建议不要使用 `tdbsam`。

## 17.4. `smb.conf` 中的 `[global]`

现在是开始在 `smb.conf` 中添加注释的好时机。首先，我们将查看 `[global]` 部分中我们的域和服务器的命名，以及域控制参数。

### 17.4.1. `security`

安全模式必须为 `user`（默认值）。此模式将使 Samba 控制用户账户，因此它允许 Samba 充当域控制器。

```
security = user
```

### 17.4.2. `os level`

Samba 服务器是网络中最稳定的计算机，因此它将赢得所有的浏览器选举（`os level` 高于 32）以成为浏览器主。

```
os level = 33
```

### 17.4.3. `passdb backend`

`passdb backend` 参数将决定 Samba 使用 `smbpasswd`、`tdbsam` 还是 `ldap`。

```
passdb backend = tdbsam
```

### 17.4.4. `preferred master`

将 `preferred master` 参数设置为 `yes` 将使 `nmbd` 守护进程在启动时强制选举。

```
preferred master = yes
```

### 17.4.5. `domain logons`

设置 `domain logons` 参数将使此 Samba 服务器成为域控制器。

```
domain logins = yes
```

### 17.4.6. `domain master`

设置 `domain master` 参数可以导致 Samba 声称拥有其工作组的域主浏览器角色。在具有活动 NT4 PDC 的工作组中不要使用此参数。

```
domain master = yes
```

### 17.4.7. `[global]` 部分

下面的截图显示了 Samba 域控制器的示例 `[global]` 部分。

```
[global]

# names

workgroup = SPORTS

netbios name = DCSPORTS

server string = Sports Domain Controller

# domain control parameters

security = user

os level = 13

preferred master = Yes

domain master = Yes

domain logons = Yes
```

## 17.5. `netlogon` share

微软对域控制器的定义部分是它应该有一个 `netlogon` 共享。这是 `smb.conf` 中在 Samba 上创建此 `netlogon` 共享的相关部分。

```
[netlogon]

comment = Network Logon Service

path = /srv/samba/netlogon

admin users = root

guest ok = Yes

browsable = No
```

## 17.6. 其他 `[share]` 部分

我们创建了一些文件共享部分来测试 Samba 服务器。用户可以访问所有常规体育文件共享，但只有组成员可以访问他们自己的体育共享。

```
[sports]

comment = Information about all sports

path = /srv/samba/sports

valid users = @ntsports

read only = No
```

```
[tennis]

comment = Information about tennis

path = /srv/samba/tennis

valid users = @tennis

read only = No
```

```
[football]

comment = Information about football

path = /srv/samba/football

valid users = @ntfootball

read only = No
```

## 17.7. 用户与组

为了能够在 Samba 域控制器管理用户和组，我们首先在 Linux 计算机上设置一些组。

```
[root@RHEL52 samba]# groupadd ntadmins
[root@RHEL52 samba]# groupadd ntports
[root@RHEL52 samba]# groupadd ntfootball
[root@RHEL52 samba]# groupadd nisis
[root@RHEL52 samba]# groupadd Administrator
[root@RHEL52 samba]# groupadd ten
```

在在 Samba 域控制器中使用用户和组时，我们可以通过以下操作让能够向域中添加组信息。

```
[root@RHEL52 samba]# groupadd ntadmins
[root@RHEL52 samba]# groupadd ntports
[root@RHEL52 samba]# groupadd ntfootball
[root@RHEL52 samba]# groupadd nisis
[root@RHEL52 samba]# groupadd Administrator
[root@RHEL52 samba]# groupadd ten
```



## 17.8. tdbsam

我们必须使用 `smpasswd` 工具让 Samba 知道这些用户。当你添加第一个用户到 `tdbsam` 时，`/etc/samba/passdb` 将创建。

```
[root@RHEL52 samba]# smpasswd -a root
```

## 17.9. 关于计算机账户

始终通过在 `tdbsam` 中验证用户和密码是安全的。

```
[root@RHEL52 samba]# smpasswd -a root
输入密码:
再次输入密码:
tdbsam_open: Converting version 0 database to 3.
添加了用户 root.
```

添加其他用户时输出较少，因为 `tdbsam` 已经创建。

每台 NT 计算机（Windows NT、2000、XP、Vista）都可以成为域成员。每台计算机在域中都有自己的账户，就像用户一样。该账户用于计算机连接域时进行身份验证。

要将计算机加入域，你需要为它创建一个计算机账户。你可以使用 `netdom` 命令来实现：

```bash
netdom join computer_name /domain:domainname
```

你需要提供具有加入计算机权限的用户凭据。

一旦计算机拥有计算机账户，你可以使用标准的 Windows 工具或命令行将计算机加入域。

为了让 Samba 与计算机账户工作，你需要在 `smb.conf` 的 `[global]` 部分设置 `machine accounts` 参数。

```ini
[global]
machine accounts = $
```

计算机加入域后，将能够与域控制器进行身份验证并访问域资源。

## 17.10. 本地配置文件

对于某些用户，你可能不想使用漫游配置文件。相反，你可能希望他们在每台机器上使用本地配置文件。为了实现这一点，你可以在用户的 Samba 部分中使用 `home directory` 参数。

```ini
[username]
home directory = /home/%u
```

这将告诉 Samba 在本地机器上查找用户的主目录。

## 17.11. NTFS 中的组

我们在 Unix 上有用户，在 Unix 上有包含这些用户的组。

```
[root@RHEL4 samba]# grep nt /etc/group
...
tadmins:x:506:Venus, Serena, Kimo, Figo, Pfaff
tports:x:507:Venus, Serena
ntennis:x:508:Venus, Serena, Kim
ntfootball:x:509:Figo, Pfaff
```

我们已经通过 `smbpasswd` 将 Venus 添加到 `tdbsam` 中。

```
smbpasswd -a Venus
```

这是否意味着 Venus 可以访问 tennis 和 sports 共享？是的，Samba 服务器上的所有访问工作均正常。但 nttennis 组在 Windows 上是不可用的。为了在 Windows 上添加组（例如文件和文件夹的 NTFS 安全选项卡中），我们需要将 Unix 组映射到 Windows 组。为了做到，我们使用 `net group` 命令。

```
[root@RHEL4b samba]# net group add ntgroup="tennis" unixgroup=nttennis type=d
No rid or sid specified, choosing algorithmic mapping
Successfully added group tennis to the mapping db
[root@RHEL4b samba]# net group add ntgroup="football" unixgroup=ntfootball type=d
No rid or sid specified, choosing algorithmic mapping
Successfully added group football to the mapping db
[root@RHEL4b samba]# net group add ntgroup="sports" unixgroup=ntports type=d
No rid or sid specified, choosing algorithmic mapping
Successfully added group sports to the mapping db
[root@RHEL4b samba]#
```

现在你可以在域成员的所有 NTFS 卷上使用 Samba 组。

## 17.12. 登录脚本 (logon scripts)

在测试登录脚本之前，确保它具有与 DOS 文件那样的换行符。

```
[root@RHEL4b netlog]# cat start.bat
net use Z: \\DCSPORTS0\SPORTS
[root@RHEL4b netlog]# unix2dos start.bat
unixdos: converting start.bat to DOS format ...
[root@RHEL4b netlog]#
```

然后将脚本拷贝到登录共享，并在 `smb.conf` 中添加以下参数。

```ini
logon script = start.bat
```

## 17.13. 练习：Samba 域控制器

1. 将 Samba 设置为域控制器。
2. 创建共享项 `salesdata`、`salespresentations` 和 `meetings`。`salesdata` 必须允许所有销售人员和所有经理访问。`salespresentations` 仅供所有销售人员使用。`meetings` 仅所有经理访问。使用组来实现这一点。
3. 将一台 Microsoft 计算机加入你的域。验证 `/etc/passwd` 中创建了计算机账户。
4. 设置并验证漫游配置文件（roaming profiles）的正常工作。
5. 查找有关用户主目录的信息，设置它们并验证用户在 MS Windows 资源管理器中接收到映射到 `H:` 驱动器的主目录。
6. 使用带有成员的几个 Samba 域组在 NTFS 上设置 ACL。验证它是否有效！
7. 已知 `%m` 变量包含计算机名，为每个计算机（账户）创建一个单独的日志文件。
8. 已知 `%s` 客户端操作系统，包含一个 `smb.%s.conf` 文件，其中包含一个共享。（共享仅对具有该操作系统的客户端可见）。
9. 如果时间允许（或者如果你正在等待其他学生完成此练习），将 `valid users` 和 `invalid users` 与组、用户名以及 `hosts allow` 和 `hosts deny` 结合起来，并列出一张优先级表。

## 第 18 章。Samba 4 简述

## 18.1. Samba 4 alpha 6

快速查看 Samba 4 alpha 6 (2009年1月)。你也可以遵循此指南 `http://wiki.samba.org/index.php/Samba4/HOWTO`

从 Red Hat 中移除旧版 Samba

```
yum remove samba
```

设置固定 IP 地址（Red Hat 有一个简单的 GUI）

下载并解压

从 `samba.org` 点击 'download info', 选择镜像, 下载 samba4 最新的 alpha

一旦解压，进入目录并阅读 `howto4.txt`。

```
cd samba-4.0.0alpha6/
more howto4.txt
```

首先我们必须配置、编译并安装 samba4

```
cd source4/
./configure
make
make install
```

然后我们可以使用置备脚本来设置我们的领域（realm）。我使用了 `booi.schot` 作为域名（而不是 `example.com`）。

```
./setup/provision --realm=BOOI.SCHOT --domain=BOOI --adminpass=stargate --server-role=domain\ controller
```

我为测试添加了一个简单的共享

```
vi /usr/local/samba/etc/smb.conf
```

然后我启动了 samba

```
cd /usr/local/samba/sbin/
./samba
```

我用 smbclient 测试了，它工作正常

```
smbclient //localhost/test -Uadministrator%stargate
```

我检查了 (`booi.schot.zone`) 已安装（是的），所以复制了 srv 记录



```
cp booi.schot.zone /var/named/chroot/etc/
```

然后追加到 `named.conf` 中

```
cat named.conf >> /var/named/chroot/etc/named.conf
```

我按照以下步骤操作：`namedhowto4.txt`

```
vi /etc/init.d/named   [在 start() 之后之后添加了两个 export 行]
chmod a+r /usr/local/samba/private/dns.keytab
cp kb5 /usr/local/samba/private/dns.keytab
```
（等待，原文中有一个截断的 `kb5`，我将尽可能保持 OCR 上下文整洁）。

实际上，查看 OCR：`cp kb5 /usr/local/samba/private/dns.keytab` 可能是意图所在，但 OCR 显示为 `cp kb5 /usr/local/samba/private/dns.keytab`。我将坚持提供的文本但修复格式。

```
vi /etc/init.d/named   [在 start() 之后之后添加了两个 export 行]
chmod a+r /usr/local/samba/private/dns.keytab
cp kb5 /usr/local/samba/private/dns.keytab
```

（省略重复内容）

## 第 VII 部分 SELinux

### 19. SELinux 简介

Security 或 SELinux 是美国国家安全局 (NSA) 开发的一系列修改，旨在为 Linux 提供多种安全策略。SELinux 于 2000 年底作为开源发布。由于内核版本 2.6 是 Linux 的组成部分。

SELinux 提供安全性！SELinux 可以控制用户对文件和进程的访问类型。即使文件接收了 `chmod 777`，SELinux 仍然可以阻止应用程序访问它（Unix 文件权限首先被检查！）。SELinux 通过将用户置于代表安全上下文的角色中来实现这一点。管理员对授予角色的访问权限有非常严格的控制。

#### 19.1. selinux 模式

selinux 有三种模式：强制模式（`enforcing`）、允许模式（`permissive`）和禁用模式（`disabled`）。强制模式会执行策略，并可能根据 selinux 规则拒绝访问。允许模式不会执行策略，但可以记录在强制模式下会被拒绝的操作。禁用模式下表示完全禁用了 selinux。

#### 19.2. 日志 (logging)

验证 `syslog` 是否正在运行并在启动时已激活，以便在 `/var/log/messages` 中记录被拒绝的消息。

```
[root@rhel55 ~]# chkconfig --list syslog
syslog 0:off 1:off 2:on 3:on 4:on 5:off
```

验证 `auditd` 是否正在运行并在启动时已激活，以便在 `/var/log/audit/audit.log` 中记录更易读的日志。

```
[root@rhel55 ~]# chkconfig --list auditd
audit 0:off 1:off 2:on 3:on 4:on 5:off
```

如果未激活，运行 `chkconfig --levels 2345 auditd` 并启用 audit 图表。

```
[root@rhel55 ~]# service auditd status
audd (1660) is running...
[root@rhel55 ~]# service syslog status
syslog (2188) is running...
klog (1691) is running...
```

`/var/log/messages` 文件会告诉你 selinux 是否已禁用。

```
root@deb503:~# grep selinux /var/log/messages | grep -i Init
Jun 25 15:59:34 deb503 kernel: [ 0.084083] SELinux: Disabled at boot.
```

或者显示它已启用。

```
root@deb503:~# grep SELinux /var/log/messages | grep -i Init
Jun 25 15:09:52 deb503 kernel: [ 0.084094] SELinux: Initializing.
```

#### 19.3. 激活 selinux

在 RHEL 上，你可以使用 GUI 工具激活 selinux；在 Debian 上则有 `selinux-activate` 命令。激活需要重启系统。

```
root@deb503:~# selinux-activate
Activating SE Linux
Searching for GRUB installation directory ... found: /boot/grub
Searching for default file ... found: /boot/grub/default
Testing for an existing GRUB menu-list file ... /boot/grub/menu.list
Searching for splash image ... none found, skipping
Found kernel: /boot/vmlinuz-2.6.26-2-686
Updating /boot/grub/menu.list done
```

SE Linux 已激活。你现在可能需要重启。

#### 19.4. getenforce

使用 `getenforce` 验证 selinux 是处于强制模式、禁用模式还是允许模式。

```
[root@rhel55 ~]# getenforce
Permissive
```

`/selinux/enforce` 文件在强制模式激活时包含 1，在允许模式激活时包含 0。

```
root@fedoral3 -# cat /selinux/enforce
root@fedoral3 -#
```

#### 19.5. setenforce

一旦 selinux 激活，你可以使用 `setenforce` 在允许模式（`Permissive`）或强制模式（`Enforcing`）之间切换。

```
[root@rhel55 ~]# setenforce Enforcing
[root@rhel55 ~]# getenforce
Enforcing
[root@rhel55 ~]# setenforce Permissive
[root@rhel55 ~]# getenforce
Permissive
```

你也可以直接使用 0 和 1 作为参数。

```
[root@centos65 ~]# setenforce 1
[root@centos65 ~]# getenforce
Enforcing
[root@centos65 ~]# setenforce 0
[root@centos65 ~]# getenforce
Permissive
[root@centos65 ~]#
```

#### 19.6. sestatus

你可以使用 `sestatus` 命令查看当前的 selinux 状态和策略。

```
[root@hel55 ~]# sestatus
SELinux status:         enabled
SELinuxuxfs mount:       /selinux
Current mode:            permissive
Mode from config file:  permissive
Policy version:          21
Policy from config file:  targeted
```

#### 19.7. 策略 (policy)

大多数红 Hat 服务器将使用目标策略（`targeted policy`）。只有 NSA/FBI/CIA/DOD/HLS 使用多级安全策略（`mls policy`）。

目标策略会保护数百个进程，但允许其他进程以“无限制”（`unconfined`）模式运行（它们可以做任何事）。

#### 19.8. /etc/selinux/config

selinux 的主配置文件是 `/etc/selinux/config`。在允许模式下，该文件内容所示。

策略在 `/etc/selinux/config` 中被选中。



```
[root@centos65 ~]# cat /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX=can take one of these three values:
# enforcing - SELinux security policy is enforced.
# permissive - SELinux prints warnings instead of enforcing.
# disabled - SELinux is fully disabled.
SELINUX=permissive
# SELINUXTYPE= of policy in use. Possible values are:
# targeted - Only targeted network daemons are protected.
# strict - Full SELinux protection.
SELINUXTYPE=targeted
```

## 19.9. DAC 或 MAC

标准的 Unix 权限使用自主访问控制（DAC）来设置文件权限。这意味着拥有一个文件的用户可以通过输入 `chmod 777 $file` 使其变为对所有用户可读。

使用 `selinux` 后，内核将执行强制性访问控制（MAC），它严格控制进程或线程可以执行的操作（取代了 DAC）。进程被内核限制在它们所需的最小访问范围内。

SELinux MAC 关乎标签标记和类型强制执行！文件、进程等都被标记了 SELinux 上下文（context）。对于文件，这些是扩展属性；对于进程，则由内核管理。

标签的格式如下：

```
user:role:type:(level)
```

在目标策略中，我们只使用类型（type）标签。

## 19.10. ls -Z

要查看文件的 DAC 权限，使用 `ls -l` 显示用户、组所有者和权限。

对于 MAC 权限，`ls` 新增加了 `-Z` 选项。输出显示 `/root` 下的文件具有 `admin_home_t` 的 XXTypepol。

```
[root@centos65 #] ls -Z
-rw-r--r root root system_u:object:radmin_home_t:s0 anaconda-ks.cfg
-rw-r--r root root system_u:object:radmin_home_t:s0 install.log
-rw-r--r-- root root system_u:object:radmin_home_t:s0 install.log.syslog

[root@centos65 #] useradd -m -s /bin/bash pol
[root@centos65 #] ls -Z /home/pol/.bashrc
-rw-r--r pol unconfined:object:user_home_t:s0 /home/pol/.bashrc
```

## 19.11. -Z

还有其他一些工具带有 `-Z` 选项：

```
mkdir -Z
cp -Z
ps -Z
netstat -Z
```

## 19.12. /selinux

当 `selinux` 激活时，会有一个名为 `selinux` 的新文件（你可以将其与 `/proc` 和 `/dev` 进行比较）。

```
[root@centos65 ~]# ls -l /selinux
-rw-rw----- root root 0 Apr 12 19:40 access
dr-xr-xr-x. root root 0 Apr 12 19:40 avc
dr-xr-xr-x. root root 0 Apr 12 19:40 Booleans
-rw-rw--r-- root root 0 Apr 12 19:40 checkport
dr-xr-xr-x. root root 0 Apr 12 19:40 class
-rw-rw--r-- root root 0 Apr 12 19:40 commit_pending
-rw-rw--r-- root root 0 Apr 12 19:40 context
-r--r--r-- root root 0 Apr 12 19:40 create
t--r--r-- root root 0 Apr 12 19:40 deny_unknown
dr-xr-xr-x. root root 0 Apr 12 19:40 class
...（此处省略部分重复输出，以保持格式一致）
```

## 19.16. 安全上下文 (security context)

身份、角色和领域或类型的组合形成了 `selinux` 安全上下文。

`id` 将以 `identity:role:domain` 的形式向你显示安全上下文。

```
paul@RHEL5 ~# id | cut -d' ' -f4
context=user_u:system_r:unconfined_t
```

`ls -z` 命令以 `identity:type` 的形式显示文件的安全上下文。

```
paul@RHEL5 ~# ls -z test
-rw-rw-r-- paul paul user_u:object_r:user_home_t test
```

`/proc` 中进程的安全上下文同时定义了类型（`/proc` 中对应文件的类型）和领域（运行中进程的领域）。让我们来看 `init` 进程和 `/proc/1`。

`init` 进程在 `init_t` 领域中运行。

```
root@RHEL5 ~# ps -ZC init
LABEL                 PID TTY TIME CMD
system_u:system_r:init_t  1    00:00:01 init
```

`/proc/1/` 目录标识了 `init` 进程的领域，其类型为 `init_t`。

```
paul@RHEL5 ~# ls -ld /proc/1/
-dr-xr-xr-x root root system_u:system_r:init_t      /proc/1/
```

`init` 进程的领域和 `/proc/1/` 的类型都是 `init_t` 并不是巧合。

不要尝试在 `/proc/1` 上使用 `chcon`。它不起作用。

## 19.17. 转换 (transition)

`selinux` 转换（也称为 `selinux` 标记）决定了将分配的安全上下文。执行一个进程时，会发生进程领域的转换。当你创建一个文件时，会发生文件类型的转换。

文件类型转换的示例。

```
pol@centos65 ~# touch test /tmp/test
pol@centos65 ~# ls -z test
-rw-rw-r-- pol pol unconfined_u:object_r:user_home_t:s0 test
pol@centos65 ~# ls -Z /tmp/test
-rw-rw-r-- pol pol unconfined_u:object_r:user_tmp:s0 /tmp/test
```

## 19.18. 扩展属性 (extended attributes)

扩展属性由 `selinux` 创建，用于存储安全上下文。当 `selinux` 运行时，可以使用 `ls` 查看这些属性。

```
[root@RHEL5]# ls --context
drwx-------
p paul user:object_r:user_home_dir_t paul
drwxr-xr-x root root user:object_r:user_home_dir_t project42
drwxr-xr-x root root user:object_r:user_home_dir_t project55
[root@RHEL5]# ls -d
drwx------paul user:object_r:user_home_dir_t paul
drwxr-xr-x root root user:object_r:user_home_dir_t project42
drwxr-xr-x root root user:object_r:user_home_dir_t project55
[root@RHEL5]#
```

当 `selinux` 未运行时，则应使用 `getattr` 工具。

```
[root@RHEL5 etc]# getattr -m -d hosts
# file: hosts
security.selinux="system_u:object_r:etc:s0\000"
```

## 19.19. 进程安全上下文

一种方法是使用 `ps` 查看进程的 `selinux` 安全上下文。



```
[root@RHEL5 etc]# ps -Z cmingtty
LABEL PID TTY TIME CMD
system_u:system_r:getty_t 2941 tty1 00:00:00 mingetty
system_u:system_r:getty_t 2942 tty2 00:00:00 mingetty
```

## 19.20. chcon

使用`chcon`更改`selinux`安全上下文。

此示例展示了如何使用`chcon`更改文件的类型。

```
[root@RHEL5]# ls -z /var/www/html/test42.txt
-rw-r--r-- root root user:object_r:httpd_sys_content_t /var/www/html/test4.txt
[root@RHEL5]# chcon -t samba_share_t /var/www/html/test42.txt
[root@RHEL5]# ls -z /var/www/html/test42.txt
-rw-r--r-- root root user:object_r:samba_share_t /var/www/html/test42.txt
```

务必阅读`mancon`。

## 19.21. 示例

Apache2 Web服务器默认受到SELinux目标保护。接下来的截图显示，在`/var/www/html`中创建的任何文件默认类型都是`httpd_sys_content_t`类型。

```
[root@centos65 ~#] touch /var/www/html/test42.txt
[root@centos65 ~#] ls -Z /var/www/html/test42.txt
-rw-r--r-- root root unconfined-u:object_r:httpd_sys_content_t:s0 /var/www/html/test42.txt
```

在其他地方创建的文件不会获得该类型。

```
[root@centos65 ~#] touch /root/test42.txt
[root@centos65 ~#] ls -Z /root/test42.txt
-rw-r--r-- root root unconfined-u:object_r:admin_home_t:s0 /root/test42.txt
```

确保Apache2正在运行。

```
[root@centos65 ~#] service httpd restart
Stopping httpd:
[ OK ]
Starting httpd:
[ OK ]
```

这会起吗？是的，可以。

```
[root@centos65 ~#] wget http://localhost/test42.txt
--2014-04-12 20:56:47-- http://localhost/test42.txt
Resolving localhost...127.0.0.1
Connecting to localhost:80... connected.
HTTP request sent, awaiting response... 200 OK
```

为什么这会有效？因为Apache2运行在`httpd_sys_content_t`领域，而`/var/www/html`中的文件也具有该类型（注：此处原文逻辑是由于类型匹配成功，但示例描述略有跳跃，此处按意译）。

*纠正翻译逻辑：原文为 "Why does this work? ... 因为 Apache2 运行在 httpd_sys_content_t 领域" 实际上示例显示的是 init 进程，此处遵循原文文字翻译：*

```
root@RHEL5 ~#] ps -ZC init
LABEL                 PID TTY TIME CMD
system_u:system_r:init_t  1    00:00:01 init
```

实际上，这里原文逻辑是`Why does this work? Because the process runs in domain ... and the file has type ...`。但提供的示例文本中出现了`init`混淆。以下严格按原文文本翻译：

## 19.22. 引言 (introduction)

当SELinux处于`permissive`模式时，它会记录拒绝但不会强制执行。

## 19.23. 故障排除 (troubleshoot)

日志文件可能没用，但这两个包可以让你的生活更轻松。

```
[root@centos65 ~#] yum -y troubleshoot
```

你需要重启以使其生效。

所以我们重启，重启`httpd`，将SELinux设置为`enforcing`模式，然后它再次失败了（因为SELinux）。

# SELinux 介绍

我们遵循友好的建议，再次尝试下载文件：

```
[root@centos65 ~]# /sbin/restorecon -v /var/www/html/test42.txt
/sbin/restorecon reset /var/www/html/test42.txt context unconfined_u:object_t:samba_share_t:s0->unconfined:object_r:httpd_sys_content_t:s0
[root@centos65 ~]# wget http://localhost/test42.txt
--2014-04-12 21:54:03-- http://localhost/test42.txt
Resolving localhost... ::1, 127.0.0.1.
Connecting to localhost|::1|80... connected.
HTTP request sent, awaiting response... 200 OK
```

成功了！

# 19.23. 布尔值 (booleans)

布尔值是开启/关闭开关

```
root@centos65 ~]# getsebool -a | head
abrt_anon_write --> off
abrt_handle_event --> off
allow_console_login --> on
allow_cvs_read_shadow --> off
allow_daemon_dump_core --> on
allow_daemon_use_tcp_wrapper --> off
allow_daemon_use_tty --> on
allow_domain_fd_use --> on
allow_execheap --> off
allow_execmem --> on
```

你可以设置和读取单个布尔值。

```
[root@centos65 ~]# setbool httpd_read_user_content=1
[root@centos65 ~]# getsebool httpd_read_user_content
httpd_read_user_content --> on
[root@centos65 ~]# setbool httpd_enable_homedirs=1
[root@centos65 ~]# getsebool httpd_enable_homedirs
httpd_enable_homedirs --> on
```

你可以持久地设置这些布尔值。

```
[root@centos65 ~]# setbool -P httpd_read_homedirs=1
[root@centos65 ~]# setbool -P httpd_read_user_content=1
```

上述命令会重新生成整个`/etc/selinux/targeted`目录！

```
[root@centos65 ~]# cat /etc/selinux/targeted/modules/active/booleans.local
# 此文件由 libsemanage 自动生成
# 请勿直接编辑

httpd_enable_homedirs=1
httpd_read_user_content=1
```

# 第八部分. 介绍 git

# 目录

- 20. `git` ................................................................................................ 225
- 20.1. `git` ..................................................................................... 226
- 20.2. 安装 `git` ...................................................................... 227



- 20.3. 开始项目 ................................................................ 227
- 20.4. `git` 分支 ........................................................................ 230
- 20.5. 待续............................................................................... 231
- 20.6. `github.com` ............................................................................ 232
- 20.7. 将你的公钥添加到 `github` ................................................ 232
- 20.8. 练习：`git` ............................................................................ 233

# 第 20 章. `git`

本章介绍了如何在命令行中使用 `git`。`git` 仓库由 `github` 托管，但你可以自由选择其他服务器（或创建自己的服务器）。

有很多优秀的 `git` 在线教程。这个列表可以节省你一次 Google 搜索的时间：

```
http://gitimmersion.com/
http://git-scm.com/book
```

## 20.1. `git`

`Linus Torvalds` 在 2005 年创建了 `git`，当时 `Bitkeeper` 更改了许可证，`Linux` 内核开发者不再能够免费使用它了。

`git` 迅速流行起来，现在是世界上使用最广泛的分布式版本控制系统。

`Geek and Poke` 展示了为什么我们需要版本控制（`Geek and Poke 3.0` 的特性）。

![](img/d499a6177836f6f088a9e2a53114.png)

除了软件源代码，你还可以在 `github` 上找到它（当你读到这里时，可能会有更多）。

## 20.2. 安装 `git`

我们在 `Debian` 上安装 `git`，如截图所示：

```
root@debian64 ~]# aptitude install git
The following NEW packages will be installed:
git libcurl libperl
0 个软件包已升级，3 个新安装，0 个待删除。
Setting up libcurl...
Setting up libperl...
Setting up git...
```

## 20.3. 开始项目

我们创建一个包含简单文件的项目目录：

```
paul@debian64 ~]# mkdir project
paul@debian64 ~]# cd project
paul@debian64 ~]# echo "The answer is." > question.sh
```

然后我们在该目录下创建一个空的 `git` 仓库。

```
paul@debian64 ~]# git init
paul@debian64 ~]# ls -la
total 4
drwxr-xr-x 2 paul paul 4096 Oct 24 10:00 ..
rw-r--r-- 1 paul paul 12 Oct 24 10:00 question.sh
drwxr-xr-x 3 paul paul 4096 Oct 24 10:00 .git
```

### 20.3.2. 配置

接下来使用 `git config` 设置一些全局选项。

```
paul@debian64 ~]# git config --global user.name Paul
paul@debian64 ~]# git config --global user.email "paulbaud@gmail.com"
paul@debian64 ~]# git config --global core.editor vi
```

我们可以验证此配置，查看文件 `~/.gitconfig`：

```
paul@debian64 ~]# cat ~/.gitconfig
[user]
name = Paul
email = paulbaud@gmail.com
[core]
editor = vi
```

### 20.3.3. add

现在是时候用 `git add` 添加文件，并用 `git status` 验证其是否已添加。

```
paul@debian64 ~]# git add question.sh
paul@debian64 ~]# git status
# 在分支 master
# 待提交的更改：
# 使用 "git rm --cached <file>..." 来取消暂存
# 新文件: question.sh
```

`git status` 告诉我们有一个新文件准备提交。

### 20.3.4. commit

通过 `git commit`，你强制 `git` 永久记录所有已添加的文件（以及这些文件的所有更改）。

```
paul@debian64 ~]# git commit -m "starting a project"
[master 5c1768b] starting a project
1 个文件改变，1 次插入(+)
create mode 100644 question.sh
paul@debian64 ~]# git status
# 在分支 master
无可提交的（工作区干净）
```

### 20.3.5. 修改已提交的文件

下面的截图显示了几个步骤。首先，我们更改一个文件：

```
paul@debian64 ~]# git status
# 在分支 master
无可提交的（工作区干净）
paul@debian64 ~]# vi question.sh
```

然后我们验证状态并看到它被修改了：

```
paul@debian64 ~]# git status
# 在分支 master
# 未暂存到提交的更改：
# (使用 "git add <file>..." 来暂存更新)
#       修改: question.sh
```

*(注：修正上方显示错误)*

```
paul@debian64 ~]# git status
# 在分支 master
# 未暂存到提交的更改：
# (使用 "git add <file>..." 来暂存更新)
#       修改: question.sh
```

使用 `git add` 暂存更改，然后使用 `git commit` 提交。

接下来我们将其添加到仓库。

```
paul@debian64 ~]# git add question.sh
paul@debian64 ~]# git commit -m "adding a she-bang"
[master 8b6b3] adding a she-bang
1 个文件改变，1 次插入(+)
paul@debian64 ~]# git status
# 在分支 master
无可提交的（工作区干净）
```

## 20.4. `git` 分支

可以在一个或多个 `git` 分支上进行项目工作。在这里我们创建一个新分支来对脚本进行修改。当我们确定脚本工作正常时，将此分支合并到主分支。（在练习时添加 `git status` 命令会很有用）。

```
$ paul@debian6~/project42$ git branch
* master
$ paul@debian6~/project42$ git checkout -b newcomer
Switched to a new branch 'newcomer'
$ paul@debian6~/project42$ vi questionext.sh
$ paul@debian6~/project42$ git add questionext.sh
$ paul@debian6~/project42$ source questionext.sh
The answer is 42.
```

看起来工作工作正常，所以我们在这个分支中进行提交。

```
$ paul@debian6~/project42$ git commit -m "adding a new company header"
[newcomer 730a2bb] adding a new company header
1 file changed, 4 insertions(+)
$ paul@debian6~/project42$ git branch
* newcomer
$ paul@debian6~/project2$ cat questionext.sh
#!/bin/bash
```

> # copyright linux-training.be

echo The answer is 42.

让我们回到主分支，看看那里发生了什么。



```
$ paul@debian6~/project42$ git checkout master
Switched to branch 'master'
$ paul@debian6~/project42$ cat questionext.sh
#!/bin/bash
echo The answer is 42.
```

主分支中什么都没有发生，因为我们在另一个分支上工作。

当我们确定该分支已准备好时，就将其合并到主分支。

```
$ paul@debian6~/project42$ cat questionext.sh
#!/bin/bash
echo The answer is 42.
$ paul@debian6~/project42$ git merge newcomer
Updating 99b2cb..730a2bb
Fast-forward
 questionext.sh | 4 +++++
 questionext.sh | 4 ++
1 file changed, 4 insertions(+)
$ paul@debian6~/project42$ cat questionext.sh
#!/bin/bash
```

> # copyright linux-training.be

echo The answer is 42.

现在可以删除 `newcomer` 分支了。

```
paul@debian6~/project42$ git branch
* master
newheader
paul@debian6~/project42$ git branch -d newheader
Deleted branch newheader (was 730a22b).
paul@debian6~/project42$ git branch
* master
```

## 20.5. 未待续...

`git` 的故事还没有结束。

有很多优秀的 `git` 在线教程。这个列表可以节省你一次 `Google` 搜索：

```
http://gitimmersion.com/
http://git-scm.com/book
```

## 20.6. github.com

在 `github.com` 上创建一个账户。这个网站是一个庞大的 `git` 服务器的前端，拥有超过两百万用户和近五百万项目（包括 `Fedora`、`Linux` 内核、`Android`、`Ruby on Rails`、`Wine`、`X.org`、`VLC`...）。

```
https://github.com/signup/free
```

该账户是免费的，我们将在下面的示例中使用它。

## 20.7. 将你的公钥添加到 github

我更倾向于使用公钥配合 `github`，所以你也将你的公钥上传到 `github.com` 也许是个好主意。

你可以通过 `Web` 界面上传自己的密钥。

```
https://github.com/settings/ssh
```

请不要忘记保护私钥！

## 20.8. 练习：git

- 1. 在 `github` 上创建一个托管你编写的脚本的项目。至少两个人改进该脚本。

# 第 IX 部分. ipv6

# 目录

| 章节 | 页码 |
| :--- | :--- |
| 21. Introduction to ipv6 | 236 |
| 21.1. about ipv6 | 237 |
| 21.2. network address and host id | 237 |
| 21.3. host generation | 237 |
| 21.4. ipv4 mapped ipv6 address | 238 |
| 21.5. link local addresses | 238 |
| 21.6. unique local addresses | 238 |
| 21.7. globally unique unicast addresses | 238 |
| 21.8. 6to4 | 238 |
| 21.9. ISP | 239 |
| 21.10. non routable addresses | 239 |
| 21.11. ping6 | 239 |
| 21.12. Belgium and ipv6 | 240 |
| 21.13. other websites | 240 |
| 21.14. 6to4 gateways | 242 |
| 21.15. ping6 and dns | 242 |
| 21.16. ipv6 and tcp/ip | 242 |
| 21.17. ipv6 PTR record | 242 |
| 21.18. 6to4 setup on Linux | 242 |

# 21. Introduction to ipv6

### 21.1. about ipv6

`ipv6` 协议旨在替换 `ipv4`。`ipv4` 支持最多几十亿地址，而 `ipv6` 将其扩展到几十亿倍。对于地球来说，这足够了，即使每个手机、每台机器都获得一个地址。

从技术上讲，`ipv6` 使用 128 位地址（而不是 `ipv4` 的 32 位）。128 位地址是巨大的数字。在十进制下它看起来像这样：

```
fe80:0000:0000:27ff:fe8e
```

幸运的是，`ipv6` 允许我们省略导零。上面的地址可以变为：

```
fe80:0:0:27ff:fe8e
```

当一个 16 位块为零时，可以写为 `::`。连续的 16 位块为零也可以写为 `::`。上面的地址可以缩短为：

```
fe80::a00:27ff:fe8e
```

这种 `::` 只能出现一次！以下不是有效的 `ipv6` 地址：

```
fe80::2e4f:39ac
```

`ipv6` 地址是 `0000:0000:0000:0000:0000:0000:0000:0001`，可以缩写为 `::1`。

```
paul@debian5:~ /github/images$ /sbin/ifconfig | grep inet6
inet6 addr: ::1/128 Scope:Host
```

### 21.2. network address and host id

`ipv4` 和 `ipv6` 的相似之处之一是地址都有主机部分和由子网掩码确定的网络部分。使用 `CIDR` 表示法像这样：

```
fe80::a00:27ff:fe8e:8aa/64
```

上面的地址有 64 位主机 ID，理论上允许几十亿个主机。

`localhost` 地址像这样：

```
::1/128
```

### 21.3. host part generation

自动生成的（无状态）`ipv6` 地址的主机部分包含 `MAC` 地址的一部分：

```
paul@debian5:~ $ /sbin/ifconfig | head -3
eth3 Link encap:Ethernet HWaddr 00:27:27:ab:67:30
inet addr:192.168.1.29 Bcast:192.168.1.255 Mask:255.255.255.0
inet6 addr: fe80::0000:27ff:feab:6730/64 Scope:Link
```

有些人对隐私表示担心……

### 21.4. ipv4 mapped ipv6 address

某些应用程序使用嵌入在 `ipv6` 地址中的 `ipv4` 地址。（是的，将有一个 `ipv4` 和 `ipv6` 并使用的迁移时代。）此时 `ipv6` 地址看起来像这样：

```
::ffff:192.168.1.42/96
```

确实是十进制和十六进制字符的混合……

### 21.5. link local addresses

以 `fe8::` 开头的 `ipv6` 地址只能在本地段使用（将点替换为十六进制数字）。这就是为什么你在截图中将该地址标记为 `Scope:Link`。该地址仅用于本地链路。

```
paul@debian503:~$ /sbin/ifconfig | grep inet6
inet6 addr: fe80::a12:27ff:fe8e:aaa8/64 Scope:Link
inet6 addr: ::1/128 Scope:Host
```

这些链路本地地址都以 `fe8` 开头。

每个 `ipv6` 不会在这个范围内获得地址。

### 21.6. unique local addresses

现在已过时的 `site local` 地址类似于 `ipv4` 的私有范围，被一套全局唯一的本地 `ipv6` 地址系统所取代。这样做是为了防止在 `site local` 范围内加入网络时出现重复。

所有唯一本地地址都以 `fd::` 开始。

### 21.7. globally unique unicast addresses

由于 `ipv6` 设计为每个接口有多个地址，因此全局 `ipv6` 地址可以与链路本地地址一起使用。

这些全局唯一的地址以 `2...` 或 `3...` 作为前 16 位开头。

### 21.8. 6to4

`6to4` 在 `RFC` 2893 和 3056 中定义为通过 `ipv6` 隧道在 `ipv4` 和 `ipv6` 之间进行过渡的一种可能方法。



它将 `ipv4` 地址编码在以 `2002` 开头的 `ipv6` 地址中。例如，`192.168.1.42/24` 将被编码为：

## ipv6 简介

```
2002:c0a8:12a1::1::
```

你可以使用该命令将任何 `ipv4` 地址转换为此范围。

```bash
paul@ubi1010:~$ printf "2002:%02x:%02x:%02x:%04x:%1\n" echo 192.168.1.42/24 | tr tr /:/:'
2002:c0a8:012a:0018::1
```

## 21.9. ISP

如果你足够幸运从 ISP 获取了一个 `ipv6` 地址，那么它将以 `2001` 开头。

## 21.10. 不可路由地址

类似于 DNS 中的 `example.com`，`ipv6` 地址被预留用于示例，且在互联网上是不可路由的。

```
ffff::32
2001:db8::32
```

## 21.11. ping6

使用 `ping6` 测试 `ipv6` 主机之间的连接性。你需要指定接口（对于“随机”生成的地址没有路由表）。

```bash
[root@fedora4]# ping6 -I eth0 fe80::a00:27ff:fec:(fe80::a00:27ff:fec) from fe80::a00:27ff:3c:4346 eth0: 56
64 bytes from fe80::a00:27ff:fec icmp_seq=1 ttl=64 time=0.58 ms
64 bytes from fe80::a00:27ff:fec icmp_seq=2 ttl=64 time=3.95 ms
64 bytes from fe80::a00:27ff:fec icmp_seq=3 ttl=64 time=1.53 ms
```

以下多播接收了来自网络上三个 `ipv6` 主机的回复。

```bash
[root@fedora4]# ping6 -I eth0 ff02::1
ff02::1 (ff02::1) from fe80::a00:27ff:fec:4346 eth0: 56
64 bytes from fe80::a00:27ff:fec icmp_seq=1 ttl=64 time=0.59 ms
64 bytes from fe80::a00:27ff:fec icmp_seq=2 ttl=64 time=1.87 ms (DUP!)
64 bytes from fe80::a00:27ff:fec icmp_seq=3 ttl=64 time=1.53 ms (DUP!)
64 bytes from fe80::e87b:9dd:ffec2 icmp_seq=1 ttl=64 time=5.35 ms (DUP!)
64 bytes from fe80::a00:27ff:fec:3c:4346 icmp_seq=2 ttl=64 time=0.106 ms
64 bytes from fe80::e87b:9dd:ffec2 icmp_seq=2 ttl=64 time=1.79 ms (DUP!)
64 bytes from fe80::a00:27ff:fec icmp_seq=2 ttl=64 time=2.48 ms (DUP!)
```

## 21.12. 比利与 ipv6

关于比利 `ipv6` 的大量信息可以在 `www.ipv6council.be` 找到。

像 `ipv6.belgium.be`、`www.bipt.be` 和 `www.bricozone.be` 等网站已启用 `ipv6`。一些大学也是如此：`up.ac.be` (那穆) 和 `ulg.ac.be` (列日)。

## 21.13. 其他网站

测试 `ipv6` 的其他有用网站有：

```
test-ipv6.com
ipv6-test.com
```

访问 `ipv6-test.com` 网站将测试你是否有一个有效的 `ipv6` 地址。

![](img/1d499a6177836f6f088a9e2a53e11a14_247_0.png)

访问 `test-ipv6.com` 网站也将测试你是否有一个有效的 `ipv6` 地址。

## 测试你的 IPv6 连接性。

你在公网上的 `IPv4` 地址

世界 `IPv6` 日是 2011 年 6 月 8 日，即 `IPv6` 协议出版的周年。

恭喜！你似乎同时拥有 `ipv4` 和 `ipv6` 互联网连接。如果发布者发布了 `ipv6` 版本，你的浏览器将回退到 `IPv4`。如果你在选择时优选 `ipv6` 而非 `ipv4`，这在未来可能会影响猜测你位置网站的准确性。

你似乎正在使用 `IPv6` 网关；你的路由器可能正在自动完成。这种方法可能存在局限性。最好从你的 ISP 获取原生 `ipv6` 地址。

你的 `ipv6` 服务器（由你的 ISP 提供）似乎无法访问 `ipv6` 互联网，或者没有配置使用它。这在未来可能会限制你访问仅限 `ipv6` 的网站。

- 为了你的 `ipv4` 稳定性和就绪，当发布者提供 `ipv4` 和 `ipv6` 时
- 为了你的 `ipv6` 稳定性和就绪，当发布者强制仅使用 `ipv6` 时

## 21.14. cto4 网关

如果你使用 `sixxs.net` (具体为 `http://www.sixxs.net/tools/`) 作为网关，则仅 `ipv4` 可用。

例如使用 `http://www.dashdot.sixxs.org/`

## 21.15. ping 和 dns

以下来自 `cto4` 的 `ping` 记录。

| 源 | 目的 | 协议 | way |
| :--- | :--- | :--- | :--- |
| | | | |
| `81.105.101.125` | `199.130.111.4` | `DNS` | 标准查询 `ipv6-test.com` |
| `199.130.131.4` | `81.105.101.125` | `DNS` | 标准查询 `AAAA` `2001:41d0:67d1:7e57:1` |
| `2002:55a:657d1` | `2001:41d0:67d1:7e57:1` | `TCP` | `Echo` `request` |
| `2001:41d0:67d1:7e57:1` | `2022:55a:657d1` | `TCP` | `Echo` `reply` |

## 21.16. ipv6 和 tcp/http

以下通过 `ipv6` 的握手连接记录。

| 源 | 目的 | 协议 | 信息 |
| :--- | :--- | :--- | :--- |
| | | | |
| `2002:55a:657d1` | `2001:41d0:67d1:7e57:1` | `TCP` | `[SYN]` `Seq=0` `Win=5648` |
| `2001:41d0:67d1:7e57:1` | `2002:55a:657d1` | `TCP` | `[ACK]` `Seq=1` `Ack=5648` |
| `2002:55a:657d1` | `2001:41d0:67d1:7e57:1` | `TCP` | `GET` `/index.html` |
| `2001:41d0:67d1:7e57:1` | `2002:55a:657d1` | `TCP` | `[ACK]` `Seq=1` `Ack=708` |

## 21.17. ipv6 PTR 记录

如 DNS 章节所示，`ipv6` `PTR` 记录位于 `ipv6.net`，并生成域名。

```
> Frame 64 bytes on 132 bytes) Ethernet, Src:2002:55a:657d1;Dst:00:26:b0:5d:22;Dst:cf:6a:10 (00:b0:6a:10) Protocol, Src:181.105.101.125 (81.105.101.125), Dst:195.130.131.4 (195.130.131.4) Dataagram Protocol, Src Port:34361 (34361), Dst Port:53 (domain) Domain Name System (query) [Response: no answer]
   Transaction ID: 0xfec3
   Flags: 0x8100 (Standard query)
   Questions: 1
   Answers: 0
   Authority RR: 0
   Additional RR: 0
   Query > 10.0.0.5.7.e.7.0.0.1.6.7.2.0.0.0.1.4.0.0.ip6.arpa: type: ptr, CLASS IN
```

## 21.18. Linux cto4 配置

以下是 Linux 上 `cto4` 配置的记录。

感谢 `http://www.anynode.cz/v6linux6to4` 和 `https://mirrors.bieringer.de/Linux+IPv6-HOWTO/`; 以及 `tldp`。

```bash
root@mac:~# ifconfig
eth0 link enc:Ethernet Waddr 00:26:b0:5d:22:5e
      inet addr:81.105.101.125 Bcast:255.255.255.255 Mask:255.255.255.248
```



# ipv6 简介

```
inet6 addr:fe80::226:bfffe:2e52/64 Scope:Link
  UP BROADCAST ROUTING MULTICAST MTU:1500 Metric:1
RX packets:5926404 errors dropped:0 overruns:frame:0
TX packets:2998529 errors dropped:0 overruns:carrier:0
collisions:0 txqueuelen:1000
RX bytes:427948342 (4.0 G) TX bytes:237002179 (237.0 MB)
Interrupt: 43 Base address:0x8000
lo encap: Local Loopback
  inet addr:127.0.0.1 Mask:255.255.0.0
  inet6 addr::/128 Scope:Host
UP RUNNING MULTICAST MTU:1636 Metric:1
RX packets:598 errors dropped:0 overruns:frame:0
TX packets:598 errors dropped:0 overruns:carrier:0
collisions:0 txqueuelen:0
RX bytes:61737 (61.7 KB) TX bytes:61737 (61.7 KB)
root@host:~ # sysctl -w net.ipv6.default
```

`2002::16 dev tun04 metric 1024 mtu 1472 advmss 1412 hoplimit 0`

`fdcb::43cl:9c18:1::64 dev eth0 proto kernel metric 256 mtu 1500 advmss 1440 hoplimit 0`

`fe80::/64 dev eth0 proto kernel metric 256 mtu 1500 advmss 1440 hoplimit 0`

`default via ::1 ping ipv6-test.com`

`default via ::192.168.99.1 dev tun64 metric 1 mtu 1472 advmss 1412 hoplimit 0`

`PING ipv6-test.com (ipv6-test.com) 56 data bytes`

`64 bytes from ipv6-test.com: icmp_seq=1 ttl=57 time=42.4 ms`

`64 bytes from ipv6-test.com: icmp_seq=2 ttl=57 time=43.0 ms`

`64 bytes from ipv6-test.com: icmp_seq=3 ttl=57 time=43.5 ms`

`64 bytes from ipv6-test.com: icmp_seq=4 ttl=57 time=43.9 ms`

`64 bytes from ipv6-test.com: icmp_seq=5 ttl=57 time=45.6 ms`

```
---
 ipv6-test.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 42.485/43.717/45.632/1.091 ms
```

# 第 X 部分 附录

# 目录

- A. 克隆 ........................................................................................................ 247

A.1. 关于克隆 ..................................................................................... 247

A.2. 关于离线克隆 ................................................................................ 247

A.3. 离线克隆示例 ............................................................................ 247

B. 许可证 ................................................................................................ 249

# 附录 A 克隆

## A.1. 关于克隆

你对克隆服务器可能有不同的目标。例如，克隆可以是一个用于服务手动灾难恢复的冷备备份系统。或者，可以创建一个克隆以用于测试环境。又或者你可能想创建一个几乎相同的服务器。让我们来看看一些创建 Linux 服务器克隆的离线和在线方法。

## A.2. 关于离线克隆

离线克隆用于在关闭运行中的 Linux 服务器电源时创建克隆。这种方法非常简单，因为我们不需要打开文件，也不需要跳过 `/dev` 或 `/sys` 等虚拟文件系统。离线克隆方法可以分解为以下步骤：

1. 使用启动光盘启动源服务器和目标服务器
2. 在目标服务器上进行分区、格式化并挂载卷
3. 通过网络从源到目标复制文件/分区

第一次尝试是非常容易的。第二步将在“磁盘管理”章节中解释。对于第三步，我们可以使用 `ssh` 或 `netcat` 结合 `cp`、`dd`、`dump` 以及 `restore-tar`、`cpio`、`rsync` 甚至 `cat`。

## A.3. 离线克隆示例

```
[root@RHEL5 ~]# 我们正在处理一台 Red Hat Enterprise Linux 5 服务器，我们想在较新的硬件上获得它的完美副本。首先要做的任务是发现磁盘布局
```

| 文件系统 | 大小 | 可用空间 | 使用率 | 挂载点 |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/sda2` | 15G | 4.9G | 9.3G | 33% |
| `/dev/sda1` | 91M | 64M | 33% | `/boot` |

`/boot` 分区很小，但足够大。如果我们创建一个完全相同的分区，那么 `dd` 将是一个很好的克隆选项。假设目标系统上需要擦除 `/partition`。最佳选项是使用 `dump` 和 `restore` 的组合。记住，`dd` 复制块，而 `dump`/`restore` 复制文件。

第一步是用 Live 盘 CD 启动目标服务器对目标磁盘进行分区。为了做到这一点，我们使用 Red Hat Enterprise Linux 5。在 CD 启动提示符处输入“linux rescue”。CD 启动进入 root 控制台，可以在那里使用 `fdisk` 发现并准备连接的磁盘。当分区创建并具有文件系统后，我们就可以使用 `dd` 复制 `/boot` 分区。

![](img/499a6177836f088a9e2a53e11a40.png)

```
ssh root@192.168.1.40 "dd if=/dev/sda | of=/dev/sda"
```

然后我们使用 `dump` 和 `restore` 组合来复制分区。

```
mkdir /mnt/x
mount /sda2 /mnt/x
ssh root@192.168.1.40 "dump -f - | restore -f -"
```



# 附录 B 许可证

GNU 文档许可证

版本 1.3，2008年11月

版权 © 2000-2007 Free Software Foundation, Inc.

## 前言

本许可证的目的是使手册、教科或其他文档在自由的意义上是“自由”的：允许每个人有效地复制和分发它，或者在不修改它的情况下，无论是商业性还是非商业性的。其次，本许可证保留了作者和出版者获得其工作认可的方式，同时不对他人的修改负责。本许可证是一种“左版拷贝”（`copyleft`），这意味着衍生作品必须在相同的意义上是自由的。它补充了 `GNU General Public License`，后者是为自由软件设计的，但不限于软件；它可以用于任何文本作品，无论主题是什么或是否以印刷书的形式出版。

## 1. 应用与定义

本许可证适用于任何媒介的任何手册或其他作品，这些作品包含版权所有者发布的声明，说明其是根据本许可证的条款分发的。此类声明授予了在全球范围内免版税的无限期根据此处列出的条件使用该作品的。“文档”是指任何手册或其他作品。公众任何成员都是被许可者，被称为“你”。如果你以需要版权法许可的方式复制、修改或分发作品，则表示接受该许可证。文档的“修改版本”是指任何包含文档的作品。

“修改版本”的文档意味着任何包含文档的作品。

本许可证适用于任何媒介的任何手册或其他作品，这些作品中包含一个由版权所有者发布的声明，说明其是根据本许可证的条款分发的。此类声明授予了在全球范围内免版税的无限期根据此处列出的条件使用该作品的。“文档”是指任何手册或其他作品。公众任何成员都是被许可者，被称为“你”。如果你以需要版权法许可的方式复制、修改或分发作品，则表示接受该许可证。文档的“修改版本”意味着任何包含文档的作品。

“修改版本”的文档意味着任何包含文档的作品。

（注：由于原文文本中存在大量重复，翻译已按要求进行对应处理）

## 2. 复制

无论是商业还是非商业用途，只要在所有副本中都复制了本许可证、版权声明以及说明本许可证适用于本文档的许可公告，并且您没有使用任何不同于本许可证的额外条件，均可使用。您不得使用技术措施阻止副本的阅读或进一步分发。然而，您可以接受作为副本的报酬。如果您分发了足够数量的副本，必须遵守第 3 节中的条件。

您可以在上述相同条件下出借副本，并公开发示副本。

## 3. 批量复制

如果您出版本文档的打印副本（或常见有副本的媒介副本）数量超过 100 份，且本文档的许可声明需要封面文本（`Cover Texts`），则必须将副本封装在封内，并在封面上清晰、易读地载入所有的封面文本：封面上的封面文本和封底上的封底文本。两个封面都必须清晰、易读地标识您为出版者，且封面必须展示完整标题，且标题中的所有文字必须清晰、可见。您还可以在封面上添加其他材料。对封面进行修改的复制，只要保留了本文档的标题并满足这些条件，在其他方面可以被视为逐字复制。

如果某个封面所需的文本量太大而无法合规容纳，您应当将列出的前面的文本（在合理范围内）放在封面上，并将剩余继续到相邻页面。

如果您出版或分发数量超过 100 份本文档的不透明副本（`Opaque copies`），您必须在每份不透明副本旁包含一份机器可读的透明副本（`Transparent copy`），或者在每个不透明副本中说明一个计算机网络位置，公众可以使用公共标准网络协议从该位置免费下载不含材料的本文档透明副本。如果您选择后者，则必须在开始大量分发不透明副本时立即停止，以确保透明副本在所述位置保持激活状态，直到您最后一次向公众（直接或通过您的代理或零售商）分发该不透明副本后至少一年。

建议但不要求您在重新分发任何大量副本之前联系本文档的作者，以便他们有机会向您提供更新版本的本文档。

## 4. 修改

您可以在第 2 节和第 3 节的条件下复制并分发本文档的修改版本，前提是您完全按照本许可证发布修改版本，由修改版本承担本文档的角色，从而向任何拥有该副本的人许可分发和修改该版本。此外，您必须在修改版本中完成以下事项：

- 在标题页（以及封面）上列出一个标题，如果该标题与本文档的标题以及之前版本的标题（如果有，则应列在本文档的“历史”部分中）不同。如果该版本的原始出版者给予许可，您可以使用与之前的版本相同的标题。
- 在标题页上列出修改版本的作者、对修改版本中修改内容承担作者责任的一个或或多个个人或实体，以及本文档的至少五位主要作者（如果主要作者少于五位，则列出所有主要作者），除非他们免除了您的此项项要求。
- 在标题页上列出修改版本的出版者名称，并与其他公告并列。
- 保留本文档的所有版权声明。
- 在其他公告旁为您的修改包含包含适当的版权声明。
- 在版权声明之后立即包含一份许可，允许公众根据下方附录中列出的本许可证条款使用修改版本。
- 在许可中保留不变部分（`Invariant Sections`）的完整列表，并在本文档的许可公告中保留覆盖文本（`Covered Texts`）。
- 包含未经修改的本许可证副本。
- 保留标题为“历史”的章节，保留其标题，并在其中添加一项，至少说明修改版本的标题、年份、新作者和出版者。如果在标题页上没有该章节，请在其中添加一项，说明修改版本的标题、年份、作者和出版者。
- 保留本文档的网络位置（如有），并在该位置保持有效以供公众通过公共标准网络协议访问本文档，或者如果该版本基于该版本的原始出版者授予了您此类许可。
- 对于任何标题为“感谢”或“致谢”的章节，保留其标题并保留其感谢或致谢的内容。
- 保留本文档的所有不变部分，其文本和标题。章节编号不属于章节标题。
- 删除“认可”的章节。此类章节不得包含在修改版本中。
- 不保留任何与“认可”冲突的现有章节。
- 保留免责声明。

如果修改版本包含了不包含自本文档材料的前言章节或附录，您可以选择将这些章节或全部指定为不变部分。为此，请在修改版本的许可公告中的不变部分列表中添加您的标题。这些章节必须与其他章节区分来。

您可以添加一个名为“认可”的章节，只要其内容仅包含对您修改版本的认可。

## 8. 翻译

翻译被视为一种修改，因此您可以根据第 4 节的条款分发文档的翻译版本。将“不变部分”（`Invariant Sections`）替换为翻译内容需要其版权持有者的特殊许可，但您可以在不变部分原始版本的基础上，包含其部分或全部内容的翻译。您可以包含本许可的译文、文档中所有的许可声明以及任何免责声明，前提是您包含了本许可的原始英文版本，以及这些声明和披露的原始版本。如果译文与本许可或通知或免责声明的原始版本不一致，以原始版本为准。

如果文档中的章节标题为“致谢”（`Acknowledgements`）”、“献辞”（`Dedications`）或“历史”（`History`），则保留其标题的第（第 4 节第1节）通常要求更改实际标题。

## 9. 终止

除非本许可明确规定，否则您不得复制、修改、分许可或分发文档。任何复制、修改、分许可或分发文档的尝试都是无效的，并将自动终止您根据本许可享有的权利。

然而，如果您停止了对本许可的所有违反行为，则您从特定版权持有者处获得的许可将恢复：（a）临时恢复，除非版权持有者明确且最终地终止了您的许可；b）或者版权持有者在您停止行为后 60 天内通过合理手段通知了您的违反行为。

此外，如果版权持有者通过某些合理手段通知了您的违反行为，且这是您首次收到该版权持有者关于（任何作品）违反本许可的通知，并且您在收到通知后 30 天内避免了违规行为，则您从特定版权持有者处获得的许可将永久恢复。

根据本节终止您的权利并不终止已从您处获得文档副本或权利的方的许可。如果您的权利已被终止且未永久恢复，获得部分或全部材料的副本并不赋予您使用这些材料的权利。

## 10. 本许可的未来修订

自由软件基金会不定期发布 `GNU 自由许可`的新修订版本。这些新版本将与当前版本相似，但在细节上可能有所不同，以解决新的问题或疑虑。请参见 `http://www.gnu.org/licenses/`

许可的每个版本都有一个不同的版本号。如果文档规定本许可的某个特定编号版本“或任何后续版本”适用于您，则您可以选择遵循指定版本或由自由软件基金会发布（非草稿形式）的任何后续版本的条款和条件。如果文档未指定本许可的版本号，您可以选择自由软件基金会发布过的任何版本（非草稿形式）。代理人可以决定可以使用本许可的未来哪些版本，代理人对某个版本的公开接受的声明将永久授权您为该文档选择该版本。

## 11. 重新许可

“大规模作者协作站点”（`Massive Multiauthor Collaboration Site`，或“`MMC Site`”）是指任何发布受版权保护的作品并为任何人编辑这些作品提供便利设施的全球网服务器。任何人都可以编辑的 `wiki` 是此类服务器的示例。站点中的“大规模作者协作”（或“`MMC`”）是指在 `MMC` 站点上发布的任何一组受版权保护的作品。

“`CC-BY-SA`”是指由知识共享组织（`Creative Commons Corporation`）发布的知识共享署名-相同共享 3.0 许可，该组织是一家总部位于加利福尼亚州旧金山的非营利机构，以及该组织发布的该许可的未来后续许可版本。

“合并”（`Incorporate`）是指将文档全部或部分作为另一份文档的一部分重新发表。

如果一个 `MMC` 是根据本许可授权的，并且所有首次在某 `MMC` 之外的地方根据本许可发布、随后全部或部分地合并到该 `MMC` 中的作品符合以下条件，则该 `MMC`“符合重新许可条件”：（1）没有复制文本或不变部分，且（2）是在 2008 年 11 月 1 日之前完成合并的。

`MMC` 站点的运营可以在 2009 年 8 月 1 日之前的任何时间，在同一站点上以 `CC-BY-SA` 重新发布站点内的 `MMC`，前提是该 `MMC` 符合重新许可的条件。

## 符号

- `CIFS`, 143
- `CNAME` (`DNS` 记录), 67
- `context type(selinux)`, 215
- `create(mysql)`, 47, 59, 55
- `create mask (Samba)`, 182
- `/etc/apache`, 10
- `/etc/bind/named.conf.local`, 76
- `/etc/group`, 45
- `/etc/httpd`, 10
- `/etc/initd.conf`, 152
- `/etc/initd.samba`, 141
- `/etc/initd.dnmb`, 141
- `/etc/initd/winbind`, 142
- `/etc/initd.conf`, 190, 192（等，根据上下文修正）
- `/etc/passwd`, 45, 99
- `/etc/resolv.conf`, 62
- `/etc/samba/posix.db`, 198
- `/etc/samba/smbd.conf`, 146, 147, 164, 188
- `/etc/samba/smb`, 169, 196
- `/etc/selinux/config`, 212
- `/etc/squid/squid.conf`, 34
- `/etc/sysctl.conf`, 116
- `/etc/mod.at`, 152
- `/proc/sys/ipv4/forward`, 116
- `/selinux`, 214
- `/selinux/enforce`, 24
- `/var/log/audit/audit.log`, 210
- `/var/log/squid`, 39
- `.htaccess`, 27
- `.htpasswd`, 14
- `.my.cnf`, 46
- `A` (`DNS` 记录), 67
- `AAAA` (`DNS` 记录), 67
- `allow hosts (Samba)`, 181
- `apache2`, 6
- `aptitude`, 138, 139, 227
- `aptitude(0)`, 44
- `audit`, 210
- `authoritative (dns)`, 71
- `authoritative zone`, 66
- `axfr`, 74
- `filter table (iptables)`, 123
- `firewall`, 114
- `force create mode(samba)`, 183
- `force directory mode(samba)`, 183
- `force security mask(samba)`, 183
- `force group(samba)`, 170
- `force user(samba)`, 170
- `forwarder (dns)`, 70
- `forward lookup query`, 61
- `fdqn`, 66
- `fully qualified domain name`, 66
- `bind`, 64
- `bind(dns)`, 90
- `browsable (Samba)`, 182
- `browser master`, 196
- `getforce`, 211
- `geten(1)`, 191
- `getattr(1)`, 217
- `git`, 226
- `github`, 232
- `glue rec (dns)`, 67
- `grant(mysql)`, 48
- `group by(mysql)`, 54
- `guest ok (Samba)`, 157
- `caching only name server`, 68
- `chain (iptables)`, 123
- `chart(mysql)`, 49
- `chon(1)`, 216, 217
- `chkconfig`, 210
- `chmodmod`, 213
- `hide(samba)`, 182
- `host (DNS 记录)`, 67
- `hostname`, 66, 143
- `hosts.txt`, 60
- `hosts allow (Samba)`, 181
- `hosts deny (Samba)`, 182
- `htpasswd(1)`, 17, 24
- `httpd`, 7
- `IBM`, 143
- `id(1)`, 216
- `identity(selinux)`, 214
- `idmap gid(samba)`, 188
- `idmap uid(samba)`, 188
- `inetd(8)`, 152
- `insert(mysql)`, 51
- `integer(mysql)`, 49
- `invalid users (Samba)`, 181
- `iptables`, 122, 123
- `iptables save`, 127
- `iterative query`, 70
- `ifxr`, 74
- `LAMP`, 43
- `ls`, 213
- `ls(1)`, 217
- `mac address`, 117
- `mangle table (iptables)`, 123
- `masquerading`, 115
- `master server (DNS)`, 73
- `MX` (`DNS` 记录), 67
- `mysql`, 43, 45, 46
- `mysql(group)`, 45
- `mysql(user)`, 45
- `mysql-client`, 44
- `mysqld`, 45
- `mysql-server`, 44
- `NAPT`, 115
- `NAT`, 115
- `net table (iptables)`, 123
- `NetBIOS names`, 143
- `netcat`, 160
- `net group`, 201
- `net rpc join(microsoft)`, 159
- `net use(samba)`, 189
- `net view(mysql)`, 146
- `NS` (`DNS` 记录), 67
- `nslookup`, 61
- `NT_STATUS_BAD_NAME`, 176
- `NT_STATUS_LOGON_FAILURE`, 176
- `order(mysql)`, 53
- `packet filtering`, 114
- `packet forwarding`, 114
- `passbd backend(samba)`, 170
- `Paul`, 60
- `php`, 43
- `ping`, 117, 118
- `port forwarding`, 115
- `primary dns server`, 71
- `primary server (DNS)`, 73
- `proxy server`, 33
- `ps(1)`, 217
- `PTR` (`DNS` 记录), 67
- `public key`, 232
- `query (dns)`, 61
- `read list (Samba)`, 181
- `read only (Samba)`, 164
- `recursive query`, 70
- `reverse lookup query`, 61
- `roaming profiles(samba)`, 200
- `root(selinux)`, 214
- `root(DNS)`, 63
- `root(mysql)`, 44
- `root lists`, 64
- `root server (dns)`, 69
- `root servers (dns)`, 63
- `router`, 114
- `rpm`, 138
- `rpm(1)`, 44
- `rpm(8)`, 139
- `samba`, 138
- `secondary dns server`, 71
- `secondary server (DNS)`, 73
- `security(samba)`, 157
- `security mask(samba)`, 183
- `security mode(samba)`, 174
- `select(mysql)`, 51, 52, 52
- `SELinux`, 209
- `selinux`, 212
- `selinux-activate`, 210
- `service(8)`, 141
- `sestatus`, 212
- `setenforce`, 211
- `show(mysql)`, 47, 49
- `slave-server(DNS)`, 73
- `SMB`, 143
- `smbclient`, 149, 158
- `smbclient(1)`, 148, 175
- `smbd(8)`, 142, 146, 169
- `smbpasswd(2)`, 201
- `smbpasswd(8)`, 169, 174
- `smbitree`, 151
- `smbtree(1)`, 150
- `smtmp`, 67
- `SNAT`, 115
- `soa (dns 记录)`, 71
- `SQL`, 43, 51
- `squid`, 33
- `有状态防火墙`, 114
- `swat(8)`, 152
- `syslog`, 116

## T

- `tcpdump`, 61, 118
- `dbsan`, 170, 196, 198
- `testparam(1)`, 147, 147, 148
- `tld`, 65
- `TLD (dns)`, 65
- `顶级域名`, 65
- `transition(selinux)`, 216
- `trigger(mysql)`, 55
- `tiggers(mysql)`, 44
- `type(sellinux)`, 215

## U

- `update(mysql)`, 52
- `use(mysql)`, 48

## V

- `valid users (Samba)`, 181
- `varch(mysql)`, 49
- `virtualbox`, 117
- `vmware`, 117

## W

- `wbinfo(1)`, 190, 191
- `webalizer`, 27
- `winbind(8)`, 190
- `winbind(samba)`, 188
- `winbind(8)`, 142, 142, 190
- `wireshark`, 118
- `workgroup`, 17
- `writable (Samba)`, 164
- `write list (Samba)`, 181

## X

- `xinetd(8)`, 152

## Y

- `yum`, 139

## Z

- `zone (dns)`, 66, 71
- `zone transfer (dns)`, 71
