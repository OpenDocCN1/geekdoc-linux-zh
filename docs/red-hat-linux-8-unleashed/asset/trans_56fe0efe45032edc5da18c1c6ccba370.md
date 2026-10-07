

## 第 5 章 Linux 入门

要查找某个命令及其对应的文档，你可以使用 `whereis` 命令。例如，如果你正在寻找 `fdisk` 命令，可以这样操作：

```
$ whereis fdisk
fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.gz
```

## 使用 man 页 (man Pages)

要学习更多关于命令或程序的信息，请使用 `man` 命令。Linux 和 X Window 命令的手页位于 /usr/share/man、/usr/local/share/man 以及 /usr/X11R6/man 目录下；例如，要阅读 `rm` 命令的手页，可以这样使用 `man` 命令：

```
$ man rm
```

按下回车键后，`less` 命令（一种名为分页器的 Linux 命令）会显示手册页。`less` 命令是一个文本浏览器，你可以向前向后滚动文档（甚至是左右滚动）以获取更多关于该命令的信息。按字母 `h` 获取帮助，使用正斜杠 `/` 输入搜索字符串，或按 `q` 退出。

> 尽管 Red Hat Linux 包含的数百个 GNU 项目命令中几乎所有都有手册页，但关于 GNU 命令的详细信息必须使用 `info` 命令进行阅读。例如，要学习关于 `bash`（它有一个非常详尽的手页），可以这样使用 `info` 命令：

```
$ info bash
```

按 `n` 和 `p` 键可以在文档中导航，或者向下滚动到屏幕上的某个菜单项并按回车键阅读特定功能的介绍。按 `q` 退出阅读。

## 查找和阅读软件包文档

各种软件包的文档包含在 /usr/share/doc 目录下；该目录又被存储在另一个标记有相关包命名的目录中。你可以通过浏览 http://www.tldp.org 在线查找其他 Linux 文档，这些文档被称为 HOWTO 和常见问题解答 (FAQs)。HOWTO 文档包含与特定主题相关的特定信息，如打印、设置网络、为串口端口（serial port）编程或在 Linux 中使用 CD-ROM 驱动器。你可以使用 Web 浏览器阅读这些文档。当然，你使用的最好的工具之一是优秀的搜索引擎，例如 Google。

你可以使用 `less` 或其他分页器/文本阅读器来阅读文档格式。例如，要阅读 GNU 通用公共许可证 (GPL) 的副本（位于 /usr/share/apps/LICENSES 目录下的名为 `GPL_V2` 文件），可以这样使用 `less`：

```
$ less /usr/share/apps/LICENSES/GPL_V2
```

按下回车键后，你可以反复滚动查看文件。按 `q` 退出阅读。如果文档是压缩格式（以 `.gz` 结尾），请使用 `zless` 分页器，它会先解压文档：

```
$ zless /usr/share/man/es/man/README.gz
```

大多数用户在图形化桌面中使用 Web 浏览器以 HTML 格式阅读文档。Hat Linux 包含至少两个通用的基于文本 Web 浏览器，通过 `lyn` 和 `links` 命令访问。要在不使用 X11 的情况下浏览系统上的 HTML 文件，请使用另一个命令并带上文件路径。例如，使用 `links` 读取 HTML 版本的 GNU GPL，可以使用如下代码：

```
$ links /usr/share/doc/HTML/en/common/gpl-1-license.html
```

按下回车键后，使用向上和向下方向键反复滚动文件。按 `q` 退出阅读。如果你配置了鼠标，点击屏幕顶部的左键，`links` 将显示其菜单。

## 使用 Shell

Shell 是一个具有许多不同功能的交互式命令提示符：

- 输入和输出重定向
- 后台处理
- 作业控制
- 历史编辑
- 内置帮助
- 命令行补全
- 命令行编辑

Shell 解释键盘命令，通常用于使用 shell 解释器语言（称为 shell 脚本）启动其他命令或程序。

> 注意：Shell 脚本将在第 22 章“Shell 脚本”中讨论。

你使用的 shell 是由系统 /etc/passwd 文件中对应条目的最后一个字段指定的。这个示例以一个名为 `winky` 的不幸用户为例，显示登录 shell 是 `bash`：

```
winky:x:502:502::/home/winky:/bin/bash
```

## 第 5 章 Linux 入门

大多数 Linux 发行版（包括 Red Hat Linux）的默认 shell 是 GNU bash 或 Bourne Again，其他其他可用的 shell，如 `tcsh`、`ksh` 和 `zsh`。你可以通过在命令行输入其名称来使用不同的 shell。或者，root 员可以在首次创建该用户账户时将用户分配到另一个 shell（参见本章后文“以 root 身份工作”）。

> 警告
如果你感兴趣在 Linux 上尝试不同的 shell，你可以使用 `csh` 命令更改你的登录 shell，并确保系统上已安装该 shell。例如，要将默认 shell 更改为 `tcsh`，首先使用 `which` 命令验证其是否已安装。

```
$ which tcsh
/bin/tcsh
```

此示例显示 `tcsh` shell 安装在 /bin 目录下。`tcsh` shell 也应该列在你系统的受批准 shell 列表 /etc/shells 中。检查它是否在列列表中：

```
$ grep tcsh /etc/shells
/bin/tcsh
```

你还可以使用 `csh` 命令的 `-l` 选项列出有效的系统 shell，以验证是否允许使用 `tcsh`。由于 `tcsh` 已安装并列在 /etc/shells 中，你就可以使用 `csh` 命令更改 shell：

```
$ csh
```

更改 winky 的 shell。
密码：
新 shell [/bin/bash]: /bin/ksh
chsh: "/bin/ksh" 不存在

注意如果你输入系统中不存在的 shell 名称，`csh` 命令将报告错误。

```
$ csh -s /bin/tcsh
更改 winky 的 shell。
密码：
shell 已更改。
```

如果你现在查看 /etc/passwd 条目，你会发现 /bin/tcsh 是你的默认 shell。下次登录时，你将使用 `tcsh`。

## 使用环境变量

当用户登录时，会分配并加载许多内存变量。这些变量被称为 shell 环境变量，各种命令可以使用它们获取有关你的环境、正在运行的系统类型、主目录以及正在使用的 shell 的信息。环境变量由 Red Hat 设置以为用户定制环境。以下列表包含常用变量：

- PWD
- USER
- LANG
- SHELL
- PATH
- LD_LIBRARY_PATH
- TERM
- MACHINE
- OSTYPE
- HOSTTYPE
- DISPLAY
- HOME
- MAIL
- LOGNAME
- SHLVL
- HISTSIZE
- BASH_ENV

> 注意：每个 shell 都可以有自己的set环境变量。更多信息请参阅 bash。

这个简短列表显示了一些常用变量。这些变量由包含在 /etc、/etc/skel 或 /home 目录下的配置文件设置。你可以找到 bash 的默认设置，例如在 /etc/profile、/etc/bashrc，以及安装在你主目录中的 .bashrc 或 .bash_profile 文件中。

