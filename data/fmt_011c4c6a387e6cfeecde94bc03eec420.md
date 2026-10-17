
如果这个 `qemu` 进程没有运行，你就无法使用某项功能。现在我们将看看如何使用它。我们将查看幻灯片并尝试理解让成功运行所需的参数。我们需要一个用户名，然后是服务器 IP。对于 CFP Mali 的东西也是一样。我们需要一个额外的文件或文件夹。如果你正在为 `fuller` 进行通信，我们需要传递 `-r` 后面跟文件夹名。现在我们将进入 `0 1 2` 并查看如何操作。由于我们没有任何外部 SSL 服务器，我们将在本地尝试所有这些命令。`127.0.0.1` 是你的本地 IP 地址，你可以进入控制台。这里我们在想这是否在运行。为此，我们需要提供，因为 SSL 调查正在运行，为了验证这一点，将退出此项并在 `sudo` 下作为 EDC 在每个点，然后设置并停止。现在我们的服务器已停止。我们无法再次访问连接到它的主机。现在看，你遇到了像这样的错误，是因为我们的服务器没有正常工作。`copy` 也是如此。来，首先我们需要启动。真的，首先我们需要启动。

```bash
qemu@qemu-VirtualBox:~/rpi/ubuntu-rpi3$ sudo apt-get install openssh-server
qemu@qemu-VirtualBox:~/rpi/ubuntu-rpi3$ sudo apt-get install openssh-server
读取软件包列表... 完成
读取状态信息... 完成
以下软件包已自动安装，但不再需要了：
linux-headers-4.15.0-29-linux-headers-4.15.0-29-generic linux-4.15.0-29-generic linux-modules-4.15.0-29-generic
以下软件包将被移除：
使用 `sudo apt autoremove` 来删除它们。
sh-ahk risk mully-guard monkeyskeysher
新请求的软件包将安装：
0 个升级，1 个新安装，0 个移除，2 个未升级。
在此操作后，将使用 904 KB 的磁盘空间。
Get:1 http://archive.ubuntu.com/ubuntu bionic/main amd64/openssh-server-amd64 1.7p2-ubuntu2.6 [335 KB]
在 1 秒内获取了 335 KB (452 KB/s)
正在设置存档...
选择之前未选择的软件包 openssh-server
准备安装 openssh-server (1.7p2-ubuntu2.6.2.64) (当前已安装)...
准备解压 .../openssh-server_1.7p2-ubuntu2.6_ubuntu2.amd64.deb ...
正在处理 readdev (0.0.0-19) 的触发器...
正在处理 libc (2.27-0ubuntu3) 的触发器...
正在处理 ufw (0.32.1) 的触发器...
正在配置 openssh-server (1.7p2-ubuntu2.6_ubuntu2.amd64) ...
qemu@qemu-VirtualBox:~/rpi/ubuntu-rpi3$ ps aux | grep ssh
qemu@qemu-VirtualBox:~/rpi/ubuntu-rpi3$ 1873 pts/0    S    00:00 grep --color=auto ssh
qemu@qemu-VirtualBox:~/rpi/ubuntu-rpi3$ 
```

```bash
qemu@qemu-VirtualBox:~/rpi/uboot-rpi3$ sudo apt apt-get
[sudo] qemu 的密码是:
读取软件包列表... 完成
构建依赖树
读取状态信息... 完成
以下软件包已自动安装：
linux-headers-4.15.0-29-linux-headers-4.15.0-29-generic
linux-modules-4.15.0-29-generic
使用 'sudo apt autoremove' 来删除它们。
建议的软件包：
ssh-askpass rrss rssh molly-guard monkeysphere
将安装新的软件包：
openssh-server
0 个升级，1 个新安装，0 个移除，82 个未升级
需要获取 335 kb 的存档。
在此操作后，将额外使用 904 kB 的磁盘空间。
Get:1 http://archive.ubuntu.com/ubuntu xenial-upd
在 1 秒内获取了 335 kb (215 kb/s)
正在预配置软件包 ...
选择之前未选择的软件包 openssh-serv
(读取数据库 ... 294521 个文件和目录)
准备解压 .../openssh-server_1%3a7.2p2-4ub
解开 openssh-server (1:7.2p2-ubuntu2.6)
正在处理 ureadhead (0.100.0-19) 的触发器...
正在处理 systemd (229-ubuntu21.0) 的触发器...
正在处理 ufw (0.35-ubuntu2) 的触发器...
正在处理 man-db (2.7.5-1) 的触发器...
正在配置 openssh-server (1:7.2p2-ubuntu2.6) ...
qemu@qemu-VirtualBox:~/rpi/uboot-rpi3$ ps -ax | grep
1837 ? Ss 0:00 /usr/sbin/sshd
1873 pts/17 S+ 0:00 grep --color=auto ssh
qemu@qemu-VirtualBox:~/rpi/uboot-rpi3$ 
```

