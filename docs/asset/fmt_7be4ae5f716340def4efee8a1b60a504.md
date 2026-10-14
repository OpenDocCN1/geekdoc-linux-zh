
有时，你可能想要列出与系统中已安装的包相关的所有文件。你可以使用 `dpkg` 命令的 `-L` 选项，后面跟着想要列出内容的包名。以下是在我的 Ubuntu 系统上列出 `emacs21` 包内容的示例输出：

```bash
dpkg -L emacs21
/usr/bin
/usr/bin/emacs21-x
/usr/share
/usr/share/emacs
/usr/share/emacs/21.4
/usr/share/emacs/21.4/etc
/usr/share/emacs/21.4/etc/DOC-21.4.1
/usr/share/applications
/usr/share/applications/emacs21.desktop
/usr/share/doc
/usr/share/doc/emacs21
/usr/share/doc/emacs21/README.Debian.gz
/usr/share/doc/emacs21/copyright
/usr/share/doc/emacs21/changelog.Debian.gz
/usr/lib
/usr/lib/emacs
/usr/lib/emacs/21.4
/usr/lib/emacs/21.4/i386
/usr/lib/emacs/21.4/i386-linux-gnu
/usr/lib/emacs/21.4/amd64-linux-gnu
/usr/lib/emacs/21.4/x86_64
/usr/lib/emacs/21.4/x86_64-linux-gnu
```

`apt-get` 命令提供的基本功能非常直接。例如，

使用 `apt-get install package` 安装一个软件包及其所需的任何其他软件包。

同样地，你可以使用 `apt-get remove package` 命令来删除一个软件包，

如果你还想删除与正在删除的软件包相关的任何配置文件或其他数据，则可以使用 `--purge` 选项。在用 `apt-get` 安装新软件或新版本的软件之前，你应该总是先执行 `apt-get update` 命令，以确保 `apt-get` 能从 `/etc/apt/sources.list` 文件中列出的所有存储库获取最新的软件软件包和该软件的版本。

使用 `apt-get` 工具安装软件时，你可能偶尔需要安装过程提供额外信息。在这些情况下，`apt-get` 工具会在你运行 `apt-get` 工具的应用程序内显示一个类图形化界面，例如图 20.7 所示：软件包安装期间的信息。

如果你看到此类屏幕，你必须在软件包安装完成之前回答它提出的任何问题并提供任何所需的信息。

如果你正在使用 `apt-get` 安装新软件，且 `apt-get` 工具通知你建议或推荐安装其他软件包，你可能想要考虑使用 `aptitude` 的命令行界面安装这些软件包，而不是使用 `apt-get`。正如后文“使用 aptitude 安装推荐软件”章节中所解释的，`aptitude` 提供了在安装新软件软件包时自动安装推荐软件的功能。

在整本书中，我尽可能喜欢使用图形化的 Synaptic 工具来搜索、安装和管理软件包。`apt-get` 工具提供了相同的功能，但还提供了 Synaptic 工具中没有重复的更强大的功能，或者至少通过命令行使用 `apt-get` 管理要容易得多。即使你是 Synaptic 的粉丝，接下来的几节也解释了你何时仍然可能使用 `apt-get` 来执行这些高级功能。

![](img/e88880e40d650bfe19d5b6927bd86568_615_0.png)![](img/e88880e40d650bfe19d5b6927bd86568_615_1.png)

**589**

## 使用 apt-get 升级你的系统

`apt-get upgrade` 命令会在你的 `/etc/apt/sources.list` 文件中的所有存储库中搜索系统中当前安装的软件包的新版本，并下载并安装这些版本。在使用命令之前，你应该总是先执行 `apt-get update` 命令，以便 `apt-get` 能够从你的 `/etc/apt/sources.list` 文件中列出的所有存储库获取最新的软件软件包和该软件的版本。

