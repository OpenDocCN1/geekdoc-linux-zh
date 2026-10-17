
```bash
tar zcvf /tmp/etcX11bkup.tar.gz /etc/X11
```

当每个文件被复制到压缩的 tar 存档中时，`tar` 命令会显示文件名列表。在这种情况下，选项是 `zcvf`，目标是 `etcX11bkup.tar.gz`（在 `/tmp` 目录中），源是 `/etc/X11` 目录（这意味着其所有子目录及其内容）。`z` 选项使 `tar` 压缩存档。`c` 选项创建存档，`f` 指定文件名，`v` 指示 `tar` 详细输出（意味着在工作时显示大量信息）。

![](img/b7e91b81e0d84c8a5261ee14a48991b2_354_0.png)

我将 `.tar.gz` 显示为存档的文件扩展名，因为这是指示压缩 tar 存档的惯用方式。对于未压缩的 tar 存档，惯用的文件扩展名是 `.tar`。当使用 `z` 选项压缩存档时，会添加 `.gz` 部分。`.gz` 来自 `gzip`——用于压缩文件的 Linux 命令。有时，压缩的 tar 存档也使用 `.tar.Z` 扩展名。

开源软件源代码文件通常以压缩的 tar 存档形式分发。这些带有 `.tar.gz` 或 `.tar.Z` 扩展名的文件通常被称为压缩 tarball。如果你需要该软件，你必须下载压缩的 tarball，解包并构建它。

要查看你之前创建的压缩 tarball `/tmp/etcX11bkup.tar.gz` 的内容，请键入以下命令：

```bash
tar ztf /tmp/etcX11bkup.tar.gz
```

你应该会看到文件名列表（每个都以 `/etc/X11` 开头），指示备份中的内容。在此 `tar` 命令中，`t` 选项列出 tar 存档的内容，`z` 负责解压缩存档。

要从 tarball 中提取文件，请按照以下步骤操作：

1. 通过键入以下命令将目录更改为 `/tmp`：

   ```bash
   cd /tmp
   ```

2. 键入以下命令：

   ```bash
   tar zxvf etcX11bkup.tar.gz
   ```

此 `tar` 命令使用 `x` 选项从 tarball `etcX11bkup.tar.gz` 中存储的存档中提取文件。

如果你检查 `/tmp` 目录的内容，你应该会看到 `tar` 命令在 `/tmp` 中创建了一个 `etc/X11` 目录树，并将所有文件从存档提取到该目录中。

这让你了解了 `tar` 命令的用法。现在，如果你遇到 tarball，你知道该怎么处理了！

### pico：编辑文本文件

`pico` 命令会运行 SUSE Linux 附带的文本编辑器。它比 `vi` 和 `ed` 文本编辑器更容易学习，并且在需要编辑文本配置文件时非常方便。

![](img/b7e91b81e0d84c8a5261ee14a48991b2_355_0.png)

如果你计划编辑任何系统配置文件（例如 `/etc/fstab`），请先备份该文件。例如，要保存 `/etc/fstab` 文件的副本，请通过键入 `su -` 成为 root，然后键入 `cp /etc/fstab /etc/fstab.saved`。编辑完原始 `/etc/fstab` 文件后，如果遇到任何问题，可以通过键入 `cp /etc/fstab.saved /etc/fstab` 恢复到已保存的版本。

要使用 `pico` 编辑文件（或创建新的文本文件），只需在终端窗口中键入 `pico filename`。图 23-1 显示了 `pico` 编辑器的典型文本模式显示。

![](img/b7e91b81e0d84c8a5261ee14a48991b2_355_1.png)

**图 23-1：** 在 `pico` 编辑器中编辑文本文件。

要添加文本，只需开始输入即可。你可以使用箭头键移动光标。最后两行（参见图 23-1 窗口底部）提供了其他 pico 命令的提示。例如，要保存文件，请按 Ctrl+O（按住 Ctrl 键，然后按 O）。要退出，请按 Ctrl+X。我相信你可以通过练习很快学会 pico。

## 附录：关于 DVD-ROM

### 本附录包含

- 系统要求
- DVD 安装说明
- DVD 中包含的内容
- 故障排除

