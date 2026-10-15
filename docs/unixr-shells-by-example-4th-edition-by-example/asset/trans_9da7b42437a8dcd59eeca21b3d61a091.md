

## 15.4 语法错误的可能原因

### 表 15.6 常见的 Bash Shell 错误信息。

表 15.6 列出了常见的 Bash shell 错误信息。

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| bash: syntax error: unexpected EOF while looking for matching `"` | echo I don't care | 脚本中单引号未匹配。 | echo "I don't care" |
| bash: syntax error: unexpected EOF while looking for matching `'` | print She said "Hello" | 脚本中双引号未匹配。 | print She said 'Hello' |
| [空白行] 无错误信息，无输出 | echo $name or echo ${Fruit[5]} | 变量不存在或为空。 | name="some value" or use -d to catch any variables that have not been set. The message will be printed later if the SET is sent to stderr. |
| bash: name: command not found | name="Tom" | 等号两侧不能有空格 | name=Tom |
| bash: 8.5: syntax error in expression (error token is ".5") | declare -i num=8.5 | 只能为变量 num 分配整数值 | num=6 |
| bash: [Ellie]: command not found | if [[ $USER = "Ellie" ]]; then or if [[ $USER = "Ellie" ]]; then | [[ 后面必须有一个空格或 [[ | if [[ $USER = "Ellie" ]]; then |
| bash: syntax error near unexpected token `fi' | if [[ $USER = "Ellie" ]]; then if [[ $USER = "Ellie" ]]; then if [[ $USER = "Ellie" ]]; then if [[ $USER = "Ellie" ]] | then 应该在下一行或前面加上分号 | if [[ $USER = "Ellie" ]]; then |
| bash: syntax error in conditional expression | if [[ $name = "John Doe" ]]; then | = 右侧不会进行单词拆分，但左侧的字符串必须加引号。 | if [[ "$name" = "John Doe" ]]; then |
| [: fret: binary operator expected | if [ grep Fred /etc/passwd ]; then | grep 命令不应被方括号或其他符号包围。方括号仅用于测试表达式。 [ 是一个测试操作符。 | if grep Fred /etc/passwd; then |

| 错误信息 | 导致原因 | 其含义 | 如何修复 |
|---|---|---|---|
| `./file: line 5: syntax error near unexpected token \`blue\''`<br>`./file: line 5: \`blue\': unexpected` | `color="blue"`<br>`case $color in`<br>`blue)`<br>`echo "red"`<br>`;;`<br>`esac` | case 命令缺少 `in` 关键字。 | `case $color in` |
| `./file: line 12: syntax error at unexpected \\`\\`'` | `color="blue"`<br>`case $color in`<br>`blue)`<br>`echo "red"`<br>`;;`<br>`esac` | case 语句在 `blue` 后未以 `;;` 终止。 | 在每个 case 模式后添加 `;;`。 |
| `bash: shift: bad non-numeric arg \`fruit\''` | `declare -a fruit=(apples pears)`<br>`shift fruit` | `shift` 内建命令不能移动数组；它仅用于移动位置参数。 | 使用 `shift 2` 或其他数值。 |
| `./file: too many arguments`<br>`./file: line 10: syntax error near unexpected token \`[\`'` | `if [ "$name" = Joe ]`<br>`if [ "$name" == Joe ]` | `[` 命令要求其参数之间有空格。 `==` 操作符是 Bash 扩展；为保证可移植性请使用 `=`。 | `if [ "$name" = Joe ]` |
| `bash: syntax error near unexpected token \`echo\''` | `function fun (echo hi)` | 函数定义中花括号周围应有空格，并且用分号终止函数语句。 | `function fun { echo hi; }` |
| `bash: if: cannot overwrite temp`<br>`existing file` | `sort file > temp`<br>`sort file` | root 变量已设置且 temp 文件存在； `sort` 不允许覆盖现有文件。 | `sort file > temp`<br>`sort file >| temp`<br>`set +o noclobber` or `set -o noclobber`<br>`(override noclobber)` |
| `bash: trap: 500: not a signal specification` | `trap "500" SIGALRM`<br>`for c in $@; do`<br>`...` | 数字 500 是非法的信号。通常使用信号 2 或 15 表示 Ctrl-C 和 Ctrl-D。 Bash 也可接受以 `SIG` 开头的字符串； trap 命令应被终止。 | `trap "" 2` or `trap 2` |

