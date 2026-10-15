
使用`Ubuntu`系统作为虚拟化主机，您可以在单台计算机上运行多个操作系统。您在主机上创建的系统称为虚拟机（`VM`）。虚拟机可以运行`MS Windows`、`Fedora`、其他`Linux`系统，或者几乎任何可以直接在主机计算机架构上运行的其他操作系统。安装虚拟机后，您可以像处理直接安装在计算机硬件上的操作系统一样处理它。值得注意的是，使用虚拟机，复制它们、将它们迁移到其他虚拟化主机以改善性能，或在主机无法操作时配置故障转移到另一主机都变得更加容易。也就是说，使用虚拟机，您可以更有效地利用您的计算机基础设施。

使用您的`Ubuntu`系统作为虚拟化主机，您可以开始构建一个随着您需要更多计算能力而可扩展的计算机基础设施。通过拥有多个主机，您还将能够迁移虚拟机以获得更好的性能，或者关闭那些利用率较低的主机。您可以使用基于内核的虚拟机（`KVM`）将`Ubuntu`配置为虚拟化主机。

那么，将`Ubuntu`作为虚拟化主机运行的最关键要求是什么？您需要确保拥有一个支持虚拟化的`CPU`。您还需要确保计算机有足够的资源来有效运行虚拟机。让我们看看如何检查我们的计算机，以确保我们有作为虚拟化主机运行的合适资产。

首先，检查`CPU`虚拟化支持。请注意，您系统上的处理器必须支持`Intel VT`技术或`AMD-V`虚拟化支持。`Ubuntu`的一个好处是，它有一个命令（即`kvm-ok`），您可以使用它来测试您的`CPU`是否支持虚拟化。您可以按照以下方式安装和使用此命令。

```bash
pswayam@pswayam-VirtualBox:~$ lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                1
On-line CPU(s) list:   0
Thread(s) per core:    1
Core(s) per socket:    1
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 60
Model name:            Intel(R) Core(TM) i5-4210M CPU @ 2.60GHz
Stepping:              3
CPU MHz:               2594.000
BogoMIPS:              5188.00
Hypervisor vendor:     KVM
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              3072K
NUMA node0 CPU(s):     0
pswayam@pswayam-VirtualBox:~$
```

## 资源

