
- 减少系统上的控制台（consoles）数量（如提示 4.31“减少低内存 Linux 系统上的虚拟控制台数量”中讨论）
- 将系统服务精简为仅核心部分（如提示 4.32“在低内存 Linux 系统上启动时仅启动核心系统服务”中讨论）

关于在低内存系统上运行 Linux 的概述，可以在 Small Memory-HOWTO 中找到：`http://linux.com/howto/mini/Small-Memory.html`。

## 提示 10.4.30：为低内存 Linux 系统构建内核

典型的 Linux 发行版包含一个默认的臃肿 Linux 内核：它包含了许多模块和驱动程序，这些对于你系统的运行并非必需，但它们是为了使内核具有通用性，以便能够在各种系统中运行。

为了优化内核，你可以像提示 4.8“重新编译你的内核”中讨论的那样重新编译，但只需关注运行你系统所需的组件。不要包含不必要的硬件支持。如果你的系统只有一个网卡，则仅包含对该网卡的支持。如果你的系统不使用 `PPP`，不要包含其支持。同样，你不需要软件支持也应该排除。如果你的系统仅使用标准的 `ext2` 文件系统，且永远不访问 DOS 或 Windows 磁盘，不要包含对 DOS 文件系统的支持。这只会白白消耗系统内存。

## 提示 10.4.31：减少低内存 Linux 系统上的虚拟控制台数量

通常，Linux 发行版配置为用户提供六个或更多虚拟控制台。如果你在控制台上进行繁重工作，这些虚拟控制台会很有用。但低内存系统通常只处理少数专用任务，使用过多的虚拟控制台可能会浪费高达 4 MB 的系统内存。

理想情况下，你希望尽可能减少虚拟控制台的数量。Small Memory Mini HOWTO (`http://linux.com/howto/mini/Small-Memory.html`) 建议减少到三个或四个控制台，但没有理由不减少到两个控制台。减少到一个控制台并不是个好主意，因为当你在主控制台上长时间运行任务时，有一个可用的备份控制台是有用的。拥有一个额外的控制台可以提供访问系统的备份途径。

你可以通过以下步骤编辑 `/etc/inittab` 文件来减少系统上的虚拟控制台数量：

1. 以 `root` 用户身份登录。你将看到 `root` 命令提示符。
2. 使用你喜爱的文本编辑器编辑 `/etc/inittab` 文件。例如，使用 `Emacs` 编辑文件，命令为 `emacs etc/inittab`。
3. 在 `/etc/inittab` 文件中找到以下系列行：

```
1:2345:respawn://sbin/mintty tty1
2:2345:respawn://sbin/mintty tty2
3:2345:respawn://sbin/mintty tty3
4:2345:respawn://sbin/mintty tty4
5:2345:respawn://sbin/mintty tty5
6:2345:respawn://sbin/mintty tty6
```

4. 从最后一行（以最高数字开始的行）开始，注释掉每个不需要的虚拟控制台（在行首放置哈希标记）。例如，如果你只需要两个虚拟控制台，结果如下：

```
1:2345:respawn://sbin/mintty tty1
2:2345:respawn://sbin/mintty tty2
#3:2345:respawn://sbin/mintty tty3
#4:2345:respawn://sbin/mintty tty4
#5:2345:respawn://sbin/mintty tty5
#6:2345:respawn:// /sbin/mintty tty6
```

5. 使用你编辑器的标准程序保存文件并退出编辑器。
6. 使用命令 `/sbin/reboot` 重启电脑。

## 提示 10.4.32：在低内存系统上启动时仅启动核心系统服务

大多数典型的 Linux 发行版会启动许多守护进程（daemons），它们提供了一个强大且功能丰富的系统，但对于专注于一个或少数任务的功能系统（如低内存系统）来说并不是必需的。困难之处在于这些守护进程：

- `inetd`：`inetd` 守护进程用于启动如 `telnet` 等服务；如果你的系统不会作为服务器，你不需要 `inetd`。
- `lpd`：如果你的系统没有打印机，你不需要 `lpd`。
- `nsfd`：如果你的系统不会作为 Unix 服务器，你不需要 `nsfd`。
- `smbd`：如果你的系统不会与 Windows 共享目录，你不需要 `smbd`。
- `sendmail`：如果你的系统不会直接接收邮件，你不需要 `sendmail`。

