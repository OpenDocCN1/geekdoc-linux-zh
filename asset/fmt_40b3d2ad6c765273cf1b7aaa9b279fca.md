
tcsh shell 的环境变量可能有些令人困惑。Bourne shell（及其衍生版本 Bash、ash 和 dash）使用单一类别的环境变量来存储系统信息。tcsh shell 包含两类环境变量：

- Shell 变量
- 系统环境变量

系统环境变量由大写文本字符串组成，提供标准的系统信息。tcsh shell 变量是对于 shell 具有特殊含义的小写变量。

### 特殊 shell 变量

表 24.2 显示了 tcsh 用于设置 shell 中行为功能的 shell 变量。

#### 表 24.2 tcsh 特殊 Shell 变量

| 变量 | 描述 |
| :--- | :--- |
| `addsuffix` | 如果设置（默认情况），文件名补全会在目录末尾添加正向斜杠 (`/`)，并在普通文件名末尾添加空格。 |
| `afuser` | 如果设置，`auto_logout` 将使用此值代替本地用户名进行 Kerberos 身份验证。 |
| `ampm` | 如果设置，所有时间均以 12 小时 AM/PM 格式显示。 |
| `argv` | 提供给 shell 的自变量。 |
| `autocorrect` | shell 在每个命令之前自动调用 `spell-word` 编辑器。 |
| `autoexpand` | 如果设置，shell 在每个命令之前自动调用 `expand-history` 编辑器。 |
| `autolist` | 如果设置，shell 在遇到歧义命令后列出可能的命令。 |
| `autologout` | 设置为自动注销前的不活动分钟数。可选的第二参数指定锁定终端前的不活动分钟数。 |
| `backslash_quote` | 如果设置，shell 始终使用反斜杠字符引用特殊字符（反斜杠、单引号和双引号）。 |
| `catalog` | 消息目录的文件名。 |
| `cdpath` | `cd` 命令将搜索子目录的目录列表。 |
| `color` | 如果设置，为某些命令启用彩色显示。 |
| `colorcat` | 如果设置，为消息使用彩色转义序列。 |
| `command` | 如果设置，定义使用 `-c` 命令行参数传递给 shell 的命令。 |
| `complete` | 控制命令补全。如果设置为 `enhance`，补全会忽略大小写并考虑特殊字符。如果设置为 `ignore`，补全仅忽略大小写。 |
| `continue` | 如果设置为命令列表，shell 将继续该命令列表，而不是开始一个新的列表。 |
| `continue_args` | 与 `continue` 相同，但 shell 会传递自变量。 |
| `correct` | 如果设置为 `cmd`，命令会自动进行拼写纠正。如果设置为 `complete`，命令会自动补全。如果设置为 `all`，整个命令行都会被纠正。 |
| `cshbetnotnl` | 如果设置，命令中的换行符和回车符将替换为空格。 |
| `cwd` | 当前目录的完整路径名。 |
| `dextract` | 如果设置，`pushd` 命令将从目录堆栈中提取第 n 个条目，而不是将其旋转到顶部。 |
| `dirstile` | `dirs` 命令查找历史文件的默认位置。 |
| `dirstack` | 目录堆栈上所有目录的数组。 |
| `dspbyte` | 控制多字节字符集的编辑。 |
| `dunique` | 如果设置，`pushd` 命令将从堆栈中删除目录名称的任何实例。 |
| `echo` | 如果设置，shell 在执行每个命令之前会回显该命令。 |
| `echo_style` | 定义 `echo` 命令的样式（bad, sys, both 或 none）。 |
| `edit` | 如果设置，使用命令行编辑器。 |
| `ellipsis` | 如果设置，提示中的 `%c`、`%` 和 `%C` 提示序列将使用 ...（省略号）指示跳过的目录。 |
| `fignore` | 列出补全时应忽略的文件名后缀。 |
| `filec` | 如果未设置 `edit` 变量，则使用传统的 csh shell 命令补全。 |
| `gid` | 用户的读取组 ID。 |
| `group` | 用户的组名。 |
| `histchars` | 决定历史替换中使用的字符的字符串值。 |
| `histdup` | 控制历史文件中重复项的处理方式（all, prev, erase）。 |
| `histfile` | 历史文件的默认位置。 |
| `histlit` | 如果设置，内置和编辑器命令以及 `savehist` 使用历史列表中行的未展开形式。 |
| `history` | 第一个条目指示要保存的历史项目数量。可选的第二条目指示历史打印的格式。 |
| `home` | 用户的主目录。 |
| `ignoreeof` | 如果设置为空字符串或 0，Ctrl-D 键组合不会退出 shell。 |
| `implicitcd` | 如果设置，在命令行输入目录名将产生类似使用 `cd` 命令配合该目录名的效果。 |
| `inputmode` | 在每行开始时将编辑器设置为插入或覆盖模式。 |
| `killdup` | 控制 kill ring 中的重复条目。可以设置为 all, prev 或 erase。 |
| `killring` | 要在内存中保留的被杀死字符串的数量（默认为 30）。 |
| `listflags` | 要添加到 `ls -F` 命令的标志列表（可以是 x, a 或 A）。 |
| `listjobs` | 如果设置，当作业挂起时列出所有作业。如果设置为 long，使用长格式。 |
| `listlinks` | 如果设置，`ls -F` 命令显示每个符号链接指向的文件类型。 |
| `listmax` | `list - choices` 编辑器命令列出的最大项目数。 |
| `listmaxrows` | `list - choices` 编辑器命令列出的最大行数。 |
| `loginsh` | 如果是登录 shell，则由 shell 设置。 |
| `logout` | 由 shell 设置为 normal, automatic 或 hangup。 |
| `mail` | 要检查新邮件的文件或目录的名称（由空格分隔）。 |
| `matchbeep` | 设置生成补全匹配蜂鸣音的条件——never, nomatch, ambiguous, notunique。 |
| `nobeep` | 禁用蜂鸣音。 |

