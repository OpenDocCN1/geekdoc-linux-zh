
假设你下载了一个 RPM 目录，并且想要有选择地更新已安装的那些包。将 RPM 目录作为当前目录，你可以输入：

```bash
# rpm -Fhv *.rpm
```

已安装的软件包将使用新的 RPM 进行更新。所有其他 RPM 将被跳过。

### 使用 rpm 移除软件包

如果你不再想使用某个软件包（或者只是想回收一些磁盘空间），请使用 `-e` 选项来移除它。在最简单的形式中，你可以像下面这样结合 `-e` 选项使用 `rpm`：

```bash
# rpm -e package
```

如果没有其他包依赖此包，它将被静默移除。不过，在移除软件包之前，你可能想快速检查一下依赖关系。`-q` 选项用于各种查询选项。（检查依赖关系并非必要，因为 `rpm` 在移除软件包前会检查依赖关系。不过，你可能想为了自己的了解而这样做。）要检查依赖关系，请执行以下操作：

```bash
# rpm -q --whatrequires package
```

如果你决定移除该软件包，我建议结合 `rpm -e` 使用 `-vv` 选项。这能让你看到实际被移除的文件。我还建议你将输出重定向到文件或通过管道传给 `more`，因为输出经常会超出屏幕。例如：

```bash
# rpm -evv jpilot | more
```

此示例移除 `jpilot` 软件包，并逐页显示被移除的文件。（按空格键翻页查看输出。）

可以与 `rpm -e` 一起运行的其他选项可用于覆盖阻止软件包被移除的条件，或防止某些处理（例如不运行预卸载和后卸载脚本）。其中三个选项如下：

- **--nodeps** — 在不检查依赖关系的情况下卸载软件包。
- **--noscripts** — 在不运行任何预卸载或后卸载脚本的情况下卸载软件包。
- **--notriggers** — 在不执行由移除软件包触发的脚本的情况下卸载软件包。

如果你对大胆移除软件包感到紧张，可以在真正卸载前先以测试模式 (`--test`) 运行卸载。测试模式会显示卸载过程中会发生的一切，但不会实际卸载。（添加 `-vv` 选项可查看详细信息。）示例如下：

```bash
# rpm -evv --test jpilot | more
D: opening db environment /var/lib/rpm/Packages joinenv
D: opening  db index   /var/lib/rpm/Packages rdonly mode=0x0
D: locked   db index   /var/lib/rpm/Packages
D: opening  db index   /var/lib/rpm/Name rdonly mode=0x0
D: opening  db index   /var/lib/rpm/Pubkeys rdonly mode=0x0
...
D: closed   db index   /var/lib/rpm/Name
D: closed   db index   /var/lib/rpm/Packages
D: closed   db environment /var/lib/rpm/Packages
```

如果结果看起来没问题，你可以再次运行该命令，去掉 `--test` 选项，从而移除该软件包。

### 使用 rpm 查询软件包

使用 `rpm` 的查询选项 (`-q`)，你可以获取关于 RPM 软件包的信息。这可以是简单地列出已安装的软件包，也可以是打印关于某个软件包的详细信息。以下是 `rpm` 查询命令的基本格式（至少需要一个选项）：

```bash
# rpm -q [options]
```

以下是一些可用于 `rpm` 查询的有用选项：

- `-qa` — 列出所有已安装的软件包。
- `-qf file` — 列出拥有 `file` 的软件包。（文件必须包含完整路径名，否则 `rpm` 会假设为当前目录。）
- `-qi package` — 列出关于软件包的大量信息。
- `-qR package` — 列出 `package` 所依赖的组件（如库和命令）。
- `-ql package` — 列出 `package` 中包含的所有文件。
- `-qd package` — 列出 `package` 中附带的所有文档文件。
- `-qc package` — 列出 `package` 中附带的所有配置文件。

要列出计算机上安装的所有软件包，请使用 `-a` 查询选项。因为列表很长，你应该将输出通过管道传给 `more`，或者可能使用 `grep` 来查找你想要的软件包。以下命令行显示所有已安装 RPM 软件包的列表，然后只显示包含字符串 `xfree` 的名称。（`grep` 的 `-i` 选项表示忽略大小写。）

```bash
# rpm -qa | grep -i xfree
```

如果你对某个特定软件包的详细信息感兴趣，可以使用 `rpm -qi` 查询选项。在下面的示例中，显示了关于 `dosfstools` 软件包（用于在 Linux 中处理 DOS 文件系统）的信息：

