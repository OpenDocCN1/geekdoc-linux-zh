
## 15.4.3 Common Error Messages from the Big 5 Shells

当你运行脚本时，shell 会报告多种不同类型的语法错误。每个 shell 通过向标准错误发送消息来报告这些错误，并且消息因 shell 而异。例如，C shell 非常啰嗦，会在错误发生的同一行报告未匹配的引号和未定义变量等错误，而 Bourne shell 的错误消息则稀少且相当晦涩。调试 Bourne shell 脚本通常非常困难，因为错误直到脚本完全解析后才会被报告，而且当你收到错误消息时，它可能不会提供任何帮助来理解你的错误。

由于每个 shell 都有自己的错误报告风格，表 15.3 至 15.6 说明了最常见的语法错误、可能的原因、错误消息的含义以及简单的修复方法。

## Common C/TC Shell Error Messages

mimics the C shell errors so closely so the chart serves to address both shells.

### Table 13.3 Common C/TC Shell Error Messages

| Error Message | What Caused It | What It Means | How to Fix It |
|---|---|---|---|
| " : Event not found. | `echo "Now"` | 感叹号（历史字符）必须转义。引号无法保护它。 | `echo 'Now!'` |
| @: Badly formed number. | `set n = 5; @ n = 3 + 4` | 只能对整数执行算术运算，且算术运算符周围必须有空格。 | `set n = 5; @ n = 3 + 4` |
| @++: Command not found. | `@n++` | `@` 符号后面必须跟一个空格。 | `@ n++` |
| Ambiguous. | `` `date` `` | 反引号用于命令替换，当命令的输出被赋给变量或成为字符串的一部分时使用。如果命令单独占一行，则不应将其括在反引号中。TCB 会给出“Command not found”错误。 | `echo `date`` or `set d = `date`` |
| Bad : modifier in $ f(). | `echo $ode:f` | `:f` 是一个无效的路径名扩展修饰符。 | `echo $ode:t` |
| Badly placed `()`. | `echo (abc)` | 括号用于启动子 shell。整个命令应放在 `()` 中或字符串应被引用。 | `echo "(abc)"` or `( echo abc )` etc. |
| echo: No match. | `echo How are you?` | 问号是 shell 元字符，用于文件名扩展。它代表文件名中的一个字符。shell 会将 you 后跟单个字符 `?` 匹配到名为 you? 的字符，或如果没有该名称的文件，则显示 No match 错误。 | `echo How are you?` or `echo How are you?` |

## 表 15.3 常见 C/Shell 错误信息（续）

| 错误信息 | 原因 | 含义 | 如何修复 |
|---|---|---|---|
| Too many 's | `if $x = $y && $x != 3 ) then` | 表达式存在不平衡的括号。要么添加右侧部分，要么在 `(` 后移除 `&&` | `if ( $x = $y && $x != 3 ) then` or `if $x = $y && $x != 3 ) then` |
| top: label not found. | `goto top` | `goto` 命令正在查找名为 `top` 的标签，该标签应单独占一行出现在程序中的某处。要么该标签本身存在但拼写不同。 | `top:` `goto top` |
| undefined variable | `echo $name` | 变量 `name` 从未被设置。 | `set name = "John"; set name = $name` |
| unmatched " | `echo "She said, "Hello"` | 双引号必须在同一行匹配。 | `echo "She said, "Hello"` |
| unmatched ' | `echo 'I don't care'` | 单引号必须在同一行匹配。 | `echo 'I don't care'` |
| while: Expression syntax. | `while ( $n <= 5 )` | 使用了错误的运算符。应为 `<=` | `while ( $n <= 5 )` |

### 表 15.4 常见 Bourne Shell 错误信息。

常见 Bourne Shell 错误信息

表 15.4 列出了常见 Bourne shell 错误信息。

### 表 15.4 常见 Bourne Shell 错误信息