### 第四部分：使用替代 Shell

**表 24.2 续表**

| 变量 | 描述 |
| :--- | :--- |
| `noclobber` | 如果设置，重定向尝试不会自动销毁文件。 |
| `noding` | 如果设置，会在小时变化时禁用提示符时间中的 DING! 显示。 |
| `noglob` | 如果设置，禁用文件名替换和目录栈替换。 |
| `noKANJi` | 如果设置且 Shell 支持汉字（Kanji），则禁用该功能，以便可以使用元键。 |
| `nomatch` | 如果设置，不匹配的文件名替换或目录栈替换不会产生错误。 |
| `nostat` | 在执行补全操作期间，`stat` 命令不应包含的目录列表。 |
| `notify` | 如果设置，Shell 会异步通知作业完成。 |
| `o` | 用户的真实组织 ID。 |
| `owd` | 旧的工作目录。 |
| `path` | 用于查找可执行命令的目录列表。 |
| `printexivalve` | 如果在交互式 Shell 中设置，Shell 会显示非零退出状态。 |
| `prompt` | 每条命令行之前打印的字符串。 |
| `prompt2` | 用于命令补全的次要命令行提示符。 |
| `prompt3` | 用于自动拼写更正的字符串。 |
| `promptchars` | 一个双字符字符串；如果设置，第一个字符用于普通用户提示符，第二个字符用于 root 用户提示符。 |
| `pushdchome` | 如果设置，`pushd` 命令默认推送到 `$HOME` 目录。 |
| `pushdsilent` | 如果设置，`pushd` 和 `popd` 命令不会打印目录栈。 |
| `reexexact` | 如果设置，即使可能存在更长的匹配，补全也会基于精确匹配完成。 |
| `recognize only_executables` | 如果设置，命令列表仅显示路径中可执行的文件。 |
| `rmstar` | 如果设置，在执行 `rm *` 命令之前会提示用户。 |
| `rrprompt` | 当左侧显示提示符时，屏幕右侧显示的字符串。 |
| `savedirs` | 如果设置，Shell 在退出前执行 `dirs -S` 命令，保存当前的 dirs 列表。 |
| `savehist` | 如果设置，Shell 在退出前执行 `history -S` 命令，保存当前的 history 列表。 |
| `sched` | `sched` 命令显示计划事件的格式。 |
| `shell` | Shell 程序的文件名。 |
| `shlvl` | 嵌套 Shell 的数量。 |
| `status` | 最后一条命令返回的退出状态。 |
| `symlinks` | 控制符号链接解析。可以设置为 `chase`、`ignore` 或 `expand`。 |
