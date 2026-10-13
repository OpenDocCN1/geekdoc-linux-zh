
您可能并非总能访问 GUI，尤其是在从远程系统工作时。无论如何，基于文本的浏览器运行得更快。Red Hat 的标准基于文本的浏览器是 elinks。安装软件包后，您可以从命令行使用它来打开您选择的网站。例如，图 2-19 说明了 `elinks http://www.mheducation.com` 命令的结果。

退出 elinks 时，按 ESC 键访问菜单栏，然后按 F1x 并接受提示退出浏览器。

如果您配置了 Web 服务器，确保其正常工作的最简单方法是使用简单的文本主页。无需 HTML 编码。例如，我可以将以下文本添加到 `home.html`：

这是我的主页

然后我可以运行 `elinks home.html` 命令在 elinks 浏览器中查看此文本。如果您已按照第 1 章讨论的内容在 `/var/www/html/inst` 目录上设置了 Apache 文件服务器，您也可以使用 elinks 通过以下命令查看复制到该服务器的文件：

$ elinks http://192.168.122.1/inst

## 图 2-19

elinks 浏览器

![](img/9139201cfcaf4292284a0eed074928e5_118_0.png)

### 使用 lftp 访问 URL

原始 FTP 客户端软件是一个基本的命令行、文本导向的客户端应用程序，提供简单但高效的界面。大多数 Web 浏览器提供图形界面，也可作为 FTP 客户端使用。

任何 FTP 客户端都允许您查看目录树和文件。使用 ftp 作为客户端很容易。您可以使用 ftp 命令通过以下命令连接到 `ftp.redhat.com` 等服务器：

# ftp ftp.redhat.com

但该客户端会要求输入用户名和密码。您可以输入用户名 anonymous 和随机密码来访问 Red Hat FTP 服务器。但如果您不小心输入了真实的用户名和密码，这些数据会以明文发送，任何恰好在网络上使用正确网络分析应用程序的人都可以获取。奇怪的是，ftp 命令客户端未安装在标准 RHEL 6 安装中。

这就是 lftp 更好的原因之一。它会自动尝试匿名登录，而不会提示输入用户名或密码。它还支持命令补全，这对于访问名称较长的文件和目录尤其有帮助。

当然，大多数 FTP 客户端都存在风险，因为它们以明文传输数据。但只要该命令的使用仅限于具有匿名访问权限的公共服务器，风险就很小。毕竟，如果您使用 lftp 从公共服务器下载 Linux 软件包，就不会有任何私人信息面临风险。确实，这类客户端还存在其他安全风险，但 Red Hat 开发人员一直在努力保持该客户端的最新状态。

如果风险可以接受，lftp 命令可用于登录启用用户名和密码的 FTP 服务器。正在准备 RHCE 考试的您将设置这种非常安全的 FTP（vsFTP）服务器。用户 michael 可以使用以下命令登录此类服务器：

$ lftp ftp.example.org -u michael

lftp 客户端可以处理多种不同的命令，如图 2-20 所示。其中一些命令在表 2-5 中有描述。

## 图 2-20

lftp 中的命令。

```
[root@Maui ~]# lftp ftp.redhat.com
lftp ftp.redhat.com:~> help
! <shell-command>
alias [<name> <value>]
cache [<SUBCMD>]
cd [<dir>]
close [ -a ]
debug [<level>|off] [ -o <file> ]
exit [<code>|bg]
glob [OPTS] <cmd> <args>
history -w file|-r file|-c|-l [cnt]
kill all|<job_no>
lftp [OPTS] <site>
mget [OPTS] <files>
mkdir [-p] <dirs>
more <files>
mrm <files>
[re]list [<args>]
pget [OPTS] <file> [ -o <file>]
pwd
quote <cmd>
rm [-r] [-f] <files>
save [<session_no>]
site <site_cmd>
torrent [-O <dir>] <file>
version
zcat <files>
lftp ftp.redhat.com:~> 
(commands)
bookmark [SUBCMD]
cat [-b] <files>
chmod [OPTS] mode file...
[re]cls [opts] [path/]pattern
du [options] [dirs]
get [OPTS] <file> [ -o <file>]
help [<cmd>]
jobs [-v]
lcd [<dir>]
ls [<args>]
mirror [OPTS] [remote [local]]
module name [args]
mput [OPTS] <files>
mv <file1> <file2>
open [OPTS] <site>
put [OPTS] <file> [ -o <file>]
queue [OPTS] [<cmds>]
repeat [OPTS] [delay] [command]
rmdir [-f] <dirs>
set [OPT] <var> [<val>]
source <file>
user <user@URL> [<pass>]
wait [<jobno>]
zmore <files>
```