如果这个 `qemu` 进程没有运行，你就无法使用某项功能。现在我们将看看如何使用它。我们将查看幻灯片并尝试理解让成功运行所需的参数。我们需要一个用户名，然后是服务器 IP。对于 CFP Mali 的东西也是一样。我们需要一个额外的文件或文件夹。如果你正在为 `fuller` 进行通信，我们需要传递 `-r` 后面跟文件夹名。现在我们将进入 `0 1 2` 并查看如何操作。由于我们没有任何外部 SSL 服务器，我们将在本地尝试所有这些命令。`127.0.0.1` 是你的本地 IP 地址，你可以进入控制台。这里我们在想这是否在运行。为此，我们需要提供，因为 SSL 调查正在运行，为了验证这一点，将退出此项并在 `sudo` 下作为 EDC 在每个点，然后设置并停止。现在我们的服务器已停止。我们无法再次访问连接到它的主机。现在看，你遇到了像这样的错误，是因为我们的服务器没有正常工作。`copy` 也是如此。来，首先我们需要启动。真的，首先我们需要启动。

## 示例

### 1. SSH (Secure Shell)

安全地连接到远程 `Linux` 机器。

```bash
ssh <username>@<hostname> # 连接到远程机器
```

请谨慎使用。连接后，你可以在远程机器上使用标准的 `Linux` 命令。

### 2. SCP (Secure Copy)

安全地在本地和远程机器之间复制文件（使用 `SSH`）。

```bash
scp <source_file> <username>@<hostname>:<destination_file> # 复制到远程机器
scp <username>@<hostname>:<source_file> <destination_file> # 从远程机器复制
```

请谨慎使用。

### 3. WinSCP (Windows)

适用于 `Windows` 的图形化 `SFTP` 客户端，类似于 `SCP`。

使用 `WinSCP` 界面浏览远程服务器上的文件、上传/下载文件并管理目录。

### 4. TFTP (Trivial File Transfer Protocol)

轻量级文件传输协议。

一种更简单的文件传输协议，通常用于网络设备的初始配置或固件更新。

`TFTP` 服务器（在你的 `Linux` 机器上）：

```bash
tftpd & # 在后台启动 TFTP 服务
```

请务必谨慎使用代码。

`TFTP` 客户端（在另一台机器上）：

```bash
tftp <hostname> <filename> # 从 TFTP 服务器下载文件
tftp -p <local_port> <hostname> <filename> # 下载文件并指定本地端口（可选）
```

注意：`TFTP` 不提供加密或身份验证，因此在不可信的网络上使用时请谨慎。

这些都是基础示例。每个工具都提供了更多选项和功能。请参考它们的手册或在线资源获取详细信息：

- `SSH`: https://man7.org/linux/man-pages/man1/ssh.html
- `SCP`: https://www.zdnet.com/article/how-to-use-the-scp-command-in-linux/
- `WinSCP`: https://winscp.net/eng/index.php
- `TFTP`: https://datatracker.ietf.org/doc/rfc1350/

# 从源码编译 QEMU

我们将学习如何从源码编译 `QEMU`，但在开始之前，我们将先了解从源码编译的必要性。在 `Linux` 中有两种可用方式：我们可以直接下载安装包，也可以下载源代码并针对我们的目的进行交叉编译。我们可以对其进行自定义，可以修改功能后再进行使用。这种功能在 `Windows` 中很少使用。在这里，我们只需要下载工具然后就可以使用这些代码。如果我们使用源码并进行编译，我们将对源代码拥有完全的控制权，可以根据我们的目的和所需功能进行定制。此外还有一点：我们可以控制代码的版本，既可以获取最新的更改，也可以获取任何适合我们目的的提交（`commit`）。但在二进制文件中，我们没有太大的控制权，它取决于发行版。接下来我将介绍 `QEMU` 的前提条件。`QEMU` 需要安装一些先决条件。如果使用源码进行构建，则需要 `SDL` 库、`pixman` 库以及 `flex` 和 `bison` 库。在所有库中，最重要的是我们的 `SDL`。这是一款跨平台多媒体库，旨在为音频、键盘、鼠标以及任何其他硬件特性提供低级访问。没有这个库，`QEMU` 将无法正常工作。

## 前提条件

- `sudo apt-get install libsdl2-dev libpixman-1-dev flex bison`

- Simple DirectMedia Layer (`SDL`) 是一款跨平台多媒体库，旨在通过 `OpenGL` 和 2D 视频帧缓冲区为音频、键盘、鼠标、摇杆以及 3D 硬件提供低层级访问。

- 没有这个库，你将无法使用 `QEMU` 的大部分功能。

