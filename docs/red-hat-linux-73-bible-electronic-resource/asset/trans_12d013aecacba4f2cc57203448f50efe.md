

验证安装确实生效的另一种方法是添加 `-h` 选项，如下例所示：

```
# rpm -ivh audiofile-devel-0.2.1-2.i386.rpm
audiofile-devel ###################################################
```

使用 `-h` 选项时，rpm 会持续输出 50 个井号（#），直到软件包安装完成。如您所见，当一切顺利时，使用 rpm 进行安装非常简单。然而，有时也会出现问题。以下是其中几种情况：

- **软件包依赖错误** — 如果您正在安装的软件包需要额外的软件包才能正常工作，您将看到一个指出缺少该软件包的错误信息。在再次尝试您的软件包之前，您应该获取并安装该缺失的软件包。（您可以使用上述安装选项来覆盖此失败情况，但我不推荐这样做，因为如果缺少依赖软件包，您的软件包可能无法正常工作。）
- **非 root 用户错误** — 如果由非 root 用户运行 rpm `-i`，该命令将失败。输出将指示无法打开 `/var/lib/rpm` 数据库。请以 root 用户身份登录并重新尝试。

## 使用 rpm 升级软件包

rpm 的升级选项（-U）的行为与安装选项非常相似。不同之处在于，它在安装软件包的新版本之前会卸载旧版本。格式如下：

```
# rpm -U [options] package
```

> **提示：** 无论您是在执行新安装还是升级，都可以使用 `-U` 选项。使用 `-U` 时，软件包在这两种情况下都会安装。因此，rpm `-U` 总是有效，而如果软件包已安装，rpm `-i` 将会失败。

升级时的一个问题是安装软件包的较旧版本。例如，如果您安装了某个软件的新版本但其表现不如预期，您可能希望回退到旧版本。为此，您可以按以下方式使用 `--oldpackage` 选项：

```
# rpm -U --oldpackage AnotherLevel-0.7.4-1.noarch.rpm
```

如果该软件名称的较新软件包已存在，它将被移除，并安装较旧版本。

## 使用 rpm 移除软件包

如果您不再需要某个软件包（或者只是想回收一些磁盘空间），请使用 `-e` 选项来移除该软件包。在最简单的形式中，您按以下方式使用 rpm 和 `-e` 选项：

```
# rpm -e package
```

如果该软件包没有依赖项，它将被静默移除。然而，在移除软件包之前，您可能想要快速检查一下依赖项。`-q` 选项用于多种查询选项。（检查依赖项并非必要，因为 rpm 在移除软件包前会检查依赖项。但为了获取信息，您可能仍希望这样做。）要检查依赖项，请执行以下操作：

```
# rpm -q --whatrequires package
```

如果您决定移除该软件包，我建议在使用 `rpm -e` 时加上 `-vv` 选项。这让您可以看到实际被移除的文件。我还建议您将输出重定向到文件或通过管道传递给 `more`，因为输出可能会超出屏幕范围。以下是一个示例：

```
# rpm -evv xpi | more
```

此示例移除了 `xpi` 软件包，并逐页向您显示被移除的文件。（按空格键翻页查看输出。）

与 `rpm -e` 配合使用的其他选项可用于覆盖那些会阻止软件包移除的条件，或阻止某些处理（例如不运行 preuninstall 和 postuninstall 脚本）。其中三个选项如下：

- `--nodeps` — 卸载软件包时不检查依赖项。
- `--noscripts` — 卸载软件包时不运行任何 preuninstall 或 postuninstall 脚本。
- `--notriggers` — 卸载软件包时不执行由移除该软件包触发的脚本。

如果您担心**大胆地**移除软件包，总可以在执行真正的卸载之前以测试模式（`--test`）运行卸载操作。测试模式向您展示卸载过程中会发生的一切，但实际不会执行卸载。（添加 `--vv` 选项以查看详细信息。）以下是一个示例：

```
# rpm -evv --test xpi | more
D: counting packages to uninstall
D: opening database in /var/lib/rpm/
D: found 1 packages to uninstall
D: uninstalling record number 4545368
D: will remove files test = 1
D: /usr/share/doc/xpi-4.3.2-1/doc/man/xpis.man.msub - removing
D: /usr/share/doc/xpi-4.3.2-1/doc/man/xpis.man - removing
.
.
.
D: /etc/X11/wmconfig/xpi - removing
D: removing database entry
```

