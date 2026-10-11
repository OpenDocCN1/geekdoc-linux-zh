
`if ($reply == "yes") then` # 检查精确匹配

  `echo` you entered yes

`else if ($reply =~ y*) then` # 检查不精确匹配

  `echo` I assume you mean yes

`endif`

`% tcsh expr1.csh` ...执行脚本。

do you like the C shell?

yeah

`% _`

```
```

### 8.4.2 算术表达式

C shell 支持图 8–10 所示的算术运算符，按优先级降序排列。

| 运算符 | 含义 |
| --- | --- |
| - | 一元负 |
| ! | 逻辑非 |
| * % | 乘法、除法、取余 |
| + - | 加法、减法 |
| << >> | 位左移、位右移 |
| <= >= | 关系运算符 |
| == != | 等于、不等于 |
| & ^ | 位与、位异或 |
| || | 逻辑或、逻辑与 |

**图 8–10** C 语言的算术运算符。

算术表达式的工作方式与其对应版本类似，但它们只能对整数进行操作。表达式可以用括号括起来，以防止 shell 特殊解释这些字符。当评估算术表达式时，空字符串等同于零。

```
% cat expr3.csh ...列出脚本。

#

set a = 3

set b = 5

if ($a > 2 && $b > 4) then

  echo expression seems to work

endif

% tcsh expr3.csh ...执行脚本。

expression seems to work

% _
```

### 8.4.3 面向文件的表达式

为了让面向文件的决策编程更简单，C shell 支持几种特定的文件表达式。每个表达式的格式如图 8–12 所示。

```
-option filename

如果所选选项为真，则返回 1 (真)，否则返回 0 (假)。如果 fileName 不存在或不可访问，所有选项都返回 0。
```

**图 8–12** C shell 面向文件表达式的描述。

图 8–13 描述了每个选项。

| 选项 | 含义 |
|---|---|
| r | shell 拥有读权限 |
| w | shell 拥有写权限 |
| x | shell 拥有执行权限 |
| e | fileName 存在 |
| o | fileName 由相同用户所有 |
| z | fileName 大小为零 |
| f | fileName 是普通文件 |
| d | fileName 是目录 |

**图 8–13** 用于文件表达式的选项。

这是一个使用 `-w` 选项来判断文件是否可写的示例脚本：

```
% cat expr4.csh ...列出脚本。

#

echo -n "the name of the file you wish to erase: "

set filename = $< # 获取一行输入。

if (! -w "$filename") then # 检查是否有权限

  echo you do not have permission to erase.

else

  rm $filename

  echo file erased

endif

% tcsh expr4.csh ...执行脚本。

enter the name of the file you wish to erase: you do not have permission to erase that file.

% _
```

## 8.5 文件名补全

与 Korn shell 一样，C shell 提供了一种避免在命令行中输入完整文件名的方法。每当你输入文件名的一部分时，按下 Tab 键可以唯一识别文件；如果你输入的文本已经可以唯一识别文件，则会自动添加剩余部分。如果文本不能唯一识别文件，则会填充所有可能的结果（即所有候选项）。你也可以输入 Control-D 查看匹配当前输入部分的文件列表。例如：

```
% ls -al .
```

## 8.6 命令编辑

大多数命令行 shell 都提供简单的方法回溯和编辑已执行的命令。原始 C shell 不提供这种功能，但 tsh 提供。回溯命令最简单的方法是按下键盘上的向上箭头。这会将最近一次输入的命令带到命令行。你可以向上移动并修改，按下回车键执行命令，或再次按下向上箭头在列表中回移动。

## Shell 命令: `alias [word [string]]`

`alias` 支持简单的命令行自定义形式。如果你将 `word` 别名为等于 `string`，并在稍后输入一个以 `word` 开头的命令，则 `word` 的第一个出现处将被替换为 `string`，然后对该命令进行重新处理。

如果你不提供 `word` 或 `string`，将显示所有 shell 别名（aliases）的列表。如果你只提供 `word`，则会显示与该别名 `word` 当前关联的 `string`。如果你同时提供 `word` 和 `string`，shell 将将指定的别名添加到其别名集合中。如果 `word` 已经存在一个同名同的别名，则它将被替换。

如果替换字符串以 `word` 开头，则不会对其进行别名重处理，以防止无限循环。如果替换字符串在其他地方包含 `word`，则在执行别名时会显示错误信息。

**图 8–14** `alias` shell 命令的描述。

以下是 `alias` 的用法示例：

```
$ alias dir 'ls -aF' ...注册一个别名。
$ dir ...等于输入 "ls -aF"
./ main2.c p.reverse.c reverse.h
./ main2.o palindrome.c reverse.old
$ dir *c ...等于输入 "ls -aF *.c"
main2.c p.reverse.c palindrome.c
$ alias dir ...查看与 "dir" 关联的值
ls -aF
$ _
```

在下面的示例中，我将一个词别命名为了它自身：

```
% alias ls 'ls -aF' ...将 "ls" 定义为自身。
% ls *c ...等于输入 "ls -aF *.c"
main2.c p.reverse.c palindrome.c
% alias dir 'ls' ...将 "dir" 定义为 "ls"
% dir ...等于输入 "ls -aF"
./ main2.c p.reverse.c reverse.h
./ main2.o palindrome.c reverse.old
% alias who 'date; who' ...无限循环问题。
% who ...
Alias loop.
% alias who 'date; /usr/bin/who' ...使用全路径避免错误
% who ...现在工作正常了。
Fri May 13 23:33:37 CST 205
glass ttyp0 Feb 13 23:30 (xyplex2)
% _
```

## 8.7 • 别名 (Aliases)

### 8.7.1 删除别名

要删除别名，请使用内置命令 `unalias`（图 8–15）。

```
Shell 命令: unalias pattern
unalias 移除所有匹配 pattern 的别名。如果 pattern 为 *，则移除所有别名。
```

**图 8–15** `unalias` shell 命令的描述。

### 8.7.2 有用的别名

图 8–16 列出了我保留在 “.tcshrc”文件中的有用别名列表，并带有简要描述。

| 别名 | 值 |
| --- | --- |
| cd | `cd \!; set prompt="$cwd > ";` 这更改你的提示符，使其包含当前工作目录和上一个命令编号（更多详情请查看历史）。 |
| ls | `ls -F` 这会让 `ls` 包含额外的文件信息。 |
| rm | `rm -i` 这会让 `rm` 询问确认。 |
| rm | `mv \* /tomb` 这会让 `rm` 将文件移动到特殊的“tomb”目录而不是删除它。 |
| h | `history` 这允许你通过仅输入一个字母获取历史信息。 |
| vim | `(mesg n:/usr/bin/vim\; msg y)` 这阻止别人在你处于 `vim` 编辑器时发送消息。 |
| mroe | `more` 这纠正了一个常见的拼写错误。 |
| ls-l | `ls -l` 这纠正了一个常见的拼写错误。 |
| ll | `ls -l` 这让你更方便地获取详细目录列表。 |

**图 8–16** 有用的 C shell 别名。

### 8.7.3 共享别名

要让别名对子 shell 可，请将其定义放在 shell 的 “.tcshrc”文件中。

### 8.7.4 参数化别名
