
你的电脑必须至少有 16MB 内存才能运行 GNOME，为了获得性能至少需要 32MB。如果你从二进制文件（如 `rms`）安装，则至少需要 50MB 磁盘空间；如果你从源码（`tarball` 包）安装，则需要 200MB 磁盘空间。显卡内存也很重要——内存越大，GNOME 运行得越快。如果你的显卡内存较小，GNOME 也可以运行，但可能会很慢，特别是当你使用复杂的窗口管理器时。如果你的显卡内存小于 4MB，请安装一个像 `sawmill` 这样的简单窗口管理器，并使用简单、整洁的主题。我们将在第 4 小时“使用窗口管理器”中学习更多窗口管理器，并在第 12 小时“理解和使用主题”中学习更多主题。

## 必要的软件

要运行 GNOME，你必须在电脑上安装并配置了功能完整的 `XFree86` X 服务器。在安装 GNOME 之前，请获取 X 服务器的最新版本。如果你运行常见的 Linux 发行版，你的 X 服务器很可能是 `XFree86`。在继续之前，请从 `http://www.xfree86.org` 下载最新的更新。在编写此时，`XFree86` 的最新版本是 `3.3.6`。

`XFree86 3.3.6` 版本于 2000 年 1 月发布。现在已支持许多错误。除了 X 服务器之外，在安装 GNOME 之前你必须拥有以下软件……（注：此处原文存在大量重复文本，已根据要求去重处理）。

## 查找已安装组件

要了解电脑上是否安装了某个组件，请使用 `locate` 命令。首先，在提示符处输入 `updatedb` 更新列出系统中每个文件路径的数据库。然后，输入以下命令查找特定文件，将 `[filename]` 替换为实际文件名：

```bash
locate [filename]
```

## 图 2.1

`locate` 的输出显示了文档加载的位置，但不是文件本身，如列表 2.1 所示。

## 列表 2.1 `locate` 命令及其输出

`locate esound` 的示例显示文档加载在此处，但实际文件并不在此。注意 `[root]@localhost i386]# locate esound:`：

```
/usr/doc/esound-0.12/AUTHORS
/usr/doc/esound-0.12/COPYING
/usr/doc/esound-0.12/ChangeLog
/usr/doc/esound-0.12/INSTALL
/usr/doc/esound-0.12/NEWS
/usr/doc/esound-0.12/README
/usr/doc/esound-0.12/TIPS
/usr/doc/esound-0.12/TODO
```

以下列表给出了你将在电脑上安装的第一组非 GNOME 组件（或验证你已拥有的组件），顺序如下：

- `libjpeg`
- `libpng`
- `libungif`
- `libtiff`
- `libgr`
- `ImageMagick`
- `zlib`
- `guile`
- `Berkeley DB`

## 图 2.2

当没有安装 KDE 和 GNOME 时，红帽和 Mandrake Linux 将 `fvwm` 作为桌面环境。

# 安装 GNOME

> 本章列出的所有 GNOME 组件都可以在随书附赠的 CD-ROM 中找到。在你运行了一个可用的 GNOME 版本后，可以按照本节的说明进行升级。

## 选择安装方法

安装 GNOME 有三种方法方法：作为 Linux 发行版的一部分从 CD-ROM 安装、从预编译的二进制包（如 `rpm` 格式包）安装，以及从源码安装。在本节中，我们将讨论前两种方法的优缺点。从源码安装 GNOME 的过程更为复杂，将在第 22 节“升级 GNOME 并加入 GNOME 项目”中进行介绍。

## 从 CD-ROM 安装 GNOME

安装 GNOME 最简单的方法是从 CD-ROM 作为预装包 Linux 发行版的一部分进行安装。如果你是 Linux 新手，或者只是想快速、简单地搭建 GNOME，那么这种方法适合你。所有软件包都经过脚本处理，会按正确的顺序安装，因此你不必担心在本章末讨论的错误。如果你从同一张光盘安装 Linux 和 GNOME，可能遇到问题。

从 CD-ROM 安装的主要缺点是 GNOME 组件已经过时了。即使你是从 CD 进行初始安装，也应该在初始 CD 安装后，按照本章的说明升级你的 GNOME 组件。

