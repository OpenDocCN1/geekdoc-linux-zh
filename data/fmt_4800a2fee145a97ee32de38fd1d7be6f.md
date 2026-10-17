
```
$ sudo apt-get update
[sudo] password for Christine:
Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
[...
Fetched 1,053 kB in 2s (631 kB/s)
Reading package lists... Done
$ sudo apt-get dist-upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages will be upgraded:
[...
Do you want to continue? [Y/n] V
[...
$
```

如果你空间只够容纳两个 Linux 发行版，CentOS 和 Ubuntu 是很棒的选择。如果你有额外的资源，添加另一个发行版 openSUSE 是值得的。

## 查看 openSUSE

openSUSE 发行版于 1994 年首次发布，当时名为另一个名称 SUSE Linux。有许多公司参与了它的支持，其中总部位于德国的 SUSE 公司是原始公司。

这个发行版拥有非常忠实且稳固的基础。openSUSE 发行版不仅受到社区开发者的强支持，openSUSE 用户也非常喜爱它。它独特且流行的工具之一是 Yet another Setup Tool（另一个设置工具，简称 YaST）。`YaST` 可以被看作一个控制中心工具，允许你从一个界面控制许多系统服务。

你可以从 `https://software.opensuse.org` 获取 openSUSE 发行版 ISO。该发行版有两个主要版本：Leap 和 Tumbleweed。我们推荐你选择 `openSUSE Leap 15.*` 版本。

> openSUSE 社区在 2017 年更改了其发行版的版本命名方案。15.0 之前的版本是 42.3。在获取 openSUSE Leap 时，请注意这一剧烈变化。

一旦你成功安装了 openSUSE，在探索此发行版之前更新所有软件是一个好主意。要通过命令行更新软件，请在终端中使用超级用户权限手动执行列表 1.5 所示的命令。

### 列表 1.5：在 openSUSE 上更新软件

```
$ sudo zypper patch
[sudo] password for root:
Loading repository data...
Reading installed packages...
Resolving package dependencies...
[...
Note: System reboot required.
Continue? [y/n]... shows all options] (y): y
[...
Warning: One of the installed patches requires a reboot of your machine. Reboot as soon as possible.
There are some running programs that might use files deleted by recent upgrade. You may wish to check and
start some of them. Run 'zypper ps'
```

## 查看 Fedora

Fedora 是红帽营中广流行的发行版，但你还需要一个来自 Debian 营的发行版。接下来，我们将探索 Ubuntu 发行版。

## 第2章

## 筛选服务

- 目标 2.5：总结并解释服务器角色。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_70_0.png)

![](img/0c1e7d2699b9d354c8d2f84669d18d73_71_0.png)

虽然 Linux 在进入桌面市场方面进展缓慢，但它在服务器市场蓬勃发展。Linux 服务器托管了许多最大的网站，并为许多家庭和企业网络提供服务。

Linux 服务器的流行在很大程度上归于它们的多功能性、性能和成本。本章将探索 Linux 服务器是如何运行的，并涵盖你可以在 Linux 中安装和运行的最常见的服务器软件包，以便为网络客户端提供服务。

## 什么是 Linux 服务器？

在我们深入研究 Linux 服务器细节之前，将首先解释什么是 Linux 服务器，并展示 Linux 服务器与 Linux 桌面之间的区别。

Linux 桌面版和 Linux 服务器都使用相同的 Linux 内核，运行相同的 shell，甚至具有运行相同程序的能力。区别在于它们主要运行哪些程序以及这些程序在系统上的运行方式。

Linux 桌面版主要关注你从图形用户界面运行的个人程序，例如当你浏览互联网或编辑文档时。图形桌面为用户提供了一个易于与操作系统以及所有文件和程序进行交互的简单界面。你通过从菜单系统中选择或点击桌面图标来启动程序。在桌面世界，一切都是交互式的。

服务器主要在没有人工干预的情况下运行。没有人坐在桌面前启动应用程序（事实上，许多服务器没有专用的显示器和键盘）。

服务器运行为多个用户（客户端）提供共享资源（称为“服务”）的程序，通常在网络环境中运行。许多服务一直运行，即使在没有客户端活动使用它们的情况下。

服务器程序很少在图形用户界面上运行。相反，它们几乎总是利用 Linux shell 的命令行界面 (CLI) 与服务器管理员进行交互，而且管理员通常会从远程客户端连接到服务器，以对服务执行任何交互。

由于与人类操作员的交互很少，服务器必须学会自己启动为客户端提供服务的程序。服务器运行服务的方式可能因服务器和服务的不同而异。以下章节描述了 Linux 服务器如何启动服务以及它们如何为客户端提供访问。

## 启动服务

Linux 服务器运行服务程序有两种主要方式：

- 作为后台进程，始终运行并监听请求
- 作为由父程序生成的进程，由该程序监听请求

当一个 Linux 服务程序作为后台进程持续运行时，它被称为“守护进程”(daemon)。Linux 服务器经常利用脚本在服务器启动时立即启动服务守护进程（参见第 6 章“维护系统启动和服务”）。

Linux 守护进程程序通常以字母 d 结尾，以指示它们是守护进程。列表 2.1 显示了 MySQL 数据库服务器守护进程在服务器后台运行的示例。

### 列表 2.1：MySQL 守护进程示例

```
$ ps ax | grep mysql
5793 7 sl 0:00 /usr/sbin/mysql --daemonize --pid file=/run/mysql/mysqld.pid
5900 pts/0 S+ 0:00 grep --color=auto mysql
$
```

`mysql` 守护进程监听来自客户端的网络连接。当守护进程收到客户端的请求时，它处理该请求并通过相同的网络通道将数据返回给客户端。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_72_0.png)

> 注意：Linux 中运行的后台程序的名称是 "daemon" 而不是经常被混淆的 "demon"。daemon 起源于希腊神话，是在需要时为人类提供帮助的超自然生物。

服务器支持的服务越多，它就必须在后台运行更多的守护进程来等待客户端请求。每个守护进程都需要服务器上的内存资源，即使在它正在监听客户端时也是。虽然今天的服务器有大量的内存可用，但在 Linux 的早期并不总是如此。因此出现了“超级服务器”(super-servers)。

超级服务器是为几种不同的应用程序监听网络连接的程序。当超级服务器收到来自客户端的服务请求时，它会生成相应的服务程序。

最初为 Linux 创建的超级服务器程序是互联网守护进程 (inetd) 应用程序。`inetd` 程序以守护进程的形式运行，监听来自客户端的特定请求，并在需要时启动相应的服务程序。`inetd` 程序使用 `/etc/inetd.conf` 配置文件定义它处理请求的服务。

扩展互联网守护进程 (xinetd) 应用程序是 `inetd` 的高级版本。它也根据客户端请求启动服务程序，但它包含额外的功能，例如访问控制列表 (ACLs)、更高级的日志功能，以及在一天或一周的不同时间设置开启关闭服务的调度功能。

## 监听客户端

标准的 Linux 服务器支持许多服务。通常，单台 Linux 服务器将同时支持多个服务。这意味着多个客户端将向服务器请求多种服务。诀窍在于如何将来自客户端的请求引导到正确的服务。
