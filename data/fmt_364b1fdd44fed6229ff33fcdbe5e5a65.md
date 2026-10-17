
```
kali@kali:~$ ss -antlp | grep apache
LISTEN 0 128 ::: ::: users:(("apache2",pid=1481,fd=4),("apache2",pid=1480,fd=4),("apache2",pid=1479,fd=4),("apache2",pid=1478,fd=4),("apache2",pid=1477,fd=4),("apache2",pid=1476,fd=4),("apache2",pid=1475,fd=4))
```

列表 19 - 使用 `ss grep` 确认 `apache2` 已启动并运行

为了让 `apache` 服务像 SSH 服务一样在开机时启动，我们需要使用 `systemctl` 及其 `enable` 选项显式地启用它：

```
kali@kali:~$ sudo systemctl enable apache2
Synchronizing service apache2.service with SysV script at /lib/systemd/system
Executing: /lib/systemd/system-sys-install enable apache2
```

列表 20 - 使用 `systemctl` 设置 `apache` 在开机时启动

Kali Linux 中的大多数服务的操作方式与 SSH 和 HTTP 相同，都是通过它们的服务或单元脚本运行的。要查看所有可用服务，运行带有 `list-unit-files` 参数的 `systemctl`：

```
kali@kali:~$ systemctl list-unit-files
...
UNIT                                 STATE
proc-sys-fs-binfmt_misc.autounount  static
.mount                             generated
dev-hugepages.mount                 static
dev-mqueue.mount                    static
media-cdrom0.mount                   generated
proc-sys-fs-binfmt_misc.mount      static
run-vmblock-x2fuse.mount            disabled
sys-fs-fuse-connections.mount      static
sys-kernel-config.mount             static
sys-kernel-debug.mount             static
...
```

列表 21 - 显示所有可用服务

有关 Kali Linux 中服务管理的更多信息（包括 `systemctl` 的用法），请参考 Kali 训练网站。

## 2.5.3 练习

（这些练习不需要提交报告）

# 攻击性安全

- 1. 练习启动和停止各种 Kali 服务。
- 2. 启用 SSH 服务在开机时启动。

## 2.6 搜索、安装和删除工具

Kali 镜像包含了渗透测试领域最常用的工具。然而，在 VMware 镜像中将 Kali 仓库中的每一个工具都包含进去是不切实际的。我们需要讨论如何搜索、安装或删除工具。在本节中，我们将探索高级软件包工具 `APT` 工具集以及在对 Kali Linux 系统执行维护操作时非常有用的命令。

`APT` 是一组用于管理 Debian 系系统上的软件包（或应用程序）的工具。由于 Kali 基于 Debian，因此我们可以使用 `APT` 安装和删除应用程序、更新软件包并升级整个系统。`APT` 的魔力之处在于它是一个软件包管理系统，通过递归满足其需求和依赖关系来安装或删除请求的软件包。

### 2.6.1 apt update

`APT` 软件包的信息缓存在本地，以加快任何涉及查询 `APT` 数据库的操作。因此，更新可用软件包列表（包括版本信息、描述等）始终是一个良好的习惯。我们可以通过 `apt update` 命令实现这一点：

```
kali@kali:~$ apt update
Hit: http://archive.kali.org/kali InRelease
Get:2 http://archive.kali.org/kali kali-backports Release [1685 B]
Fetched 1685 B in 1s 1.68 MB/s
Get:2 http://archive.kali.org/kali kali-testing InRelease [1685 B]
Fetched 1685 B in 1s 1.68 MB/s
Get:2 http://archive.kali.org/kali kali-main InRelease [1685 B]
Fetched 1685 B in 1s 1.68 MB/s
Reading package lists lists... Done
Reading dependency tree... Done
All packages are up to date.
```

> 使用 `apt update` 更新软件包列表

### 2.6.2 apt upgrade

在更新软件包数据库后，我们可以使用 `apt upgrade` 命令来升级已安装软件包：

```
kali@kali~$ apt upgrade
Reading package lists... Done
Building dependency tree... Done
0 upgraded, 0 newly installed, 0 to remove.
```

> 使用 `apt upgrade` 升级软件包

### 2.6.3 apt search

为了查看哪些软件包可用，可以使用 `apt search` 命令，它会显示可以升级的软件包：