- 初学者极客：如何创建和使用虚拟机
  [http://bit.ly/1mFyDm5](http://bit.ly/1mFyDm5)

- 关于虚拟化的一切
  [http://bit.ly/29elxQ](http://bit.ly/29elxQ)

- 设置新的虚拟机
  [http://bit.ly/20eXfm](http://bit.ly/20eXfm)

`$ sudo apt-get install cpu-checker`
`$ sudo kvm-ok`

上述命令的输出指示`CPU`是否支持`KVM`所需的相应`CPU`扩展。

请注意，实际上还有一种更手动的方法来检查虚拟化支持。你可以检查`/proc/cpuinfo`文件中设置的`CPU`标志。使用常用的`grep`命令，你可以在该文件中搜索`Intel-VT`支持(`vmx`)或`AMD-V`支持(`svm`)。可以按以下方式操作：

`$ grep -E'(svm|vmx)' /proc/cpuinfo`

在上述命令的输出中，你应该只看到`vmx`或`svm`标志，而不应两者同时出现。如果你没有从`grep`命令中得到任何输出，这意味着你的电脑`CPU`不支持`KVM`虚拟化。

接下来，你需要在`BIOS`中启用虚拟化支持。如果你认为你的电脑支持虚拟化，但相应的标志未设置，那么你可能需要在`BIOS`中打开虚拟化支持。为了做到这一点，首先重启你的电脑，并在看到第一个`BIOS`界面时中断引导过程。在你看到的`BIOS`界面中，寻找类似`CPU`或`Performance`（性能）的标题（具体因制造商而异）并选择它。然后你需要寻找诸如`Intel Virtualisation Tech`这样的虚拟化选项并将其启用。一旦你更改了虚拟化的`BIOS`设置，请保存并确保关闭电脑电源，以使`BIOS`设置生效。

如果可能，请尝试使用`64`位计算机作为你的虚拟化宿主。某些操作系统不支持在`32`位系统上使用`KVM`。`32`位`KVM`宿主机的一个缺点是，每个虚拟机限制为`2GB`内存。为了检查你的电脑是`32`位还是`64`位，你可以检查`CPU`标志。

`$ sudo egrep lm /proc/cpuinfo`

![](img/628186dda7facdc011bf39c938de3975_44_0.png)

`lm`标志代表长模式(`long mode`)。如果存在此标志，则可以肯定该处理器是`64`位处理器。

检查可用的`RAM`和磁盘空间。由于你将在一台物理计算机上运行多个操作系统，所需的`RAM`和磁盘空间量可能需要成倍增加。确保你有足够的内存来支持宿主机和你计划同时运行的所有虚拟机。你可以使用`free`命令来检查可用内存：

`$ free -m`

![](img/628186dda7facdc011bf39c938de3975_44_1.png)

在评估需要多少内存时，你可以使用如`top`等命令来了解你需要多少内存。

对于磁盘空间，你需要确保将存储虚拟机所使用的磁盘镜像的目录中有大量可用空间。默认情况下，该位置是`/var/lib/libvirt/images`。你可以尝试使用`df`命令来检查该位置的可用磁盘空间。

请注意，`/var/lib/libvirt/images`目录只有在安装`libvirt-bin`包后才会创建。因此，如果尚未安装，请使用`/var/lib`目录，如下所示：

`$ df -h /var/lib`

## 虚拟机概览

虚拟机可以被认为是一种创建虚拟计算机系统的计算机程序。这个虚拟计算机作为一个进程运行在你当前操作系统的一个窗口中。你可以在虚拟机内启动一个操作系统安装光盘（或`Live CD`），操作系统会被欺骗，以为它正在一台真实计算机上运行。它将像在真实的物理机器上一样进行安装和运行。每当你要使用该操作系统时，你可以打开虚拟机程序，并在当前桌面上的一个窗口中使用它。这里需要注意的是，虚拟机会带来一些开销，因此它们不会像将操作系统安装在真实硬件上那样快。

> “虚拟机可以运行`Windows`、`Fedora`、另一个`Linux`系统或几乎你想要的任何其他操作系统”

### 教程：虚拟化

为了能够执行`KVM`虚拟化，你需要添加三个软件组件。它们是：

- `libvirt` – 这为虚拟化软件提供接口
- `qemu` – 这为虚拟机模拟`PC`硬件
- `bridge-utils` – 这提供了一种通过宿主将虚拟机的网络进行网桥连接的方式

然后你可以运行以下`apt-get`命令，这样`KVM`虚拟化所需的基本软件就会被安装：

`$ sudo apt-get install libvirt-bin kvm bridge-utils qemu-common qemu-kvm qemu-tui`

除了`KVM`虚拟化所需的基本软件外，你还可以添加一个用于管理虚拟机的图形界面。使用以下命令安装用于管理虚拟机的`virt-manager`图形软件：

`$ sudo apt-get install virt-manager`

当`virt-manager`安装完成后，我们可以选择从图形界面或命令行来管理我们的虚拟机。在下一步中，我们需要确保我们要用来管理虚拟化的用户账户已配置好相应权限。

![](img/628186dda7facdc011bf39c938de3975_45_0.png)

如果你用来管理`KVM`的用户账户不是`libvirtd`组的成员，那么需要将该用户添加到该组中。例如，如果你想要用户账户`james`来管理虚拟化，那么你可以如下图所示将该用户添加到`libvirtd`组：

`$ sudo adduser james libvirtd`

你可能需要重启系统，以确保所有必要的服务都在运行，并且你添加到`libvirt`组的用户账户已登录并准备就绪。