如果结果看起来正常，您可以再次运行该命令，但不加 `--test` 选项，以移除该软件包。

## 使用 rpm 查询软件包

使用 `rpm` 的查询选项（`-q`），您可以获取有关 RPM 软件包的信息。这可以简单地是列出已安装的软件包，或者打印软件包的详细信息。以下是 `rpm` 查询命令的基本格式（至少需要一个选项）：

```
# rpm -q [options]
```

以下是一些可用于 `rpm` 查询的有用选项：

- `-qa` — 列出所有已安装的软件包。
- `-qf file` — 列出拥有 `file` 的软件包。（该文件必须包含完整的路径名，否则 `rpm` 将假设当前目录。）
- `-qi package` — 列出关于 `package` 的大量信息。
- `-qR package` — 列出 `package` 所依赖的组件（如库和命令）。
- `-ql package` — 列出包含在 `package` 中的所有文件。
- `-qd package` — 列出随 `package` 提供的所有文档文件。
- `-qc package` — 列出随 `package` 提供的所有配置文件。

要列出计算机上安装的所有软件包，请使用 `-a` 查询选项。由于这是一个很长的列表，您应该将输出通过管道传递给 `more`，或者可能使用 `grep` 来查找您需要的软件包。以下命令行显示所有已安装的 RPM 软件包列表，然后仅显示名称中包含字符字符串 `xfree` 的那些软件包。（`grep` 的 `-i` 选项表示忽略大小写。）

```
# rpm -qa | grep -i xfree
```

如果您对特定软件包的详情感兴趣，可以使用 `rpm -qi` 查询选项。在以下示例中，显示了关于 `dosfstools` 软件包（用于在 Linux 中处理 DOS 文件系统）的信息：

```
# rpm -qi dosfstools
Name        : dosfstools    Relocations: (not relocatable)
Version     : 2.8           Vendor: Red Hat, Inc.
Release     : 1            Build Date: Fri 06 Jul 2001 08:29:15 AM PDT
Install date: Fri 05 Apr 2002 12:42:28 PM PDT  Build Host: redhat.com
Group       : Applications/System  Source RPM: dosfstools-2.8-1.src.rpm
Size        : 67734         License: GPL
Packager    : Red Hat, Inc. <bugzilla.redhat.com/bugzilla>
Summary     : Utilities to make/check MS-DOS FAT filesystems on Linux.
Description :
```

`dosfstools` 软件包包含 `mkdosfs` 和 `dosfsck` 实用工具，它们分别在硬盘或软盘上创建和检查 MS-DOS FAT 文件系统。

若要了解软件包内容的更多详情，您可以在查询时使用 `-l`（list）选项。以下示例显示了 `xpiilot` 软件包中包含的文件的完整路径名：

```
# rpm -ql xpiilot | more
/etc/X11/wmconfig/xpiilot
/etc/X11/wmconfig/xpiilots
/usr/X11R6/bin/xp-replay
/usr/X11R6/bin/xpiilot
...
```

您想知道如何使用软件包中的组件吗？在查询时使用 `-d` 选项将显示随软件包提供的文档（手册页、README 文件、HOWTO 等）。如果您在让 X Window 系统正常运行时遇到困难，可以使用以下命令行查找可能有帮助的文档：

```
# rpm -qd XF8686 | more
/usr/X11R6/man/man1/editres.1x.gz
/usr/X11R6/man/man1/iceauth.1x.gz
/usr/X11R6/man/man1/lbxproxy.1x.gz
/usr/X11R6/man/man1/libxrx.1x.gz
/usr/X11R6/man/man1/lsdir.1x.gz
/usr/X11R6/man/man1/makedepend.1x.gz
/usr/X11R6/man/man1/makespres.1x.gz
/usr/X11R6/man/man1/makesstrs.1x.gz
/usr/X11R6/man/man1/mkcfm.1x.gz
...
```

许多软件包都有相关的配置文件。若要查看与特定软件包关联的配置文件，请在查询时使用 `-c` 选项。例如，若要查看与 `ppp` 软件包一起使用的配置文件，您会输入：

```
# rpm -qc ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果您想知道某个特定命令或配置文件来自哪个软件包，可以使用 `-qf` 选项。在以下示例中，`-qf` 选项显示 `chgrp` 命令来自 `fileutils` 软件包：

