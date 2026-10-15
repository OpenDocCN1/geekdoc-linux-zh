
## 表 13.25 Bash 2.x Shell 调用选项（续）

| 选项 | 含义 |
|---|---|
| -r | 启动受限 shell。 |
| -- | 表示选项结束并禁用后续选项处理。`--` 或 `-` 之后的任何参数都被视为文件名和参数。 |
| --dump-strings | 与 -0 相同。 |
| --help | 显示内置命令的使用信息并退出。 |
| --login | 使 bash 作为登录 shell 被调用。 |
| --noediting | 当 bash 以交互方式运行时，不使用 Readline 库。 |
| --noprofile | 启动时，bash 不读取初始化文件：/etc/profile、~/.bash_profile、~/.bash_login 或 ~/.profile。 |
| --norc | 对于交互式 shell，bash 不会读取 ~/.bashrc 文件。如果作为 sh 运行 shell，则默认启用。 |
| --posix | 如果 bash 的行为不符合 POSIX 1003.2 标准，则更改其行为以匹配该标准。 |
| --quiet | 在 shell 启动时不显示任何信息，这是默认行为。 |
| --rcfile file | 如果 bash 是交互式的，则使用此初始化文件而不是 ~/.bashrc。 |
| --restricted | 启动受限 shell。 |
| --verbose | 打开详细模式；与 -v 相同 |
| --version | 显示此 bash shell 的版本信息并退出。 |

## 13.19.1 set 命令与选项

set 命令可用于打开和关闭 shell 选项，也可用于处理命令行参数。要打开某个选项，在选项前加上短横线（-）；要关闭某个选项，在选项前加上加号（+）。有关 set 选项的列表，请参见表 13.26。

## 示例 13.90

```
1  $ set -f
2  $ echo *
   a
3  $ echo ??
   ??
4  $ set +f
```

## 说明

- 1. 打开 f 选项，禁用文件名扩展。
- 2. 星号不会被扩展。
- 3. 问号不会被扩展。
- 4. 关闭 f 选项，启用文件名扩展。

## 表 13.26 内建 set 命令选项

| 选项名称 | 快捷开关 | 作用 |
|---|---|---|
| allexport | -a | 从设置该选项开始直到取消设置，自动将新的或修改过的变量标记为用于导出。 |
| braceexpand | -B | 启用花括号扩展，这是默认设置。 |
| emacs |  | 对于命令行编辑，使用 emacs 内置编辑器，这是默认设置。 |
| errexit | -e | 如果命令返回非零退出状态（失败），则退出。读取初始化文件时不设置。 |
| histexpand | -H | 在执行历史替换时启用 ! 和 !!，这是默认设置。 |
| history |  | 启用命令行历史；默认开启。 |
| ignoreeof |  | 禁止 EOF（Ctrl-D）退出 shell；必须输入 exit。相当于设置 shell 变量 IGNOREEOF=10。 |
| keyword | -k | 将关键字参数放入命令的环境中。 |
| interactive_comments |  | 对于交互式 shell，行首的 # 用于注释掉该行剩余的任何文本。 |
| monitor | -m | 允许作业控制。 |
| noclobber | -C | 防止在使用重定向时覆盖文件。 |
| noexec | -n | 读取命令但不执行。用于检查脚本语法。交互式运行时不会开启。 |
| noglob | -d | 禁用路径名扩展（即关闭通配符）。 |
| notify | -b | 当后台作业完成时通知用户。 |
| nounset | -u | 展开未设置的变量时显示错误。 |

## 表 13.26 内建 set 命令选项（续）

| 选项名称 | 快捷开关 | 作用 |
|---|---|---|
| onecmd | -t | 读取并执行一条命令后退出。 |
| physical | -P | 如果设置，则在输入 cd 或 pwd 时不遵循符号链接。而是使用物理目录。 |
| posix |  | 如果默认操作不符合 POSIX 标准，则更改 shell 行为。 |
| privileged | -p | 设置后，shell 不读取 .profile 或 ENV 文件，并且 shell 函数不会从环境中继承；对于 setuid 脚本会自动设置。 |
| verbose | -v | 打开详细模式以进行调试。 |
| vi |  | 对于命令行编辑，使用 vi 内置编辑器。 |
| xtrace | -x | 打开回显模式以进行调试。 |

## 13.19.2 shopt 命令与选项

shopt（bash 2.x）命令也可用于打开和关闭 shell 选项。

## 表 13.27 shopt 命令选项

| 选项 | 含义 |
|---|---|
| cdable_vars | 如果 cd 内置命令的参数不是目录，则假定它是一个变量名，其值为要切换到的目录。 |
| cdspell | 纠正 cd 命令中目录名拼写的小错误。检查的错误包括字符颠倒、缺少一个字符和多一个字符。如果找到更正，则打印更正后的路径，并继续执行命令。仅由交互式 shell 使用。 |
| checkhash | bash 在尝试执行命令之前，会检查哈希表中找到的命令是否存在。如果哈希命令不再存在，则执行正常的路径搜索。 |
| checkwinsize | bash 在每条命令之后检查窗口大小，并在必要时更新 LINES 和 COLUMNS 的值。 |
| cmdhist | bash 尝试将多行命令的所有行保存在同一条历史记录中。这样可以方便地重新编辑多行命令。 |
| dotglob | bash 在文件名扩展的结果中包含以点（.）开头的文件名。 |
