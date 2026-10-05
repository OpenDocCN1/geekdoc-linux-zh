
现在测试一下：

```
# /usr/local/atalk/bin/pap -p "LaserWriter 16/600
PS":LaserWriter@biology product.ps
```

如果你是向你所在区域的打印机打印，可以不写名称。

假设一切运行正常，文档应该会打印出来。现在你可以继续设置 `/etc/printcap`。这里有一个示例条目：

```
lp|NetworkWriter|LaserWriter 16/600 PS:\n:sd=/usr/spool/laserwriter:\
:lp=/dev/null:\
:pl#63:\
:pw#85:\
:mx#0:\
:sh:\
:sf:\
:lf=/usr/adm/lpd-errors:\n:if=/usr/local/atalk/etc/filters/ifpap:\n:of=/usr/local/atalk/etc/filters/ofpap:
```

（此处，抱歉）

关于设置远程和本地 AppleTalk 打印机的更多信息，请访问 http://www.giub.unibe.ch/~eugster/appleprint.html。

## 5.5 网络信息服务 (NIS)

网络信息服务 (NIS) 是一组用于从主服务器管理用户各种网络服务的程序。最近，NIS 的增强版本 NIS+ 更安全，在大规模网络中运行更好，但设置起来更复杂。

NIS 最初被称为“黄页”（Yellow Pages）。然而，黄页是英国电信的注册商标，因此更改了名称。原始名称的遗产仍然存在，大多数与 NIS 相关的程序都以 "yp" 开头。

NIS 将信息存储在根于 `/var/yp/` 的目录和 GDBM（GNU 数据库管理）文件中。NIS 将这些文件称为“映射”（maps）。然后通过 RPC（远程过程调用）让 NIS 域内的其他机器（与 DNS 域不同！）可以使用这些映射。NIS 还允许从服务器从主服务器获取映射，并在主服务器缓慢或宕机时回答请求，类似于辅助 DNS 服务器的工作方式。

## 5.5 网络信息服务 NIS

NIS 映射由 /etc/ 中常见的各种设置文件构建：passwd、group、hosts、services、aliases 等。没有必要使用每一个映射。只使用密码和组映射，因为大多数其他文件通常很少更改。

NIS 最大的问题之一是广播 NIS 请求带来的安全漏洞——任何人都可以建立一个服务器，该服务器有机会回答这些请求。最近版本的 ybind 允许通过 IP 数或名称指定域服务器。

## NIS 客户端设置

你第一次遇到 NIS 很有可能是作为客户端。将你的 Linux 机器设置为 NIS 客户端相当简单。

首先，你需要知道正在通过 NIS 管理哪些信息。我们假设的是一个相当典型的设置，包含密码、组和主机信息。

你需要将 "nis" 添加到你的 `/etc/host.conf` 中。顺序非常重要。如果你实际上大部分的大部分时间都花在与局域网之外的主机进行通信，你可能希望将 NIS 放在搜索顺序的最后。

在下面的示例中，我们假设 `/etc/passwd` 是非常精简的，包含超级用户、各种守护进程等的条目，但没有更多的用户条目。

要将整个 NIS 密码映射附加到本地 `/etc/passwd` 文件，请使用此行：

```
:+:::::
```

你可以通过添加以 `+` 或 `-` 开头的额外行来自定义访问权限。例如，拒绝用户 "cary" 的访问但允许所有其他用户（至少在他们任何其他 NIS 客户端上的权限范围内），添加以下内容：

```
:+:::::
-cary
```

"+:::::"" 条目不是强制的。此外，你可以使用 "@" 通过组来控制访问权限。此条目：

```
+cary::::
+rachel::::
+@plan9::::
-paul
-entry
```

## 第 5 章 • 与 Linux 联网

允许 "cary"、rachel" 和组 "plan.9" 访问。用户 "paul" 和 "entry"（假设他们在上述组中）被拒绝访问。

还可以覆盖 passwd 映射中的部分信息，或者添加 NIS 中完全不存在的用户。例如，要给 paul 分配 shell `/bin/tcsh` 并更改 Rachel 的家目录（并仅允许他们访问）以及添加用户 surya，可以使用如下条目：

```
++:::
+paul::::/bin/tcsh
+rachel::::/local/home/rachel:
+*:/bin/false
surya:UGj6khgT:506:100:/home/surya:/bin/bash
```

最后，你需要设置 ypcient 程序并设置 NIS 域名。你的发行版可能已经带了 NIS 客户端（和服务器）程序。如果没有，你应该能从任何 Linux 发行版网站获取它们。

设置 NIS 域名是通过运行 `/bin/domain-name nis` 完成的。你还需要确保 portmap 程序正在运行。使用 `rpcinfo` 命令来实现此：

```
[root:/home/cary]# rpcinfo -p localhost
program vers proto port
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
```

如果它不在列表中，运行 `/usr/sbin/portmap`，然后运行 `/usr/sbin/ypbind`。rpcinfo 应该显示类似：

```
[root:/home/cary]# rpcinfo -p localhost
program vers proto port
100000 2 tcp 111 portmapper
100000 2 udp 111 portmapper
100000 2 tcp 631 ybind
100000 2 udp 631 ybind
```

此时，NIS 客户端的设置就完成了。

## nsswitch.conf 文件

nsswitch.conf 决定了查找信息的顺序（这与 `/etc/host.conf` 不同）。

## 5.5 网络信息服务 (NIS)

（此处，抱歉）

设置 NIS 客户端 `/etc/nsswitch.conf` 示例如下：

```
passwd: files nis
group: files nis
hosts: files nis
shadow: files nis
```

## NIS+

NIS+ 是 Sun 对 NIS 的继任者。它更安全并能处理大量的客户端。遗憾的是，Linux 下的 NIS+ 支持仅限于客户端，并且仍处于开发阶段。除非你有真正的 NIS+ 需求，否则使用传统的 NIS。

如果你需要设置 NIS+ 客户端，首先需要几件事。首先是 glibc 2；其次是 NIS+ 客户端程序。如果你运行 Debian 或 RedHat 发行版，你应该已经有了 glibc 2。NIS+ 客户端程序可以在 http://ftp.kernel.org/pub/linux/net/ 找到。你需要两个文件：`nis-tools-1.4.gz` 和 `pam_keylogin-1.1.gz`。解压并编译它们。

假设你的 NIS+ 服务器已设置好回答客户端请求（请参考你的 Solaris 文档了解如何操作），你需要设置 NIS+ 域就像 NIS 一样，然后运行：

```
nisinit -c server
```

## 设置 NIS 主服务器

再次，你的发行版可能已经带了 NIS 服务器程序，或者你可以从 kernel.org 或任何 Linux 发行版网站获取。

如果需要，编译 NIS 软件。然后编辑 `/var/yp/Makefile` 以添加或删除你将提供的映射。

