

# 高级 Bash 脚本指南

```bash
# 目标文件的前缀。修复此处。
# 2) 第 17 行仅将点视为句子结束符。
# 修改此内容以包含其他句尾字符，
# 例如 ?, !, 和 "。
```

# 字符串开头匹配子字符串长度

expr match "String" "$substring"
  $substring 是一个正则表达式。
expr "String" : "$substring"
  $substring 是一个正则表达式。

```bash
stringZ=ABC123ABCabc
#-------
# 12345678

echo expr match "$stringZ" 'abc[A-Z].*2' # 8
echo expr "$stringZ" : 'abc[A-Z].*2' # 8
```

# 索引

expr index $string $substring
$string 中与 $substring 中第一个字符匹配的的数字位置。

```bash
stringZ=ABC123ABCabc
# 123456...
echo expr index "$stringZ" C12 # 6
  # C 的位置。
```

```bash
echo expr index "$stringZ" 1c # 3
  # 'c'（在第 3 位置）在 '1' 之前匹配。
这等同于 C 语言中的 strchr。
```

# 子字符串提取

$string:position]
从 $string 的 $position 处提取子字符串。

如果参数 $string 为 "*" 或 "@"，则从从 $position 开始提取这些位置参数。
$string:length]
从 $string 的 $position 处提取 $length 个字符的子字符串。

```bash
stringZ=ABC123ABCabc
# 0123456789...
# 从 0 开始索引。

echo ${stringZ:0} # ABC123ABCabc
echo ${stringZ:1} # BCABC123ABCabc
echo ${stringZ:7} # 23ABCabc

echo ${stringZ:7:3} # 23A
  # 子字符串的三个字符。
```

第 10 章 变量操作

# 高级 Bash 脚本指南

```bash
# 是否可以从字符串的右端进行索引？
echo $(stringZ:-4)                                # abcABC123ABCabc
# 默认为整个字符串，类似于 $(parameter:-default)。
# 但是 . . . 

echo ${stringZ:(-4)}                                # Cabc
echo $(stringZ:-4)                                # Cabc
# 现在可以了。
# 括号或添加空格可以“转义”位置参数。
```



感谢 Dan Jacobson 指出这一点。
位置和长度参数可以是“参数化”的，即表示为变量而不是数值常量。

# 示例 10-2. 生成一个 8 位的“随机”字符串

```bash
#!/bin/bash
# rand-string.sh
# 生成一个 8 位的“随机”字符串。

if [ -n "$1" ]                                # 如果存在命令行参数
then
    # 将 start-string 设置为它。
    str0="$1"
else                                         # 使用脚本的 PID 作为 start-string。
    str0=$$
fi

POS=2 # 从字符串的位置 2 开始。
LEN=8 # 提取八个字符。

str1=$(echo "$str0" | md5sum)
# 双重混乱
# 通过管道传输并再次传输到 md5sum 实现。

randstring="${str1:$POS:$LEN}"
# 可以参数化

echo "$randstring"
```

```bash
exit $?

bozo ./rand-string.sh my-password
ldbb88c4

# 不，这并不推荐
# 这种方法作为生成防破解密码的方法。
```

如果参数 $string 为 "" 或 "@"，则从 $position 开始提取最多 $length 个位置参数。

```bash
echo ${*:2}                                     # 回显第二个及随后的位置参数。
echo ${@}                                          # 与上述相同。

echo ${*:2:3}                                     # 回显从第二个开始的三个位置参数。
```

expr substr String Position Length

# 第 10 章 变量操作

# 高级 Bash 脚本指南

从 $string 的 $position 开始从 $string 中提取 $length 个字符字符。

```bash
stringZ=ABC123ABCabc
# 123456789......
# 从 1 开始索引。
echo ' expr substr $stringZ 1 2 '
# ABC
echo ' expr substr $stringZ 4 3 '
```

expr match "$string" "\(substring)"
在 $string 的开头提取 $substring，其中 $substring 是一个正则表达式。
expr "$string": "\(substring)"
在 $string 的末尾提取 $substring，其中 $substring 是一个正则表达式。

```bash
stringZ=ABC123ABCabc
=====
echo ' expr match "$stringZ" "\.([b-c][A-Z].[0-9])\'' ' #ABC1
echo ' expr match "$stringZ": "\.(b-c)[A-Z].[0-9])\'' ' #ABC1
echo ' expr match "$stringZ": "\.(......)\'' ' #ABC1
# 以上所有形式给出相同的结果。
```

expr match "$string" "\(substring)"
在 $string 的末尾提取 $substring，其中 $substring 是一个正则表达式。
expr "$string": "\(substring)"
在 $string 的末尾提取 $substring，其中 $substring 是一个正则表达式。

```bash
string2=ABC123ABCabc
=====
echo ' expr match "$stringZ" "\*([A-C][A-C][a-c])*\'' ' #ABCabc
echo ' expr match "$stringZ": "\.(......)\'' ' #ABCabc
```

# 删除子字符串

$[$substring]
从 $string 开头删除 $substring 的匹配项。
${string##substring}
从 $string 开头删除 $substring 的最长匹配项。

```bash
stringZ=ABC123ABCabc
# 最短
# ----|
# 最长
echo ${stringZ#*C} # 123ABCabc
# 删除 'a' 和 'C' 之间最短的匹配项。
echo ${stringZ##*a} # abc
# 删除 'a' 和 'C' 之间最长的项。

# 你可以对子字符串进行参数化。
X='a*C'
echo ${stringZ#$X} # 123ABCabc
echo ${stringZ##$X} # abc
# 同上。
```

# 第 10 章 变量操作

#

# 高级 Bash 脚本指南

${string%substring}
从 $string 末尾删除 $substring 的最短匹配项。

# 例如：

```bash
stringZ=ABC123ABCabc
# 最短
# ----|
# 最长
echo ${stringZ#*C} # 123ABCabc
# 删除 'a' 和 'C' 之间最短的匹配项。
```

