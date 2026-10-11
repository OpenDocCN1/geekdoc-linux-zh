

- 空闲物理内存的量（free）
- 缓冲区使用的内存量（以 KB 为单位）（buff）
- 作为缓存使用的内存量（cache）
- 每秒换入磁盘的内存量（以 KB 为单位）（si）
- 每秒换出到磁盘的内存量（以 KB 为单位）（so）
- 每秒发送到块设备的块数（bi）
- 每秒从块设备接收的块数（bo）
- 每秒发送给 CPU 的中断次数（in）
- 每秒发送给 CPU 的上下文切换次数（cs）
- CPU 用户时间（us）
- CPU 系统时间（sy）
- CPU 空闲时间（id）
- 等待 I/O 的时间（wa）

因此，前面显示的 vmstat 输出表明没有使用交换内存，因为 swpd、si 和 so 均为零；然而，这也表明原因是当前系统没有运行大量进程（r=2, id=87）。

## 自定义内核

由于 Linux 内核与计算机硬件接口交互，您可以通过改变内核的工作方式提供额外的硬件支持或更改现有的硬件支持。这可以通过向内核插入模块或重新编译内核以整合不同功能来实现。或者，可能需要下载并编译一个新的内核以获得当前版本中不可用的某些硬件支持。此外，Linux 内核也会影响性能；重新编译内核以移除不必要内核特性会减小其大小并提高其速度。

### 内核模块

许多设备驱动和内核特性被编译进内核中；然而，这些也可以作为模块插入内核以减小内核的大小。将标准设备支持编译进内核，并将其他设备和特性的支持保留为模块是一种良好的做法。由于存在各种各样的声卡和网卡制造商，这些组件的驱动程序通常由可以插入内核的模块表示，而 IDE 硬盘支持则通常被编译进内核，因为它是如此经常被需要。

一些内核特性可以作为模块提供；这些模块必须手动插入内核。此外，如果 kudzu 未能正确检测新硬件，你需要将适当的模块加载到内核中以提供必要的硬件支持。

模块通常存储在 /lib/modules/<kernel-version> 目录的子目录中。例如，要查看 2.6.5-1.358 内核的网卡驱动模块的部分列表，你可以列出 /lib/modules/2.6.5-1.358/kernel/drivers/net 目录的内容。

```
[root@server1 root]# ls -F /lib/modules/2.6.5-1.358/kernel/drivers/net/
3c593.ko  r44.ko  forcethink.ko  ppp_async.ko  starfire.ko
3c503.ko  bonding/  hamachi.ko  ppp_deflate.ko  sundance.ko
3c505.ko  c899x0.ko  hpp100.ko  ppp_generic.ko  sungem.ko
3c507.ko  de600.ko  irda/  pppoe.ko  sungeem_phy.ko
3c509.ko  de620.ko  ixgb/  pppox.ko  sunhme.ko
3c515.ko  deppca.ko  lance.ko  ppp_synctty.ko  tg3.ko
3c59x.ko  dgns.ko  mii.ko  r8169.ko  tlan.ko
8139cp.ko  d12x.ko  natsemi.ko  rcp1.ko  tulip/
8139too.ko  dummy.ko  ne2k-pcl.ko  s2io.ko  tun.ko
82596.ko  e1000/  netconsole.ko  sk1000.ko  typhoon.ko
8390.ko  el100.ko  ni52.ko  sis900.ko  via-rhine.ko
ac3200.ko  epci100.ko  ni65.ko  sk98lin/  wd.ko
acenic.ko  eprol0.ko  ns83820.ko  skfp/  wireless/
amd8111e.ko  eql.ko  pcmcia/  slhc.ko  yellowfin.ko
appletalk/  ethertap.ko  pnetc32.ko  smc91.ko
atp.ko  fealnx.ko  plip.ko  smc-ultra.ko
```

前面输出显示的大多数文件具有 .ko 扩展名，这表明它们已编译并准备插入内核。

> **注意**
>
> 较旧内核中的模块，例如 2.4 内核，使用 .o 扩展名。

如果你的计算机中有一个 PCI NE2000 网卡，你可以使用 `insmod ne2k-pci` 命令将模块插入内核。`insmod` 命令不需要 /lib/modules/<kernel-version> 目录下模块的完整路径，因为它默认在那里搜索并找到 ne2k-pci.ko 文件，如前面输出所示。