如果你的 Linux CD 中有 GNOME，但在安装 Linux 时没有安装它，你可以再次运行安装程序进行升级（参阅你的 Linux 文档），也可以直接从 CD-ROM 将文件 `rpm` 到你的硬盘上。

将 CD-ROM 插入驱动器。使用 `/etc/fstab` 中创建的挂载点挂载 CD-ROM（在以下示例中，挂载点为 `/mnt/cdrom`）。

```
# mount /mnt/cdrom
```

接下来，通过输入命令更新你的文件数据库

```
# updateddb
```

使用 `locate` 命令找到列表中的每个组件。在列表 2.2 中，`locate` 显示版本为 0.2.10 的 `esound` 已经安装。

### 列表 2.2 使用 locate esound

```
# locate esound
/mnt/cdrom/Mandrake/RPMS/esound-0.2.12-6mdk.i586.rpm
/mnt/cdrom/Mandrake/RPMS/esound-devel-0.2.12-6mdk.i586.rpm
/usr/doc/esound-0.2.10
/usr/doc/esound-0.2.10/AUTHORS
/usr/doc/esound-0.2.10/COPYING
/usr/doc/esound-0.2.10/ChangeLog
/usr/doc/esound-0.2.10/INSTALL
/usr/doc/esound-0.2.10/NEWS
/usr/doc/esound-0.2.10/README
/usr/doc/esound-0.2.10/TIPS
/usr/doc/esound-0.2.10/TODO
/usr/doc/esound-0.2.10/esound.sgml
/usr/src/RPM/i386/esound-0.2.10-1.i386.rpm
```

如你所示，CD-ROM 上的版本是较版本，因此我们将使用 `rpm -Uvh` 命令进行更新：

# cd /mnt/cdrom/Mandrake/RPMS/esound-0.2.12-6mdk.i586.rpm

# rpm -Uvh esound-0.2.12-6mdk.i586.rpm

在卸载 CD 之前，你不需要再次更新。在 CD 上找到每个组件并以相同的方式安装。除非你卸载并重新挂载 CD，或者更换了 CD，否则无需重复 `updatedb` 命令。

按以下顺序安装组件：

- `audiofile`
- `esound`
- `glib`
- `libxml`
- `ORBit`
- `GTK+`
- `imlib`
- `fnlib`
- `gnome-audio`
- `gnome-libs`
- `lib-gtop`
- `libhttp`
- `enlightenment`
- `xloadimage`
- `xscreensaver`
- `gnome-core`
- `mc`
- `control-center`
- `libglade`
- `gnome-print`
- `ee`
- `gtop`
- `extace`
- `gnome-media`
- `gnome-pim`
- `gnome-utils`
- `gnome-games`
- `gnome-users-guide`
- `numericic`

## 从下载的 rpm 安装 GNOME

`rpm` 是已经为你编译成二进制格式的包。目前，Red Hat/Mandrake Linux、Caldera Linux、LinuxPPC、SuSE Linux、Debian 和 Solaris 都有二进制包。如果你将 GNOME 安装到另一个系统，请参阅第 15 节“互联网与 GNOME”中的“从源码安装 GNOME（tarballs）”。你可以在 `http://www.gnome.org/start` 了解更多关于二进制包的信息。显示了 GNOME 安装网页。

要从二进制包安装 GNOME，首先将包下载到中心位置，例如 `/usr/src/RPM`。

```
http://www.gnome.org/start
```

```
http://www.enlightment.org
```

```
http://www.redhat.com/download (或你的 Linux 发行版网站)
```

### 图 2.3

尽管 GNOME 官方仅支持从压缩包（tarballs）安装，但从服务器那里有许多二进制包![](img/56ffc05f2012b0375f0809ea492838b_45_0.png)

下载列表中的所有包：

- `audiofile`
- `gnome-core`
- `esound`
- `mc`
- `glib`
- `control-center`
- `libxml`
- `liblade`
- `ORBit`
- `gnome-print`
- `GTK+`
- `ee`
