
```bash
setenv mail /var/spool/mail/$user
if ( -z $DISPLAY ) then
    setenv TERM vt100
else
    setenv TERM xterm
endif
stty erase '^H' kill '^Au' -lcase tab3
date '+%A %B %d at %I:%M %p'
```

上述 `.login` 文件通过设置 `TERM` 变量来确立你正在使用的终端类型（通过第 368 页的语句判断你是否正在使用图形界面，从而决定给 `TERM` 赋值什么值）。随后它运行 `getty`（第 778 页）来设置终端特性，并运行 `date`（第 630 页）显示你登录的时间。

`/etc/csh.login` 当你和 `.logout` 退出系统时，TC Shell 会按顺序运行 `/etc/csh.login` 和 `~/logout` 文件。接下来的示例 `.logout` 文件使用 `date` 命令来显示你退出的时间。`sleep` 命令确保 `echo` 在系统注销你之前有时间显示消息。对于需要一些时间来显示消息的拨号链路，这种延迟可能很有用。

```bash
tcsh $ cat ~/.logout
date '+Login on %A %B %d at %I:%M %p'
sleep 5
```

## BOURNE AGAIN 和 TC SHELL 的共同特征

`bash` 和 `tsh` 大多数共同特征都源于原始的 C Shell：

- 命令行扩展（也称为替换；第 344 页）
- 历史记录（第 344 页）
- 别名（第 347 页）
- 作业控制（第 348 页）
- 文件名替换（第 348 页）
- 目录栈操作（第 349 页）
- 命令替换（第 349 页）

由于 `bash` 章节详细讨论了这些特征，本节重点关注 `bash` 和 `tsh` 实现之间的差异。

## 命令行扩展（替换）

请参阅第 322 页的“处理命令行”以了解 Bourne Again Shell 中的命令行扩展。`tcsh` 的手册页使用“substitution”（替换）一词，而不是 `bash` 使用的“expansion”（扩展）。TC Shell 按照以下顺序扫描每个标记以进行可能的扩展：

1. 历史记录替换（第 344 页）
2. 别名替换（第 347 页）
3. 变量替换（第 356 页）
4. 命令替换（第 349 页）
5. 文件名替换（第 348 页）
6. 目录栈替换（第 349 页）

## 历史记录

TC Shell 为每个命令行分配一个顺序事件编号。你可以将此事件编号作为 `tcsh` 提示符的一部分显示（参见第 363 页的“prompt”）。本节中的示例显示了带编号的提示符，这有助于说明命令的行为。

### history 内置命令

与 `bash` 一样，`tcsh` 内置命令 `history` 显示历史列表中的事件。事件列表顺序排序，最旧的事件在顶部。历史列表中的最后一个事件是显示列表的 `history` 命令。在接下来的历史列表中（通过 `history` 命令的参数 `10` 将其限制为十行），命令 `23` 修改了 `tcsh` 提示符以显示历史事件编号。每个命令执行的时间显示在事件编号的右侧。

```bash
32 $ history 10
23 23:59 set prompt = "! $ $$
24 23:59 is = -1
25 23:59 cat temp
26 00:00 rm temp
27 00:00 vim memo
28 00:00 lpr memo
29 00:00 vim memo
30 00:00 lpr memo
31 00:00 rm memo
32 00:00 history
```

### 历史记录扩展

相同的事件和单词标识符在两种 shell 中均有效。例如，`!!` 在 `tcsh` 中指代上一个事件，就像在 `bash` 中一样。命令 `!1328` 执行编号为 `328` 的事件，而 `!$txt` 执行包含字符串 `txt` 的最新事件。

更多信息请参阅第 300 页的“使用感叹号 (!) 引用事件”。表 9-1 列出了 `bash` 中未找到的少量 `tcsh` 单词修饰符。

#### 表 9-1 单词修饰符

| 修饰符 | 功能 |
| --- | --- |
| `u` | 将第一个小写字母转换为大写 |
| `l` | 将第一个大写字母转换为小 |
| `a` | 在单词内全局应用下一个修饰符 |

你可以在命令中使用多个单词修饰符。例如，修饰符结合 `u` 或 `l` 修饰符，可以让你更改整个单词的大小写。

```bash
tcs echo $ VERSION
VERSION: Undefined variable.
tcs echo !!1:al
echo Version
tcs 6.12.00 (Astron) 2002-07-23 (1386-intel-linux) options 8b,nls,...
```

除了在 `tsh` 中使用事件标识符访问历史列表外，你还可以使用命令行编辑器来访问、修改和执行之前的命令（第 353 页）。