或者，你可以使用 `modprobe ne2k-pci` 命令将模块插入内核。`modprobe` 命令检查并确保任何先决模块已首先加载，并在需要时加载它们，然后再加载指定的模块。

某些模块在插入内核时可能需要额外参数。例如，非 PnP ISA 网卡需要在模块名称旁边指定 IRQ 和 I/O 地址；要将此模块插入用于使用 IRQ 10 和 I/O 地址范围 0x300-31F 的网卡的内核中，你可以使用命令 `insmod module_name irq=10 io=0x300`。

> **注意**
>
> 如果关联设备不存在，`insmod` 和 `modprobe` 命令都会失败插入驱动模块。

要查看已插入 Linux 内核的模块列表，你可以使用 `lsmod` 命令：

```
[root@server1 root]# lsmod
Module Size Used by
nls_utf8 1536 0
nls_cp437 5376 0
vfat 10496 0
fat 33472 1 vfat
snd_mixer_oss 13824 0
snd 38372 1 snd_mixer_oss
soundcore 6112 1 snd
parport_pc 19392 1
lp 8236 0
parport 29640 2 parport_pc,lp
autofs4 10624 0
rfcomm 27164 0
l2cap 16004 5 rfcomm
bluetooth 33636 4 rfcomm,l2cap
sunrpc 101064 1
tulip 36256 0
floppy 47440 0
sg 27552 0
scsi_mod 91344 1 sg
microcode 4768 0
dm_mod 33184 0
cpia2_usb 5892 0
cpia2 36356 1 cpia2_usb
videodev 6656 1 cpia2
uhci_hcd 23708 0
ipv6 184288 8
ext3 102376 1
jbd 40216 1 ext3
[root@server1 root]# _
```

`lsmod` 命令也可以用于显示模块依赖关系；从前面输出中，`snd_mixer_oss` 模块需要 `snd` 模块，因为 `snd` 模块被 `snd_mixer_oss` 使用。

要从内核中移除模块，你可以使用 `rmmod` 命令。要移除前面输出中显示的 snd_mixer_oss 模块，你可以在命令提示符下使用命令 `rmmod snd_mixer_oss`。

通常，模块在启动时通过 /etc/modprobe.conf 文件中的条目使用 `modprobe` 命令自动插入内核；此文件的一个示例显示在以下输出中：

```
[root@server1 root]# cat /etc/modprobe.conf
alias eth0 tulip
alias usb-controller usb-uhci
[root@server1 root]# _
```

![](img/09bf13b782f71165e17bb3839040c96a_532_0.png)

> **注意**
>
> 较旧的 Linux 发行版通常在启动时从 /etc/modules.conf 或 /etc/conf.modules 文件中的条目加载模块。

前面的输出在启动时为 PnP Macronix 网卡加载 tulip 模块，并给予其 eth0 的别名。如果网卡不是 PnP，你还需要指定 IRQ 和 I/O 地址选项，如以下输出所示：

```
[root@server1 root]# cat /etc/modprobe.conf
alias eth0 tulip
options tulip irq=10 iO=0x300
alias usb-controller usb-uhci
[root@server1 root]# _
```

你可以编辑 /etc/modules.conf 文件并添加一行以在系统启动时加载特定模块，如果硬件未被正确检测或需要某些内核特性。或者，你可以将适当的 insmod 或 modprobe 命令放在 /etc/rc.d/rc.local 文件中，该文件在系统启动结束时执行，如第 9 章所述。

### 编译新的 Linux 内核

为了获得某些硬件或内核支持，可能需要重新编译当前内核以包含不同功能，或下载更新内核的源代码并编译它。

内核源代码存储在 /usr/src/<kernel-version> 目录下。当前内核版本的源代码存在于此目录下。你可以选择下载更新内核的 tarball 格式源代码，并将 tarball 放置在 /usr/src 目录中。提取后，会在 /usr/src 下创建相应的 <kernel-version> 目录。无论你重新编译的是当前内核版本还是新版本，剩余步骤是相同的。下一步是创建一个名为 /usr/src/linux 的符号链接，指向...

