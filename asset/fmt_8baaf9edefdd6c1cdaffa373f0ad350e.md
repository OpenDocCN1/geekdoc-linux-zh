
### EXPLANATION

- 1 The variable name is assigned the value null.
- 2 The special modifier `:=` will check to see if the variable name has been set. If it has been set, it will not be changed; if it is either null or not set, it will be assigned the value to the right of the equal sign. Patty is assigned to name because the variable is set to null. The setting is permanent.
- 3 The variable name still contains the value Patty.
- 4 The value of the variable EDITOR is set to `/bin/vi`.
- 5 The value of the variable EDITOR is displayed.

# 示例 7.27

```
*(Assigning temporary alternate values)

1  $ foo=grapes

2  $ echo ${foo:+pears}

   pears

3  $ echo $foo

   grapes

   $
```
# 解释

- 1. 变量 `foo` 已被赋值为 `grapes`。
- 2. 特殊修饰符 `+` 会检查变量是否已设置。如果已设置，则 `pears` 将临时替代 `foo`；如果未设置，则返回 null。
- 3. 变量 `foo` 现在具有其原始值。

# 示例 7.28

```
*(Creating error messages based on default values)

1  $ echo ${name:?"name is undefined"}

   name: name is undefined

2  $ echo ${y:?}

   y: parameter null or not set
```
# 解释

- 1. `?` 修饰符会检查变量是否已设置。如果未设置，则 `?` 右侧的字符串会连同变量名一起打印到标准错误。如果在脚本中，脚本会退出。
- 2. 如果在 `?` 之后未提供消息，shell 会向标准错误发送默认消息。

#### 7.6.7 位置参数

通常，特殊内置变量，通常称为位置参数，用于在 shell 脚本中传递命令行参数，或在函数中保存传递给函数的参数的值。参见表 7.6。变量被称为位置参数，因为它们由其在命令行上的位置表示。Bourne shell 允许最多九个位置参数。shell 脚本的名称存储在 `$0` 变量中。位置参数可以用 `set` 命令设置和重置。

# 表 7.6 Bourne Shell 位置参数

| 位置参数 | 含义 |
|---|---|
| `$0` | 引用当前 shell 脚本的名称 |
| `$1-$9` | 表示位置参数 1 到 9 |
| `$#` | 计算为位置参数的数量 |
| `$@` | 计算为所有位置参数 |
| `$0` | 与 `$@` 相同，除了在双引号中时 |
| `"$*"` | 计算为 `"$1 $2 $3"` |
| `"$@"` | 计算为 `"$1"` `"$2"` `"$3"` |

# 示例 7.29

```
1  $ set tim bill ann fred

$ echo $*  # Prints all the positional parameters.

tim bill ann fred

2  $ echo $1  # Prints the first positional parameter.

tim

3  $ echo $2 $3  # Prints the second and third positional parameters.

bill ann

4  $ echo $#  # Prints the total number of positional parameters.

4

5  $ set a b c d e f g h i j k l m

$ echo $10  # Prints the first positional parameter followed by a zero.

a0

6  $ echo $@

a b c d e f g h i j k l m

7  $ set file1 file2 file3

$ echo \$$#

$3

8  $ eval echo \$$#

file3
```
# 解释

- 1 `set` 命令为位置参数分配值。`$*` 特殊变量包含所有已设置的参数。
- 2 显示第一个位置参数 `tim` 的值。
- 3 显示第二个和第三个参数 `bill` 和 `ann` 的值。
- 4 `$#` 特殊变量包含当前设置的位置参数的数量。
- 5 `set` 命令重置所有位置参数。原始设置被销毁。位置参数不能编号超过九。打印第一个位置参数的值，后跟数字 0。
- 6 `$` 允许你打印所有参数，即使超过九个。
- 7 位置参数被重置为 `$1`、`$2`、`$3` 和 `$n`。美元符号被转义；`$#` 是参数的数量。`echo` 命令显示 `$$`。
- 8 `eval` 命令在执行命令之前第二次解析命令行。第一次解析时，shell 将 `$$` 替换为 `$3`，第二次解析时，shell 将 `$3` 的值替换为 `$1 $3`。

# 7.6 变量

#### 7.6.8 其他特殊变量

shell 具有由单个字符组成的特殊变量。在字符前加上美元符号即可访问变量中存储的值。参见表 7.7。

| 变量 | 含义 |
| --- | --- |
| `$` | shell 的 PID |
| `-` | 当前设置的 sh 选项 |
| `?` | 最后执行的命令的退出值 |
| `!` | 最后放入后台的作业的 PID |

```
1 $ echo The pid of this shell is $$

The pid of this shell is 4725

2 $ echo The options for this shell are $-

The options for this shell are s

3 $ grep dodo /etc/passwd

$ echo $?

4 $ sleep 2&

4736

$ echo $!

4736
```
- 1 `$` 变量保存此进程的 PID 值。
- 2 `-` 变量列出此交互式 Bourne shell 的所有选项。

### EXPLANATION (CONTINUED)

3 `grep` 命令在 `/etc/passwd` 文件中搜索字符串 `dodo`。`?` 变量保存上一个执行的命令的退出状态。因为 `grep` 返回的值为 1，所以认为 `grep` 在搜索中失败了。退出状态 0 表示成功退出。

4 `!` 变量保存上一个放到后台的命令的 PID 号。附加到 `sleep` 命令的 `&` 将命令发送到后台。

# 7.7 Quoting

引用用于保护特殊元字符不被解释。有三种引用方法：反斜杠、单引号和双引号。表 7.8 中列出的字符对 shell 来说是特殊的，必须加引号。

### Table 7.8 Special Metacharacters Requiring Quotes

| Metacharacter | Meaning |
|---|---|
| `;` | 命令分隔符 |
| `&` | 后台处理 |
| `( )` | 命令分组；创建子 shell |
| `{ }` | 命令分组；不创建子 shell |
| `|` | 管道 |
| `<` | 输入重定向 |
| `>` | 输出重定向 |
| `newline` | 命令终止 |
| `space/tab` | 单词分隔符 |
| `$` | 变量替换字符 |
| `* [ ] ?` | Shell 用于文件名扩展的元字符 |

单引号和双引号必须匹配。单引号保护特殊元字符，如 `$`、`*`、`?`、`!`、`>` 和 `<`，不被解释。双引号也保护特殊元字符不被解释，但允许变量和命令替换字符（美元符号和反引号）被处理。单引号会保护双引号，双引号会保护单引号。

# 7.7 Quoting

Bourne shell 不会让你知道引号是否不匹配。如果交互运行，当引号不匹配时会出现二级提示。如果在 shell 脚本中，文件会被扫描，如果引号不匹配，shell 会尝试用下一个可用的引号匹配它；如果 shell 无法用下一个可用的引号匹配它，程序会中止，并在终端上出现 'end of file' unexpected 消息。对即使是最好的 shell 程序员来说，引号也可能是一个真正的麻烦！请参阅第 985 页的“关于引号你应该知道的内容”了解 shell 引用的规则。

#### 7.7.1 The Backslash

反斜杠用于引用（或转义）单个字符，使其不被解释。反斜杠在单引号中放置时不被解释。如果反斜杠被双引号包围，它会保护美元符号（`$`）、反引号（`` ` ``）和反斜杠本身不被解释。

# EXAMPLE 7.31
```
