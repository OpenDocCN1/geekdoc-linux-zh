

# 使用 Linux 命令浏览文件系统

此命令将名为 `/dev/cdrom`（DVD/CD-ROM）的设备文件系统挂载到 Linux 系统中的 `/mnt/cdrom` 目录（也称为挂载点）。

在 `mount` 命令成功完成任务后，你就可以通过 `/mnt/cdrom` 目录视为光盘的根目录来访问 DVD-ROM 上的文件。换句话说，要查看 DVD-ROM 的内容，输入

```
ls -F /mnt/cdrom
```

当你使用 DVD-ROM 时 —— 在将其从驱动器中弹出之前 —— 你必须使用以下命令“卸载”光驱驱动器：

```
umount /dev/cdrom
```

将设备挂载到 `/mnt` 目录下的目录是习惯做法。Linux 自带了两个预定义的目录：`/mnt/cdrom` 用于挂载 DVD/CD-ROM，`/mnt/floppy` 用于挂载软驱驱动器。

# 检查磁盘空间使用的命令

我想告诉你们两个命令 —— `df` 和 `du` —— 你可以用它们来检查系统的磁盘空间使用情况。这些命令非常易用。`df` 命令显示所有挂载设备磁盘空间使用的摘要。我们在示例中显示的 `df` 输出：

| Filesystem 1K-blocks Used Avail% Mounted on |
|---|---|---|---|---|
| /dev/hda5 7392428 3855112 3161800 55% / |
| /dev/hda3 101105 15760 80124 17% /boot |
| none 127880 0 127880 0% /dev/shm |
| /dev/cdrom 658144 658144 0 100% /mnt/cdrom |

输出是一个表格，显示了设备、存储总字节数（单位为K 块）、已用量、可用量、使用百分比以及挂载点。

要以更易于人类阅读的格式查看 `df` 的输出，请输入 `df -h`。以下是 `df -h` 的输出：

```
Filesystem Size Used Avail% Mounted on
|---|---|---|---|---|
| /dev/hda5 7.1G 3.7G 3.1G 55% / |
| /dev/hda3 99M 16M 79M 17% /boot |
| none 125M 0 125M 0% /dev/shm |
| /dev/cdrom 643M 643M 0 100% /mnt/cdrom |
```

![](img/d9230b719dc0efd80851f363d8c6f571_193_0.png)

![](img/d9230b719dc0efd80851f363d8c6f571_193_1.png)

![](img/d9230b719dc0efd80851f363d8c6f571_193_2.png)

# 168 使用 Linux 命令浏览文件系统

如果你将此输出与普通 `df` 的输出（见上一个列表）相比，你会发现 `df -h` 使用类似 M（兆字节）和 G（GB）的术来打印大小。这些显然比 `1K-blocks` 更容易理解。

另一个命令 `--du` 可用于查找目录占用了多少空间。例如，输入以下命令查看 `/etc/rc.d` 目录下所有目录的内容（该目录包含系统启动文件）：

```
du /etc/rc.d
4 /etc/rc.d/rc1.d
4 /etc/rc.d/rc0.d
4 /etc/rc.d/rc5.d
4 /etc/rc.d/rc3.d
4 /etc/rc.d/rc4.d
4 /etc/rc.d/rc2.d
308 /etc/rc.d/init.d
4 /etc/rc.d/rc6.d
372 /etc/rc.d
```

每个目录名称前面都有一个数字 —— 它告诉你该目录占用了多少 KB 的磁盘空间。因此，`/etc/rc.d` 目录整体使用了 372K 的磁盘空间，而 `/etc/rc.d/init.d` 目录（包含该目录下的所有文件和子目录可以使用 `-s` 选项，如下：

```
du -s /etc/rc.d
372 /etc/rc.d
```

`-s` 选项导致 `du` 打印 `/etc/rc.d` 目录的摘要信息。

![](img/d9230b719dc0efd80851f363d8c6f571_194_0.png)

就像 `-h` 以兆字节和 GB 输出磁盘空间信息一样，你可以使用 `-h` 命令以更易于人类阅读的格式查看 `du` 的输出。例如，这里是如何使用 `-s` 选项查看我的主目录（`/home/naba`）使用的空间：

```
du -sh /home/naba
29M /home/naba
```

# 第 4 章：探索 Fedora Core 应用

本章内容

