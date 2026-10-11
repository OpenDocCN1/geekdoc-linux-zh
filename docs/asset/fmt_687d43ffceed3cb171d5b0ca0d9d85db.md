
- GIMP 官方网站 <http://www.gimp.org/>：关于 GNU 图像操作程序（GNU Image Manipulation Program）的所有信息。
- SourceForge.net <http://sourceforge.net/>：开源软件开发站点。
- vim 主页 <http://www.vim.org/>

# 附录 B

## DOS 与 Linux 命令

在本附录中，我们将 DOS 命令与其等效的 Linux 命令进行了匹配。

作为给具有 Windows 背景的新用户的一种额外导航辅助手段，下表列出了 MS-DOS 命令及其对应的 Linux 命令。请注意，Linux 命令通常有许多选项。请阅读该命令的 Info 文档或 man 手册页以了解更多信息。

| DOS 命令 | Linux 命令 |
| :--- | :--- |
| `<command>` /? | `man <command>` |
| `cd` | `cd` |
| `chdir` | `pwd` |
| `cls` | `clear` |
| `copy` | `cp` |
| `date` | `date` |
| `del` | `rm` |
| `dir` | `ls` |
| `echo` | `echo` |
| `edit` | `vim`（或其他编辑器） |
| `exit` | `exit` |
| `fc` | `diff` |
| `find` | `grep` |
| `format` | `mke2fs` 或 `mformat` |
| `mem` | `free` |
| `mkdir` | `mkdir` |
| `more` | `more` 或 even `less` |
| `move` | `mv` |
| `ren` | `mv` |
| `time` | `date` |

表 11.2. DOS/Linux 命令概览

# 附录 C

## Shell 特性

本文档概述了常见的 shell 特性（在所有 shell 变体中相同）以及不同的 shell 特性（特定于特定 shell 的特性）。

### C.1 通用特性

以下特性是所有 shell 的标准配置。请注意，`stop`、`suspend`、`jobs`、`bg` 和 `fg` 命令仅在支持任务控制（job control）的系统上可用。

| 命令 | 含义 |
|---|---|
| `>` | 重定向输出 |
| `>>` | 追加到文件 |
| `<` | 重定向输入 |
| `<<` | “Here” 文档（重定向输入） |
| `|` | 管道输出 |
| `&` | 在后台运行进程。 |
| `;` | 在同一行上分隔命令 |
| `*` | 匹配文件名中的任意字符 |
| `?` | 匹配文件名中的单个字符 |
| `[1]` | 匹配包含在括号内的任意字符 |
| `( )` | 在子 shell 中执行 |
| `' '` | 替换括号内命令的输出 |
| `" "` | 部分引用（允许变量和命令扩展） |
| `' '` | 完全引用（不扩展） |
| `\` | 引用后一个字符 |
| `$var` | 使用变量的值 |
| `$$` | 进程 ID |
| `$0` | 命令名称 |
| `$n` | 第 n 个参数（n 从 0 到 9） |
| `$*` | 所有参数作为一个简单的单词 |
| `#` | 注释开始 |
| `bg` | 后台执行 |
| `break` | 跳出循环语句 |
| `cd` | 更改目录 |
| `continue` | 继续程序循环 |
| `echo` | 显示输出 |
| `eval` | 计算参数 |
| `exec` | 执行一个新的 shell |
| `fg` | 前台执行 |
| `jobs` | 显示活动任务 |
| `kill` | 终止运行中的任务 |
| `newgrp` | 更改到新的组 |
| `shift` | 移位位置参数 |
| `stop` | 挂起后台任务 |
| `suspend` | 挂起前台任务 |
| `time` | 对命令计时 |
| `umask` | 设置或列出文件权限 |
| `unset` | 擦除变量或函数定义 |
| `wait` | 等待后台任务完成 |

表 C. 1. 通用 Shell 特性

### C.2 差异化特性

