

# 高级 Bash 脚本指南

```
# 当“限制字符串”被引用或转义时，不会进行参数替换。
# 在在此文档（here document）头部使用以下任意一种方式
# 效果相同。
# cat <<"Endofmessage"
# cat <<\Endofmessage
```

```bash
# 同样地：
cat <<"SpecialChartTest"
如果限制字符串没有加引号，
将输出目录列表。
ls -1
如果限制字符串没有加引号，
将进行算术扩展。
如果限制字符串没有加引号，
将回显单个反斜杠。
\\\
SpecialChartTest
exit
```

禁用参数替换允许输出字面量文本。生成脚本甚至程序代码是其用途之一。

# 示例 19-8. 一个生成另一个脚本的脚本

```bash
#!/bin/bash
# generate-script.sh
# 基于 Albert Reiner 的想法

OUTFILE=generated.sh      # 要生成的文件名。

----------------------------------------------------------------------
# 包含生成脚本体的在此文档。
cat <<'EOF'
#/bin/bash
```

```bash
echo "这是一个生成的脚本。"
# 注意我们正处于一个子 shell 中，
# 我们无法访问“外部”脚本中的变量。

echo "生成的文件将命名为: $OUTFILE"
# 上述行不会按预期工作
# 因为参数扩展已被禁用。
# 相地，结果是字面量输出。
```

# 第 19 章 在此文档 (Here Documents)

# 高级 Bash 脚本指南

```bash
a=7
b=3

let "c = $a * $b"
echo "c = $c"

exit 0
EOF
) > $OUTFILE
# ---
```

# 引用“限制字符串”可以防止在上述“在此文档”体内部进行变量扩展。
# 这允许在输出文件中输出字面量字符串。

```bash
if [ -f "OUTFILE" ]
then
  chmod 755 $OUTFILE
  # 使生成的文件具有执行权限。
else
  echo "创建文件错误: $OUTFILE"
fi
```

# 此方法也适用于生成
## C 程序、Perl 程序、Python 程序、Makefiles
## 以及等。

```bash
exit 0
```

可以从在此文档的输出设置变量。这实际上是一种狡猾的命令替换形式。

```bash
variable=$$(cat <<SETVAR
此变量
跨越多行。
SETVAR
)
```

```bash
echo "$variable"
```

在此文档可以为同一脚本中的函数提供输入。

示例 19-9. 在此文档与函数

```bash
#!/bin/bash
# here-function.sh

GetPersonalData ()
{
  read firstname
  read lastname
  read address
  read city
  read state
  read zipcode
)# 这看起来显然是一个交互式函数，但 . . .
```

第 19 章 在此文档

# 高级 Bash 脚本指南

```bash
# 为上述函数提供输入。
GetPersonalData <<RECORD001
Bozo
Bozeman
2726 Nondescript Dr.
Bozeman
MT
21226
RECORD001

echo "$firstname $lastname"
echo "$address"
echo "$city, $state $zipcode"
echo

exit 0
```

可以使用冒号 `:` 作为占位符注释来接受在此文档的输出。这实际上创建了“匿名”的在此文档。

# 示例 19-10. “匿名”在此文档

```bash
#!/bin/bash
: <<TESTVARIABLES
${HOSTNAME}?${USER}?${MAIL?}\  # 如果其中一个变量未设置，则打印错误消息。
TESTVARIABLES

exit $?
```

> 上述技术的变体，“注释掉”代码块。

# 示例 19-11. 注释代码块

```bash
#!/bin/bash
# 注释
: <<COMMENTBLOCK
echo "这一行不会回显。"
这是一个缺少 "#" 前缀的注释行。
这是另一个缺少 "#" 前缀的注释行。

上述行行不会导致错误消息，
因为 Bash 解释器将忽略它。
COMMENTBLOCK

echo "COMMENTBLOCK 的值为 $?.  # 没有显示错误。
echo
```

# 上述技术也用于调试注释掉
# 代码块。它避免了在每行开头添加 "#"。

# 第 19 章 在此文档

```bash
# 然后稍后删除每行的 "#"。
# 注意上述冒号的使用是可选的。

echo "注释掉代码块之前。"
# 在注释掉的代码块之间的行不会执行。
######################################################
: <<DEBUGUGXX
for file in
do
cat "$file"
done
DEBUGUGXX
######################################################
echo "注释掉代码块之后。"

exit 0
```

