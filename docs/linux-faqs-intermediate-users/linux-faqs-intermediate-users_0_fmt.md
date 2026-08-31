

# Linux 常见问题解答：中级用户指南

![](img/Image00003.jpg)

# 献辞

本书献给因新冠肺炎去世的 Sujata Biswas 女士。没有她的每一天都是一种折磨。她仍然是这家初创出版社背后的灵感来源。

# 交互式书籍

这是一个正在进行中的项目，如果您想向此常见问题解答中添加任何问题，我们将添加您的内容并反复出版本书。您可以将您的查询/问题/建议发送至`bookreviewer25@gmail.com`。

# 引言

所使用的方法是独特且在企业界备受青睐的。与其面对在关键时刻毫无用信息的长章节和段落，您可以获得相关问题——这些问题收集了 30 年的 IT 经验，并为您提供即时答案。

# 如何在 Linux 上创建 SUDO 用户？

在学习如何创建 SUDO 用户之前，我们为什么不复习创建普通用户和组的概念呢。

您的任务是在最近购买的 Linux 设备上创建新用户。访问系统的用户是 Helen、Leena 和 Tony – 他们属于 DevOps 组。您还需要创建一个组，富有想象力地命名为`devops`。用户将成为`devops`组的成员。

## 第 1 步：添加用户 –

```bash
# useradd helen
# useradd leena
# useradd tony
```

注意：以`ROOT`登录。

## 第 2 步：创建一个名为`devops`的组 –

```bash
# groupadd devops
```

当您创建用户时，他们是所属组的成员。我们可以将`devops`添加为附加组。

## 第 3 步：您使用的命令是`usermod` –

```bash
# usermod -aG devops helen
# usermod -aG devops leena
# usermod -aG devops tony
```

## 第 4 步：要检查每个用户的组成员身份，请使用命令`id` –

```bash
# id leena
uid=1003(leena) gid=1003(leena) groups=1003(leena),1005(devops)

# id tony
uid=1004(tony) gid=1004(tony) groups=1004(tony),1005(devops)

# id helen
uid=1002(helen) gid=1002(helen) groups=1002(helen),1005(devops)
```

您可以看到，每个用户都是附加组`devops`的成员。

如果您想锁定某个特定用户 - 他正在休假或离开了组织。您可以使用命令：

```bash
# usermod -L tony
```

必须**不要**赋予所有用户特权；然而，您无法独自完成所有任务，因此您必须将某些工作委托给选定的用户执行某些作业。如果这些用户需要执行需要管理员权限的任务，那么他们可以使用`SUDO`命令。您应该创建 SUDO 用户。

使用命令`visudo`检查 SUDO 配置文件并查看特定的一行。这是一个长文件。

此行意味着`wheel`组的成员可以运行所有命令。

```
%wheel  ALL=(ALL) ALL
```

创建一个名为`rosie`的用户 –

```bash
# useradd rosie
```

使用命令以`rosie`登录 shell：

```bash
$ su – rosie
```

尝试读取`/etc`目录下的 shadow 文件。shadow 文件包含加密后的密码。

```bash
$ cat /etc/shadow
```

`cat: /etc/shadow: Permission denied`

# 如何在 Linux 上创建目录结构？

您将学习关于 BASH 花括号扩展。例如，以下命令是一个在一个基础目录下创建子目录的快速方法。这里基础目录是`jupiter`。不要忘记斜杠，否则结果将会不同。

```bash
$ mkdir -p jupiter/{Io,Europa,Ganymede,Callisto}

$ cd jupiter

$ ls -l

total 0
drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Callisto
drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Europa
drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Ganymede
drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Io
```

你应该学习如何使用`touch`命令创建空文件。这是测试与权限相关的错误的好方法。

```bash
$ touch hello123
```

# 我如何处理压缩文件？

压缩文件在 Linux 用户中有通用的用法。如果有人必须发送日志文件进行故障排除，她通常会使用`tar`命令压缩日志，以减小日志的字节大小。如果她使用了`tar`命令，该压缩文件被称为 tarball（归包）。

让我们来看`fox.txt`文件：

