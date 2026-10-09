
> 完成
$ cp -d id*.so* $(PRJROOT)/rootfs/lib

第一条 cp 命令复制实际的共享库，第二条命令复制主版本号符号链接，第三条命令复制动态链接器及其符号链接。这三条命令均基于本节前面概述的关于 $[TARGET_PREFIX]/lib 中不同文件命名规则的说明。在第二条和第三条 cp 命令中使用了 -d 选项，以原样保留符号链接。否则，符号链接指向的文件将被完整复制。

当然，你可以从上述命令组中的列表中移除你的应用程序未使用的库。如果你希望在根文件系统中包含 glibc 的完整库集合，请使用以下命令：

```
$ cd $[TARGET_PREFIX]/lib
$ cp *-*.so $(PRJROOT)/rootfs/lib
$ cp -d *.so.[*-9] $(PRJROOT)/rootfs/lib
$ cp libSegFault.so libmwmusage.so libpcapprofile.so \
> $(PRJROOT)/rootfs/lib
```

如果你的应用程序使用了 glibc NSS，别忘了将所需的 libnss_SERVICE 库复制到目标系统的根文件系统。libnss_files 和 libnss_dns 是最常用的。你还需要将 glibc 附带的示例 nsswitch.conf 复制到目标系统的 /etc 目录，并根据你的配置进行定制：¹

```
$ cp $(PRJROOT)/build-tools/glibc-2.2.1/nss/nsswitch.conf \
> $(PRJROOT)/rootfs/etc
```

无论你复制 glibc 库的全部还是部分，你都会注意到其中一些库文件体积较大。为了减小已安装库的大小，你可以使用在第 4 章中构建的跨平台 strip 工具。请小心不要对原始库执行 strip 操作，否则你将不得不重新安装所有库。只有在将库复制到根文件系统之后，才对其执行 strip 操作：

```
$ powerpc-linux-strip $(PRJROOT)/rootfs/lib/*.{so,}
```

在我们的控制模块上，包含所有 glibc 库的 $(PRJROOT)/rootfs/lib 目录在执行 strip 之前大小约为 10 MB。对所有库执行 strip 后，目录大小减小到 2.5 MB。

glibc 组件现已安装到目标系统的根文件系统中，并准备好在运行时被你的应用程序使用。

> ¹ 有关 nsswitch.conf 文件定制的详细信息，请参阅 Tony Baus、Terry Dawson 和 Gregor Purdy 撰写的《Linux Network Administrator's Guide》（O'Reilly 出版社）。

## uClibc

与 glibc 一样，uClibc 包含多个库。查看 $${PREFIX}/uclibc/lib 目录以获取完整列表。它包含与 glibc 目录相同的四种不同类型的文件。

由于 uClibc 旨在作为 glibc 的替代品，因此 uClibc 组件的名称和用途与 glibc 组件相同。因此，你可以使用表 6-2（前文已展示）来研究 uClibc 组件。然而请注意，并非所有 glibc 组件都由 uClibc 实现。uClibc 仅实现了 *ld, libc, libcrypt, libdl, libm, libpthread, libresolv 和 libutil*。使用与 glibc 描述相同的方法来确定你在目标系统上所需的 uClibc 组件。

确定了所需组件列表后，现在可以将它们及其相关符号链接复制到目标根文件系统的 *lib* 目录中。以下命令集复制了基本的 uClibc 组件：

```
$ cd $${PREFIX}/uclibc/lib
$ for file in libc libc libc-nonshared libdl libcres libm libpthread libresolv
>        do
>         cp $file*.so $${PREFIX}/rootfs/lib
>         cp -d $file.so.$${*} $${PREFIX}/rootfs/lib
> done
```

这些命令很可能报告找不到两个文件：

```
cp: libcNonshared.so.[*-*]: No such file or directory
cp: libc*.so: No such file or directory
```

这没有问题，因为这些文件本就不应存在。上面展示的命令集旨在易于输入，但如果你不想看到任何错误，可以在 *cp* 命令周围添加条件语句。

与 glibc 一样，你可以根据需求修改要复制的库列表。请注意，与 glibc 不同，仅复制选定的几个 uClibc 组件并不会节省太多空间。例如，对于之前提到的控制模块，当复制 *所有* uClibc 组件时，根文件系统的 *lib* 目录大小仅为 300 KB 左右。以下命令将所有 uClibc 组件复制到目标系统的根文件系统：

```
$ cd $${PREFIX}/uclibc/lib
$ cp *.so $${PREFIX}/rootfs/lib
$ cp -d *.so.[*-*] $${PREFIX}/rootfs/lib
```

