
如果出于某种原因无法引导或访问系统，可能是因为配置、库或应用程序发生冲突。在这种情况下，你可以将 Linux 系统引导至救援模式，然后使用 Vi 等文本编辑器编辑配置文件，删除可疑的库，或使用 `RPM` 重新安装损坏的软件。要进入救援模式，请使用 CD-ROM 或 DVD-ROM 引导盘，并在初始菜单中选择 **救援已安装系统（Rescue Installed System）**。

系统将启动到命令行模式，且系统文件已挂载在 `/mnt/sysimage`。你会收到通知，可以使用 `chroot` 命令将系统目录设置为根目录 `/`。在命令行提示符处输入以下命令：

```bash
chroot /mnt/sysimage
```

使用 `cd` 命令在不同目录之间移动。检查 `/etc` 和 `/etc/sysconfig` 中的配置文件。你可以使用 Vi 编辑文件，并使用 `less` 命令查看文件。若要重新安装文件，请使用 `rpm` 命令。完成后，输入 `exit` 命令。如果你有命令行系统，在引导提示符处输入：

```bash
linux rescue
```

你还可以下载并创建 Linux 救援 CD。只需从 Fedora 仓库下载 Linux 救援 CD 的 iso 文件，并使用该光盘引导即可。

## 重新安装引导加载程序

如果你使用的是双引导系统，即在同一台机器上同时运行 Windows 和 Linux，你可能会遇到需要重新安装 GRUB 引导加载程序的情况。如果 Windows 系统完全崩溃且无法修复，你需要安装新版 Windows，或者在已安装 Linux 的机器上添加 Windows 时，都会出现此问题。Windows 会自动覆盖你的引导加载程序（或者，你可以选择将引导加载程序安装到 Linux 分区而不是 MBR）。届时你将无法再访问你的 Linux 系统。

你只需要重新安装引导加载程序即可。首先使用 Linux DVD/CD-ROM 安装盘引导，并在菜单中选择 **救援已安装系统（Rescue Installed System）**。

如前一节所述，这将使系统以救援模式启动。然后使用 `grub-install` 和你第一个分区的设备名称来安装引导加载程序。Windows 通常希望位于包含 MBR（主引导记录）的第一个分区上。你需要指定该分区。在提示符处输入：

```bash
grub-install /dev/hda1
```

> **提示** 即使你的 Linux 救援盘也无法访问系统，你也可以使用 Fedora Live CD 启动 Fedora，然后手动挂载你的 Fedora 分区。你需要知道分区设备名称（使用 GParted）。一旦挂载，你就可以访问已挂载分区上的系统文件并进行必要的更改。

## 使用 Pungi 创建自定义 Fedora 安装光盘

你可以使用 Pungi 创建自己的发行版光盘。Pungi 工具使用位于 `/etc/pungi` 目录中的配置文件。它将生成一组基本软件包，并从 Fedora 仓库下载它们。默认设置列在 `pungi.conf` 文件中。要添加到安装光盘的软件包按类别列在 `minimal-manifest` 文件中。它使用与 kickstart 相同的语法。`/etc/pungi` 目录中的 `comps.xml` 文件定义了你的发行版的软件包分组。`/etc/pungi/comps-fc7.xml` 文件将保存 Fedora 7 的软件包分组。这些分组与你在“添加/删除软件”浏览面板中看到的分组相同。在清单文件中，你可以使用分组名称来将整个软件包组添加到安装光盘中，例如 Desktop（用于所有桌面）或 Servers（用于所有服务器）。对于仅包含子组，只需指示其名称，如 GNOME（仅用于 GNOME 桌面及其软件）或 Editors（仅用于编辑器）。对于特定软件包，选择其唯一前缀，例如 `kmod-fglrx` 用于 ATI 驱动程序。

默认使用的目录是 `/srv/pungi/cache` 和 `/srv/pungi/Fedora`。其他默认设置针对你当前的安装环境设计。你可以通过更改 `/etc/pungi/pungi.conf` 文件中的 `product_name` 条目，或在调用 Pungi 时使用 `--destdir=` 选项指定目录来更改目标目录。Pungi 还需要知道是使用 32 位还是 64 位版本的软件。这是通过 `arch` 选项指定的。此外，Pungi 还必须告知 Yum 使用哪些仓库目录以及是使用 64 位还是 32 位软件包。`yum.conf` 选项设置为包含所有你要检查的仓库的 Yum 配置文件。默认情况下，这些仓库仅包括 Fedora 仓库，但你可以根据需要添加其他仓库。此文件包含的信息与 `/etc/yum/yum.conf` 文件以及 `/etc/yum.repos.d` 目录中的各种仓库文件中的信息大致相同。

