

# 第二部分
配置与环境

# 11

# 环境

![](img/314a0280bc10c5c0d45be132de172677_177_0.png)

正如我们之前讨论过的，shell 在会话期间会维护一组信息，称为 *环境*。程序利用环境中存储的数据来确定系统配置的相关信息。虽然大多数程序使用 *配置文件* 来存储程序设置，但有些程序也会查找环境中存储的值来调整自身行为。了解这一点后，我们就可以利用环境来定制我们的 shell 体验。

在本章中，我们将使用以下命令：

- `printenv` 打印部分或全部环境
- `set` 设置 shell 选项
- `export` 将环境导出给后续执行的程序
- `alias` 为命令创建别名

## 环境中存储了什么？

shell 在环境中存储两种基本类型的数据；不过，对于 bash 来说，这两种类型在很大程度上难以区分。它们分别是 *环境变量* 和 *shell 变量*。shell 变量是由 bash 放入其中的数据位，而环境变量则是其他所有内容。除了变量之外，shell 还存储一些程序性数据，即 *别名* 和 shell 函数。我们在第 5 章中介绍了别名，并将在本书的第四部分中介绍 shell 函数（与 shell 脚本相关）。

## 检查环境

要查看环境中存储的内容，我们可以使用 bash 的内置命令 `set` 或 `printenv` 程序。`set` 命令会同时显示 shell 变量和环境变量，而 `printenv` 只显示后者。由于环境内容的列表会相当长，最好将任一命令的输出通过管道传递给 `less`。

```
[me@linuxbox ~]$ printenv | less
```

这样做后，我们应该会看到类似这样的内容：

```
USER=me
PAGER=less
LSCOLORS=Gxfxcxdxbxegedabagacad
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/usr/share/upstart/xdg:/etc/xdg
PATH=/home/me/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
DESKTOP_SESSION=ubuntu
QT_IM_MODULE=ibus
QT_QPA_PLATFORMTHEME=appmenu-qt5
JOB=dbus
PWD=/home/me
XMODIFIERS=@im=ibus
GNOME_KEYRING_PID=1850
LANG=en_US.UTF-8
GDM_LANG=en_US
MANDATORY_PATH=/usr/share/gconf/ubuntu.mandatory.path
MASTER_HOST=linuxbox
IM_CONFIG_PHASE=1
COMPIZ_CONFIG_PROFILE=ubuntu
GDMSESSION=ubuntu
SESSIONTYPE=gnome-session
XDG_SEAT=seat0
HOME=/home/me
SHLVL=2
LANGUAGE=en_US
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
LESS=-R
LOGNAME=me
COMPIZ_BIN_PATH=/usr/bin/
```

```
LC_CTYPE=en_US.UTF-8
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/
QT4_IM_MODULE=xim
DBUS_SESSION_BUS_ADDRESS=unix:abstract=/tmp/dbus-IwaesmWaT0
LESSOPEN=| /usr/bin/lesspipe %s
INSTANCE=
```

我们看到的是环境变量及其值的列表。例如，我们看到一个名为 `USER` 的变量，其值为 `me`。`printenv` 命令还可以列出特定变量的值。

```
[me@linuxbox ~]$ printenv USER
me
```

`set` 命令在没有选项或参数的情况下使用时，会显示 shell 变量和环境变量，以及任何已定义的 shell 函数。与 `printenv` 不同，它的输出会按字母顺序整齐地排序。

```
[me@linuxbox ~]$ set | less
```

也可以使用 `echo` 命令查看变量的内容，如下所示：

```
[me@linuxbox ~]$ echo $HOME
/home/me
```

环境中有一种元素既不会由 `set` 也不会由 `printenv` 显示，那就是别名。要查看它们，请在不带参数的情况下输入 `alias` 命令。

```
[me@linuxbox ~]$ alias
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

## 一些有趣的变量

环境中包含相当多的变量，虽然你的环境可能与这里展示的不同，但我们很可能会在自己的环境中看到表 11-1 中列出的变量。

### 表 11-1：环境变量

| 变量 | 内容 |
|---|---|
| DISPLAY | 如果你正在运行图形环境，这是你的显示器名称。通常为 `:0`，表示 X 服务器生成的第一个显示。 |
| EDITOR | 用于文本编辑的程序名称。 |
| SHELL | 你的 shell 程序的名称。 |
| HOME | 你的主目录的路径名。 |
| LANG | 定义你的语言的字符集和排序顺序。 |
| OLDPWD | 上一个工作目录。 |
| PAGER | 用于分页输出的程序名称。通常设置为 `/usr/bin/less`。 |
| PATH | 以冒号分隔的目录列表，当你输入可执行程序的名称时会搜索这些目录。 |
| PS1 | 代表“提示字符串 1”。它定义了 shell 提示符的内容。稍后我们会看到，它可以被广泛定制。 |
| PWD | 当前工作目录。 |
| TERM | 你的终端类型名称。类 Unix 系统支持多种终端协议；此变量设置要与终端模拟器使用的协议。 |
| TZ | 指定你的时区。大多数类 Unix 系统以协调世界时（UTC）维护计算机的内部时钟，然后通过应用此变量指定的偏移量来显示本地时间。 |
| USER | 你的用户名。 |

