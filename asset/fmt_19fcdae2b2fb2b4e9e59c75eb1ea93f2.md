
```
From - Sun Jan 27 22:42:06 2001
ftp://rpmfind.net/linux/redhat/updates/6.2/i1386
Directory of /linux/redhat/updates/6.2/i1386
Current directory is /linux/redhat/updates/6.2/i1386
Up to higher level directory
SysVint-2.7-8.i1386.rpm             80 KB Thu Nov 9 20:45:00 2000
apache-1.3-14-2.6.i1386.rpm         420 KB Mon Oct 23 23:35:00 2000
apache-devel-1.3-14-2.6.i1386.rpm    108 KB Mon Oct 23 23:36:00 2000
apache-manual-1.3-14-2.6.i1386.rpm   462 KB Mon Oct 23 23:36:00 2000
auth_ldap-1.4.0-i1386.rpm          26 KB Mon Oct 23 23:36:00 2000
imap-2000-2.6.i1386.rpm           1934 KB Fri Nov 10 16:45:00 2000
imap-devel-2000-2.6.i1386.rpm     1118 KB Fri Nov 10 16:51:00 2000
kernel-2.2.16-3.i1386.rpm           5818 KB Mon Jun 25 00:00:00 2000
kernel-BOOT-2.2.16-3.i1386.rpm     3351 KB Mon Jun 26 00:00:00 2000
kernel-doc-2.2.16-3.i1386.rpm       953 KB Mon Jun 26 00:00:00 2000
kernel-headers-2.2.16-3.i1386.rpm  1128 KB Mon Jun 26 00:00:00 2000
mod_perl-1.2.3-0.i1386.rpm         746 KB Mon Oct 23 23:37:00 2000
netscape-common-4.76-0-0.6.i1386.rpm 8326 KB Fri Nov 17 19:50:00 2000
netscape-communicator-4.76-0-0.6.i1386.rpm 5909 KB Fri Nov 17 19:51:00 2000
ns_ldap-1.2.1-i1386.rpm            314 KB Mon Oct 23 23:55:00 2000
openssl-1.2.9-6.i1386.rpm          1326 KB Fri Nov 10 17:00:00 2000
openssl-devel-1.2.9-6.i1386.rpm     128 KB Fri Nov 10 17:00:00 2000
openssl-0.95-a-2.6.i1386.rpm     1170 KB Fri Nov 10 16:46:00 2000
openssl-devel-0.95-a-2.6.i1386.rpm    894 KB Fri Nov 10 16:46:00 2000
openssl-perl-0.95-a-2.6.i1386.rpm     15 KB Fri Nov 10 16:46:00 2000
openssl-python-0.95-a-2.6.i1386.rpm   123 KB Fri Nov 10 16:46:00 2000
perl-5.0053-13.i1386.rpm           4923 KB Fri Aug 18 22:45:00 2000
php-3.0.17-1.2.i1386.rpm            306 KB Mon Oct 23 23:37:00 2000
php-image-3.0.17-1.2.i1386.rpm        352 KB Mon Oct 23 23:35:00 2000
php-ldap-3.0.17-1.6.i1386.rpm        314 KB Mon Oct 23 23:36:00 2000
php-manual-3.0.17-1.6.i1386.rpm     968 KB Mon Oct 23 23:36:00 2000
php-postgresql-3.0.17-1.6.i1386.rpm   16 KB Mon Oct 23 23:36:00 2000
python-1.5.2-27.6.x.i1386.rpm       1805 KB Thu Dec 21 21:32:00 2000
python-xmlrpc-1.2.1-0-6.x.i1386.rpm     35 KB Thu Dec 21 21:32:00 2000
```

## 通过 RPM 添加模块

向基于 RPM 的发行版添加新模块只需调用 `rpm` 来升级/安装内容：

```
# rpm -Uvh apache-x.x.x.rpm
```

当升级完成后，Apache 应该已经准备好运行。

## 启动 Apache

Red Hat 使用 `httpd` 来启动服务器：

```
httpd
```

`httpd` 是一个位于 `/usr/sbin/` 的脚本，用于启动 Apache 守护进程。该脚本位于 `/etc/rc.d/init.d/`。要查看命令行选项，输入 `httpd` 即可显示：

```
Usage: ./httpd {start|stop|restart|status}
```

## 本地验证功能

升级 Apache 的最后一步是测试服务器。当守护进程运行时，Apache 应该监听环回设备的 80 端口。通常环回设备位于 `127.0.0.1`，并可以通过 `localhost` 访问。任何 Web 浏览器都可以进行此测试。`Lynx` 是一个不错的选择：

```
lynx localhost
```

Apache 测试页面应该加载并显示以下内容：

It Worked! The Apache Server is Installed!

如果你看到此页面，说明该域的所有者刚刚成功安装了 Apache 服务器软件。他们现在需要向此目录添加内容并替换此占位页面，或者将服务器指向他们的真实内容。

## 调用不带任何选项的 ifconfig

调用不带任何选项的 `ifconfig` 可以找到系统上所有可用网络接口的列表：

```
ifconfig
eth0 Link encap:Ethernet HWaddr 00:80:C8:14:73:77
       inet addr:10.168.1.2 Mask:255.255.0.0
       UP BROADCAST MTU:1500 Metric:1
       RX packets:20477 errors:0 dropped:0
       TX packets:20895 errors:0 dropped:0
       collisions:0 txqueuel:100
       Interrupt:Base address:0x340
lo Link encap:Local Loopback
       inet addr:127.0.0.1 Mask:255.255.0.0
       UP LOOPBACK RUNNING MTU:3924 Metric:1
       RX packets:3993 errors:0 dropped:0
       TX packets:3993 errors:0 dropped:0
       collisions:0 txqueuel:100
```

`inet addr:10.168.1.2` 部分表示系统的本地 IP 地址。

可以使用 `Lynx` 或任何其他浏览器进行此测试：

```
# lynx 10.168.1.2
```

在此处使用您实际的 IP 地址。

如果所有配置均正确，Apache 测试页面应该会在浏览器中加载。如果用户没有浏览器，请使用 `telnet` 连接。

接下来，使用名称而不是 IP 地址来测试该页面。

## 将域名映射到 IP 地址两种方法

最简单的方法是在客户端的 `/etc/hosts` 文件中添加条目。该条目的格式如下：

```
10.168.1.1 alias1 alias2.domain.com alias3.xyz.cx
```

格式为 IP 地址，后跟所有映射到该地址的名称。

另一种方法是使用 DNS。DNS 超出了本课程的范围，但如果服务器已经添加到 IP 网络中，添加 DNS 条目应该不没问题。

## 源 RPM

使用 RPM 进行软件开发遵循严格的阶段：从应用了本地补丁的源码开始，经过配置、编译和安装。构建的最终输出由一个源包和一个或可以安装的二进制包组成。整个构建过程在一个名为 `spec` 的文件中描述。
