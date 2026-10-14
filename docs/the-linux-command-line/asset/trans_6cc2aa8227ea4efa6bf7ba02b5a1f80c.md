

这样做，我们应该得到类似这样的内容：

```
KDE_MULTIHEAD=false
SSH_AGENT_PID=6666
HOSTNAME=linuxbox
GPG_AGENT_INFO=/tmp/gpg-Pd0t7g/S.gpg-agent:6689:1
SHELL=/bin/bash
TERM=xterm
XDG_MENU_PREFIX=kde-
HISTSIZE=1000
XDG_SESSION_COOKIE=6d7b05c65846c3eaf3101b0046bd2b00-1208521990.996705-1177056199
GTK2_RC_FILES=/etc/gtk-2.0/gtkrc:/home/me/.gtkrc-2.0:/home/me/.kde/share/config/gtkrc/gtkrc-2.0
GTK_RC_FILES=/etc/gtk/gtkrc:/home/me/.gtkrc:/home/me/.kde/share/config/gtkrc
GS_LIB=/home/me/.fonts
WINDOWID=29360136
QTDIR=/usr/lib/qt-3.3
QTINC=/usr/lib/qt-3.3/include
KDE_FULL_SESSION=true
USER=me
LS_COLORS=no=00:fi=00:di=00;34:ln=00;36:pi=40;33;so=00;35:bd=40;33;01:cd=40;33;01:or=01;05;37;41:mi=01;05;37;41:ex=00;32:* .cmd=00;32:* .exe :
```

我们看到的是环境变量及其值的列表。例如，我们看到一个名为 USER 的变量，其值包含“me”。printenv 命令也可以列出特定变量的值：

```
[me@linuxbox ~]$ printenv USER
me
```

set 命令在不使用选项或参数时，会显示 shell 和环境变量，以及任何已定义的 shell 函数。与 printenv 不同，其输出会礼貌地按字母顺序排序：

```
[me@linuxbox ~]$ set | less
```

也可以使用 echo 命令查看变量的内容，如下所示：

```
[me@linuxbox ~]$ echo $HOME
/home/me
```

set 或 printenv 都不会显示环境中的一个元素，那就是别名。要查看它们，请在不带参数的情况下输入 alias 命令：

```
[me@linuxbox ~]$ alias
alias l='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

## 有趣的变量

环境中包含相当多的变量，虽然你的环境可能与此处展示的不同，但你很可能会在环境中看到以下变量：

表 12-1：环境变量

| Variable | Contents |
|---|---|
| DISPLAY | 如果你正在运行图形环境，则为显示器的名称。通常这是“:0”，表示 X 服务器生成的第一个显示。 |
| EDITOR | 用于文本编辑的程序名称。 |
| SHELL | 你的 shell 程序的名称。 |
| HOME | 你的主目录的路径名。 |
| LANG | 定义你的语言的字符集和排序顺序。 |
| OLD_PWD | 上一个工作目录。 |
| PAGER | 用于分页输出的程序名称。这通常设置为 /usr/bin/less。 |
| PATH | 当你输入可执行程序的名称时会被搜索的目录的冒号分隔列表。 |
| PS1 | 提示符字符串 1。这定义了你的 shell 提示符的内容。正如我们稍后将看到的，这可以被大量自定义。 |
| PWD | 当前工作目录。 |
| TERM | 你的终端类型的名称。类 Unix 系统支持许多终端协议；此变量设置与你的终端模拟器一起使用的协议。 |
| TZ | 指定你的时区。大多数类 Unix 系统以 *协调世界时 (UTC)* 维护计算机的内部时钟，然后通过应用此变量指定的偏移量来显示本地时间。 |
| USER | 你的用户名。 |

如果其中一些值缺失也不必担心。它们因发行版而异。

## 环境是如何建立的？

当我们登录系统时，bash 程序启动，并读取一系列称为启动文件的配置脚本，这些脚本定义了所有用户共享的默认环境。随后会读取我们主目录中的更多启动文件，以定义我们的个人环境。确切的顺序取决于正在启动的 shell 会话的类型。有两种类型：登录 shell 会话和非登录 shell 会话。

登录 shell 会话是指我们被提示输入用户名和密码的情况；例如，当我们启动一个虚拟控制台会话时。非登录 shell 会话通常发生在 GUI 中启动终端会话时。

登录 shell 会读取如表 12-2 所示的一个或多个启动文件：

表 12-2：登录 Shell 会话的启动文件

| File | Contents |
|---|---|
| /etc/profile | 适用于所有用户的全局配置脚本。 |
| ~/.bash_profile | 用户的个人启动文件。可用于扩展或覆盖全局配置脚本中的设置。 |
| ~/.bash_login | 如果未找到 ~/.bash_profile，bash 会尝试读取此脚本。 |
| ~/.profile | 如果既未找到 ~/.bash_profile 也未找到 ~/.bash_login，bash 会尝试读取此文件。这是基于 Debian 的发行版，例如 Ubuntu 的默认值。 |

非登录 shell 会话读取以下启动文件：