```bash
$ ls -l fox.txt
-rw-rw-r--. 1 liza liza 14859 Nov 16 15:12 fox.txt
```

大小为 14859 字节。

使用`gzip`压缩文件：

```bash
$ gzip fox.txt
$ ls -l

total 4
-rw-rw-r--. 1 liza liza 139 Nov 16 15:12 fox.txt.gz
```

该文件现在只有 139 字节了。哇！

要解压，请使用以下命令：

```bash
$ gunzip fox.txt.gz
```

另一个你可以使用的压缩命令是`bzip2`。

```bash
$ bzip2 fox.txt
$ ls -l

total 4
-rw-rw-r--. 1 liza liza 149 Nov 16 15:12 fox.txt.bz2
```

解压命令是`bunzip2`。

还有一个较新的压缩命令叫做`xz`。

```bash
$ xz fox.txt
$ ls -l

total 4
-rw-rw-r--. 1 liza liza 164 Nov 16 15:12 fox.txt.xz
```

解压缩命令是`unxz`。

压缩是由这三种压缩算法完成的，而不是通过`tar`。

使用`gunzip`创建 tarball：

```bash
tar -cvzf fox.tar.gz fox.txt
```

使用`bzip2`创建 tarball：

```bash
tar -cvjf fox.tar.bz2 fox.txt
```

使用`xz`创建 tarball：

```bash
tar -cvJf fox.tar.xz fox.txt
```

注意：

请不要参考我的压缩结果，因为我使用的是一个小文件。你的结果会好得多。

## 你能解释一下文件/目录权限吗？

许多人离开组织时，忘记了交目录和文件权限，导致组成员无法访问这些目录。

请看下例示例，用户`prabal`已经离开了组织，但公共目录仍归他所有。而且组或其他人没有任何权限。当用户`liza`尝试访问该目录时，她无法进入。

```bash
$ ls -l
total 0
drwx------. 2 prabal prabal 6 Nov 16 15:53 common

$ cd common
-bash: cd: common: Permission denied
```

你需要做的是赋予目录`777`权限，这样`liza`就能访问该目录。

作为 root：

```bash
# chmod 777 common/
```

作为`liza`，你可以看到她能够访问该目录。

```bash
$ pwd
/opt/common

$ id
uid=1001(liza) gid=1001(liza) groups=1001(liza) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

对于文件权限，确保给`common`目录下的所有文件赋予`666`权限，但没有执行权限。

```bash
# chmod 666 * -R common
```

查看`common`的内容。

```bash
# ls -l
total 0
drwxr-xr-x. 2 root root 6 Nov 16 16:11 hello123
```

应使用以下命令移除执行权限：

```bash
# chmod -x * -R
# ls -l
total 0
drw-r--r--. 2 root root 6 Nov 16 16:11 hello123
```

## 什么是符号链接？

符号链接（Symbolic links）错误很常见，甚至能让经验丰富的系统管理员感到困惑。Linux 中有两种符号链接：

1. 软链接 (Soft links)

2. 硬链接 (Hard Links)




当你对现有文件创建软链接时，你创建了一个不同的文件。当你对现有文件创建硬链接时，你创建的是该文件的精确副本。软链接和硬链接都是使用`ln`命令创建的。

使用带有`-s`标志的`ln`命令创建软链接：

```bash
$ ln -s /etc/hosts hosts
```

现在执行`ls -l`命令。

```bash
$ ls -l
total 0
lrwxrwxrwx. 1 liza liza 10 Nov 16 16:30 hosts -> /etc/hosts
```

权限位中的`l`代表它是一个符号链接文件，并且有一个指向真实文件位置的箭头。

然而，尽管这两个文件的内容相同，它们仍然是不同的。如果你查看 inode 节点号（一种在文件系统中唯一标识文件的系统——类似于社会安全号）。

```bash
$ ls -i hosts
4525881 hosts

