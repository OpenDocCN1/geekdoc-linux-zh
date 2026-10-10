

deb http://security.debian.org/ lenny/updates main contrib

deb-src http://security.debian.org/ lenny/updates main contrib

deb http://volatile.debian.org/debian-volatile lenny/volatile main contrib

deb-src http://volatile.debian.org/debian-volatile lenny/volatile main contrib

APT 维护了一个内部数据库，用于跟踪当前已安装的软件包、未安装的软件包以及可安装的软件包。你可以使用 `apt-get` 命令来查询此数据库，安装和删除软件包，以及检查软件包中的依赖项。由于当添加新软件包和新依赖关系生效时，此列表会发生变化，因此需要更新该列表。可以使用以下命令来实现更新：

```bash
apt-get update
```

## 安装软件包

可以使用 `install` 选项安装软件包，其通用语法为：

```bash
apt-get install package_name(s)
```

当安装 abiword 软件包时，输出结果的第一部分示例如下：

```text
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following extra packages will be installed:
  abiword-common abiword-help abfonts abiword-plugin-grammar abiword-plugin-mathview
  aspell-en-doc-base latex-xft-fonts libaiksaurus-1.2-0c2a
  libaiksaurus-1.2-data libaiksauruskat-1.2-0c2a libfreetype-perl
  libfribidi0 libgdom2-0 libgdom2-cpp-smart0c2a libgoffice-0-4
  libgoffice-0-common libgsl-gnome-1-l14 libgtkmathview0c2a liblink-grammar4
  libloudmouth-1-0 libmdbm-perl libots0 libti-5 libuuid-perl libwww-1-2-3
  link-grammar-dictionaries-en
Suggested packages:
  abiword-plugin-goffice
The following NEW packages will be installed:
  abiword abiword-common abiword-help abiword-plugin-grammar
  abiword-plugin-mathview aspell-en-doc-base latex-xft-fonts
  libaiksaurus-1.2-0c2a libaiksaurus-1.2-data libaiksauruskat-1.2-0c2a
  libfreetype-perl libfribidi0 libgdom2-cpp-smart0c2a libgoffice-0-4
  libgoffice-0-common libgsl-gnome-1-l14 libgtkmathview0c2a
```

```text
liblink-grammar4 libloudmouth-1-0 libmdbm-perl libots0 libti-5 libuuid-perl
libwww-1-2-3 link-grammar-dictionaries-en
0 upgraded, 27 newly installed, 0 to remove and 0 not upgraded.
Need to get 0B/9858kB of archives.
After this operation, 31.3MB of additional disk space will be used.
Do you want to continue [Y/n]? y
Selecting previously deselected package libaiksaurus-1.2-data.
(Reading database ... 95088 files and directories currently installed.)
Unpacking libaiksaurus-1.2-data (from .../libaiksaurus-1.2-data-1.2.1+dev-0.12-
6_all.deb) ...
```

这将调用 *apt-get* 在数据库中搜索该软件包的最新版本，然后从 /etc/apt/sources.list 中指定的位置检索它，如果存在依赖项，则同时安装这些依赖软件包。在 install 选项中可以使用 `-y` 选项，自动对所有查询回答“是”，以减少用户交互。如果你希望确保文件是最新可用的版本，或者怀疑某些文件已损坏，你也可以重新安装软件包。

```bash
apt-get --reinstall install package_name(s)
```

你可以使用 install 选项中的 `-d` 选项下载软件包以便稍后安装。这些文件存储在 /var/cache/apt/archives 目录中。

```bash
apt-get -d install package_name(s)
```

## 移除软件包

使用 remove 选项从系统中移除软件包。

```bash
apt-get remove package_name(s)
```

该软件包将被移除，连同所有依赖于它的软件包一并移除。配置文件不会被移除，但添加 `--purge` 选项将移除与该软件包相关的所有文件。如果你确定将来不会使用该软件包，使用 purge 选项是很有价值的，因为它可以清理磁盘，不会在文件系统中留下大量不需要的文件。

## 高级安装和移除

你可以在同一命令行中安装和移除软件包。例如，要在安装软件包时移除某个 [或某些] 软件包，只需在软件包名称后加后缀“-”，该命令的语法看起来像这样：

