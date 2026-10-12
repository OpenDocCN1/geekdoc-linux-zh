
`--whatrequires` 选项是 `--whatprovides` 选项的逻辑补集。它用于显示哪些软件包需要指定的能力。正如我们开始的示例所示：

```
# rpm -q --whatrequires kernel
kernel-0.18-5
```

## 5.2 查询命令，第二部分

在指定了想要查询的软件包（或软件包）后，如果你想获取更详细的信息，有几个选项可以进一步探索。虽然挖掘系统中已安装软件包的信息确实非常有用，但那些尚未安装的软件包呢？`-p` 选项可以为你完成任务。在这种情况下，我们将探索这些选项：

### -i — 显示软件包信息

在 `rpm -q` 后面添加 `-i` 会让 RPM 显示所选软件包的信息。正如你可能注意到的，这提供了很多信息。为了清晰起见，我们来看看它包含的软件包信息：

```
# rpm -qi
Name         : rpm
Distribution: Red Hat
Version      : 2.3
Release      : 1
Build Date   : Tue Dec 24 09:07:59 1996
Vendor       : Red Hat Software
Group        : Utilities/System
Source RPM   : rpm-2.3-1
Size         : 63157
Summary      : RPM
Description  : RPM 是一个强大的软件包管理器，用于构建、安装、查询和卸载软件包。
```

将 `-i` 选项及其后的能力添加到查询命令中，RPM 将选择提供该信息的软件包。这里有一个示例：

```
# rpm -qi rpm
```

软件包的构建包含以下内容：

- Name         : rpm
- Distribution: Red Hat
- Version      : 2.3
- Release      : 1
- Build Date   : Tue Dec 24 09:07:59 1996
- Vendor       : Red Hat Software
- Group        : Utilities/System
- Source RPM   : rpm-2.3-1
- Size         : 63157
- Summary      : RPM
- Description  : RPM 是一个强大的软件包管理器，用于构建、安装、查询和卸载软件包。

使用 `-i` 选项还可以使用统一资源定位符（URL）来指定软件包文件。有关使用 URL 的更多信息，请参见第 17 页第 2.2.1 节。

`-i` 还有一个最后的杀手锏 —— 它还可以通过从标准输入读取软件包来执行查询。这里有一个示例：

```
# cat bother-3.5-1.4386.rpm | rpm -qi
```

我们将 `cat` 的输出通过管道交给 RPM。命令行末尾的连字符 `-` 引导 RPM 从标准输入读取软件包。

### -l — 显示软件包的文件列表

将 `-l` 添加到 `rpm -q` 后会让 RPM 显示由指定软件包或软件包安装的文件列表。如果你以前用过 `ls`，你不会对 RPM 的文件列表感到惊讶。这里是 Red Hat Linux 上一个较小的软件包示例 — `adduser`：

```
# rpm -ql adduser
/usr/sbin/adduser
#
```

`adduser` 软件包只包含一个文件，所以只有一个文件名显示。

## 5.2 RPM 查询的组成部分

### -v 显示额外信息

在某些情况下，可以在查询中添加 `-v` 选项以获取额外信息。我们一直在讨论的 `-v` 选项就是此类情况的一个例子。注意 `-v` 选项是如何增加输出详细程度的。

```
# rpm -glv adduser
-rwxr-xr-x- root root 3894 Feb 25 13:45 /usr/sbin/adduser
#
```

这看起来像 `ls` 的输出，不是吗？外往往具有欺骗性。你在这里看到的所有内容都直接来自 RPM 数据库。然而，它的格式与 `ls` 相同，因此很容易理解。如果你觉得这看起来像天书，请查阅 `ls` 的 man 页。

### -c 显示软件包的配置文件列表

当在 `rpm -c` 命令中添加 `-c` 时，RPM 将显示指定软件包或多个软件包包含的配置文件。正如书在前面提到的，配置文件非常重要，因为它们控制着被封装软件的行为。让我们来看 XFree86 的配置文件列表：

