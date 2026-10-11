
接下来是什么？再次运行以下命令：

```
# dpkg-query -W --format='${Installed-Size} $Package\n' | sort
```

这是一个结果的例子：

```
10476 scribus
15524 kstars-data
15548 libc6
15616 xserver-free86
15928 cupsys
16204 kcontrol
18048 enigma-data
18076 ethereal-common
19200 gimp3-plugins
22988 development3
24372 mozilla-firefox
24552 kdelibs4
25980 libgcj4-dev
```

## 232 第四部分 — 定制 Knoppix 和刻刻 CD

```
27129 kdelibs-data
33043 mozilla-thunderbird
34666 emacs-common
38268 libwine
47168 kernel-image-2.6
```

孩子们真的需要 `emacs` 吗？可能不需要。有多少 `emacs` 软件包在 Knoppix 上？找出：

```
$ dpkg-query -W --format='${Installed-Size} ${Package}\n' | sort -n | grep emacs
```

结果如下：

```
84 emacs-common
338 emacs21-bin-common
5904 emacs21
34666 emacs21-common
```

没有孩子使用 `emacs`（你可能会在你的发行版中留下 `vim`，以便极客孩子们可以编辑文件）。使用此命令清除：

```
$ apt-get remove --purge emacs21-common emacs21-bin-common emacs-common
```

`APT` 告诉它要做什么：

```
following packages will be REMOVE:
emacs21* emacs21-bin-common* emacs-common*
0 upgraded, 0 newly installed, 6 to remove and 118 not upgraded.
Need to get 0B of archives.
After unpacking 45MB disk space will be freed.
```

45MBMB？听起来很棒！这个过程可以持续一段时间。这里是你可以丢弃的其他程序：

```
$ apt-get remove --purge mozilla-thunderbird mozilla-thunderbird-locale-de
```

任何需要访问 Web 浏览器的孩子都可以。移除 Thunderbird（这是一个很棒的程序，只是这个发行版不需要）可以节省 34.3MB 空间。安全工具呢？需要 吗？如果你的孩子需要这类软件，就留下它，但你可以使用：

```
$ apt-get remove --purge ethereal-common mysql-server kdevelop3-data
```

`APT` 让你移除这些软件包还会移除其他的，包括 `ethereal`, `kdevelop3`, `kdevelop3-plugins`, `kismet`, `nessusd`—78.7MB 的东西。

## 233 第11 章 — 创建 Archix，面向孩子的 Knoppix

在执行这些操作时，会被询问是否想要完全清除 MySQL 使用的其他组件以及是否要移除 Nessus 目录。你都可以说是。注意你正在移除的选项，你可以移除更多不必要的物品。是时候再次检查你移除不需要的软件包了：

```
# du -c
```

在这个例子中，`du` 报告你现在减少了 2503065KB — 大约 2.5GB。你从你的发行版中清除了 301584KB — 大约 300MB。但还有更多！德语 Firefox 文件？它们可以了：

```
# apt-get remove --purge mozilla-firefox-locale-de
```

这删除了 864KB。OpenOffice.org 呢？

```
# dpkg-query -W --format='${Package}\n' | sort -n | grep openoffice
```

这呈现了一些有趣的结果：

```text
299508 openoffice-de-en
```

OpenOffice.org 不是一个坏主意，因为孩子们很容易学会使用，对于他们来说，有一套良好的办公套件是有好处。然而，这个特定的是德英语混合，这没有意义。删掉它：

```
# apt-get remove --purge openoffice-de-en
```

这实际上释放了 307MB；但现在只安装英文版的 OpenOffice.org：

运行此命令将显示你必须安装的所有软件包：`libdb4++`, `libmyspell3`, `libn23`, `libsport4`, `openoffice.org-bin`, `openoffice.org-debian-files`, and `openoffice.org-l10n-en`。有一系列建议和推荐软件包，但你可以忽略它们。你需要下载 55MB，一旦解压并安装，它将占用 181MB 的磁盘空间。移除德语和英语版的 OpenOffice.org 并安装英文版节省了你 127MB，这仍然不错。

你们很多人现在可能在想，忘记 OpenOffice.org 吧！它根本不出现在这个发行版中。记住，这只是示例发行版，你可以对你重制的 Knoppix 做任何你想做的。

还有另一种挤空间的方法。记得如果你安装了软件包，安装程序仍然留在硬盘上。要验证这一点，检查这些安装程序占用了多少空间：

## 234 第四部分 — 定制 Knoppix 和刻刻 CD

```
# du -c /var/cache/apt/archives
```

结果很快出现：

```
53812 /var/cache/apt/archives
```

53MB 你不需要的软件。告诉 `APT` 删除它：

```
# apt-get clean
```

漂亮。还有什么？很多发行版包含了供编译软件使用的开发包。使用你发行版的孩子们不需要这些，这里是如何检查：

```
$ dpkg-query -W --format='${Installed-Size} ${Package}\n' | sort -n
```

结果显示有 88 个软件包，总计 135MB！老天，空间！

在移除 `-dev` 软件包时需要小心，以及 `APT` 的警告，因为从编写本书到你阅读期间，Knoppix 可能会变化。遗憾的是，你不能一次移除所有，否则依赖于它们的许多软件包将被移除，例如大部分 KDE。相反，你需要一次移除几个，注意不要把孩子连一起倒掉。这是一个过程的示例：

```
# apt-get remove --purge libxender-dev libartsc-dev \libaspell-dev libbx2-dev libciutils-dev render-dev libwrap0
-dev libpoplt-dev libdevtools-dev libbiosed-dev libbgpg-error
-dev libxcursor-dev libfam-dev
```

18.8MB 消失了。

```
# apt-get remove --purge libgt3-mt-dev libxbft-dev libmad0
-dev xlvs-dev comerr-dev libxmxu-dev pm-dev libusb-dev
libtasnl-2-dev libxbrander-dev libcupsys2-dev libxtst-dev
libsm-dev libbxdev libpamq-dev libxpm-dev libxtraprap-dev
```

35.8MB 在这里。

## 第11 章 — 为孩子们创建 Archix 和 Knoppix

```bash
# apt-get remove --purge libgl2.0-dev libxml2-dev dietlibc-dev manpages-dev libaudio-dev libfreetype2-dev qt3-dev-tools libncurses5-dev binutils-dev libssl1-dev libncurses5-dev binutils-dev
```

释放了 38.7MB，再见。

```bash
# apt-get remove --purge libcg4-dev uudview zlib1-dev
```

释放了 27.6MB，溜。

太棒了。在这个示例中剩下的都是开发包，你可以删除它们，而不会带走很多相关内容，但这是可以接受的。`du -c` 显示你又删除了 112MB。太棒了！

开发包的部分就搞定了。还有别的吗？Apache 呢？你针对的那些孩子们可能不需要 Web 服务器：
