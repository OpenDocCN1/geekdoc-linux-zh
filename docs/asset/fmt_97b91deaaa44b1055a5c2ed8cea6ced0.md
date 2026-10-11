
基于内核的虚拟机（简称 KVM）是 Linux 对虚拟化领域的官方回答和贡献。KVM 通过将内核转换为虚拟机管理程序（hypervisor）来工作。支持虚拟化 CPU 扩展的 x86 平台（如 Intel-VT 和 AMD-V 系列提供的）支持稳定的 KVM 实现。

由于 KVM 直接实现在 Linux 内核中，它被许多 Linux 发行版。不同发行版之间的主要区别在于，尽管虚拟机管理工具和用户空间工具是围绕特定的实现构建的，然而，如果选择基础的 KVM 设置，可以在任何 Linux 发行版上使用相同的指令集。

`/proc/cpuinfo` 伪文件系统条提供了 Linux 系统上运行 CPU 的详细信息。除外，该条目还显示了运行 CPU 支持的标志/扩展。

在 Intel 平台上，显示支持全硬件虚拟化的标志是 `vmx`。要检查 Intel 处理器是否支持 `vmx`，我们可以在 `/proc/cpuinfo` 中 grep 所需的标志，如下：

```
[root@intel-serverA]# grep -i "vmx" /proc/cpuinfo
flags : fpu pae mce cx8 apic ..OUTPUT TRUNCATED.. vmx
```

上述示例输出中存在 `vmx` 说明 Intel 处理器已配备了必要的 CPU 扩展。

在 AMD 平台上，显示支持全硬件虚拟化的标志是安全虚拟机 (`svm`) 标志。要检查 Intel 处理器是否支持 `svm`，我们可以在 `/proc/cpuinfo` 中 grep 相应的标志，如下：

```
[root@amd-serverA ]# grep --color -i svm /proc/cpuinfo
flags : fpu vme pse 3dnowext ..OUTPUT TRUNCATED.. svm
```

上述示例输出中存在 `svm` 说明 AMD 处理器已配备了必要的 CPU 扩展。

## KVM 示例

如前所述，KVM 具有良好的跨平台/发行版支持。在接下来的章节中，我们将查看 Fedora Linux 发行版上的 KVM 实现示例。

我们将使用一组基于 Libvirt C 库的工具。特别地，我们将使用“虚拟机管理器”（`virt-manager`）应用工具包。`virt-manager` 是一个用于管理虚拟机的桌面用户界面。它承诺提供完整的图形用户界面 (GUI) 前端和命令行实用程序。

在这个示例中，我们将使用“Virt Install”工具（`virt-install`，`virt-install` 是一个命令行工具，为 `virt-manager` 应用提供应用程序编程接口 (API)，用于其图形化虚拟机创建向导）。

我们的示例主机系统规格如下：

- 硬件软件支持全虚拟化（特别是 AMD-V）
- 4 GB字节 (GB) 内存
- 宿主机操作系统有足够的可用空间
- 宿主机操作系统运行 Fedora 版本的 Linux

对于我们的示例虚拟化环境，目标是：

- 使用内置的 KVM 虚拟化平台。
- 设置一个运行 Fedora Linux 发行版的客户操作系统 (VM)。我们将使用宿主机系统 DVD 光驱（`/dev/sr0`）中的安装媒体安装 Fedora。
- 为 VM 分配总共 10GB 的磁盘空间。
- 为 VM 分配 1GB 内存。

我们将使用以下步骤来实现目标：

1. 使用 Yum 安装“Virtualization”包组。该包包含 `python-virtinst`、`kvm`、`qemu`、`virt-manager` 和 `virt-viewer` 包。
2. 启动 `libvirtd` 服务。输入。

```
[root@serverA ~]# yum groupinstall 'Virtualization'
```

```
[root@serverA ~]# service libvirtd start
Starting libvirtd daemon: [ OK ]
```

3. 使用 `chkconfig` 工具确保 `libvirtd` 服务在下次系统启动时自动启动。

```
[root@serverA ~]# chkconfig libvirtd on
```

4. 使用 `virsh` 工具确保虚拟化在系统中启用并正常运行。

```
[root@serverA ~]# virsh -c qemu:///system
```

5. 只要之前的输出没有返回任何错误，在我们的示例服务器上，我们将文件存储在虚拟机名称下。
6. 我们将使用 `python-virtinst` 自带的 `virt-install` 包来设置虚拟机。