```bash
apt-get install newpackage oldpackage-
```

因此，要安装 python 软件包并移除 nano 软件包，请使用：

```bash
apt-get install python nano-
```

## 安装、移除和更新程序

相反，要在安装软件包的同时移除一个软件包，需给要安装的软件包加后缀“+”

```bash
apt-get remove oldpackage newpackage+
```

在上述示例中，我们可以使用以下命令移除 nano 软件包并安装 python：

```bash
apt-get remove nano python+
```

## 升级软件包

在 APT 系统中，软件包的升级非常容易完成。当前发行版中的所有软件包都可以通过单条命令进行升级：

```bash
apt-get upgrade
```

要将软件包升级到新的发行版，最好使用以下命令，以确保软件包之间的所有关系都得到更新：

```bash
apt-get dist-upgrade
```

对于这两个命令，添加 `-u` 选项是值得的，以确保有足够的输出让你看到正在升级的内容。输出的初始部分如下所示：

```text
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages will be upgraded:
libcupsimage2 libcupsys2 libdnssd5 libebook1.2-9 libecall1.2-7 libedata-book1.2-2 libedata-call1.2-6 libedataserver1.2-9 libedataserverui1.2-8 libgeogroupwise1.2-13 libexchange-storage1.2-3 libfreepypes6 libgdata-google1.2-1 libgdata1.2-1 libglib2.0-0 libicu38 libisc45 libiscss40 libisccfw40 libkrb53 liblwres40 libm2o3js1d libmssqlclientiso9f1 libmss3-1d libpango1.0-0 libpng1.0.0-common libpoppler-glib3 libpoppler3 libpostproc51 libpurple0 libsasl2-2 libsasl2-modules libsmclient libss10.9.8 libvxml-ide-10 libwbclient0
```

## 通过示例学习：摆脱“依赖地狱”

当我在 20 世纪 90 年代后期刚开始使用 Linux 时，我选择了一个特别著名的发行版，唯一的原因是它很流行，并且我不必制作一堆软盘来开始安装。我想我当时有点不耐烦。在我学习 Linux 的过程中，我进步到安装各种应用程序的阶段，而我选择的发行版使用 RPM 作为包管理器。没过多久，我发现自己陷入了一个非常令人沮丧的境地，一个不友好的地方，叫做“依赖地狱”。我会下载一个 .rpm 软件包并执行 rpm -Uvh 命令，结果却发现我还需要多一两个甚至五个 .rpm 软件包，因为我想安装的运行需要这些其他文件先安装好。我会去追这些其他软件包，结果往往发现我需要额外的 .rpm 软件包，因为依赖项本身也有依赖项。一个看似简单的安装最终本应只需几分钟完成，实际上却花了一个多小时，因为我必须寻找、下载并安装所有的依赖项。出于这个原因，我切换到了使用 APT 作为包管理器的系统。APT 会自行进行依赖项检查，如果存在依赖项，它会参考散布在互联网上的应用程序存储库列表，并自动下载和安装它们以及我期望的应用程序。那感觉就像我死了并去了天堂。

## 获取软件包信息

你经常可能想安装一个软件包，但不确定该软件包的名字是什么。查找这些软件包的一种方法是使用 `apt-cache`。要搜索软件包，你需要使用：

```bash
apt-cache search name
```

例如，假设你想搜索 *abiword*，你可以执行命令 `apt-cache search abiword`，输出如下所示：

```text
abiword - efficient, featureful word processor with collaboration
abiword-common - efficient, featureful word processor with collaboration -- common files
abiword-help - online help for AbiWord
libgtkmathview0c2a - rendering engine for MathML documents
abiword-plugin-grammar - grammar checking plugin for AbiWord
abiword-plugin-mathview - equation editor plugin for AbiWord
abiword-plugin-goffice - GOffice interaction plugin for AbiWord
```

要获取有关特定软件包的更多信息，你需要使用以下命令 `apt-cache show abiword`，输出的第一部分如下所示（为简洁起见已编辑）：

```text
Package: abiword
Priority: optional
Section: editors
Installed-Size: 7352
Maintainer: Masayuki Hatta (mhatta) <mhatta@debian.org>
Architecture: i386
Version: 2.6.4-5
```

