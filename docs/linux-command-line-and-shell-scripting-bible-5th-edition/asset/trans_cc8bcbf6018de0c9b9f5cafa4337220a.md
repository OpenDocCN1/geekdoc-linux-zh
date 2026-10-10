
## 第四部分：使用替代 Shell

**表 24.2 续表**

| 变量 | 描述 |
| :--- | :--- |
| noclobber | 如果设置，重定向尝试不会自动销毁文件。 |
| noding | 如果设置，会在小时变化时禁用提示符时间中的 DING! 显示。 |
| noglob | 如果设置，禁用文件名替换和目录栈替换。 |
| noKANJi | 如果设置且 Shell 支持汉字（Kanji），则禁用该功能，以便可以使用元键。 |
| nomatch | 如果设置，不匹配的文件名替换或目录栈替换不会产生错误。 |
| nostat | 在执行补全操作期间，`stat` 命令不应包含的目录列表。 |
| notify | 如果设置，Shell 会异步通知作业完成。 |
| o | 用户的真实组织 ID。 |
| owd | 旧的工作目录。 |
| path | 用于查找可执行命令的目录列表。 |
| printexivalve | 如果在交互式 Shell 中设置，Shell 会显示非零退出状态。 |
| prompt | 每条命令行之前打印的字符串。 |
| prompt2 | 用于命令补全的次要命令行提示符。 |
| prompt3 | 用于自动拼写更正的字符串。 |
| promptchars | 一个双字符字符串；如果设置，第一个字符用于普通用户提示符，第二个字符用于 root 用户提示符。 |
| pushdchome | 如果设置，pushd 命令默认推送到 $HOME 目录。 |
| pushdsilent | 如果设置，pushd 和 popd 命令不会打印目录栈。 |
| reexexact | 如果设置，即使可能存在更长的匹配，补全也会基于精确匹配完成。 |
| recognize only_<br>executables | 如果设置，命令列表仅显示路径中可执行的文件。 |
| rmstar | 如果设置，在执行 `rm *` 命令之前会提示用户。 |
| rrprompt | 当左侧显示提示符时，屏幕右侧显示的字符串。 |
| savedirs | 如果设置，Shell 在退出前执行 `dirs -S` 命令，保存当前的 dirs 列表。 |
| savehist | 如果设置，Shell 在退出前执行 `history -S` 命令，保存当前的 history 列表。 |
| sched | `sched` 命令显示计划事件的格式。 |
| shell | Shell 程序的文件名。 |
| shlvl | 嵌套 Shell 的数量。 |
| status | 最后一条命令返回的退出状态。 |
| symlinks | 控制符号链接解析。可以设置为 **chase**、**ignore** 或 **expand**。 |
| tcsh | tcsh Shell 的版本号。 |
| term | 终端类型。 |
| time | 如果设置为一个数字，**time** 命令会在每个耗时超过指定 CPU 秒数的命令之后自动执行。 |
| tperiod | 定期执行特殊别名之间的时间间隔（以分钟为单位）。 |
| tty | Shell 所连接的当前 TTY 设备的名称。 |
| uid | 用户的真实用户 ID。 |
| user | 用户的登录名。 |
| verbose | 如果设置，Shell 在历史记录替换后显示每条命令。 |
| version | 显示 tcsh Shell 版本。 |
| visiblebell | 如果设置，屏幕闪烁代替可听见的铃声。 |
| watch | 设置要监视登录和注销的用户/终端对列表（可以使用 any 关键字）。如果用户或终端被使用则报告。 |
| who | 用于 **watch** 消息的格式字符串。 |
| wordchars | 编辑器命令视为单词一部分的非字母数字字符列表。 |

tcsh Shell 可用的 Shell 变量列表相当长！这些变量展示了 tcsh Shell 的强大功能。它允许你仅通过设置 Shell 变量来定制 Shell 的许多不同方面。

要显示当前 Shell 中已设置的 Shell 变量，请使用 `set` 命令：

