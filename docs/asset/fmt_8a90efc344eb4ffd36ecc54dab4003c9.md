
KDE 的技巧远比我们这样的章节能涵盖的，而且我们甚至还没有尝试涵盖基本的配置和使用基础。有关更多关于使用 KDE 的教程类信息，请参阅 KDE 帮助系统；对于那些喜欢更深入内容的读者，可以查看《24小时自学KDE》（Sams Teach Yourself KDE in 24 Hours）。

# 12 GNOME 1.0 环境

GNOME（或 GNU 网络对象模型环境）是一个项目，其启动部分是为了响应 K 桌面环境（KDE），因为由于一些用户担心 KDE 较不传统的开源许可方法。在过去的几年里，GNOME 已经演变成了一个独立的、可用的桌面环境，其个人风格在某些方面与更加实用的 KDE 有径然不同。

本章旨在帮助你发现可能并非立而易见但对使用 GNOME 有帮助的技巧和方法。它主要为正在使用 GNOME 的人员编写，他们很可能是作为 Linux 发行版的一部分获得它。对于还没有 GNOME 但想尝试一下的人，我们将从关于获取和安装 GNOME 的简要章节开始。

## GNOME 基础：获取、安装、启动、配置

万维网上的 GNOME 主页可以在网站 `http://www.gnome.org` 找到。对下载 GNOME 感兴趣的用户至少要有 200 兆的可用磁盘空间以通过包安装，并有 700–800 兆的可用磁盘空间以从源码编译。GNOME 1.0 的主要下载位置位于 `ftp.gnome.org` 站点的 `/pub/gnome-1.0` 目录下，但该网站可能非常繁忙且难以访问。因此，建议用户访问以下镜像站点之一，这些站点摘自 `ftp.gnome.org` 在过载时发送的拒绝通知中。

### 美国和加拿大：

- `ftp://ftp.cybertrails.com/pub/gnome/`
- `ftp://ftp.geo.net/pub/gnome/`
- `ftp://ftp.net.lut.ac.uk/pub/gnome/`
- `ftp://ftp.snoopy.net/pub/mirrors/GNOME/`
- `ftp://gnomeftp.wgn.net/pub/gnome/`
- `ftp://server.ph.ucla.edu/pub/mirror/ftp.gnome.org/`
- `ftp://sod.intermezzo/mirror/ftp.gnome.org/`

### 澳大利亚：

- `ftp://ftp.tas.gov.au/pub/gnome/`
- `ftp://mirror.aarnet.edu.au/pub/gnome/`

### 欧洲：

- `ftp://ceu.fi.udc.se/pub/os/linux/X Window/GNOME/`
- `ftp://ftp.archive.de.uu.net/pub/X11/GNOME/`
- `ftp://ftp.dataplus.se/pub/linux/gnome/`
- `ftp://ftp.dit.upm.es/linux/gnome/`
- `ftp://ftp.fr.gnome.org/pub/gnome/`
- `ftp://ftp.gts.cz/pub/gui/gnome/`
- `ftp://ftp.informatik.uni.bonn.de/pub/os/unix/gnome/`
- `ftp://ftp.linux.hr/pub/gnome/`
- `ftp://ftp.linux.it/pub/mirrors/gnome/`
- `ftp://ftp.net.lut.ac.uk/gnome/`
- `ftp://ftp.sunet.se/pub/X11/GNOME/`
- `ftp://ftp.task.gda.pl/pub/unix/GNOME/`
- `ftp://ftp.uni.trie.trier.de/pub/unix/X11/toolkits/gnome/`
- `ftp://ftp.utt.ro/mirrors/ftp.gnome.org/pub/GNOME/`
- `ftp://ftp3.linux.it/pub/mirrors/gnome/`
- `ftp://gd.tuwien.ac.at/hci/GNOME/`
- `http://gd.tuwien.ac.at/hci/GNOME/`
- `ftp://linux.a2000.nl/gnome/`
- `ftp://sunsite.icm.edu/pub/Linux/GNOME/`
- `ftp://sunsite.mff.uni.cz/X11/Desktops/`
- `ftp://unix.hensa.ac.uk/mirrors/ftp.gnome.org/pub/GNOME/`

### 亚洲：

