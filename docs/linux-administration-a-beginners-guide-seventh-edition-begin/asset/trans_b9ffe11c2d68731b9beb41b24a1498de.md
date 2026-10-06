

## 第 22 章 安全外壳 (SSH)

系统自带内置的 SSH 客户端，因此无需担心它们；然而，非 UNIX 操作系统就就是另一回事了。以下是关于 SSH 客户端和其他有用资源的简要介绍：

- PuTTY (https://chiark.greenend.org/~sgatham/putty) 这可能是适用于 Win32（微软 Windows）平台的最古老且最受欢迎的 SSH 实现之一。它非常轻量级，可以作为独立的、自包含的可执行文件使用，也可以像其他 Windows 程序一样安装使用。该网站还托管了其他工具，例如 pscp，它是 Secure SCP 的 Windows 命令行版本。
- 适用于 Apple OS X 的 OpenSSH 是一个基于 UNIX 且符合 UNIX 标准的操作系统。其主要组件之一——内核是基于 BSD 内核的。当你打开终端应用程序时，可以在 OS X 命令行中执行 `ssh` 命令。OS X 系统还分发了 OpenSSH 服务器。
- MindTerm，多平台 (https://www.cryptzone.com) 该程序支持 SSH 协议的第 1 和第 2 版本。它由 100% Java 编写，可以在许多平台（包括 Linux）以及 Windows 和 OS X 上运行。请查看网页获取测试过的操作系统列表。
- Cygwin (www.cygwin.com) 这可能有点大材小用，但投入精力进行设置是非常值得的。它是一个为 Windows 提供 Linux 环境的工具集。它提供了一个环境，可以在无需对源代码进行大量更改的情况下运行大量的 Linux/Unix 程序。在 Cygwin 下，你可以运行所有喜爱的 GNU/Unix 程序，如 bash、grep、find、map（注：此处原文可能为 man）、gcc、awk、emacs、rsync、OpenSSH 客户端等，就像你运行在传统的 GNU/Linux shell 中一样。
- FileZilla (https://zilla-project.org/) FileZilla 是一个跨平台的 FTP 和 SFTP 客户端。
- PowerShell (https://github.com/PowerShell/Win32-OpenSSH) 通过 PowerShell 环境将 OpenSSH 原生移植到微软 Windows 平台。

## 薄弱环节

你可能听过一种说法：“安全性取决于你最薄弱的环节。”在涉及到 OpenSSH 和你的网络安全时，这尤为相关：OpenSSH 的安全性取决于用户与服务器之间最弱的连接。这意味着，例如，如果一个用户使用 Telnet 从主机 A 连接到主机 B，然后使用 ssh 连接到主机 C，那么主机 A 和主机 B 之间的连接就可以被监控。主机 B 和主机 C 之间的连接经过了加密这一事实就变得无关紧要了。

当你通过 SSH 强制用户登录服务器时，务必向你的用户解释这些微妙的观点；遗憾的是，如果你的用户在互联网上的（你无法管理的）系统上使用了 Telnet 等不安全协议，那么通过使用 SSH（在受管理的系统上）实施安全性的努力将付诸东流。而且更多用户可能完全不知道为什么这样做是一个坏主意。

**注意** 当使用 Telnet 访问网络边界时，每一个提供商都有完全的权利嗅探流量并收集他们想要的任何信息。例如，某人可以在你阅读邮件时轻易地看到邮件内容。在使用 SSH 且其他条件相同的情况下，你可以放心地连接是安全的。

## 在 Fedora 中通过 RPM 安装 OpenSSH

这是在任何 Linux 系统上启动 SSH 最简单、最快的方法。在现代 Linux 发行版中，几乎可以肯定你已经安装并运行了该包。即使你选择了精简安装（即在操作系统安装期间选择了最少的软件集），OpenSSH 通常也是常态而非特例。

但是，如果你运行的是在开发时至少安装了红帽软件包管理器 (RPM) 的 Linux 发行版，你始终可以下载并安装预编译的 RPM 包。使用以下命令确保 OpenSSH 确实已经安装：

```
root@fedora-server ~# rpm -qa | grep openssh
```

如果由于某种原因，你还没有安装它（或不小心删除了），你可以使用 `dnf` 安装服务器：

```
root@fedora-server ~# dnf -y install openssh
```

## 在 Ubuntu 中安装 OpenSSH

Ubuntu 发发行版通常预装了客户端，但如果你需要服务器组件，可能必须显式安装。在 Ubuntu 中使用高级软件包工具 (APT) 安装服务器只需运行以下命令：

```
master@ubuntu-server:-$ sudo apt-get -y install openssh
```

在安装后，该过程还会为你启动 SSH 守护进程。你可以运行以下命令来确认软件已安装：

```
master@ubuntu-server:-$ dpkg -l openssh
```

## 从源码下载、编译并安装 OpenSSH

如所述，几乎所有的 Linux 版本都带有 OpenSSH；然而，出于某种原因，你可能需要从源码构建自己的版本。本节将介绍下载 OpenSSH 软件及其所需的两个组件：OpenSSL 和 zlib。一旦这些准备就绪，你就可以编译并安装软件。如果你想坚持使用发行版自带的预编译版 OpenSSH，可以跳过本节，直接进入“服务器启动与关闭”。

在本节中我们将使用 OpenSSH 7.01 版本，但你仍然可以根据任何可用的 OpenSSH 当前版本遵循步骤（只需更改版本号）。你可以从 www.openssh.com/portable.html 下载。选择一个离你最近的下载项，并将 `openssh-7.01.tar.gz` 下载到有足够空间的目录（`/usr/local`）。

（注：由于译文后部分原文内容存在大量重复和逻辑混乱，翻译时已根据技术意图进行了梳理，以确保逻辑清晰。）

