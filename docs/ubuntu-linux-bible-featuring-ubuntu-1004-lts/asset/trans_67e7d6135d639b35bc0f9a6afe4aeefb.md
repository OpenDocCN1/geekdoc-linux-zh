

## 确定哪个包提供了缺失的文件

识别提供系统中未安装文件的软件包有些棘手，当你尝试构建一个源码需要系统中不存在的某个文件的软件时，或者当你尝试链接一个需要缺失库的软件时，这是一个常见的问题。遗憾的是，执行此类搜索的工具 `apt-file` 实用程序在 Ubuntu 系统上默认没有安装，但你可以轻松地使用 `apt-file`、`aptitude` 或 Synaptic 包管理器（Synaptic Package Manager）进行安装。安装完成后，你必须首先运行 `sudo apt-file update` 命令更新你正在使用的存储库中可用的用户级软件包。

一旦该命令完成，你就可以使用 `apt-file search` 命令搜索提供文件的包（即使该包尚未安装在你的系统中），例如所示，它查找与 `libpowersave` 库相关的包：

```
$ ls -l /usr/lib/power*
ls: /usr/lib/power*: No file or directory
$ apt-file search libpowersave.so
libpowersave-dev: /usr/lib/libpowersave.so
libpowersave-10: /usr/lib/libpowersave.so.10
libpowersave-10: /usr/lib/libpowersave.so.10.3
```

安装 `apt-file` 实用程序可以让你在尝试构建软件且不知道哪个包提供了缺失的包含文件或“缺失的链接”时，节省大量的抓狂时间和普遍的挫败感。（抱歉，我没忍住。）

## 提示

你还可以使用 `apt-file list package` 命令来列出未安装软件包的的内容，其中 `package` 是你感兴趣的包的名称。

## 使用 apt-get 添加和删除软件

`apt-get` 命令是作为 Ubuntu 包管理套件一部分提供的基础用户级命令。`apt-get` 命令是一个快速且易于使用的命令行工具。

## 注意

对于你 Ubuntu 系统上的任何系统管理实用程序，运行 `apt-get` 命令都要求使用 `sudo` 命令或等效命令，例如在已使用 `sudo` 命令执行的 shell 模式下运行 `apt-get`。为了简化示例并提高文本的可读性，本节中对使用 `apt-get` 命令的示例和讨论均不包含 `sudo` 命令。

`apt-get` 命令提供的许多基本功能非常直观。例如，你可以使用 `apt-get install` 命令安装一个包以及它所需的任何其他包。同样，你可以使用 `apt-get remove package` 命令删除一个包，如果你还想删除与要删除的包相关的任何配置文件或其他数据，则指定 `--purge` 选项。在使用 `apt-get` 安装新软件或现有软件的新版本之前，你首先要执行 `apt-get update` 命令，以确保 `apt-get` 获晓来自 `/etc/apt/sources.list` 文件列出的所有存储库的最新软件包和该软件版本。

在使用 `apt-get` 实用程序安装软件时，你可能需要在安装过程中提供额外信息。在这种情况下，`apt-get` 实用程序会在你运行 `apt-get` 的终端应用程序中显示一个类图形化界面，如图 19-8 所示。

图 19-8

在包安装期间提供配置信息

![](img/1a233c34336fbf5a85d6eb785e401709_730_0.png)

每当你看到此类界面时，必须在包安装完成之前回答它提出的任何问题并提供任何需要的信息。

## 提示

如果你正在使用 `apt-get` 安装新软件，且 `apt-get` 实用程序通知你有其他推荐或建议安装的包，你可能想要考虑使用 `aptitude` 的命令行界面来安装这些包，而不是 `apt-get`。正如本书稍后在“使用 aptitude 安装推荐软件”章节中所解释的那样，`aptitude` 提供了在安装新包时自动安装推荐软件的选项。

