

## 5.2.2.4. -c：显示包的配置文件列表

当在 `rpm -q` 命令中添加 `-c` 时，RPM 将显示指定包中包含的配置文件。正如本书前文所述，配置文件非常重要，因为它们控制着打包软件的行为。让我们来看看 XFree86 的配置文件列表：

```
# rpm -qc XFree86
/etc/X11/fs/config
/etc/X11/twm/system.twmrc
/etc/X11/xdm/GIveConsole
/etc/X11/xdm/TakeConsole
/etc/X11/xdm/Xaccess
/etc/X11/xdm/Xresources
/etc/X11/xdm/Xservers
/etc/X11/xdm/Xsession
/etc/X11/xdm/Xsetup 0
/etc/X11/xdm/chooser
/etc/X11/xdm/xdm-config
/etc/X11/xinit/xinitrc
/etc/X11/xsm/system.xsm
/usr/X11R6/lib/X11/XF86Config
#
```

这些是你想要自定义 XFree86 以满足特定需求时首先应该查看的文件。就像 `-l` 一样，我们还可以添加 `v` 以获取更多信息：

```
# rpm -qcv XFree86
-r--r--r- root root 423 Mar 21 00:17 /etc/X11/fs/config
....
lrw-  root root 30 Mar 21 00:29 /usr/X11R6/lib/X11/XF86Config
-> ../.../.../etc/X11/XF86Config
#
```

注意最后一个文件：RPM 也会显示符号链接。

## 5.2.2.5. -d：显示包的文档列表

当在查询命令中添加 `-d` 时，我们将获得指定包中包含的所有文档文件列表。当你遇到不熟悉软件的问题时，这是快速了解该软件的绝佳方式。与 `-c` 和 `-l` 一样，你会看到一个简单的文件名列表，或者（如果你添加了 `-v`）一个更全面的列表。下面是一个示例，乍一看可能令人望而生畏，但其实并非如此：

```
# rpm -qdcf /sbin/dump
/etc/dumpsdates
/usr/doc/dump-0.3-5
/usr/doc/dump-0.3-5/CHANGES
/usr/doc/dump-0.3-5/COPYRIGHT
/usr/doc/dump-0.3-5/INSTALL
/usr/doc/dump-0.3-5/KNOWNBUGS
/usr/doc/dump-0.3-5/THANKS
/usr/doc/dump-0.3-5/dump-0.3.announce
/usr/doc/dump-0.3-5/dump.lsm
/usr/doc/dump-0.3-5/linux-1.2.x.patch
/usr/man/man8/dump.8
/usr/man/man8/rdump.8
/usr/man/man8/restore.8
/usr/man/man8/rmt.8
/usr/man/man8/rrestore.8
#
```

让我们逐一解析这串字母汤般的选项：

- `- q`——执行查询。
- `- d`——列出所有文档文件。
- `- c`——列出所有配置文件。
- `- f`——查询拥有指定文件（在此情况下为 `/sbin/dump`）的包。

文件列表代表适用于拥有 `/sbin/dump` 文件的所有文档和配置文件。

## 5.2.2.6. -s：显示包中每个文件的状态

与过去三个讨论某类文件列表的章节不同，在查询命令中添加 `-s` 将列出组成一个或多个包的每个文件的状态。我能听到你在问：“文件的状态是什么？”对于 RPM 安装的每个文件，都有一个关联的状态。有四种可能的状态：

- `- normal`——处于正常状态的文件未因在系统上安装了其他包而修改。
- `- replaced`——处于已替换状态的文件因在系统上安装了其他包而修改。
- `- not installed`——当文件未被安装时，它被分类为未安装。通常只有在包部分安装时才会看到此状态。部分安装包的一个例子是使用 `--excludedocs` 选项安装的包。使用此选项时，不会安装任何文档文件。RPM 数据库仍将包含这些缺失文件的条目，但它们的状态将为未安装。
- `- net shared`——网络共享状态用于提醒 RPM 该文件位于共享文件系统中，且不应被删除。当多台计算机使用 NFS 挂载同一文件系统时就会发生这种情况。如果一台计算机删除了包含共享文件系统文件的包，那么共享该文件系统的其他计算机将只有该被删包的未完成副本。当以下两种情况发生时，文件将处于网络共享状态：
    - `rpmrc` 文件中的 `netsharedpath` 条目已从默认值（null）更改。
    - 文件将被安装在网络共享路径内的目录中。

下面是一个显示文件状态示例：

```
# rpm -qs adduser
normal /usr/sbin/adduser
#
```

行首的 `normal` 是状态，后面跟着文件名。

文件状态是 RPM 用于决定在包安装或删除时采取最适当措施的工具之一。

普通人需要检查文件状态吗？其实并不需要。但如果出现问题，这类信息有助于使系统恢复正常轨道。

## 5.2.2.7. --provides：显示包提供的功能

通过在查询命令中添加 `--provides`，你可以查看一个或多个包提供的功能。如果包未提供功能，`--provides` 选项将没有输出：

```
# rpm -q --provides rpm
#
```

然而，如果包确实提供功能，它们将被显示出来：

```
# rpm -q --provides foonly
index
#
```

重要的是要记住，功能并不是文件名。在上例中，foonly 包不包含名为 `index` 的文件；它只是打包者选择一个字符串。这与下面的示例并无不同：

```
# rpm -q --provides libc
libm.so.5
libc.so.5
#
```

虽然 /lib 中可能存在名为这些名字的符号链接，但功能是包的属性，而不是包中包含的文件！

## 5.2.2.8. --requires：显示包所需的功能

`--requires` 选项（-R 等效）是 `--provides` 选项的逻辑互补。它显示指定包所需的功能。如果包没有依赖项，则没有输出（或在较新版本的 RPM 中，显示单词 `none`）：

```
# rpm -q --requires adduser
#
```

在有依赖项的情况下，它们如下显示：

```
# rpm -q --requires rpm
libz.so.1
libdb.so.2
libc.so.5
#
```

你也有可能遇到像这样的情况：

```
# rpm -q --requires blather
blather >= 3.1
#
```

包也可以构建为需要另一个包。此需求还可以包括特定版本。在前面的例子中，**blather** 包被 **blather**（具体而言，是版本大于或等于 3.1 的 **blather**）所需要。

这里有件值得理解的事情。假设我们决定追踪 **blather** 声称其需要的 **blather**。如果我们使用 RPM 的查询功能，可以使用 **--whatprovides** 包选择选项来尝试找到它：

```
# rpm -q --whatprovides blather
no package provides blather
#
```

未果。这可能会让你认为 **blather** 包存在问题。这个故事的道理是，当试图找出哪个包满足另一个包的需求时，使用需求作为包名进行简单查询也是一个好主意。继续我们之前的例子，让我们看看是否有名为 **blather** 的包：

```
# rpm -q blather
blather-3.5-1
#
```

命中目标！然而，如果我们查看 **blather** 包提供的功能，却一无所获：

```
# rpm -q --provides blather
#
```

没有输出的原因是，默认情况下，所有包都会提供其包名（和版本）。

## 5.2.2.9. --dump：显示每个文件的所有可验证信息

**--dump** 选项用于显示 RPM 在其数据库中关于一个或多个文件的每项信息。信息以非常简洁的方式列出。由于 **--dump** 选项显示与文件相关的信息，必须使用 **-l**、**-c** 或 **-d** 选项（或其某种组合）来选择文件列表：

```
# rpm -ql --dump adduser
/usr/sbin/adduser 4442 84103888 ca5fa53dc74952aa5b5e3a5fa5d8904b 0100755
root root 0 0 0 X
#
```