$ ls -i /etc/hosts
4358377 /etc/hosts
```

当你创建硬链接时，你创建的是文件的精确副本。硬符号链接是在带`-s`标志的情况下创建的。请注意，硬符号链接无法跨越同一系统上的不同文件系统，而软符号链接可以。

```bash
# ln /etc/passwd passwd
# ls -i passwd
4527544 passwd
# ls -i /etc/passwd
4527544 /etc/passwd
```

如你所见，它们共享相同的 inode 节点号`4527544`。

## 什么是 Linux BASH shell 环境？

Shell 是你与系统之间的接口。它是一个信息黑洞，由于变化迅速，可能需要一一生才能精通。在 Linux 世界中，一切皆文件。这意味着硬件设备如磁带驱动对于 Linux 来说仅仅是一个可以写入或执行其他操作的文件。

`BASH` 或 Bourne Again Shell 是许多 Linux 发行版（如不同的 Windows 版本）的默认 shell。

## 如何在 Linux Bash Shell 环境中创建别名（alias）？或者如何创建我自己的 Linux 命令？

别名可以定义为命令的 DOS 批处理方法，或者为你创建一个新的个性化命令。让我们为系统中运行的 Squid 代理服务器创建一个命令。我们将此别名命名为`proxystat`。

```bash
$ echo 'proxystat="systemctl status"' >> ~/.bashrc
```

别名是用于创建`systemctl status`命令的。这应该存在你的`.bashrc`文件中。通过`touch`命令在主目录下创建一个文件：

```bash
$ touch .bashrc
```

我们需要通过`source .bashrc`来刷新环境，让`systemctl status`命令被识别。

```bash
$ source .bashrc
```

现在运行你自己的命令`proxystat`：

```bash
$ proxystat
Redirecting to /bin/systemctl status
● squid.service - Squid proxy
    Loaded: loaded (/usr/lib/systemd/system/squid.service; disabled; vendor preset: disabled)
    Active: active (running) since Mon 2021-11-15 14:00:37 IST; 20h ago
    Process: 9959 ExecStart=/usr/sbin/squid $SQUID_OPTS -f /etc/squid.conf (code=exited, status=0)
    Process: 9954 ExecStart=/usr/libexec/squid/cache_swap.sh (code=exited, status=0)
    Main PID: 9962 (squid)
    CGroup: /system.slice/squid.service
      ├9962 /usr/sbin/squid -f /etc/squid.conf
      ├9964 (squid-1) -f /etc/squid.conf
      └9965 (logfile-daemon) /var/log/squid/access.log
```

## 如何在 Linux shell 环境中创建函数？

为了创建一个告诉你目录占用多少空间的简单函数，我们将使用`$1`（它是位置参数，是命令后的第一个占位符）以及提供空间详情的`du -h`命令。以下行必须添加到你的`.bashrc`文件中：

```bash
function spaceinfo()
{
    du -h /home/$1;
}
```

现在，你需要`source .bashrc`文件。函数的名称是`spaceinfo`。

```bash
$ source .bashrc
$ spaceinfo liza
4.0K  /home/liza/.ssh
8.0K  /home/liza/interns
0     home/liza/p3
2.2M  /home/liza
```

```text
├─647 /usr/sbin/NetworkManager --no-daemon

