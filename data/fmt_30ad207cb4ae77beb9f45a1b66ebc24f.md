
只需升级指定的应用程序而不是所有可用端口，请使用 `portupgrade pkgname`。包含 `-R` 参数以列出该应用程序所需的所有端口是非常重要的：

```bash
# portupgrade -R firefox
```

如果包含了 `-P`，Portupgrade 会在 `PKG_PATH` 列出的本地目录中搜索可用包。如果没有找到，它将从远程站点获取包。如果无法在本地找到或从远程获取包，Portupgrade 将使用 ports。若要完全避免使用 ports，请指定 `-PP`。最后这个选项列表告诉 Portupgrade 在没有可用包时终止：

```bash
# portupgrade -PP gnome3
```

如果指定了 `-P`，则仅获取端口源码包（distfiles）或包，而不构建或安装任何内容，此时请使用 `-F`。有关所有所有可用开关的更多信息，请参阅 `portupgrade` 的帮助页。

关于 `ports-mgmt/portupgrade` 的更多信息可以在其 `pkg-descr` 中找到。

### 4.5.4. 端口与磁盘空间

使用 Ports Collection 会随着时间推占用磁盘空间。在构建并安装端口后，在端口框架内运行 `make clean` 将使用临时工作目录。如果使用 Portmaster 安装端口，除非指定 `-K`，否则会自动删除此目录。如果安装了 Portupgrade，此命令将删除 Ports Collection 本地副本发现的所有工作目录：

```bash
# portsclean -C
```

此外，过时的源码发行版随时间推积在 `/usr/ports/distfiles` 中。使用 Portupgrade 删除不再被任何端口引用的 distfiles：

```bash
# portsclean -D
```

Portupgrade 可以移除系统当前安装的任何端口未引用的 distfiles：

```bash
# portsclean -DD
```

如果安装了 Portmaster，请使用：

```bash
# portmaster --clean-distfiles
```

默认情况下，此命令是交互式的，并提示用户确认是否删除 distfile。除了这些命令外，`ports-mgmt/pkg_cutleaves` 自动完成移除不再需要的安装端口的任务。

## 4.6. 使用 Poudriere 构建包

Poudriere 是一个 BSD 许可的工具，用于创建和测试 FreeBSD 包。它使用 FreeBSD jails 来建立隔离的编译环境。这些 jails 可以用于构建与安装系统不同的 FreeBSD 版本包，并且当主机为 amd64 系统时，为 i386 构建包。一旦构建了包，它们的布局与官方镜像完全相同。这些包可以被 `pkg(8)` 和其他包管理工具使用。

Poudriere 通过 `ports-mgmt/poudriere` 包或端口安装。安装过程包含一个位于 `/usr/local/etc/poudriere.conf.sample` 的示例配置文件。将此文件复制到 `/usr/local/etc/poudriere.conf`。编辑复制的文件以适应本地配置。

运行 poudriere 的系统不需要 ZFS，但使用它是有益的。当使用 ZFS 时，必须在 `/usr/local/etc/poudriere.conf` 中指定 `ZPOOL`，并将 `FREEBSD_HOST` 设置为附近的镜像。定义 `CACHE_DIR` 允许使用 `devel/ccache` 来缓存编译和...

11amd64-local-workstation -make.conf 系统的 make.conf 和此新文件在构建时合并，以创建构建围狱（jail）使用的 make.conf。

要构建的软件包列录在 11amd64-local-workstation -pkglist 中：

- editors/emacs
- devel/git
- ports-mgmt/pkg
...

配置指定端口的选项和依赖关系：

```bash
# poudriere options -j 11amd64-p local -z workstation -f 11amd64-local-workstation-pkglist
```

最后，构建软件包并创建一个包仓库：

```bash
# poudriere bulk -j 11amd64-p local -z workstation -f 11amd64-local-station-pkglist
```

在运行期间，按下 Ctrl+t 可以显示构建的当前状态。
Poudriere 还会在 `/poudriere/logs/bulk/jailname` 目录下构建文件，这些文件可以配合 Web 服务器显示构建信息。

完成后，新的软件包现在可以从 poudriere 仓库进行安装了。

有关如何使用 poudriere 的更多信息，请参见 `poudriere(8)` 和主网站：https://github.com/freeb-sd/poudriere/wiki。

