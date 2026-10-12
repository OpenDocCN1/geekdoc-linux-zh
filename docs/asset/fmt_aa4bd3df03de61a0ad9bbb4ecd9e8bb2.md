
### 工作原理

如你所示，使用`pool-define`命令创建多个存储池很容易。每种类型的存储池都需要更多或参数。对于NFS存储池，我们需要指定NFS服务器和导出。这是通过指定`--source-host`和`--source-path`实现的。

创建网络稍微复杂一些，因为它要求你创建一个XML配置文件。当你想要透明地连接到你的物理网络时，你只能使用桥接网络，因为无法直接绑定到你的网络接口。

### 更多...

本教程创建的存储后端并不是限制。Libvirt还支持以下后端：

## 本地存储池

本地存储池直接连接物理机器。它们包括本地目录、磁盘、分区和LVM卷组。本地存储池并不企业，因为不支持实时迁移。

## 网络或共享存储池

网络存储池包括通过网络标准协议共享的存储，这在物理主机之间迁移虚拟机时是需要的。支持的网络存储协议包括基于光纤的LUN、iSCSI、NFS、GFS2和SCSI RDMA。

通过在`libvirt`中定义存储池和网络，我们确保了虚拟机可用资源。由于某种原因资源不可用，KVM将不会尝试启动这些资源的虚拟机。

查看`virsh (1)`的帮助页时，你会发现类似于`net-define`和`pool-define`的命令：`net-create`和`pool-create`（以及`pool-create-as`）。`net-create`命令类似于`pool-create`和`pool-create-as`，它创建瞬时的（临时）资源，这些资源在`libvirt`重启时将消失。另一方面，`net-define`和`pool-define`（以及`pool-define-as`）创建持久的（永久的）资源，它们在重启`libvirt`后仍然存在。

### 另请

你可以在<https://libvirt.org/storage.html>了解`libvirt`存储后端池。

关于`libvirt`网络的更多信息可以在<http://wiki.libvirt.org/page/Networking>处找到。

## 构建虚拟机

在主机系统上安装并创建KVM后，你就可以创建虚拟机操作系统。每个虚拟机都由一组存储在XML格式中的资源和参数定义。当你想要创建一个虚拟机时，创建这样的XML文件是非常繁琐的。创建虚拟机有两种方法：

- `virt-manager`
- `virt-install`

本教程将采用后者，因为它非常适合脚本，而`virt-manager`是一个GUI，不非常适合自动化操作。

### 准备工作

在本教程中，我们将涵盖一种通用方法，使用`bridge-eth0`网络桥接创建一个新的虚拟机，并在`localfs-vm`存储池上创建一个格式为QCOW2的虚拟磁盘。QCOW2格式是一种流行的虚拟磁盘格式，因为它允许精简配置和快照。我们将从位于`localfs-iso`存储池的RHEL 7安装介质（`rhel7-install.iso`）启动，开始安装新的RHEL 7系统。

## 创建虚拟机

让我们按照以下步骤为虚拟机创建一个磁盘并在磁盘上创建虚拟机：

- 在`localfs-vm`存储池中创建一个10 GB的QCOW2格式磁盘：

```bash
virsh vol-create-as --pool localfs-vm --name rhel7_guest-vda.qcow2 --format qcow2 --capacity 10G
```

- 使用以下命令创建并启动虚拟机：

```bash
virt-install \
--hvm \
--name rhel7_guest \
--memory=2048,maxmemory=4096 \
--vcpus=2,maxvcpus=4 \
--os-type linux \
--os-variant rhel7 \
--boot hd,cdrom,network,model=virtio-scsi \
--controller type scsi,model=virtio-scsi \
--disk device=cdrom,vol=localfs-iso/rhel7-install.iso,readonly=on,bus=scsi \
--disk device=disk,vol=localfs-vm/rhel7_guest-vda.qcow2,cache=none,bus=scsi \
--network network=bridge-eth0,model=virtio \
--graphics vnc \
--graphics spice \
--noautoconsole \
--memballoon virtio
```

## 删除虚拟机

在某些情况下，您需要移除虚拟机。可以按照以下步骤操作：

- 首先，运行以下命令确保虚拟机已关闭：

```bash
virsh list -all
```

| Id | Name | State |
|---|---|---|
| | `rhel7_guest` | `shut off` |

如果状态不是`shut off`，你可以强制将其关机：

```bash
virsh destroy --domain <guest name>
```

- 列出虚拟机正在使用的存储卷并将其复制到某处：

```bash
virsh vdomklist <guest name>
```

| Type | Device | Target | Source |
|---|---|---|---|
| `file` | `disk` | `vda` | `/vm/rhel7-guest-vda.qcow2` |
| `file` | `cdrom` | `hda` | `/iso/rhel7-install.iso` |

- 通过以下命令删除虚拟机：

```bash
virsh undefine --domain <guest name> --storage volume
```

在命令中添加`--remove-all-storage`会在从池中删除虚拟机之前，擦除该虚拟机专用存储卷上的数据。

### 工作原理...

`virt-install`命令支持通过指定大小、池和格式来创建存储卷（磁盘）。如果卷已存在，安装将失败。根据你的KVM机磁盘（本地或网络）的速度以及虚拟机磁盘的大小，创建`virt-install`新磁盘的过程可能需要一些时间。通过在`virt-install`指定现有磁盘，你可以重用该磁盘来重新安装虚拟机。可以仅在第一次创建磁盘，之后更改命令行以便对你想要的操作进行更细粒度的控制。

我们使用QCOW2格式来包含虚拟机磁盘，因为它是存储KVM虚拟机磁盘的流行格式。因为它支持精简配置（provisioning）和快照。

在创建虚拟机时，我们同时指定了内存配置的`memory`选项和vcpu配置的`maxcpu`选项。这允许我们在虚拟机运行时添加更多的CPU和内存。如果不这样做，我们必须在使用以下命令更改XML配置之前先关闭系统：

```bash
virsh edit <hostname>
```

如你所示，对于任何支持的硬件（网络、磁盘或气球），我们使用了`virtio`驱动，因为它是KVM原生的并包含在RHEL 7中。

> 如果由于某些原因，你的虚拟机操作系统不支持`virtio`驱动，你应该移除命令行中的`--controller`选项以及`--disk`选项中的`bus`规范。

有关`virtio`支持的更多信息，请访问<http://wiki.libvirt.org/page/Virtio>。

## 与 KVM 虚拟机一起工作

`--memballoon`选项将确保我们在进行内存超配（overcommit）时不会遇到问题。当特定虚拟机需要更多内存时，气球驱动程序将确保“空闲”虚拟机的内存可以被均匀重新分配。

`graphics`选项允许你通过主机使用VNC（一种流行的远程客户端）或`spice`（`virt-manager`的默认客户端）连接到虚拟机。VNC和`spice`的配置都是安全的，尽管你可以通过在每个`graphics`段落中添加`<password>`来设置密码，或者通过编辑KVM宿主机上的`/etc/libvirt/emu.conf`文件，后者将应用于所有虚拟机。

### 更多内容...

在本教程中，我们使用了ISO镜像形式的“本地”安装媒体来安装系统。然而，也可以在没有CD、DVD的情况下安装虚拟机，`--location`安装方法允许你指定一个包含内核/initrd对的URI，这是启动安装程序所必需的。

使用`--location`结合`--extra-args`允许你指定传递给安装程序的内核命令行参数。例如，这可以传递Anaconda kickstart文件的位置以便自动安装，和或指定你的IP配置。

## 第1章

确保客机的XML配置文件包含以下元素及相应的属性：

```xml
<domain type='kvm'>
...
```
