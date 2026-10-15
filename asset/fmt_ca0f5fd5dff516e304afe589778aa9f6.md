
`make oldconfig` 命令尝试从已安装的系统创建一个 `.config` 文件。你可能需要运行两次此命令。如果有必要，你可以通过输入 `make xconfig` 来编辑配置，这将提供大量的可点击选项。你可以为某个选项选择 'y'（Yes）按钮将其编译进内核，选择 'n' 将其排除，或选择 'm' 将其编译为可以由运行中的内核加载的模块。
下一步是输入 `make dep`，它会遍历整个内核寻找依赖关系，即需要其他文件才能构建源文件的信息。如果这一步正确完成，你就可以构建内核本身了。输入 `make bzImage`，除非立即发生错误，否则给自己泡杯茶吧。构建过程将运行许多分钟，最后创建一个包含内核常驻部分可加载镜像的文件。
在继续之前，请确保即使你破坏了已安装的内核，仍然能让系统启动。使用 `mkbootdisk` 命令（在某些发行版中命令可能不同）创建一个应急启动软盘。
内核源码中的 `README` 文件告诉下一步是构建可加载模块。然而，如果你构建的内核与你正在运行内核的版本不相同，则这可能不起作用。问题在于脚本可能会使用已安装内核的信息来构建可加载模块，并由于各种不兼容性而失败。如果发生这种情况，你需要通过 `make install` 安装你刚刚构建的内核，然后再使用 `make modules` 构建模块，这可能比构建常驻部分花费更长时间。
通过安装新内核，你不应该损坏旧内核——它们应该有不同的版本号。万一发生极小概率出现问题并导致系统无法运行，你可以通过恢复软盘启动，并将软盘上的文件复制回 `/boot` 目录来恢复状况。你可能还需要重新安装引导加载程序（boot loader）——请遵循第 8 章的说明。
某些发行版利用 `EXTRA` 参数，通过在版本号后附加“custom”或类似的词汇来对你构建的内核进行区分。请查看 `/usr/src/linux/Makefile` 看看你的发行版是否使用了此功能。
现在输入
```
make modules_install
```
将你创建的模块复制到 `/lib/modules` 中。
安装内核应该也会重新构建初始内存磁盘（initial ramdisk）。然而，它可能是用旧内核的模块重新构建的，因此在此时再次执行
```
make install
```
以强制将当前模块存到初始内存磁盘中。
调整你的引导加载程序（见第 8 章），将你的新内核作为启动选项。在某些发行版中，这会在安装内核时自动完成。
你现在可以重启机器，如果一切顺利，它将运行你的新内核。如果没有，请仔细检查任何错误信息。新内核无法启动的常见原因有：
- *引导加载程序设置错误。它可能正尝试从错误的文件加载内核，或者内核与初始内存磁盘的版本不一致。*
- *内核为错误的硬件构建的。你的内核可能正尝试在旧的 486 上运行为 Pentium 构建的代码。*
- *内置驱动程序不正确。如果你编译了一个针对你机器上未安装的硬件的驱动程序，你可能会产生一个启动后立即崩溃的内核。*
一旦你的新内核运行，你就可以开始对其进行自定义。
首先尝试更改一个选项并观察会发生什么。命令序列是：
```
make xconfig
make dep
make bzImage
make modules
make modules_install
```
完成这些操作后，你就可以对内核进行任何操作。特别是，你可以安装内核补丁（patches）。
图 12.1 显示了内核补丁的一个示例。该补丁由 Steve Purcell 编写，感谢他慷慨许可将其包含在书中。
此补丁使内核能够与 Freecom FS-1 CD 驱动器正确通信。该驱动器对 USB INQUIRY 命令的响应略微异常。该补丁让 Linux 能够根据其响应正确识别该驱动器。
该补丁是通过编辑内核源码的新副本来修复问题创建的，然后使用 `diff` 命令列出更改列表。`diff` 的输出（即补丁）是行中的文本。
补丁中的 `.h` 表示三个文件——`unusual_dev.h`、`usb.c` 和 `usb.b` 被修改了。在每个文件中，它通过以 `@@` 开头的行给出了更改的大致位置。然后它显示了一段未修改代码示例，新代码在行首标记有 `+` 符号，以及另一个简短的未修改部分。被删除的行（示例中没有）将在行首标记为 `-` 符号。
`patch` 命令可以通过读取补丁并进行编辑，对另一组源文件进行相同的更改。
即使被打补丁的代码与生成补丁的版本不完全相同，这在大多数情况下也是有效的。`patch` 以一种非常智能的方式处理这个问题，尝试将未修改代码样本与它正在编辑的文件进行匹配，并调整插入或删除代码的位置以匹配。
此补丁是在内核版本 2.4.21 上生成的。我将其放在内核源码中名为 `fs1patch` 的文件中，并使用这些命令完全应用到 `2.4.20`：
```bash
cd /usr/src/linux-2.4.20-13.9/
patch -b -p1 -F 5 <fs1patch
```
```diff
diff -N kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h
@@ -48,31 +48,38 @@
-UNUSUAL_DEV=0xc003, 0x3000, 0x9999,
+UNUSUAL_DEV=0xc007f, 0x0004, 0x0100, 0x01d3,
-    US_SC_QC=CD-RW_QC, US_FI_INQUIRY_CD,
+    US_SC_QC=FS1_QC, US_FI_INQUIRY_CD,
-    qscb_S20,FB_HW, US_FI_INQUIRY_CD,
+    qscb_S20,FB_HW,US_FI_INQUIRY_CD,
+    qscb_SBI-B250,
-    UNUSUAL_DEV=0xc07af, 0x0000, 0x0000, 0x0000,
+    UNUSUAL_DEV=0xc07af, 0x0000, 0x0000, 0x0ffff,
@@ -63,7 +70,11 @@
-    fill_inquiry(us,data_ptr, 6);
+    fill_inquiry(us,data_ptr, 6);
-    us_sg->cmd_result = GOOD
+    us_sg->cmd_result = GOOD
+    if (us_sg->cmd_result != 0) {
+        return EIO;
+    }
```
```diff
diff -N kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h
@@ -78,11 +89,13 @@
-    /* 0x0020 supports multiple targets */
+    /* 0x0020 supports multiple targets */
-    /* 0x0040 needs filtering */
+    /* 0x0040 needs filtering */
-    /* 0x0080 needs filtering to CD */
+    /* 0x0080 needs filtering to CD */
```
此补丁是在内核版本 2.4.21 上生成的。我将其放在内核源码中名为 `fs1patch` 的文件中，并使用这些命令完全应用到 `2.4.20`：
```bash
cd /usr/src/linux-2.4.20-13.9/
patch -b -p1 -F 5 <fs1patch
```
```diff
diff -N kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h
@@ (lines omitted) @@
-    /* 0x0020 supports multiple targets */
+    /* 0x0020 supports multiple targets */
-    /* 0x0040 needs filtering */
+    /* 0x0040 needs filtering */
-    /* 0x0080 needs filtering to CD */
+    /* 0x0080 needs filtering to CD */
```
此补丁是在内核版本 2.4.21 上生成的。我将其放在内核源码中名为 `fs1patch` 的文件中，并使用这些命令完全应用到 `2.4.20`：
```bash
cd /usr/src/linux-2.4.20-13.9/
patch -b -p1 -F 5 <fs1patch
```
```diff
diff -N kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h kernel-source-2.4.21-pre3/drivers/usb/storage/unusual_devs.h
@@ (48,11 +,1) @@
-    /* 0x0020 supports multiple targets */
+    /* 0x0020 supports multiple targets */
-    /* 0x0040 needs filtering */
+    /* 0x0040 needs filtering */
-    /* 0x0080 needs filtering to CD */
+    /* 0x0080 needs filtering to CD */
```
此补丁是在内核版本 2.4.21 上生成的。我将其放在内核源码中名为 `fs1patch` 的文件中，并使用这些命令完全应用到 `2.4.20`：
```bash
cd /usr/src/linux-2.4.20-13.9/
patch -b -p1 -F 5 <fs1patch
```
图 12.2 包格式与构建序列
创建 spec 文件的简单方法是在你的源目录中使用 emacs 开始编辑它。当前版本的 emacs 会自动为你创建该几乎所有的文件内容。你可以在 RPM howto 中找到撰写 spec 文件的完整说明。请注意阅读与你所拥有的 RPM 副本相对应的版本，该过程中的某些步骤最近发生了变化。
为了创建 .rpm，我将源文件放在名为 `/home/unclebob/tsplit-1.0.3/` 的目录中，名称的最后部分必须与我们要的包和压缩包（tarball）匹配。
接下来，我使用此命令创建压缩包（它应该是一行）：
```
tar -C /oldhome/unclebob/ -cvzf /usr/src/redhat/SOURCES/tsplit-1.0.3.tar.gz tsplit-1.0.3
```
这会在 `/usr/src/redhat/SOURCES` 中创建压缩包，并使用 `-C` 选项，以确保只有最后一个路径分量被放入压缩包中。`/usr/src/REDHAT` 下的目录是为构建 rpm 专门布局的。
最后，我输入 `rpmbuild --clean -ta tsplit/tsplit-1.0.3.tar.gz`，由 rpmbuild 完成剩余工作。它解压我的压缩包，使用我的 Makefile 编译程序并压缩 man 页面，然后创建三个文件：
```
/usr/src/redhat/RPMS/i386/tsplit-1.0.3-1.i386.rpm
/usr/src/redhat/RPMS/i386-tsplit-debuginfo-1.0.3-1.i386.rpm
/usr/src/redhat/SRPMS/tsplit-1.0.3-1.src.rpm
```
这些 rpm可以通过 rpm 的 `-i` 选项安装到系统上，或者通过互联网发送给其他人；一个极小的调试信息 rpm，以及一个源码 rpm。
源码 rpm 包含了压缩包。你可以从源码 rpm 重复整个构建过程。
如果你收到一个压缩包形式的程序，可以尝试同样的方法将其转换为 rpm。这并不总是有效，你收到的程序可能是在不同的系统上开发的，需要一些微调才能在 Linux 上运行。
处理此问题的简洁方法是将压缩包两次解压到两个名称略有不同的目录，修复问题（有时说起来容易做起来难），并使用 `diff` 程序列出你的更改。这个列表被称为补丁（patch）——前面的章节中提到过补丁。
现在当你构建 rpm 时，只需在 spec 文件中提及补丁，rpmbuild 就会应用该补丁。
你现在已经有了足够的 Linux 知识来设置、使用、保护和排错 Linux 系统。
Linux 是一个巨大且快速增长的世界，你已准备好开启无限迷人的发现之旅。这里是一些实用的信息来源，帮助你找到方向。
# 发行版厂商
# 其他组织
- Linux Online http://www.linux.org/
- 自由软件基金会与 GNU 项目 http://www.gnu.org/
- X-Windows http://www.xfree.org/ 和 http://www.x.org/
- Rpmfind，巨大的免费软件集 http://www.rpmfind.net
- ALSA (音频) 项目 http://www.alsa-project.org/
- 通用串行总 (USB) 项目 http://www.linux-usb.org/
- 高性能图形 http://www.opengl.org/
- Video for Linux – 电视卡和摄像头 http://www.exploits.org/v41/
- 笔记本上的 Linux http://www.linux-laptop.net/
# 应用程序
- CUPS http://www.cups.org/ (打印)
- OpenOffice http://www.openoffice.org/
- Gimp http://www.gimp.org/
- Gphoto http://www.gphoto.org/
- Xephem http://www.clearskyinstitute.com/
- Samba http://www.samba.org/
- SQL http://www.postgresql.com/ http://www.mysql.com/
# 仅供娱乐
- 关于游戏的信息源，下载链接 http://www.linuxgames.com/
# 认证
- 红帽 (Red Hat) http://www.redhat.com/training/rhce/courses/
- LPI http://www.lpi.org/
# Linux 用户的书籍
- 《Linux in a Nutshell (第四版)》，Ellen Sievier, Aaron Weber, Stephen Figgins (编)。(O'Reilly, 2003, ISBN: 0596004826) 关于命令和工具的有用参考书。
- 《Running Linux (第四版)》，Matt Welsh, Lar Kaufmann, Matthias Kalle Dalheimer, Terry Dawson 著。(O'Reilly, 2002, ISBN: 0596002726) 解释了系统的部分工作原理。
# 编程书籍
- 《Learning Perl (第三版)》，Randal L. Schwartz, Tom Phoenix 著。(O'Reilly, 2001, ISBN: 0596001320) 这是对 Perl 语言的一个非常有用的介绍。
- 《Linux Device Drivers (第二版)》，Alessandro Rubini, Jonathan Corbet 著。(O'Reilly, 2001 ISBN: 0596000831) 这本书不仅涵盖了如何编写设备驱动，还解释了 Linux 内核的一些工作原理。如果你想为 Linux 机器添加新硬件，这本书将引导你完成驱动程序的编写过程。注意，第一版没有涵盖当前的内核。
- 《PostScript® Language Tutorial and Cookbook》，Adobe Systems Inc. 著。(Addison-Wesley, 1985, ISBN: 0201017993) 这本书解释了 Linux 用于打印的 PostScript 语言。它向你展示如何从自己的程序创建打印输出。
- 《Programming with Qt (第二版)》，Matthias Kalle Dalheimer 著。(O'Reilly, 2002, ISBN: 0596000642) 这是对 Qt 的介绍，将帮助你编写使用 GUI 的应用程序。
- 《Linux Kernel Internals (第二版)》，Michael Beck 著。(Addison-Wesley, 1997, ISBN: 020133142) 内核内部机制的指南。
- 《Learning GNU Emacs》，Debra Cameron, Bill Hobbs, Eric Raymond 著。(Wiley, 2003, ISBN: 0596002551) 关于 emacs 的实用介绍。
- 《Practical Programming in Tcl and Tk》，Brent Welch, Jeffrey Jones 著。(O'Reilly, 2003, ISBN: 0596003856) 这是一本关于 Linux 的实用书籍。
# 术语表
| 术语 | 定义 |
| :--- | :--- |
| absolute path | 独立于当前目录的文件查找路径描述。 |
| always on | 不依赖拨号的网络连接。 |
| bandwidth | 数据传输速度的衡量。 |
| baud rate | 接口发送数据的速率，单位为比特每秒。 |
