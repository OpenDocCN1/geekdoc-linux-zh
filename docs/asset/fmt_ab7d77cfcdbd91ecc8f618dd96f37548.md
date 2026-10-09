
## 升级 端口树

`FreeBSD` 升级过程也会升级端口树。

## 升级端口和包

人们在升级时遇到的最常见问题是确定系统上的哪些软件需要升级。我的通用规则是，不要仅仅因为有新版本就升级。这条规则对于大型、复杂的软件包，例如一些新的桌面窗口管理器也是如此。

尽管如此，你可能会发现即使一切运行良好，新版本的软件也解决了某个问题或提供了所需的功能。通过升级端口树可以让你的工作变得更容易，允许你安装那个新软件。

以下列表假设你正在升级：

1. 升级时的第一件事是确保你有备份。如果出现问题，你将希望回到旧版本。
2. 如果可能，在非生产系统上测试升级的软件。成功的升级会让后续升级容易得多。
3. 确保你有系统备份。有关如何操作请参第 3 章。
4. 获取升级后的软件，最好通过包。
5. 通知你的用户你将在该时间使用服务，并且该机器将不可用。
6. 在预定时间，对旧包执行卸载或 `pkg_delete`，然后对新端口执行 `make install`。

## 升级索引和读取文件

# make index && make readme

注意：
这两个命令（`make index` 和 `make readme`）都需要一些时间才能完成。通过使用 `&&`，你将它们关联在一起；当第一个命令成功完成后，第二个命令将会运行。这为你节省了在半小时后又回来手动输入第二个命令的麻烦。

端口升级（`ports upgrade`）不会删除旧的构建目录。如果你安装了 `ports` 但没有运行过 `make clean`，那么工作目录和旧源代码仍然存在，并伴有跟踪状态的隐藏文件。如果你在这些端口中执行 `make`，隐藏文件将显示该端口已构建并拒绝运行，此时你需要运行 `make clean` 来重新构建这些端口。

## 端口集合升级问题

升级端口集合（`ports collection`）的问题在于，任何软件集合都旨在作为一个有凝聚的整体来使用。如果你新软件需要的某个常用工具是旧版本，你可能也需要升级该工具以及依赖于它的程序。危险之处在于，简单的升级可能会迅速变成一系列连锁反应。

当然，`FreeBSD` 并不是唯一受此困扰的操作系统。每个操作系统平台上的每个软件软件包都存在这个问题。（在 `Windows` 中，你经常会看到这表现为 `DLL` 冲突、不明的程序崩溃或任何其他奇怪且令人不悦的行为。）优秀的软件设计可以减少但无法消除这个问题。遗憾的是，优秀的软件设计是稀缺的。

## 检查软件版本

在单用途型机器上，链式升级并不困难；毕竟，Web 服务器通常没有安装成百上千个软件软件包。工作站则是如此，甚至我的笔记本电脑在 `/var/db/pkg/` 中也有超过 200 个条目（你，我真的应该去检查一遍并卸载那些我不再使用的东西；我真的需要那个跟随我鼠标的小守护进程吗？）如果你的系统有复杂的软件依赖关系，你该怎么办？

`FreeBSD` 有一个名为 `pkg_version(1)` 的软件版本检查工具。`pkg` 将你已安装的软件版本与 `/usr/ports/INDEX` 中的版本号进行比较，如果你的 `INDEX` 是最新的，那么你就大功告成了。（你听了我在上一节的建议并更新了你的 `index` 和 `readme`，对吧？你不是那种会把辛苦赚来的钱花在电脑上就置之不管的人吧？当然不是。）

一个基础版本看起来像这样：

```text
# pkg_version -v

apache-1.3.20 = up-to-date with port

autoconf-2.13_1 = up-to-date with port

bzip2-1 = up-to-date with port

cvsup-bin-16.1 = orphaned: net/cvsup-bin

emacs-20.7 = up-to-date with port

gettext-0.10.35 = up-to-date with port

gmake-3.79.1 = up-to-date with port

ispell-3.1.20c_2 < needs updating (port 3.2.04_1)

jade-1.2.1 = up-to-date with port

libtool-1.3.4_2 = up-to-date with port

links-0.96repr7 < needs updating (port 0.96,1)

m-1.4 = up-to-date with port

mutc-2.5 = up-to-date with port

rddftool-1.0.33 = up-to-date with port

sftp-0.9_6_6 = up-to-date with port

cudo-1.6.3_7 < needs updating (port has 1.6.3,7_1)

ucsnmp-4.2.1 = up-to-date with port

unzip-5.42 = up-to-date with port

uillib-2.0.13 = up-to-date with port

xsysinfo-1.4 = up-to-date with port

zip-2.3 = up-to-date with port
```