64 位和 32 位有单独的 Yum 配置文件。这些文件位于 `/etc/pungi` 目录中。

在 `/etc/pungi` 目录中，你会找到多个可能的 Pungi 配置文件和 Yum 配置文件，以及一个默认版本。Pungi 配置文件的前缀为 `pungi`，Yum 配置文件的前缀为 `yum.conf`。配置文件随后会根据架构进一步区分：i386、x86_64、source 和 ppc。已经有一个设置为 64 位架构的默认 `pungi.conf` 文件。要创建发行光盘，你首先需要决定使用哪种架构以及从哪些 Yum 仓库下载。在设置你的 `pungi.conf` 文件时，首先为你想要的架构复制一份 `pungi-fc7` 配置文件，然后确保在 `pungi.conf` 文件中指定相应的 Yum 配置文件。

例如，要为 64 位机器创建发行版，你将在 `pungi.conf` 文件中指定 x86_64 选项。请确保 `pungi.conf` 文件中的 `yumconf` 选项设置为 `yum.conf.x86_64` 文件。实际上，架构和 Yum 配置必须对应。64 位架构使用 64 位 Yum 仓库，而 ppc 架构将使用 ppc 仓库。在你的 `pungi.conf` 文件中，请确保 `arch` 选项设置为与你的 `yumconf` 选项使用的架构相同。64 位架构的 `arch` 选项设置为 x86_64，而你的 `yumconf` 选项将使用 64 位 Yum 仓库，即 `yum.conf.x86_64`。对于源代码光盘，请使用 source 架构以及对应于你所需架构源代码的 Yum 配置文件。

默认的 Pungi 配置文件是 `/etc/pungi/pungi.conf`。在这里你可以找到创建发行版光盘的选项。如果你想进行更改，可以先备份该文件，或者用它创建一份副本，然后编辑该副本。通过 `--conf=` 选项，你可以指示 Pungi 使用你的新配置文件。无论如何，请保留一份原始 `pungi.conf` 文件的副本以供参考。Pungi 选项列在表 2-1 中。

默认的 `pungi.conf` 文件如下所示：

```ini
pungi.conf

product_name = myFedora ; 安装时使用的名称
product_path = Fedora ; RPM 所在的目录
iso_basename = F ; ISO 映像文件名的第一部分
bugurl = http://bugzilla.redhat.com ; 用于测试标签
comps = /etc/pungi/comps-fc7.xml ; 软件包分组和默认安装
manifest = /etc/pungi/minimal-manifest ; 决定引入哪些内容。Kickstart 语法
yumconf = /etc/pungi/yum.conf.x86_64 ; 从哪里获取软件包
destdir = /srv/pungi/Fedora ; 顶级组合目录，必须干净
cachedir = /srv/pungi/cache ; 用于重复运行的缓存
arch = x86_64 ; 组合的架构（必须与系统架构相同）
version = 7 ; 既用于安装，也是目标树的一部分
flavor = Custom ; 进一步定义给定的软件包集切分
discs = 1 ; 容纳数据所需的光盘数量。
#cdsize = 4608.0 ; 如果光盘数量为 1 则不使用
getsource = YES ; 用于确定是否需要源代码软件包
```

要收集到发行版中的文件列在由 `pungi.conf` 文件中的 `manifest` 选项指定的清单文件中。默认情况下，这设置为 `/etc/pungi/minimal-manifest`，其中包含任何发行版所需的最小软件包集。然后你可以添加更多软件包或更改某些设置。一种策略是复制 `minimal-manifest` 文件并对副本进行更改。然后将更改后的副本作为 Pungi 使用的清单文件，并更改

### 表 2-1 Pungi 选项

| 选项 | 描述 |
| :--- | :--- |
| `product_name` | 安装时使用的名称；默认值为 Fedora。 |
| `product_path` | 存放 RPM 包的目录；默认值为 Fedora。 |
