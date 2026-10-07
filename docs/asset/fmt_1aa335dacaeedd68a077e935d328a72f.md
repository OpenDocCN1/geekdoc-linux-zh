
```
D: installing binary packages
D: opening environment /var/lib/rpm/Packages joinenv
D: opening db index /var/lib/rpm/Packages create mode=0x42

D: closed db index /var/lib/rpm/Basenames
D: closed db index /var/lib/rpm/Name
D: closed db index /var/lib/rpm/Packages
D: closed db environment /var/lib/rpm/Packages
```

从这些输出中，你可以看到 `rpm` 在此归档中找到了一个二进制包，验证了校验和，打开 RPM 数据库，安装了包并在完成后关闭数据库。另一种验证安装是否实际生效的方法是使用 `-h` 选项，如下：

```
# rpm -Uvh RealPlayer-8.0-1.1386.rpm
RealPlayer #################
```

## 第 5 章：访问和运行应用程序

使用 `-h` 选项时，`rpm` 会连续输出 50 个哈希标记 `#`，直到包安装完成。如你所见，当一切顺利时，使用 `rpm` 安装非常简单。可能会发生一些问题，这里是其中几个：

- **软件包依赖关系错误** — 如果包需要安装额外的软件包才能正常工作，你将看到一个指出缺失包的错误。你应该在再次尝试安装你的包之前，先获取并安装该包。（你可以使用上述描述的安装选项覆盖失败，但我不建议这样做，因为没有该依赖包，你的包可能无法工作。）

- **非 root 用户错误** — 如果非 root 用户使用 `rpm`，命令将失败。输出将指示无法打开 `/var/lib/rpm` 数据库。请以 root 用户身份登录并重试。

### 使用 rpm 升级软件包 (-U)

`rpm` 的升级选项 `-U` 正如你预期的那样，也可以用于升级已有的软件包。我们上面使用的格式如下所示：

```
# rpm -U [options] package
```

> 提示：有一个独立的安装选项 `-i`，我建议无论你是在进行新安装还是升级都使用它。使用 `-U` 时，包在两种情况下都会安装。因此 `rpm -U` 总是有效的（有一个例外），而例外是如果包已经安装，`rpm -i` 将失败。

例外情况是你正在安装内核包时。在安装新内核或你（推测是正在使用的）内核时使用 `-U`，可能会导致旧内核被移除，你可能会导致系统无法启动！

升级时的一个问题是安装旧版本的软件包。例如，如果你安装了某个软件的新版本但它运行效果没那么好，你可能想回到旧版本。要做到这一点，你可以如下所示使用 `--oldpackage` 选项：

```
# rpm -U --oldpackage AnotherLevel-0.7.4-1.noarch.rpm
```

如果已存在此名称的后续包，它将被移除并安装旧版本。

### 使用 rpm 刷新软件包

与 `-U` 选项类似一个选项是刷新 `-F` 选项。两者之间的主要区别在于，如果你要更新或刷新的 RPM 尚未安装在你的 Fedora 上会发生什么。`-U` 可以执行全新安装或升级。而 `-F` 只执行升级（所以如果包尚未安装，`rpm -F` 将什么都不做）。

刷新的一个绝佳用处是，当你有一个包含 RPM 文件的完整目录，你想将其安装到系统中，但你只想更新那些已经安装的包。换句话说，目录中可能有很多你不需要的 RPM。刷新让你只需更新你已经拥有的包。

### 第二部分：使用 Fedora

假设你有一个包含 RPM 文件的完整目录，你想将它们安装到系统中，但你只想更新那些已经安装的包。换句话说，目录中可能有很多你需要的 RPM。刷新让你只需更新你已经拥有的包。为此使用：

```
# rpm -F *.rpm
```

### 使用 rpm 软件包

如果你想移除软件包，可以使用 `-e` 选项。在执行之前，你可能想通过以下方式检查哪些将被移除：

```
# rpm -qrequires
```

### 移除软件包

如果你对移除某个包感到担心，可以始终通过测试模式（test）运行命令。这会显示将要

```
# rpm -e --test package
```

### 第 5 章：访问和运行应用程序

在不实际卸载的情况下发生。（添加 `-vv` 选项以查看详情。）这是一个示例：

```
# rpm -evv --test pilot | less
D: opening environment /var/lib/rpm/Packages joinenv
D: opening db index /var/lib/rpm/Packages create mode=0x42
D: locked index /var/lib/rpm/Packages
D: opening db index /var/lib/rpm/Name readonly=0x0
D: closed db index /var/lib/rpm/Basenames
D: closed db index /var/lib/rpm/Name
D:  
```

如果结果看起来良好，你可以再次运行命令并去掉 `--test` 选项来移除包。

### 查询软件包

你可以使用 `rpm` 的查询选项 `-q` 来获取软件包信息。这可以是简单的列出已安装的包，也可以打印包的详细信息。这里是 `rpm` 查询命令的基本格式（至少需要一个选项）：

```
# rpm -q [options]
```

以下列表显示了用于 `rpm` 查询的一些有用选项：

