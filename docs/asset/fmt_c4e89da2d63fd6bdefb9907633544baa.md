
`umask` 命令设置默认文件保护……（略）……三个八进制数字分别指所有者、组和世界的访问权限。与 OpenVMS 不同，UNIX 不提供系统级保护；如上所述，超级用户可以随时访问所有文件。在本示例中，值 `0` 表示读、写、执行访问，`2` 表示读和执行访问，`7` 表示无访问。因此，`027` 表示所有者具有读写执行访问权限，组具有读执行访问权限，世界无访问权限。

许多邮件处理程序现在使用它们自己的内部设置来定义此目录。

……（文本省略）……在第二个示例中，`alias DIR 'ls -1 !* more'` 中，反斜杠（`\`，另一种元字符）防止了在定义别名时立即解析历史替换。相反，替换在调用别名时发生。如之前所示，感叹号从历史列表中调用命令，而星号（`*`，另一种元字符）则指示该命令的最后一个参数。

![](img/e259ba2750941fa3d146eda78c65e89d_65_0.png)

## 3.2 用户环境

### 表 3.1 一些 Shell 变量

| Shell 变量 | C Shell 变量 | OpenVMS 等效 | 含义 |
| --- | --- | --- | --- |
| `$1`, `$2`, 等. | `argv`, 或 `$1`, `$2`, 等. | `P1`, `P2`, 等. | 传递给 shell 或 shell 脚本的参数 |
| `'alexexport` | `autoexport` | | 自动导出所有后续定义的变量 |
| `TMOUT=n` | `autologout = n` | | 设置交互式 shell 终止前的空闲分钟数（C）或秒数（Korn） |
| `CDPATH=string` | `cdpath = string` | | 设置 `cd` 命令的备用目录树搜索 |
| `PWD` | `cwd` | `F$DIRECTORY()` | 设置当前工作目录 |
| `'xtrace` | `echo` | `SET VERIFY` | 回显命令行和参数 |
| `EDITOR = string` | `editmode = string` | | 设置用于命令行编辑时模拟的编辑器名称 |
| `histchars = string` | | | 替换用于历史替换的默认 `!` |
| `HISTFILE=string` | | `RECALL/INPUT` | 指定命令历史文件的名称 |
| `HISTSIZE=n` | `history = n` | `RECALL` | 保留最后 n 条命令以便回溯 |
| `HOME=string` | `home = string` | `SYS$LOGIN` | 设置主目录 |
| `IFS=string` | `breakchars = string` | `TPU` 单词分隔符定义 | 设置内部字段符，通常为空格、制表符和换行 |

### 表 3.1 一些 Shell 变量（续）

| Korn Shell 变量 | C Shell 变量 | OpenVMS 等效 | 含义 |
| --- | --- | --- | --- |
| `tignoreeof` | `ignoreeof` | `SET` | 防止 `<CTRL>-D` 登录；需要使用 `logout` (C shell) 或 `exit` (Korn, Bourne shells) 命令 |
| `MAILPATH=` | `mail` | `MAIL_DIRECTORY` | 设置 shell 检查邮件的位置 |
| `**= **` | `**= **` | | 防止重定向期间的无意覆盖 |
| `*string*` | `*string*` | | 防止文件名展开 |
| `Cnlobber` | `noclobber` | | |
| `tnoglob` | `noglob` | | 如果未找到匹配命令的文件时防止产生错误状态 |
| `nonomatch` | `tnotify` | `notify` | 设置作业完成的通知时间 |
| `*PATH=string*` | `path` | | 设置解析命令调用的搜索路径 |
| `**= **` | `**= **` | | 定义为搜索列表的逻辑名称 |
| `*string*` | `*string*` | | |
| `*PS1=string*` | `*PS1=string*` | `SET PROMPT` |
| `prompt =` | | | 设置备用提示符，默认 C shell 提示符 `%` 或 Korn shell 提示符 `$` 以及延续符 `>` |
| `*PS2=string2*` | `*string*` | | |
| `*string*` | | | |
| `RANDOM` | | | 返回 0 到 32,767 之间的随机数 |
| `REPLY` | | | 包含对提示符的响应文本 |
| `savehist =` | `n` | `RECALL/OUTPUT` | 在下一次终端会话开始时记住最后 n 条命令以便调用 |
| `SHELL`, or `shell` | `shell:` | | 设置 shell 程序的路径 |
| `FSGETJPI(...,$0 at login)` | | | 以命令完成的形式显示状态：z = 错误；0 = 无错误 |
| `*strin*` | `"CLINAME"` | | |
| `$?` | `status` | `$STATUS` | |
| `TERM` | `term` | | 设置终端类型 |
| `USER` | `user` | | 设置用户名 |
| `time = n` | | | |
| `FSGETDVI("TT-"DEVTYPE")` | | | 使任何耗时超过 n 秒的命令报告 CPU 和经过时间 |
| `FSGETJPI(...,"USERNAME")` | | | |
| `*verbose*` | `verbose` | `SET VERIFY` | 在历史替换后回显每个命令的单词 |

Host Korn shell 变量在 `bash` shell 中是相同的。通过 `set -o` 命令可用。

使用第二个示例中 `DIR` 的修订定义 `mZR *.e` 现在可以正常运行：参数 `*.e` 被传递给 `-1`，所有以 .f 结尾的文件的长目录列表被管道到 `more` 进行显示。

在最后一个示例中，不带选项或参数的 `ls`st明了关于设置变量命令的 UNIX 惯例：如果不带参数的情况下执行，设置变量的命令将返回之前使用该命令时建立的值。

`unalias` 命令顾名思义，移除之前定义的别名。图 3.2 展示了一个由 `alias` 和 `set` 命令组成的典型 `.shrc` 文件。

如果你修改了 `.shrc` 文件，必须在更改对当前 shell 生效之前执行 `source` 命令。`source` 命令内置于 C shell 中（见第 10.9 节）。`.shrc` 对应于 OpenVMS 命令 `@SYS$LOGIN:COM`。

![](img/e259ba2750941fa3d146eda78c65e89d_68_0.png)
![](img/ba27d146eda78c65e89d_69_0.png)

### 3.2 用户环境

#### 图 3.2 示例 `.shrc` 文件

```bash
set autologout=30

set prompt="uh>"

set cdpath=$HOME/sys

set path=$HOME/bin:/usr/bin:/etc.

set notify history=100

set inc=*/include

alias pwd='echo $cwd'

alias history='set old=$cwd'

alias pushd='set old=$cwd; chdir'

alias popd='cd $old; unset'
```