## 4.6.2. 配置 pkg 客户端使用 Poudriere 仓库

虽然可以在官方仓库的同时使用自定义仓库，但有时禁用官方仓库是有用的。这通过创建一个覆盖并禁用官方配置文件的配置来实现。创建 `/usr/local/etc/pkg/repos/FreeBSD.conf` 包含以下内容：

```
FreeBSD: {
enabled: no
}
```

通常，通过 HTTP 向客户端机器提供 poudriere 仓库是最简单的。设置一个 Web 服务器来提供包目录，例如：`/usr/local/poudriere/data/packages/11amd64`，其中 11amd64 是构建的名称。

如果包仓库的 URL 为：http://pkg.example.com/11amd64，那么 `/usr/local/etc/pkg/repos/custom.conf` 中的仓库配置文件将如下所示：

```
custom: {
url: "http://pkg.example.com/11amd64",
enabled: yes,
}
```

# 第 4 章：安装应用程序：软件包与端口

## 4.7. 安装后考虑事项

无论是从二进制包还是端口（port）安装软件，大多数第三方应用程序在安装后都需要某种程度的配置。可以使用以下命令和位置来帮助确定应用程序安装了哪些内容。

- 大多数应用程序会在 `/usr/local/etc` 中安装一个默认配置文件。在应用程序具有大量配置的情况下，会创建一个子目录来存放它们。通常会安装以 `.sample` 等后缀结尾的示例配置文件。应该检查并可能对这些配置文件进行编辑以满足系统需求。要编辑示例文件，首先复制一份不带 `.sample` 后缀的副本。
- 提供文档的应用程序将安装到 `/usr/local/share/doc` 和许多手册页。应该参考这些文档。
- 某些应用程序运行的服务必须添加到 `/etc/rc.d`。

注意：
根据设计，应用程序不会自动运行它们的启动脚本，也不会在停止时自动执行操作。

- `csh(1)` 的用户可以确定应用程序安装了哪些内容。
- 使用 `pkg info` 来确定问题。

## 4.8. 处理端口

当端口无法构建或安装时，请尝试以下方法：
1. 搜索查看是否有待处理的（pending）。
2. 询问维护者的帮助。
3. 使用 Bugzilla 提交报告。
4. 检查 FreeBSD 文档。

# 第 5 章：窗口系统

## 5.1. 概述

X Window System 是一个提供界面的图形环境。本章描述了如何配置图形环境。然后它描述了窗口管理器。

在阅读本章后，你将了解：
- 窗口系统的各种组件以及它们如何相互作用。
- 如何安装和配置 Xorg。
- 如何安装窗口管理器和桌面环境。
- 如何使用字体。
- 如何设置你的系统。

在阅读本章之前，你应该：
- 理解 X 窗口系统的组件。

## 5.2. 术语

虽然不需要理解所有组件的每一个细节，但具备这些组件的基础知识会很有帮助。

X 服务器
X 从初就被设计为以网络为中心，并采用“客户端-服务器”模型。在这种模型中，“X 服务器”运行在连接了键盘、显示器和鼠标的计算机上。服务器的职责包括管理显示、处理来自键盘的输入以及处理来自平板电脑或投影仪等设备的输入。这让一些人感到困惑，因为 X 的术语与他们预期的完全相反。他们预期“X 服务器”是强大的机器，而“X 客户端”是桌子上的机器。

X 客户端
每个应用程序（如 XTerm 或 Firefox）都是“客户端”。客户端向服务器发送消息，例如“请在这些坐标处画一个窗口”，服务器返回消息，例如“用户点击了 OK 按钮”。

在家庭或小型办公环境中，X 服务器和客户端通常运行在同一台计算机上。也可以在性能较弱的计算机上运行 X 服务器，并在性能强大的系统上运行 X 应用程序。在这种情况下，X 客户端和服务器之间的通信通过网络进行。

Xorg

