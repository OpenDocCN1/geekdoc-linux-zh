
## 表 11.1 全局配置文件中的选定变量

| 变量或编号 | 命令名称 | 描述 |
|:---:|:---:|:---:|
| 1 | `PATH` | Shell 将查找命令的目录列表 |
| 2 | `PS1` | 主要系统提示符 |
| 3 | `ulimit` | 文件或命令可使用的系统资源上限 |
| 4 | `umask 002` | root 用户新文件或目录的权限 |
| | `umask 022` | 普通用户新文件或目录的权限 |
| 5 | `$USER` | 应用于命令和脚本的用户名格式 |
| 6 | `LOGNAME` | 预期登录名格式 |
| 7 | `MAIL` | 查找用户邮件消息的目录 |
| 8 | `HOSTNAME` | 计算机名称 |
| 9 | `HISTSIZE` | 响应 history 命令时显示的最大历史命令数 |

**MAIL** 变量告诉 shell 在哪里查找 **USER** 的邮件消息。邮件将在名为 **USER** 的目录中找到，该目录位于 `/var/spool/mail` 目录下。

**HOSTNAME** 变量告诉 shell 在哪里找到计算机名称（在这种情况下，是 `/bin/hostname`）。

**HISTSIZE** 变量设置了当用户输入 `history` 时 shell 将显示的历史命令行数（即历史命令数量）。正如之前讨论的那样，此功能对于重新输入历史命令、对命令参数进行敏感性分析甚至故障排除都非常有用。如示例 11.7 所示，默认值为 1,000 条命令！

## /etc/bashrc 文件示例

`/etc/bashrc` 文件是另一个由 **init** 调用的系统初始化脚本。它是 `/etc/profile` 的配套文件，但 `/etc/profile` 旨在存储环境变量和命令，而 /etc/bashrc 旨在存储其他系统功能和命令或过程的别名。请记住，函数是一种转换值或执行其他操作并返回结果的过程。调用该操作或转换通常称为调用函数。

在示例 11.8 中，我们看到一个提醒，即环境信息将放在 /etc/profile 中。然后，我们确保无论用户在何处操作，用户的主要系统提示符都是一致的。最后，定义了一个别名（本章稍后讨论），它允许任何用户在使用他们命名的任何命令来确定其绝对路径位置时使用新定义的命令。例如，输入 which man 会返回 /usr/bin/man，即调用 man 页面的可执行文件的位置。

### 示例 11.8 使用 /etc/bashrc 进行系统初始化

除了检查全局配置文件外，Freston 还会定期检查 /etc/bashrc 文件，包括其系统范围的功能和别名：

```bash
cat /etc/bashrc<Enter>
# /etc/bashrc

# System wide functions and aliases

# Environment stuff goes in /etc/profile

# are we an interactive shell?
if [ "$PS1" ]; then
  if [ -x /usr/bin/tput ]; then
    if [ "x`tput kbs`" = "x" ]; then # We can't do this with
# dumb" terminal
      stty erase `tput kbs`
    elif [ -x /usr/bin/wc ]; then
      if [ "`tput kbs | wc -c `" -gt 0 ]; then # We can't do
# this with *dumb" terminal
      fi
    fi
  fi
  case $TERM in
    xterm*)
      PROMPT_COMMAND="echo -ne
"< 033>0;$USER@$HOSTNAME>: $PWD\007"";
      ;;
    *)
      ;;
  esac
  [ "$EPS1" = "s\v\$" ] && PS1="s\v\$"

if [ *$SHLVL != "x1" ]; then ## We're not a login shell
	for i in /etc/profile.d/*.sh; do
		if [ -x $i ]; then
			. $i
		fi
	done
fi
fi
```

该文件仍然有效，且没有收到任何投诉或请求，因此 Freston 暂时保留原样。

## $HOME/.bash_profile 文件示例

在示例 11.9 中，我们看到为个人用户在其个人 .bash_profile 脚本文件中设置的变量。每次用户（在本例中为 Don Quixote）登录时，该脚本会被读取，其变量和命令会被采用或执行。

### 示例 11.9 为个人用户设置变量

好奇为什么她的 PATH 包含他的主目录而 Sanch’o 的不包含，Don Quixote 再次求助于 Freston。Freston 让他检查其隐藏的 .bash_profile 文件。“它可能在那里指定了，” Freston 说。因此，Don 进入他的主目录并 cat 他的 .bash_profile：

