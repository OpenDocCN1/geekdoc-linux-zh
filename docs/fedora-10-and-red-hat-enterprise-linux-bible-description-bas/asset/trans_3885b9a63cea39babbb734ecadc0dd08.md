

# 第二部分：使用 Fedora RHEL

已安装。换句话说，你所在的目录中可能有很多你不需要的 RPM 包。Freshen 命令允许你更新已经安装的软件包。

假设你下载了一个包含 RPM 包的目录，并想要选择性地更新你已经安装的包。以该 RPM 目录为当前目录，你可以输入：

```
# rpm -Fv * *.rpm
```

已安装的软件包将用新的 RPM 包更新。所有其他 RPM 包将被跳过。

> 警告：再次提醒，你不应该刷新（freshen）或升级内核包，因为在你添加新内核时，可能会导致你唯一运行的内核被移除。

## 使用 rpm 移除软件包

如果你不再需要某个软件包（或只是想恢复一些磁盘空间），请使用 -e 选项来移除软件包。在最简单的情况下，你如下所示使用带有 -e 选项的 rpm：

```
# rpm -e package
```

如果该包没有依赖项，它将被静默删除。在移除软件包之前，你可能想快速快速检查一下依赖关系。-q 选项用于各种查询。（检查依赖关系并不是必要的，因为 rpm 在移除软件包之前会检查依赖关系。你可能为了自己的信息需要这样做：--whatrequires。）要检查依赖关系，执行以下命令：

```
# rpm -q --whatrequires package
```

如果你决定移除该软件包，我建议在 rpm -e 中使用 -vv 选项。这让你让你看到正在被移除的文件。我建议将输出重定向到文件，或者至少使用 less 命令让输出不在屏幕上滚动。例如：

```
# rpm -evv jpilot | less
```

此示例移除了 jpilot 软件包，并逐页显示正在被移除的文件。（按空格键翻页输出。）

配合 rpm -e 使用的其他选项可以用于覆盖阻止软件包移除的条件，或阻止某些处理（例如不运行安装前或安装后脚本）。其中三个如下：

- --nodeps -- 在不检查依赖关系的情况下卸载软件包
- --noscripts -- 在不运行任何安装前或安装后脚本的情况下卸载软件包
- --notriggers -- 在不执行由移除包所触发的脚本的情况下卸载软件包

## 第五章：访问和运行应用程序

如果你对大胆移除某个软件包感到紧张，可以在执行实际卸载之前运行测试模式下的卸载（--test）。测试模式会显示卸载时会发生的一切，但不会实际卸载。（添加 --vv 选项可以查看详情）。这是一个示例：

```
# rpm -evv --test | less
D: opening db environment /var/lib/rpm/Packages joinenv
D: opening db index /var/lib/rpm/Packages rdonly mode=0x0
D: locked db index /var/lib/rpm/Packages rdonly mode=0x0
D: opening db index /var/lib/rpm/Name rdonly mode=0x0
D: opening db index /var/lib/rpm/Pubkeys rdonly mode=0x0

D: closed db index /var/lib/rpm/Name
D: closed db index /var/lib/rpm/Packages
D: closed db environment /var/lib/rpm/Packages
```

如果结果看起来良好，你可以再次运行命令（不带 --test 选项）来移除软件包。

## 使用 rpm 查询软件包

你可以使用查询选项 (-q) 获取有关 RPM 包的信息。这可以简单地列出已安装的软件包，也可以打印关于软件包的详细信息。以下是 rpm 查询命令的基本格式（至少需要一个选项）：

```
# rpm -q [options]
```

以下列表显示了你可以在 rpm 查询中使用的有用选项：

- -qa — 列出所有已安装的软件包。
- -qf — 列出拥有特定文件的软件包。（文件必须包含完整路径，否则 rpm 会假设为当前目录。）
- -qi package — 列出关于软件包的大信息。
- -QR package — 列出软件包依赖的组件（如库和命令）。
- -ql package — 列出软件包包含的所有文件。
- -qd package — 列出软件包中的所有文档文件。
- -qc package — 列出软件包中的所有配置文件。
- -qp [option] package — 查询尚未安装的软件包。结合此选项与其他查询选项可以查询可以。

要列出计算机上安装的所有软件包，请使用 -qa 查询选项。由于这是一个很长的列表，你应该将输出传递给 less，或者可能使用 grep 来查找你需要的包。以下命令行显示了所有已安装的 RPM 包列表，并仅显示包含字符串 xfree 的名称。（grep 的 -i 选项表示忽略大小写。）

```
# rpm -qa | grep -i xorg
```

如果你对软件包的详情感兴趣，可以使用 rpm -i 查询。在下面的示例中，dosstools 软件包（用于工作）的信息如下：

```
# rpm -qi dosstools
Name: dosstools Relocations: (not relocatable)
Version: 3.0 Vendor: Fedora Project
Release: 1.fc10 Build Date: Tue 30 Sep 2008 09:58 AM host: x86_64
Install Date: 04 Oct 2008 11:29 AM Source: RPM
Size: 14236
Group: Applications License: GPL
URL: http://dosstools.com
Summary: Utilities for working with
Signature: GPG Sig: Matthias Shaou, Wed 30 May 2007 01:02:58 GMT, Key ID: 692ac459e254d574
```

如果你想知道某个命令或配置文件来自哪里，可以使用 -qf 选项。在这个示例中，-qf 显示 `chgrp` 来自 coreutils 软件包：

```
# rpm -qf /bin/chgrp
coreutils-6.12-10.fc1.i86
```

## 查询文件和文档

许多软件包都有与其关联的配置文件。要查看与软件包关联的配置文件，请使用 -c 选项。例如，你可以输入以下内容来查找：

```
# rpm -qc ppp
/etc/logrotate.d/ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果你想查看软件包的文档，请使用 -d 选项。这将显示帮助页、README 等。例如：

```
# rpm -qd xorg
/usr/share/man/1/
```

如果你想查看软件包中包含的所有文件，请使用 -ql 选项。这将显示软件包中每个文件的完整路径。例如：

```
# rpm -ql dosstools
/sbin/fsck
/sbin/mkfs
/sbin/mkdos
/sbin/mkfat
/usr/share/man8/fsck
```