本书附带的 DVD 包含 SUSE Linux 10.0 特别版，助你开启 Linux 学习之旅。此版本的 SUSE Linux 10.0 包含来自 openSUSE 项目的 SUSE Linux 10.0 开源软件（OSS），以及一些额外内容，如 Acrobat Reader、RealPlayer 10 和用于 Web 浏览器的 Macromedia Flash 插件。你可以直接从 DVD 运行 SUSE Linux，也可以将 SUSE Linux 安装到 PC 上。本附录简要介绍 DVD 的内容，并说明如何开始安装。

### 系统要求

请确保你的计算机满足以下列表所示的最低系统要求。如果你的计算机与这些要求中的大多数不匹配，则在使用 DVD 上的软件和文件时可能会遇到问题：

- 一台配备 Intel Pentium 或兼容处理器且主频为 400 MHz 或更高的 PC（用于图形化安装）
- 计算机至少安装 256MB 总内存（用于图形化安装，建议 512MB）
- 硬盘上至少要有 520MB 可用空间才能进行最小化安装；如果你打算安装大部分软件包，建议留出 5GB 可用空间，以便试用本书涵盖的所有内容
- 一个 DVD-ROM 驱动器

### DVD 安装说明

要从随书 DVD 安装 SUSE Linux，请按照以下步骤操作（详见第 2 章）：

![](img/b7e91b81e0d84c8a5261ee14a48991b2_358_0.png)

1. **检查 PC 的硬件（如显卡、网卡和 SCSI 卡）是否能在 SUSE Linux 中正常工作。如果不能，请尝试为该设备寻找 Linux 驱动程序。**

    要检查 PC 的硬件是否与 SUSE Linux 兼容，请访问 `hardwaredb.suse.de` 上的 SUSE Linux 硬件数据库。如果你为任何设备下载了 Linux 驱动程序，应将它们刻录到 CD 上妥善保管。

2. **将 PC 设置为从 CD/DVD 驱动器启动（为此，你需要在 PC 启动时进入 SETUP）。**

3. **使用 DVD 启动 PC。**

4. **在初始启动屏幕上选择 Installation（安装），然后按 Enter 键。**

    SUSE Linux 安装程序——YaST——将运行并显示图形化界面，你可以通过它执行安装步骤。在安装程序引导你完成初始安装步骤时，请回答相关问题并做出选择。以下是一些关键步骤：

    - 查看 YaST 推荐的硬盘分区方案。如果你的硬盘上安装了 Microsoft Windows（任何版本），YaST 可以缩小 Windows 分区的大小，为 SUSE Linux 腾出空间。你不需要任何其他分区软件。
    - 设置本地时区。
    - 选择 GUI 桌面环境——KDE 或 GNOME。

5. **YaST 会在初始安装后重新启动系统，并继续完成 SUSE Linux 的进一步安装和配置。**

    安装更多软件包后，YaST 会继续对系统进行配置。以下是你必须完成的一些关键配置步骤：

    - 配置以太网（如果有）。通常，你可以使用 DHCP 自动配置网络。
    - 设置 root 密码。
    - 添加用户账户（你通常使用此账户登录）。
    - 配置显卡、声卡和打印机等硬件。

### DVD 中包含的内容

本节概述 DVD 上可以找到的软件和其他实用程序。如果你在安装 DVD 提供的项目时需要帮助，请参阅上一节中的安装说明。

![](img/b7e91b81e0d84c8a5261ee14a48991b2_359_0.png)

GNU 软件受其自身许可证的约束，该许可证包含在 GNU 软件的文件夹中。GNU 软件的分发不受限制。详情请参阅 DVD 根目录或本书末尾的 GNU 许可证。按照 GNU 许可证的要求，Novell 提供 SUSE Linux 源代码。你可以从以下 URL 下载 SUSE Linux 的源代码：

```
http://ftp.opensuse.org/pub/opensuse/distribution/SL-OSS-stable/inst-source/suse/src/
```

DVD 包含 SUSE Linux 10.0 特别版。随书 DVD 上的 SUSE Linux 版本包含来自 openSUSE 项目的 SUSE Linux 10.0 OSS 的所有基本功能，以及一些额外内容：

- KDE 或 GNOME 图形桌面环境，任你选择
- Konqueror Web 浏览器和文件管理器
- 用于播放 CD 和 DVD、刻录 CD 以及抓取音频 CD 的多媒体工具
- 办公软件，即广受赞誉的 OpenOffice.org 套件
- 照片和图形编辑软件，如 The GIMP，以及更多其他软件
- 额外附赠内容，如 Acrobat Reader、RealPlayer 10 和用于 Web 浏览器的 Macromedia Flash 插件
