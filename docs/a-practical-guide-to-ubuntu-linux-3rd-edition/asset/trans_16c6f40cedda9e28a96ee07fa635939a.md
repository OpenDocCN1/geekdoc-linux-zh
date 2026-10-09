

$ sudo aptitude install xxx
...
找不到软件包"xxx"。不过，以下软件包名称中包含"xxx"：
    mixxx mixxx-data
不会安装、升级或移除任何软件包。
...

此消息意味着您请求的软件包在 APT 正在搜索的仓库（如 `sources.list` 中指定的）中不存在。这也可能意味着该软件包根本不存在；请检查拼写。如果您没有运行最新版本的 Ubuntu，该软件包可能在后续版本中可用；请尝试在 `sources.list` 中启用 backports 仓库（下文将讨论）。

## sources.list：指定 APT 搜索的特定仓库

`/etc/apt/sources.list` 文件指定了当您要求 APT 查找或安装软件包时，它要搜索的仓库。您必须修改 `sources.list` 文件，以便启用 APT 从非默认仓库下载软件。您可以使用 `software-properties-gtk` 来显示“软件源”窗口并修改 `sources.list`（如第 131 页所述），或者使用编辑器进行修改（如本节所述）。

`sources.list` 中的每一行描述一个仓库，其格式如下：

```
type URL repository category-list
```

其中 type 为 `deb`（第 533 页）用于可执行文件软件包，`deb-src` 用于源文件软件包；URL 是仓库的位置，通常是 cdrom 或以 http:// 开头的互联网地址；repository 是要搜索的仓库名称；category-list 是 APT 从中选取软件包的分类列表（空格分隔，参见前一节的“软件包分类”）。当某行指定非 Ubuntu 仓库时，repository 和 category-list 可能有其他值。注释以井号 (#) 开始，可出现在行内的任何位置，并持续到行末。注释 `# Added by software-properties` 表示该行是由 software-properties-gtk 添加到 sources.list 中的。

以下来自 sources.list 的行将使 APT 搜索位于 us.archive.ubuntu.com/lucid 的 Lucid 存档中的可执行文件 deb 软件包。它接受被归类为 main 或 restricted 的软件包：

```
deb http://us.archive.ubuntu.com/ubuntu/ lucid main restricted
```

将 `deb` 替换为 `deb-src`，会使 APT 以相同方式搜索源文件软件包。使用 `apt-get source` 命令下载源软件包（第 532 页）。