```text
ubuntu2404:--> set

addsuffix
anyerror
argv    ()
autoexpand
autolist
cdpath
cshatsignol
cwd     /home/rich
dir     /etc/csh/cshrc.d
dirstack        /home/rich
echo_style      both
edit
eid     1000
euser   rich
gid     1000
group   rich
history
home
killring
owd
path
Prompt
prompt2
prompt3
shell
shlvl
status
tcsd
term
tty
uid
user
version
    100
    /home/rich
    30
    /usr/local/sbin /usr/local/bin /usr/sbin /usr/bin /sbin /bin /usr/games /usr/local/games /snap/bin /snap/bin
    $\u\m\u:$\B\r-$b\t#
    ?\f
    CORRECT>\r\ (Y|N|[E|A|]?
    /bin/tcsd
    2
    0
    6.24.10
    xterm-256color
    pts/0
    1000
    rich
    tcsd 6.24.10 (Astron 2023-04-14 (x86_64-unknown-linux)) options wide,nls,d1,ai,kan,sm,rb,nd,color,fileX
ubuntu2404:~>
```

请注意，tcsh `set` 命令的输出与你列出的 Bash Shell 变量产生的输出略有不同。tcsh Shell 版本在左侧显示 Shell 变量，在右侧显示当前值。

你应该能认出这些 Shell 变量中的许多个，它们与 Bash Shell 中的对应项相似。以下是两个需要注意的区别：

- tcsh Shell 使用 `prompt` Shell 变量（以及 `prompt2` 和 `prompt3`），而不是 PS1、PS2 和 PS3 环境变量。
- `path` Shell 变量包含一个索引目录列表，而不是一个由冒号分隔值的单个字符串。

要显示或使用 Shell 变量的当前值，必须在其前面加上美元符号：

```text
ubuntu2404:~> echo $path
/usr/local/sbin /usr/local/bin /usr/sbin /usr/bin /sbin /bin /usr/games /usr/local/games /snap/bin /snap/bin
ubuntu2404:~>
```

该索引字符串使用数组格式来包含 Shell 变量的各个值。你可以使用数组格式来访问各个元素：

```text
ubuntu2404:~> echo ${path[1]}
/usr/local/sbin
ubuntu2404:~> echo ${path[2]}
/usr/local/bin
ubuntu2404:~> echo ${path[3]}
/usr/sbin
ubuntu2404:~>
```

请注意，数组从索引位置 1 开始。

重要的是要记住，Shell 变量使用全小写字母，而环境变量使用全大写字母。混淆它们可能会导致问题。

### Shell 环境变量

tcsh Shell 还维护一组环境变量，类似于 Bourne Shell。表 24.3 列出了环境变量。

#### 表 24.3 tcsh Shell 环境变量

| 变量 | 描述 |
| :--- | :--- |
| AFsUSER | 等同于 af$u$er Shell 变量。 |
| COLUMNS | 终端上可用的列数。 |
| DISPLAY | 指向 X Windows 图形窗口的服务器。 |
| EDITOR | 默认编辑器的路径名。 |
| GROUP | 等同于 group Shell 变量。 |
| HOME | 等同于 home Shell 变量。 |
| HOST | Shell 进程正在运行的系统名称。 |
| HOSTTYPE | Shell 进程正在运行的机器类型。 |
| HPATH | 以冒号分隔的目录列表，run-help 编辑器命令在其中查找命令文档。 |
| LANG | 指定首选字符环境。 |
| LC_CTYPE | 如果设置，仅更改 ctype 字符处理。 |
| LINES | 终端中的行数。 |
| LS_COLORS | 与 ls 命令一起使用的文件类型和颜色分配的冒号分隔列表。 |
| MACHTYPE | 系统的微处理器类别或机器型号。 |
| OSTYPE | 系统的当前操作系统。 |
| PATH | 用于定位可执行文件的目录名的冒号分隔列表。 |
| PWD | 等同于 cwd Shell 变量，但仅在目录实际更改后更新。 |
| REMOTEHOST | 如果当前用户已远程登录，则远程主机的 IP 地址。 |
| SHLVL | 嵌套 Shell 的数量（等同于 shlvl Shell 变量）。 |
| SYSTYPE | 当前系统类型。 |
| TERM | 终端类型（等同于 term Shell 变量）。 |
| TERMCAP | 终端功能字符串。 |
| USER | 等同于 u$er Shell 变量。 |
| VENDOR | 系统处理器的供应商。 |
| VISUAL | 全屏编辑器的路径名。 |
