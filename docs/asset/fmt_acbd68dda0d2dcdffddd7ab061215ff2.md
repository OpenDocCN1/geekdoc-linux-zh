
## 它的工作原理是

它的工作原理是：客户端将 `NetBIOS` 和 `IP` 地址发送到 `NBNS` 服务器，服务器将这些信息存储在一个简单的数据库中。当客户端想要与另一个客户端通信时，它会将另一个客户端的名称发送到 `NBNS` 服务器。如果名称在列表中，`NBNS` 就会返回 `IP` 地址。你拿到了，查查号码。

不同子网的客户端可以共享同一个 `NBNS` 服务器，因此与广播不同，点对点机制局限于本地局域网。`NBNS` 在任何方面与 `DNS` 相似，但它是完全动态的，并且缺乏足够的控制手段来确保只有授权的客户端才能注册名称。冲突可能会发生，而且很容易发生。

### 最后是浏览

这是一个“非常棘手的问题”，但 `Samba` 的 `nmbd` 会处理它。它不是我们熟悉并喜爱的网页浏览，而是网络上计算机提供的服务（文件和打印共享）的浏览列表。

在局域网上，参与的计算机将举行选举，以决定其中哪一个成为主浏览器。它不是我们熟悉并喜爱的网页浏览，而是网络上计算机提供的服务（文件和打印共享）的浏览列表。

### Samba 2.0 里程碑

`Samba` 2.0 发布于 1999 年 1 月。2.0 版本的一个非常重大且酷的功能之一是速度的提升。`Ziff-Dev Publishing` 使用他们的 `Netbench` 软件对 Linux 上的 `Samba` 2.0 和 `Windows NT` 进行了测试。他们在相同的 PC 硬件上运行了所有测试，结果显示 `Samba` 的负载吞吐量至少是 `NT` 的两倍。`Samba` 包含在所有主要的 Linux 发行版中，`Ziff-Dev` 测试了其中三个。

另一个里程碑是 `Silicon Graphics` (`SGI`) 成为第一个支持 `Samba` 的商业 UNIX 供应商。在 1998 年 12 月的新闻稿中，他们声称运行 `Samba` 2.0 的 `Origin` 系列服务器是目前适用于 `Windows` 客户端的最强大的服务器系列。`SGI` 现在为 `Samba` 提供商业支持，许多其他供应商也列在网站上。

## 39.1. Samba 简介

### 39. smbd - Samba NT 服务器

当然，仍然可以通过 `comp.protocols.smb` 新闻组和 `samba@samba.org` 邮件列表获取互联网支持。

`Samba` 团队继续致力于开发各种新功能。目前的关注点包括 `NT ACLs`（访问控制列表）、对 `LDAP`（轻量级目录访问协议）的支持、`NT` 域控制以及微软的 `DFS`（分布式文件系统）。

## 未来

`Windows 2000` 迫在眉睫，像一只懒惰的动物从洞穴边缘探出头，试图决定是否要出来。没有人确切知道它出现时会是什么种动物，但人们非常确定它会有牙。

由于微软在桌面端占据主导地位，它决定了 `CIFS` 的增长方向。像之前的各个主要操作系统版本发布一样，通过测试版本以及微软拥有的资源，有一些值得关注的现象：

- **带有 NetBIOS 的 CIFS**：微软将尝试将 `CIFS` 和 `NetBIOS` 解耦。`NetBIOS` 不会消失，但你的 `CIFS` 网络也将需要它。`SMB` 协议将简单地封装在 `TCP/IP` 之上。通过 `DNS` 进行名称查找。
- **动态 DNS**：动态 `DNS` 将实现动态 `DNS`，这是一个由 `IETF`（互联网工程任务组）设计的、仍在进化中的系统。动态 `DNS` 允许动态地向 `DNS` 服务器添加名称。
- **活动目录（Active Directory）**：活动目录似乎是 `Windows 2000` 网络的核心。可能是旧的 `NetBIOS` 可能会在活动目录中注册它们的名称。
- **分级 NT 域**：`NT` 域系统将从孤立的域控制器变为分级。命名系统将变为与 `DNS` 极其相似的系统。

可以确定的是，`W2K`（通常如此被称为）并且将受到严密监控。`Windows` 已经引起了互联网仙境中更有好奇心的居民的关注，包括安全分析师、标准小组、破解者聚集以及普通的全能极客。已经尝到开源软件自由之美的商业世界可能对所有权、单供应商解决方案的世界感到抵触。代码掌握在手中既有回报又能赋权。

无论下一个 `Windows` 像什么样，帮助它在多样的互联网世界中与其同行共处将是 `Samba` 的任务。`Samba` 团队作为互联网社区的缩影，是观察 `W2K` 如何发展的群体之一。尽管在等待与 `Samba` 并行进行，但 `Samba` 是一项持续且开放的努力。访问 `Samba` 网站，加入邮件列表，看看正在发生什么。

参与未来。

## 39.2 配置 Samba

尽管如此，配置 `smbd` 实际上非常简单。典型的局域网需要一台可以向 `Windows` 客户端共享 `/home/*` 目录的 UNIX 机器，每个用户可以使用其家目录名称作为登录名。它还必须作为一个通过 `lpr` 打印的打印共享；然后以我们喜欢的 `PostScript` 方式打印。考虑本地局域网 `192.168.3.0/24` 上的 `Windows` 机器 `divinian.cranzgot.co.za`。该机器的用户将在服务器上以 UNIX 登录 `psheer` 证书。

`Samba` 配置文件的常规位置在所有发行版中都是 `/etc/samba/smbd.conf`。一个执行上述功能的极简配置文件可能是：

```
[global]
workgroup = MYGROUP
server string = Samba Server
hosts allow = 192.168.127.
printcap name = /etc/printcap
load printers = yes
printing = bsd
log file = /var/log/samba/%m.log
max log size = 0
security = user
sock-opt options = TCP_NODELAY SO_RCBUF=8192 SO_SNDBUF=8192
enncrypt passwords = yes
smb passwd file = /etc/samba/smbpasswd
[homes]
comment = Home Directories
browsable = no
writable = yes
[printers]
comment = All Printers
path = /var/spool/samba
browsable = no
guest ok = no
printable = yes
```

`SMB` 协议存储密码的方式与 UNIX 不同。因此，它需要自己的密码文件，通常为 `/etc/samba/smbpasswd`。在 `/etc/samba/smbusers` 中也有 UNIX 登录与 `Samba` 登录之间的映射，但为了简单起见，我们将使用相同的 UNIX 名称作为 `Samba` 登录名。我们可以通过以下命令添加新的 UNIX 用户并设置密码：

```
adduser psheer
smbpasswd psheer
```

### 39.2. 配置 Samba

注意，`SMB` 在大小写解释方面存在各种问题——输入错误的密码在 `Samba` 中可能仍然有效，但在 UNIX 中则不会。要启动 `Samba`，运行熟悉的：