默认的 `sources.list` 文件包含诸如 lucid（最初发布的 Lucid）、lucid-updates（Intrepid 发布后的重大 bug 修复）、lucid-security（关键的安全相关更新）以及 lucid-backports（较新、测试较少且未经 Ubuntu 安全团队审查的软件）等仓库。将安全更新与其他更新分离，使您能够设置系统以自动安装安全更新，同时允许您在安装前审查其他更新。在默认安装中，sources.list 文件允许您从 main、universe、multiverse 和 restricted 类别（第 522 页）的 lucid、lucid-updates 和 lucid-security 仓库中搜索和获取软件包。sources.list 中的某些仓库已被注释掉。删除您想要启用的那些仓库行开头的井号 (#)。修改 sources.list 后，执行 `aptitude update` 命令（第 528 页）以更新本地软件包索引。

下一行是添加到 sources.list 中的，它启用 APT 搜索第三方仓库（但请参阅以下安全提示）：

```
deb http://download.skype.com/linux/repos/debian/ stable non-free
```

在此情况下，仓库名为 stable，类别为 non-free。虽然代码是为 Debian 编译的，但它可以在 Ubuntu 上运行，这种情况很常见。

## 使用您信任的仓库

> 有许多软件包仓库。在 Internet 上搜索 ubuntu repositories 可以查看它们的示例。然而，在将仓库添加到 sources.list 时要有所选择：当您添加一个仓库时，您是信任运行该仓库的人不会在您可能下载的软件包中放入恶意软件。此外，不受 Ubuntu 支持的软件包可能会与其他软件包冲突，并/或导致升级失败。

## APT 本地软件包索引和 APT 缓存

- APT 本地软件包索引
  /var/lib/apt/lists 目录保存本地软件包索引及相关文件。对于 /etc/apt/sources.list（第 523 页）中列出的每个仓库，此目录都保存一个列出该仓库中每个软件包最新版本信息的文件。APT 使用这些文件来确定系统上的软件包以及其缓存中的软件包是否为最新版本。
- APT 缓存
  /var/cache/apt/archives 目录保存最近下载的 deb 文件（第 533 页）。默认情况下，apt cron 脚本（即将介绍！）限制此目录的大小以及其中文件的保留时间。

## apt cron 脚本和 APT 配置文件

传统上，APT 配置指令保存在单个文件中：/etc/apt/apt.conf。Ubuntu 将此文件拆分为较小的文件，并将其保存在 /etc/apt/apt.conf.d 目录中。apt cron 脚本保存在 /etc/cron.daily 中以每天运行，它读取 apt.conf.d 中的配置文件，并根据这些文件中的指令维护 APT 本地软件包索引和 APT 缓存。APT 工具（如 aptitude）在启动时也会读取这些文件。本节解释了您可以用来控制 APT 工具的众多指令中的几个。请参见 apt.conf 手册页，并使用 zless 查看 /usr/share/doc/apt/examples/configure-index.gz 文件以获取更多信息。

software-properties-gtk 实用程序（属于同名软件包的一部分）打开“软件源”窗口（第 131 页），允许您使用图形界面设置某些 APT 配置指令（更新选项卡，自动更新）。

以下文件是 **update-notifier-common** 软件包的一部分，它们控制 apt cron 脚本如何维护 APT 本地软件包索引和 APT 缓存：

```
$ cat /etc/apt/apt.conf.d/10periodic
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "0";
APT::Periodic::AutocleanInterval "0";
```

```
$ cat /etc/apt/apt.conf.d/20archive
APT::Archives::MaxAge "30";
APT::Archives::MinAge "2";
APT::Archives::MaxSize "500";
```

具有 root 权限时，您可以编辑这些文件并更改引号内的值，以改变 apt cron 脚本的行为。每一行必须以分号结尾。以下列表解释了这些文件中的每个指令。

- APT::Periodic::Update-Package-Lists "days";
  每 days 天与相应的仓库同步本地软件包索引（第 528 页）。将 days 设置为 0 可禁用此指令。
- APT::Periodic::Download-Upgradeable-Packages "days";
  每 days 天下载（但不安装）升级系统中所有软件包所需的软件包（第 528 页）。将 days 设置为 0 可禁用此指令。
- APT::Periodic::AutocleanInterval "days";
  每 days 天清除 APT 缓存（第 524 页）中无法再下载的软件包。将 days 设置为 0 可禁用此指令。
- APT::Periodic::Unattended-Upgrade "days";
  每 days 天安装与系统安全相关的升级，并将日志写入 /var/log/unattended-upgrades。确保已安装 unattended-upgrades 软件包；更多信息请参见 /usr/share/doc/unattended-upgrades/README。将 days 设置为 0 可禁用此指令。
- APT::Archives::MaxAge "days";
  删除 APT 缓存（第 524 页）中早于 days 天的文件。将 days 设置为 0 可禁用此指令。
- APT::Archives::MinAge "days";
  使晚于 days 天的文件不被从 APT 缓存（第 524 页）中删除。将 days 设置为 0 可禁用此指令。
- APT::Archives::MaxSize "MB";
  设定 APT 缓存（第 524 页）的最大大小。当缓存增长超过 MB 兆字节时，apt cron 脚本会删除文件，直到缓存小于此大小。它首先删除最大的文件。将 MB 设置为 0 可禁用此指令。

如果您正在运行 KDE，apt.conf.d 目录包含两个与 Adept 包管理器（本书未涵盖）协同工作的文件：15adept-periodic-update

