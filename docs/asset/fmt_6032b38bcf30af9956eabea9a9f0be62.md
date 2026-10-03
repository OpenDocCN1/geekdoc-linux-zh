
为了帮助你从零理解云技术，本节将说明现代云基础设施的一些基本构建模块。通过三台计算机，我将帮助你创建一个包含以下内容的设置：

- **虚拟机管理器 (Hypervisors)**：虚拟机管理器是一个直接运行在计算机硬件上的软件组件，允许你在其上运行其他多个计算机系统。这些其他系统被称为虚拟机 (VMs)。云基础设施可能有几十或数百个虚拟机管理器正在运行，并可能运行着数千个虚拟机。

- **虚拟机 (Virtual machines)**：你在 Linux 系统上运行的虚拟机可以是相同类型的 Linux 系统、不同的 Linux 系统、Windows 系统或任何与虚拟机管理器运行硬件兼容的类型系统。因此，我们在这里构建的虚拟机可能包括 Fedora、Ubuntu、CentOS、RHEL、Microsoft Windows 等。

- **共享存储 (Shared storage)**：为了提供最大的灵活性，虚拟机管理器为虚拟机提供的存储通常在虚拟机管理器组之间共享，以共享一组它们用于安装或启动虚拟机的镜像。它还允许同一组虚拟机运行在组内的任何虚拟机管理器上，甚至在不关闭虚拟机的情况下移动到另一台虚拟机管理器上。如果虚拟机管理器负载过高或需要为了维护而关闭，迁移虚拟机将非常有用。

我们在接下来的步骤中构建的设置允许你以以下方式与虚拟机协同工作：

- 在虚拟机管理器上安装虚拟机
- 在你的虚拟机上设置功能
- 登录并使用运行在虚拟机管理器上的虚拟机
- 将运行中的虚拟机迁移到另一台虚拟机管理器

我们将探索以下技术：

**基于内核的虚拟机 (KVM)**：KVM 是允许虚拟机与 Linux 内核交互的基本内核技术。

**QEMU 进程仿真器**：系统上的每个活动虚拟机都会运行一个 `qemu` 进程。QEMU 提供了相关功能，使得每个虚拟机看起来都像是运行在物理硬件上一样。

**libvirt 服务守护进程 (libvirtd)**：每个虚拟机管理器上都运行着 libvirt 服务。`libvirtd` 守护进程监听启动、停止、暂停以及其他管理虚拟机管理器虚拟机的请求。这些请求可能来自设计用于管理虚拟机的应用程序（如 `virt-manager` 或 OpenStack Dashboard），也来自你创建的直接与 libvirt API 通信的应用程序。

**虚拟机管理器 (Virtual Machine Manager)**：虚拟机管理器 (`virt-manager` 命令) 是用于管理虚拟机的图形界面。除了允许你请求启动和停止虚拟机外，`virt-manager` 还允许你以不同的方式安装、配置和管理虚拟机。你可以使用 `virsh` 命令向命令行传递选项来处理虚拟机，而不是在 GUI 窗口中点击。

**虚拟机查看器 (Virtualization Viewer)**：虚拟机查看器 (`virt-viewer` 命令) 在你的桌面上启动一个控制台窗口。出现的窗口允许你从控制台进行操作（取决于虚拟机需要做什么）。这意味着你的虚拟化平台可以将操作系统、应用程序和配置文件打包在一起部署。

下一节将让你接触 Linux 云的一些基础技术。它描述了如何通过配置虚拟机管理器、虚拟机和存储来设置小型云。

## 设置小型云

通过在网络上连接三台物理机器，你可以演示构建你自己的云所需的基本概念。运行 Fedora 42 的三台计算机以及连接它们的网络配置如下：

- **网络**：建立了一个高速有线网络来连接三台计算机。快速的网络对于成功的虚拟机迁移至关重要。在示例中，每个虚拟机管理器还配置了网桥，以便每个虚拟机可以直接从网络上的 DHCP 服务获取 IP 地址。

- **虚拟机管理器**：两台计算机被配置为虚拟机管理器。虚拟机管理器（有时称为主机节点）允许你运行虚拟机。在 Fedora 42 中，常用的虚拟机管理器技术被称为基于内核的虚拟机 (KVM)，而实际虚拟机由 libvirt 服务管理。

- **存储**：一台计算机被配置为两个虚拟机管理器之间提供共享存储。为了简单，使用了 NFS 创建共享存储，但在生产环境中，ISCSI 或光纤应该是更好的解决方案。

> 为了目的，你可以使用两个虚拟机管理器之一提供共享存储。然而，配置两个虚拟机管理器和独立的共享存储的主要目的之一是你能够关闭任何虚拟机管理器，同时让所有的虚拟机正常运行。如果共享存储是从其中一个虚拟机管理器提供的，你就无法在不关闭使用该存储的所有虚拟机的情况下关闭该虚拟机管理器。

## 第 28 章：使用 Linux 进行云计算

## 配置虚拟机管理程序

