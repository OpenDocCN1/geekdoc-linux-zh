
理想的方法是编辑`dosemu-HOWTO-xx.x.pgsql`来合并更改，通过输入类似命令创建`diff`：

```
diff --uw original-file new-file
```

并发送到`bon@elektron-ikp.physics.th-darmstadt.de <mailto:bon@elektron-ikp.physics.th-darmstadt.de>`。如果你不知道`SGML`，那也没关系。接受任何形式的新信息。创建`diff`只是为了方便`HOWTO`维护者。

### 1.11 来自来自

另有说明，`Linux HOWTO`文档版权归相应作者所有。`Linux HOWTO`文档可以在任何物理或电子媒介上全部或部分复制和分发，只要在所有副本上保留此版权声明即可。

# 1868

# 目录

简而言之，我们希望尽可能通过各种渠道传播这些信息。然而，我们希望保留`HOWTO`文档的版权，并希望对任何重新分发`HOWTO`的计划获得通知。

如果你有任何问题，请联系`Linux HOWTO`协调员`Greg Hankins`，邮箱：`gregh@cc.gate.edu` (95/8/1)。

## 2 编译与安装 dosemu

### 2.1 安装指南在哪里？

安装指南位于发行版包含的`QuickStart`文件中。

### 2.2 编译和安装 dosemu 时遇到的十大问题。

- 1. 忘记阅读快速启动指南（`QuickStart Guide`）。

- 2. 尝试编译旧版本的`dosemu`。

- 3. 尝试使用早于`2.0.28`或`2.1.15`的内核进行编译。

- 4. 在`/usr/src/linux`中放置了错误的`Linux`内核源码，或缺少`/usr/src/linux/include/version.h`。

- 5. 使用编译了`IPC`的内核运行`dosemu`。

- 6. 使用早于`2.7.2`的`gcc`或早于`x.x.x`的`lib`进行编译。

- 7. 忘记编辑你的`/etc/dosemu.conf`文件。

- 8. 使用已经挂载的分区运行`DOMU`。

- 9. 没有足够的权限（即`root`）安装`dosemu`。(97/04/08)

### 2.3 如何在旧版本的 Linux 内核上使用 dosemu。

如果你仍在使用`1.2.13`且某些原因无法升级，请使用`dosemu-0.60.4`。如果你使用低于`2.0.28`和`2.1.15`的某些版本`dosemu`，`Hans Lermen`(`lermen@elserv.ffm.fgan.de <mailto:lermen@elserv.ffm.fgan.de>`) 报告过 (97/1/25 和 97/2/11)：

> `dosemu-0.64.3.tgz`版本的模拟器是否适用于`2.xx yy`版本的`Linux`内核？

是的，……

```
if ((xx == 0) && (yy >= 28)) || ((xx >= 1) && (yy >= 15) ))
    take_dosemu_0_64_4();
else {
    if (xx == 1) exit(1);
    take_dosemu_0_64_2_x();
}
```

## 2. 编译并安装 dosemu ;-)

### 2.4 我如何生成二进制执行文件？

从`0.64.4`版本开始，不再支持`a.out`。如果你绝对需要它，必须使用`0.64.3.1`版本。如果你设置了标准配置 (97/2/11)，那么配置脚本应该会处理这个问题。

### 2.5 如何在内存较小的机器上编译 dosemu？

`Marty Leliner`(`leisner@sdsp.mc.xerox.com`) 报告 (95/4/8)：

如果你遇到交换空间（`swap space`）不足的问题，可能想在`dpmi/Makefile`定义`CFLAGS`后添加`CFLAGS+=-fno-inline`。在执行之前请务必小心并检查交换空间是否存在。发现`Linux`在没有交换空间时会崩溃几次。

### 2.6 编译时出现关于 "slang" 的奇怪错误

你可能已经安装了自己版本的`Slang`库。`Hans Lermen`(`<lemen@elserv.ffgan.de>`) 写道 (97/2/11)：

```
configure --enable-force-slang
```

### 2.7 有哪些可配置选项

尝试执行

```
configure --help
```

