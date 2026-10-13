
虽然 Linux 附带的大约数百个 GNU 命令几乎都有手册页，但关于如何使用 GNU 命令的详细信息必须使用 `info` 命令来阅读。例如，若要进一步了解 `bash`（其手册页相当详尽），请像这样使用 `info` 命令：

```bash
$ info bash
```

按 `n` 键和 `p` 键在文档中导航，或向下滚动到屏幕上的菜单项并按 Enter 键以阅读有关特定功能的说明。按 `q` 键停止阅读。

## 查找和阅读软件包文档

各种软件包的文档包含在 `/usr/share/doc` 目录中；该目录存储在一个以相关软件包名称标记的另一个目录中。你可以通过浏览 http://www.tldp.org/ 在线找到其他 Linux 文档，包括 HOWTO 和常见问题解答（FAQs）。HOWTO 文档包含与特定主题相关的具体信息，例如打印、设置网络、编程串行端口或在使用 Linux 时使用 CD-ROM 驱动器。这些文档可以使用你的网络浏览器阅读。当然，你可以使用的最佳在线工具之一是一个好的搜索引擎，例如 Google。

你可以使用 `less` 或其他分页器或文本阅读器阅读文本等文档格式。例如，若要阅读位于 `/usr/share/apps/LICENCES` 目录下名为 `GPL_v2` 的 GNU 通用公共许可证（GPL）副本，请像这样使用 `less`：

```bash
$ less /usr/share/apps/LICENCES/GPL_v2
```

按 Enter 键后，你可以前后滚动文件。按 `q` 键停止阅读。如果文档处于压缩形式（以 `.gz` 结尾），请使用首先解压文档的 `zless` 分页器：

```bash
$ zless /usr/share/man/es/man1/README.gz
```

大多数用户使用网络浏览器在图形桌面中阅读 HTML 等文档格式。然而，Fedora 至少包括两种通用的基于文本的网络浏览器，可以通过 `lynx` 和 `links` 命令访问。若要浏览系统上的 HTML 文件而无需使用 X11，请使用这两个命令中的任意一个，并附上文件路径。例如，若要使用 `links` 阅读 GNU GPL 的 HTML 版本，请像这样使用命令：

```bash
$ links /usr/share/doc/HTML/en/common/gpl-license.html
```

按 Enter 键后，使用上下方向键在文件中前后滚动。按 `q` 键然后按 Enter 键以停止阅读。如果你已配置鼠标，点击屏幕顶部的左键，`links` 将显示其菜单。

## 使用 Shell

Shell 是一个具有许多不同功能的交互式命令提示符：

- 输入和输出重定向
- 后台处理
- 作业控制
- 历史编辑
- 内置帮助
- 命令行补全
- 命令行编辑

Shell 解释键盘命令，通常使用称为 shell 脚本的 shell 解释器语言来启动其他命令或程序。

> **注意**
>
> Shell 脚本在第 15 章中讨论。

你使用的 shell 由系统 `/etc/passwd` 文件中你条目的最后一个字段指定。此示例显示，对于名为 `andrew` 的用户，登录 shell 是 `bash`：

```text
andrew:x:502:502::/home/andrew:/bin/bash
```

大多数 Linux 发行版（包括 Fedora）的默认 shell 是 GNU `bash` 或 Bourne Again Shell，但也可以使用其他 shell，例如 `tcsh`、`ksh` 和 `zsh`。你可以通过在命令行输入其名称来使用不同的 shell。或者，root 操作员在创建用户帐户时可能将用户指定为另一个 shell（参见本章节后面的“以 root 身份工作”）。

> **警告**
>
> 如果你有兴趣尝试 Linux 中的不同 shell，你可以使用 `chsh` 命令更改你的登录 shell，但请确保该 shell 实际已安装在你的系统上。例如，若要更改你的默认 shell 为 `tcsh`，首先使用 `which` 命令验证它是否已安装：

```bash
$ which tcsh
/bin/tcsh
```

此示例表明 `tcsh` shell 安装在 `/bin` 目录下。`tcsh` shell 还应列在你的系统批准 shell 列表 `/etc/shells` 中。检查以确保它已列出：

