
`declare -r SHELLOPTS="braceexpand:emacs:hashall:histexpand: ..."`

`declare -ir UID="500"`

`declare -r person2="zach"`

`declare -rx person3="helen"`

前七个是自动声明为只读（readonly）的关键字变量。这些变量中的某些以整数形式存储（`-i`）。`-a` 选项表示 `BASH_VERSIONINFO` 是数组变量；数组每个元素的值列在等号右侧。

默认情况下，变量的值以字符串形式存储。当你对字符串变量进行算术运算时，shell 会将变量转换为数字，进行处理，然后转换回字符串。具有整数属性的变量以整数形式存储。按照如下方式分配整数属性：

```bash
$ declare -i COUNT
```

## 关键字变量

关键字变量是在 shell 启动时继承的，或者由 shell 声明并初始化。你可以从命令行或启动文件为这些变量赋值。通常情况下，你希望这些变量适用于你启动的所有子 shell 以及你的登录 shell。对于那些 shell 未自动导出的变量，你必须使用 `export`（见第 1008 页）让子 shell 可以使用它们。

### HOME：你的主目录

默认情况下，你的主目录是登录时的工作目录。主目录在设置你的账户时建立；其名称存储在 `/etc/passwd` 中。

```bash
$ grep sam /etc/passwd
sam:x:500:500:sam Great:/home/sam:/bin/bash
```

当你登录时，shell 会继承你主目录的路径并将其赋值给变量 `HOME`。当你输入不带参数的 `cd` 命令时，`cd` 会将存储在 `HOME` 中的目录设置为工作目录：

```bash
$pwd
/home/max/laptop
$ echo $HOME
/home/max
$ cd
$pwd
/home/max
```

## 第 9 章 Bourne Again Shell

此示例展示了 `HOME` 变量的值以及 `cd` 内置命令的效果。在你执行不带参数的 `cd` 后，工作目录的路径与 `HOME` 的值相同：即你的主目录。

shell 使用 `HOME` 的值来展开使用波浪号（`~`）简符号（见第 193 页）表示用户主目录的路径。以下示例使用 `echo` 显示此快捷的值，然后使用 `ls` 列出 Max laptop 目录中的文件，该目录是他主目录的子目录。

```bash
$ echo ~
/home/max
$ ls ~/laptop count lineup
tester
```

### PATH：shell 查找程序

当你提供绝对或相对路径而不是简单的文件名作为命令时，shell 会指定的目录下查找可执行文件。如果路径文件不存在，shell 会报告未找到命令（command not found）。如果文件存在但你没有执行权限，或者对于 shell 脚本，你没有读取和执行权限，shell 会报告拒绝访问（Permission denied）。

如果你提供一个简单的文件名作为命令，shell 会在某些目录（你的搜索路径）中搜索你想执行的程序。它会在几个目录中查找与命令同名且你拥有执行权限（编译后的程序）或读取和执行权限（shell 脚本）的文件。`PATH` 控制着这种搜索。

`PATH` 的默认值是在 bash 编译时确定的。它没有在启动文件中设置，尽管可能会被修改。通常，shell 默认搜索系统目录来查找常用命令。系统目录包括 `/bin` 和 `/usr/bin` 以及适用于本地系统的其他目录。当你给出命令时，如果对于 shell 脚本，在 `PATH` 列出的任何目录中找到了以命令命名的可读文件，shell 将生成上述错误消息之一。

`PATH` 变量指定了 shell 搜索目录的顺序。每个目录之间用冒号分隔。以下命令设置 PATH 以便搜索可执行文件：

### 表格 9-4 PS1 符号