在接下来的过程中，我在两台物理计算机上安装了 Fedora 42 Server（包含 GNOME 桌面），并将它们配置为运行 `libvirtd` 服务的 KVM 主机。请按照以下步骤完成操作。

### 第 1 步：获取 Linux 软件

访问 Fedora 项目页面（https://fedoraproject.org）并下载最新的 Fedora Server。我选择下载了 Fedora 42 64位 Server DVD ISO。如果可用更高版本的 Fedora，你可能也可以使用该版本。

使用如 Fedora Media Writer 等应用程序（也可从 https://fedoraproject.org 获取）将镜像写入 USB 驱动器。

### 第 2 步：检查你的计算机

在 Fedora 42 中，你用作虚拟机管理程序的计算机需要满足几项要求。在开始安装之前，你应该在计算机上检查以下内容：

- **支持虚拟化**。你可以通过查看 CPU 中的标志位（flags）来检查是否支持虚拟化。
- **内存**。计算机必须有足够的 RAM，不仅要运行主机操作系统，还要满足你预计在系统上运行的每个虚拟机的需求。
- **处理能力**。记住，每台虚拟机都会自身以及虚拟机内部运行的任何程序消耗处理能力。

存储是另一个考虑因素。但由于我们打算从网络上的独立节点配置存储，稍后我们会处理该问题。

要检查计算机的所有功能是否符合要求，请启动 Linux CD 或 DVD，打开终端并运行以下命令：

```bash
# cat /proc/cpuinfo | grep --color -E "vmx|svm|lm*"
flags : fpu vmme de tsc pse tsc msr mce cx8 apic sep mtr pge ca cmov pavat p36 clflush dt acpi fxsr sse sse2 si ht tm mype syscall nx pddeglb rdscp constant_arch perfmon pebs repclmulqd dtes64 rep_good xtopology nonstop_arch apermfperf pnlquad monitor ds_cpl vmx smx es...
```

运行上述命令显示这台计算机是 64 位计算机 (`lm`)，且 Intel 芯片支持虚拟化功能 (`vmx`)。如果 CPU 是支持虚拟化的 AMD 芯片，你将看到 `svm` 被高亮。这些设置表明这台计算机可以作为虚拟机管理程序。

在主机上启动虚拟机时，内存通常是瓶颈。对于内存需求，你必须将主机所需的内存加到每个虚拟机所需的内存上。你可以通过不安装桌面软件来降低内存需求，大多数虚拟机管理程序都是这样做。

在这种情况下，我执行了 Fedora Server 安装，然后添加了 GNOME 桌面。为了检查计算机上的内存和交换分区，我输入了：

```bash
# free -m
total used free shared buff/cache available
Mem: 15318 4182 6331 1047 4805 9678
Swap: 7743 0 7743
```

该系统拥有 16GB RAM 和 8GB 交换分区。我估计 4GB 对于主机系统（包括添加的 GNOME 桌面）是足够的。如果我为每个虚拟机分配 1GB 或 2GB，该系统应该能够带桌面运行 6-12 台虚拟机。检查你计划运行的操作系统和应用程序的内存需求，以确定你的内存需求。

要检查计算机上处理器的数量和类型，我输入了：

```bash
# grep processor /proc/cpuinfo
processor : 0
...
processor : 4
processor : 5
# head /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 158
model name : Intel (R) Core (TM) i5-8500CT @ 2.10GHz
stepping : 10
```

上述代码中的第一个命令显示计算机上有六个（0 到 5）处理器。针对第一个处理器的第二个命令显示它是 GenuineIntel，并列出了型号数字、型号名称、CPU 家族以及其他信息。

要在两个虚拟机管理程序之间进行热迁移，CPU 必须属于同一家族。如果它们没有兼容的 CPU，你可以通过在一台主机上关闭虚拟机并在另一台的共享存储上启动它来迁移虚拟机。

评估完两台虚拟机管理程序的配置后，开始在它们上安装 Fedora。

### 第 3 步：在虚拟机管理程序上安装 Linux

使用 Fedora 42 安装介质开始安装两台虚拟机管理程序。安装 Fedora 请参考第 9 章“安装 Linux”中的描述。你需要了解以下针对本过程的特定要点：

- **命名虚拟机管理程序**：我将虚拟机管理程序的主机设置为 `host1.example.com` 和 `host2.example.com`。
- **分区**：在分区时，我删除了整个硬盘。然后我创建了一个 500MiB 的 `/boot` 分区和一个 12GiB 的交换分区，并将磁盘的剩余空间分配给根分区 (`/`)。`/var/lib/libvirt/images` 目录存储了该系统的大部分数据，但它是一个共享目录，可以从网络上的另一个系统访问，并在两个虚拟机管理程序之间共享（稍后详述）。
- **网络**：在允许的情况下，为每个虚拟机管理程序开启有线网络接口。
- **软件**：然而，安装后，我执行了 Fedora Server 安装，然后添加了 GNOME 桌面。为了检查计算机上的内存和交换分区，我输入了……

