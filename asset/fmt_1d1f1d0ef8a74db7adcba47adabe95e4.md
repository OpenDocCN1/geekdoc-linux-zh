
# 使用终端

## 通过终端安装应用 – 第一部分

### 命令行安装

通过终端安装应用可能需要一些巧妙的键盘操作，但它可以让你对正在安装的内容及其安装位置有更好的了解。

- **步骤 1** 从终端安装应用相对简单。首先，你需要确保系统是最新版本。要执此此操作，请使用终端并输入：`sudo apt-get update && sudo apt-get upgrade`。
- **步骤 2** 正如你使用 `sudo apt-get update/upgrade` 一样，这些命令设计用于升级系统中已安装的软件。你要安装的应用比你想象的要多吗？恰好这非常简单。首先你需要一个要安装的应用，让我们用 Stella 为例。输入：`sudo apt-get install stella`。
- **步骤 3** 你需要输入 `y` 来确认安装，这将占用系统约 5MB 的存储。一旦 Stella 安装完成，你会发现 Mint 已自动在菜单中创建了“游戏”分类。
- **步骤 4** 有时在安装软件时，你需要添加应用的仓库（Repository）。仓库或简称 repo 是存放软件的最简单远程服务器位置，包含了软件及其所有的依赖项（运行所需的库和文件）。要执行此操作，请使用：`sudo apt-add-repository ppa:peterlevi/ppa`。按回车键添加该 PPA（个人包存档）。

```bash
davidsmith-mint$ sudo apt-get update && sudo apt-get upgrade

Reading package lists... Done

Building dependency tree... Done

Reading state information... Done

0 up./ubuntu-security 0 upgraded, 0 newly installed, 0 to remove and 0 failed to upgrade.

0 upgraded, 0 to upgrade.
```

```bash
davidsmith-mint$ sudo apt-add-repository ppa:peterlevi/ppa

Contains packages for variety changer

More info: https://launchpad.net/~peterlevi/archive/ubuntu/

Press Enter to continue or cancel.
```

#### 步骤 5 这为 Wallpaper Changer 添加了仓库，这是一个基于 Ubuntu 的应用，可以在 Mint 中自动更改壁纸。当仓库添加后，输入：`sudo apt-get update` 来更新软件包信息并添加到数据库。

```bash
sudo apt-add-repository ppa:variety-team/ppa

sudo apt-get update

sudo apt-get install variety
```

Setting up dependencies...

```
Reading package list...
Building dependency tree...
Reading state information...Done

The following packages will be automatically installed,
  variety

The following packages will be upgraded:
  0

The following packages will be removed:  0
```

```bash
sudo apt-get remove variety
sudo apt-get autoremove
```

## 删除应用

除了安装，apt 命令还可以用于删除应用并释放系统资源。

#### 步骤 1 要卸载应用，输入 `sudo apt-get remove variety`。按 `y` 继续卸载应用；你会注意到删除操作释放了多少磁盘空间。

#### 步骤 2 `apt-get autoremove` 命令会卸载应用，但不会移除它附带的额外内容，如配置和库文件。要完全删除应用，输入：`sudo apt-get purge`。

#### 步骤 3 当你从系统移除软件包时，某些包不再需要。通过 `sudo apt-get autoremove` 可以清理系统，然后按 `y` 接受该过程。

```
sudo apt-get remove variety

Reading package list...
Building dependency tree...
Reading state information...Done

The following packages were automatically installed and no longer required
  variety-*

The following packages will be removed:
  variety-common-*

The following packages will be installed:
  0

The following packages will be upgraded:
  0

The following packages will be removed:
  0

Do you want to continue? [Y/n]
```

#### 步骤 4 最后，为了清理系统中所有未使用的软件包并移除 autoremove 命令删除的元素，你可以输入：`sudo apt-get autoremove`。这些残留文件对于保持 Mint 设置良好以及关闭不必要的安装和升级至关重要。

```
sudo apt-get remove variety

Reading package list...
Building dependency tree...
Reading state information...Done

The following packages were automatically installed and no longer required
  variety-*

The following packages will be removed:
  variety-common-*

The following packages will be installed:
  0

The following packages will be upgraded:
  0

The following packages will be removed:
  0

Do you want to continue? [Y/n]
```

```
sudo apt-get purge variety

Reading package list...
Building dependency tree...
Reading state information...Done

The following packages were automatically installed and no longer required
  variety-*

The following packages will be removed:
  variety-common-*

The following packages will be installed:
  0

The following packages will be upgraded:
  0

The following packages will be removed:
  0

Do you want to continue? [Y/n]
```

```
sudo apt-get autoremove

Reading package list...
Building dependency tree...
Reading state information...Done

The following packages were automatically installed and no longer required
  variety-*

The following packages will be removed:
  0

The following packages will be installed:
  0

The following packages will be upgraded:
  0

The following packages will be removed:
  0

Do you want to continue? [Y/n]
```