窗口管理器
X 不规定窗口在屏幕上应该什么样、如何用鼠标移动它们、使用哪些快捷键在窗口之间切换、每个窗口的标题栏应该什么样、是否带有关闭按钮等。相反，X 将此责任委托给一个独立的窗口管理器应用程序。有几十种窗口管理器可用。每个窗口管理器都提供不同的视觉效果：有些支持虚拟桌面，有些允许自定义快捷键来管理桌面，有些带有“开始”按钮，有些是可以自定义主题的，允许完全改变桌面的视觉效果。窗口管理器可以在端口集合的 `x11-wm` 中找到。每个窗口管理器使用不同的配置机制。有些期望手动编写配置，而另一些则提供图形工具用于大部分配置任务。

焦点策略
窗口管理器负责鼠标焦点策略。该策略提供了一些方法来选择

哪个窗口正在接收按键输入，它还应该可见地显示哪个窗口是当前激活的。

一种焦点策略被称为“点击聚焦”（click-to-focus）。在这种模型下，窗口在接收到鼠标点击后变为激活状态。在“鼠标跟随焦点”（focus-follows-mouse）策略中，鼠标指针下的窗口具有焦点，通过指向另一个窗口来切换窗口。如果鼠标悬停在根窗口上，则该窗口将获得焦点。

在“松散聚焦”（sloppy-focus）模型中，如果鼠标移动到根窗口上，最近使用的窗口将获得焦点。在松散聚焦下，只有当光标进入新窗口时才会改变焦点，而在离开当前窗口时不会。在“点击聚焦”策略中，通过鼠标点击选择活动窗口。该窗口可能会被置顶并显示在所有其他窗口之前。现在，所有的按键输入都将指向此窗口，即使光标移动到另一个窗口。

不同的窗口管理器支持不同的焦点模型。它们都支持点击聚焦，并且大多数管理器还支持其他策略。请查阅窗口管理器的文档以确定可用哪些焦点模型。

## 部件 (widgets)

部件（Widget）是用户界面中所有可以进行某种方式点击或操作的项目术语。包括按钮、复选框、单选按钮、图标和列表。部件工具包（widget toolkit）是一组用于创建图形化应用程序的部件。有几个流行的工具包，包括 KDE 使用的 Qt 和 GNOME 使用的 GTK+。因此，应用程序的外观和感受取决于使用哪种工具包来创建。

## 5.3. 安装 Xorg

在 FreeBSD 上，Xorg 可以作为软件包（package）或端口（port）进行安装。

二进制包可以快速安装，但自定义选项较少：

```
# pkg install xorg
```

从端口集合（Ports Collection）构建并安装：

```
# cd /usr/ports/x11/xorg
```

```
# make install clean
```

108

# 第 5 章 X 窗口系统

这两种安装方式都会安装完整的 Xorg 系统。对于大多数用户来说，二进制包是最佳选择。

适用于经验丰富的用户的较小版本 X 系统位于 `x11/xorg-minimal` 中。大多数文档、库和应用程序将不会安装。某些应用程序需要这些额外的组件才能运行。

## 5.4. Xorg 配置

原文由 Warren Block 贡献。

### 5.4.1. 快速上手

Xorg 支持大多数常见的显卡、键盘和指针设备。

**提示**
显卡、显示器和输入设备会自动检测，不需要任何手动配置。除非自动配置失败，否则请勿创建 `xorg.conf` 或运行 `-configure` 步骤。

- 1. 如果此台电脑上使用过 Xorg，请移动或删除任何现有配置文件：

```
# mv /etc/X11/xorg.conf ~/xorg.conf.etc
```

```
# mv /usr/local/etc/X11/xorg.conf ~/xorg.conf.localetc
```

- 2. 将运行 Xorg 的用户添加到 `video`（视频）组或 `wheel`（轮子）组，以便在可用时启用 3D 加速。要将用户 jru 添加到任何可用组中：

```
# pw groupmod video -m jru || pw groupmod wheel -m jru
```

- 3. 默认包含 `twm` 窗口管理器。它在 Xorg 启动时运行：

```
% startx
```

- 4. 在某些旧版本的 FreeBSD 上，在切换回文本控制台之前必须将系统控制台设置为 `vt(4)`才能正常工作。参见第 5.4.3 节，“内核模式设置 (KMS)”。

### 5.4.2. 加速视频的用户组

需要访问 `/dev/dri` 以允许显卡的 3D 加速。最简单的方法是将运行 X 的用户添加到 `video` 组或 `wheel` 组。使用 `pw(8)` 将用户 slurms 添加到 `video` 组，或者如果没有 `video` 组则添加到 `wheel` 组：