查看列出的可配置选项列表 (97/2/12)。

### 2.8 如何加快编译？

`Marty Leliner`(`leisner@sdsp.mc.xerox.com`) 报告 (95/4/8)：

默认优化选项是`-O2`。你可能想修改`Makefile`以使用`-O`（编译速度快快/体积更小）。

### 2.9 来自 Marty 的更多编译提示…………

`Marty Leliner`(`leisner@sdsp.mc.xerox.com`) 报告 (95/4/8)：

你需要在系统上构建内核以获取当前版本。如果不是，你可能需要修改顶层`Makefile`中的`KERNEL_VERSION`。数字格式为`"nnnn,"`，其中`"n"`是次版本，`"ppp"`是补丁级别。例如，内核`1.1.88`对应`"1010888"`，内核`1.2.1`对应`"102001"`。

来自`lemen@elserv.ffgan.de`的补充：

对于大于`0.64.3`的版本，这不再适用。你需要一个有效的`<linux/version.h>`，它必须是你的标准`/usr/include`的一部分。如果你没有它，要么是对内核源码执行了`make clean`，要么你的发行版未为此提供支持。

### 2.10 我需要以 root 身份编译 dosemu 吗？

(95/4/8)

不需要。但你必须以`root`身份安装。

`Marty Eisner`(`leisner@sdsp.mc.xerox.com`) 补充道

为了访问`I/O`端口（包括控制台），`dosemu`以`root`身份运行。在`X`窗口的`xterm`中运行需要直接访问的`dosemu`现在允许你以用户身份运行。`setuid`的影响将在开发版本中处理 (95/8/11)。

请查看`/doc/SECURITY.readme` (97/2/9)。

### 2.11 如何补丁 dosemu。

如果你将`dosemu`从一个版本补丁到另一个版本，请执行`make pristine; configure; make`。如果你没有执行`pristine`，新可执行文件的版本将是，如果整个程序能编译的话 (97/2/9)。

### 2.12 哪些 DOS 版本可以在 dosemu 上运行？

`Caldera`的`OpenDOS`（以前称为`DrDOS`）报告可以在`dosemu`上运行 (`Nicolas St-Pierre <draggy@kosmic.org>`)。据报道，`OpenDOS`可以免费用于非商业用途。然而，截至目前，不允许重新分发。你必须从`Caldera`获取`OpenDOS`。

### 2.13 不可运行的版本

`DOS 4.0`在`dosemu`上也有问题 (`Mattias Hembruch <mgembru@ece.waterloo.ca> 97/3`)

## 3. 硬盘设置

### 3.1 如何将我的硬盘分区作为 Linux？

首先，将你的硬盘分区挂载为`Linux`子目录。

### 3.2 我如何从 Linux 访问镜像文件（himage）？

使用较新的`mtools`（编写时版本为`3.0`）。在`/etc/mtools.conf`中添加类似下面的行：

```
drive g: file="/var/lib/dosemu/himage" Offset=8832
```

你就可以对镜像使用`mtools`了，例如`mdir g.` `mcopy g:/config.emu /tmp`会将镜像中的`config.emu`文件复制到`/tmp/config.emu`。你可以对其进行编辑，然后将其复制。

## 我可以使用我的堆叠/双倍间距/超级存储磁盘吗？

此时，标准内核上无法通过重定向器（`lredir`或`emufs`）访问压缩驱动器。有一个内核补丁可以以`“dmsdofs”`的名称挂载压缩文件。可以在`sunsite.unc`及其镜像站找到它。

```
http://sunsite.unc.edu:/pub/Linux/system/Filesystems/dosfs/
```

建议去`http://sunsite.unc.edu/pub/Linux/Incoming`查找更新版本。不过，许多人通过简单地取消`dosemu`配置文件中该行

```
disk { device "dev/hda" # 1 partition on 1st disk
```

行的注释取得了成功。其他人使用以下方法也成功了：

```
disk { partition "/dev/hda1" }
```

这样做存在着在`dosemu`崩溃时丢失数据的风险（97/2/9）。 
