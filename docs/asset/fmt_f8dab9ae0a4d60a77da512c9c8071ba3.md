
输出末尾的数字）。在客户机和主机上使用相同的 GPU 会导致问题，因为这些 ID 是相同的（请查阅 Arch wiki 以获取解决方案指导）。为了直通你的 GPU 和音频设备，我们需要创建一个包含以下内容文件 `/etc/modprobe.d/vfio.conf`：

```
options vfio-pci ids=1002:67b0,1002:aa8b
```

为了让这个魔法起作用，我们需要在 initramfs 中加载 VFIO 模块。在 Ubuntu 上，这是通过 `/etc/initramfs-tools/modules` 文件完成的；而在 Arch 上（顺便说一下，我们使用的是 Arch），我们需要编辑 `/etc/mkinitcpio.conf` 中的 `MODULES` 行。无论如何，请添加四个模块 `vfio`、`vfio_iommu_type1`、`vfio_pci` 和 `vfio_virqfd`，以确保它们出现在任何与视频相关的模块之前。通常情况下，这里可能根本没有任何模块，除非你设置了早期 KMS 或某种模式设置。现在，我们在 Ubuntu 上使用 `sudo update-initramfs -u` 或在 Arch 上使用 `mkinitcpio -k` 重新生成 initramfs。重启后，检查以下命令的输出：

```
$ dmesg | grep -i vfio
希望你会看到一些令人更安心的诗句：
[  1488571] VFIO - User Level meta-driver version: 0.3
[  1489469] vfio-pci 0000:01:00.0: vgaarb: changed VGA decodes: olddecodes=+io+mem,decodes=io+mem owns=none
[  1504260] vfio-pci idd [1002:67b0|ffffff]: class 0x000000/00000000
[  1520925] vfio-pci idd [1002:aa8b|ffffff]: class 0x000000/00000000
[  5429259] vfio-pci 0000:01:00.0: vgaarb: changed VGA decodes: olddecodes=+io+mem,decodes=io+mem owns=none
```

这可能不是你看到的内容，而且这可能也不是世界末日。检查以下命令的输出：

```
$ lspci -nnk -d 1002:67b0
```

根据实际情况更改供应商-设备对。这将显示 VFIO 驱动程序是否正确绑定到该设备。

### 公正但顽固的固件

为了让任何这些功能正常工作，直通 GPU 必须支持 UEFI，并且虚拟机必须配置为使用 UEFI 启动。开放虚拟机固件（OVMF）是 Intel TianoCore（也称为 EFI 开发套件 II，或 edk2）UEFI 固件的移植版本，它允许虚拟机享受 UEFI 带来的好处。使用 `sudo apt install ovfmf` 安装它。我们假设你已经从上一节中获取了 QEMU、`Libvirt` 和 `virt-manager` 软件包。我们需要告诉 `Libvirt` 在哪里找到此固件，这需要向 `/etc/libvirt/qemu.conf` 添加一行。在此文件中搜索 `nvram`，你会找到一些解释，并在这些注释下方添加这一行：

```
nvram = [
 "/usr/share/OVMF/OVMF_CODE.fd:/usr/share/OVMF/OVMF_VARS.fd"
]
```

这是针对 Ubuntu 的。在 Arch 上，请将路径更改为 `/usr/share/edk2/x64/`。最后，我们准备好在 `virt-manager` 中设置虚拟机了。这遵循与之前相同的流程，只是使用 Windows ISO（你可以从 Microsoft 下载）。当你到达向导的最后阶段时，请务必勾选“自定义”复选框，这样你就可以选择 UEFI 启动（参见右侧截图）。由于篇幅所限，我们不会对安装 Windows 说太多——我们相信你能搞定——但请设置一个 VirtIO SCSI 磁盘，如果磁盘 I/O 拖慢了速度，请尝试关闭缓存进行实验。安装完 Windows 后，我们可以将其关机并设置直通魔法。

