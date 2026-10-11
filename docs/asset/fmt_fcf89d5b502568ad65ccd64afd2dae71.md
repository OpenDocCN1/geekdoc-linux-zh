
客户机操作系统预期执行的所有指令都必须能够在完全虚拟化的操作系统安装中运行。这是因为没有额外的软件驱动程序安装在客户机内部，以将指令转换为模拟或真实硬件。完全虚拟化的客户机是指客户机（或 `HardwareVM`）不知道自己是一个正在运行的虚拟机实例的情况。为了使这种类型的虚拟化在基于 x86 的硬件上发生，必须在安装了 `Hypervisor` 的系统上启用 `Intel VT-x` 或 `AMD-V` CPU 扩展。这可以通过 BIOS 或 UEFI 固件配置菜单完成。

### 半虚拟化

半虚拟化客户机（或 `PVM`）是指客户机操作系统知道自己是一个正在运行的虚拟机实例的情况。这些类型的客户机将利用修改后的内核和特殊驱动程序（称为 `客户机驱动程序`），帮助客户机操作系统利用 `Hypervisor` 的软件和硬件资源。由于这些软件驱动程序提供的优势，半虚拟化客户机的性能通常优于完全虚拟化客户机。

### 混合

半虚拟化和完全虚拟化可以结合使用，通过使用半虚拟化驱动程序在完全虚拟化的操作系统上，使未修改的操作系统获得接近原生的 I/O 性能。半虚拟化驱动程序包含具有增强磁盘和网络 I/O 性能的存储和网络设备驱动程序。

虚拟化平台通常为虚拟化的操作系统提供打包的客户机驱动程序。`KVM` 使用 `Virtualio` 项目提供的驱动程序，而 `Oracle VM VirtualBox` 使用可从下载的 ISO CD-ROM 映像文件获得的 `Guest Extensions`（客户机扩展）。

### libvirt 虚拟机示例

我们将查看一个由 `libvirt` 管理并使用 `KVM Hypervisor` 的虚拟机示例。虚拟机通常由一组文件组成，主要是一个 `定义` 虚拟机的 XML 文件（例如其硬件配置、网络连接、显示能力等）以及一个包含操作系统及其软件安装的关联硬盘映像文件。

首先，让我们开始检查虚拟机的一个示例 XML 配置文件及其网络环境：

```bash
$ ls /etc/libvirt/qemu
total 24
drwxr-x-x 3 root root 4096 Oct 29 17:48 networks
-rw----1 root root 5667 Jun 29 17:17 rhe18.0.xml
```

> `注意` 目录路径中的 `qemu` 部分指的是基于 KVM 的虚拟机所依赖的底层软件。`QEMU` 项目提供用于...

`hypervisor` 会模拟虚拟机将要使用的硬件设备，例如磁盘控制器、对宿主机 CPU 的访问、网卡模拟等。

请注意，有一个名为 `networks` 的目录。此目录包含定义文件（同样使用 XML），用于创建虚拟机可使用的网络配置。此 `hypervisor` 仅使用一个网络，因此只有一个定义文件，其中包含这些系统将使用的虚拟网络段的配置。

```bash
$ ls -l /etc/libvirt/qemu/networks/
total 8
drwxr-x 2 root root 4096 Jun 29 17:15 autostart
-rw------ 1 root root  576 Jun 28 16:39 default.xml
$ sudo cat /etc/libvirt/qemu/networks/default.xml
<!--
  WARNING: THIS IS AN AUTO-GENERATED FILE. CHANGES TO IT ARE LIKELY TO BE
  OVERWRITTEN AND LOST. Changes to this xml configuration should be made using:
    virsh net-edit default
  or other application using the libvirt API.
-->

<network>
  <name>default</name>
  <uuid>55ab064f-62f8-49d3-8d25-8ef36a524344</uuid>
  <forward mode='nat'/>
  <bridge name='virbr0' stp='on' delay='0'/>
  <mac address='52:54:00:b8:e0:15'/>
  <ip address='192.168.122.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.122.2' end='192.168.122.254'/>
    </dhcp>
  </ip>
</network>
```

此定义包含一个 C 类私有网络和一个模拟硬件设备，充当该网络的路由器。还有一组 IP 地址范围，供 `hypervisor` 与 DHCP 服务器实现一起使用，可分配给使用此网络的虚拟机。此网络配置还利用网络地址转换 (NAT) 将数据包转发到其他网络，例如 `hypervisor` 的局域网。

现在我们将注意力转向一个 Red Hat Enterprise Linux 8 虚拟机定义文件。（特别值得注意的部分使用 `粗体` 文本）：

```bash
$ sudo cat /etc/libvirt/qemu/rhel8.0.xml
```
