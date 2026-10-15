

# 表 15.5 常见的 Korn Shell 错误信息（续）

## 15.4 语法错误的可能原因

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| [空白行] | echo $name 或 echo ${fruit[5]} | 变量不存在或为空。 | name="Some value" |
| file2: line2: syntax error at line 6: `done' unexpected | while (( $n < 5 )) do statements done | while 缺少 do 关键字 | while (( $n < 5 )) do statements done |
| file: syntax error at line 3: unmatched | print I don't care | 脚本中单引号未匹配。应使用双引号括起来。 | echo "I don't care" 或 echo 'I don't care' |
| file: syntax error at line 3: unmatched | print She said Hello | 脚本中双引号未匹配。 | print She said "Hello" |
| ksh: [: Doe: unknown operator | name="John Doe"; then if [ $name = Joe ]; then 或 if [[ $name == Joe ]]; then | 变量 `name' 应在测试表达式中用双引号括起来。= 测试运算符的左侧只能有一个字符串。使用此运算符时不会使用其他替代方案。使用 [ 或 [[ 时单词会被拆分。 | if [ "$name" = Joe ]; then 或 if [[ $name == Joe ]]; then |
| ksh: [ellie: not found | if [ $USER = "ellie" ]; then if [[ $USER = "ellie" ]]; then | [ 或 [[ 运算符后面必须有空格。 | if [ $USER = "ellie" ]; then if [[ $USER = "ellie" ]]; then |
| ksh: apples: bad number | set -a; apples pears peaches fruit | shift 内置命令 shift 只能移动仅在 shift 命令中使用的位置参数。 | set apples pears peaches fruit |
| -ksh: file.exe-foo: not found | file.exe-foo | 变量名中不能包含句点。 | file.exe-foo |
| ksh: file: file already exists. | sort file > temp | nodobber 变量已设置且 temp 文件存在。 | sort file > temp（使用不同的输出文件）或 sort file > temp（覆盖 nodobber）或 nodobber 不允许你覆盖现有文件。 |

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| ksh: fred: unknown test operator if [ grey fred /etc/passwd ] ; then | if [ grey fred /etc/passwd ] ; then | grep 命令不应被方括号或其他符号包围。方括号仅用于测试表达式。! 是一个测试运算符。 | if grep fred /etc/passwd ; then |
| ksh: name: not found name = "Tom" | name = "Tom" | 没有空格可用于内置命令或用于移动位置参数。内置命令要么是等号。 | set name "Tom" |
| ksh: shift: bad number shift 2 | shift 2 | shift 命令将移动 apples 和 pears 将从列表中移出。至少应有两个位置参数。如果不会则会失败。 | apples 2 |
| ksh: syntax error: "echo hi" not expected | function fun { echo "hi"; } | 函数定义中大括号周围应有空格（fun）。分号将终止函数语句。 | function fun { echo "hi"; } |
| ksh: syntax error: "Doe" unexpected if [[ $name = "John Doe" ]] | if [[ $name = John Doe ]] | = 左侧不会执行单词拆分，但右侧的字符串必须加引号。 | if [[ $name = "John Doe" ]] |
| ksh: syntax error: "fi" unexpected if [ USER = "ellie" ] then or | if [ USER = "ellie" ] then or | then 应在下一行或前面加上分号。 | if [ USER = "ellie" ] then |
| ksh: syntax error: "then" unexpected if (( $a == $b )) | if (( $a == $b )) | 括住第二个表达式的括号不匹配。 | if (( $a == $b )) |
| ksh: trap: 500: bad trap trap 'm trap' 500 | trap 'm trap' 500 | 数字 500 是非法的信号。通常在 shell 脚本中会捕获信号 2 或 3。2 用于 Ctrl-C，3 用于 Ctrl-Y。两者都会导致以 trap 命令命名的程序被终止。 | trap 'm trap' 2 |

# 表 15.5 常见的 Korn Shell 错误信息（续）

a. 此错误在使用公共领域的 Korn shell 时出现，但 Korn shell 88（Solaris）不产生任何输出。