无需对 uClibc 组件执行 strip 操作，因为它们已经由 uClibc 自己的构建脚本执行过 strip。你可以使用 *file* 命令来验证这一点。

## 内核模块

在第 5 章中，我们构建了内核模块并将其安装到临时目录 \$[PRJROOT]\*/images* 中。现在，我们可以准备将这些模块复制到它们在目标系统 */lib* 目录中的最终位置。

由于你可能编译了许多内核以测试目标系统，现在你需要选择要复制到根文件系统的内核模块集合。例如，对于我们的控制模块，我们为选择了一个 2.6.20 内核。以下命令将该内核的整个 */modules* 目录复制到根文件系统：

```
  \$ cp -a \$[PRJROOT]*/images/modules-2.6.20/* \$[PRJROOT]*/rootfs*
```

这里我们使用 */cp* 的 *-a* 选项以归档模式复制文件和目录。其效果是保留文件属性和链接，并递归复制目录。请注意，由于我们在第 5 章中将模块安装在 \$[PRJROOT]*/images/modules-2.6.20* 目录中的方式，在上述命令中无需显式地在 \$[PRJROOT]*/rootfs* 后追加 */lib/modules* 路径。

就这样，内核模块现已准备就绪，可在目标系统上使用。你可能还需要添加 */etc/modprobe.conf* 文件，以指定特殊的模块参数值、手动覆盖模块，或执行其他改变 *modprobe* 默认行为的操作。详情请参阅 *modprobe.conf* 手册页。

## 内核映像

正如我们之前所说，实际的内核映像是否存在于你的根文件系统中，主要取决于你的引导加载器的功能。如果你预期你的引导加载器配置将从根文件系统引导内核，此时你可以将内核映像复制到目标系统的根文件系统：

```
  \$ mkdir \$[PRJROOT]*/rootfs/boot
  \$ cd \$[PRJROOT]*/images
  \$ cp zImage-2.6.20 \$[PRJROOT]*/rootfs/boot*
```

除了内核映像外，你可能希望将复制用于创建内核的配置文件作为标准做法，以便你可以为原始项目工作区可能丢失的单元提供服务：

```
  \$ cp 2.6.20.config \$[PRJROOT]*/rootfs/boot*
```

由于我们在第 9 章中讨论实际的引导加载器设置，目前关于内核的设置无需做更多事情。我们将稍后继续内核映像的设置。

## 设备文件

遵循 Unix 传统，Linux 系统中的每个对象都显示为文件，包括设备。² Linux 根文件系统所有设备文件（又称设备“节点”）都位于 /dev 目录中。再次强调，/dev 中的设备文件并非由内核决定，而是由期望在那里找到设备文件的标准应用程序（如交互式 shell）决定的。

在通用 Linux 系统中，管理设备文件是一项复杂的任务，因为设备从一台计算机到另一台计算机可能会变化，外部设备也可能随时变化。因此，这些系统需要一种方法来跟踪连接的设备，以确保相应的设备文件存在并且相应的驱动程序已加载。幸运的是，许多定制的嵌入式系统始终使用相同的设备运行，并且只需要固定的设备文件。

### 静态设备文件

这些设备文件被称为 *静态* 文件，因为它们只需在文件系统中创建一次。它们是特殊文件，由类型（*字符* 或 *块*）以及 *主* 和 *次* 号数特征化。虽然用户空间应用程序通过名称区分设备文件，但内核仅依赖其类型以及主次号数来查找管理每个设备的驱动程序。因此，两个具有相同类型、主号和次号的不同的设备文件将以相同的方式处理。

静态设备主次号数的官方信息源是内核源代码中的 *Documentation/devices.txt* 文件。当你不确定某个设备的名称或编号时，可以查阅此文件。另一个更简单的选项是读取 Linux 工作站上设备文件的编号。

例如，列出 /dev/console 显示它是一个字符设备（因为该行的第一个字符是 c），主号为 5，次号为 1：

```
$ ls -1 /dev/console
        crw-r----- 1 root root 5, 1 2007-05-10 07:05 /dev/console
```

类似地，/dev/ram0（第一个 RAM 磁盘）是一个块设备（以 b 字符列出），主号为 1，次号为 0：

```
$ ls -1 /dev/ram0
        brw-rw---- 1 root disk 1, 0 2007-05-04 13:20 /dev/ram0
```

表 6-3 列出了 /dev 目录中所需的必要项。根据你的特定配置，你很可能需要添加一些额外的条目。在某些情况下，你甚至可能需要使用表中未列出的条目。例如，在某些系统中，第一个串行端口不是 ttyS0。基于 SuperH 的系统就是这种情况。

> ² 对此的一个显著例外是网络接口，如以太网卡，它们没有设备文件。

