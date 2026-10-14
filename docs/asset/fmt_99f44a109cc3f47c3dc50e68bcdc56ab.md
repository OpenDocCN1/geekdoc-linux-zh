
```
#!/bin/sh
if [ "$1" != x ]; then
FILE=$1
else
FILE=-
fi
gs -q -dBATCH -dOPAUSE -dSAFER -sOutputFile=$FILE- \
r000x600 -sDEVICE=ljmono file | sambclient args
```

有一个较新的 Ghostscript 驱动程序 `unpre` 支持多种打印机。这是一个为 Epson Colorplex 600 处理 PostScript 文件的命令：

```
gs @stc600.up -q -dBATCH -dOPAUSE -dSAFER -sOutputFile== file
```

如果你不知道使用哪个驱动程序，首先检查 Ghostscript 库目录中的 `.app` 文件查看是否有适用于你打印机的。如果看起来都不对，使用 `gs -help` 显示所有驱动程序列表，或者查阅 Ghostscript

# 第 10 章：网络服务

网站及文档 http://www.ghostscript.com/

## 10.8 Unix 系统的 SSH 远程 Shell 访问

Unix 系统可以轻松地从远程登录并执行许多通常在控制台上进行的操作。在 VMware Workstation 中，你可以利用这一特性：你可以从主机系统登录到 Unix 虚拟机。这种方法意味着你可以完全避免在主机系统和 VMware 窗口/全屏模式之间切换；你只需要切换窗口即可。此外，如果你使用安全 Shell `SSH`，你可以通过连接发送图形。

有多个 SSH 软件包。我们在书中提到 `OpenSSH`，它是由 OpenBSD 人员实现的。它支持 SSH 版本 1 和 2 协议，你可以从 http://www.openssh.com/ 获取它。

### 10.8.1 安装和配置 SSH 服务软件

Red Hat Linux 系统提供了 SSH 服务软件的二进制文件，但对于大多数实现，如果你的虚拟机系统中没有自带，你就需要获取源代码并从那里构建。要编译 `OpenSSH`，你需要 `OpenSSL`，这是一种安全套接层 `SSL` 协议的实现。

安装 `OpenSSH` 后，验证配置和密钥位置：

- 1. 找到 `OpenSSH` 安装前缀目录（默认是 `/usr/local/etc`）。你应该看到两个配置文件：`ssh_config` 和 `sshd_config`。（如果你想使用 X 客户端转发，需要修改这些文件；我们很快会介绍。）

- 2. 在同一目录中，查找主机密钥文件。所有密钥文件都以 `ssh_host_` 开头。应该有三组。如果文件名包含 `rsa` 或 `dsa`，则它是用于 SSH 版本 2 协议。其他密钥用于 SSH 版本 1。任何带有 `.pub` 后缀的都是公钥。然而，任何没有后缀的都是私钥。不要让任何人看到它们。

- 3. 如果缺少这些密钥，请手动创建它们（将它们放在与 `sshd_config` 文件相同的目录中）。使用以下命令生成版本 1 密钥：

```
ssh-keygen -t rsa -f ssh_host_key
```

- 使用此命令生成版本 2 密钥：

```
ssh-keygen -t rsa -f ssh_host_rsa_key
ssh-keygen -t dsa -f ssh_host_dsa_key
```

- 现在你应该能够在虚拟机操作系统上启动 SSH 服务。

### 10.8.2 启动 SSH 服务

要启用 SSH 远程访问，你需要在要访问的虚拟机上启动 `sshd`。你应该在虚拟机系统的 `sbin` 目录之一找到服务器：`/usr/sbin` 或 `/usr/local/sbin`。

让 `ssh` 在启动时启动，你可以将脚本添加到启动设置。在 Linux 发行版中，这是 `init.d` 脚本；在 BSD 系统中，使用 `/etc/rc` 脚本。关于这些脚本的更多信息请参见第 6、7、8 章。

你也可以使用选项启动 `ssh`，这通常不是好主意，因为 `ssh` 每次启动时都会执行计算，而且由于每个连接都会调用新进程，你可能会等待一段时间。

### 10.8.3 SSH、主机网络和主机名解析

`SSH` 客户端和服务器对主机名解析非常严格。特别是，它们会对 `/etc/hosts` 进行正向和反向检查，并绕过 `/etc/resolv.conf` 文件。如果你使用主机网络，这可能会是一个问题，因为 DHCP 默认将主机的 IP 地址作为 DNS 服务器。除非主机上运行了名称服务器，否则虚拟机上的 SSH 发送请求时永远得不到响应，任何的 SSH 连接都会挂起。

