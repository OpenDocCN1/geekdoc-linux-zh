
```bash
# .bashrc
# 用户特定的别名和函数

alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'

# 挂载全局定义
if [ - /etc/bashrc ]; then
  /etc/bashrc
```
你可以将任何你自定义的命令或定义添加到你的 `.bashrc` 文件中。如果你对 `.bashrc` 制作了更改，并希望这些更改在当前登录会话中生效，你需要使用 `.` 或 `source` 命令重新执行该文件。

`$ .bashrc`

### 级 `/etc/bashrc` BASH 脚本

Fedora 有一个为所有用户执行的系统 bash 脚本，称为 `/etc/bashrc`。目前 `/etc/bashrc` 文件设置了默认的 bash 提示符，以及检查用户是否有权限使用某个命令的指令。在交互式 shell 中，`/etc/bashrc` 文件将决定默认提示符。如果不是登录 shell，它将确定 `PATH` 并运行 `profile.d` 脚本。

注意：`/etc/bash_completion.d` 目录下的 `.bash_completion` 文件为应用程序提供了命令补全。

### Bash Shell 退出文件：`.bash_logout`

`.bash_logout` 文件也是配置文件，但它是在用户注销时执行的。它的设计是为了在你每次注销时执行任何任何操作。变量定义不同，`.bash_logout` 文件通常包含形成某种关机程序的命令——即你在注销之前总是想要执行的操作。一个常用的命令是清除屏幕然后发出告别信息。

`.bash_logout`

```bash
# ~/.bash_logout: 当 bash(1) 登录 shell 退出时执行。
# 离开控制台时清除屏幕以增加隐私
if [ "$SHELL" = 1 ]; then
  [ -x /usr/bin/clear-console ] && /usr/bin/clear-console -q
fi
```

`echo "Good-bye for now",`

就像 `.bash_profile` 一样，你可以将自己的 shell 命令添加到 `.bash_logout` 中。默认的 `.bash_logout` 文件包含了调用 `clear-console` 命令清除屏幕的指令。在下一个示例中，用户在 `.bash_logout` 文件中添加了一个 `echo` 命令。

## 附录 A：获取 Fedora

Fedora Linux 发行版安装了一个专业级且非常稳定的 Linux 系统，并带有 KDE 和 GNOME 图形界面、灵活易用的系统配置工具、一套广泛互联网服务器、各种不同的多媒体应用程序以及数千种各种 Linux 应用程序。你可以在 `fedaproject.org` 获取有关 Red Hat Fedora 项目的最新信息。

大多数 Fedora 软件都可以从 Fedora 仓库下载。也提供安装磁盘，可以是较小的仅桌面版安装，也可以是较大的服务器安装版。你可以使用 Live CD 安装 Fedora。Fedora 发行版策略依赖于带有精选软件集合的安装磁盘，这些软件稍后从 Fedora 仓库中海量的软件集中进行更新和增强。这意味着初始安装中的软件集合可能相对较小。Fedora 仓库中的软件也在不断更新，因此任何安装都可能需要从仓库进行大量的更新。

### 下载镜像映像

要获取 Fedora 9，只需访问 Fedora 项目网站并点击 Get Fedora 链接。在这里，你将看到针对不同 Fedora 安装 DVD 和 Fedora Live 版本的 torrent 或直接下载链接。Direct downloads 链接指向当前可用的镜像站。

```
http://fedaproject.org/get-fedora
```

你可以通过输入以下 URL 直接访问 Fedora 镜像站。然后，你需要浏览版本和目录，找到存放 Fedora 安装映像和 Live 映像的 Fedora 和 Live 目录。

```
download.fedaproject.org
```

你也可以通过以下 URL 访问特定的镜像。这里将列出当前的 Fedora 镜像及其地址。

```
mirrors.fedaproject.org
```

关于所有 Fedora 下载选项的详细描述，包括你需要的所有 ISO 文件和镜像站的链接，可以在以下 URL 获取。请检查此站点获取最新的下载程序。

`http://fedoraproject.org/wiki/Distribution/Download`

或者，你仍然可以使用 `download.fedora.redhat.com` 上的链接直接从 Fedora 站点下载。

`download.fedora.redhat.com/pub/fedora/linux/releases/`

使用宽带 DSL 或电缆，配合如 `gFTP`（应用程序 | Internet 菜单）之类的 FTP 客户端，直接下载可以非常快。使用 Firefox 等浏览器的 Web 客户端下载往往较慢。

### 安装 Live 映像

要从 DVD/CD-ROM 驱动器下载用于安装 Fedora 9，你需要下载 Fedora Install DVD 映像或 Fedora Live 映像。扩展名为 `.iso` 的大文件。Fedora Install DVD 位于 Fedora 子目录下，对应版本（i386, x86, 64 和 PPC）的任何目录中（`Fedora/i386/iso`）。Live 映像位于 Live 子目录下，对应版本（i686, x86, 64 和 PPC）之下。一旦下载，你可以使用你的 CD 或 DVD 刻录机和刻录软件（如 Fedora 中的 Nautilus 文件浏览器或 K3）将它们刻录到磁盘。

