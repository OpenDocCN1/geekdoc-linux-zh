
```bash
# /sbin/mkbootdisk --verbose --device /dev/fd0 `uname -r`
grubby: bad argument --info: missing argument
Insert a disk in /dev/fd0. Any information on the disk will be lost.
Press <Enter> to continue or ^C to abort:
Formatting /dev/fd0... done.
Copying /boot/vmlinuz-2.4.20-2.48... done.
Creating initrd image... done.
Configuring bootloader... done.
```

这基本上是将内核和其他必需文件复制到软盘中，以便我们随时可以使用这张磁盘启动系统。

#### 工作原理

`/boot` 目录保存内核及相关文件。如果你查看该目录的内容，你会看到一个名为`vmlinuz-2.4.20-2.48`（或类似名称）的文件。这就是内核！

> 关于版本号的说明：如果你使用的是 Red Hat Linux 9，那么你的内核可能是 v2.4.20-2.48。在 Linux 内核的版本方案中，第一位数字（此处为 2）代表主版本，第二位数字（此处为 4）代表次版本。如果次版本号是奇数，则内核是测试版（beta）；否则，它来自发布/生产分支。第三个数字（此处为 20）是内核补丁号，最后一个数字是软件包号。

相比之下，Linux 可加载内核模块（LKMs）存储在目录`/lib/modules/2.4.20-2.48`中。如果你查看该目录的内容，你会发现这里有大量可用的模块。如果你想知道这里的确切模块数量，可以执行以下语句：

```bash
# find /lib/modules/\`uname -r\` -name '*.o' -print | wc -l
898
```

我们使用`find`命令来查找与系统内核相关的`/lib/modules`目录中所有的模块（即扩展名为`.o`的文件）。我们没有硬编码内核版本，而是使用带有`-r`选项的`uname`命令，该命令返回系统的内核版本。

现在，我们终于准备好开始使用内核了！

### 一个小型、精简的内核

我们将构建一个小型、精简的单体内核，它非常适合用于路由器和防火墙。与你在台式电脑或笔记本电脑上通常使用的“常规”内核不同，为路由器或防火墙设计的内核必须具备非常具体的特性：

- 它必须精简，以免占用大量资源。
- 它必须是单体的；它不应该具备加载或卸载模块的能力。
- 它应该禁用对任何热插拔设备、软盘驱动器和多媒体组件的支持。
- 应启用高级网络功能。

看到这些特性，你可能会想知道，例如，我们为什么要禁用对软盘驱动器的支持。我们当然不希望任何有可能物理接触此路由器或防火墙服务器的入侵者向我们的服务器引入任何文件或可执行程序。通过完全禁用软盘驱动器，我们就不必担心这种可能性了。

通过牢记这些特性，我们将得到一个精简、安全且针对网络性能优化的内核。让我们构建这个内核！

#### 动手实验：构建内核

1. 首先，我们需要将当前目录更改为`/usr/src/linux-2.4.20-2.48`：

```bash
# cd /usr/src/linux-2.4.20-2.48
```

2. 在那里，我们可以使用以下命令来运行基于 X 窗口的内核配置编辑器：

```bash
# make xconfig
rm -f include/asm
( cd include ; ln -sf asm-i386 asm)

make -C scripts kconfig.tk ...
cat tail.tk >> kconfig.tk
chmod 755 kconfig.tk
make[1]: Leaving directory `/usr/src/linux-2.4.20-2.48/scripts`
wish -f scripts/kconfig.tk
```

经过短暂等待，你会看到配置编辑器出现：

![](img/b852150740856958b10aff9e8c9d2adc_450_0.png)

如果你没有安装 X 窗口，你可以通过执行以下命令使用基于文本的编辑器：

```bash
# make menuconfig
```

正如你从下图中所见，基于文本的编辑器看起来有点不同，但支持所有相同的配置选项：

使用方向键浏览菜单。<Enter> 选择子菜单 --->。高亮显示的字母是热键。按 <> 包含，<N> 排除，<M> 模块化管理功能。按 <Esc><Esc> 退出，<?> 获取帮助。图例：[*] 内置 [ ] 排除 <M> 模块 < > 支持模块

- [*] 代码成熟度级别选项 --->
- [*] 可加载模块支持 --->
- [*] 处理器类型和功能 --->
- [*] 通用设置 --->
- [*] 存储器技术设备 (MTD) --->
- [*] 并口支持 --->
- [*] 即插即用配置 --->
- [*] 块设备 --->
- [*] 多设备支持 (RAID 和 LVM) --->
- [*] 加密支持 (CryptoAPI) --->

> 在本配置节的其余部分中，我们将使用 X 窗口配置编辑器。