- `ftp://ftp.kddlabs.co.jp:/X11/GNOME`
- `ftp://ftp2.sinica.de/pub2/gnome`

### 南美：

- `ftp://ftp.infum.cl/pub/Linux/Gnome`
- `ftp://linuxxlabs.sci.uf.br/pub/gnome`

对于 Debian Linux、Red Hat Linux、Slack Linux、Stampede Linux、S.S.E. Linux 发行版，在某些架构 i386、PPC 和 Sparc 中存在可下载的二进制包。GNOME 太大，无法轻松放入一组特定的包中；特定 Linux 发行版的可用包及其安装顺序在所有平台上并不一致。处理特定发行版的包说明请参见 `http://www.gnome.org/gnome-1.0/`。大多数包分为应用程序和开发两组，只有当你打算开发 GNOME 应用程序时才安装后者。

## 从源码编译 GNOME

由于 GNOME 环境的大小和复杂性以及 Linux 系统的变性，从源码编译 GNOME 是一个既漫长又痛苦的过程。因此，只有具有编译 Linux 应用程序经验的人才建议从源码编译 GNOME。不建议 5.x发行版的用户从源码编译，因为 GNOME 是为 6.x 发行版编写的。它假设系统不仅包含较新的 `libc`，还包含许多其他 6.x 组件。几个发行版的 5.x 版本所示表 12.1。

| 发行版 | 最后 libc5 版本 | 最后 libc6 版本 |
| --- | --- | --- |
| Red Hat Linux | 4.2 | 5.0 |
| Caldera OpenLinux | 1.3 | 2.2 |
| Slackware Linux | 4.0 | 无 |
| Debian GNU/Linux | 1.3.1 | 2.0 |
| S.S.E. Linux | 5.3 | 6.0 |

同样重要的是理解，即使在某些 6.x 发行版上安装 GNOME 1.0 可能需要大量升级依赖 GNOME 使用组件的其他应用程序。要从源码编译 GNOME，从你选择的 GNOME 镜像的 `gnome-1.0/` 子目录下下载所有 GNOME 1.0 源码文件。你可能还需要 GNOME 1.0 编译页面左底部列出的几个图形支持库：`http://www.gnome.org/start/gnome.html`。注意，这些库是 Linux 系统常见的较版本库，因此在编译和安装任何这些或 GNOME 1.0 正确包之前，最好将其与已安装的 Linux 包进行检查以查看是否存在冲突。如果你发现冲突，将不得不决定如何妥善处理。此类讨论超出了本书的范围，如果你发现了无法解决的冲突，对你来说最好使用二进制包或等待 GNOME。大多数 GNOME 1.0 源码文件可以使用基本命令进行编译和安装，这些命令可能来自第 11 章“KDE 1.11 环境”。这些命令按顺序如下：

```
tar -xzvf gnome-component-version.tar.gz
cd gnome-component-version
./configure
make; install
```

注意，这一系列命令会将 GNOME 1.0 及其组件安装到 `/usr/local` 目录树中。如果你想为 GNOME 选择另一个位置，重要的是在你编译每个包时，使用以下命令代替调用 `configure`：

```
./configure --help
```

在执行此命令后，你将看到一个配置选项列表，包括指定安装位置的选项以及指定之前编译组件安装位置的选项。注意，包的编译顺序非常重要，如果乱序编译，编译将不会成功。对于正确的编译顺序以及从源码编译和安装 GNOME 1.0 的完整详细说明，请参阅提供的 GNOME 1.0 编译页面。源码包应该按照在页面左侧列出的顺序进行编译。

## 启动 GNOME

在解决所有褶皱后，启动 GNOME 是一个相当简单的过程。由于 Enlightenment（最常用的 GNOME 窗口管理器）在从源码编译时会将二进制文件安装在非标准位置，这使得过程变得稍微复杂。

如果你是从二进制包安装的 GNOME，那么启动 GNOME 可能只需简单地确保 GNOME 二进制文件的路径在你的 `PATH` 变量中，然后执行 GNOME 会 命令即可。在你的 `$HOME/.xinitrc` 文件中而不是窗口管理器中调用 GNOME 可能需要如下：

```
export PATH=$PATH:/opt/gnome/bin
gnome-session
```
