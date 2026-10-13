
### 20.2.2 Full Virtualization

完整虚拟化为未修改的来宾操作系统提供支持。术语“未修改”指的是未被修改以在 hypervisor 上运行的操作系统内核，因此仍像在 CPU 的 ring 0 中运行一样执行特权操作。在此场景中，hypervisor 提供 CPU 模拟来处理和修改未修改的来宾操作系统内核所进行的特权和受保护的 CPU 操作。不幸的是，此模拟过程需要时间和系统资源来运行，导致与准虚拟化提供的性能相比性能较低。

### 20.2.3 Hardware Virtualization

硬件虚拟化利用了英特尔和 AMD 最新一代 CPU 中内置的虚拟化功能。这些技术分别称为 Intel VT 和 AMD-V，提供了在不使用完整虚拟化 CPU 模拟固有开销的情况下运行未修改来宾虚拟机的必要扩展。用非常简化的术语来说，这些处理器提供了一个额外的特权模式（ring -1），位于 ring 0 之上，hypervisor 可以在此模式下运行，从而使 ring 0 可供未修改的来宾操作系统使用。

The following figure illustrates the Type-1 hypervisor approach to virtualization:

![](img/be1f159c3cc937d7b264dc5b134856dc_176_0.png)

Figure 20-3

如上图所示，除了虚拟机之外，管理操作系统或管理控制台也运行在 hypervisor 之上，使系统管理员能够管理虚拟机。

### 20.3 Virtual Machine Networking

虚拟机不可避免地需要连接到网络才能发挥实际用途。一个选项是让来宾连接到运行在主机计算机操作系统内的虚拟网络。在此配置中，虚拟网络上的任何虚拟机都可以相互看到，但网络地址转换（NAT）提供对外部网络的访问。当使用虚拟网络和 NAT 时，每个虚拟机在外部网络（主机所连接的网络）上都使用主机系统的 IP 地址表示。这是 RHEL 9 上 KVM 虚拟化的默认行为，通常不需要额外配置。通常默认会创建一个虚拟网络，用名称 `默认` 和设备 `virbr0` 表示。

为了使来宾在外部网络上作为独立的系统（即具有自己的 IP 地址）出现，它们必须配置为共享主机上的物理网络接口。实现此目的最快捷的方法是配置虚拟机以使用“direct connection”网络配置选项（也称为 MacVTap），这将为来宾系统提供与主机相同的网络上的 IP 地址。不幸的是，虽然这使虚拟机可以访问网络上的其他系统，但在使用 MacVTap 驱动程序时，无法在来宾和主机之间建立连接。

更好的选择是在主机系统上配置网络桥接接口，让来宾可以连接。这为来宾提供外部网络上的 IP 地址，同时也允许来宾和主机通信，该主题在题为“`创建 RHEL 9 KVM 网络桥接接口`”的章节中进行了介绍。

### 20.4 Summary

虚拟化是在单个主机操作系统内运行多个来宾操作系统的能力。已经开发了多种虚拟化方法，包括来宾操作系统和 hypervisor 虚拟化。Hypervisor 虚拟化分为两类，称为 Type-1 和 Type-2。Type-2 虚拟化解决方案分为准虚拟化、完整虚拟化和硬件虚拟化，后者使用某些英特尔和 AMD 处理器型号的特殊虚拟化功能。

虚拟机来宾操作系统在网络方面有多种选择，包括 NAT、直接连接（MacVTap）和网络桥接配置。

## Chapter 21

## 21. Installing KVM Virtualization on RHEL 9

RHEL 的早期版本提供了两种虚拟化平台：基于内核的虚拟机（KVM）和 Xen。在最近的版本中，Xen 的支持已被移除，使 KVM 成为随 RHEL 9 提供的唯一捆绑虚拟化选项。除了 KVM 之外，第三方解决方案也在 VMware 和 Oracle VirtualBox 等产品中提供。然而，由于 KVM 随 RHEL 9 提供，因此本章及后续章节将介绍此虚拟化解决方案。

在深入安装和运行 KVM 之前，值得讨论一下它如何适应上一章概述的各种虚拟化类型。

### 21.1 An Overview of KVM