| 错误信息 | 原因 | 含义 | 如何修复 |
|---|---|---|---|
| (file): syntax error near 'case' | `case "blue"` | `case` 命令缺少 `in` 关键字。 | `case $color in` |
| (file): syntax error near 'case' | `case $color` | 变量不存在或为空。 | `name="some value"` |
| (blank line): no error message. | `blank line` | `{` 后面必须有一个空格 | `if [ $USER = "elfie" ] ; then` |
| [elfie]: not found | `if [ $USER = "elfie" ] ; then` | 等号两侧不能有任何空格。 | `answer="Yes"` |
| answer: not found | `answer = "Yes"` | | |

### 表 15.4 常见 Bourne Shell 错误信息（续）

| 错误信息 | 原因 | 含义 | 如何修复 |
|---|---|---|---|
| cannot shift | `shift 2` | `shift` 内建命令用于将位置参数左移。如果剩余的位置参数不足两个，`shift` 将失败。 | `set apples pears peaches; shift 2` (apples and pears will be shifted from the list) |

### 表 15.4 常见 Bourne Shell 错误信息（续）

| 错误信息 | 原因 | 含义 | 如何修复 |
|---|---|---|---|
| test: unknown operator Doe | `name="John Doe"` `if [ "$name" = "Joe" ]` | 测试表达式中变量名应使用双引号。`=` 运算符左侧只能有一个字符串，除非它被引用。 | `if [ "$name" = "Joe" ]` |
| trap: bad trap | `trap 'rm trap' 500 500` | `trap` 中的数字是非法信号。正常情况下信号 2 或 3 会被捕获。2 用于 Ctrl C，3 用于 Ctrl-\ 。这两个信号都会导致在 `trap` 命令之后命名的程序被终止。 | `trap 'rm trap' 2` |
| unexpected EOF or unexpected end of file | `echo "hi"` | shell 双引号在文件中未匹配。Bourne shell 将一直搜索到文件末尾寻找匹配的引号。你可能不会收到 unexpected EOF 错误信息，但程序输出将不会收到。如果 `case` 或循环命令未分别以其关键字 `esac` 和 `done` 结束，将会发生错误信息。 | `echo "hi"` |

表 15.5 列出了常见 Korn shell 错误信息。

### 表 15.5 常见 Korn Shell 错误信息