要在虚拟机系统上解决这个问题，检查虚拟机上的 DNS 配置（见第 9.4 节）。主机网络无法访问会导致虚拟机不知道向哪里发送数据包并立即生成“网络不可到达”错误。另一种解决办法是使用 IP 数字而不是名称，但这不方便。

### 10.8.4 SSH 客户端

现在你已经在虚拟机操作系统上运行了服务器，你需要一种从主机系统连接到虚拟机操作系统的方法。

许多应用程序的最佳方法也是使用 `OpenSSH`。因为客户端和服务器包整合在一起，Linux 操作系统的安装过程与虚拟机相同，只是你不需要担心启动 `sshd` 服务器。

对于 Windows 操作系统，获取 FreeBSD 的 `OpenSSH`。有关安装 FreeBSD 的更多信息请参见第 5.5 节，尽管第 5 章关注虚拟机，但本节适用于主机和虚拟机。

从主机系统登录到虚拟机，在命令提示符中运行：

```
ssh user@guest_system
```

在这里，`user` 是你的用户名，`guest_system` 是虚拟机的名称或 IP 地址。`ssh` 程序会提示输入密码。

你可以使用另一个 `OpenSSH` 工具 `scp` 在虚拟机进出复制文件。例如，要从 `guest_system` 复制到当前目录，输入：

```
scp user@guest_system:.
```

反过来，输入：

```
scp user@guest_system:file
```

`OpenSSH` 还包括一个实用的 `sftp` 工具，看起来用起来像 `ftp`。

#### 其他 Windows 客户端

尽管 FreeBSD 的 `OpenSSH` 与 Unix 版本一样，你可能想要一个具有 Windows 风格的客户端。Windows 有多种商用和开源 SSH 客户端。本节将重点介绍开源客户端；你可以在 http://www.ssh.com/ 找到一些商业 SSH 客户端。

有一个支持版本 1 的 SSH 扩展。你可以从 http://www.zip.com.au 获取该扩展（如果链接失效，尝试在 http://google.com/ 输入 ssh）。你也会找到下载版本的链接。终端客户端作为独立的 Windows 运行，并有许多外观自定义。当你连接到远程服务器时，确保你使用 SSH 协议。这种做法有两个缺点：其一分为两个阶段。你必须先安装软件，然后必须安装扩展。可能会引起一些困惑，因为安装后有两个客户端：一个是普通版本，另一个是 SSH 扩展版本。另一个局限性是它不支持 SSH 版本 2，这并不是什么大问题。

另一个流行的 SSH 客户端是 `PuTTY`。像 Unix 上的 `OpenSSH` 一样，这是一个命令行工具，`PuTTY` 体积很小，并带有实用的传输工具如 `pscp` 和 `psftp`。你可以从美国的镜像站 http://putty.bnhni.net/ 获取 `PuTTY`（或者像其他一样，如果找不到，尝试在 http://google.com/ 输入 putty）。

### 10.8.5 带有 SSH 的 X 转发

如前所述，你现在可以从远程机器发送 X11 服务器显示和端口，所有流量通过主机传输。要这样做，你通过加密的 SSH 通道建立一个隧道，然后转发到原始机器上的 X11 服务器端口。连接授权通过 `xauth` 完成；`ssh` 为显示生成一个 cookie 值并将其发送到远程机器。

## 第10 章：网络服务

`X11Forwarding no`

`X11DisplayOffset 10`

将 `no` 改为 `yes`。另一行应该没有问题（除非由于某种原因，你在该机器上运行了超过 10 个 X 显示器）。

- 2. 关闭客机系统的 `sshd` 服务并重新启动它，使其重新读取配置文件。

- 3. 编辑你宿主机系统的 `ssh_config` 文件。查找以下行：

```
# *

# ForwardAgent no

# ForwardX11 yes
```

移除 `Host` 和 `ForwardX11` 行前的注释字符。如果你只想允许你的虚拟机系统进行转发，请将 `*` 更改为你的宿主机仅主机网络子网。

- 4. 测试你的转发安装。从宿主机向客机系统发送 `ssh` 连接，当进入 shell 后，输入如 `x` 的命令。如果你看到一个新窗口，说明安装成功。

有时，由于库和协议的变化，转发机制可能无法与预先安装的 SSH 配合。在这种情况下，将所有内容升级到最新版本的 `OpenSSH` 应该可以解决问题。

## Windows 宿主机系统如何处理？
