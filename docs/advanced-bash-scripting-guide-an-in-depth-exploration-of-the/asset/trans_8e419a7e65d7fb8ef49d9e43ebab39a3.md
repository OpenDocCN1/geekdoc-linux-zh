

# 高级 Bash 脚本指南

它仅包含 `COMMAND <<< $WORD`，
其中 `$WORD` 被展开并输入到 `COMMAND` 的标准输入（stdin）。

作为一个简单的示例，考虑这种 `echo-grep` 结构的替代方案。

```bash
# 替换使用：
if echo "$VAR" | grep -q txt
# if [[ $VAR = *txt* ]]
# 等。
```

```bash
# 尝试：
if grep -q "txt" <<< "$VAR"
then
  echo "$VAR contains the substring sequence $txt"
fi
# 感谢 Sebastian Kaminski 的建议。
```

或者，与 `read` 结合使用：

```bash
String="This is a string of words."
read -r -a Words <<< "$String"
# 将读取到数组连续成员的选项
# 将结果值赋值给数组。
```

```bash
echo "First word in String: ${Words[0]}" # 这
echo "Second word in String: ${Words[1]}" # 是
echo "Third word in String: ${Words[2]}" # 一个
echo "Fourth word in String: ${Words[3]}" # 字符串
echo "Fifth word in String: ${Words[4]}" # 字符串
echo "Sixth word in String: ${Words[5]}" # 单词
echo "Seventh word in String: ${Words[6]}" # (空)
# 越过了 $String 的末尾。
```

感谢 Francisco Lobo 的建议。
当然，可以将 here string（在此字符串）的输出馈送给循环的标准输入。

```bash
# 如 Seamus 指出的 =
ArrayVar=$(element0 element1 element2 {A..D})

while read element; do
  echo "$element" 1>&2
done <<< $(echo ${ArrayVar[*]})

# element0 element1 A B C D
```

# 示例 19-13. 在文件开头添加一行

```bash
#!/bin/bash
# prepend. 在文件开头添加文本。
# 示例由 Kenny Stauffer 提供，
# + 由文档作者略微修改。
```

```bash
E_NOSUCHFILE=85
```

第 19 章 Here Documents（在此文档）

# 高级 Bash 脚本指南

```bash
read -p "File: " file # -p 参数给 'read' 显示提示符。
if [ -e "$file" ]
then # 如果没有此类文件，则退出。
echo "File $file not found."
exit $E_NOSUCHFILE
fi
```

```bash
read -p "Title: " title
cat $file <<<$title > $file.new
```

```bash
echo "Modified file is $file.new"
```

```bash
exit # 结束脚本执行。
```

来自 'man bash'：
Here Strings（在此字符串）
文档的一种变体，格式为：

<<Word

单词被展开并提供给命令的标准输入。

当然，以下方法也有效：
sed -e '!!i'
Title: '$file'

# 示例 19-14. 解析邮箱箱文件

```bash
#!/bin/bash
# 脚本由 Francisco Lobo 编写，
#+ 由 ABS Guide 作者略微修改和注释。
# 经许可在 ABS Guide 中使用。（感谢！）
```

```bash
# 此脚本不会在 Bash 版本低于 3.0 时运行。
```

```bash
E_MISSING_ARG=87
if [ -z "$1" ]
then
echo "Usage: $0 mailbox-file"
exit $E_MISSING_ARG
fi
```

```bash
mbox_grep() # 解析邮箱箱文件。
{
  declare -i body=0 match=0
  declare -a date sender
  declare mail header value
```

```bash
while IFS= read -r mail
# 重置 IFS。
# 否则 "read" 将去除其输入前后的空格。

  if [[ $mail =~ ^From ]]; # 匹配消息中的 "From" 字段。
then
    (( body = 0 )) # 清空变量。
    (( match = 0 ))
```

第 19 章 Here Documents

# 高级 Bash 脚本指南

```bash
elif (( body ))
then
    (( match ))
    # echo "mail"
    # 如果你想显示整个
+# 消息正文。
```

```bash
elif [[ $mail ]]; then
IFS=- read -r header value <<< "$mail"
#                               在此字符串"

case "$header" in
    [F][Rr][Oo] [Mm]) [[ $value = "$2" ]] && (( match++));
    # 匹配 "From"
    [Dd][Aa][Tt] [Ee]) read -r -a date <<< "$value";
    # 匹配 "Date" 行。
    [Rr][Ee][Cc] [Ei][Ii] [Vv][Ee] [Dd]) read -r -a sender <<< "$value"; # 匹配 IP 地址（可能是伪造的）。
```

```bash
else
    (( body ))
    (( match )) &&
    echo "MESSAGE ${date+of: ${date[*]}}"
    # 整个 $date 数组
    echo "IP address of sender: ${sender[1]}"
    fi
fi # 将文件的标准输出重定向到循环。
```

```bash
mbox_grep "$1" # 将邮箱文件发送给函数。
```

```bash
exit $?
```

+   # 练习：
#-
# 1) 拆分函数，
#-
# 2) 使用邮箱解析器按发送者计数消息。
# 3) 使用在此字符串向函数传递变量。

# 1) 拆分函数，
#-
# 2) 使用邮箱解析器按发送者计数消息。
# 3) 使用在此字符串向函数传递变量。

# 1) 拆分函数，
#-
# 2) 使用邮箱解析器按发送者计数消息。
# 3) 使用在此字符串向函数传递变量。

# 1) 拆分函数，
#-
# 2) 使用邮箱解析器按发送者计数消息。
# 3) 使用在此字符串向函数传递变量。

# 1) 拆分函数，
#-
# 2) 使用邮箱解析器按发送者计数消息。
# 3) 使用在此字符串向函数传递变量。

