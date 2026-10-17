
# 加载 HP-UX 11i 和 vPars 软件

请记住，每个您希望运行的虚拟分区都必须加载 HP-UX。例如，如果您想运行两个虚拟分区，如本书中的示例所示，则需要为这两个虚拟分区都加载 HP-UX 11i。关于加载 HP-UX 11i 的过程需要为您希望运行的每个虚拟分区执行。HP-UX 11i 可以从媒体（如 CD-ROM 上的 HP-UX 11i 发行版）或 Ignite-UX 服务器加载。您可以使用任何方法为希望运行的每个虚拟分区加载 HP-UX 11i 和虚拟分区软件。

在撰写本文时，有两个 vPars 产品：一个具有全书覆盖的全部功能的产品，以及一个具有完整产品子集功能且免费的产品。免费产品限制最多两个 vPars，其中一个 vPar 只能有一个 CPU。

购买完整产品（产品编号 `T1335AC`）时，会提供一个 CD-ROM，其中包含以下组件：

- `vPars` 软件
- 补丁
- `vPars` 管理指南
- 小册子
- 用于启动的 `WINSTALL` 文件

在某个时间点，完整产品将通过标准发行版提供，而不是单独的 CD-ROM。免费产品（在撰写本文时称为 `VPARSBASE`）可以从 `www.software.hp.com` 下载。

图 1-3 展示了完整产品 `T1335AC` 下方显示的软件组件示例。

![](img/eff8b9287a5f38c5adf538f24aacf29e_42_0.png)

图 1-3 加载 vPars 软件的示例

图 1-3 显示了构成 `T1335AC` 的三个组件：内核、监控程序和运行环境。前面列出的额外组件，即补丁和 `WINSTALL`，也必须加载以使 vPars 完全运行。

请记住，由于本章使用的 vPars 软件尚未发布，您可能会看到一些不同的产品编号。

加载此软件后，系统将重新启动以构建内核。这是自动为您完成的；vPars 内核相关背景在第 2 章和第 4 章中均有介绍。

## 安装范围

所有 vPars 软件必须加载到将在 vPars 服务器上使用的每个 HP-UX 11i 卷上。此软件的加载将在您希望在 vPars 服务器上同时运行的每个 HP-UX 11i 实例上进行。有两种方法可以将 HP-UX 11i 操作系统和 vPars 软件加载到所有用于 vPars 的卷上。第一种，也是全书使用的方法，是在创建虚拟分区之前将 HP-UX 11i 和 vPars 软件加载到所有 vPars 卷上。第二种是仅将第一个 vPar 的卷加载所有软件，创建任意数量的 vPars，然后使用 `vparboot -v vp_name -l ignore_kernel` 启动并在其他磁盘上加载 HP-UX 11i。在本章中，我在创建 vPars 之前先在所有磁盘上加载 HP-UX 11i 和 vPars 软件。由于加载了 vPars 软件，大量软件已被加载。`/sbin` 目录中包含我们将在后续章节中使用的 `vpar` 命令。以下是 `/sbin` 中 `vpar` 命令的长列表。

```
# ll /sbin/vpar*
-rXr-xr-X    1 bin     bin     128760 Oct 18 22:08 /sbin/vparboot
-rXr-xr-X    1 bin     bin     561236 Oct 18 22:07 /sbin/vparcreate
-rXr-xr-X    1 bin     bin     101040 Oct 18 22:04 /sbin/vpard
-rXr-xr-X    1 bin     bin     559592 Oct 18 22:04 /sbin/vpardump
-rXr-xr-X    1 bin     bin     30920 Oct 18 22:04 /sbin/vparesxtract
-rXr-xr-X    1 bin     bin     140072 Oct 18 22:08 /sbin/vparemmodify
-rXr-xr-X    1 bin     bin     47232 Oct 18 22:04 /sbin/vparreloc
-rXr-xr-X    1 bin     bin     127808 Oct 18 22:08 /sbin/vparremove
-rXr-xr-X    1 bin     bin     132008 Oct 18 22:13 /sbin/vparstate
-rXr-xr-X    1 bin     bin     152040 Oct 18 22:13 /sbin/vparstatus
-rXr-xr-X    1 bin     bin     26152 Oct 18 22:14 /sbin/vparutil
#
```

这些是您用于创建、查看、修改以及通常处理 vPars 的命令。第 2 章专门用于描述这些命令并提供使用它们大多数形式的示例。此外，随书附带的撕页卡片总结了这些命令中的许多。

## 内核相关文件

`/stand` 中有几个与 vPars 内核相关的文件。以下列表显示了其中一些：

```
# ll /stand/vp*
-ww------    1 root    root      8232 Nov  8  7:09 /stand/vpdb
-rXr-xr-X    1 bin     bin       849992 Oct  5 23:18 /stand/vpmon
#
```

`vpmon` 在系统启动时加载，是运行 vPars 的基础。第 3 章详细涵盖了启动过程，包括启动 `vpmon`。`vpdb` 是包含系统中所有运行 vPars 相关信息的 vPars 数据库。此文件由 vPars 应用程序自动同步，以确保所有 vPars 拥有关于系统中所有 vPars 的相同信息。

## 启动相关文件

有几个与启动相关的文件，包括下面显示的文件，它们在涵盖启动过程的第 8 章中有更详细的介绍。

`/etc/rc.config.d/vpqstd`

`/etc/rc.config.d/vparhb`

`/etc/rc.config.d/vparinit`

`/sbin/init.d/vpard`

`/sbin/init.d/vparhb`

`/sbin/init.d/vparinit`

第 8 章详细涵盖了这些文件，该章节也详细说明了 vPar 的启动过程。其中特别值得关注的是 `vparhp`，它是与保持所有 vPar 上的 `vpdh` 同步相关的心跳守护进程。

对于与 vPar 相关的工作，在线手册页（man pages）非常重要。以下列表显示了在撰写本文时我系统上加载的手册页。