3. 从配置编辑器中，你可以启用或禁用许多选项和内核模块。在此示例中，我们计划构建一个单体内核；因此，我们需要禁用可加载模块支持。为此，点击“可加载模块支持”按钮 – 这会弹出同名对话框。然后，在对话框中，将“启用可加载模块支持”设置从`y`更改为`n`：

**可加载模块支持**

| | y | n | 选项 | 帮助 |
|---|---|---|---|---|
| v | y | n | 启用可加载模块支持 | 帮助 |
| v | y | n | 在所有模块符号上设置版本信息 | 帮助 |
| v | y | n | 内核模块加载器 | 帮助 |

主菜单 下一个 上一个

> 如果你浏览其他一些选项，你会注意到在每个功能描述之前都有三个选项：`y`、`m` 和 `n`。点击`y`会启用该特定功能，选择`n`会禁用它。点击`m`选项会将该功能构建为可加载模块。

4. 这只是第一项设置。现在，浏览其余的配置 – 你可以使用**下一个**和**上一个**按钮从一个配置对话框切换到下一个。使用以下配方，它只列出了需要更改的设置；每个高亮显示的顶层部分代表内核配置中的一个主要部分/按钮：

##### 可加载模块支持

- 启用可加载模块支持 (N)

##### 处理器类型和功能

- 处理器家族 (选择处理器)
- 对称多处理支持 (N)

你只需在`/var/log/messages`日志文件的启动引导消息中搜索字符串“CPU:”，就可以确定你机器的处理器名称和类型，如下所示：

```bash
# grep CPU /var/log/messages
Feb 18 19:25:15 localhost kernel: Initializing CPU#0
Feb 18 19:25:15 localhost kernel: CPU: L1 I cache: 16K, L1 D cache: 16K
Feb 18 19:25:15 localhost kernel: CPU: L2 cache: 256K
Feb 18 19:25:15 localhost kernel: Intel machine check reporting enabled on CPU#0.
Feb 18 19:25:15 localhost kernel: CPU: Intel Pentium III (Coppermine) stepping 0a
```

让我们继续这份配方：

##### 通用设置

- 热插拔设备支持 (N)
- 内核对 MISC 二进制文件的支持 (N)
- 电源管理支持 (N)

##### 即插即用配置

- 即插即用支持 (Y)
- ISA 即插即用支持 (N)

##### 块设备

- 普通 PC 软盘支持 (N)

##### 网络选项

- 数据包套接字 (Y)
- 数据包套接字：映射 IO (Y)
- 网络数据包过滤（取代 ipchains） (Y)
- 套接字过滤 Y
- TCP/IP 网络 Y
    - IP：高级路由 Y
    - IP：策略路由 Y
    - IP：将 netfilter MARK 值用作路由键 Y
    - IP：快速网络地址转换 Y
    - IP：等价多路径 Y
    - IP：将 TOS 值用作路由键 Y
    - IP：详细路由监控 Y
    - IP：大型路由表 Y
    - IP：隧道封装 Y
    - IP：多播路由 Y
    - IP：支持 PIM-SM 版本 1 Y

##### IP：Netfilter 配置

- 连接跟踪（伪装/NAT 所必需） Y
- FTP 协议支持 Y
- IP 表支持（过滤/伪装/NAT 所必需） Y
    - 限制匹配支持 Y
    - MAC 地址匹配支持 Y
    - netfilter MARK 匹配支持 Y
    - 多端口匹配支持 Y
    - TOS 匹配支持 Y
    - AH/ESP 匹配支持 Y
    - LENGTH 匹配支持 Y
    - TTL 匹配支持 Y
    - tcpmss 匹配支持 Y
    - 连接状态匹配支持 Y
    - 数据包过滤 Y
    - REJECT 目标支持 Y
    - 完全 NAT Y
    - MASQUERADE 目标支持 Y
    - REDIRECT 目标支持 Y
    - 本地连接 NAT（阅读帮助） Y
    - 数据包修改 Y
    - TOS 目标支持 Y
    - MARK 目标支持 Y
    - LOG 目标支持 Y
    - ULOG 目标支持 Y
    - TCPMSS 目标支持 Y
    - ARP 表支持 Y
    - ARP 数据包过滤 Y

##### ATA/IDE/MFM/RLL 支持

- ATA/IDE/MFM/RLL 支持 Y

##### IDE、ATA 和 ATAPI 块设备

- CMD640 芯片组修复/支持 N
- RZ1000 芯片组修复/支持 N

##### SCSI 支持

- SCSI 支持 N

##### 网络设备支持

- 以太网 (10 或 100Mbit)
    - DECchip Tulip (dc21x4x) PCI 支持 Y

根据系统是否具有 IDE 或 SCSI 设备，启用或禁用适合您硬件的功能。您应该注意，CMD640 和 RZ1000 芯片组存在设计缺陷，可能会导致 486 和 Pentium 主板上的数据损坏。如果您使用的是较新的机器，可能可以禁用这些修复，如上所示。

