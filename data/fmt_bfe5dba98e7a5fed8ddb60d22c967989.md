
将所有内核复制到 `/boot` 目录是一个好主意。这个启动目录可以制成一个独立的分区。当你设置 Linux 机器时，可以将该分区设置为一个较小的（10MB）分区并将其挂载为 `/boot`。通过这种方式，你可以将硬盘移动到一台具有旧版 BIOS 的机器上，且无需进行任何更改即可启动。旧版 BIOS 对硬盘的限制约为 500MB。如果你使用较大的硬盘并按照上述方法进行设置，Linux 在旧系统上的启动方式将与在新系统上一样。

其原因是 Linux 没有硬盘限制，并且并不依赖 BIOS 来提供有关硬盘的信息。然而，`lilo(8)` 是由 BIOS 引导的，需要将内核放在 BIOS 可以看到的地方。一旦内核开始加载，Linux 就会接管，你将不再有任何限制。在某些使用旧版 BIOS 或安装到第三块硬盘的安装程序中，你可能需要为 `/boot` 目录预留一个小分区。

# /proc 目录

`Proc` 是一个虚拟目录；它实际上并不存在于硬盘上。它的所有信息都由内核维护。这是获取内核正在做什么信息的极佳来源。它还包含许多你可以调整的变量，以更改内核的行为。你应该花些时间查看 `proc` 目录。以下是存在的一些信息文件示例。

```
cat /meminfo
total: free: shared: cached:
Mem: 64651264 62717952 1933312 50225152 1527808 31232000
Swap: 3212048 1273856 3548192
MemTotal: 63136 kB
MemFree: 1888 kB
MemShared: 49048 kB
Buffers: 1492 kB
Cached: 30500 kB
SwapTotal: 36252 kB
SwapFree: 35008 kB
```

## cat /proc/cpuinfo

```
processor: 0
vendor_id: GenuineIntel
cpu family: 6
model: 6
model name: Celeron (Mendocino)
stepping: 5
cpu Idhz: 400.924148
cache size: 128 KB
fdiv_bug: no
hlt_bug: no
sep_bug: no
f00_bug: no
fpu: yes
fpu_exception: yes
cpuid level: 2
wp: yes
flags: fpu vme de pse tsc msr pace cex sep mtr pge mca cmov pat pse36
mmx osfxsr
nbogims: 399.77
```

# 内核重新编译与安装

有很多程序只需查看信息并以更易读的格式报告。更重要的是，有一些内核变量是可以修改内核行为的。以下是一些示例：

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

这将开启系统的转发功能，本质上使其成为一台路由器。

```
echo 1 > /proc/sys/net/ipv4/tcp_syncookies
```

这将启用 TCP SYN 数据包 cookie，从而防止你的系统遭受 SYN 洪水攻击。

```
echo "sbin/modprobe" > /proc/sys/kernel/modprobe
```

这将允许内核在 `kmod` 安装到内核中时找到 `modprobe`。`Kmod` 是内核的替代品，且内核会直接加载模块。你可以在 `rc.local` 文件中设置这些 `echo` 语句，以便快速方便地修改内核变量。

## 内核源码树与文档

内核源代码保存在 `/usr/src/linux` 目录。`/usr/src` 目录通常如下：

| 权限 | 链接 | 所有者 | 组 | 大小 | 日期 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| lrw-rw-rw | 1 | root | | | May 15 14:55 | linux -> linux-2.2.5 |
| drwxr-xr-x | 17 | root | | 1024 | May 15 19:48 | linux-2.2.5 |
| drwxr-xr-x | 7 | root | | 1024 | May 15 14:58 | redhot |

物理目录是 `linux-2.2.5`，有一个指向该目录的软链接。通过这种方式，你可以将硬盘移动到机器上。

| 权限 | 目录 |
| :--- | :--- |
| drwxr-xr-x | arch/ |
| drwxr-xr-x | Documentation/ |
| drwxr-xr-x | drivers/ |
| drwxr-xr-x | include/ |
| drwxr-xr-x | init/ |
| drwxr-xr-x | modules/ |
| drwxr-xr-x | net/ |

