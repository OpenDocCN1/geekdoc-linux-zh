
在完整安装 Eclipse 时，你获得的许多功能和能力其实并不需要，而且会大幅增加启动和编译时间。其他一些“功能”不仅令人厌烦，还会引起无尽的困惑和挫败感。

归根结底，如果你不熟悉 Eclipse，就会面临学习曲线。如果你独自开发一个小型项目，可以独立使用 CVS，并且还有其他方法来解决单元测试问题，那么你可以考虑跳过 Eclipse。

然而，鉴于 Eclipse 的迅速崛起及其看似占据主导地位的事实，如果你想从事嵌入式系统开发事业，你迟早需要学习如何配置和使用它。此时动手为时未晚。幸运的是，你有大量可用的资源，从纸质书籍到在线站点、教程以及论坛。不幸的是，Eclipse 的高度灵活性使得进一步深入讨论变得困难，因此我们就在此处停下。

## 使用 gdb 调试应用程序

GNU 调试器（GDB）是 GNU 项目的符号调试器（由 Richard Stallman 于 1986 年发起），可以说它是任何 Linux 系统上最重要的调试工具。GDB 已经存在足够长的时间，以至于许多非 Linux 嵌入式系统已经使用它，并结合所谓的 GDB 桩（stubs）来远程调试目标系统。自本书第一版出版以来，GDB 在多个方面发生了演变，最显著的是，处理目标核心文件的功能已整合到其功能中*。*然而，由于 Linux 内核实现了 ptrace() 系统调用，因此你不需要 GDB 桩来远程调试嵌入式应用程序。相反，GDB 软件包中提供了一个 GDB 服务器。该服务器是一个非常小的应用程序，运行在目标系统上，并执行来自主机上运行的 GDB 调试器的命令。因此，任何应用程序都可以在目标系统上进行调试，而无需在目标系统上实际运行 GDB 调试器。这一点非常重要，因为我们将看到，实际的 gdb 二进制文件相当大。

本节将讨论在宿主/目标配置中安装和使用 GDB，而不是讨论实际使用 GDB 来调试应用程序。例如，要了解如何设置断点、查看变量以及查看回溯，请阅读讨论 GDB 使用的书籍或手册之一。特别是，请参考 Matthias Dalheimer 和 Matt Welsh 所著的《Running Linux, Fifth Edition》（O'Reilly 出版社）第 21 章，以及 GDB 手册，该手册既包含在 GDB 软件包中，也可在线访问：http://www.gnu.org/manual。

### 构建和安装 gdb 组件

GDB 软件包在 GPL 条款下可从 ftp://ftp.gnu.org/gnu/gdb 获取。请在你的 `$PRJROOT/debug` 目录中下载并解压 GDB 软件包。例如，对于我们的测试模块，我们使用了 GDB 版本 6.6。与前面章节中描述的其他 GNU 工具集组件一样，最好不要使用软件包目录来构建实际的调试器。相反，创建一个构建目录，切换到该目录，然后按以下方式构建 GDB：

```bash
$ mkdir $PRJROOT/debug/build-gdb
$ cd $PRJROOT/debug/build-gdb
$ ../gdb-6.6.xx/configure --target=$TARGET --prefix=$PREFIX
$ make
$ make install
```

这些命令用于构建能处理目标应用程序的 GDB 调试器。与其他 GNU 工具集组件一样，二进制文件的名称取决于目标。例如，对于我们的测试模块，调试器是 `arch-texture-linux-gdb`。该二进制文件和其他调试器文件安装在 `$PREFIX` 目录中。在我的硬件上，正式的构建过程只需几分钟，而生成的二进制文件相当大。例如，对于 PPC 目标，动态链接后的剥离（stripped）二进制文件大小为 4 MB。这就是为什么不能直接在目标上使用 `gdb` 二进制文件，而是使用 GDB 服务器的原因。

我们现在才开始构建 GDB 服务器，因为它必须使用适当的工具为目标进行交叉编译。为此，创建一个用于构建 GDB 服务器的目录，切换到该目录，然后构建 GDB 服务器：

```bash
$ mkdir $PRJROOT/debug/build-gdserver
$ cd $PRJROOT/debug/build-gdserver
$ chmod +x ../gdb-6.6/gdb/gdserver/configure
$ CC=powerpc-linux-gcc ../gdb-6.6/gdb/gdserver/configure \
    --host=$TARGET --prefix=$TARGET_PREFIX
$ make
$ make install
```

GDB 服务器二进制文件 `gdserver` 现在已经安装到你的 `$TARGET_PREFIX/bin` 目录中。与 gdb 相比，gdserver 的大小更容易接受。构建完成后，将 gdserver 复制到目标系统的根文件系统：

```bash
$ cp $TARGET_PREFIX/bin/gdserver $PRJROOT/roofs/usr/bin
```

在目标系统上配置使用 GDB 服务器不需要额外步骤。下一节将介绍其使用。

### 使用 gdb 组件调试目标应用程序

