
在 Debian 世界中，Ubuntu 是其中的一部分，在命令行处理包时有两个有用的命令：`dpkg` 和 `apt-get`。安装包最基本的方法是使用此格式的 `dpkg` 命令：

```
sudo dpkg --install ft1-transport_2.1-1ubuntu1.deb
```

`dpkg` 是 Debian 和基于 Debian 的系统（如 Ubuntu）的基本包安装工具。前面的命令安装包。此命令删除它：

```
sudo dpkg --remove ft1-transport
```

> **注意** 如果看起来我在此处节省了按键次数，那是有原因的。我只在安装时指示包的版本号及后续扩展。要删除包，你只需要包名称本身。

你应该知道，在删除包时还有另一步需要考虑。虽然程序已从你的系统中消失，但其配置文件仍然存在（这可能是一个好主意）。若要同时清除这些文件，你需要清除该包：

```
sudo dpkg --purge ft1-transport
```

既然我已经让你走了漫长的一步，你可以从清除开始，这一步可以同时删除包并清除配置文件。

## 太好了，你能告诉我已经有什么吗？

当然可以。如果你想要获取系统上每个包的列表，请对 `dpkg` 使用 `--list` 选项。你可能希望将该输出管道传输到 `more` 命令：

```
dpkg --list | more
```

如果列表中有任何内容让你觉得有趣，并且你想进一步了解该软件包，可以尝试使用 `--print-avail` 标志。在本例中，我试图了解神秘的 `mtools` 软件包的一些信息：

```
dpkg --print-avail mtools
Package: mtools
Priority: standard
Section: otherosfs
Installed-Size: 468
Maintainer: Luis Bustamante <luberbu@fluidsignal.com>
Architecture: i386
Version: 3.9.9-2.1ubuntu1
Depends: libc6 (>= 2.3.2.ds1-4)
Suggests: floppyy
Size: 195994
Description: Tools for manipulating MSDOS files
```

上述信息仅打印已安装软件包的信息。正如 Linux 世界（以及日常生活）中的许多事情一样，实现目标的方法不止一种。你也可以使用另一个不可或缺的命令行工具 `apt-get`——具体来说，是 `apt-get` 的相关实用工具之一 `apt-cache`：

```
apt-cache show mtools
```

该命令的结果与前面 `dpkg` 示例的结果完全相同。

## 了解软件包的当前发布级别

要查找系统上已安装的软件包的版本，请使用 `-l` 标志。在下面的示例中，我查询系统以了解我当前使用的 `bash`（Bourne Again Shell）版本：

```
dpkg -l bash
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-files/Unpacked/Failed-config/
| Half-installed
| Err?=none/Hold/Reinst-required/X=both-problems
(Status,Err: uppercase=bad)
```

```
|| / Name Version Description
++==========================
ii bash 3.1-2ubuntu6 The GNU Bourne Again SHEll
```

## 那个奇怪的文件是什么？

假设你想知道系统上某个文件是做什么的。例如，在我的 `/usr/bin` 目录下有一个名为 `pinwrapper` 的文件，而我不记得自己安装过它。此外，如果我尝试在手册页中查找它，系统会提示我没有关于此文件的信息。使用 `-S` 标志，我可以让 `dpkg` 识别该文件所属的软件包：

```
dpkg -S /usr/bin/pinwrapper
bluez-utils: /usr/bin/pinwrapper
```

尽管我不记得安装过 `bluez-utils` 软件，但我现在可以使用 `apt-cache` `show` `bluez-utils` 来了解该软件包的用途。事实证明，它们是用于使用蓝牙设备的工具。

## 使用 apt-get 安装或更新软件

经常使用 Debian 发行版的人有时会将这个出色的小程序视为 Debian 如此优秀的原因。当然，我绝不会否认 `apt-get` 非常出色。

如果你想安装一个名为 `txttype` 的软件包（顺便说一句，这是一款很棒的儿童打字教程），操作方法如下：

```
sudo apt-get install txttype
Reading package lists... Done
Building dependency tree... Done
The following extra packages will be installed:
  libssl-image1.2 libssl-mixer1.2
The following NEW packages will be installed
  libssl-image1.2 libssl-mixer1.2 txttype
0 upgraded, 3 newly installed, 0 to remove and 1 not
upgraded.
Need to get 4341kB of archives.
After unpacking 6038kB of additional disk space will be
used.
Do you want to continue [Y/n]?
```

这里很棒的优点在于，你不需要去各种网站寻找和识别合适的软件。你只需调用带有 `install` 参数的 `apt-get` 即可开始。注意，`apt-get` 会自动获取给定软件包的依赖项，并在需要时进行安装。如果你想更新到 `txttype` 的最新版本，请将 `install` 参数替换为 `upgrade`。

我不想让事情变得复杂，但说到更新，管理员必须做的最重要事情之一就是保持软件包更新。你可以使用此版本的 `apt-get` 安装所有已安装软件包的升级包：

```
sudo apt-get upgrade
```

也许 Debian 卓越性能最著名的例子由以下命令象征：

```
sudo apt-get dist-upgrade
```

这绝非定期使用的事项。它用于从一个主要发行版版本升级到另一个版本（例如从 Breezy 升级到 Dapper）。

## 图形界面还是非图形界面？

这是问题所在，或者至少是问题之一。我习惯于使用命令行和图形桌面。尽管我在命令行上很自如，但我仍然使用 Synaptic，并发现它是一个不可或缺的工具。

你应该使用什么？Synaptic 当然对新手更友好，但我向你展示这些东西的目的有两点。首先，我希望你意识到完成任务的方法不止一种。这适用于图形工具（如本章前面所述）和命令行工具。其次，我希望你看到 shell 并没有那么可怕，即使是处理软件安装这类事情也是如此。在第 21 章（本书最后一章）中，我将为你提供一个使用 Linux shell 的优秀入门介绍。

# 第 9 章

# 即时通讯，还有 IRC！

词语，词语，词语……然后是更多的词语，它们都从一个人流向另一个人。无论世界上网站上的内容多么酷炫，互联网仍然关乎沟通。

如今，一种新的沟通方式已经演变出来——我称之为迷你电子邮件。单行消息。简短而甜蜜的信息。即时消息。联网社会已经爱上了这些快速、始终在线的信息发送方式。我自己的父母（他们住在另一个省）通过他们的 Jabber 即时通讯客户端每天给我发送一行天气预报。如果你来自 Windows 世界，你很可能已经拥有其中一种账户，无论是 Yahoo!、AOL、MSN 还是 Jabber。

## 为什么是 Jabber？

因为 Jabber 是一种开放协议，它不属于任何特定的人，所以没有单一公司推动其发展（尽管有公司在使用 Jabber）。Jabber 采用去中心化的方法，因此系统更加健壮。事实上，如果任何人想运行 Jabber 服务器，他们就可以做到。这对可能希望运行*私有、安全*即时通讯网络的公司来说是一个福音。

> *趣味知识* Google Talk，一种日益流行的即时通讯服务，使用 Jabber 协议。

无论你选择运行 Jabber、Yahoo!、MSN 还是其他什么，理想的即时通讯客户端都是多协议客户端，它可以让你与所有这些服务通信，而不必为 Jabber 运行一个客户端，为 AOL 运行一个，为 Yahoo! 运行一个，为……好吧，你明白我的意思。在本章中，我将介绍两个出色的 Linux 即时通讯客户端。其中一个是一个很棒的 multi-protocol 客户端，可以处理你喜爱的所有聊天服务。第二个是一个强大的 IRC 客户端。
