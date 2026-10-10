
```
root@kemal:~# cat profile
### /etc/profile: system-wide .profile file for the Bourne shell (sh)
### and Bourne compatible shells (bash(1), ksh(1), ash(1), ...).

if [ "$u" -eq 0 ]; then
PATH=$usr/local/sbin:usr/local/bin:usr/sbin:usr/bin:$bin
else
PATH=$usr/local/bin:usr/bin/bin:usr/local/games:usr/games
fi
export PATH

if [ "$PS1" ]; then
if [ "$BASH" != "bin/sh" ]; then
### The file bash.bashrc already sets the default PS1.
# PS1='\h:\$'
if [ -f /etc/bash.bashrc ]; then
 /etc/bash.bashrc
fi
```

## 22 | Linux 命令精师

- `~/.bashrc`（包含初始化 bash 参数的设置文件）

```
root@local:~# cat .bashrc
### ~/.bashrc: executed by bash(1) for non-login shells.
### see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
### for examples

### If not running interactively, don't do anything
case $-
n  +i))
    return;
nesac

### don't duplicate lines or lines starting with space in the history
### See(1) for more options
HISTCONTROL=ignoreboth

### append to the history file, don't overwrite it
shopt -s histoptappend

### for setting history length size HISTSIZE and HISTFILESIZE in bash(1)
HISTSIZE=1000
HISTIFILIZE=2000
```

### ignoreeof 配置

bash shell 有许多功能。其中之一是使用 `CTRL + D` 键来退出 shell。当我们按下按键并退出 shell 时，shell 本身就会终止。可以进行某种规定来防止意外退出 shell。我们通过 `ignoreeof` 来进行这种安排。`ignoreeof` 设置可以防止通过 `CTRL + D` 键退出 shell。我们可以通过几种不同的方式来组织它。例如，我们可以使用 `set -o ignoreeof` 命令来启用它，通过使用 `set +o ignoreeof` 命令来恢复。

另一个命令是 `export IGNOREEOF=2`。可以使用 `export IGNOREEOF=0` 来恢复。我们可以通过在 `.bashrc` 的最后一行写入此第二个命令（通过输入 `IGNOREEOF=2`）并保存来使这种安排永久化。因此，此调整将变为永久。

最后的方法是使用 `ignoreeof = 2` 命令。在这种安排下，如果你按下两次 `CTRL + D` 键盘，我们将按照我们的指令退出 shell。

```
root@kemal:~# set -o ignoreeof
root@kemal:~# Kabuğu bırakmak için "exit" kullanın.
root@kemal:~# Kabuğu bırakmak için "exit" kullanın.
root@kemal:~# Kabuğu bırakmak için "exit" kullanın.
root@kemal:~# Kabuğu bırakmak için "exit" kullanın.
root@kemal:~# Kabuğu bırakmak için "exit" kullanın.
root@kemal:~# 
```

如你所见，当系统处于这种状态时，它会执行命令。

（注：由于用户提供的文本后部分存在重复和逻辑混乱，此处翻译已根据上下文进行了平顺处理）

```
root@kemal:/usr/share/doc# ls
trace
acceck
accountservice
ace-voip
ac
adduser
adwaita-icon-theme
afflib-tools
agfln
aircraft-ng
alsa-tools
amap
amd64-microcode libpng12-dev
libpod-latex-perl
libpod-readme-perl
polkit-agent-1-0
libpolkit-backend-1-0
libpolkit-geoip-1-0
libpopler-46
libpopler-glib
libpopler-qt4-4
libport0
libportaudio2
libpostproc52
libpotrace0
```

Man pages（帮助页）是 Linux 系统中的基础帮助文件。一个 man 页的结构通常如下：

- NAME：命令的名字和定义

- SYNOPSIS：如何使用该命令

- DESCRIPTION：命令功能的描述

- EXAMPLES：命令的用法示例。

- SEE ALSO：相关标题。

手册页位于下方 `/usr/share/man`。

```
root@kemal:/usr/share/man# ls id man1 man5 nl pt_BR sl vi
cs es fr.,UTF-8 gl it man2 man6 pl ro sr zh
da fi qi ja man3 man7 pl.UTF-8 ru sv_CN
de br hr de.UTF-8 fr.TR.ISO8859-1 hu ko man4 man8 pl sk tr zh_TW
root@kemal:/usr/share/man# _
```

手册页的配置如下：

- `man1`：通用用户程序。

- `man2`：系统程序。

- `man3`：库函数。（关于 C 语言编程）

- `man4`：私有文件。

- `man5`：文件格式。

- `man6`：游戏和屏幕保护程序。

- `man7`：不属于其他类别的各种命令。

- `man8`：系统管理与维护。

要查看 `ls` 命令的 man 帮助页（解释我们在上面提供的示例中的 help 命令），我们可以使用 `man ls command`。

![](img/aa6ce54dbb8ffe5b9d7befb8c6764064_28_0.png)

在查阅手册页中的帮助主题后，应按 `Q` 键退出。

## 30 | Linux 命令精大师

### Whatis

另一个名为 `whatis` 的命令，它可以间接帮助我们。我们可以使用这个命令来查找手册中某个应用程序或命令的帮助主题所在的位置。

```
root@kemal:~ whatis echo
echo (1)           - 显示一行文本
```

如果你想使用通配符进行查询（我们稍后会讨论到），你必须使用 `-w` 参数。例如 `whatis -w cal`。

```
root@kemal:~ whatis cal+
cal+: nothing appropriate.
root@kemal:~ whatis cal+
cal (1)           - 显示日历和复活节日期
calendar (1)      - 提醒服务
calloc (3)       - 分配和释放动态内存
calloc (3avr)     - (未知主题)
callprpc (3)     - 远程过程调用的库程序
```

### Apropos

`apropos` 命令用于获取帮助，它实际上会在后台运行 `man -k` 命令。
