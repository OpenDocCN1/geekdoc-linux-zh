
```
# cd /opt/ignite/boot
# cp WINSTALL WINSTALL_NoReloc
# cp <source_path>/WINSTALL . (可能还需要执行 chmod 和 chown。)
```

注意，上面的 `<source_path>` 指的是任何存在 `WINSTALL` 的源。

目前，使用 Ignite-UX 内捆绑的 `WINSTALL` 无法用于 vPars，因为它不是可重定位的。以下命令用于验证是否正在使用正确的 `WINSTALL`：

```
/usr/ccs/bin/elfdump -r /opt/ignite/boot/WINSTALL | fgrep -i relocation
```

如果上述命令没有输出，则 `WINSTALL` 不是可重定位的。

## 5) 启动 Ignite-UX 服务器管理器

```
/opt/ignite/bin/ignite
```

## 6) 完成 Ignite-UX 服务器配置

- 选择：*Options -> Server Configuration...*

- 选择 *Server Options* 选项卡

- 默认配置：*HP-UX B.11.11 Default.*

- 客户端超时：40

- 在 `server` 上运行客户端安装 UI

选择：`Options -> Server Configurations... -> Session Options`

- 验证只设置了以下选项：

  - `Confirm new clients`

  - `Show the welcome screen for the install server`

  - 确保未选中 `Hall the client after installation` 选项。

![](img/eff8b9287a5f38c5adf538f24aacf29e_583_0.png)

一旦 Ignite-UX 服务器安装并配置好以安装 HP-UX OEs 和 vPars，就可以继续使用 `vparsboot` 按需安装所有剩余的 vPars。

有关 Ignite-UX 的更多信息可以在 `Ignite-UX Administration Guide` 中找到。

正如我在本章开头提到的，当你使用 vPars 时，你将拥有更多需要管理的 HP-UX 11i 实例。从 Ignite-UX 服务器安装这些 vPars 将为你节省大量时间，并确保你的安装具有软件的一致性基础。

### 章节非-vPar 特定部分：Ignite-UX 概述

Ignite-UX 是一款功能非常强大的产品。它与许多功能相关联，要全面覆盖这些功能需要一整本书。这个背景部分是根据旧版本的 Ignite-UX 编写的，不包含任何与 vPar 相关的信息。然而，对于从未使用过 Ignite-UX 的人来说，它是一个很好的概览。我将重点介绍我认为 Ignite-UX 的两个主要功能区域。它们是：

- 从拥有软件库的服务器对客户端（或目标）系统进行网络安装。这些库通常通过从介质复制软件到 Ignite-UX 服务器上的库来创建。这与第 2 章中介绍的软件安装有些相似，不同之处在于软件位于服务器上而不是介质上。还有一个图形用户界面，允许你从服务器控制此过程。使用此技术，你可以选择要在每个特定客户端上加载的具体软件。你可以从服务器“推送”软件到客户端，或者从服务器“拉取”软件到客户端。除了从介质创建软件库外，你还可以从“黄金镜像”创建操作系统归档。“黄金镜像”是你希望复制到许多系统的完美运行系统。`make_sys_image` 命令生成“黄金系统”的压缩镜像。在本章中，我们将重点讨论通过从服务器上的介质复制到库来创建的软件库。

- 创建可引导的系统恢复磁带。此功能允许你将根卷的镜像创建到磁带上。之后你可以从此磁带引导并直接从磁带恢复根卷组。

让我们在接下来的部分中看看 Ignite-UX 的这两个方面。请务必检查 www.docs.hp.com 以获取有关 Ignite-UX 的优秀文档，以及 www.software.hp.com 以获取最新的 Ignite-UX 软件。其中一些文档比我在接下来的“如何做”部分中提供的细节更丰富。

我将假设你已经在你的服务器系统上加载了 Ignite-UX 产品。此软件与 HP-UX 11i 和 11.0 捆绑提供，因此只需从介质将其加载到你的服务器系统即可。如果你从 *software.hp.com* 网站下载，可以确保获取最新版本的 Ignite-UX。本章中处理 Ignite-UX 的过程对于 HP-UX 10.20、11.0 和 11i 几乎相同。无论你运行哪个版本的 HP-UX，本章都适用。

安装 Ignite-UX 后，你可能希望更新你的路径，以便无需为每个 Ignite-UX 命令输入完整路径。对于默认的正 POSIX shell，你可以执行以下命令：

```
# export PATH=${PATH}:/opt/ignite/bin
```

此命令更新你的路径以包含大多数 Ignite-UX 可执行文件的目录，`/opt/ignite/bin`。

#### 设置带有库的服务器并安装客户端

你可以使用几乎任何系统作为你的 Ignite-UX 服务器。你可以在你的服务器上为 HP-UX 11i、11.0 和 10.20 设置库。我建议使用 11.00 或 11i 系统作为 Ignite-UX 服务器，因为我曾遇到 10.20 系统作为服务器为 11.00 和 11i 客户端加载软件时的问题。我从未见过 11.0 或 11i 系统作为服务器为任何版本的 HP-UX 客户端加载软件时出现问题。不过，总的来说，服务器作为库的主机，其操作系统不是将软件加载到客户端的组成部分。在我们的示例中，我们将使用运行 11.00 的工作站（型号 J2240）。从我们在此系统上创建的 11.00 库中，我们可以加载各种客户端。就加载客户端而言，重用工作站而不是服务器无关紧要。我发现许多系统管理员使用工作站作为 Ignite-UX 服务器，即使他们主要加载的是服务器，如 N-Class 系统。

你在 Ignite-UX 服务器上创建的软件库会占用大量磁盘空间。包含许多应用程序的核心操作系统可能占用数 GB 的磁盘空间。我喜欢为 Ignite 服务器分配几 GB 的磁盘空间，这样在系统上加载额外库时，我就不必增加 `/var`（软件库的默认位置）的大小。我的经验法则是 `/var` 设为 6 GB，以支持多个库。

为了让您大致了解软件仓库（depots）所消耗的磁盘空间，我在初始系统安装完成时（此时尚未创建任何软件仓库）以及创建核心操作系统和应用仓库之后，分别执行了以下 `bdf` 命令。软件仓库的默认位置是 `/var`；不过，您可以将仓库加载到任何目录中。我建议创建一个文件系统，例如 `/var/depots`，作为仓库区域。在下面的示例中，我们将重点关注 `/var` 的容量，因为它在后续示例中用作仓库的目标位置。

```
# bdf
Filesystem      kbytes   used    avail  %used Mounted on
/dev/vg00/lvol3 204800   19830   173464  10%  /
/dev/vg00/lvol1  83733    13654   61705   18%  /stand
/dev/vg00/lvol8  6553600 156292  5998347   3%  /var
/dev/vg00/lvol7  512000   341251  160127   68%  /usr
/dev/vg00/lvol4  102400    1522   94578    2%  /tmp
/dev/vg00/lvol6  602112  186976  389238   32%  /opt
/dev/vg00/lvol5  204800    1157  190923    1%  /home
/dev/dsk/c1t2d0 2457600 2457600      0   100%  /var/tmp/cddirAAAA02574
```

以下是在创建 11.0 核心操作系统仓库后立即执行的 `bdf` 命令输出，显示 `/var` 的可用空间已从 5.998 GBytes 减少到约 5.667 GBytes。这代表了约 330 MBytes 的数据作为核心操作系统的一部分被加载。
