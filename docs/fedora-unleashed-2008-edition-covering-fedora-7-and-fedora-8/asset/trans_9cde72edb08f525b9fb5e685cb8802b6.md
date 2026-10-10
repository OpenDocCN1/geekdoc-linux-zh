

-   **SHELL**——用于声明当前 Shell 的名称和位置，例如 /bin/bash
-   **PATH**——用于设置可执行文件的默认位置，例如 /bin、/usr/bin 等
-   **LD_LIBRARY_PATH**——用于声明重要软件库的位置（因为大多数（但并非全部）Linux 命令都使用共享资源）
-   **TERM**——用于设置正在使用的终端类型，例如 vtt100，这在使用面向屏幕的程序（如文本编辑器）时可能非常重要
-   **MACHINE**——用于声明系统类型、系统架构等

# 注意

每个 Shell 都可以拥有自己的特性集和语言语法，以及一组独特的默认环境变量。有关使用 Fedora 中附带不同 Shell 的更多信息，请参阅第 15 章“通过 SSH 进行远程访问”。

在命令行中，您可以使用 `env` 或 `printenv` 命令来显示这些环境变量，例如：

```
$ env
SSH_AGENT_PID=2881
HOSTNAME=teletran.hudson.com
SHELL=/bin/bash
TERM=xterm
DESKTOP_STARTUP_ID=
USERNAME=andrew
MAIL=/var/spool/mail/andrew
PATH=/usr/kerberos/bin:/usr/lib/ccache:/usr/local/bin:\
/usr/bin:/bin:/home/andrew/bin
DESKTOP_SESSION=default
INPUTRC=/etc/inputrc
PWD=/home/andrew
KDEDIRS=usr
SSH_ASKPASS=/usr/libexec/openssh/gnome-ssh-askpass
SHLVL=2
HOME=/home/andrew
DISPLAY=:0.0
```

这个简化的列表显示了一些常见变量。这些变量由 /etc、/etc/skel 或用户 /home 目录中包含的配置或资源文件设置。例如，您可以找到 bash 的默认设置，位于安装在您主目录中的 /etc/profile、/etc/bashrc、.bashrc 或 .bash_profile 文件中。请阅读 bash 的手册页，以了解有关使用这些配置文件的详细信息。

最重要的环境变量之一是 `$PATH`，它定义了可执行文件的位置。例如，如果作为普通用户，您尝试使用一个不在您的 `$PATH` 中的命令（如 `ifconfig` 命令），您将会看到类似以下内容：

```
$ ifconfig
-bash: ifconfig: command not found
```

但是，您可能知道 `ifconfig` 确实已安装在您的系统上，您可以使用 `whereis` 命令来验证这一点，如下所示：

```
$ whereis ifconfig
ifconfig: /sbin/ifconfig /usr/share/man/man8/ifconfig.8.gz
```

您还可以通过输入其完整路径名，或像这样输入完整的目录规范来运行该命令：

```
$ /sbin/ifconfig
```

如您在这个例子中所见，`ifconfig` 命令确实已安装。发生的情况是，默认情况下，/sbin 目录不在您的 $PATH 中。其中一个原因是，/sbin 目录下的命令通常仅 intended 由 root 运行。您可以通过编辑主目录中的 `~/.bash_profile` 文件（如果您默认使用 `bash` Shell，就像大多数 Linux 用户那样）将 `/sbin` 添加到您的 `$PATH` 中。查找以下行：

```bash
PATH=$PATH:$HOME/bin
```

然后，您可以编辑此文件，也许使用 `vi` 编辑器（在本章中讨论过），像这样添加 `/sbin` 目录：

```bash
PATH=$PATH:/sbin:$HOME/bin
```

保存该文件。下次登录时，`/sbin` 目录将位于您的 `$PATH` 中。立即使用此更改的一种方法是使用 `bash` Shell 的 `source` 命令读取 `~/.bash_profile` 中的新设置，如下所示：

```bash
$ source ~/.bash_profile
```

现在，您可以运行 `ifconfig`，而无需明确输入其完整路径名。

一些 Linux 命令也使用环境变量——例如，用于获取配置信息（例如，通信程序查找诸如 `BAUD_RATE` 这样的变量，它可能表示默认调制解调器速度）。

若要试验环境变量，您可以修改 `$PS1` 变量来操控 Shell 提示符的外观。如果您正在使用 `bash`，可以使用其内置的 `export` 命令来更改 Shell 提示符。例如，如果您的默认 Shell 提示符看起来像