KVM 被归类为 Type-1 hypervisor 虚拟化解决方案，使用 Intel VT 和 AMD-V 硬件虚拟化支持实现完整虚拟化并支持未修改的来宾操作系统。

KVM 与许多其他 Type-1 解决方案不同之处在于，它将主机 Linux 操作系统转变为 hypervisor，同时运行完整、企业级的主机操作系统，实现裸机虚拟化。

### 21.2 KVM Hardware Requirements

在继续本章之前，我们必须讨论在 KVM 环境中运行虚拟机的硬件要求。首先，KVM 虚拟化仅在特定处理器类型上可用。如前所述，这些处理器必须包含 Intel VT 或 AMD-V 技术。

要检查虚拟化支持，请在终端窗口中运行 `lscpu` 命令：

```
# lscpu | grep Virtualization:
```

如果系统包含支持 Intel VT 的 CPU，则上述命令将提供以下输出：

```
Virtualization:      VT-x
```

或者，当检测到支持 AMD-V 的 CPU 时，将显示以下输出：

```
Virtualization:      AMD-V
```

如果 CPU 不支持虚拟化，则上述 `lscpu` 命令不会显示任何输出。

请注意，虽然上述命令仅报告处理器是否支持相应功能，但它并不能表明该功能是否已在 BIOS 中启用。实际上，虚拟化支持通常在大多数系统的 BIOS 中默认被禁用。因此，在继续本教程之前，您应检查 BIOS 设置，以确保已启用适当的虚拟化技术。

与双启动环境不同，虚拟化环境涉及在单个计算机系统上同时运行两个或多个完整操作系统。这意味着系统必须具有足够的物理内存、磁盘空间和 CPU 处理能力，以便并行舒适地容纳所有这些系统。因此，在开始配置和安装过程之前，请检查 RHEL 9 和您选择的来宾操作系统的最低系统要求，并验证主机系统是否具有足够的资源来处理两个系统的要求。

### 21.3 Preparing RHEL 9 for KVM Virtualization

与 Xen 不同，不需要运行特殊版本的内核来支持 KVM。因此，通过安装 KVM 内核模块，KVM 支持已可与标准内核一起使用，从而消除了安装和启动特殊内核的需要。

然而，为了避免冲突，如果系统当前正在运行 Xen 启用的内核，请在继续本章剩余部分之前重新启动系统并从启动菜单中选择非 Xen 内核。

用于设置和维护基于 KVM 的虚拟化系统的工具仅在 RHEL 9 操作系统安装过程中明确选择时才默认安装。要从命令行安装 KVM 工具，请在终端窗口中执行以下命令：

```
# dnf install qemu-kvm qemu-img libvirt virt-install libvirt-client
```

如果您有权访问图形桌面环境，`virt-manager` 包也推荐安装：

```
# dnf install virt-manager
```

### 21.4 Verifying the KVM Installation

在继续之前，值得检查 KVM 安装是否正确完成。当 KVM 安装并运行时，将有两个模块加载到内核中。这些模块的存在与否可以通过在终端窗口中运行 `lsmod` 命令来验证：

```
# lsmod | grep kvm
```

假设安装成功，上述命令应生成类似于以下内容的输出：

```
kvm_intel      237568  0
kvm            737280  1 kvm_intel
irqbypass      16384  1 kvm
```

请注意，如果系统包含 AMD 处理器，`kvm` 模块可能显示为 `kvm_amd` 而不是 `kvm_intel`。

安装过程还应已配置 `libvirtd` 守护进程在后台运行。再次使用终端窗口，运行以下命令以确保 `libvirtd` 正在运行：

```
# systemctl status libvirtd
  libvirtd.service - Virtualization daemon
    Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)
    Active: active (running) since Wed 2019-03-06 14:41:22 EST; 3min 54s ago
```

如果进程未运行，可按如下方式启动：

```
# systemctl enable --now libvirtd
# systemctl start libvirtd
```

如果桌面环境可用，通过选择 Activities 并在搜索框中输入“virt”来运行 `virt-manager` 工具。当虚拟机管理器图标出现时，点击它以启动。加载后，管理器应如以下图所示出现：

![](img/be1f159c3cc937d7b264dc5b134856dc_181_0.png)

图 21-1
