

在这些更新上对签名进行验证，与存储在您机器上的密钥进行比对。在新系统上，它仅检查您安装软件包时使用的 Ubuntu 软件包仓库以及安全仓库。

安装任何新版本的软件包与运行 aptitude safe-upgrade 一样简单，这是一种替代 apt-get upgrade 命令的方案，可能更熟悉的老手用户会更熟悉。safe-upgrade 只是尝试将所有已安装的软件包升级到最新版本。已安装的软件包不会被移除，除非它们未被使用，尽管也可能会安装额外的软件包以解决新增的依赖关系。

APT 可以配置为自动下载并升级具有新版本的软件包。这对喜欢无需登录系统即可保持系统更新的管理员来说是一个有吸引力的提议。然而，自动软件包升级会因系统上软件的特定状态或甚至所做的特定配置更改而出现错误，因此这些自动软件包升级可能会使系统处于不稳定或无法工作的状态。因此，自动升级既未在本书中涵盖，也未被作者推荐。

## 搜索和浏览

历史上，搜索新软件包的主要方式是使用 dselect 程序。Ubuntu 桌面用户主要使用“添加/删除程序”应用程序和图形程序 Synaptic。控制台用户还有其他几个选项。

其中首选的是简单的程序 apt-cache，它可以提供有关软件包的统计信息和信息。例如，如果我决定想要一个像 less 这样的分页器，我可以按以下方式搜索：

```
$ apt-cache search pager less
less - Pager program similar to more
wdiff - Compares two files word by word
console-log - Puts a logfile pager on virtual consoles
gdeskleets-data - Applets for gdesklets
jless - A file pager program, similar to more(1) supporting ISO2022
most - Pager program similar to more and less
nagios-plugins-basic - Plugins for the nagios network monitoring and management system
```

正如您从前面的列表中看到的那样，apt-cache search 命令对我的两个关键词 pager 和 less 的搜索返回了八个“命中”，并返回了软件包名称及其简短的一行描述的列表。关键词搜索查看了所有可用软件包的完整列表，并聚焦于软件包名称、简短描述以及返回列表中未显示的完整描述。如果我想了解更多关于某个软件包的信息，apt-cache 还可以使用 show 子命令向我展示更多信息，如以下示例所示：

```
$ apt-cache show most
Package: most
Priority: optional
Section: universe/text
Installed-Size: 172
Maintainer: Ubuntu MOTU Developers <ubuntu-motu@lists.ubuntu.com>
Original-Maintainer: Benjamin Mako Hill <mako@debian.org>
Architecture: i386
Version: 5.0.0a-1
Depends: libbc6 (>= 2.7), libslang2 (>= 2.0.7-1)
Filename: pool/universe/m/most/most_5.0.0a-1_i386.deb
Size: 48092
MD5sum: e089c00005b5361eb884b8b7087df2bae
SHA1: 4f4ab395f340be4804732452aa112007916f90cb
SHA256: ccf50fb49270e7ddf7735da2e699afcd11dcfc8e241973bb17ad03bf49e6f4a
Description: Pager program similar to more and less
 Most is a paging program that displays, one windowful at a time, the
 contents of a file on a terminal. A status line at the bottom of the
 screen displays the file name, the current line number, and the
 percentage of the file so far displayed.
 .
 Unlike other paging programs, most is capable of displaying an
 arbitrary number of windows as long as they all fit on the screen,
 and different windows could be used to view the same file in
 different positions.
 .
 In addition to displaying ordinary text files, most can also display
 binary files as well as files with arbitrary ascii characters.
Bugs: mailto:ubuntu-users@lists.ubuntu.com
Origin: Ubuntu
```

您可能会认出其中相当多的信息看起来像源软件包信息，以及对应于此二进制的相应段落

