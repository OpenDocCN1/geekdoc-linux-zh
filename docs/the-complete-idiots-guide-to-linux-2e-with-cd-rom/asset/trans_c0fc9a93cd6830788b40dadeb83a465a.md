

已安装的软件及其相互依赖关系。此数据库可搜索，因此您可以查找文件属于哪个软件包，甚至可以检查文件自初始安装以来是否已被修改、意外损坏或删除。就依赖关系而言，RPM 确保您安装其他软件运行可能需要的任何必需软件包。

RPM 可以通过 FTP 工作，因此您无需下载软件即可安装它；RPM 可以同时完成这两项工作。它还管理着配置文件，因此当您升级软件或系统时，这些自定义设置会得以保留。这是自升级开始以来所有操作系统和软件安装一直存在的问题。

对于开发人员和程序员，RPM 允许将二进制文件（程序）和源代码打包供用户使用。如果开发人员修改了程序的源代码，这些称为“补丁”的内容会与“原始”或原始源代码分开维护。这使得升级基本源并将补丁重新应用到新版本变得容易。

对于管理员，RPM 允许他们升级系统，而无需重新安装所有内容然后进行配置。RPM 能够高效地仅升级已更改的软件包，而不会丢失您的自定义设置。

有关 RPM 的最新信息，请访问 Web 上的 http://www.rpm.org。

## 安装、升级、降级和删除软件

仅凭您可以在系统上安装、升级和降级软件，并在无需手动操作的情况下将其从系统中删除这一事实，就足以成为安装 rpm 软件的理由。

## 安装

安装软件包极其简单。以下是语法：

```
rpm -i mypackage-1.0-2.i386.rpm
```

通常，您可能需要具有 root 权限才能安装软件包。RPM 会负责安装所有内容——软件和文档——将所有内容放在正确的位置。

安装时可能会出现一些错误。如果 RPM 检测到新软件包将覆盖另一个软件包的文件，它会通知您冲突。要覆盖，可以提供 --replacefiles 选项：

```
rpm -i --replacefiles mypackage-1.0-2.i386.rpm
```

如果软件包依赖于另一个软件包，您会看到一个错误，提示该软件包需要另一个软件包。您应该获取所需的软件包，然后重试软件的安装。您也可以使用 --nodeps 选项覆盖此警告；但是，这样做会给自己带来问题。

如果软件已经安装，您会收到一个错误，提示该软件包已安装。要覆盖安装该软件包，您应提供 --replacepkgs 选项，如下所示：

```
rpm -i --replacepkgs mypackage-1.0-2.i386.rpm
```

## 升级

升级应用程序与安装一样简单。不是指定 -i 选项，而是指定 -U 选项，如下所示：

```
rpm -U mypackage-1.0-4.i386.rpm
```

需要记住的是，升级软件包实际上会卸载之前的安装。如果升级版本的配置文件不兼容，您会看到一条消息告知您。RPM 会为您保存原始配置文件，以便您与新文件进行核对。

## 降级

有时升级实际上是升级到新的不良错误。要降级回您在获取错误之前使用的软件，只需升级到旧软件包并提供 --oldpackage 选项即可。

```
rpm -U --oldpackage myoldpackage-1.0-1.i386.rpm
```

## 卸载

如果您发现自己不需要已安装的软件，请使用 -e（Erase）标志。这次，只提供软件包的基本名称。对于名为 mypackage-1.0-4.i386.rpm 的软件包，只需输入以下内容：

```
rpm -e mypackage
```

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark It

Search this book:

Previous Table of Contents Next

## 已安装软件的数据库

RPM 中最有趣的功能是能够查询有关系统上已安装文件和软件包的信息。此功能非常强大，因为您可以查询 RPM 以搜索已安装软件列表中的许多内容。查询（搜索）使用 -q 选项进行。

## 查找有关软件包的信息

要查找有关软件包文件的信息，请对软件包执行 rpm 查询。您应输入以下内容：