几乎所有来自 FTP 提示符的命令都在远程主机上运行，类似于 Telnet 会话。您可以从该提示符运行常规 shell 命令；只需在命令前加上感叹号 (!) 即可。这只是通过 lftp 可用的命令子集。如果您不记得某些内容，命令 `help cmd` 会给出该命令本身的简要描述。

### 认证摘要

鉴于虚拟化在当今计算环境中的重要性，Red Hat 将 KVM 纳入 RHCSA 相关要求也就不足为奇了。假设与适当存储库的有效连接，安装与 KVM 相关的软件包相当容易。您可能需要使用类似 `modprobe kvm` 的命令来确保加载了适当的模块。然后可以使用虚拟机管理器在 RHEL 6 系统上使用 KVM 设置 VM。您也可以使用 `virt-install`、`virt-clone` 和 `virsh` 等命令来安装、克隆和管理这些 VM。

您可以使用 Kickstart 自动化整个安装过程。每个 RHEL 系统都在 `/root` 目录中有一个 Kickstart 模板文件，您可以修改它并自动在其他系统上安装 RHEL。或者，您可以使用 GUI Kickstart 配置器创建适当的 Kickstart 文件。

对于所有这些系统，远程访问是必须的。SSH 命令可以帮助在 Linux 系统之间建立远程加密通信。RHCSA 要求您知道如何使用 SSH 客户端。`ssh` 命令可用于登录远程系统；`ssh -X` 命令甚至可用于访问远程 GUI 应用程序。`scp` 复制命令可通过该加密连接远程复制文件。

在审查和排除 RHEL 服务故障时，拥有一些命令行工具会很有帮助。`telnet` 命令可以连接到选定端口上的远程服务。`nmap` 命令可用作端口扫描器。`mutt` 命令可以检查电子邮件服务器的功能。`elinks` 命令可用作命令行浏览器。最后，`lftp` 命令是一个出色的 FTP 客户端，支持命令补全。

### 两分钟练习

以下是第 2 章认证目标中的一些关键要点。

### 为 Red Hat 配置 KVM

- KVM 所需的软件包是虚拟化软件包组的一部分。
- 基于 KVM 的 VM 可以使用虚拟机管理器进行配置。
- KVM 所需的模块包括 `kvm` 和 `kvm_intel` 或 `kvm_amd`。

### 在 KVM 上配置虚拟机

- KVM 虚拟机的默认存储目录为 `/var/lib/libvirt/images`。
- VM 配置文件存储在各个 `/etc/libvirt` 子目录中。
- VM 控制台可通过虚拟机管理器访问，您可以在 GUI 中使用 `virt-manager` 命令启动它。
- VM 可以使用 `virt-install`、`virt-clone` 和 `virsh` 命令进行安装、克隆和配置。
- `virsh list --all` 命令列出所有已配置的 VM。
- `virsh autostart vmname` 命令配置名为 vmname 的 VM 在主机系统启动时自动启动。
- `virsh start vmname` 命令启动名为 vmname 的 VM 的启动过程。
- `virsh destroy vmname` 命令实际上切断了名为 vmname 的 VM 的电源。

### 表 2-5 标准 lftp 客户端命令

| 命令 | 描述 |
|---|---|
| cd | 在远程主机上更改当前工作目录 |
| ls | 列出远程主机上的文件 |
| get | 从远程主机检索一个文件 |
| mget | 使用通配符或完整文件名从远程主机检索多个文件 |
| put | 将一个文件从您的计算机上传到远程主机 |
| mput | 将一组文件上传到远程主机 |
| pwd | 列出远程主机上的当前工作目录 |
| quit | 结束 FTP 会话 |
| !ls | 在当前目录中列出您主机计算机上的文件 |
| lcd | 更改用于上传/下载的本地主机目录 |
| !pwd | 列出本地主机计算机上的当前工作目录 |