有各种架构的 ISO 文件。Live CD/DVD 提供了一种无需安装到硬盘即可运行系统的方法，这对于测试操作系统或执行系统恢复很有用。

### 使用 Live 映像

从 DVD/CD-ROM 驱动器下载用于安装 Fedora 9，你需要下载 Fedora Install DVD 映像或 Fedora Live 映像。扩展名为 `.iso` 的大文件。Fedora Install DVD 位于 Fedora 子目录下，对应版本（i386, x86, 64 和 PPC）之下。

Live 映像默认启用 `NetworkManager`，自动检测并连接你的网络连接。Live DVD/CD 有一个默认用户名且没有密码。

## 附录 B：Fedora Live DVD/CD

通过 Fedora Live DVD/CD，你可以从任何 CD/ROM 驱动器运行 Fedora。某些映像使用 CD，另一些使用 DVD。实际上，你可以只通过一个 DVD/CD 携带你的操作系统。新用户也可以使用 Live DVD/CD 检查他们是否喜欢。文件和数据可以写入 USB 驱动器等移动设备，但无法更改操作系统配置。你也可以挂载运行 Live DVD/CD 系统的硬盘分区。

Fedora 提供的 Live DVD/CD 包含非常有限的软件软件包。没有提供 OpenOffice 应用，只有 Abiword 用于文字处理和 Gnumeric 用于电子表格。尽管有限制，你拥有一个功能完整的 Fedora 桌面。你拥有全套管理工具，可以在 Live DVD/CD 运行时使用它们添加用户并更改配置设置。当你关机时，配置将丢失。

你可以注销，这将显示带有简单登录按钮和语言菜单的登录界面。你可以使用语言菜单更改语言。但你无法从登录菜单关机或重启。你只能从桌面操作。

# Fedora 自定义版本 (Custom Spins)

自定义版本也由特殊兴趣小组提供，请参见 `fedoraproject.org/wiki/CustomSpins`。这些版本可以从 `spins.fedoraproject.org` 下载，该页面列出了 Fedora Project Spins 跟踪器上的 Torrent 文件。这些版本包括：

- Fedora 开发版 (Developer Spin)：仅限 i686 架构。包含 GNOME 桌面以及如 Eclipse IDE 等开发应用程序，以及调试和性能分析工具及文档。
- Fedora Creative Commons (cc)：仅限 i686 架构。CD 格式。为 Creative Commons 项目的免费分发 GNU 许可软件和媒体而设计。
- Fedora 游戏版 (Games Spin)：目前为 Live DVD。为游戏玩家配置的 Fedora，包含丰富的游戏集合。
- Xfce 版本 (Xfce Spin)：使用 Xfce 桌面。

下载后，你可以将镜像刻录到 DVD（i686 版本使用 CD）。

# USB Live 启动盘

你也可以将 Fedora Live 安装到 USB 盘上。USB 盘上的原始数据将被保留。从开发存储库下载 `livedcd-tools`，然后使用 `livedcd-to-disk` 命令安装镜像。使用 Live 镜像和 USB 设备名称作为参数。

```
/usr/bin/livedcd-iso-to-disk Fedora-9-Live-i686.iso /dev/sdb1
```

如果你想在 USB Live 版本上保存 Fedora 操作系统的更改，请在 USB 驱动器上设置覆盖内存段（overlay memory segment）。要此操作，请使用 `--overlay-size-mb` 选项并指定 MB 为单位的大小。确保你的 USB 驱动器足够大，能够容纳覆盖内存和 CD 镜像。以下命令允许 512 MB 的持久化数据。

```
livedcd-iso-to-disk --overlay-size-mb 512 Fedora-9-Live-i686.iso /dev/sdb1
```

每个 CD 在你的 LiveOS 目录下也都提供了一个 lived 脚本。

# 启动 Live DVD/CD

启动时，你可以按下空格键显示启动选项。选项包括直接启动 Live DVD/CD（默认）、首先验证磁盘介质、进行内存测试或启动硬盘上已有的另一个操作系统。如果你不按任何键，Live DVD/CD 将自动启动。系统启动后，你将看到标准的登录界面（KDE 磁盘将直接引导到桌面）。使用用户 `fedora` 访问，或直接按回车键。在密码提示符处按回车键。GNOME（见图 B-1）或 KDE（见图 B-2）将启动。

请记住，使用硬盘运行 Fedora 与在硬盘上安装 Fedora 是不同的。从硬盘运行是标准的 Fedora Live 操作，它使用硬盘空间作为 Live DVD/CD 磁盘镜像。点击桌面上的“安装到硬盘”（Install to Hard Drive）图标图标标准的 Fedora 安装过程，将 Fedora 安装到你的系统中，就像进行普通安装一样。

