

## 第 4 章 软件管理

一旦你安装了完整的图形化桌面环境并通过该环境登录系统，你仍然可以通过在 GUI 终端应用程序（或伪终端）中输入命令来跟进本书中的所有练习。

在大多数环境中，你可以通过右键点击桌面并从上下文菜单中选择“启动终端”(Launch Terminal)来启动伪终端。如果没有该特定选项，请在应用程序菜单中寻找“运行命令”(Run Command)选项（或按 ALT+F2 启动运行应用程序对话框）。运行对话框打开后，你可以输入终端模拟器的名称（否则不退款！），例如在所有 Linux 系统中存在的古老的 `xterm`。如果你使用的是 GNOME 桌面，默认是 `gnome-terminal`。如果你使用的是 KDE，默认是 `konsole`。

![](img/9f6657924397c33f088db5321b751a83_117_0.png)

> 注意：在系统上安装和卸载软件被视为管理或特权功能。这就是为什么你会发现后续章节中的大多数命令都是使用提权权限执行的。实现这种特权状态取决于发行版，但所使用的思想和工具在所有发行版中都是通用的。另一方面，查询软件数据库并不视为特权功能。

## 使用 RPM 管理软件

后续章节将介绍在 Fedora、RHEL、CentOS 和 openSUSE 等 Red Hat 类型发行版上查询、安装、卸载和验证软件的细节。

### 使用 RPM 方式查询信息
（相互了解）

开始任何关系的最好方式之一就是了解对方。一些相关信息可能包括人的名字、职业、生日以及她的喜好。RPM 软件包也遵循同样的规则。同样地，在你获取某段软件（从互联网、发行版的 CD/DVD 或第三方处）后，你应该在将其成为你生活的一部分——即你的系统的一部分之前，先了解该软件。

随着你继续使用 Linux/UNIX，你会发现软件名称是非常直观的，你通常只需要看一眼名称就能判断出一个包是什么的。例如，对于初学者来说，可能无法立即看出一个名为 `gcc-5.1.1.rpm` 的文件是 GNU 编译器集合 (GCC) 的软件包。但一旦你熟悉了系统并知道要寻找什么，这些事情就会变得直观得多。你可以使用 RPM 查询各种类型的信息，例如软件包的构建日期、它的权重（或大小）、喜好（或其依赖关系）等。

让我们开始使用 RPM。通过具有管理权限的用户（即 root，超级用户）登录系统，如果你是通过 GUI 登录的，请启动终端。

## 查询所有软件包

使用 `rpm` 命令列出系统中当前已的所有软件包软件包。在 shell 提示符下：

```bash
[root@fedora-server ~] rpm --query --all
```

这将为你提供已安装软件的列表。

> 注意：与 Linux 命令一样，`rpm` 命令也有自己的长格式和短格式（或缩写）选项或参数。例如，`--query` 的短形式是 `-q`，`--all` 的短形式是 `-a`。我们在书中主要使用短形式，但偶尔也会使用长格式，以便你看到它们之间的关系。

## 查询特定软件包的详情

让我们关注上命令输出中的一个软件包，Bash 应用程序。使用 `rpm` 查看你的系统中是否确实安装了 Bash：

```bash
[root@fedora-server ~] rpm --query bash-4*
bash-4.*.x86_64
```

输出应该类似于第二行，显示 Bash 软件包已安装。它还显示了附加在包名后的版本号。

> 注意：在 Linux 发行版中处理软件包时，你系统上的准确版本号可能与我们示例系统的版本号不同。更新系统和 Linux 发行版本身等因素会影响并决定准确的软件包版本。这就是为什么有时我们在某些练习中省略软件包或软件名称中的版本号的原因之一。例如，我们可能不写 `bash-9.8.4.2.rpm` 而是写 `bash-9.*`。

你可以确定的是，主包名几乎总是相同的——也就是说，Bash 在 openSUSE、Fedora、Mandrake、CentOS、RHEL、Ubuntu 等系统中都是 Bash。

这引出了我们的下一个问题：Bash 是什么？它是做什么的？要找到答案，在这里输入查询：

```bash
[root@fedora-server ~]# rpm -qi bash
Name : bash
Version : 4.*
Architecture: x86_64
Install Date : Mon 20 Mar 2017 11:26:40 PM EDT
Group : System Environment/Shells
...  <OUTPUT TRUNCATED>...
Packager : Fedora Project
Vendor : Fedora Project
URL : http://www.gnu.org/software/bash
Summary : The GNU Bourne Again
```

Description :
GNU Bourne Again (Bash) 是一个与 Bourne shell 兼容的 shell 或命令解释器。

GNU Bourne Again (Bash) 是一个与 Bourne shell 兼容的 shell 或命令解释器。这为你提供了版本号、发布版本、描述等。要查看它还带有什么，输入：

```bash
[root@fedora-server ~]# rpm -ql bash
/etc/skel/.bash_logout
/etc/skel/.bash_profile
/etc/skel/.bashrc
```

`rpm` 的查询功能非常强大。RPM 软件包在标签中存储了大量信息。要查找软件包安装在你系统上的日期，你可以输入：

```bash
[root@fedora-server ~]# rpm -qf "%{INSTALLTIME}"
Mon 20 Mar 2017 11:26:40 PM EDT
```

要查找它属于哪个组，输入：

```bash
[root@fedora-server ~]# rpm -q "%{GROUP}"
System Environment/Shells
```

你可以查询多个软件包，也可以查询多个标签信息。例如，显示 Bash 和 nano 软件包的名称和包组，输入：

```bash
[root@fedora-server ~]# rpm -qq "%{NAME} %{SUMMARY}"
bash - System Environment/Shells - The Bourne Again shell
nano - Applications/Editors - A small text editor
```

要确定系统依赖哪些包来自 Bash，输入

```bash
[root@fedora-server ~]# rpm --requires bash
```

> 提示：这里提到的 RPM 查询是针对系统中已安装软件执行的。你也可以对从其他来源获得的软件执行类似的查询——即计划安装且从互联网或发行版 CD/DVD 获取的软件。你也可以对尚未安装的软件包执行类似的查询。只需在查询末尾添加 `-p` 选项即可。例如，假设你将 `joe-9.1.6.noarch.rpm` 下载到工作目录，并想查询该未安装包以获取更多信息。你会输入：
# rpm -qip joe-9.1.6.noarch.rpm

## 使用 RPM 安装软件（共同生活）

现在，你们都准备好进入这段关系的下一个阶段了。你们决定共同生活。这可能是件好事，因为允许你们双方查看并测试彼此是否真正兼容。这种关系的阶段类似于将软件包安装到你的系统上——即将软件移动到你的系统中。

在接下来的步骤中，你将在系统上安装一个名为“lynx”的简单文本浏览器。首先，你需要获取一个 RPM 副本