阅读每个软件包旁边的注释，可以很容易看到系统中的大部分软件都是最新版本。对于 `ispell-1.2.10`，需要更新。

## 启动脚本

让我们来看一个典型的启动脚本 `snmpd.sh`，它是 `net-snmp` 软件包的一部分，我们稍后会安装它。你现在需要了解的是，它在系统启动时启动 SNMP 服务器，并在关机时停止该守护进程。以下是该脚本：

`#!/bin/sh` 这一行 (v) 表示这是一个 shell 脚本。文件的其余部分（类似于 `Windows` 批处理文件）包含了由脚本运行的命令。

第一部分由 `if (w)` 和 `fi` 隔开，确定程序的路径，并告诉脚本的其他部分它是在 `/usr/local`、`/usr/X11R6` 还是其他目录启动的。脚本的其余部分 (x) 需要知道这一点，以便找到自己的文件。

第 (x) 行中的 `case "$1"` 是脚本实际做出决策的地方。脚本的这部分读取调用脚本时提供的第一个参数。例如，如果你的脚本命令是 `snmpd.sh start`，那么 `start` 就是你的第一个参数。如果你运行 `snmpd.sh stop`，那么 `stop` 就是你的第一个参数。脚本有几个较小的部分：`stop` 和双分号 (`;`) 之间的所有内容是在第一个参数为 `start` 时将采取的操作。`stop` 和下一个双分号之间的所有内容是在第一个参数为 `stop` 时将采取的操作。最后一个选项 `(*)` 是所有可能输入的参数的通配符。

例如，如果你通过 `snmpd.sh start` 运行此脚本，脚本将运行以下命令：

```bash
[ -x ${PREFIX}/sbin/snmpd ] && ${PREFIX}/sbin/snmpd && echo -n ' snmpd'
```

这些是标准的 UNIX shell 命令。该命令首先检查 `snmpd` 程序是否存在。如果存在，它会运行该程序并打印它的名称。同样，如果你带有 `stop` 参数调用脚本，它会毫不留情地杀死所有 `snmpd` 进程。

要更改软件包在启动时的行为，请编辑它的启动脚本。例如，要带参数 `-D` 启动 `snmpd`，你需要编辑 `start` 行。选择实际启动 `snmpd` 的所在命令部分，并在那里插入你的更改：

```bash
[ -x $(PREFIX)/sbin/snmpd ] && $(PREFIX)/sbin/snmpd -D && echo -n ' snmpd'
```

## 使用脚本管理运行中的程序

你也可以在系统运行时使用这些脚本。例如，为了重新启动 `snmpd` 使其重新读取配置文件，你可以运行此命令：

```bash
/usr/local/etc/rc.d/snmpd.sh stop && /usr/local/etc/rc.d/snmpd.sh start
```

> 注意：并不完全需要使用脚本来管理运行中的程序。如果你阅读 `snmpd.sh` shell 脚本，你需要知道该程序运行了 `killall snmpd` 命令，并且通过运行 `snmpd` 来启动程序。你可以直接在命令行编辑这些命令，其效果与运行两次之前的脚本完全相同。你必须记住每个脚本对其特定程序的作用，或者如果你不确定，就使用脚本或输入启动脚本的完整路径。

## 管理共享库

共享库背后的基本思想非常直观：它是一块编译后的代码，为其他编译代码块提供和服务功能。共享库为所有程序提供常用的函数，并被设计为尽可能被许多不同的程序重用。

例如，许多程序必须作为其功能的一部分对代码进行哈希（或单向加密）。但如果每个程序都有哈希代码，我们的程序将会变得更大、更难编写且维护起来更不方便。此外，如果实现方式不同，程序将产生兼容性问题。通过使用库（在本例中为 `libcrypt`），需要哈希的程序访问函数消除了维护和兼容性问题。同样，其他共享库提供常用函数来支持其他软件。这减少了程序的平均大小，释放了相当数量的系统内存。

`FreeBSD` 在运行时构建可用共享库的缓存。程序不需要扫描整个磁盘来寻找共享库；它们只需要向缓存请求它们需要的函数。事实上，能够管理库缓存的能力是区分新手和专业人士的标准之一。