```bash
# 注意，如果在注释掉的代码块内包含括号变量，
# 那么可能会导致问题。例如：

#!/bin/bash

# <<COMMENTBLOCK
echo "这一行不会回显。"
$!
foo_bar)
$(rm -rf /tmp/)
$(touch my_directory/cups/)
COMMENTBLOCK

$ sh commented-bad.sh
commented-bad.sh: 第 3 行 foo_bar: 参数为空或未设置

# 解决方法是引用第 49 行的 'COMMENTBLOCK'。
# <<'COMMENTBLOCK'

这种巧妙的转折让自文档脚本成为可能。

# 示例 19-12. 一个自文档脚本

```bash
#!/bin/bash
# self-documenting.sh: 自文档脚本
# 修改自 "colm.sh"

DOC_REQUEST=70

if [ "$1" = "-h" -o "$1" = "--help" ]; then 请求帮助。
then
echo " 用法: $0 [directory-name] "; echo
sed --silent -e '/DOCUMENTATION$$/,/DOCUMENTATION$$/p' "$0" |

# 第 19 章 在此文档

# 高级 Bash 脚本指南

```bash
sed -e '/DOCUMENTATION$/d'; exit $DOC_REQUEST; fi

: <<DOCUMENTATIONXX
以表格格式列出指定目录的统计信息。

命令行提供了要列出的目录。
如果没有指定目录或目录无法读取，
则列出当前工作目录。

```bash
DOCUMENTATIONXX

if [ -z "$1" -o -r "$1" ]
then
directory=
else
directory="$1"
fi
```

```bash
echo "Listing of "$directory":"; echo
printf "PERMISSIONS OWNER GROUP SIZE DAY HH:MM PROG-NAME\n" \n; ls -l "$directory" | sed 1 | column -t
```

exit 0
使用 cat 脚本是实现此点的另一种方法。

```bash
DOC_REQUEST=70
if [ "$1" = "-h" -o "$1" = "--help" ] # 请求帮助。
使用 "cat 脚本"
then
cat <<DOCUMENTATIONXX
以表格格式列出指定目录的统计信息。

命令行提供了要列出的目录。
如果没有指定目录或目录无法读取，
则列出当前工作目录。

```bash
DOCUMENTATIONXX
exit $DOC_REQUEST
fi
```

更多自文档脚本的示例请参见 A-28, A-40, A-41, A-42。

> 创建临时文件，但这些文件在打开后会被删除，且其他进程无法访问。

```
bash -c 'lsof -a p -sd0' EOF
> EOF
lsof 1 REG 03386 /tmp/t1213 (deleted)
```

+ 某些工具在此文档内无法工作。

+ 在文档最后一行的结束限制字符串必须从第一个字符开始。可以有领先空格。限制字符串后的尾空格会导致意外行为。空格会导致限制字符串无法被识别。

# 高级 Bash 脚本指南

```bash
#!/bin/bash
echo "-LimitString
cat <<-echo "这是在此文档内的第 1 行消息。"
echo "这是在此文档内的第 2 行消息。"
echo "这是在此文档内的最后一行。"
LimitString
缩进的限制字符串。错误！此脚本的行为将不符合预期。"
echo "
```

# 这些注释在“在此文档”之外
## 并且应该回显。

echo "在此文档之外。"
exit 0
echo "这一行最好不要回显。" # 跟跟在 'exit' 命令之后。

有些人巧妙地使用单个 '!' 作为限制字符串。但这并不一定是个好主意。

```bash
# 这有效。
cat <<!
Hello!
! 三个感叹号 !!!
!
# 但 . . .
cat <<!
Hello!
后面跟着一个感叹号！
!
# 错误消息崩溃。

# 然而，以下将有效。
cat <<EOF
Hello!
后面跟着一个感叹号！
!
EOF
# 使用多字符限制字符串更安全。
```

对于那些在此文档无法处理的复杂任务，考虑使用 expect 脚本语言，它专门设计为交互式程序提供输入。

# 19.1. 在此字符串 (Here Strings)

在此字符串可以被视为在此文档的精简形式。