## 提示 10.4.33：可以容于软磁盘的 Linux 发行版

目前有几种所谓的 Linux 微型发行版可供选择。所有这些微型发行版都设计用于适应小内存或小磁盘空间。常见的微型发行版包括：

- Linux Router Project（Linux路由器项目）：`Linux Router Project` 是一种专为路由器和防火墙设计的软磁盘发行版，尽管它也可以用于创建终端。
- `DLX`：`DLX` 是一个功能全 Linux 发行版，可以放入软磁盘，并包含了网络和并行支持。`DLX` 可以从 `http://www.wu-wien.at/ucsr/h93/30172/dlx.html` 获取。
- `Tomsrt`：`Tomsrt` 是一种基于软磁盘的 Linux 发行版，旨在系统诊断和故障排除。用于检查和修复硬盘的实用工具是该发行版的一部分。`Tomsrt` 可以从 `http://www.toms.net/trbl/` 获取。
- `Trinx`：`Trinx` 是一种从单软磁盘启动并从其他软磁盘加载系统其余 Linux 发行版。`Trinx` 甚至可以从 Web 或 FTP 服务器加载包。`Trinx` 可以从 `http://www.trinx.org/` 获取。

## 提示提示：在软磁盘上构建你自己的完整 Linux 系统

你可以使用提示 4.33“可以容于单张软磁盘的 Linux 发行版”中列出的软磁盘发行版在软磁盘上构建 Linux 系统。对于本提示，你将使用 Linux Project 发行版。`Linux Router Project` 发行版网站为 `http://www.linuxrouter.org`。

你可以按照以下步骤在现有的 Linux 系统上创建 `Linux Router Project` 启动软：

- 从 `ftp:/ftp.linuxrouter.org/linux-router/dists/2.9.8/idiot-image_1440KB_FAT_2.9.8_Linux_2.2.gz` 下载 `Linux Router Project` 的最新磁盘镜像，并保存到方便的位置，例如 `/tmp`。`idiot-image_1440KB_FAT_2.9.8_Linux_2.2.gz` 是包含基础 Linux Router 发行版的软磁盘文件。
- 使用命令解压镜像文件：

```
# gzip -d /tmp/idiot-image-1440KB_FAT_2.9.8_Linux_2.2.gz
```

# 让 LINUX 运行起来：核心技巧与技术

1. 将一张空白且格式化过的软盘插入软盘驱动器。
2. 使用以下命令将 Linux 路由器镜像拷贝到软盘：

```
# dd if=/tmp/idiot-image_1440KB_FAT_2.9.8_Linux_2.2 of=/dev/fd0<ENTER>
```

如果你将软盘插入了第二个软盘驱动器（DOS 中的 `B:`），请将 `/dev/fd0` 替换为 `/dev/fd1`。

你现在可以从软盘启动 Linux 路由器系统了。如果你需要安装模块来支持硬件，可以在 `http://www.dcn.davis.ca.us/~jdnewmill/lrp/modulenotes.html` 找到一份良好的 LRP 模块列表。

# 技巧 10.4.35：获取 Perl

Perl 在互联网上免费提供给多个平台使用，包括 Linux。你始终可以通过执行以下步骤下载最新版本：

1. 在浏览器中加载 URL `http://www.perl.com/`。
2. 点击鼠标上的 `Downloads`（下载）链接。你的浏览器随后会加载 `Downloading Perl Software` 页面。
3. 点击鼠标上的 `Stable Production Release`（稳定生产版）源码发行版。你的浏览器随后会下载 `Stable Production Release` 页面。
4. 点击鼠标上的 `stable.tar.gz` 链接。你的浏览器随后将下载 Perl 的最新源码版本。

除了下载 Perl 的源码发行外，每个 Linux 发行版都包含了预编译的 Linux 二进制文件，包括 `CalderaDesktop`、`Corel Linux`、`RedHat Linux`、`Debian Linux` 和 `Slackware Linux`。

# 技巧 10.4.36：从 RedHat 或 Caldera CD-ROM 安装 Perl

要从你的 `RedHat Linux 7` CD-ROM 安装 Perl，将 CD-ROM 插入 CD-ROM 驱动器并使用以下命令挂载它：