虽然 `FreeBSD` 为缓存提供了许多默认值，但我们将讨论在所有特殊情况下妥善配置和管理你的缓存所需的工具。共享库是复杂的野兽。通过 `ldconfig`、`ldd` 和稍加思考，你就可以开始驯服它们。

## ldconfig

管理共享库的主要工具是 `ldconfig(8)`。（你可能会在某处听到对它的各种引用）。我们将讨论几个与 `ldconfig` 相关的不同命令：`rld(1)`、`ldd(1)` 以及 `ldconfig` 本身。

### 二进制类型：Aout 和 ELF

首先我们有二进制类型的问题：`aout` 和 `ELF`。虽然作为管理员你不需要了解 `aout` 和 `ELF` 的细节，但你应该知道 `aout` 是旧标准，`ELF` 是新标准，且编译为一种类型的程序无法使用另一种类型的共享库。（`FreeBSD Netscape` 库采用一种格式，这就是为什么你必须使用 `XFree86` 的兼容库来使用它。）虽然 `aout` 二进制正在逐渐消失，`FreeBSD` 将无限支持这两种类型。

当你执行需要共享库的 `ELF` 二进制文件时，系统会调用 `rld(1)`，即“运行时链接器”。`rld` 在加载时检查二进制文件。`aout` 二进制文件正在消失，`FreeBSD` 将无限支持这两种类型。

*(注：此处原文似乎存在部分重复或逻辑跳跃，已按要求翻译)*

`rld` 检查加载的二进制文件，确定它们需要哪些库并并加载这些库。`aout` 二二进制文件，使用 `ldconfig` 就会出现问题。`rld` 检查加载的二进制文件，确定它们需要哪些库并加载这些库。`aout` 二进制文件，使用 `ldconfig` 就会出现问题。

注意：这并不完全安全；如果你将 `LD_LIBRARY_PATH` 设置为一个过于容易访问的位置，你的程序可能会链接该处的任何内容。`LD_LIBRARY_PATH` 还会覆盖缓存，所以请务必小心你放在其中的内容！

你可以在 `LD_LIBRARY_PATH` 中指定任何目录，并用冒号分隔。例如，我可能想将 `/home/mwlucas/lib` 和 `/compat/linux/usr/lib/local` 目录放入 `LD_LIBRARY_PATH` 以完成软件安装。我会这样操作：

```bash
# setenv LD_LIBRARY_PATH /home/mwlucas/lib:/compat/linux/usr/lib/local
```

例如，我通常是手动安装 `StarOffice` 而不是通过路径。当我这样做时，安装程序会在 `/tmp/sv001.tmp` 中解出各种库，并期望在启动图形化安装程序时能够找到这些库。为了确保它能找到这些库，我使用 `LD_LIBRARY_PATH` 变量指向 `/tmp/sv001.tmp` 目录来启动 `setup`，如下：

```bash
# LD_LIBRARY_PATH => /tmp/sv001.tmp /setup
```

当图形化 `StarOffice` 安装程序启动时，它会检查该目录下的解压库。结果是，我不需要为了使用这个程序就配置 `FreeBSD` 系统。

> 注意：请记住，你可以通过在你的 `.cshrc` 或 `.profile` 文件中输入来自动设置环境变量。

## 程序需要哪些库？

最后，关于程序期望拥有哪些库的问题。你可以通过 `ldd(1)` 获取这些信息。例如，使用此命令查看 `Emacs` 需要什么：

```bash
# ldd /usr/local/bin/emacs

libXaw.so => /usr/X11/libXaw.so (0x28159000)

libXmu.so => /usr/X11/libXmu.so (0x28180000)

libXt.so => /usr/X11/libXt.so (0x2819f000)

libBM.so => /usr/X11/libBM.so (0x28220000)

libIBC.so => /usr/X11/libIBC.so (0x281a8000)

libExt.so => /usr/X11/libExt.so (0x281fe000)

libX11.so => /usr/X11/libX11.so (0x28029000)

libutil.so.3 => /usr/lib/libutil.so.3 (0x282a2000)

libsm.2 => /usr/lib/libsm.2 (0x282b0000)

libc.so.4 => /usr/lib/libibc.so.4 (0x282c6000)

libXtStub.so => /usr/X11/libXtStub.so (0x28361000)
```