从虚拟机的详细信息对话框中，点击“添加硬件”，选择“PCI 主机设备”，并选择我们之前检查过的 IOMMU 组中的所有设备。直通 USB 键盘和鼠标也是个好主意，但这些需要与你用来控制主机的键盘和鼠标分开。不再需要虚拟设备（Spice 通道、QXL 视频适配器、模拟外设），这些可以删除。现在是真刀真枪的时刻：启动虚拟机，插入（或切换显示器输入）直通 GPU 和键盘，敲几下按键，希望你会启动进入 Windows。这是我们从未想过自己会说的一句话！

![](img/7a0a282248f9658f0c87e55744c797b6_74_0.png)

### 硬件要求

为了让这些技巧奏效，需要一些大致上现代的硬件，即使拥有现代硬件，有时也会出现错误。主机使用的显卡可以是任何显卡，甚至是集成显卡。如果你有俩个独立 GPU，那么你需要熟悉进入 BIOS/UEFI 的关键组合，因为你的机器几乎肯定会尝试从错误的显卡启动。客户机的显卡需要支持 UEFI（主板不需要），因为我们要使用 OVMF 进行启动。有可能制造商提供了更新的 GPU BIOS（有些人报告说只需询问即可成功），你可以将此 BIOS 传递给 QEMU，而不是刷写你的显卡。一般来说，2012 年后制造的任何东西都没问题。你的主板必须支持 IOMMU（也称为 Directed I/O），这可能需要在 BIOS 中启用，并且你的 CPU 也必须支持它（Intel 称之为 VT-d，AMD 称之为 AMD-Vi；请注意，这些是在之前提到的更常见的 VT-x 和 AMD-V 之外的额外功能）。

除了这些要求之外，你可能希望投资购买一个 KVM 切换器（与内核无关）或额外的键盘/鼠标/触摸板设备（在 VNC 或 SPICE 连接之外）。客户机无法访问主机输入设备。你可以直通 USB 设备，但如果客户机出错，它们可能不会被释放，这将使你无法控制主机。如果你不喜欢来回更换线缆，那么你需要一个具有多个输入端口的显示器（以及另一根视频线），或者第二个显示器。如果你使用 Nvidia 显卡，可能会遇到可怕的“错误 43”，可以通过调整 QEMU 设置来解决。

### 更多操作

### 深入容器世界

管理你的应用程序，运行一个邮件服务器，并享受一段美好的时光。

![](img/7a0a282248f9658f0c87e55744c797b6_75_0.png)

那些自豪地被称为 Linux 老手，或者曾经使用实时光盘修复损坏的 Linux 安装的朋友，将熟悉 `chroot` 命令。这会更改当前 shell 的根目录，如果进入一个包含 Linux 安装的目录，实际上就进入了该目录。只要你先做一些绑定挂载的技巧，就可以使用 `/chroot` 目录中的所有软件库，同时使用正在工作的安装环境的内核和硬件。大多数桌面 Linux 安装程序就是这样工作的。

如果你加入了一些相当复杂的内核技术（即使用 `cgroups` 进行资源管理和使用命名空间进行隔离），那么现代容器只是这一想法的自然进化。从另一个角度看，现代容器是你牺牲了一些虚拟机（VMs）的隔离性并放弃拥有完整操作系统的需求后得到的结果。这使得它们比虚拟机更具可移植性且更容易启动。从实用主义的角度来看，容器使应用程序能够以一致且轻量级的方式进行打包和部署。

### 安装 Docker

Ubuntu 仓库中有一个 `docker` 软件包，但它与容器毫无关系，它是一个用于老牌 WindowMaker 窗口管理器的码头小部件。要在 Ubuntu 18.04 上安装 Docker，你可以使用 Snap（可以直接从*软件中心*获取），或者添加 **Docker 仓库**。后者稍微麻烦一点，但比 snap 更新更及时，所以让我们这样做。首先确保所有内容都是最新的：

```
$ sudo apt update && sudo apt upgrade
```

然后安装一些 Apt 的附加组件和助手，并添加 **Docker GPG** 密钥：

```
$ sudo apt install git apt-transport-https ca-certificates curl software-properties-common
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

现在添加 **Docker Ubuntu 仓库**并更新软件包列表：

```
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
$ sudo apt update
```

最后，我们可以使用以下命令安装 Docker 社区版：

```
$ sudo apt install docker-ce
```

### 带有额外 moo 的邮件