└─743 /sbin/dhclient -d -q -sf /usr/libexec/nm-dhcp-helper -pf /var/run/dhclient-enp0s3.pid -lf...
```

### 第 2 步

使用命令查找激活的网络接口：

```bash
$ nmcli c show
```

```text
NAME    UUID                               TYPE               DEVICE
enp0s3  ac113210-a008-43fa-b398-1fd052d81165  802-3-ethernet  enp0s3
```

激活设备是`enp0s3`。

### 第 3 步

对于你想要的信息，以下命令的输出提供了详细数据。

```bash
$ nmcli d show enp0s3
```

```text
GENERAL.DEVICE:                         enp0s3
GENERAL.TYPE:                           ethernet
GENERAL.HWADDR:                         08:00:27:                            4C:46:F9
GENERAL.MTU:                           1500
GENERAL.STATE:                          100 (connected)
GENERAL.CONNECTION:                    enp0s3
GENERAL.CON-PATH:                      /org/free            desktop/NetworkManager/ActiveConnection/1
WIRED-PROPERTIES.CARRIER:              on
IP4.ADDRESS[1]:                        192.168.29.182/24
IP4.GATEWAY:                           192.168.29.1
IP4.DNS[1]:                            192.168.29.1
IP6.ADDRESS[1]:                        2405:201:4003:8cc:98a:902d:637:d5d/64
IP6.ADDRESS[2]:                        fe80::e19:c87:e029:8cc/64
IP6.GATEWAY:                           fe80::e62:86ff:fe1e:c7c
IP6.ROUTE[1]:                          dst = 2405:201:4003:80cc::/64, nh = ::, mt = 100
IP6.DNS[1]:                            2405:201:4003:80cc::c0a8:1d01
```

```bash
[liza@lx-centos ~]$ nmcli d show enp0s3
```

```text
GENERAL.DEVICE:                         enp0s3
GENERAL.TYPE:                           ethernet
GENERAL.HWADDR:                         08:00:27:4C:46:F9
GENERAL.MTU:                           1500
GENERAL.STATE:                          100 (connected)
GENERAL.CONNECTION:                    enp0s3
GENERAL.CON-PATH:                      /org/freedesktop/NetworkManager/ActiveConnection/1
WIRED-PROPERTIES.CARRIER:              on
IP4.ADDRESS[1]:                        192.168.29.182/24
IP4.GATEWAY:                           192.168.29.1
IP4.DNS[1]:                            192.168.29.1
IP6.ADDRESS[1]:                        2405:201:4003:80cc:984a:902d:2637:d5d/64
IP6.ADDRESS[2]:                        fe80::e19d:c87:e029:81cc/64
IP6.GATEWAY:                           fe80::e626:86ff:fe1e:c7c
IP6.ROUTE[1]:                          dst = 2405:201:4003:80cc::/64, nh = ::, mt = 100
IP6.DNS[1]:                            2405:201:4003:80cc::c0a8:1d01
```

## 我在 Linux 上如何处理 DNS？

如果你是系统管理员，或者任何负责家庭办公室或小型企业 Linux 系统的人员，你必须了解 Linux 系统上的 DNS 设置（即使在你的 Windows 系统上也是如此）。

它是一种翻译协议，将你的域名（如`www.foo.com`）翻译为 IP 地址。

要检查你的系统配置是否正确，这里有一些对你很有用的 DNS 故障排除命令。

`host`命令将`www.yahoo.com`翻译为对应的 IP 地址，具体取决于我的地区。

```bash
$ host www.yahoo.com
```

预期的结果是：

```bash
$ host www.yahoo.com
```

`www.yahoo.com`是`new-fp-shed.wg1.b.yahoo.com`的别名。

`new-fp-shed.wg1.b.yahoo.com`有地址`202.165.107.50`。

`new-fp-shed.wg1.b.yahoo.com`有地址`202.165.107.49`。

`new-fp-shed.wg1.b.yahoo.com`有 IPv6 地址`2406:2000:e4:1605::9001`。

`new-fp-shed.wg1.b.yahoo.com`有 IPv6 地址`2406:2000:e4:1605::9000`。

如果存在 DNS 问题，预期的结果是连接超时；无法访问服务器。

要检查你的系统上有哪些 DNS 服务器，你需要查看`/etc/resolv.conf`的内容：在我的情况下，它是`192.168.29.1`，这是提供 DNS 服务的宽带调制器的 IP 地址。

```bash
$ cat /etc/resolv.conf
```

```text
Generated by NetworkManager
nameserver 192.168.29.1
nameserver 2405:201:4003:80cc::c0a8:1d01
```

要检查你拥有的接口，需要使用 Network Manager：

```bash
$ nmcli con show
```

```text
NAME    UUID                                     TYPE               DEVICE
enp0s3                                        enp0s3
```

我们有一个以太网接口，另一个由虚拟机软件创建的桥接接口。

要查看每个接口的 DNS 设置，请使用命令：

```bash
$ nmcli -f ipv4.dns con show enp0s3
```

```bash
$ nmcli -f ipv4.dns con show virbr0
```

我们可以看到没有任何接口有任何 DNS 设置。要使用 DSL 服务器的 DNS 服务，请遵循以下步骤：

1. 以 root 身份登录。
2. 但请使用`sudo`。

```bash
# nmcli con mod "enp0s3" ipv4.dns "192.168.29.1"
```

检查接口`enp0s3`的 DNS 设置。

```bash
# nmcli -f ipv4.dns con show enp0s3
```

```text
ipv4.dns:     192.168.29.1
```

重启服务使用命令：

```bash
# nmcli con up "enp0s3"
```

## 我如何监控网络访问？

你需要监控两个节点之间的网络流量。在 COVID 时代，由于都在使用 VPN，这比你想象的要常见。如果你在家里工作并受到应用程序响应缓慢的困扰（特别是那些依赖 TCP/IP 客户端/服务器方法的应用程序）。

考虑系统 A 为 CentOS 7，系统 B 为 CentOS 8。我们将使用`nc`命令通过 TCP 端口`5000`发送流量（你也可以使用系统的其他 TCP 端口）。监控工具`iptraf`会为你捕获流量以便分析。在两个服务器上安装`iptraf-ng`和`nc`：

```bash
# yum install iptraf-ng nc
```

```text
Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from [192.168.29.32:51294] to [192.168.29.182:5000] ; FIN sent; 5 packets, 295 bytes, avg flow rate 0.06 kbps

Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from [192.168.29.182:5000] to [192.168.29.32:51294] ; FIN acknowleged

Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from [192.168.29.182:5000] to [192.168.29.32:51294] ; FIN sent; 5 packets, 278 bytes, avg flow rate 0.06 kbps

Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from [192.168.29.32:51294] to [192.168.29.182:5000] ; FIN acknowleged
```

## 如何在 Linux 上操作文本文件？

文本文件是一个 ASCII 文件。要识别文本文件，你需要使用`file`命令。

例如：

```bash
file hosts
```

```text
hosts: ASCII text
```

现在，考虑`fox.txt`文件，其包含以下内容：

```bash
$ cat fox.txt
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
```

如果你想将单词`lazy`替换为`clever`，可以使用`sed`命令来实现。

```bash
$ sed -i 's/lazy/clever/g' fox.txt
$ cat fox.txt
The quick brown fox jumps over the clever dog
The quick brown fox jumps over the clever dog
The quick brown fox jumps over the clever dog
The quick brown fox jumps over the clever dog
The quick brown fox jumps over the clever dog
```



其中`-i`代表原地替换（in-place replacement），`s`代表替换（substitution），`g`代表`lazy`的全局存在（global existence）。

## 你能提供一个正则表达式的示例吗？

正则表达式用于 Shell 和编程层面，以匹配未知的字符/字符串。这是一个复杂的课题，你必须学习更多的书籍来理解它。

`^`表示行开头的模式，例如它可以如下所示使用：

```bash
# grep ^refresh_pattern squid.conf
```

```text
refresh_pattern ^ftp:           1440    20%     10080
refresh_pattern ^gopher:        1440    0%      1440
refresh_pattern -i (/cgi-bin/|\?) 0       0%      0
refresh_pattern .               0       20%     4320
```

`$`表示行尾的模式，`grep`命令找到所有行尾的`http`实例。

```bash
# grep http$ squid.conf
```

```text
acl Safe_ports port 80          # http
acl Safe_ports port 488         # gss-http
acl Safe_ports port 777         # multiling http
```

## 如何在 Linux 上设置静态 IP 地址？

你需要的第一步是使用以下命令识别你正在使用的接口：

```bash
$ nmcli c
```

```text
NAME    UUID                               TYPE      DEVICE
enp0s3  7b1642d8-22e4-46f9-8f9d-c1b6d3c5bd42 ethernet enp0s3
vir0    c9e04188-1c13-402e-9d0b-e0571725264 bridge vir0
```

接口名称是`enp0s3`。让我们通过命令查看更多关于`enp0s3`的信息：

```bash
$ nmcli d show enp0s3
```

```text
GENERAL.DEVICE:     enp0s3
GENERAL.TYPE:       ethernet
GENERAL.HWADDR:     08:00:27:92:4E:C
GENERAL.MTU:        1500
GENERAL.STATE:      100 (connected)
GENERAL.CONNECTION:  enp0s3
GENERAL.CON-PATH:   /org/freedesktop/NetworkManager/Active
WIRED-PROPERTIES.CARRIER: on
IP4.ADDRESS[1]:     192.168.29.32/24
IP4.GATEWAY:        192.168.29.1
IP4.ROUTE[1]:       dst = 0.0.0.0/0, nh = 192.168.29.1, mt
IP4.ROUTE[2]:       dst = 192.168.29.0/24, nh = 0.0.0.0, mt
IP4.DNS[1]:        192.168.29.1
IP6.ADDRESS[1]:     2405:201:4003:80cc:9c47:139c:3724:4bf/64
IP6.ADDRESS[2]:     fe80::fd7c:3d3f:2a54:d54f/64
IP6.GATEWAY:        fe80::e626:86ff:fe1e:c77c
IP6.ROUTE[1]:       dst = 2405:201:4003:80cc::64, nh = ::
IP6.ROUTE[2]:       dst = ::/0, nh = fe80::e626:86ff:fe1e:c77c
IP6.ROUTE[3]:       dst = ff00/8, nh = ::, mt = 256
IP6.DNS[1]:        2405:201:4003:80cc::0a8:1d1
```

不是从 DHCP 获取 IP 地址，而是手动设置，我们拥有通过上述命令设置静态 IP 信息：

```text
IP4.ADDRESS[1]:     192.168.29.32/24
IP4.GATEWAY:        192.168.29.1
IP4.DNS[1]:        192.168.29.1
```

以 root 身份登录或使用`sudo`并输入以下命令：

```bash
# nmcli mod enp0s3 ipv4.method manual ipv4.addresses 192.168.29.32/24 ipv4.gateway 192.168.29.1 ipv4.dns 192.168.29.1
```

现在，我们可以使用以下命令确认设置已完成：

```bash
# nmcli c show enp0s3 | grep ipv4
```

```text
ipv4.method:           manual
ipv4.dns:              192.168.29.1
ipv4.dns-search:       --
ipv4.dns-options:      --
ipv4.dns-priority:      0
ipv4.addresses:         192.168.29.32/24
ipv4.gateway:          192.168.29.1
ipv4.routes:            --
ipv4.route-metric:      -1
ipv4.route-table:       0 (unspec)
ipv4.routing-rules:     --
ipv4.auto-routes:       --
ipv4.auto-dns:         --
ipv4.auto-method:      --
ipv4.auto-config:     --
ipv4.ignore-route:      --
ipv4.ignore-dns:       --
ipv4.ignore-method:    --
ipv4.ignore-config:    --
```

Nov 19 19:46:31 lx-centos8 firewalld[162379]: WARNING: AllowZoneDrifting is ena>

检查防火墙设置的命令，输入以下命令：

```bash
firewall-cmd --list-all
```

public (active)

  target: default

  icmp-block-inversion: no

  interfaces: enp0s3

  sources:

  services: cockpit dhcpv6-client ssh

  ports:

  protocols:

  masquerade: no

  forward-ports:

  source-ports:

  icmp-blocks:

  rich rules:

firewalld 拥有多个`ZONES`（区域），此信息涉及`PUBLIC`区域。我们看到 DHCP 客户端和`ssh`都在允许的服务之中。

## 如何检查我的 Linux 机器上的本地解析？

本地解析是指启用主机名/域名翻译为 IP 地址的功能。为了实现这一点，我们需要检查`/etc/nssswitch.conf`文件，并确保你中已包含以下条目：

```
hosts: files dns myhostname
```

这意味着解析将通过你的`/etc/hosts`文件进行。让我们打开`/etc/hosts`文件并添加条目：

```
192.168.29.32 www.lx-centos8.com
```

如果解析完成，执行 ping 测试：

```bash
ping www.lx-centos8.com
```

```
PING www.lx-centos8.com (192.168.29.32) 56(84) bytes of data.
64 bytes from www.lx-centos8.com (192.168.29.32): icmp_seq=1 ttl=64 time=0.036 ms
64 bytes from www.lx-centos8.com (192.168.29.32): icmp_seq=2 ttl=64 time=0.052 ms
64 bytes from www.lx-centos8.com (192.168.29.32): icmp_seq=3 ttl=64 time=0.039 ms
```
