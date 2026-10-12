
`useradd` 命令默认为用户创建一个家目录（`/home/john`）。要查看用户的属性，检查：

```bash
# cat /etc/passwd
```

如果你想修改用户的属性，使用 `usermod` 命令。这是一个示例：

```bash
# usermod -l newname oldname
```

如果你想删除一个用户，使用 `userdel` 命令。这是一个示例：

```bash
# userdel -r john
```

## 限制磁盘空间

如果你正在管理一台多用户机器（许多人都有登录账户），你还需要执行一些额外的任务。要限制用户可以使用的磁盘空间，使用：

```bash
# quota -u john /home/john
```

## 网络服务

如果你正在管理一台多用户机器（许多人都有登录账户），你还需要执行一些额外的任务。以下章节描述了你可能想要开启的网络服务：

### 启用安全壳 (ssh) 服务

当你管理一台多用户机器（许多人都有登录账户），你还需要执行一些额外的任务。他们开启的第一服务之一是安全壳 (`ssh`)。安装 Linux 系统后，`ssh` 服务通常是开启的。输入 `ps -ef | grep ssh` 查看守护进程是否正在运行。如果没有，你可以通过以下方式启动服务：

```bash
# /etc/init.d/sshd start
# chkconfig ssh
```

当 `ssh` 服务运行时，你可以登录到：这是一个示例：

```bash
$ ssh john@example.com
The authenticity of host 'example.net (10.0.0.1)' can't be established.
RSA key fingerprint is 8b:21:08:e7:41:c0:d9:b2:93:w1:af:fe:da2. Are you sure you want to continue connecting (yes/no)? yes
john@example.com password: *******
[john]
```

在这个示例中，你以用户 `john` 的身份登录到名为 `example.com` 的主机。一旦登录，你就可以像登录 shell 一样使用命令。因为是安全壳，所有事务都是加密的，因此窃听线路看不到你在做什么。你甚至可以直接以 `root` 身份登录，尽管良好的做法是以不同的用户登录并在需要时使用 `root`。

`scp` 是另一个你可以与运行 `ssh` 守护进程的计算机通信的命令。通过 `scp`，你可以在网上安全地传输文件。这里是一个 `scp` 命令的示例：

```bash
$ scp -r /home/chris/gallery/ chris@server:/home/chris/
chris's password: *******
```

刚刚显示的命令行递归 (`-r`) 将 `gallery` 目录的所有内容（及其所有子目录）复制到名为 `chris` 的机器上的 `/home/chris` 目录。这是在不同机器之间传递文件的一种方便且安全的方法。

如果你在 `ssh` 服务器上使用了防火墙，并且无法登录（使用 `ssh`）到该计算机，请确保端口 `22` 是可用的。否则，机器将不会允许另一台计算机请求 `ssh` 服务。

![](img/1b8a24a162893627b8005ac678b79236_377_0.png)

### 启用其他网络服务

其他的网络协议对于你的 Linux Toys 项目与局域网（LAN）其他机器之间交换信息有用。特别是，你应该考虑启用 `Samba` 服务（用于与局域网内的 Windows 系统共享文件和打印机）、`FTP` 服务（用于在你的 Linux Toys 机器之间传输文件）、`NFS`（用于在 Linux 和 UNIX 系统之间共享文件）以及 Web 服务（能够与网络上的其他人共享 Web 内容）。

## 总结

精通 Linux 需要花费大量的时间和努力。本附录旨在为你提供有效运行和使用 Linux 系统所需的一些基础知识。尽管本附录应该是学习 Linux 的良好起点，但你可能需要考虑一本更完整的参考书（如《红帽 Fedora 和企业 Linux 4 圣经》），以便深入探讨此处讨论的话题。

### 安装 Linux

在开始本书中的任何项目之前，你应该已经有一个安装好的 Linux 系统可以进行工作。即使是那些无需在硬盘上安装 Linux 即可运行的项目（如 `eMovieX` 和 `Linux Server` 项目），也需要你有一个运行中的 Linux 系统来设置它们。

这些项目是在 `Fedora Core 4` 上测试的，这是由红帽公司赞助的免费操作系统（第 4 章中的 `MythTV` 项目除外，建议使用 `Fedora Core 3`）。你也可以对这两个系统都使用 `Red Hat Core`，你可以为每个项目安装随书附带的 `RPM`。