## 变量

你在 `tsh` 中用于控制历史记录的变量与 `bash` 不同。

#### 表 9-2 历史记录变量

| 变量 | 默认值 | 功能 |
| --- | --- | --- |
| `history` | `500` | 会话期间最大事件数 |
| `historyfile` | `~/.history` | 历史记录文件的位置 |
| `savehist` | unset | 会话之间的最大事件数 |

如果你想在命令编号 `250` 后面添加 `w`，可以使用大括号隔离该数字：

```bash
!{250}w
```

### 别名中的历史替换

你可以使用历史机制来替换命令行参数，其中单个感叹号表示包含该别名的命令行。修饰符与 `history` 使用的修饰符相同（第 300 页）。在接下来的示例中，感叹号被引号起来，这样 shell 在构建别名时就不会对其进行解释：

```
$1 alias last echo \:\n$2 last this is just a test
test
$3 alias fn2 \:2:t
$4 alias fn2 /home/jenny/test /home/alex/home/barbara/new
temp
```

事件 `21` 为 `last` 定义了一个别名，显示最后一个参数。事件 `23` 为 `fn2` 定义了一个别名，用于显示命令行上第二个参数的简单文件名或尾部（tail）。

## 作业控制

作业控制在 `bash`（第 271 页）和 `tsh` 中都很相似。你可以在前台和后台之间移动命令，临时挂起作业，并获取当前作业列表。字符 `%` 在后面跟随作业号或唯一标识该作业的字符串前缀时引用该作业。当你从每个 shell 在后台运行多进程命令行时，你会发现细微的：`bash` 仅显示每个作业中最后一个后台进程的 PID 号，而 `tsh` 显示属于一个作业的所有进程数字。第 271 页的示例如下：

```
tsh $ find -print | sort | lpr & grep -1 alex /tmp/* auxfiles &
[1] 18839 18840 18841
[2] 18876
```

## 文件名替换

TC Shell 如 `bash` 一样展开路径中的字符 `*`、`?` 和 `[]`（第 127 页）。`*` 匹配零或多个字符的任意字符串，`?` 匹配任意单个字符，`[]` 定义字符类，用于匹配括号内的字符。

TC Shell 以 `bash` 相同的方式将以波浪号 (`~`) 开头的命令行参数展开文件名（第 351 页），`~` 代表用户的家目录或波浪号后跟随用户的家目录。`bash` 的特殊扩展 `+` 和 `--` 在 `tsh` 中不可用。

`tsh` 支持大括号扩展（第 324 页）。与波浪号扩展一样，它被视为文件名替换的一个方面，尽管大括号扩展可以生成并非实际文件名的字符串。

## 操作目录栈

`tsh` 中的目录栈操作与 `bash`（第 274 页）没有太大区别。内置命令 `dirs` 显示栈的内容，而 `pushd` 和 `popd` 内置命令将目录推入栈中或从栈中弹出目录。

## 命令替换

`tsh` 不支持 `$(...)` 格式的命令替换。取而代之的是你必须使用原始的反引号格式。否则，`bash` 和 `tsh` 的实现是相同的。关于命令替换的更多信息，请参考第 329 页。

## 重定向标准错误

`bash` 和 `tsh` 都使用大于符号 (`>`) 来重定向标准输出，但 `tsh` 不使用 `bash` 的符号 `2>` 来重定向标准错误。在 `tsh` 下，你使用大于符号后跟一个符号 (`&`) 来合并并重定向标准输出和标准错误。虽然在 `bash` 下可以使用这种符号，但并不常见。以下示例类似于第 261 页的 `bash` 示例，引用了不存在的文件 `x` 和包含单行的文件 `y`。

```
tsh $ cat x
cat: x: No such file or directory
tsh $ cat y
This is y.
tsh $ cat x y & hold
tsh $ cat hold
cat: x: No such file or directory
This is y.
```

在上述示例中，参数为 `y` 时，`cat` 将字符串发送到标准输出。参数 `y` 会导致 `cat` 将错误消息发送到标准错误。

与 `bash` 不同，`tsh` 没有提供一种从标准输出单独重定向标准错误的简单方法。一种变通方法提供了合理的解决方案。

```
tsh $ cat x
cat: x: No such file or directory
tsh $ cat y
This is y.
tsh $ cat x y & hold
tsh $ cat hold
cat: x: No such file or directory
This is y.
```

## 使用命令行

本节涵盖了单词补全、编辑命令行和拼写检查。