# 附录 B：Fedora Live DVD/CD 419

![](img/6775ff646544702d90d6288b3c111705_420_0.png)

图 B-1：Fedora Live CD

# 在 KDE 上使用 USB 盘

KDE Live CD 使用新的 Plasma 桌面和面板。USB 盘不再以图标形式显示在桌面上。USB 盘的图标将同时出现在 Kickoff 菜单和文件管理器侧边栏中。要挂载驱动器，只需点击其图标。驱动器上会出现一个挂载标记（见图 B-3）。在文件管理器窗口中，点击侧边栏中的 USB 盘项以打开 USB 盘的文件列表。然后你可以将文件保存到驱动器。

![](img/6775ff646544702d90d6288b3c111705_420_1.png)

图 B-2：Fedora KDE Live CD

# 420 附录

![](img/6775ff646544702d90d6288b3c111705_421_0.png)

图 B-3：Fedora Live CD USB 盘

要移除 USB 盘，你必须先选择移除选项。在文件管理器侧边栏（或 Kickoff 菜单）中右键点击 USB 盘。这将打开一个带有“安全删除卷”（Safely remove Volume）选项的菜单。选择此选项以完成向驱动器写入任何数据（见图 B-4）。挂载标记将从 USB 图标消失，然后你可以安全地移除 USB 盘。

![](img/6775ff646544702d90d6288b3c111705_421_1.png)

图 B-4：Fedora Live CD 移除 USB 盘

# 从 Live CD 安装 Fedora

Live CD 可用作安装盘，为系统提供其有限的软件集合，安装一个完整的 Fedora 操作系统，该系统可以从 Fedora 在线存储库进行扩展和更新。在这种情况下，你不需要下载完整的 Fedora 安装盘，只需 Live CD，并在稍后从存储库添加包。双击桌面上的“安装到硬盘”图标开始安装。从 Live 磁盘安装将默认启用 NetworkManager 并禁用 SSH 守护进程 (`sshd`)。

# 创建你自己的 Live CD

你也可以创建自己的 Live CD...（注：原文此处存在大量重复文本，已按要求处理，保留核心意图）...

Live CD 可用作安装盘，为系统提供其有限的软件集合，安装一个完整的 Fedora 操作系统，该系统可以从 Fedora 在线存储库进行扩展和更新。在这种情况下，你不需要下载完整的 Fedora 安装盘，只需 Live CD，并在稍后从存储库添加包。

你也可以创建自己的 Live CD...（注：原文此处存在大量重复文本）...

# 表列表

| 表 | 描述 | 页码 |
| :--- | :--- | :--- |
| 表 1-1 | Fedora | 32 |
| 表 2-1 | 基础管理工具 | 46 |
| 表 2-2 | Fedora 配置 | 47 |
| 表 2-3 | 系统目录 | 48 |
| 表 2-4 | 配置和目录 | 50 |
| 表 2-5 | 带有系统管理工具的配置文件 | 51 |
| 表 2-6 | cron 文件和目录 | 58 |
| 表 3-1 | 系统启动文件和目录 | 70 |
| 表 3-2 | 运行级别 (状态) | 72 |
| 表 3-3 | 关机选项 | 74 |
| 表 3-4 | chconfig 选项 | 77 |
| 表 4-1 | Fedora 和 Linux 软件站点 | 89 |
| 表 5-1 | rsyslog 设施、优先级和运算符 | 113 |
| 表 5-2 | 性能工具 | 117 |
| 表 6-1 | 用户配置文件路径 | 127 |
| 表 6-2 | chage 命令选项 | 132 |
| 表 6-3 | useradd 和 usermod 选项 | 133 |
| 表 6-4 | edquota 选项 | 138 |
| 表 6-5 | quota 选项 | 138 |
| 表 7-1 | 内核 make 命令的编译选项 | 162 |
| 表 8-1 | 虚拟化资源 | 167 |
| 表 10-1 | PGP 站点 | 191 |

## 表列表

- 表 10-1: GPG 命令与选项 ................................................................ 202
- 表 11-1: 文件和目录权限操作 ....................................................... 215
- 表 12-1: SELinux 资源 ............................................................................... 227
- 表 12-2: SELinux 工具 ....................................................................... 234
- 表 12-3: SELinux 策略配置文件 ................................................. 249
- 表 13-1: SSH 和 Kerberos 资源 ................................................................... 253
- 表 13-2: SSH 工具 ............................................................................................ 256
- 表 13-3: SSH 配置文件 ........................................................ 259
- 表 14-1: 网络安全应用 ................................................................ 269
- 表 14-2: Iptables 目标 ................................................................................ 275
- 表 14-3: Netfilter 内置链 ................................................................ 276
- 表 14-4: Iptables 命令 ....................................................................... 277
- 表 14-5: Iptables 选项 ................................................................................. 279
- 表 14-6: 常见 ICMP 包 ................................................................ 281
- 表 15-1: Linux 文件系统目录 ...................................................... 301