```bash
# rpm -qi dosfstools
Name    : dosfstools           Relocations: (not relocatable)
```

| 键 | 值 |
|-----|-------|
| 版本 | 2.8 |
| 供应商 | Red Hat, Inc. |
| 发行版本 | 5 |
| 构建日期 | Tue 18 Feb 2003 11:08:21 PM PST |
| 安装日期 | Sat 09 Aug 2003 02:15:35 PM PST |
| 构建主机 | daffy.perf.redhat.com |
| 组 | Applications/System |
| 源 RPM | dosfstools-2.8-6.src.rpm |
| 大小 | 73278 |
| 许可证 | GPL |
| 签名 | (none) |
| 打包者 | Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla> |
| 摘要 | 用于在 Linux 上创建和检查 MS-DOS FAT 文件系统的实用程序。 |
| 描述 | dosfstools 软件包包含 mkdosfs 和 dosfsck 实用程序，分别用于在硬盘或软盘上创建和检查 MS-DOS FAT 文件系统。 |

要了解软件包的内容，可以在查询中使用 `-l`（列表）选项。以下示例显示 `dosfstools` 软件包中包含的文件的完整路径名：

```bash
# rpm -ql dosfstools | more
/sbin/dosfsck
/sbin/fsck.msdos
/sbin/fsck.vfat
/sbin/mkdosfs
/sbin/mkfs.msdos
/sbin/mkfs.vfat
/usr/share/man/man8/dosfsck.8.gz
```

想知道如何使用软件包中的组件吗？在查询中使用 `-d` 选项将显示随软件包附带的文档（手册页、README 文件、HOWTO 等）。如果你在让 X Window System 正常运行方面遇到麻烦，可以使用以下命令行查找可能有帮助的文档：

```bash
# rpm -qd XFree86 | more
/usr/X11R6/man/man1/XFree86.1x.gz
/usr/X11R6/man/man1/Xmark.1x.gz
/usr/X11R6/man/man1/Xserver.1x.gz
/usr/X11R6/man/man1/appres.1x.gz
/usr/X11R6/man/man1/atobm.1x.gz
/usr/X11R6/man/man1/bdfptofc.f.1x.gz
```

许多软件包都有与之关联的配置文件。要查看与特定软件包关联的配置文件，请在查询中使用 `-c` 选项。例如，要查找与 `ppp` 软件包一起使用的配置文件，你可以输入：

```bash
# rpm -qc ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果你想知道某个特定命令或配置文件来自哪个软件包，可以使用 `-qf` 选项。在下面的示例中，`-qf` 选项显示 `chgrp` 命令来自 `fileutils` 软件包：

```bash
# rpm -qf /bin/chgrp
fileutils-4.1-4
```

### 使用 rpm 验证软件包

如果软件包中的某些内容工作不正常，或者你怀疑系统被篡改过，rpm 的验证 (`-V`) 选项可以帮助你将已安装的软件与其原始软件包进行对比验证。关于每个已安装软件包的信息存储在你计算机上的 RPM 数据库中。通过使用验证选项，你可以检查软件包中的组件是否发生了任何更改。

> **注意：** 验证选项使用大写字母 (`-V`)，而详细选项使用小写字母 (`-v`)。

验证操作期间会进行各种文件大小和权限测试。如果一切正常，则没有输出。自安装以来发生变化的任何组件将被打印出来，并附带指示其如何变化的信息。示例如下：

```bash
# rpm -V ppp
S.5...T c /etc/ppp/chap-secrets
S.5...T c /etc/ppp/options
S.5...T c /etc/ppp/pap-secrets
```

此输出显示 `ppp` 软件包（用于拨号连接 TCP/IP 网络，如互联网）自安装以来有三个文件发生了变化。开头的标记显示文件大小 (S)、MD5 校验和 (5) 和修改时间 (T) 都已更改。字母 `c` 表明这些都是配置文件。通过查看这些文件，确认更改只是我为使 PPP 工作而做的更改，我可以验证软件是正常的。

当你验证配置文件内容时，可能会看到的指示符如下：

- **5** — MD5 校验和 — MD5 校验和表示文件内容已更改。
- **S** — 文件大小 — 文件中的字符数已更改。
- **L** — 符号链接 — 该文件已成为指向另一个文件的符号链接。
- **T** — 修改时间 — 文件的修改时间已更改。
- **D** — 设备 — 该文件已成为设备特殊文件。