## 第 28 章：使用 Linux 进行云计算

对于 Ubuntu 和类似的系统，输入以下命令：

```bash
# apt-get install nfs-kernel-server
```

## 第 2 步：配置 NFS 共享

要创建一个 NFS 共享，你需要标识要共享的目录并在 `/etc/exports` 文件中添加相关信息。按照以下步骤操作：

1. **创建目录。** 你可以共享任何包含你想要共享的空间目录。考虑创建一个新目录并在上面挂载磁盘或分区。在本例中，我按照如下方式创建了一个名为 `/var/storage` 的目录：

```bash
# mkdir -p /var/storage
```

2. **允许导出。** 在你的存储系统上，在 `/etc/exports` 文件中创建一个条目，与选定的系统（通过名称或 IP 地址）共享该目录。在本例中，我允许所有系统读写访问 (`rw`)（这是出于测试目的，生产环境中应确保永久生效）：

```
/var/exports * (no_root_squash,rw,sync)
```

3. **导出目录。** 在存储系统上，导出共享的目录：

```bash
# exportfs -a
```

## 第 3 步：启动 NFS 服务

启动 NFS 服务并打开存储系统上的防火墙以允许访问该服务。操作方法如下：

1. **启动并启用 NFS。** 在最新版本的 Fedora 和 RHEL 系统上，输入以下命令启动 nfs 服务器：

```bash
# systemctl start nfs-server.service
# systemctl enable nfs-server.service
```

2. **打开防火墙。** 为了打开防火墙端口以便本地系统之外可以使用你的 NFS 共享，请在 Fedora 42 上执行操作：

```bash
# firewall-cmd --permanent --add-service=rpc-bind
# firewall-cmd --permanent --add-service=nfs
# systemctl restart firewall
```

## 第 4 步：在虚拟机程序上挂载 NFS 共享

登录到每个虚拟机程序并按照这些步骤使共享在本地可用。请注意，每个虚拟机程序上挂载点目录的位置必须相同。操作方法如下：

1. **检查 NFS 共享的可用性。** 从两个虚拟机程序中的每一个，通过输入以下内容确保你可以看到可用的共享：

```bash
# showmount -e storage.example.com
Export list for storage.example.com:
/var/storage *
```

2. **挂载 NFS 共享。** 将有关共享的信息添加到 `/etc/fstab` 文件中。对于我们的示例，为了允许来自 `storage.example.com` 的目录在每次系统启动时都挂载到本地相同的目录，`/etc/fstab` 文件可能看起来所示：

```
storage.example.com:/var/storage /var/lib/libvirt/images nfs defaults 0 0
```

3. **设置 SELinux 布尔值。** 如果 SELinux 处于强制模式，设置以下布尔值 `virt_use_nfs` 以使用 NFS 共享：

```bash
# setsebool -P virt_use_nfs 1
```

4. **测试 NFS 挂载。** 为了检查挂载条目是否正确，运行以下命令挂载 `/etc/fstab` 中尚未挂载的所有条目，并检查 NFS 共享是否已挂载：

```bash
# mount -a
# grep libvirt
storage.example.com:/var/storage /var/lib/libvirt/images type nfs4 (rw,relime,vers=4.0,size=1048576,wsize=1048576,namlen=255,hard,proto=tcp,port=0,timeo=600,retrans=2,sec=sys,clientaddr=192.168.0.1,local_lock=none,addr=192.168.0.138)
```

现在你的虚拟机程序和存储已经就绪，你可以开始创建你的虚拟机了。

## 创建虚拟机

虚拟机管理器 (`virt-manager`) 是创建第一台虚拟机的一个很好的工具。它会引导你完成虚拟机的安装和设置，并提供了一种查看和更改现有虚拟机状态的方法。

稍后当你了解了创建虚拟机的功能后，可以使用 `virt-install` 来创建虚拟机。`virt-install` 的优势在于你可以编写脚本或轻松地复制粘贴命令来创建虚拟机，而无需点击 GUI 窗口。

我选择下载一个 Fedora 42 Workstation DVD ISO 来为我的虚拟机安装操作系统。然而，如果你愿意，也可以安装许多不同版本的 Linux 或 Windows 作为你的虚拟机。

## 第 1 步：获取制作虚拟机的镜像

你可以通过许多方式创建虚拟机。通常，你从一个预构建的镜像（基本上是运行中的虚拟机的副本）开始，或者直接从 ISO 镜像安装到新的存储区域。我们将采取后者，从 Fedora 42 Workstation 安装 ISO 镜像创建一个虚拟机。

假设你已以 root 身份登录其中一个虚拟机程序，且 ISO 镜像位于当前目录，请将 ISO 复制到 `virt-manager` 用于存储的默认目录 (`/var/lib/libvirt/images`)：

```bash
# cp Fedora-Workstation-Live-42-1.1.x86_64.iso /var/lib/libvirt/images/
```

由于该目录被两个虚拟机程序共享，你可以进入该目录。
