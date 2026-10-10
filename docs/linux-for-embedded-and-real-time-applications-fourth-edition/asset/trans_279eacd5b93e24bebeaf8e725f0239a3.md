

## 资源

- www.busybox.net—这是 BusyBox 的官方网站。
- access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sect-Managing_Services_with_systemd-Unit_Files.html—非常详细的 systemd 文档。
- www.linux.com/learn/understanding-and-using-systemd
- www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal
- 这里有两篇关于从零开始构建最小化 BeagleBone Black 系统的博客文章。
- gist.github.com/sergeev/2391575
- www.bootembedded.com/embedded-linux/building-embedded-linux-scratch-beaglebone-black

## U-Boot 引导加载程序及发货准备

### 章节大纲

- **U-Boot** 233
  - **背景** 233
    - 安装和配置 U-Boot 234
    - 测试新的 U-Boot 236
    - “Sandbox”（沙箱） 237
    - 设备树 238
- **将应用程序放入 eMMC 闪存** 240
- **资源** 241

> *盒子上写着“需要 Windows 95 或更高版本”。于是，我安装了 Linux。*

### U-Boot

正如我们在前一章中所见，引导加载程序（boot loader）是一个在加载和运行操作系统及其支持基础设施之前执行某些初始化工作的程序。从某种意义上说，引导加载程序就像台式 PC 或服务器中的 BIOS（基本输入/输出系统）。主要区别在于，引导加载程序在系统启动时执行一次，然后就消失了。BIOS 会保留下来以提供低级 I/O 服务。

#### 背景

桌面 Linux 系统除了 BIOS 之外还有一个引导加载程序。如今，这通常是 GRUB，即 GRand Unified Bootloader（大型统一引导加载程序），或 GRUB2。但由于 BIOS 完成了初始化硬件的大部分繁重工作，GRUB 本身除了加载并启动操作系统外，几乎不做其他事情。如果你正在构建基于传统 x86 PC 硬件的嵌入式系统，GRUB 可能是不错的选择。

另一方面，我们的 BBB 目标板使用了一个非常流行、功能强大、开源且跨平台的引导加载程序来启动系统。我们在第 6 章《硬件》中首次启动目标板时，简要了解了一些 u-boot 的特性。

U-boot 最初是一个名为 8xxROM 的 PowerPC 引导加载程序，由 Magnus Damm 编写。随后，Wolfgang Denk 将该项目移至 Source Forge，并将其重命名为 PPCBoot。源代码曾被 Sysgo GmbH 分支为一个名为 ARMBoot 的产品。当 ARMBoot 分支合并回 PPCBoot 代码树时，名称改为 u-boot。如今，u-boot 支持大约十种架构和超过 1000 种不同的板卡。

u-boot 的开发与 Linux 紧密相关，二者共享一些头文件。部分源代码源自内核源码树。

U-boot 支持一套广泛的命令集，不仅有助于引导，还能管理闪存、通过网络下载文件等。附录 I 详细介绍了该命令集。该命令集通过环境变量和脚本语言进行了增强。

#### 安装和配置 U-Boot

当前版本的 u-boot 可从以下 git 仓库获取：

```
git clone git://git.denx.de/u-boot.git
```

顶级目录中有一个非常详尽的 README 文件。doc/ 目录中还有额外的 README 文件，主要描述特定板卡的功能。

还有一个针对 BeagleBoard 主线代码的补丁。请将你的网络浏览器指向：

```
https://rcn-ee.com/repos/git/u-boot-patches/
```

并选择与你从 git 获取的 u-boot 版本对应的子文件夹。将 0001-am335x_evm-uEnv,t-txtdoottz-n-fixes.patch 下载到你的 u-boot 目录。然后执行：

```
patch -p1 < 0001-am335x_evm-uEnv,t-txtdoottz-n-fixes.patch
```

在我的案例中，八个文件中有两个补丁应用失败，但手动修补起来相当简单。

当前的 u-boot 实现支持与 Linux 内核和 BusyBox 相同的 Kconfig 配置机制。同样，我们必须从默认配置开始。我下载的 u-boot 版本拥有超过一千种板卡的 _defconfigs。在我们的情况下，它是：

```
make am335x_boneblack_defconfig
```

接着执行：

```
make xconfig
```

图 15.1 是 u-boot 的顶级 xconfig 菜单。这表明已选择 ARM（Advanced RISC Machines）架构以及 TI OMAP2 + 变体。除了包含哪些命令外，你可能不需要更改太多其他内容。

![](img/f03d6fa2c5faefc793771df52bbb2ef9_239_0.png)