```
[root@serverA ~]# mkdir -p /home/vms/
```

7. `virt-install` 将运行一系列问题来设置机器。

```
[root@serverA ~]# virt-install --hvm
```

8. 我们将为 VM 分配 1GB 内存。
9. 我们将磁盘镜像存储在 `/home/vms/ubuntu-vm`。
10. 指定磁盘大小为 10GB。
11. 我们为 VM 启用图形支持。
12. 我们将光驱指定为 `/dev/sr0`。
13. 我们将使用 `/dev/sr0` 中的安装媒体。
14. 从这里开始，你可以像普通机器一样继续操作。

## 第 28 章：虚拟化

之前设置的 KVM 虚拟化是使用管理工具（`virt-manager`）完成的，这些工具为 Fedora、红帽企业 Linux (RHEL) 和 CentOS 设计的。

注意 Libvirt 和 `virt-manager` 已移植到最新版本的 Ubuntu。Virt-manager 可以通过以下命令安装：

```
yyang@ubuntu-server~$ apt-get install virt-manager
```

具体，我们将查看如何在基于 Debian 的发行版（如 Ubuntu）中设置 KVM。我们的 Ubuntu 服务器处理器支持必要的 CPU 扩展。我们将在带有 Intel-VT 处理器的计算机上安装。

目标虚拟机将是 Ubuntu 版本版本并使用 `http://releases.ubuntu.com/releases/8.04/ubuntu-8.04-desktop-i386.iso` 安装。

1. 安装 KVM 和 QEMU 包。在 Ubuntu 上，输入

```
yyang@ubuntu-server:-$ sudo apt-get -y kvm qemu
```

2. 手动加载 `kvm-intel` 模块。输入

```
yyang@ubuntu-server:-$ sudo modprobe kvm-intel
```

> 注意加载 `kvm-intel` 模块也会加载所需的 `kvm` 模块。在 AMD 系统上，所需的模块被称为 `kvm-amd`。

3. 我们将作为普通用户运行 KVM，因此我们需要将示例用户 (yang) 添加到 kvm 系统组。输入

```
yyang@ubuntu-server:-$ sudo adduser yyang yang
```

4. 注销并重新以 yyang 用户登录，以便新的组权限生效。
5. 我们将使用 `qemu-img` 工具为虚拟机创建一个磁盘镜像。该镜像的大小为 10GB。存放虚拟磁盘的文件将命名为 `disk.img`。输入：

```
yyang@ubuntu-server:~/vms/ubuntu-VM$ qemu-img create disk.img -f qcow2 10G
```

> 提示 `qemu-img` 命令中指定的 `-f` 选项用于指定磁盘镜像格式。在这里我们使用 `-qcow2` 格式。这种格式通过不预先分配整个磁盘空间提供了节省空间的选项。相反，它会创建一个小文件，该文件会随着数据写入虚拟磁盘镜像而增大。另一个有趣的虚拟磁盘格式是 `-vmdk` 选项，它允许创建与 VMware 虚拟机兼容的虚拟磁盘。

6. 一旦创建了虚拟磁盘镜像，我们就可以通过向 kvm 直接传递必要的选项来启动虚拟机的安装程序。执行此操作的命令是：

```
yyang@ubuntu-server:~/vms/ubuntu-VM$ kvm -m 1024 \
-cdrom ubuntu-8.04-desktop-i386.iso \
-boot d disk.img
```

> 注意 传递给 `kvm` 命令的选项有：
> - `-m` 指定分配给虚拟机的内存量。在这种情况下，我们指定了 1024MB，即 1GB。
> - `-cdrom` 指定虚拟 CD-ROM 设备。在这种情况下，我们指向了早早下载并保存在当前工作目录下的 ISO 镜像。
> - `-boot d` 指定启动设备。在这种情况下，“d” 表示基于磁盘的。其他选项有软盘 (a)、硬盘 (c) 和网络 (n)。
> - `disk.img` 指定原始硬盘镜像。这是我们之前使用 `qemu-img` 创建的虚拟磁盘。

> 提示 由于在某些实例上发现图形化启动界面存在问题，你可能需要在使用用于启动向虚拟机中安装操作系统的 `kvm` 命令时添加 `-no-kvm` 开关。