```bash
$ grep tcsh /etc/shells
/bin/tcsh
```

你还可以使用 `chsh` 命令的 `-1` 选项列出有效的系统 shell，以验证是否允许使用 `tcsh`。由于 `tcsh` 已安装并列在 `/etc/shells` 中，然后你可以使用 `chsh` 命令更改你的 shell：

```bash
$ chsh
Changing shell for andrew.
Password:
New shell [/bin/bash]: /bin/ksh
chsh: "/bin/ksh" does not exist.
```

请注意，如果你输入系统中未安装的 shell 名称，`chsh` 命令将报告错误。

```bash
$ chsh -s /bin/tcsh
Changing shell for andrew.
Password:
Shell changed.
```

如果你现在查看你的 `/etc/passwd` 条目，你会看到 `/bin/tcsh` 是你的默认 shell。下次登录时，你可以使用 `tcsh`。

用户登录时，默认会分配和加载一些内存变量。这些变量被称为 shell *环境变量*，可由各种命令使用以获取关于环境的信息，例如你运行的系统类型、你的主目录以及正在使用的 shell。环境变量由 Linux 操作系统使用，以帮助定制你系统的计算环境，并包括有用的规范和设置，例如可执行文件和软件库的默认位置。如果你开始编写 shell 脚本，你可能会在脚本中使用环境变量。在那之前，你只需要了解环境变量是什么以及它们的作用。

## 使用环境变量

以下列表包括一些环境变量，以及 shell 如何使用它们的说明：

- `PWD` — 提供当前工作目录的名称，由 `pwd` 命令使用（例如 `/home/andrew/foo`）
- `USER` — 声明用户名，例如 `andrew`
- `LANG` — 设置语言默认值，例如英语
- `SHELL` — 声明当前 shell 的名称和位置，例如 `/bin/bash`
- `PATH` — 设置可执行文件的默认位置，例如 `/bin`、`/usr/bin` 等
- `LD_LIBRARY_PATH` — 声明重要软件库的位置（因为大多数但并非所有 Linux 命令都使用共享资源）
- `TERM` — 设置正在使用的终端类型，例如 `vt100`，这在使用面向屏幕的程序（如文本编辑器）时可能很重要
- `MACHINE` — 声明系统类型、系统架构等

> **注意**
>
> 每个 shell 可以有自己的功能集和语言语法，以及独特的默认环境变量集。有关使用 Fedora 包含的不同 shell 的更多信息，请参阅第 15 章。

在命令行，你可以使用 `env` 或 `printenv` 命令来显示这些环境变量，如下所示：

```bash
$ env
PWD=/home/andrew
HOSTNAME=laptop.andyhudson.co.uk
USER=andrew
MACHTYPE=i386-redhat-linux-gnu
MAIL=/var/spool/mail/andrew
```

```bash
BASH_ENV=/home/andrew/.bashrc
LANG=en_GB
DISPLAY=:0
LOGNAME=andrew
SHLVL=1
PATH=/usr/kerberos/bin:/usr/local/bin:/bin:/usr/bin:
    /usr/X11R6/bin:/home/andrew/bin
SHELL=/bin/bash
HOSTTYPE=i386
OSTYPE=linux-gnu
HISTSIZE=1000
TERM=xterm
HOME=/home/andrew
```

上述简略列表展示了一些常见的变量。这些变量由位于 `/etc`、`/etc/skel` 或用户 `/home` 目录中的配置或资源文件设置。例如，你可以在 `/etc/profile`、`/etc/bashrc`、`.bashrc` 或 `.bash_profile` 文件中找到 bash 的默认设置，这些文件安装在你的主目录中。有关使用这些配置文件的详细信息，请阅读 bash 的手册页。

最重要的环境变量之一是 `$PATH`，它定义了可执行文件的位置。例如：如果你作为普通用户尝试使用一个不在你的 `$PATH` 中的命令（如 `ifconfig` 命令），你将看到类似以下内容：

```bash
$ ifconfig
-bash: ifconfig: command not found
```