- 盘点 Fedora Core 应用
- 探索办公应用
- 设置数据库
- 玩转多媒体
- 处理图像

Fedora Core 自带了大量的应用程序。你只需要查看 GNOME 或 KDE 的菜单，就能明白我的意思了。通常，每种类型不止一个应用程序。GNOME 和 KDE 都带了 OpenOffice.org 办公套件，其中包含文字处理器、电子表格、演示文稿软件等。你会发现许多 CD 播放器和多媒体播放器的选择，更不用说游戏、实用程序以及有用工具，如扫描仪和数字相机应用。

我将为你概述这些应用中的，并简要向你展示一些有趣实用的应用。在了解这些应用后，你可以在需要时尝试它们。

# 盘点 Fedora Core 应用

表 4-1 显示了按类别组织的主要的 Fedora Core 应用示例。对于主要应用程序，我还显示了相关的网站，你可以在那里获取有关该应用程序的更多信息。此列表绝非详尽。Fedora Core 发行版带有比表中更多的应用程序和实用工具。

如果你的系统安装了 GNOME 和 KDE，这些大部分应用程序都是可用的。

我简要介绍表中的某些应用程序，并从每个类别中选择一两个。

# 170 盘点 Fedora Core 应用

| 表 4-1 Fedora Core 应用示例 |
|---|---|
| 应用 | 说明 |
| 办公应用 | |
| OpenOffice.org Writer | 类似于 Word 的文字处理程序 (www.office.org) |
| OpenOffice.org Calc | 类似于 Excel 的电子表格程序 (www.office.org) |
| OpenOffice.org Impress | 类似于 PowerPoint 的演示文稿应用 (www.office.org) |
| OpenOffice.org Draw | 一个绘图程序 (www.office.org) |
| OpenOffice.org Math | 用于编写数学公式的编辑器，可以包含在 OpenOffice 文档中 (www.office.org) |
| Dia | 一个绘图程序 (www.office.org) |
| 办公工具 | |
| GNOME Calculator | 一个简单的计算器 |
| Kcalc | KDE 的计算器 |
| Aspell | 文本模式拼写检查器
| Dictionary | 字典服务器的图形客户端，你可以从中查找单词 |
| 数据库 | |
| PostgreSQL | 复杂的对象关系数据库管理系统，支持 SQL |
| MySQL | 流行的数据库管理系统，支持 SQL |
| 多媒体 | |
| GNOME CD Player | 音频 CD 播放器 |
| Rhythmbox | 可以播放许多格式的多媒体播放器 |
| Internet | |
| Ksnapshot | 屏幕截图程序 |

# 办公应用和工具

| 应用 | 说明 |
|---|---|
| Cdrecord | 一个可以刻录音频 CD 以及 DVD-R 的命令行应用 |
| XC-Roast | cdrecord 和 cdrdao 的图形界面，使刻录变得简单 (www.xcdroast.org) |
| Gtkam | 支持 150 台数字相机的数字相机应用 (g.sourceforge.net/gtkam/) |
| 图形和图像 | |
| The GIMP | GNU 图像处理，适用于照片修饰、图像合成和图像创作 (www.gimp.org) |
| GQView | 强大的图像查看器 (gv.sourceforge.net) |
| Kview | KDE 的简单图像查看器 |
| GGV | Gnome Ghost (GGV) 是一个 PostScript 文档查看器 (www.gnu.org/directory/print/misc/ggv.html) |
| Xsane | 用于通过 Xsane（扫描仪访问容易）库访问扫描器的图形界面 (www.xsane.org) |
| Internet | |
| Xianian Evolution | 一种集成电子邮件、日历、联系人管理和在线任务列表个人信息管理应用 (www.xmian.com/products/xmian_evolution) |
| GFTP | 从网络下载文件的 FTP 客户端 |
| Gaim | AOL 消息客户端 (gaim.sourceforge.net) |
| Mozilla | 著名的开源 Web 浏览器，源自 Netscape 源码 (www.mozilla.org) |
| Kmail | KDE 的电子邮件客户端 (kmail.kde.org) |

文字处理器、电子表格、演示文稿软件、日历、计算器 —— 这些都是办公的核心组件。GNOME 和 KDE 都带了 OpenOffice.org（通常缩为 OO.o 或 Ooo）办公应用套件和工具。你可以尝试其中的每一个，看看哪个更适合你。