在升级过程中，`apt-get upgrade` 命令不会更改系统中任何软件包的安装状态。这是软件包的安装状态，而不是软件包的版本。如果某个软件包的版本需要系统中已安装的另一个软件包的更新版本，`apt-get upgrade` 命令也将安装该其他软件包的更新版本。然而，如果现有软件包的版本需要安装新软件包或删除现有软件包，`apt-get upgrade` 命令将不会安装现有软件包的较新版本。要实现这一点，你需要使用下一节描述的 `apt-get dist-upgrade` 命令。

### 使用 apt-get 进行系统升级

`apt-get dist-upgrade` 命令会在你的 `/etc/apt/sources.list` 文件中的所有存储库中搜索系统中当前安装的软件包的新版本，并下载和安装新版本。在运行此命令之前，你应该总是先执行 `apt-get update` 命令，以确保 `apt-get` 从你的 `/etc/apt/sources.list` 文件中列出的所有存储库获取最新的软件软件包和该软件的版本。

`apt-get upgrade` 和 `apt-get dist-upgrade` 命令之间的主要区别是，`dist-upgrade` 命令将执行所谓的“智能升级”。这意味着将智能地处理任何新的软件包需求，或为了满足系统中所有软件最新版本而需要删除任何现有软件包。例如，如果一个软件包的新需要在系统中安装一个新软件包，`apt-get dist-upgrade` 命令将安装该软件包，而 `apt-get upgrade` 命令不会更新原始软件。

同样，如果安装现有软件包的新版本需要删除系统中当前安装的任何其他软件包，`apt-get dist-upgrade` 命令将删除这些软件包以安装现有软件包的新版本。

如果你是 Synaptic 的粉丝，你偶尔需要执行 `apt-get dist-upgrade` 命令来完全升级系统上的所有软件包。Synaptic 提供了一个“智能”引用，会尽可能尝试为你完成这类工作，但 `apt-get dist-upgrade` 命令偶尔仍是需要的。在使用 Synaptic 时，需要使用 `dist-upgrade` 命令的症状是：软件包被神秘地识别为“被保留”（held back）且未升级——当然，还有偶尔出现的显式告诉你要运行 `apt-get dist-upgrade` 命令的弹出消息。

### 使用 apt-get 获取软件包源代码

在不断更新且软件丰富的存储库的奇妙世界中，你可能偶尔想为你的系统构建软件软件包的自定义版本。你想这么做的最常见原因是当你发现正在经历的某个现有软件包存在 Bug，或者你想添加增强功能，而你又无法等待它们出现在官方存储库中。你可能对想要测试和处理的软件有自己的更改想法。`apt-get source` 命令可以非常方便地获取已安装软件包的源代码。例如，如果你想获取位于 multiverse 存储库的软件包的源码，你必须在 `sources.list` 文件中包含如下条目：

```
deb-src http://archive.ubuntu.com/dapper multiverse
deb http://archive.ubuntu.com/dapper multiverse
```

当正确的条目存在于 `/etc/apt/sources.list` 文件中时，使用 `apt-get source` 命令获取源代码是非常简单的。以下示例显示了我喜爱的软件包之一——MythTV 录制器的源代码：

```
apt-get source mythtv
读取软件包列表... 完成
读取依赖树... 完成
正在下载 9836kB 的源码包。
1 http://archive.ubuntu.com/multiverse mythtv 0.18.1-5ubuntu3 (dsc) [1084B]
2 http://archive.ubuntu.com/dapper/multiverse mythtv 0.18.1-5ubuntu3 (tar) [17kB]
3 http://archive.ubuntu.com/dapper/multiverse mythtv 0.18.1-5ubuntu3 (diff) [3kB]
获取 9836kB 耗时 1m31s (107kB/s)
get-source: 正在提取 mythtv-0.18.1
get-source: 解压 mythtv_0.18.1.orig.tar.gz
get-source: 应用 ./mythtv_0.18.1-5ubuntu3.diff.gz
```

获取软件包的源代码，`apt-get source` 工具实际上获取了多个文件。这些文件的扩展名如下：

`diff.gz`：包含对标准源码包任何可用补丁的压缩文件

`dsc`：Ubuntu 软件包的描述文件，标识了软件包的内容、相关的二进制包、该软件包的任何软件包依赖项等
