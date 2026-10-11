
在前一个示例输出中出现 `vmx` 表示该 Intel 处理器已配备了所需的 CPU 扩展。

在 AMD 平台上，显示支持基于硬件的全虚拟化的标志是 Secure Virtual Machine (`svm`) 标志。要检查处理器是否支持 `svm`（注：原文此处误写为 Intel，实应为 AMD），我们可以在 `/proc/cpuinfo` 中 `grep` 所需的标志，如下：

```
[root@amd-server ~]# grep -color -i svm /proc/cpuinfo

flags : fpu vmx pse 3nowext ..<OUTPUT TRUNCATED>... svm
```

在前一个示例输出中出现 `svm` 表示该 AMD 处理器已配备了所需的 CPU 扩展。

## KVM 示例

如前所述，KVM 具有良好的跨平台/发行版支持。在接下来的部分中，我们将查看 Fedora Linux 发行版上的示例 KVM 实现。

我们将使用一组基于 Libvirt C 库的工具。特别是，我们将使用“虚拟机管理器”`virt-manager` 应用程序工具包。`virt-manager` 是一个用于管理虚拟机的桌面用户界面。它承诺同时提供完整的图形用户界面 `GUI` 前端和命令行实用。

在示例中，我们将使用“Virt Install”工具 `virt-install`，`virt-install` 是一个提供各种方式来配置虚拟机的命令行工具。它还为 `virt-manager` 应用程序提供了应用程序接口 `API`，用于其图形化虚拟机创建向导。

我们的示例主机的规格如下：

- 硬件软件支持全虚拟化（特别是 AMD-V）
- 4 GB 字节 `GB` 内存
- 宿主机操作系统有足够的空间
- 宿主机操作系统运行 Fedora 版本的 Linux

对于我们的示例虚拟化环境，我们的目标是：

- 使用内置的 KVM 虚拟化平台。
- 设置一个运行 Fedora Linux 发行版的客户操作系统 `VM`。我们将使用宿主机系统 DVD 驱动器 `/dev/sr0` 中的安装介质安装 Fedora。
- 为虚拟机分配总 10GB 的磁盘空间。
- 为虚拟机分配 1GB 内存。

我们将使用以下步骤来实现我们的目标：

1. 使用 Yum 安装“Virtualization”软件包组。该包包含了 `python-virtinst`、`qemu`、`virt-manager` 和 `virt-viewer` 包。

```
[root@serverA ~]# yum groupinstall 'Virtualization'
```

2. 启动 `libvirtd` 服务（注：原文为 libvird，实应为 libvirtd）。输入

```
[root@serverA ~]# service libvird start

Starting libvird daemon: [ OK ]
```

3. 使用 `chkconfig` 工具确保 `libvirtd` 服务在下次系统启动时自动启动。

```
[root@serverA]# chkconfig libvirtd on
```

4. 使用 `virsh` 工具确保虚拟化在系统上已启用并正常运行。

```bash
[root@serverA]# virsh -c qemu:///system list State
```

只要之前的输出没有返回任何错误，我们就没问题。

5. 在我们的示例服务器上，我们将每个虚拟机相关的所有文件存储在自己的文件夹下，使用虚拟机名称作为父文件夹名称。

因此，对于名为 `fedora-VM` 的示例虚拟机，我们将开始创建用于存放虚拟机的目录结构。输入

```
[root@serverA]# mkdir /home/vms/fedora-VM/
```

6. 我们将使用 `python-virtinst` 包自带的 `virt-install` 工具来设置虚拟机。`virt-install` 工具将引导您通过一个快速设置向导，在控制台上询问一系列问题。通过运行以下命令启动 `virt-install`

```bash
[root@serverA]# virt-install --hvm
```

7. 我们将虚拟机 `VM` 的名称设为 `fedora-VM`。

虚拟机名称是什么？`fedora-VM`

8. 我们将为虚拟机分配 1GB 或 1000 兆字节 `MB` 的内存。

应该分配多少内存（兆字节）？`1000`