现在还需要理解一个概念，为了从源码构建任何包，我们需要三个步骤。首先，我们需要配置该包，然后构建并安装该包。配置是最重要的部分，我们对功能微调拥有完全控制权，或者可以对其进行自定义，甚至可以在包中添加我们的代码并进行构建。现在我将进入 `Ubuntu` 并逐一完成这些操作。首先，我们需要使用 `git clone` 获取源码。这部分已经在 `git` 项目中涵盖过了。我先获取源码。

```bash
## 获取源码
git clone https://github.com/qemu/qemu.git

## 配置
./configure --target-list=arm-softmmu,arm-linux-user --disable-vnc --enable-sdl --prefix=$PWD/sysroot

## 构建
make

## 安装
make
```

我们将进行配置和安装过程。它被下载在 `Qemu` 文件夹中。我们需要进入 `Qemu` 文件夹。

## qemu-VirtualBox: ~/rpi/qemu

```bash
qemu@qemu-VirtualBox: ~/rpi/test_cmd
qemu@qemu-VirtualBox:~/rpi$ cd qemu
qemu@qemu-VirtualBox:~/rpi/qemu$ ls
qemu@qemu-VirtualBox:~/rpi/qemu$ git clone https://github.com/qemu/qemu.git
Cloning into 'qemu'
remote: Enumerating objects: 2, done.
remote: Counting objects: 100% (2/2), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 402898 (delta 0), reused 0 (delta 0), pack-reused 402898
Receiving objects: 100% (402898/402898), 20.15 MiB | 1.05 MiB/s, done.
Resolving deltas: 100% (324332/324332), done.
checking connectivity... done.
qemu@qemu-VirtualBox:~/rpi/qemu$
```

只需输入 `ls` 命令查看它是否已成功下载。为了检查它是否真的是 `git` 源码，输入 `git log` 你就能看到它是否为 `git` 仓库。从 `git log` 中我们可以看到提交信息，这意味着这是一个 `git` 仓库。现在我们将进行配置。对于配置，我们将提供目标列表。我们正在为 `ARM` 编译，因此只提供 `ARM` 相关的配置文件：`arm-softmmu` 和 `arm-linux-user`。第一个参数提示我们要运行我们的 `OS`。第二个参数提示我们要运行应用程序，并禁用 `VNC`，否则它不会在控制台上自动启动。最后一个参数我们提供了构建和安装的 `sysroot` 目录，但在之前我们需要创建这个目录。现在这个目录创建了。

```bash
$ qemu-VirtualBox: ~/rpi/qemu
qemu@qemu-VirtualBox: ~/rpi/test_cmd
qemu@qemu-VirtualBox:~/rpi$ cd qemu
qemu@qemu-VirtualBox:~/rpi/qemu$ ls
qemu@qemu-VirtualBox:~/rpi/qemu$
qemu@qemu-VirtualBox:~/rpi/qemu$ git clone https://github.com/qemu/qemu.git
Cloning into 'qemu'
remote: Enumerating objects: 2, done.
remote: Counting objects: 100% (2/2), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 402898 (delta 0), reused 0 (delta 0), pack-reused 402898
Receiving objects: 100% (402898/402898), 20.15 MiB | 1.05 MiB/s, done.
Resolving deltas: 100% (324332/324332), done.
checking connectivity... done.
qemu@qemu-VirtualBox:~/rpi/qemu$
```

只需输入 `ls` 命令查看它是否已成功下载。为了检查它是否真的是 `git` 源码，输入 `git log` 你就能看到它是否为 `git` 仓库。从 `git log` 中我们可以看到提交信息，这意味着这是一个 `git` 仓库。现在我们将进行配置。对于配置，我们将提供目标列表。我们正在为 `ARM` 编译，因此只提供 `ARM` 相关的配置文件：`arm-softmmu` 和 `arm-linux-user`。第一个参数提示我们要运行我们的 `OS`。第二个参数提示我们要运行应用程序，并禁用 `VNC`，否则它不会在控制台上自动启动。最后一个参数我们提供了构建和安装的 `sysroot` 目录，但在之前我们需要创建这个目录。现在这个目录创建了。

（注：由于原文中存在大量重复的构建日志输出，根据“不要重复输出原文”的原则，此处仅对描述性文字进行翻译，重复的构建日志已略去或合并）

在配置之后，我们需要配置它。现在我将启动这个包，它已成功配置。现在可以运行命令来构建。构建需要一些时间。还有一点：直接下载 `QEMU` 源码可能无法直接构建它，因为某些先决包需要从 `git` 下载。现在构建完成，我们将安装它并查看运行情况。

```
GEN
  trace/generated-helpers.c
CC
  arm-softmu/trace-target.o
CC
  arm-softmu/qemu-system
LINK
  arm-softmu/qemu-system-arm
... (此处省略重复日志)
```
