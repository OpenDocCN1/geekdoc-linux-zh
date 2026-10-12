
- 在使用 `cp` 命令时，你是否有足够的磁盘空间在本地驱动器上存储数据 CD 的副本？

- 空白可刻录 CD 是否真的是一个空白、未使用过的、没有划痕、污垢或其他问题的？

- 可刻录 CD 是否能够记录与你用 `mkisofs` 创建的 `backup.iso` 文件相同的信息？你可以通过以下命令查看 `backup.iso` 文件的兆字节大小：

```
ls -l --block-size=MB backup.iso
```

请参阅章节后部分的“cdrecord”部分了解其他可能的问题。

## 使用 mkisofs

在如何备份数据到 CD-R(RW) 的说明中，你使用了 `mkisofs` 实用将备份文件转换为适用于刻录到 CD-R(RW) 的 CD 镜像。再次查看该命令：

```
mkisofs -o backup.iso -x /home/joeuser/emptydirectory/ -J -R -A -V -v / home/joeuser/
```

表 8-1 解释了每个命令行选项。有关 `mkisofs` 的更多信息，请参阅章节后面的。

### 表 8-1：mkisofs 选项

| 选项 | 功能 |
| --- | --- |
| `-O` | 输出镜像文件名。 |
| `-J` | 生成 Juliet 命名记录；适用于 Windows 环境。 |
| `-R` | 生成 Rock Ridge (RR) 命名记录以保留文件名大小写，特别适用于 Unix/Linux 环境。 |
| `-A` | 设置应用程序 ID --a 字符串，将写入镜像的卷标。 |
| `-V` | 设置卷 ID --a 名称，当镜像被刻录时分配。 |
| `-v` | 设置详细执行，用于查看镜像制作过程的状态。 |
| `-x` | 从即将创建的镜像中排除目录。 |

## cdrecord

一旦你有了 CD 镜像，使用 `cdrecord` 将其写入 CD-R(RW)。这里是命令的另一种写法：

```
cdrecord -v dev=1,0,0 backup.iso
```

你还可以通过以下命令使用 `cdrecord` 擦除 CD 以重复：

```
cdrecord --dev=1,0,0 --blank
```

## 附加资源

本章简要介绍了一些应用程序。更多信息请参考以下资源。

### 安装文档

- `cdrecord` 手页——讨论了如何刻录数据、音频和混合模式 CD-ROM。提供了详细的选项和命令，以及 CD-R(W) 刻录任务的示例。

- `/usr/share/doc/cdrecord-version`（`version` 是你系统中安装的 cdrecord 版本）——包含了通用用法和许可信息的文档文件。

- `mkisofs` 手页——该工具的详细介绍，包括关于创建 ISO 类型的警告。提供了详细的选项和命令，以及创建 ISO 镜像文件的示例。

- `/usr/share/doc/mkisofs-version`（`version` 是你系统中安装的 mkisofs 版本）——包含了通用用法和许可信息的文档文件。

- `xcdroast` 手页——包含了 CD-R(W) 刻录应用的有用命令行选项和使用信息。

- `/usr/share/doc/xcdroast-version`（`version` 是你系统中安装的 xcdroast 版本）——如果你有 DVD-R(+W) 设备，这些文档将帮助你开始制作数据备份和多媒体演示的 DVD-ROM。

### 有用的网站

- `http://www.xcdroast.org/`——X-CD-Roast 项目的官方网站。

- `http://freshmeat.net/projects/cdrecord/`——Freshmeat 上的 cdrecord 项目页面会定期更新最新发布、新闻和用户评论。

- `http://www.freesoftware.fsf.org/dvdrtools/`——dvdtools 项目的官方网站，其中包含了用于刻录 DVD-R(+W) 光盘的 `dvdrecord` 工具。

# 命令行威力：Shell 提示符基础

在图形化桌面和鼠标出现很久以前，计算机用户通过输入命令和编写脚本来自动化这些命令来工作。“理解”这些命令并执行它们的程序称为 shell（外壳）。Linux 提供了许多命令 shell，但默认 shell 是 Bourne Shell 的一个免费许可变体（以其创建者 S.R. Bourne 命名）。Linux 变体称为 Bourne Again Shell，更广为人知的是 bash。

