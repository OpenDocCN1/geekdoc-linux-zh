
- `qR package` — 列出软件包依赖的所有组件（如库和命令）。
- `ql package` — 列出软件包包含的所有文件。
- `qd package` — 列出软件包中所有的文档文件。
- `qc package` — 列出软件包中所有的配置文件。

## 第 5 章：访问和运行应用程序 215

- `qp [option] package` — 表示未安装的软件包。使用此选项结合其他查询选项，可以让你查询你尚未安装的软件包。

要列出计算机上所有安装的软件包，请使用 `-a` 查询选项。由于列表很长，你应该将输出管道到 `less`，或者可能使用 `grep` 来查找你需要的软件包。以下命令列出了所有已安装的 RPM 包，然后只显示包含字符串 `xfree` 的名称。（`grep` 的 `-i` 选项表示忽略大小写）。

```bash
# rpm -qa |grep -i xorg
```

如果你对特定软件包的详情感兴趣，可以使用 `rpm -i` 查询选项。在下面的示例中，显示了 `dosfstools` 软件包（用于在 Linux 中处理 DOS 文件系统）的信息：

```
# rpm -qi dosfstools
Name : dosfstools Relocations: (not relocatable)
Version : 2.11 Vendor: Red Hat, Inc.
Release : 6.1.fc6 Build Date: Wed 12 Jul 2006 02:56:22 AM CST
Install Date: Fri 22 Sep 2006 12:44:53 PM CDT
Build Host : hs20-bc2-4.build.redhat.com
Group : Applications/System RPM:dosfstools-2.11-6.1.fc6.src.rpm
Size : 74865 License: GPL
Signature : DSA/Sha1, Thu 24 Aug 2006 09:28:51 PM CDT, Key ID fd372689927da0
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary : Utilities for making and checking MS-DOS FAT filesystems on Linux.
```

`dosfstools` 软件包包含了 `mkdosfs` 和 `dosfsck` 工具程序，它们分别在硬盘或软磁盘上创建和检查 MS-DOS FAT 系统。

要了解某个软件包的内容，你可以在查询时使用 `-l` (list) 选项。下面的示例显示了 `dosfstools` 软件包包含的文件的完整路径：

```bash
# rpm -q1 dosfstools | less
/bin/dosfsck
/bin/fsck.msdos
/bin/fsck.vfat
/bin/mkdosfs
/bin/mkfs.msdos
/bin/mkfs.vfat
/usr/share/man/man8dosfsck.8.gz
```

## 216 第二部分：使用 Fedora 和 RHEL

你想要知道如何使用软件包中的组件吗？在查询时使用 `-d` 选项将显示软件包包含的文档（帮助页、README 文件、HOWTO 等）。如果你在让 X Window 系统正常运行方面遇到困难，可以使用以下命令行来查找可能有所帮助的文档：

```bash
# rpm -qd xorg-x11 | less
/usr/X11R6/man/man1/Xark.ix.gz
/usr/X11R6/man/man1/Xorg.ix.gz
/usr/X11R6/man/man1/Xserver.ix.gz
/usr/X11R6/man/man1/appres.ix.gz
/usr/X11R6/man/man1/atomb.ix.gz
/usr/X11R6/man/man1/bitmap.ix.gz
/usr/X11R6/man/man1/bmtoa.ix.gz
```

许多软件包都有与其关联的配置文件。要查看与特定软件包关联配置文件，请在查询时使用 `-c` 选项。例如，这是你输入的内容以查找用于 `ppp` 软件包的配置文件：

```bash
# rpm -qc ppp
/etc/logrotate.d/ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果你想知道某个特定命令或配置文件来自哪个软件包，可以使用 `-q` 选项。在下面的示例中，`-q` 选项显示 `chgrp` 命令来自 `fileutils` 软件包：

```bash
# rpm -qf /bin/chgrp
coreutils-5.97-11
```

在安装软件包之前，你可以对它进行与已安装软件包相同的查询。这对于查找软件包位于当前目录或软件存储库中的信息非常有用的工具。以下是使用 `-qp` 选项的示例——查看软件存储库中软件包的描述：

```bash
# rpm -q -i -
http://ayo.freshrpms.net/fedora/linux/1/i386/freshrpms/RPMS/blackbox-0.65.0-8.1.fcl.fr.i386.rpm
Name : blackbox          Relocations: (not relocatable)
Version : 0.65.0        Vendor : Freshrpms.net
Release : 8.1.fcl.fr    Build Date: 25 Mar 2004 12:45:45 PM PST
```

## 252 第 5 章：访问和运行应用程序 217

要查找软件包的内容，你可以在查询时使用 `-l` (list) 选项。下面的示例显示了 `dosfstools` 软件包包含的文件路径：

```bash
# rpm -q1 dosfstools | less
/bin/dosfsck
/bin/fsck.msdos
/bin/fsck.vfat
/bin/mkdosfs
/bin/mkfs.msdos
/bin/mkfs.vfat
/usr/share/man/man8dosfsck.8.gz
```

你想要知道如何使用软件包中的组件吗？在查询时使用 `-d` 选项将显示软件包包含的文档（帮助页、README 文件、HOWTO 等）。如果你在让 X Window 系统正常运行方面遇到困难，可以使用以下命令行查找可能有所帮助的文档：

```bash
# rpm -qd xorg-x11 | less
/usr/X11R6/man/man1/Xark.ix.gz
/usr/X11R6/man/man1/Xorg.ix.gz
/usr/X11R6/man/man1/Xserver.ix.gz
/usr/X11R6/man/man1/appres.ix.gz
/usr/X11R6/man/man1/atomb.ix.gz
/usr/X11R6/man/man1/bitmap.ix.gz
/usr/X11R6/man/man1/bmtoa.ix.gz
```

许多软件包都有与其关联的配置文件。要查看与特定软件包关联的配置文件，请在查询时使用 `-c` 选项。例如，这是你输入的内容以查找用于 `ppp` 软件包的配置文件：

```bash
# rpm -qc p
/etc/logrotate.d/ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果你想知道某个命令或配置文件来自哪个软件包，可以使用 `-q` 选项。在下面的示例中，`-q` 选项显示 `chgrp` 命令来自 `fileutils` 软件包：

```bash
# rpm -qf /bin/chgrp
coreutils-5.97-11
```

在安装软件包之前，你可以对它进行与已安装软件包相同的查询。这对于查找软件包位于当前目录或软件存储库中的信息非常有用的工具。这里是使用 `-qp` 选项的示例——查看软件存储库中软件包的描述：

```bash
# rpm -q -i -
http://ayo.freshrpms.net/fedora/linux/1/i386/freshrpms/RPMS/blackbox-0.65.0-8.1.fcl.fr.i386.rpm
Name : blackbox          Relocations: (not relocatable)
Version : 0.65.0        Vendor : Freshrpms.net
Release : 8.1.fcl.fr    Build Date: 25 Mar 2004 12:45:45 PM PST
```

## 使用 rpm 验证软件包