下表显示了标准 shell (`sh`)、`Bourne Again Shell` (`bash`)、`Korn shell` (`ksh`) 和 C shell (`csh`) 之间的主要差异。

#### Shell 兼容性

由于 Bourne Again **Shell** 是 `sh` 的超集，所有 `sh` 命令在 **bash** 中也将有效 - 反之则不成立。**bash** 拥有更多自身的特性，并且如下表所示，还引入了许多其他 shell 的特性。

由于 Turbo C shell 是 `csh` 的超集，所有 `csh` 命令在 `tesh` 中都有效，但反之则不成立。

| `sh` | `bash` | `ksh` | `csh` | 含义/操作 |
|---|---|---|---|---|
| `$` | `$` | `$` | `%` | 默认用户提示符 |
| `>` | `>` | `>` | `>!` | 强制重定向 |
| `> file 2>&1` | `&> file` 或 `> file 2>&1` | `> file 2>&1` | `>& file` | 将 stdout 和 stderr 重定向到文件 |
| | `{ }` | | `{ }` | 展开列表中的元素 |
| `command` | `command` 或 `$(command)` | `$(command)` | `command` | 替换括号内 **command** 的输出 |
| `$HOME` | `$HOME` | `$HOME` | `$home` | 主目录 |
| | `~` | `~` | `~` | 主目录符号 |
| | `--`, `-`, `dirs` | `--`, `-` | `= -, =N` | 访问目录堆栈 |
| `var=value` | `VAR=value` | `var=value` | `set var=value` | 变量赋值 |
| `export var` | `export VAR=value` | `export var=val` | `setenv var val` | 设置环境变量 |
| | `${nnnn}` | `${nn}` | | 可以引用超过 9 个参数 |
| `"$@"` | `"$@"` | `"$@"` | | 所有参数作为单独的单词 |
| `$#` | `$#` | `$#` | `$argv` | 参数数量 |
| `$?` | `$?` | `$?` | `$status` | 最近执行的命令的退出状态 |
| `$$` | `$$` | `$$` | | 最近后台化的进程的 PID |
| `$-` | `$-` | `$-` | | 当前选项 |
| `. file` | `source file` 或 `. file` | `. file` | `source file` | 读取文件中的命令 |
| | `alias x='y'` | `alias x=y` | `alias x y` | 名称 x 代表命令 y |
| `case` | `case` | `case` | `switch` 或 `case` | 选择备选方案 |
| `done` | `done` | `done` | `end` | 结束循环语句 |
| `esac` | `esac` | `esac` | `endsw` | 结束 **case** 或 **switch** |
| `exit n` | `exit n` | `exit n` | `exit (expr)` | 以特定状态退出 |
| `for/do` | `for/do` | `for/do` | `foreach` | 循环遍历变量 |
| | `set -f` `set -o nulglob` `dotglob` `nocaseglob` `noglob` | | `noglob` | 在文件名生成时忽略替换字符 |
| `hash` | `hash` | `alias -t` | `hashstat` | 显示已缓存的命令（跟踪的别名） |
| `hash cm ds` | `hash cm ds` | `alias -t cm ds` | `rehash` | 记住命令位置 |
| `hash -r` | `hash -r` | | `unhash` | 忘记命令位置 |
| | `history` | `history` | `history` | 列出以前的命令 |
| | `ArrowUp+Enter` 或 `!!` | | `!!` | 重做上一个命令 |
| | `!str` | `! str` | `!str` | 重做最后一个以 "str" 开头的命令 |
| | `!cmd:s/x/y/` | `! x=y cmd` | `!cmd:s/x/y/` | 在最近的以 "cmd" 开头的命令中用 "y" 替换 "x"，然后 |

## 表 C.2. 不同的 Shell 特性

| `sh` | `bash` | `ksh` | `csh` | 含义/操作 |
|---|---|---|---|---|
| | | | | 执行。 |