## 通过终端安装应用 – 第二部分

大多数情况下，你会使用标准的 `apt-get` 命令从终端安装应用。然而，有时某些应用需要更多的工作。这意味着从其源码安装应用，这听起来并没有那么可怕。

### 从源码安装

你需要熟悉的命令有 `Configure`、`Make` 和 `Install`。你会发现很多应用都是从源码使用的，因此这是一项值得投入时间的技能。

步骤 1 Linux 源码文件通常以 `.TAR.GZ` 或 `.TAR.BZ2` 形式出现。两者都是包含“make” 所需所有代码的压缩文件。在 Home 目录下创建一个新文件夹开始本教程：`mkdir vim`。

步骤 2 顺便说一下，Vim 是一种高级文本编辑器，可以帮助我们编辑代码。`cd vim`，然后从互联网获取内容（此处为 Vim 的 BZ 文件），在新的 Vim 文件夹内，在终端输入以下命令：`wget ftp://vim.org/pub/unix/vim-7.4.tar.bz2`。

步骤 3 现在我们需要配置文件的内容，所以：在终端中输入 `tar -xf vim-7.4.tar.bz2`。你可以按 Tab 键自动填充文件名。

#### 步骤 5 如果你再次输入 `ls`，你会发现了一个了一个文件夹：`vim`：在 Mint 中用浅色文本表示文件夹。为主应用创建根文件夹总是更好的，因为当你使用这种方法升级 apt 时，每个单独的版本将会有它们自己的文件夹。

#### 步骤 6 输入 `cd vim` 进入文件夹，再次输入 `ls` 查看其内容。会有相当数量的文件；大部分是核心文件，其他应该应该是 `README` 或 `INSTALL`。阅读这些文件总是明智的，因为它们提供了关于安装的宝贵信息。

#### 步骤 7 安装的第一部分要求你配置系统以使用与应用关联的依赖项。`./configure`。如果你在编译组件时收到错误，该命令将生效。使用 `sudo apt install build-essential`。缺少了第三方应用 ncurses。正如我们提到的，你需要获取 `sudo apt-install libcurses5-dev ncurses-dev`。

#### 步骤 8 你可能需要继续安装依赖项。每安装一个依赖项后，运行 `sudo ./configure`，如果没有报告错误，即可继续安装的下一个阶段。你可能需要在网上搜索某些信息。

#### 步骤 9 成功执行 `./configure` 后，系统将创建一个 Makefile。这需要在终端中进行“make”。这可能需要一段时间时间，取决于应用的大小。

#### 步骤 10 最后，你需要在终端输入：`sudo make install`。这将安装应用，在这种情况下，你可以通过终端输入或通过 Dash 搜索来执行它。

# 使用终端

```
Kernel command line: block2mtd.block2mtd=/dev/hda2,131072.rootfs root=/dev/mtdblock0 roottype=jffs2 init=//etc/preinit noinittrd console=tty0 console=ttyS0,38408 reboot-bios

Found and enabled local APIC:

Enabling FPU save and restore... done.

Enabling unmasked SIMD FPU exception support... done.

Initializing CPU...

PID hash table entries: 32 (order: 5, 128 bytes)

Detected i686GP77+ MHz processor.

Console: colour VGA+0x25

console [tty0] enabled

console [tty0] enabled

Dentry cache hash table entries: 1024 (order: 0, 4096 bytes)

Inode-cache hash table entries: 1024 (order: 0, 4096 bytes)

Memory: 512K/812K available (1497k kernel code, 264k reserved, 597k data, 196k init, Ok highmem)

virtual kernel memory layout:

fixmap: 0xfffff9000 - 0xffffff (280 KB)

vmalloc: 0xc0000000 - 0xffff7000 (1007 MB)

lowmem: 0xc0000000 - 0xc07f0000 (7 MB)

.init: 0xc0313000 - 0xc0344000 (196 KB)

.data: 0xc0d27653c - 0xc030bbfc (597 KB)

.text: 0xc0010000 - 0xc027653c (1497 KB)

Checking if this processor honours WP bit in supervisor mode...Ok. Calibrating delay using timer routine (lp)=203810)
```

# Linux 内核

你可能知道吗...

```c
#include <linux/sched.h>

/*
 * 此模块实现了控制台 IO 函数
 * 希望这将是一个完整的实现。
 */

#include <linux/sched.h>
#include <linux/tty.h>
#include <asm/system.h>
#define SCREEN_START 0x0800
#define SCREEN_END 0x0000
#define LINES 25
#define COLUMNS 80
#define WIDTH 1
extern void interrupt(struct tty_queue *queue) {
    static unsigned long end=SCREEN_START;
    static unsigned long x,y;
    static unsigned long top=LINES;
    static unsigned long line,columns=COLUMNS;
    static unsigned long status=0;
    static unsigned char attr=0;
}
```
