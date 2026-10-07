
你可以从帮助文件中学习更多信息：
```
mathew@vmseym:-$ vmbuilder kvm ubuntu --help
```

由于`vmbuilder`非常专门化，我们侧重于使用`virtinst`的工具，因为它们更可能受普通观众青睐。然而，如果你正在寻找运行在 KVM 或 VMware 安装环境上的服务器虚拟机，你绝对想要充分探索`vmbuilder`。不过，你可能并不需要。在`http://cloud-images.ubuntu.com`可以下载一组官方、预构建且受 Ubuntu 支持的虚拟机镜像。这些是 Ubuntu 在 EC2 中使用的镜像。

## 注意 (NOTE)

Ubuntu Server 的开发者之一 Dustin Kirkland 在一个博客博文中概述了预用 Ubuntu Server 安装的方法，使过程变得更快。你可以在此处阅读它：`http://blog.dustinkirkland.com/2011/03/ubuntu-server-quick-install-no.html`。

`virtinst`由多个工具组成。在这里我们重点关注：`virt-install`，用于提供新的虚拟机；以及`virt-clone`，用于创建现有的虚拟机。

## VirtualBox

VirtualBox 的使用起来比 KVM 易用得多，特别是如果你只是想在它上面运行一个操作系统。它由 Innotek GmbH 创建，被 Sun Microsystems 收购，现在由 Oracle 在收购 Sun VirtualBox 后拥有并进行开发。VirtualBox 安装在另一个操作系统之上，因此对于对每个处理器周期都关重要的密集型活动来说并不理想。但是，对于测试或运行需要特定应用程序的操作系统，它是很棒的。VirtualBox 运行在大多数 UNIX 类型操作系统上，如 Linux、BSD 和 Mac OS X（以及 Windows）。

Ubuntu 仓库中有 VirtualBox 的版本，但通常从 VirtualBox 网站下载是更好的主意：`www.virtualbox.org`。从那里，你可以下载适用于你可能使用的任何操作系统的版本，包括 Linux 上使用高级软件包工具 (`APT`) 安装的 DEB 文件，因此包管理不是问题。然而，这可以让你轻松访问扩展包（extension pack），该扩展包在 Ubuntu 仓库中不可用，因此你可以快速地获取它。扩展包添加了一些优秀但专有的功能，这些功能无法在主程序使用的 GPL 协议下提供，它可以从 VirtualBox 中的客机连接到主机的 USB 端口。安装后，使用以下命令在命令行启动 VirtualBox：

```
mathew@seymour:-$ virtualbox
```

如果你希望在关闭终端时保持 VirtualBox 运行，请在命令后加一个取符符号 (`&`) 来在后台运行 VirtualBox，如下：

```
mathew@seymour:-$ virtualbox &
```
