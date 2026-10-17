
让我们使用 `RPM` 和 `dpkg` 尝试一些操作。首先登录系统并启动终端（参见上一个提示）。

## 查询所有软件包

使用 `rpm` 列出系统中当前安装的所有软件包。在 `shell` 提示符下：

```
[root@fedora-server A]# rpm query --all
```

这将为你提供一份已安装软件的长列表。

> 注意：与大多数 Linux 命令一样，`rpm` 也有自己的选项或参数的长形式和短（缩写）形式。例如，`--query` 选项的短形式是 `-q`，`--all` 的短形式是 `-a`。我们在书中主要使用短形式，但偶尔也会使用长形式，以便你看到它们之间的关系。

## 正式进入正题

上一章节带你走完了安装过程。现在你已经有了一个可以运行的系统，你需要登录该系统以执行本书在本章节及其他章节中的练习。大多数练习都会隐式地要求你输入一条命令。虽然这看起来像是在说显而易见的事，但每当你被要求输入命令时，你必须在 `shell prompt` 的控制台中输入它。这类似于 Microsoft Windows 中的 DOS 命令行提示符，但功能更强大。

在 `shell` 中输入命令有多种方法。一种方法是使用窗口、终端（GUI 终端）；另一种方法是使用系统控制台。窗口化控制台被称为终端模拟器（伪终端），它们有非常多。在登录到你选择的桌面（`GNOME`、`KDE`、`Xforms` 桌面环境 [`XFCE`, 等]）后，你通常可以通过右键点击桌面并从上下文相关菜单中选择“启动终端”（Launch Terminal）来启动一个伪终端。如果你没有那个特定选项，请在菜单中寻找“运行命令”（Run Command）选项（或同时按下 `ALT` 和 `r` 键启动“运行应用程序”对话框）。在运行对话框出现后，你可以在运行框中输入终端模拟器的名称。所有 Linux 系统中几乎可以保证（否则退钱退款！）存在一个流行的终端模拟器，那就是老牌的 `xterm`。如果你使用的是 `GNOME` 桌面，默认是 `gnome-terminal`。如果你使用的是 `KDE`，默认的是 `konsole`。

## 查询特定软件包的详情

让我们仔细关注上一个命令输出中列出的软件包之一：`bash` 应用程序。使用 `rpm` 检查你的系统中是否确实安装了 `bash` 应用程序。

```
[root@fedora-serverA ~]# rpm --query bash
bash-3.2-*
```

输出结果应该与所示类似。它显示你确实已经安装了名为 `bash` 的包。它还显示了附加在包名后的版本号。请注意，你系统上输出的版本号可能不同；但主包名几乎总是相同的，即在 OpenSUSE、Fedora、Mandrake、RHEL、Ubuntu 等系统中，`bash` 始终是 `bash`，`bash` 永远是 `bash`。

# Linux 管理：入门指南

这引出了我们的下一个问题。`bash` 是什么？它能做什么？要找到答案，请输入

```
[root@fedora-serverA ~]# rpm -qi bash
Relocations: (not relocatable)
Name         : bash
Version      : 3.2
Vendor       : Red Hat, Inc.
<OUTPUT TRUNCATED>...
```

URL          : http://www.gnu.org/software/bash

Summary      : The GNU Bourne Again shell (bash) version 3.2

Description

GNU Bourne Again shell (Bash) 是一种 shell 或命令语言解释器，与 Bourne shell (`sh`) 。Bash 包含了 Korn shell (`ksh`) 和 C shell (`csh`) 的有用功能。大多数 `sh` 脚本可以在无需修改的情况下由 `bash` 。此软件包 (`bash`) 包含了 3.2  `bash`，它比之前的版本改进了 POSIX 兼容性。

此输出提供了大量信息。它显示了版本号、发行版本、描述、包信息等。

`bash` 软件包看起来相当了不起。让我们看看它包含哪些内容。

```
[root@fedora-serverA ~]# rpm -ql bash
/usr/bin/bash
/usr/bin/bash.login
/usr/bin/bash_completion
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/share/profile
/usr/share/bash/bashinfo
/usr/share/bash/bashrc
/usr/share/bash/bashquote
/usr/share/bash/bash_completion
/usr/share/bash/bash_completion
/usr/share/bash/bash_profile
/usr/share/bash/bash_profile
/usr/share/bash/bash_profile
/usr/share/bash/bash_profile
/usr/share/bash/bash_profile
/usr/share/bash/bash_profile
/usr/share/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
/usr/lib/bash/bash_completion.bash
```

`bash` 软件包看起来相当了不起。让我们看看它包含哪些内容。