### 300 第 6 章：高级用户管理

数学仿真 (`CONFIG_MATH_EMULATION`) [Y/n?] n

MTRR（内存类型范围寄存器）支持 (`CONFIG_MTRR`) [Y/n?] n

对称多处理支持 (`CONFIG_SMP`) [Y/n?] n

#### 可加载模块支持

- +* 可加载模块支持

- 启用启用可加载模块支持 (`CONFIG_MODULES`) [Y/n?] y

在这里，您的变量列在括号中，答案在方括号中。默认答案是大写字母。如果您回答 `?`，则会看到一个解释该选项作用的帮助页面。如果直接按回车键（ENTER），将接受默认值。

创建 `.config` 文件的更好方法是使用 `menuconfig`。这要求您已安装 `curses`。这是一个基于文本的菜单驱动系统，使修改内核变得更加容易。要加载它，只需执行以下命令：

```
make menuconfig
```

屏幕显示如下：

```
Main Menu
方向键导航菜单。<Enter> 选择子菜单 ---->
高亮字母是热键。按 <Y> 包含，按 <N> 排除，
<M> 模块化功能。按 <Esc> 退出，<Q> 帮助。
图例: [* 内置 [ ] 排除 <M> 模块可用
代码成熟度级别选项 ---->
处理器类型和特性 ---->
可加载模块支持 ---->
通用设置 ---->
即插即用支持 ---->
块设备 ---->
网络选项 ---->
SCSI 支持 ---->
网络设备支持 ---->
业余无线电支持 ---->
Vi(+)
<Select>          < Exit          < Help >
```

Linux 内核 v2.2.5 配置

### 内核重新编译与安装 30I

`menuconfig` 的优越之处是它在 telnet 连接下运行良好。此外，菜单底部还有选项可以以备名保存 `.config` 文件，您在升级内核时可以使用它。

修改内核的最后一种方法是使用 X Windows。您可以通过使用 `xconfig` 使用一个图形化菜单系统来配置内核。图 6-9 显示了具体的选项。

您还有保存备用文件的能力。我们将在接下来的章节中显示子菜单的一些选项。

## 理解内核配置选项

您需要理解一些主要的内核配置选项。要了解更多信息，您几乎可以从上述配置脚本中选择帮助，以获得对特定选项的更详细描述。

图 6-9

xconfig 主菜单

![](img/d93cde4788f2827fc3c67c2526fc3dc0_342_0.png)

### 302 第 6 章：高级用户管理

#### 标准 Red Hat 内核配置

标准发行版内核支持几乎所有内容。几乎每个可以的模块都是如此。这是一个巨大的内核，标准安装中为其包含了大量的模块。这在安装时不是问题，但强烈建议精简发行版内核并移除不需要的模块。本章显示的所有 xconfig 均来自默认的 Red Hat 配置。

## 代码成熟度级别选项

如图 6-10 所示，代码成熟度级别选项用于对尚未完全开发的内核源码驱动程序启用提示。这些可以认为是 alpha 版本驱动程序。这些驱动程序通常尚未准备好供普通管理员广泛使用——开发者们基本上是在尝试接收电子邮件，告知他们仍有某些无法工作。

## 可加载模块支持选项

如图 6-11 所示，可加载模块支持界面是您启用在内核中使用模块的地方。您还有能够让内核为您加载模块的功能。这基本上是 `kerneld` 的替代品。在这里，内核会在需要模块时加载该模块。要使用此选项移除未使用的内核模块，您必须在 root 的 crontab 文件中设置 `rmmod -a`。要了解更多关于 `kmod` 的信息，请查看 `/usr/src/linux/Documentation/kmod.txt`。

![](img/d93cde4788f2827fc3c67c2526fc3dc0_343_0.png)

### 内核重新编译与安装 303

图 6-11 xconfig—可加载模块支持子菜单

![](img/d93cde4788f2827fc3c67c2526fc3dc0_344_0.png)

## 通用设置选项