### 单词补全

TC Shell 在你输入 `TAB` 时补全命令行上的文件名、命令和变量名。这些功能的通用术语是单词补全。

#### 波浪号补全

解析单词第一个字符出现的波浪号 (`~`)，并在输入 `TAB` 时将其展开为用户名：

```
tsh $ cd -al → TAB → cd -alex/ → RETURN
tsh $ pwd
/home/alex
```

通过附加斜杠 (`/`)，`tsh` 表示完成的单词是一个目录。斜杠也方便继续指定路径。

#### 文件名补全

TC Shell 在你指定前缀后可以补全文件名。`tsh` 会补全名称并添加空格，留下光标输入额外的参数或按回。在下面的示例中，用户输入命令 `cat` 并按下 `TAB`；系统将补全以以下开头的文件名：

```
tsh $ cat trig1
```

如果多个文件名匹配你输入的前缀，`tsh` 无法在没有更多信息的情况下补全文件名。shell 会尝试通过添加字符来尽可能增加前缀的长度，然后报错，直到需要额外的输入来消除歧义：

```
tsh $ ls h
help.hist help.trig01 help.txt
tsh $ cat h → TAB → cat help. (beep)
```

你可以输入足够的字符来消除歧义，然后再次按下 `TAB`。或者，你可以按下 `CONTROL-D` 使 `tsh` 显示匹配的文件列表：

```
tsh $ cat help. → CONTROL-D
help.hist help.trig01 help.txt
tsh $ cat help.
```

在显示文件名后，`tsh` 会重绘命令行，让你消除歧义（并再次按下 `TAB`）或手动完成文件名。

#### 命令和变量补全

你可以使用列出和补全文件名的机制来处理命令和变量名。除非给出完整路径，否则 shell 将使用变量 `path` 来尝试补全命令名。列出的选项可能位于不同的目录。

```
tcsh $ up → TAB (哔声) → CONTROL-O
update2 updatedb uptime
update2-config update-mime-database
update2-nox updmap
tcsh $ up → t → TAB → uptime → RETURN
9:59am 31 days, 15:11, 7 users, load average: 0.03, 0.02, 0.00
```

如果你在下面的示例中设置了 `autolist` 变量，当你通过 `TAB` 触发补全时，shell 会自动列出选项。你不需要按 `CONTROL-D`。

```
tcsh $ set autolist
tcsh $ up → TAB (哔声)
update2 updatedb
update2-config update-mime-database
update2-nox updmap
tcsh $ up → t → TAB → uptime → RETURN
10:01am 31 days, 15:14, 7 users, load average: 0.20, 0.06, 0.02
```

如果你设置了 `autolist-ambiguous`，当你按下 `TAB` 时，如果输入的单词是命令的最长前缀，shell 会列出选项。否则，按下 `TAB` 会导致 shell 向命令添加一个或多个字符，直到它成为最长前缀；再次按下 `TAB` 则会列出选项：

```
tcsh $ set autolist-ambiguous
tcsh $ echo sh → TAB (哔声)
histfile history
tcsh $ echo sh → i → TAB → echo shist → TAB
histfile history
tcsh $ echo shist → o → TAB → echo shistory → RETURN
1000
```

shell 必须依赖单词在输入行中的上下文来判断它是用户名、命令还是变量名。输入行的第一个单词被假认为是命令名；如果一个单词以特殊字符 `$` 开头，则它被视为变量名；依此类推。在接下来的示例中，第二个命令没有正常工作：该单词的上下文使其看起来像文件名的开头，而不是命令的开头。TC Shell 为 `which` 命令以 `updates`（一个不可执行文件）作为参数，并显示错误消息：

```
tcsh $ ls *\updates
tcsh $ which updatedb ups uptime
/usr/bin/updatedb
/usr/local/bin/ups
/usr/bin/uptime
tcsh $ which up → TAB → which updates
updates: Command not found.
```

### 编辑命令行

`bindkey` 的命令行编辑功能类似于 `bash` 下提供的功能。你可以使用 `emacs` 模式命令（默认）或 `vi` 模式命令。使用 `bindkey -v` 切换到 `vi` 模式命令，使用 `bindkey -e` 切换到 `emacs` 模式命令。箭头键在两种模式下都绑定了明显的移动命令，你可以在历史列表中上下移动（前后移动），也可以在当前命令行上左右移动。

在不带参数的情况下，`bindkey` 内置命令显示编辑器命令与你可以在键盘上输入的键序列之间的当前映射：