- `-qa` — 列出所有安装的包。
- `-qf` — 显示拥有文件的包。（文件必须包含完整路径，否则 `rpm` 会假设在当前目录下。）
- `-qi package` — 显示关于包的大量信息。
- `-qR package` — 显示包依赖的组件（如库和命令）。
- `-ql package` — 列包包含的所有文件。
- `-qd package` — 显示包包含的所有文档文件。
- `-qe package` — 显示包包含的所有配置文件。
- `-qp [option] package` — 查询尚未安装的包。结合此选项与其他查询选项，允许你查询尚未安装的包。

要列出计算机上安装的所有包，请使用 `-q` 选项。因为这是一个长列表，你应该将输出通过到 `less`，或者可能使用 `grep` 查找你需要的包。以下命令显示了所有已安装的 RPM 包列表，然后

仅显示包含字符串 `xfree` 的名称。（`grep` 的 `-i` 选项用于忽略大小写。）

```
# rpm -qa | grep -i xorg
```

如果你对特定软件包的详细信息感兴趣，可以使用 `rpm -i` 查询选项。在下面的示例中，显示了关于 `dosfstools` 包（用于在 Linux 中处理 DOS 文件系统）的信息：

```
# rpm -qi dosfstools
```

| 名称 : dosfstools | 重位信息: (不可重定位) |

| :--- | :--- |

| 版本 : 2.8 | 供应商: Red Hat, Inc |

| 发布版本 : 5 | 构建日期: PST 2004年2月16日周二 下午02:59:38 |

| 安装日期: PST 2004年4月29日周四 下午02:15:35 | |

| 构建主机 : tweety.redhat.com | |

| 组 : Applications/System Source RPM:dosfstools-2.8-12.src.rpm | |

| 大小 : 70346 | 许可证: GPL |

| 签名 : DSA/SHA1, PST 2004年3月17日周三 上午11:48:55, Key ID da88cb4d30c9ec6f | |

| 打包员 : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla> | |

| 摘要 : 用于在 Linux 上创建和检查 MS-DOS FAT 文件系统的工具。 | |

描述

`dosfstools` 软件包包含 `mkdosfs` 和 `fsckdos` 实用，它们分别用于在硬盘或软盘上创建和检查 MS-DOS FAT 系统。

要查找软件包的内容，可以在查询时使用 `-l`（列出）选项。下面的示例显示了 `xpilot` 包中包含的文件完整路径名：

```
# rpm -ql dosfstools | less
/sbin/dosfck
/sbin/fsck.msdos
/sbin/fsck.vfat
/sbin/mkdosfs
/sbin/mkfs.msdos
/sbin/mkfs.vfat
/usr/share/man8/dosfck.8.gz
```

你想知道如何使用软件包中的组件吗？在查询时使用 `-d` 选项将显示软件包包含的文档（man 页面、README 文件、HOWTO 等）。如果你的 Windows 系统运行不正常遇到问题，可以使用以下命令行来查找可能有帮助的文档：

```
# rpm -qd xorg-x11 | less
/usr/X11R6/man/man1/mark.ix.gz
/usr/X11R6/man/man1/Xorg.ix.gz
```

```
/usr/X11R6/man/man1/Xserver.lx.gz
/usr/X11R6/man/man1/appres.lx.gz
/usr/X11R6/man/man1/atobm.lx.gz
/usr/X11R6/man/man1/bitmap.lx.gz
/usr/X11R6/man/man1/bmtoa.lx.gz
```

许多软件包都有与其相关的配置文件。要查看与特定软件包关联的配置文件，请在查询时使用 `-c` 选项。例如，你将输入以下内容来查找与 `ppp` 包一起使用的配置文件：

```
rpm -qc ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果你想知道某个特定命令或配置文件来自哪个软件包，可以使用 `-qf` 选项。在下面的示例中，`-qf` 选项显示 `chgrp` 命令源自 `fileutils` 软件包：

```
rpm -qf /bin/chgrp
fileutils-4.1-4
```

在安装软件包之前，你可以对它执行与对已安装软件包相同的查询。这对于查找位于当前目录甚至软件存储库中的软件包信息来说，是一个非常棒的工具。以下是一个使用 `-qp -i` 选项查看软件库中软件包描述的示例：

```
rpm -qp -i \
http://ayco.freshrpmps.net/fedora/linux/i386/freshrpmps/RPMS/blackbox-0.65.0-8.1.fcl1.i386.rpm
```

| | blackbox | 重位信息: (不可重定位) |

| :--- | :--- | :--- |

| 版本 | 0.65.0 | 供应商: Freshrpmps.net |

| 发布版本 | 8.1.fcl1 | 构建日期: PST 2004年3月25日周四 下午12:45:45 |

| 安装日期: | (未安装) | 构建主机: python2.freshrpmps.net |

Blackbox 是 X Window 环境的一个窗口管理器，它是一个……

在上一个示例中，显示的三行显示的命令行实际上应该在一行内输入。如果你担心下载软件包的内容或合法性，此示例是在下载软件包之前阅读其描述的方法。