```bash
[andrew@telettran ~]$
```

您可以通过使用 PS1 变量像这样更改其外观：

```
$ PS1='$STYPE r001z .>'
```

按下回车键后，您会看到以下内容：

```
linux-gnu r001z .>
```

> **注意** 请参见 bash 手册页，了解可用于提示符设置的其他变量。

# 使用文本编辑器

Linux 发行版包含许多被称为 *文本编辑器* 的应用程序，您可以使用它们来创建文本文件或编辑系统配置文件。文本编辑器类似于文字处理程序，但通常功能较少，仅处理文本文件，并且可能支持也可能不支持拼写检查或格式设置。文本编辑器在功能和使用便捷性上有所不同，但几乎存在于每个 Linux 发行版中。系统中安装的编辑器数量取决于您在系统上安装了哪些软件包。

一些基于控制台的文本编辑器如下所示：

-   **emacs**——综合的 GNU emacs 编辑环境，它远不止一个编辑器；请参见本章后面“使用 emacs”部分
-   **joe**——Joe's Own Editor，一种文本编辑器，可用于模拟其他编辑器
-   **nano**——一种简单的文本编辑器，类似于随 pine 邮件程序提供的 pico 文本编辑器
-   **vim**——vi 文本编辑器的改进、兼容版本（我们在本章其余部分将其称为 vi，因为它有一个名为 vi 的符号链接和一个符号链接的手册页）

请注意，此处描述并非所有文本编辑器都是 *面向屏幕的*。X 窗口系统的一些文本编辑器提供了图形界面，例如菜单栏、按钮、滚动条等，如下所示：

-   **gedit**——GNOME 的 GUI 文本编辑器
-   **kate**——一个简单 KDE 文本编辑器
-   **kedit**——另一个简单 KDE 文本编辑器

学习如何使用基于文本的编辑器（如 vi）的一个良好原因是，系统维护和恢复操作通常不在 X 窗口会话期间进行（从而否定了使用 GUI 编辑器的可能性）。许多更大、更复杂且功能更强大的编辑器在 Linux 启动到单用户模式或维护模式时无法工作。有关 Fedora 启动方式的更多信息，请参见第 11 章。如果您的系统出现任何问题，您可能无法进入 X 窗口系统，因此熟悉使用命令行和 vi 等文本编辑器是很重要的。务必打开一些编辑器并试用它们；您永远不知道——也许某天您会感谢我！

学习如何在 Linux 控制台模式下使用基于文本的编辑器的另一个原因是，这样您就可以通过电话拨号或网络 Shell 会话编辑文本文件，因为许多服务器不提供图形桌面。

## 使用 vi

几乎在所有 UNIX 和 Linux 系统上都能找到的编辑器，毫无疑问，就是 vi 编辑器，最初由 Bill Joy 编写。这个简单但功能强大的编辑器拥有一套略显晦涩的命令集，但只需几个命令即可熟练使用。尽管更有经验的 UNIX 和 Linux 用户在计算会话中仍然大量使用 vi，但许多较新的用户可能更喜欢学习使用更容易操作的文本编辑器，如 pico 或 GNU nano。忠实的 GNU 爱好者和程序员肯定使用 emacs。

话虽如此，学习如何使用 vi 是个好主意。您可能需要编辑具有最小安装配置的 Linux 系统上的文件，或者远程服务器上没有安装更多可选文本编辑器。vi 可用的可能性非常大。

您可以像这样使用 vi 命令来开始编辑会话：

```
$ vi file.txt
```

vi 命令通过使用插入（或编辑）模式和查看（或命令）模式来工作。

当您刚开始编辑时，您处于查看模式。您可以使用光标或其他导航键（如稍后所示）滚动浏览文本。要开始编辑，请按 i 键插入文本或按 a 键追加文本。完成后，使用 Esc 键从插入或追加模式切换到查看（或命令）模式。要输入命令，输入冒号（:），然后输入命令，例如 w 用于写入文件，并按回车键。

虽然 vi 支持许多复杂的编辑操作和众多命令，但您可以使用几个基本命令来完成工作。这些基本的 vi 命令如下：

-   光标移动——h、j、k、l（左、下、上、右）
-   删除字符——x
-   删除行——dd
-   模式切换——Esc、Insert（或 i）

