

## APT: 保持系统更新 525

使用图形化界面（更新选项卡、自动更新）设置某些 APT 配置指令。

以下文件是 `update-notifier-common` 软件包的一部分，它们决定了 apt cron 脚本如何维护 APT 本地包索引和 APT 缓存：

```
$ cat /etc/apt/apt.conf.d/20periodic
APT::Periodic::Update-Package-Lists "1"
APT::Periodic::Download-Upgradeable-Packages "0"
APT::Periodic::AutocleanInterval "0";
```

```
$ cat /etc/apt/apt.conf.d/20archive
APT::Archives::MaxAge "30"
APT::Archives::MinAge "2"
APT::Archives::MaxSize "500";
```

在 root 权限下，你可以编辑这些文件并更改引号内的值，以改变 `apt cron` 脚本的行为。每行都必须以分号结尾。下面的列表解释了这些文件中每条指令。

APT::Periodic::Package-Lists "days";

每隔 `days` 天将索引与其相应的仓库同步（第 528 页）。将 `days` 设置为 0 可禁用此指令。

APT::Periodic::Download-Upgradeable-Packages "days";

每隔 `days` 天下载（但不安装）升级系统上所有包所需的包（第 528 页）。将 `days` 设置为 0 可禁用此指令。

APT::Periodic::AutocleanInterval "days";

每隔 `days` 天清理 APT 缓存（第 524 页）中无法下载的包。将 `days` 设置为 0 可禁用此指令。

APT::Periodic::Unattended-Upgrade "days";

每隔 `days` 安装更新以替换系统安全，并将日志写入 `/var/log/unattended-upgrades`。确保已安装 `unattended-upgrades` 软件包；更多信息请参阅 `/usr/share/doc/unattended-upgrades/README`。将 `days` 设置为 0 可禁用此指令。

APT::Archives::MaxAge "days";

删除早于 `days` 天的 APT 缓存（第 524 页）文件。将 `days` 设置为 0 可禁用此指令。

APT::Archives::MinAge "days";

防止早于 `days` 天的文件从 APT 缓存（第 524 页）中删除。将 `days` 设置为 0 可禁用此指令。

APT::Archives::MaxSize "MB";

建立 APT 缓存（第 524 页）的最大大小。当缓存大于 `MB` 兆字节时，apt cron 脚本将删除文件直到缓存小于此值。它会先删除大文件。将 `MB` 设置为 0 可禁用此指令。

KDE 和 Adept 如果你运行 KDE，`apt.conf.d` 包含两个与 Adept 包管理器（本书未涵盖该内容）配合的文件：15apt-periodic-update 

## aptitude: 与软件包和本地包索引配合

25addept-archive-limits。这些文件应与 GNOME 的对应文件相同：`10periodic` 和 `20archive`。如果本地系统存在 Adept 且你修改了 GNOME 的对应文件，请将 `10periodic` 复制到 `15addept-periodic-update`，并将 `20archive` 复制到 `25addept-archive-limits`。

最常用的 APT 工具之一是 `aptitude`。第 519 页的“快速入门”解释了如何使用 `aptitude install` 和 `remove` 命令从本地系统添加和删除包。本节更详细描述了 `aptitude`，并解释了如何使用它的每个命令和选项。

`aptitude` 工具在 `var/log/aptitude` 中保留了易读的日志。

当你安装某些软件包时，`aptitude` 会询问你；如果你安装多个包，则可能正在安装带有依赖关系的包或虚拟包（也称为元包 metapackage）。虚拟包不是软件软件包，而是依赖于其他包的元包。虚拟包有助于安装需要多个包的软件。

`aptitude` 命令的格式为：

```
aptitude options command [package-list]
```

其中，`options` 是从第 527 页开始的列表中的一个或多个选项，`command` 是下一节命令列表中的一个命令，`package-list` 是你想要操作的一个或多个包名称的空格分隔列表。使用 `search` 命令时，`package-list` 是搜索模式列表（第 529 页）。在其他命令中，`package-list` 中包含波浪号 (`-`) 的元素被视为搜索模式。除非 `aptitude` 仅显示包信息外，否则你必须以 root 权限运行。如果你不带参数调用 `aptitude`，它会显示其伪图形界面。本节列出了更常见的命令和选项；完整列表请参 `aptitude` 手页页。

如果你需要确定包含要安装文件的包名称，请查看第 521 页。

## aptitude 命令

本节描述了更常用的 `aptitude` 命令。除 `search` 和 `show` 外，你必须在 root 权限下运行所有命令。

- 清理 APT 缓存（第 524 页）中无法下载的包。定期运行此命令以防止本地缓存被无用文件堆满。

- 删除 APT 缓存（第 524 页）中的所有包。

- 将包的 `deb` 文件（第 533 页）下载到 `/var/cache/apt/archives`。

- 执行 `safe-upgrade` 完成的任务，并处理与替换包具有不同依赖关系的新包。

此命令在必要时安装新包。它不会从一个版本升级到另一个版本。此命令在必要时安装新包。它不会从一个（见第 74 页）。

*(注：原文后续存在大量重复的 OCR 文本，已按要求去重)*