```
# pw groupmod -m slurms || pw groupmod -m slurms
```

### 5.4.3. 内核模式设置 (KMS)

当计算机从控制台切换到 X 的更高分辨率时，必须设置视频输出模式。Xorg 的最新版本使用内核内部的系统更有效地进行这些模式更改。旧版本的 FreeBSD 使用 `sc(4)`，它不感知 KMS 系统。结果是关闭 X 后，系统控制台是空白的，尽管它仍在运行。较新的 `vt(4)` 避免了这个问题。

将此行添加到 `/boot/loader.conf` 以启用 `vt(4)`：`kern.vty=vt`

109

配置文件

### 5.4.4. 配置文件

通常不需要手动配置。除非自动配置不起作用，请勿手动创建配置文件。

### 5.4.4.1. 目录

Xorg 在 FreeBSD 上会从几个目录中查找配置。`/usr/local/etc/X11/` 是推荐的目录。使用此目录有助于将应用程序与操作系统分离。

在旧的 `/etc/X11/` 中存储配置仍然有效。然而，这会将应用程序与基础 FreeBSD 混合在一起。

### 5.4.4.2. 单文件或多文件

在 `/usr/local/etc/X11/xorg.conf.d/` 子目录下使用多个文件比使用传统的单设置更方便。这些文件的示例将在后文中显示。传统的 `xorg.conf` 仍然有效，但灵活性不如多个文件。

### 5.4.5. 显卡

由于 FreeBSD 几个版本的更改，现在可以使用端口集合中的标准显卡驱动程序。请安装与显卡匹配的驱动程序。

295

110

# 第 5 章 X 窗口系统

NVIDIA

在端口集合的 `x11` 中有多个 NVIDIA 驱动程序。请安装与显卡匹配的驱动程序。

参考请参见 https://en.wikipedia.org/List_of_Nvidia_graphics_units。

混合显卡

某些笔记本电脑为芯片组和处理器增加了额外的图形单元。Optimus 结合了 Intel 和 NVIDIA。切换显卡（Switchable Graphics）或混合显卡（Hybrid Graphics）是 Intel 或 AMD 处理器与 AMD GPU 的组合。这些图形系统的实现各异，FreeBSD X 无法驱动所有系统。某些电脑提供了 BIOS 选项来禁用一个适配器或选择一个离散模式。例如，有时可以在 Optus 系统中禁用 NVIDIA GPU。然后可以使用 Intel 驱动程序使用 Intel 视频。BIOS 设置取决于电脑型号。在某些情况下，可以保持两个 GPU 都开启，但在 Device 部分中创建一个只使用主 GPU 的配置就足够让系统运行了。

其他显卡

某些不常用显卡的驱动程序可以在端口集合的 `x11-drivers` 目录中找到。未被特定驱动支持的显卡可能可以使用 `x11-drivers/xf86-video-esa` 驱动程序。该驱动由 `x11/xorg` 安装，也可以手动安装为 `x11-drivers/xf86-video-esa`。当未找到显卡的特定驱动时，Xorg 会尝试使用此驱动。`x11-drivers/xf86-video-scfb` 是一个类似的非专用视频驱动程序，适用于许多 UEFI 和 ARM® 计算机。

296

在文件中设置视频驱动

要在配置文件设置 Intel® 驱动：

示例 5.1. 在文件中选择 Intel® 视频驱动

```
/usr/local/etc/X11/xorg.conf.d/driver-intel.conf
```

```
Section "Device"
Identifier "Card0"
Driver "intel"
# BusID "PCI:1:0:0"
EndSection
```

如果存在多个显卡，可以取消 BusID 标识符的注释并设置以选择所需的显卡。可以通过 `pciconf -lv | grep -B3 display ..` 显示显卡总线 ID列表。

在配置示例中设置 Radeon 驱动：

示例 5.2. 在文件中选择 Radeon 视频驱动

```
/usr/local/etc/X11/xorg.conf.d/driver-radeon.conf
```

```
Section "Device"
Identifier "Card0"
Driver "radeon"
EndSection
```

在配置示例中设置 VESA 驱动：

示例 5.3. 在文件中选择 VESA 视频驱动

```
/usr/local/etc/X11/xorg.conf.d/driver-vesa.conf
```