| 符号 | 在提示符中的显示 |
|---|---|
| `\$` | 如果用户以 root 权限运行，显示为 #；否则为 $ |
| `\w` | 工作目录的路径 |
| `\W` | 工作目录的基名（basename） |
| `\!` | 当前事件（历史）编号（第 324 页） |
| `\d` | “星期 月 日”格式的日期 |
| `\h` | 机器主机名，不包含域名 |
| `\H` | 完整的机器主机名，包含域名 |
| `\u` | 当前用户的用户名 |
| `\@` | 12 小时制、AM/PM 格式的当前时间 |
| `\T` | 12 小制 HH:MM:SS 格式的当前时间 |
| `\A` | 24 小制 HH:MM:SS 格式的当前时间 |
| `\t` | 24 小制 HH:MM:SS 格式的当前时间 |

### PS2：用户提示符 (SECONDARY)

`PS2` 变量持有次要提示符。在命令的第一行，未加引号的字符串跟随 `echo`。shell 假设命令尚未结束并给出次要提示符（`>`）。此提示符表示 shell 正在等待用户继续，直到引号关闭字符串并执行命令：

```
$ echo "demonstration of prompt string\n> 2"
demonstration of prompt string
2
$ PS2="secondary prompt: "
$ echo "this demonstrates\nsecondary prompt: prompt string 2"
this demonstrates
prompt string 2
```

第二个命令将次要提示符改为 secondary prompt: 空。多行 echo 显示一个新的提示符。

### PS3：菜单提示符

`PS3` 变量持有 `select` 控制结构的菜单提示符（第 1000 页）。

### PS4：调试提示符

`PS4` 变量持有调试符号（第 982 页）。

### IFS：分隔字段（单词分割）

`IFS`（内部字段分隔符）变量指定了用于分离命令行参数的字符。它的默认值为空格制表符。无论 `IFS` 的值如何，你始终可以使用一个或多个空格或制表符来分隔命令行参数，只要这些字符没有被引用或转义。当赋值 `IFS` 值时，这些字符也可以分隔字段——但只有在经过展开的情况下。这种命令行解释类型被称为单词分割。

#### 更改 IFS 时小心

更改 `IFS` 有多种副作用，请谨慎操作。你可能会发现，更改之前保存 `IFS` 的值很有用。或者，如果你遇到了意想不到的结果，可以使用 bash 命令进入一个新 shell；然后退回到旧的 shell，此时 `IFS` 恢复正常工作。以下示例演示了 `IFS` 如何影响命令行的解释：

```
$ a=w:x:y:z
```

```
$ cat
cat: w:x:y:z 没有这样的文件或目录
$ IFS=":"
```

```
$ cat
cat: w 没有这样的文件或目录
cat: y 没有这样的文件或目录
cat: z 没有这样的文件或目录
```

在在第一次调用 `cat` 时，shell 扩展变量 `a`，将字符串 wxyz 解释为单个单词作为 `cat` 的参数。该工具找不到名为 wxyz 的文件，并报告文件名错误。如果 `IFS` 设置为冒号（`:`），shell 将变量扩展为四个单词，每个单词都是 `cat` 的参数。现在 `cat` 报告文件不存在：w、y 和 z。基于冒号（`:`）的单词分割仅在变量 `a` 扩展后发生。

shell 根据 `IFS` 中找到的分隔符分割所有单词。当没有展开时，就不会分割。考虑以下命令：

```
$ IFS+="p"
$ export VAR
```

尽管 `IFS` 被设置为 `p`，但 `export` 命令行中的 `p` 没有被展开，因此单词 `export` 不会被分割。

以下示例使用变量展开来尝试产生 `export` 命令：

```
$ IFS="p"
$ aa=export
$ echo $aa
export
```

这次发生了展开，因此 `export` 命令行中的 `p` 被解释为分隔符（如 `echo` 命令）。现在当你尝试使用 `aa` 变量的值来导出 `VAR` 变量时，shell 将命令行解析为 `export VAR`。结果是命令带有两个文件名启动 `export`：

```
$ aa VAR
2 个文件待编辑
进入编辑模式。输入 "visual" 进入普通模式。
```