此外，选择您的以太网卡并启用它，或者选择默认值。最后，如果您想支持 USB 设备，请启用以下选项：

##### 输入核心支持

- 输入核心支持 Y
- 键盘支持 Y
- 鼠标支持 Y

##### 字符设备

- 正在使用的 Unix98 PTY 最大数量 (0-2048) 8
- 直接渲染管理器 (XFree86 DRI 支持) N

##### 鼠标

- 总线鼠标支持 Y

##### 文件系统

- 内核自动挂载器版本 4 支持（也支持 v3） N
- Ext3 日志文件系统支持 Y

##### 网络文件系统

- NFS 文件系统支持 N
- NFS 服务器支持 N

##### 声音

- 声卡支持 N

##### USB 支持

- 初步 USB 设备文件系统 Y
- USB 人机接口设备（完整 HID）支持 Y
- HID 输入层支持 Y
- `/dev/hiddev` 原始 HID 设备支持 Y

5. 当您完成所有这些选项的设置后，单击“保存并退出”按钮以保存配置并退出编辑器。

6. 我们快要完成了；您只需再做一些更改。首先，我们必须编辑位于`/usr/src/linux-2.4.20-2.48`目录中的`Makefile`，通过更改分配给`EXTRAVERSION`变量的标识符，如下所示：

```
EXTRAVERSION = -2.48lean
```

其中`-2.48`对应于包号（内核标识符的最后部分：`2.4.20-2.48`），而`lean`是我们添加的，用于将此内核配置与其他配置区分开来。因此，我们的内核将作为`2.4.20-2.48lean`安装。

7. 接下来，我们需要创建一些空文件和一个与我们的内核相关的空`modules`目录，因为`Makefile`假定这些文件已经就位。否则，我们将看到编译时错误。

```bash
# touch drivers/pci/classlist.h drivers/pci/devlist.h
# mkdir /lib/modules/2.4.20-2.48lean
```

8. 我们准备好了！让我们构建我们的内核。第一步是在源代码中创建依赖项，以便为编译做好准备：

```bash
# make dep
make[1]: Entering directory `/usr/src/linux-2.4.20-2.48/arch/i386/boot`
make[1]: Nothing to be done for `dep'.
make[1]: Leaving directory `/usr/src/linux-2.4.20-2.48/arch/i386/boot'
scripts/mkdep -- init/*.c > .depend
..
make[1]: Leaving directory `/usr/src/linux-2.4.20-2.48'
(find /usr/src/linux-2.4.20-2.48 \( -name .depend -o -name .hdepend \) \
-print | xargs awk -f scripts/include_deps > tmp_include_depends
sed -ne 's/^\\([^.].*\\):.*/ \\1\\/p' tmp_include_depends > \
tmp_include_depends_1(echo ""; echo "all: \\\"; cat \
tmp_include_depends_1; echo "") >> tmp_include_depends
rm tmp_include_depends_1
```

9. 接下来，清理旧代码的残留、临时目标文件和其他不必要的文件：

```bash
# make clean
make[1]: Entering directory `/usr/src/linux-2.4.20-2.48/arch/i386/boot'
rm -f tools/build
rm -f setup bootsect zImage compressed/vmlinux.out
rm -f bsetup bbootsect bzImage compressed/bvmlinux.out
..
rm -f parport-share.png parport-multi.png parport-structure.png \
parport-share.eps parport-multi.eps parport-structure.eps
rm -f procfs_example.sgml
make[1]: Leaving directory `/usr/src/2.4.18-14/Documentation/DocBook'
```

10. 现在，构建内核：

```bash
# make bzimage
gcc -Wall -Wstrict-prototypes -O2 -fomit-frame-pointer -o \
scripts/split-include scripts/split-include.c \
scripts/split-include include/linux/autoconf.h include/config
make -r -f tmp_include_depends all
make[1]: Entering directory `/usr/src/linux-2.4.20-2.48`
make[1]: Leaving directory `/usr/src/linux-2.4.20-2.48`
gcc -D KERNEL -I/usr/src/linux-2.4.20-2.48/include -Wall \
-Wstrict-prototypes -Wno-trigraphs -O2 -fno-strict-aliasing \
-fno-common -fomit-frame-pointer -pipe -mpreferred-stack-boundary=2 \
-march=i686 -DKBUILD_BASENAME=main -c -o init/main.o init/main.c
...
tools/build -b bbootsect bsetup compressed/bvmlinux.out CURRENT > bzImage
Root device is (3, 5)
Boot sector 512 bytes.
Setup is 2536 bytes.
System is 821 kB
make[1]: Leaving directory `/usr/src/linux-2.4.20-2.48/arch/i386/boot`
```

11. 接下来，将新内核及相关文件安装到`/boot`：