```
kali@kali~$ apt search apache2
apache2/kali-main 2.4.52-1 all64 Apache web server
apache2-bin/kali-main 2.4.52-1 all64 The Apache web server binary
apache2-data/kali-main 2.4.52-1 all64 Apache web server data files
apache2-doc/kali-main 2.4.52-1 all64 The Apache web server documentation
apache2-icu/kali-main 2.4.52-1 all64 The Apache web server with ICU support
apache2-utils/kali-main 2.4.52-1 all64 The Apache web server utilities
apache2-mod-php/kali-main 8.2.12-1 all64 The Apache module for PHP
apache2-mod-php-fpm/kali-main 8.2.12-1 all64 The Apache module for PHP FPM
```

> 使用 `apt search` 搜索软件包

### 2.6.4 apt install

`apt install` 命令可以用于在系统中安装新软件包：

```
kali@kali~$ sudo apt install apache2
Reading package lists... Done
Building dependency tree... Done
The following NEW packages will be installed:
apache2 apache2-bin apache2-data apache2-doc apache2-icu apache2-utils libapache2-bin-2 common-apache2
7 newly installed, 0 upgraded, 0 to remove.
After this operation, 4.2 MB of disk space will be used.
Get:1 http://archive.kali.org/kali kali-main apache2 2.4.52-1 [155 KB]
Get:2 http://archive.kali.org/kali kali-main apache2-bin 2.4.52-1 [110 KB]
Get:3 http://archive.kali.org/kali kali-main apache2-data 2.4.52-1 [350 KB]
Get:4 http://archive.kali.org/kali kali-main apache2-doc 2.4.52-1 [2.10 MB]
Get:5 http://archive.kali.org/kali kali-main apache2-icu 2.4.52-1 [85 KB]
Get:6 http://archive.kali.org/kali kali-main apache2-utils 2.4.52-1 [120 KB]
Get:7 http://archive.kali.org/kali kali-main common-apache2 2.4.52-1 [150 KB]
Fetched 4.2 MB in 1s 4.2 MB/s
Selecting previously selected...
The following packages will be unpacked:
  apache2 (2.4.52-1)
  apache2-bin (2.4.52-1)
  apache2-data (2.4.52-1)
  apache2-doc (2.4.52-1)
  apache2-icu (2.4.52-1)
  apache2-utils (2.4.52-1)
  common-apache2 (2.4.52-1)
Unpacking apache2 (2.4.52-1)...
Unpacking apache2-bin (2.4.52-1)...
Unpacking apache2-data (2.4.52-1)...
Unpacking apache2-doc (2.4.52-1)...
Unpacking apache2-icu (2.4.52-1)...
Unpacking apache2-utils (2.4.52-1)...
Unpacking common-apache2 (2.4.52-1)...
Setting up common-apache2 (2.4.52-1)...
Setting up apache2-data (2.4.52-1)...
Setting up apache2-icu (2.4.52-1)...
Setting up apache2-utils (2.4.52-1)...
Setting up apache2-bin (2.4.52-1)...
Setting up apache2 (2.4.52-1)...
Setting up apache2-doc (2.4.52-1)...
```

> 使用 `apt install` 安装软件包

### 2.6.5 apt remove --purge

同样，我们可以使用 `apt remove --purge` 命令来删除软件包。注意的是，使用 `apt remove` 软件包会删除数据，但会留下通常（修改过的）用户配置文件以防误删。使用 `purge` 选项可以移除所有残留文件：

```
kali@kali~$ sudo apt remove --purge apache2
Reading package lists...
Building dependency tree...
Reading state information... Done
The following packages will be REMOVED:
  apache2
0 upgraded, 0 newly installed, 1 to remove.
After this operation, 581 KB disk space will be freed.
Do you want to continue? [Y/n
(Reading database 388024 files and directories currently installed)
Removing apache2 (2.4.52-1)...
Purging configuration files for apache2 (2.4.52-1)...
Processing triggers for systemd (240-6) ...
```

> 使用 `apt remove --purge` 彻底移除软件包

# 攻击性安全

太棒了！现在可以在 Kali Linux 中搜索、安装和删除工具了。让我们探索本模块中的一个命令：`dpkg`。

## 2.6 dpkg