```
# rpm -qc XFree86
/etc/X11/fs/config
/etc/X11/twm/system.tmrc
/etc/X11/xdm/GiveConsole
/etc/X11/xdm/TakeConsole
/etc/X11/xdm/Xaccess
/etc/X11/xdm/Xresources
/etc/X11/xdm/Xservers
/etc/X11/xdm/Xsession
/etc/X11/xdm/Xsetup.0
/etc/X11/xdm/chooser
/etc/X11/xdm/xdm-config
/etc/X11/xinit/xinitrc
/etc/X11/xsm/system.xsm
/usr/X11R6/lib/X11/XF86Config
#
```

如果你想根据特定需求定制 XFree86，这些就是你首先想要查看的文件。就像 `-l` 一样，你可以添加 `-v` 来获取更多信息：

```
# rpm -qcu XFree86
-r--r--r-- root root 423 Mar 21 00:17 /etc/X11/fs/config

rwxrxrwx- root root 30 Mar 21 00:29 /usr/X11R6/lib/X11/XF86Config
-> ../../../etc/X11/XF86Config
#
```

（注意最后一个文件：RPM 也会显示符号链接。）

### -d — 显示软件包文档列表

当在查询中添加 `-d` 时，我们得到一个包含命名软件包或多个软件包文档的所有文件列表。当你在使用熟悉的软件遇到问题时，这是一个快速进入状态的好方法。和 `-c` 以及 `-l` 一样，你将看到文件名简单列表，或者（如果你添加了 `-v`）更全面的列表。这里有一个初看起来可能望而却畏的示例，其实并不如此：

```
# rpm -qdcf /sbin/dump
/etc/dumpdates
/usr/doc/dump-0.3-5
/usr/doc/dump-0.3-5/CHANGES
/usr/doc/dump-0.3-5/COPYRIGHT
/usr/doc/dump-0.3-5/INSTALL
/usr/doc/dump-0.3-5/KNOWNBUGS
/usr/doc/dump-0.3-5/THANKS
/usr/doc/dump-0.3-5/dump.0.3.announce
/usr/doc/dump-0.3-5/dump.lsm
/usr/doc/dump-0.3-5/linux-1.2.patch
/usr/doc/man8/dump.8
/usr/doc/man8/rdump.8
/usr/doc/man8/restore.8
/usr/doc/man8/rmt.8
#
```

让我们逐个查看这些字母的选项：

- `q` — 执行查询。
- `d` — 列出所有文档文件。
- `c` — 列出所有配置文件。
- `f` — 查询拥有指定文件（在本例中为 `/sbin/dump`）的软件包。文件列表代表了该文件的文档和配置文件。

### -s — 显示软件包中每个文件的状态

与处理某种类型文件列表之前的章节不同，`-s` 查询将列出组成软件包的文件的*状态*。听起来就像在问：“文件的状态是什么？”对于 RPM 安装的每个文件，都有一个关联的状态。共有四种可能的状态：

1. normal（正常）——正常状态的文件没有被另一个软件包修改。
2. replaced（已替换）——替换状态的文件被另一个软件包修改过。
3. not installed（未安装）——文件被归类为未安装！这种状态通常在软件包部分安装时看到。使用 `--excluded` 选项是部分安装软件包的示例。RPM 数据库仍然包含这些文件的条目，但它们的状态为未安装。
4. net shared（网络共享）——共享状态用于支持从服务器挂载文件的系统。如果软件包将文件导出到多个客户端，共享状态将提醒 RPM 文件系统上的文件不应删除。当发生以下情况时，文件处于共享状态：
   - (a) 共享条目值发生了变化。
   - (b) 文件要在目录下安装。

这是一个显示状态如何出现的示例：

```
# rpm -qs adduser
normal /usr/sbin/adduser
#
```

（行首的 normal 是状态，后面是文件名）状态是 RPM 在安装或删除软件包时确定最合适操作的工具之一。现在普通人需要检查状态吗？并不需要。但如果有问题，这种信息可以帮助重回正轨。

## --provides 显示软件包提供的内容