```
rpm -qip packagefile
[alberto@digital alberto]$ rpm -qip DUMP-0_4.RPM
Name        : dump                          Distribution: OpenLinux 1.2
Version     : 0.4b4                          Vendor: Caldera, Inc.
Release     : 1                              Build Date: Wed Jan 07
                                            01:15:34 1998
Install date: (not installed)                Build Host: '
                                            buildmeister.caldera.com
Group       : Administration/Archiving      Source RPM: dump-0.4b4-1.
                                            src.rpm
Size        : 295767
Packager    : Raymund Will <ray@lst.de>
Summary     : BSD dump/restore backup system (BETA).
Description :
 dump and restore, as known from BSD/SunOS/..., is a quite
 reliable method for backup, because 'dump' gets all needed
 information directly from the storage media -- not via
 the high-level filesystem-interface (as tar, cpio, etc. do).

 Additionally the output format of dump is readable on
 other platforms (like SunOS, BSD) and vice versa.

 But BEWARE, this software is still under development (BETA)!!!
 Don't rely too much on it -- but without testing, there would be
 no further improvement! Interleave with another backup method
would be a good idea.

## 查找拥有文件 的软件包

如果您想知道文件来自哪个软件包，请输入以下命令：

```
rpm -q -f filepath
[alberto@digital alberto]$ rpm -q -f /sbin/restore
dump-0.4b4-1
```

## 查找由软件包拥有的文件

要查看软件包拥有的所有文件，只需输入以下内容：

```
rpm -q -l packagename
[alberto@digital alberto]$ rpm -q -l dump
/etc/dumpdates
/etc/rmt
/sbin/dump
/sbin/rdump
/sbin/restore
/sbin/rmt
/sbin/rrestore
/usr/doc/dump-0.4b4-1
/usr/doc/dump-0.4b4-1/CHANGES
/usr/doc/dump-0.4b4-1/COPYRIGHT
/usr/doc/dump-0.4b4-1/KNOWNBUGS
/usr/doc/dump-0.4b4-1/THANKS
/usr/doc/dump-0.4b4-1/TODO
/usr/doc/dump-0.4b4-1/dump-0.4b1.announce
/usr/doc/dump-0.4b4-1/dump.lsm
/usr/man/man8/dump.8.gz
/usr/man/man8/rdump.8.gz
/usr/man/man8/restore.8.gz
/usr/man/man8/rmt.8.gz
/usr/man/man8/rrestore.8.gz
```

## 查找与软件包相关的文档

假设您想了解与特定软件包一起安装的所有文档来源。RPM 也能在这里提供帮助。只需输入以下内容：

```
rpm -q -d packagename
[alberto@digital alberto]$ rpm -q -d dump
/usr/doc/dump-0.4b4-1
/usr/doc/dump-0.4b4-1/CHANGES
/usr/doc/dump-0.4b4-1/COPYRIGHT
/usr/doc/dump-0.4b4-1/KNOWNBUGS
/usr/doc/dump-0.4b4-1/THANKS
/usr/doc/dump-0.4b4-1/TODO
/usr/doc/dump-0.4b4-1/dump-0.4b1.announce
/usr/doc/dump-0.4b4-1/dump.lsm
/usr/man/man8/dump.8.gz
/usr/man/man8/rdump.8.gz
/usr/man/man8/restore.8.gz
/usr/man/man8/rmt.8.gz
/usr/man/man8/rrestore.8.gz
```

现在您知道要为您的软件包阅读什么了！

## 验证您的系统

很多时候您可能需要能够检查文件或应用程序，甚至整个系统是否存在损坏的迹象。RPM 会跟踪校验和（一种计算出可用于确定文件内容是否更改的唯一数字的复杂计算）。通过发出一个简单的命令（rpm -Va）您可以验证整个系统！

如果 RPM 打印出某些内容，很可能该软件包需要重新安装。如果您看不到任何消息，则验证过程成功。指定 rpm -Vf 将仅验证单个文件。请注意，您修改的一些配置文件将被列出，但这是正常的。

要将已安装的软件包与软件包文件进行比较，您将输入 rpm -Vp fullpackagename，如以下示例所示

```
rpm -Vp mypackage-1.0-4.i386.rpm
```

## RPM 的图形前端

有几个 RPM 的图形前端可用：一个是 KDE 环境的一部分，称为 kpackage（kpackage-0.9.02-1.i386.rpm；请参阅下图），另一个称为 glint（glint-2.3-3.rpm）。虽然拥有 UI 版本的程序是朝着正确方向迈出的一步，但命令行工具提供了 UI 中无法访问的许多功能。出于这个原因，我将介绍该程序的命令行版本。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_248_0.png)

这是 kpackage 工具的屏幕截图。它为安装 RPM 软件包提供了一个不错的前端；然而，它缺乏 RPM 程序提供的许多强大的查询功能。