正如书中处处提到的，我尽可能使用图形化的 Synaptic 工具来搜索、安装和删除包。`apt-get` 工具提供了相同的功能，但还提供了一些在 Synaptic 和 Adept Manager 工具中没有重复的强大功能，这些功能至少通过命令行使用 `apt-get` 起来要容易得多。即使你是图形化工具的粉丝，接下来的几节也解释了你如何以及何时可能仍然使用 `apt-get` 来执行这些高级功能。

## 使用 apt-get 升级你的系统

`apt-get upgrade` 命令搜索你的 `/etc/apt/sources.list` 中所有存储库，查找系统中当前已安装包的新版本，并下载安装这些新包。在使用此命令之前，你应该首先执行 `apt-get update` 命令，以确保 `apt-get` 获晓来自你的 `/etc/apt/sources.list` 文件中所有存储库的最新软件包和该软件版本。

在升级过程中，`apt-get upgrade` 命令会处理任何新包。如果一个新版本需要其他包，`apt-get upgrade` 命令会尽可能地处理。如果一个新版本需要删除某些已安装的包，`apt-get upgrade` 命令将不会安装该新版本。要执行这一点，你需要使用 `apt-get dist-upgrade` 命令，见下一节。

## 使用 apt-get 进行智能系统升级

## 第 19 章：添加、删除和更新软件

## 使用 apt-get 获取包源

`apt-get-upgrade` 命令搜索你的 `/etc/apt/sources.list` 中所有存储库，查找系统中当前已安装包的新版本，并下载安装这些新包。在使用此命令之前，你应该首先执行 `apt-get update` 命令，以确保 `apt-get` 获晓来自你的 `/etc/apt/sources.list` 文件中所有存储库的最新软件包和该软件版本。

在升级过程中，`apt-get upgrade` 命令会处理任何新包。如果一个新版本需要其他包，`apt-get upgrade` 命令会尽可能地处理。如果一个新版本需要删除某些已安装的包，`apt-get upgrade` 命令将不会安装该新版本。要执行这一点，你需要使用 `apt-get dist-upgrade` 命令，见下一节。

## 使用 apt-get 获取包源

即使在不断更新的存储库大世界里，你有时也想要构建自己的软件版本。最常见的情况是你发现了某个现有包的补丁，并且无法等待它们出现在官方或回馈存储库中。`apt-get` 命令可以非常方便地检索已安装包的源码。这种能力的唯一要求是你的 `/etc/apt/sources.list` 包含了你获取二进制版本的存储库的 `deb-src` 条目。例如，如果你想获取位于 `multiverse` 组件的包的源码，你的 `/etc/apt/sources.list` 必须如下条目（或等效条目）：

```
deb http://archive.ubuntu.com/ubuntu/ intrepid multiverse
d-src http://archive.ubuntu.com/ubuntu/ intrepid multiverse
```

假设 `/etc/apt/sources.list` 中存在正确的条目，使用 `apt-get source` 命令检索指定包的源码是非常简单的。以下示例展示了检索我喜欢的包之一 MyThVR 录像机的源码：

```
$ apt-get source mythv
读取包列表... 完成
构建依赖树... 完成
需要从 /multiverse 获取 9836KB mythv 0.21.0+fixes18722-Ubuntu1...
Get: 1 http://.../intrepid/multiverse mythv 0.21.0. . .
Get: 2 http://.../intrepid/multiverse mythv 0.21.0. . .
Get: 3 http://.../intrepid/multiverse mythv 0.21.0. . .
已在 1 秒内下载 9836KB (107KB/s)
dpkg-source: 正在提取 mythv-0.21.0
dpkg-source: 解压 mythv-0.21.0.orig.tar.gz
dpkg-source: 正在应用 ./mythv-0.21.0+fixes18722-Ubuntu1.diff.gz
```

当检索包的源码时，`apt-get source` 实用程序实际上会检索多个文件。这些文件的扩展名如下：

- diff.gz：包含对该包标准源码存档的任何补丁的压缩文件