9. 我们将磁盘镜像存储在 `/home/vms/fedora-VM/` 目录下，虚拟磁盘名为 `fedora-VM-disk`。

您想使用哪个磁盘（文件路径）？`/home/vms/fedora-VM/fedora-VM-disk.img`

10. 根据提示指定虚拟磁盘大小为 10GB。

您希望磁盘 `/home/vms/fedora-VM/fedora-VM-disk` 有多大（千字节）？`10`

11. 我们将为虚拟机启用图形支持。

您想启用图形支持吗？`yes or no` `yes`

12. 我们示例服务器上的驱动器位于 `/dev/sr0`。将其指定为虚拟 CD。

虚拟 CD 镜像是什么？`/sr0`

13. 新配置的虚拟机将在“Virt Viewer”窗口中启动。虚拟机将尝试从安装介质引导。

![](img/92d05360cfbe3adba30a0993f6974865_654_0.png)

14. 从这里开始，你可以像普通机器一样继续安装。

## 在 Ubuntu/Debian 中设置 KVM

我们早期提到过，不同发行版虚拟化实现之间的一个主要区别是围绕虚拟化解决方案构建的管理工具。`Libvirt` 和 `virt-manager` 已移植到 Ubuntu 发行版的最新版本。`Virt-manager` 可以通过以下命令轻松安装

具体来说，我们将查看如何在基于 Debian 的发行版（如 Ubuntu）中设置 KVM。我们 Ubuntu 服务器上的处理器支持所需的 CPU 扩展。我们将在一台带有 Intel-VT 处理器的计算机上安装。目标虚拟机将是 Ubuntu 桌面版本，并将使用从 `//releases.ubuntu.com/releases/8.04/ubuntu-8.04-desktop-i86` 下载的 ISO 镜像安装。

1. 安装 KVM 和 QEMU 包。在 Ubuntu 服务器上输入
`yyang@ubuntu-server:-$ sudo apt-get -y install kvm qemu`

2. 手动加载 `kvm-intel` 模块。输入
`yyang@ubuntu-server:-$ sudo modprobe kvm-intel`

3. 我们作为普通用户运行 KVM，因此需要将示例用户 `yang` 添加到 `kvm` 系统组。
`yyang@ubuntu-server:-$ sudo adduser yyang`

4. 注销会话并以用户 `yyang` 重新登录，以便新的组成员关系生效。
5. 在用户主目录中创建一个文件夹来存储虚拟机，并进入该目录。
`yyang@ubuntu-server:-$ mkdir -p /home/yang/vms/ubuntu-VM`
`yyang@ubuntu-server:-$ cd /home/yang/vms/ubuntu-VM`

> 注意：加载 `kvm-intel` 模块也会自动加载所需的模块。在基于 AMD 的系统中，所需的模块被称为 `kvm-amd`。

6. 我们将使用 `qemu-img` 工具为虚拟机创建一个磁盘镜像。该镜像的大小为 10GB。用于存放虚拟磁盘的文件将命名为 `disk.img`。输入：

```
yyang@ubuntu-server:~/vms/ubuntu-VM$ qemu-img create disk.img -f qcow2 10G
```

> 提示：在 `qemu-img` 命令中指定的 `-f` 选项用于指定磁盘镜像格式。在这里我们使用 `-qcow2` 格式。这种格式通过不预先分配指定的整个磁盘空间提供了节省空间的选项。相反，它会创建一个小文件，并随着数据写入虚拟磁盘镜像，该文件会随之增大。另一个有趣的虚拟磁盘格式是 `-vmdk` 选项，它允许创建与 VMware 虚拟机兼容的虚拟磁盘。

7. 一旦创建了磁盘镜像，我们就可以通过向 `kvm` 直接传递必要的选项来启动虚拟机的安装程序。执行此操作的命令为：

```
yyang@ubuntu-server:~/vms/ubuntu-VM$ kvm -m 1024 \
-cdrom ubuntu-8.04-desktop-i386.iso \
-cdrom d disk.img
```