```bash
$ pwd<Enter>
/home/quixote
$ cat .bash_profile<Enter>
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
	. ~/.bashrc
fi

# User-specific environment and startup programs

PATH=$PATH:$HOME/bin
BASH_ENV=$HOME/.bashrc

export BASH_ENV PATH
unset USERNAME
```

Don 看到第一个 if-then-else 条件判断结构要求 shell 检查是否存在一个名为 *.bashrc* 的隐藏脚本文件（仅包含特定于该用户的别名和函数，而不是所有用户，如 */etc/bashrc* 中的那些），如果存在，则执行它。请注意，包含用户特定函数和别名的 *.bashrc* 文件可以命名为任何名称，但惯例是将其命名为与具有全局函数和别名的 */etc/bashrc* 文件相似。

接下来，他看到他的用户的 *PATH* 语句是如何被修改的。现有的 *PATH* 目录被采用，并且用户主目录中的 *bin* 目录被添加进去（请注意，此场景是 bash shell 的情况；Sancho 的环境是 tcsh，不包含将主目录添加到 *PATH* 的这一项）。如果你想确保 *当前* 目录包含在 *PATH* 变量中，请验证该变量是否包含两个或更多相邻的冒号，或者一个后跟一个点的冒号。

Don Quixote 现在明白为什么他的 *PATH* 和 Sancho 的在正常操作期间不具有一致性了。Freston 后来告诉他，*当 Sancho 在 bash shell 中工作时，这些 PATH 是相同的*。

与此同时，*BASH_ENV* 变量导致用户主目录中的 *.bashrc* 脚本在每次调用新的 *bash* shell 时运行。该脚本不被导出，因为 *.bashrc* 中的设置、别名和其他功能可能不是变量，因此不受导出限制。

请注意，*BASH_ENV* 和 *PATH* 变量被导出，以便子进程可以采用这些变量及其相应的值。

最后，变量 *USERNAME*（在最近版本的 Linux 中已不受欢迎），如果它幸存到这一步，将被移除。它以前曾让用户和系统管理员都感到困惑。

正如 */etc/profile* 在系统函数和别名方面有其配套文件 */etc/bashrc* 一样，*$HOME/.bash_profile* 按照惯例也有其配套文件 *$HOME/.bashrc*，用于用户定义的函数和别名。

## $HOME/.bashrc 文件示例

示例 11.3 包含 *BASH_ENV*=$HOME/.*bashrc* 变量，它导致 *$HOME/.bashrc*（带有其额外细节）在用户每次启动新的 *bash* shell 时执行。*$HOME/.bash_profile* 文件仅在用户登录时执行一次。

在示例 11.10 中，我们看到推荐用户特定的别名和函数，然后通过 if-then-else 判断语句搜索并调用全局别名和函数。否则，那些函数、别名等就不会被调用。

### 示例 11.10 用于用户定义函数和别名的脚本

在这里，我们窃听 Don 检查他的 `.bashrc` 文件：

```bash
$ pwd<Enter>
/home/quixote
$ cat .bashrc
# .bashrc
# User specific aliases and functions
# Source global definitions
if [ -f /etc/bashrc ]; then
. /etc/bashrc
fi
# Begin aliases written by Quixote de La Mancha
# Number 1 - Alias similar to old DOS command; written on July 23
alias dir-p="ls -l | less"
# End of aliases written by Quixote de La Mancha
```

在示例 11.10 中，我们看到 Don Quixote 如何编写了自己的别名。似乎 Don 是 DOS 老手，更喜欢 `dir` 样式的命令而不是 UNIX `ls` 样式。然而，请注意，他不能使用 `dir /p`，这是正确的 DOS 语法。他必须修改该命令。为什么？Shell 不会像 DOS 那样解释前斜杠，因此会返回错误消息。

## 练习

- 1. 确保你在你的主目录中，然后显示 shell 变量。

  ```bash
  $ cd<Enter>
  $ pwd<Enter>
  $ set<Enter>
  ```

- 2. 创建一个名为 `lunch` 的变量并将其值设置为 `pizza`。创建另一个名为 `dinner` 的变量并将其值设置为 ham。使用 `echo` 显示变量的值。

  在变量列表中找到它们。

  ```bash
  $ lunch=pizza<Enter>
  $ dinner=ham<Enter>
  ```

