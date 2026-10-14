
# 使用 QEMU 和 KVM 创建虚拟机

`matthew@seymour:~$ sudo cap cap_net_admin=ei /usr/bin/qemu-system-x86_64`

如果你是 32 位系统，使用此命令：

```
matthew@seymour:~$ sudo cap cap_net_admin=ei /usr/bin/qemu
```

然后通过向 `/etc/network/interfaces` 或你的网络设置中添加这些行来创建一个名为 `br0` 的桥接接口：

```
auto br0

iface br0 inet eth0

bridge_stp off

bridge_fd 0

bridge_maxwait 0
```

通过输入以下内容重启网络：

```
matthew@seymour:~$ sudo /etc/init.d/networking restart
```

最后，你需要创建一个使用此网络的客机操作系统。创建用于 KVM 的虚拟机有多种方法。一种方法是使用 `vmbuilder`。这是一个 Python 脚本，最适用于你打算在其运行 Ubuntu Jeans 的服务器，Jeans 是一种专门的、非常轻量的 Ubuntu 变体，它包含一个仅包含作为服务器运行的基础元素的内核，特别是在 KVM 或 VMware 环境下。然而，实际上有大量的选项和自定义可用。这里有一个示例，它为 Ubuntu 的 `Natty Narwhal` 版本从 KVM 构建一个虚拟机，在 `i386` 架构上使用虚拟变体，例如 Jeans，同时覆盖之前的之前的任何版本的虚拟机，使用 `libvirt` 通知虚拟化环境，将其添加到可用虚拟机列表中，为新虚拟机指定特定的 IP 地址、主机名 `lovelace`，并使用 `br0` 桥接接口。呼！命令里的信息量可真大了。

```
matthew@seymour:~$ vmbuilder kvm ubuntu --suite natty --flavour virtual --arch i386 --co --libvirt qemu://system --ip 192.168.0.100 --hostname lovelace --bridge br0
```

你可以从帮助信息中了解更多：

```
matthew@seymour:~$ vmbuilder kvm ubuntu --help
```

由于 `vmbuilder` 过于专业，在这里我们专注于使用 `virtinst` 中的工具，因为它们可能更受普通受众欢迎。然而，如果你打算在 KVM 或 VMware 安装上创建服务器虚拟机，你绝对想要深入探索 `vmbuilder`。不过，你可能不需要这样做。一组官方、预构建且 Ubuntu 支持的虚拟机镜像可以下载自：`http://cloud-images.ubuntu.com`。这些是 Ubuntu 在 EC2 中使用的镜像。

`virtinst` 包含多个工具。在这里我们专注于：`virt-install`，用于配置新虚拟机；以及 `virt-clone`，用于克隆现有的虚拟机。

你可以使用 `virt-install` 执行与之前使用 `vmbuilder` 相似的操作。主要的区别在于可用的选项，且 `virt-install` 还可以创建包含 GUI 的桌面镜像，可以通过 VNC 进行访问。关于 VNC 的讨论，请参见第 18 章“使用 SSH、Telnet 和 VNC 进行远程访问”。

这是一个示例：

```
$ matthew@semour:-$ sudo virt-install -n hopper -r 512 --disk --path=/var/lib/libvirt/hopper.img,size=20 -c /dev/cdrom --accelerate --connect=qemu:///system -vnc --noautoconsole -v
```

上述示例包含以下选项：

- `-n hopper` 定义新虚拟机的名称。
- `-r 512` 指定分配给虚拟机的内存，单位为兆字节。
- `--disk --path=...` 是虚拟磁盘的路径。它可以是一个文件、分区或逻辑卷。在这里，我们在 `/var/lib/libvirt/images` 中创建一个名为 `hopper.img` 的 20GB 文件。
- `-c /dev/cdrom` 是宿主机 CD-ROM 设备的路径。你也可以使用 ISO 文件。
- `--accelerate` 启用内核加速。
- `--connect` 定义要使用的虚拟机监控程序。
- `--vnc` 使用 VNC 虚拟控制台导出客户机。
- `--noautoconsole` 防止自动连接到虚拟机的控制台。
- `-v` 创建一个完全虚拟化的客户机。

要复制虚拟机，请使用 `virt-clone`：

```
$ matthew@semour:-$ sudo virt-clone -o hopper -n hopper -f /var/lib/libvirt/images/knuth.img --connect=qemu:///system
```

上述示例包含以下选项：

- `-o hopper` 定义源或源虚拟机的名称。
- `-n knuth` 定义新虚拟机的名称。
- `-f` 定义新虚拟机将使用的文件、分区或逻辑卷的路径。
- `--connect` 定义要使用的虚拟机监控程序。

要启动虚拟机，请使用以下命令：

```
$ matthew@semour:-$ virsh -c qemu:///system start hopper
```

## VirtualBox

要停止虚拟机，请使用此命令：

```
matthew@semour:~$ virsh -c qemu:///system shutdown hopper
```

在虚拟机安装并运行后，你可以使用配置的 IP 地址和 `ssh` 工具连接到它。你也可以配合以下使用 GUI：

```
matthew@semour:~$ virt-viewer -c qemu:///system hopper
```

你可以通过连接到以下内容使用 GUI 管理你的虚拟机：

```
matthew@semour:~$ virt-manager -c qemu:///system
```

如果你感兴趣如何使用 KVM 测试 Ubuntu 开发版本的简单方法，请参考第 40 章“帮助 Ubuntu 测试与 QA”，以及对 Test Drive 的讨论，它可以自动化处理整个过程，包括下载特定的 Ubuntu 文件。

VirtualBox 比 KVM 易于使用得多，尤其是当你们都想在 Ubuntu 之上运行第二个操作系统时。它由 innotek GmbH 创建，被 Sun Microsystems 购买，现在在 Oracle 收购 Sun 后由 Oracle 拥有并开发。VirtualBox 安装在另一个操作系统之上，因此对于对每个处理器周期都至关重要的计算密集型活动并不是理想的。然而，对于测试或因为需要特定应用程序而运行另一个操作系统，它是棒的。VirtualBox 运行在大多数 UNIX 类型的操作系统上，如 Linux、BSD 和 Mac OS X，以及 Windows。

Ubuntu 软件存储库中有 VirtualBox 版本，但通常认为从 VirtualBox 网站下载是更好的主意。访问 `www.virtualbox.org/wiki/Downloads`。从那里，你可以下载任何你可能使用的操作系统的版本，包括 Linux 页面的 Ubuntu DEB 文件，该文件使用高级软件包工具 `APT` 安装，软件包管理不是问题。然而，这也能让你方便地下载扩展包 `extension pack`，该扩展包在 Ubuntu 存储库中不可用，因此你可以快速方便地获取它。扩展包添加了一些优秀但专有的功能，这些功能无法在主程序所使用的 GPL 协议下提供，例如从 VirtualBox 中的客户机连接到宿主机的 USB 端口。安装完成后，使用以下命令在命令行启动 VirtualBox：

```
matthew@semour:~$ virtualbox
```

如果你希望在关闭终端的同时保持 VirtualBox 运行，可以在命令后加上一个 ampersand `&`，通过在后台运行 VirtualBox，例如：

```
matthew@semour:~$ virtualbox &
```