| 错误信息 | 原因 | 含义 | 如何修复 |
|---|---|---|---|
| ./file: The 5: syntax error near `case $color' unexpected token `)' | `case $color in blue)` | 脚本中 `case` 命令缺少 `in` 关键字。 | `case "$color" in blue)` |
| filename: line2: syntax error at `)' line 6: unexpected | `case $color in blue echo "blue" red) echo "red" ;; esac` | 第一个 `case` 语句未在 `echo "blue"` 后以 `;` 终止。 | `case $color in blue) echo "blue" ;; red) echo "red" ;; esac` |

常见 Korn Shell 错误信息。

# 表 15.5 常见的 Korn Shell 错误信息（续）

## 15.4 语法错误的可能原因

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| [空白行] | `echo $name` 或 `echo ${fruit[5]}` | 变量不存在或为空。 | `name="Some value"` |
| file2: line2: syntax error at line 6: `done' unexpected | `while (( $n < 5 )) do statements done` | `while` 缺少 `do` 关键字 | `while (( $n < 5 )) do statements done` |
| file: syntax error at line 3: unmatched | `print I don't care` | 脚本中单引号未匹配。应使用双引号括起来。 | `echo "I don't care"` 或 `echo 'I don't care'` |
| file: syntax error at line 3: unmatched | `print She said Hello` | 脚本中双引号未匹配。 | `print She said "Hello"` |
| ksh: [: Doe: unknown operator | `name="John Doe"; then if [ $name = Joe ]; then` 或 `if [[ $name == Joe ]]; then` | 变量 `name` 应在测试表达式中用双引号括起来。`=` 测试运算符的左侧只能有一个字符串。使用此运算符时不会使用其他替代方案。使用 `[` 或 `[[` 时单词会被拆分。 | `if [ "$name" = Joe ]; then` 或 `if [[ $name == Joe ]]; then` |
| ksh: [ellie: not found | `if [ $USER = "ellie" ]; then` `if [[ $USER = "ellie" ]]; then` | `[` 或 `[[` 运算符后面必须有空格。 | `if [ $USER = "ellie" ]; then` `if [[ $USER = "ellie" ]]; then` |
| ksh: apples: bad number | `set -a; apples pears peaches fruit` | `shift` 内置命令 `shift` 只能移动仅在 `shift` 命令中使用的位置参数。 | `set apples pears peaches fruit` |
| -ksh: file.exe-foo: not found | `file.exe-foo` | 变量名中不能包含句点。 | `file.exe-foo` |
| ksh: file: file already exists. | `sort file > temp` | `nodobber` 变量已设置且 `temp` 文件存在。 | `sort file > temp`（使用不同的输出文件）或 `sort file > temp`（覆盖 `nodobber`）或 `nodobber` 不允许你覆盖现有文件。 |

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| ksh: fred: unknown test operator if [ grey fred /etc/passwd ] ; then | `if [ grey fred /etc/passwd ] ; then` | `grep` 命令不应被方括号或其他符号包围。方括号仅用于测试表达式。`!` 是一个测试运算符。 | `if grep fred /etc/passwd ; then` |
| ksh: name: not found name = "Tom" | `name = "Tom"` | 没有空格可用于内置命令或用于移动位置参数。内置命令要么是等号。 | `set name "Tom"` |
| ksh: shift: bad number shift 2 | `shift 2` | `shift` 命令将移动 `apples` 和 `pears` 将从列表中移出。至少应有两个位置参数。如果不会则会失败。 | `apples 2` |
| ksh: syntax error: "echo hi" not expected | `function fun { echo "hi"; }` | 函数定义中大括号周围应有空格（`fun`）。分号将终止函数语句。 | `function fun { echo "hi"; }` |
| ksh: syntax error: "Doe" unexpected if [[ $name = "John Doe" ]] | `if [[ $name = John Doe ]]` | `=` 左侧不会执行单词拆分，但右侧的字符串必须加引号。 | `if [[ $name = "John Doe" ]]` |
| ksh: syntax error: "fi" unexpected if [ USER = "ellie" ] then or | `if [ USER = "ellie" ] then` or | `then` 应在下一行或前面加上分号。 | `if [ USER = "ellie" ] then` |
| ksh: syntax error: "then" unexpected if (( $a == $b )) | `if (( $a == $b ))` | 括住第二个表达式的括号不匹配。 | `if (( $a == $b ))` |
| ksh: trap: 500: bad trap trap 'm trap' 500 | `trap 'm trap' 500` | 数字 500 是非法的信号。通常在 shell 脚本中会捕获信号 2 或 3。2 用于 Ctrl-C，3 用于 Ctrl-Y。两者都会导致以 `trap` 命令命名的程序被终止。 | `trap 'm trap' 2` |

# 表 15.5 常见的 Korn Shell 错误信息（续）

a. 此错误在使用公共领域的 Korn shell 时出现，但 Korn shell 88（Solaris）不产生任何输出。

## 15.4 语法错误的可能原因

### 表 15.6 常见的 Bash Shell 错误信息。

表 15.6 列出了常见的 Bash shell 错误信息。

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| bash: syntax error: unexpected EOF while looking for matching `"` | `echo I don't care` | 脚本中单引号未匹配。 | `echo "I don't care"` |
| bash: syntax error: unexpected EOF while looking for matching `'` | `print She said "Hello"` | 脚本中双引号未匹配。 | `print She said 'Hello'` |
| [空白行] 无错误信息，无输出 | `echo $name` or `echo ${Fruit[5]}` | 变量不存在或为空。 | `name="some value"` or use `-d` to catch any variables that have not been set. The message will be printed later if the SET is sent to stderr. |
| bash: name: command not found | `name="Tom"` | 等号两侧不能有空格 | `name=Tom` |
| bash: 8.5: syntax error in expression (error token is ".5") | `declare -i num=8.5` | 只能为变量 `num` 分配整数值 | `num=6` |
| bash: [Ellie]: command not found | `if [[ $USER = "Ellie" ]]; then` or `if [[ $USER = "Ellie" ]]; then` | `[[` 后面必须有一个空格或 `[[` | `if [[ $USER = "Ellie" ]]; then` |
| bash: syntax error near unexpected token `fi' | `if [[ $USER = "Ellie" ]]; then` `if [[ $USER = "Ellie" ]]; then` `if [[ $USER = "Ellie" ]]; then` `if [[ $USER = "Ellie" ]]` | `then` 应该在下一行或前面加上分号 | `if [[ $USER = "Ellie" ]]; then` |
| bash: syntax error in conditional expression | `if [[ $name = "John Doe" ]]; then` | `=` 右侧不会进行单词拆分，但左侧的字符串必须加引号。 | `if [[ "$name" = "John Doe" ]]; then` |
| [: fret: binary operator expected | `if [ grep Fred /etc/passwd ]; then` | `grep` 命令不应被方括号或其他符号包围。方括号仅用于测试表达式。 `[` 是一个测试操作符。 | `if grep Fred /etc/passwd; then` |

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| `./file: line 5: syntax error near unexpected token \`blue\''`<br>`./file: line 5: \`blue\': unexpected` | `color="blue"`<br>`case $color in`<br>`blue)`<br>`echo "red"`<br>`;;`<br>`esac` | `case` 命令缺少 `in` 关键字。 | `case $color in` |
| `./file: line 12: syntax error at unexpected \\`\\`'` | `color="blue"`<br>`case $color in`<br>`blue)`<br>`echo "red"`<br>`;;`<br>`esac` | `case` 语句在 `blue` 后未以 `;;` 终止。 | 在每个 `case` 模式后添加 `;;`。 |
| `bash: shift: bad non-numeric arg \`fruit\''` | `declare -a fruit=(apples pears)`<br>`shift fruit` | `shift` 内建命令不能移动数组；它仅用于移动位置参数。 | 使用 `shift 2` 或其他数值。 |
| `./file: too many arguments`<br>`./file: line 10: syntax error near unexpected token \`[\`'` | `if [ "$name" = Joe ]`<br>`if [ "$name" == Joe ]` | `[` 命令要求其参数之间有空格。 `==` 操作符是 Bash 扩展；为保证可移植性请使用 `=`。 | `if [ "$name" = Joe ]` |
| `bash: syntax error near unexpected token \`echo\''` | `function fun (echo hi)` | 函数定义中花括号周围应有空格，并且用分号终止函数语句。 | `function fun { echo hi; }` |
| `bash: if: cannot overwrite temp`<br>`existing file` | `sort file > temp`<br>`sort file` | `root` 变量已设置且 `temp` 文件存在； `sort` 不允许覆盖现有文件。 | `sort file > temp`<br>`sort file >| temp`<br>`set +o noclobber` or `set -o noclobber`<br>`(override noclobber)` |
| `bash: trap: 500: not a signal specification` | `trap "500" SIGALRM`<br>`for c in $@; do`<br>`...` | 数字 500 是非法的信号。通常使用信号 2 或 15 表示 Ctrl-C 和 Ctrl-D。 Bash 也可接受以 `SIG` 开头的字符串； `trap` 命令应被终止。 | `trap "" 2` or `trap 2` |

## 15.4.4 逻辑错误与健壮性

逻辑错误很难发现，因为它们不一定会显示错误消息，但会导致程序以意外方式运行。这类错误可能是误用关系运算符、相等运算符或逻辑运算符，在一组嵌套条件语句中错误分支，或陷入无限循环。健壮性指的是，如果执行了充分的错误检查（例如检查错误的用户输入、参数不足或变量中的空值）本应被发现的错误。

逻辑运算符错误。示例15.13展示了逻辑运算符错误及可能的修复方法。

### 示例15.13

```