`dpkg` 是用于安装软件包的核心工具，可以直接安装或间接通过 `APT` 安装。它也是离线操作时的首选工具，因为它不需要互联网连接。注意，`dpkg` 不会安装软件包所需的任何依赖项。要使用 `dpkg` 安装软件包，请提供 `-i` 或 `--install` 选项以及 `deb` 包文件的路径。这假设软件包的 `deb` 文件已经通过某种其他方式被下载或安装。

```
kali~$ sudo dpkg -i man-db-2.7.0.2-5_amd64.deb
(Reading database) ... 86425 files and directories installed. ...
Preparing to unpack man-db-2.7.0.2-5_amd64.deb ...
Unpacking man-db (2.7.0.2-5) over (2.7.0-4) ...
Setting up man-db (2.7.0.2-5) ...
Updating database of manual pages ...
Processing triggers for mime-support (3.58) ...
```

| 列表 27 - 使用 `dpkg -i` 安装 `man-db` |

### 2.6.1 练习题

（报告并非你 Kali 虚拟机的快照（可选））。

- 1. 为你的 Kali 虚拟机创建一个快照。
- 2. 搜索一个 Kali 中未安装的工具。
- 3. 安装该工具。
- 4. 该工具。
- 5. 将 Kali 虚拟机恢复到之前拍摄的快照（可选）。

## 2.7 总结

在本模块中，我们为接下来的模块奠定了基础。我们探索了新用户的技巧和窍门，并回顾了一些更高级用户可能会青睐的标准。

鼓励所有学生查看 Kali Training 网站上的免费在线培训。该网站包括《Kali Linux Revealed》书籍、旨在测试你理解能力的练习题、专门的支持论坛等等内容。这些免费资源为所有技能水平的用户提供了宝贵的见解，并作为本课程所提供培训的绝佳伙伴。

> 46 (Offensive Security, 2019), https://kali.training

## 3. 命令行行的乐趣

在本模块中，我们将简要介绍几个流行的 Linux 命令行程序。可以随时参考 Kali Linux 培训网站进行复习或进行更深入的讨论。

## 3.1 Bash 环境

`Bash` 是一个与 `sh` 兼容 shell，允许我们从终端窗口运行复杂的命令并执行不同的任务。它结合了 KornShell 和 C shell (`csh`) 的一些有用功能。

### 3.1.1 环境变量

当打开终端窗口时，会初始化一个新的 `Bash` 进程，该进程有自己的环境变量。这些变量是全局存储的形式，用于存储会话期间运行的应用程序所继承的各种设置。最常引用的环境变量之一是 `PATH`，它是一个由冒号分隔的目录路径列表，每当在没有完整路径运行命令时，`Bash` 都会搜索这些路径。

我们可以使用 `echo` 命令后跟 `$` 符号和环境变量名称来查看给定环境变量的内容。例如，让我们来看 `PATH` 环境变量的内容。

```
kali@kali:- echo $PATH
/usr/local/bin:/usr/bin:/usr/sbin:/bin:/sbin
```

> 列表 29 - 使用 `echo` 显示 `PATH` 环境变量

其他一些环境变量包括 `USER`、`PWD` 和 `HOME`，它们分别持有当前用户用户名、当前工作目录和主目录的值。

```
kali@kali:- echo $USER
kali
kali@kali:- echo $PWD
/home/kali
kali@kali:- echo $HOME
/home/kali
```

> 列表 29 - 使用 `echo` 显示 `USER`, `PWD` 和 `HOME` 环境变量

可以使用 `export` 命令定义环境变量。例如，如果我们正在扫描目标且不想重复输入系统的 IP 地址，可以快速为其赋值并使用：

```
kali@kali:-$ export b=10.11
```

```
kali@kali:-$ ping -c 3 b
PING 10.11 (10.11) 56(84) bytes of
64 bytes from 10.11: icmp_seq=1 ttl=62 time=23 ms
64 bytes from 10.11: icmp_seq=2 ttl=62 time=23 ms
64 bytes from 10.11: icmp_seq=3 ttl=62 time=56 ms

---
---
3 packets transmitted, 3 received, 0% packet loss, time 102ms
rtt min/avg/max/mdev = 23/34.0/56.0/16.5 ms
```