这个 shell 提示符（也称为命令行界面，或 CLI）是你的 Fedora 系统的纯文本界面，它比以往任何时候都要强大。几乎任何管理任务（如管理文件、用户和组）都可以在 shell 提示符中完成。当你在 shell 提示符处输入命令时，shell 会解释这些命令并告诉 Linux 操作系统（OS）该做什么。经验丰富的用户可以编写 shell 脚本来扩展他们的功能。

默认情况下，Fedora 使用 bash shell，但如果你有需要，可以在命令提示符处输入 shell 的名称来切换到另一个 shell；例如，在 bash 提示符处输入 `csh` 即可切换到 C shell。

本章将介绍如何通过 shell 提示符与 Fedora 交互的基础。

## 为什么要使用 shell 提示符？

Linux 的图形化环境在过去几年里取得了巨大进步。你在 X Window 系统中可以完全高效地工作，几乎不需要打开 shell 提示符来完成所有工作。许多 Fedora 功能在 shell 提示符中完成的速度比在 GNOME 或 KDE 等图形化桌面上更快。例如，在 shell 提示符中定位目录、创建、删除和修改文件，比打开文件管理器并使用图形桌面通过点击来执行相同操作要简单快捷得多。正如你在图 9-1 中所示，shell 提示符看起来与你熟悉的其他命令行界面相似，例如 MS-DOS。

![](img/67d9607982940021da1fe4247b9b224c_175_0.png)

**图 9-1：** Shell 提示符

后续章节将解释如何导航、操作文件、执行简单的管理任务以及其他 shell 提示符基础。

## 打开 shell 提示符

在可以在 shell 提示符处输入命令之前，你需要启动一个，或者换句话说，打开一个终端窗口。你可以从系统菜单中选择多个可用终端，它们根据你使用的是 Fedora 的 GNOME 版本还是 KDE 版本而略有不同。无论你使用的是 GNOME 还是 KDE，都可以在桌面的空白区域点击右键，并在弹出菜单中选择“打开终端”（Open Terminal）。你也可以通过按 Alt-F2 弹出运行命令对话框来打开一个基础命令行提示符终端，然后你可以输入 `xterm` 并按回车键。

## 什么是目录？

当你双击桌面上的主目录图标时，你打开了一个所谓的“文件夹”（folder）。图形桌面通常使用“文件夹”一词来反映办公环境，在其中你将文档存储在文件夹中，可能将这些文件夹存储在其他文件夹中。但在 Linux 中，文件夹就是目录（directory）。当你另一个文件夹内部创建一个新文件夹时，你实际上是在一个目录下方（或内部）创建了一个新目录。将新目录视为现有目录的分支可能会很有用，因为整个目录系统是一个目录树。Linux 文件系统的根由从根目录开始的目录组成。在“根目录”术语中的 root 与 root 用户（超级用户）没有关系。在这种情况下，root 一词仅仅意味着该目录位于整个目录树的根部或基部。

根目录是 `/`。根目录下有一个名为 `/home` 的目录，那是所有用户主目录存储的地方。例如，carlotta 的主目录是 `/home/carlotta`。

你系统上的几乎所有内容都被视为目录或文件。甚至你的 CD-ROM 和软盘也被视为目录。你的 CD-ROM 驱动器通常被挂载并访问为目录 `/mnt/cdrom`，软盘通常被挂载并访问为 `/mnt/floppy`。所以，如果你挂载了一张光盘并想查看该光盘上存在哪些文件和目录，你应该查看 `/mnt/cdrom` 目录来查找。

### 使用 `pwd` 确定当前目录

一旦你开始浏览目录，就很容易获取或忘记当前目录的名称。默认情况下，bash shell 仅显示当前目录，而不是整个路径。

要确定当前目录在文件系统中的确切位置，请进入 shell 提示符，输入命令 `pwd` 并按回车，如图 9-2 所示。

你应该看到类似这样的内容：

```
/home/carlotta
```

这告诉你你位于用户 carlotta 的目录中，该目录位于 `/home` 目录。

![](img/67d9607982940021da1fe4247b9b224c_176_0.png)

图 9-2：`pwd` 命令显示你所在的位置

`pwd` 命令代表 print working directory（打印工作目录）。当你输入 `pwd` 命令时，你基本上是在要求 Linux 显示你在文件系统中的当前位置。Linux 通过在 shell 提示符显示屏（也称为标准输出）打印当前目录的名称来响应。

### 使用 `cd` 切换目录