**图 15.1**

U-boot make xconfig。

你会注意到，xconfig 菜单中没有 `CROSS_COMPILE` 前缀，因此你必须编辑 `Makefile` 或在 make 命令中输入它。此外，我尚未找到 `Makefile` 中定义 `ARCH` 变量的位置，因此你必须在 make 命令行上指定它。你的 make 命令看起来如下：

```
make CROSS_COMPILE=arm-linux- ARCH=arm
```

我遇到了几个问题。我首次运行 make 时得到了此错误消息：

```
bad value (armv5) for -march = swit ch
```

谷歌没有为此找到什么有用的信息，至少不是关于 u-boot 的。在 `Makefiles` 中四处摸索后，我在 `arch/arm/Makefile` 中发现了这两行：

```
arch-$ (CONFIG_CPU_V7)          = $(call cc-option, -march=armv7-a, \
                                        $(call cc-option, -march=armv7, \
-march=armv5))
```

确实，`CONFIG_CPU_V7` 已设置，因此这些行会被添加到 gcc 命令行中。但为什么会有 `—march=armv5`？作为实验，我从第二行中移除了 “, -march=armv5”，make 成功执行。

另一个问题是你需要 python-devel 软件包。

make 步骤生成几个输出文件：

- `MLO`—次要程序加载器 (SPL)，用于将 u-boot 加载到 RAM 中
- `u-boot`—ELF 二进制格式的可执行文件。不清楚此文件的用途
- `u-boot.bin`—原始二进制映像，适合写入闪存
- `u-boot.nodtb.bin`—似乎与 `u-boot.bin` 相同
- `u-boot.img`—似乎是在 `u-boot.bin` 前面添加了 64 字节的 u-boot 头文件
- `u-boot.map`—链接器输出的映射文件
- `u-boot.cfg`—以 C 头文件形式表示的 `.config` 文件
- `u-boot.sym`—符号表
- `u-boot.srec`—Motorola S 记录格式的可执行文件

make 步骤还在 `tools/` 目录中构建了几个工具。

#### 测试新的 U-Boot

你最初希望在 RAM 中测试新的 u-boot，然后再将其烧录到闪存中。将 `u-boot.bin` 复制到 `/var/lib/tftpboot`。将 BBB 引导至 u-boot 并执行：

```
setenv ipaddr 192.168.1.50
setenv serverip 192.168.1.2
tftp 80800000 u-boot.bin
go 80800000
```

我们必须设置 `ipaddr` 和 `serverip`，因为这些通常不会在 u-boot 读取 `uenv.txt` 之前被设置。`go` 命令将控制权转移到指定的内存地址。除非你中断自动引导，否则新的引导加载程序应该开始执行并引导内核。

如果你碰巧有一个 JTAG（Joint Test Action Group）硬件调试器，也可以使用它。如果你进行了大量更改并确实需要测试新的 u-boot，这将很有用，因为这可能是在引导加载程序代码上使用断点的唯一方法。

#### “Sandbox”（沙箱）

如果你对 u-boot 的修改是架构无关的，有一种方法可以在你的工作站上进行测试。U-boot 提供了名为 “sandbox”（沙箱）的目标“板卡”，其理念源于我们在第 8 章《调试嵌入式软件》中探讨的模拟环境。沙箱将 u-boot 作为用户空间应用程序运行，允许你使用 Gnu DeBugger (GDB) 调试你的修改。要构建沙箱版本，你可能需要安装 `openssl-devel` 软件包。

默认情况下，沙箱需要一种名为 `libSDL` 的东西，SDL 代表 Simple DirectMedia Layer（简单直接媒体层）。u-boot 文档暗示这对于显示和键盘支持是必要的。据说该软件包名为 `libSDL-1.2-dev`，但我无法在 CentOS 存储库中找到它。通过在 make 命令中添加 `NO_SDL=1`，你可以在没有 SDL 支持的情况下构建沙箱。

但这还不是全部。你必须编辑 `include/configs/sandbox.h`。大约在第 104 行附近有这三行：

```
#define SANDBOX_NO_SDL
#define CONFIG_SANDBOX_SDL
#endif
```

将这些行注释掉。现在执行：

```
make NO_SDL=1
```

构建似乎成功了，但我在最后得到了以下消息：

```
./scripts/dtc-version.sh: line 17: dtc: command not found
./scripts/dtc-version.sh: line 18: dtc: command not found
*** Your dtc is too old, please upgrade to dtc 1.4 or newer
make: *** [checkdtc] Error 1
```