在使用 GDB 调试应用程序之前，你需要使用适当的标志来编译应用程序。主要是在 gcc 命令行中添加 `-g` 选项。该选项会将调试信息添加到编译器生成的目标文件中。要添加更多调试信息，请使用 `-gdb` 选项。最终二进制文件的大小会增加，有时甚至会大幅增加，因为所需的调试信息将被嵌入二进制文件中。但是，假设你在主机上有包含调试信息的原始未剥离版本，你仍可以在目标上使用剥离的二进制文件。为此，在你的主机上以完整的调试信息构建应用程序。将生成的二进制文件复制到目标系统的根文件系统，并使用 `strip` 通过移除所有符号信息（包括调试信息）来减少刚复制的二进制文件的大小。在目标上使用剥离的二进制文件配合 `gdbserver`。在主机上使用原始未剥离的二进制文件配合 `gdb`。虽然两个 gdb 组件使用不同的二进制映像，但在主机上运行的目标 gdb 能够找到并使用你应用程序的适当调试符号，因为它可以访问未剥离的二进制文件。

以下是 Makefile 中需要的相关部分：

```makefile
DEBUG           = -g
CFLAGS          = -O2 -Wall $(DEBUG)
```

虽然 gcc 允许我们同时使用 `-g` 和 `-O` 选项，但在生成用于调试的二进制文件时，通常最好不使用 `-O` 选项，因为优化后的二进制文件可能与应用程序的原始源代码存在一些细微差异。例如，一些未使用的变量可能未被纳入二进制文件中，或者二进制文件中实际执行的指令序列顺序可能与原始源代码中包含的指令顺序不同。

在目标上运行的 GDB 服务器与在主机上运行的 GDB 调试器之间存在两种通信方式：使用交叉串行链路或 TCP/IP 连接。尽管这些通信接口在许多方面有所不同，但你需要发出的命令语法非常相似。使用 GDB 服务器启动调试会话涉及两个步骤：在目标上启动 GDB 服务器，并从主机上的 GDB 调试器连接到它。

准备好调试应用程序后，以通信方式和应用程序名称作为参数在目标上启动 GDB 服务器。如果你的目标有配置好的 TCP/IP 接口可用，你可以启动 GDB 服务器并配置其通过 TCP/IP 运行：

```bash
# gdbserver
host_ip_address:2345 application
```

例如：

```bash
# gdbserver 192.168.172.50:2345 command-daemon
```

在此示例中，主机的 IP 地址是 192.168.172.50，用于本地监听 GDB 连接的端口号是 2345。请注意，GDB 用于在主机和目标之间通信的协议不包含任何形式的认证或安全机制。因此，我们不建议通过不安全通道（如公共互联网）以这种方式调试应用程序，但如果必须这样做，你可以考虑使用 SSH 端口转发来加密 GDB 会话。Daniel Barrett 和 Richard Silverman（O'Reilly 出版社）所著的 *SSH, The Secure Shell: The Definitive Guide* 解释了如何实现 SSH 端口转发。

如前所述，传递给 `gdbserver` 的 `command-daemon` 可以是主机上构建的原始 `command-daemon` 的剥离副本。

如果你使用串行链路来调试目标，请在该目标上使用以下命令行：

```bash
# gdbserver /dev/ttyS0 command-daemon
```

在此示例中，目标到主机的串行链路是第一个串行端口，`/dev/ttyS0`。

在目标上启动 GDB 服务器后，你可以使用 `target remote` 命令从主机上的 GDB 调试器连接到它。如果你通过 TCP/IP 网络连接到目标，请使用以下命令：

```bash
$ architecture-linux-gdb command-daemon
(gdb) target remote 192.168.172.10:2345
Remote debugging using 192.168.172.10:2345
0x10000074 in _start ()
```

在这种情况下，目标位于 IP 192.168.172.10，指定的端口号与我们之前在目标上启动 GDB 服务器时使用的端口相同。与目标上的 GDB 服务器不同，这里使用的 `command-daemon` 必须是二进制文件的未剥离副本。否则，你将没有调试信息，GDB 将没有什么用处。

如果程序在目标上退出或重新启动，你不需要在主机上重启 GDB。只需在目标上重启 `gdbserver` 后重新发出 `target remote` 命令即可。

如果主机通过串行链路连接到目标，请使用以下命令，并在 `target remote` 中指定目标的串行端口：

```bash
$ architecture-linux-gdb progsname
(gdb) target remote /dev/ttyS0
Remote debugging using /dev/ttyS0
0x10000074 in _start ()
```

虽然此示例在目标主机和目标上都使用了 `/dev/ttyS0`，但这只是巧合。目标和主机可以使用不同的串行端口来相互连接。每条命令中指定的设备是串行电缆连接的本地串行端口。

在目标和主机连接后，你现在可以设置断点并执行你通常在符号调试器中执行的任何操作。

几条 GDB 命令在调试嵌入式目标时可能特别有用。以下是其中一些及其用途的摘要：