本附录描述了你可能想要作为 Linux Toys 项目基础的几种 Linux 发行版。我建议使用 `Fedora Core` 来构建大多数 Linux Toys 项目，我也在附录中包含了对 `Fedora Core` 安装过程的完整描述。

> 注意：一旦你安装了 Linux 系统，请参阅附录 A，获取有关如何从书中附带的光盘中的软件安装 Linux Toys 项目的信息。这包括安装 `RPM` (`*, .rpm`) 格式和压缩 `TAR` (`*.tar.gz`) 格式的包。

### 选择不同的 Linux 发行版

如果你想使用 `Fedora Core` 或 `RHEL` 以外的 Linux 发行版来安装你的项目，你可以随意为。你可能已经安装了 Linux 系统，在这种情况下，你可以直接进入你想要尝试的项目。然而，如果你感兴趣为 Linux Toys II 安装不同的 Linux 发行版，这里有几个地方可以去选择：

### 本附录中的附录

![](img/1b8a24a162893627b8005ac678b79236_379_0.png)

- 选择 Linux 发行版
- 安装 Fedora Core Linux
- 运行 Fedora Setup Agent
- 安装后的后续操作

## 356 第五部分 — 附录

- **`Linux` 之书，2005年版** —— 本书（由作者编写）在光盘和 DVD 上包含了十种不同的 Linux 发行版。它还包含了如何选择和安装其中的描述。
- **`Debian GNU/Linux`** —— 要获取 `Debian`，请参阅 Debian 页面 (`www.debian.org/distrib`)。要安装 `Debian`，请查看安装手册 (`www.debian.org/releases/stable/installmanual`)。
- **`Slack`** —— 有关获取 `Slack` 的信息，请参阅 Get Slack 页面 (`www.slack.com/getslack`)。要安装 `Slack`，请参阅 Slack 安装帮助页面 (`www.slack.com/install`)。
- **`Gentoo`** —— 要找到 `Gentoo Linux` 下载地址，请参阅 Gentoo 镜像页面 (`www.gentoo.org/main/mirrors.xml`)。有关安装 `Gentoo` 的信息，请访问 Gentoo 文档资源页面 (`www.gentool.org/doc/en?cat=install`)。
- **`SUSE`** —— 要获取 `SUSE Linux`，访问 SUSE Linux 专业下载页面 (`www.novell.com/products/linuxprofessionals/downloads`)。需要安装帮助，请参阅 SUSE 论坛（在 `www.suseforums.net` 中选择 `Install/Boot`）。

当我们用 `Linux Toys II` 测试了所有这些发行版时，许多项目只需通过安装 `Linux Toys II` 光盘中包含的 `tar` 包即可直接运行。这些大部分项目都是由项目开发者自己创建的。因此，通常它们可以在不经修改的情况下运行在其他 Linux 系统上。你应该检查该项目的网站是否有专门为你的使用而封装的软件，例如用于 `Debian` 的 `.deb` 包，或者用于 `Gentoo` 的可以通过 `emerge` 安装的树目录包。

如果你选择使用 `Fedora` 或红帽企业 Linux (`RHEL`)，你可以遵循本附录包含的安装程序。本附录中的大部分描述都取自《红帽 Fedora 和企业 Linux 4 圣经》。通过获得那本书，你将拥有用于安装 `Fedora Core 4` 的媒体（包括 DVD 和光盘）。

### 安装 Fedora Core 4

本章详细介绍了如何从 DVD 或光盘集安装 `Fedora 4`。本章中还提到了从硬盘或通过网络安装 `Fedora 4` 的其他方法。

#### 选择安装方法

`Fedora` 提供了几种灵活的安装操作系统的方法。如前所述，你可以从《红帽 Fedora 和企业 Linux 4 圣经》中获取媒体。或者，你可以通过从互联网下载这些光盘的磁盘镜像获取 `Fedora Core 4` DVD 或四光盘安装版，并自己刻录到光中。访问 `http://fedora.redhat.com` 获取下载信息。

#### 附录 C — 安装 Linux 357

#### 安装其他红帽 Linux 系统
