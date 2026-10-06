

# 高级 Bash 脚本指南

```
# 将所有匹配 'abc' 的部分替换为 'wyz'
${string//substring/replacement}
```

如果 $substring 匹配 $string 的开头，则将 $substring 替换为 $replacement。
${string%substring/replacement}

如果 $substring 匹配 $string 的结尾，则将 $substring 替换为 $replacement。

```
stringZ=abc123ABCabc
echo ${stringZ/#abc/XYZ}
# XYZABC123ABCabc
# 将开头匹配的 'abc' 替换为 'xyz'
echo ${stringZ/%abc/XYZ}
# abc123ACXYZ
# 将结尾匹配的 'abc' 替换为 'xyz'
```

# 9.2.1 使用 awk 处理字符串

Bash 脚本可以调用 awk 的字符串处理功能作为内置操作的替代。

示例 9–11. 提取子字符串的替代方法

```bash
#!/bin/bash
# substring-extraction.sh

String=23skidoodle
# 0123456789  Bash
# 123456789 awk
# 索引系统：
# 注意 awk 将字符串的第一个字符标记为 '0'
# Bash 将字符串的第一个字符标记为 '1'
echo ${String:2:4} # 位置 3 (0-1)，长度 4 个字符
# skid

${string:pos:length} 的 awk 等效等式是 substr(string,pos,len)。
echo '' | awk '
{ print substr("""\$String""",3,4) }
# skid

# 向 awk 管道传递一个空的 "echo" 可以提供伪输入，
# 并使得无需提供文件名。

exit 0
```

# 9.2.2. 进一步讨论

有关脚本中更多字符串处理操作，请参考第 9.3 节和 `expr` 命令列表的相关部分。脚本示例请参阅：

9.2.1. 使用 awk 处理字符串

- 1. 示例 12–6
- 2. 示例 9–13
- 3. 示例 9–14
- 4. 示例 9–15
- 5. 示例 9–17

# 9.3. 参数替换

变量的处理和/或扩展

$$(parameter)

相当于 $parameter，即变量参数的值。在某些上下文中，只有这种无歧义的 $(parameter) 形式有效。

可用于将变量与字符串拼接。

```bash
your_id=$(USER)-on-$(HOSTNAME)
echo "$your_id"
echo "Old $PATH = $PATH"
PATH=$(PATH):/opt/bin # 在脚本运行期间向 $PATH 添加 /opt/bin。
echo "New $PATH = $PATH"
```

$(parameter-default)

如果参数未设置，则使用默认值。

```bash
echo ${username-`whoami`}
# 如果变量 $username 仍未设置，则输出 `whoami` 的结果。
```

这与 $(parameter:-default) 几乎等效。额外的 `:-` 仅在参数已声明但为空时才会产生区别。

```bash
#!/bin/bash
username0=
# username0 已声明，但被设置为空值。
echo "username0=${username0-`whoami`}"
# 不输出。
echo username1=${username1-`whoami`}
# username1 未声明。
# 将输出。
username2=
# username2 已声明，但被设置为空值。
echo "username2=${username2:-`whoami`}"
# 将输出，因为使用了 :- 而不仅仅是在条件测试中。
```

exit 0
${parameter=default} , ${parameter:=default}

如果参数未设置，则将其设置为默认值。

两种形式几乎等效。仅当 $parameter 已声明且为空时（如上文 [21]），才会产生区别。

```bash
echo ${username=whoami}
# 变量 `username` 现在设置为 `whoami`
${parameter+alt_value}, ${parameter:+alt_value}

如果参数设置，则使用 alt_value，否则使用空字符串。

两种形式几乎等效。仅在参数已声明且为空时才会产生区别，见下文。

```bash
######## $(parameter+alt_value) #######
echo
a=$(param1+xyz)
echo "a = $a"  # a =
param2=
a=$(param2+xyz)
echo "a = $a"  # a =
param3=123
a=$(param3+xyz)
echo "a = $a"  # a =
######## $(parameter+alt_value) #######
echo
a=$(param4+xyz)
echo "a = $a"  # a =
param5=
a=$(param5+xyz)
echo "a = $a"  # a =
# 结果与 a=${param5+xyz} 不同
param6=123
a=$(param6+xyz)
echo "a = $a"  # a =
```

${parameter?err_msg}

如果参数设置，则使用它，否则打印 err_msg。两种形式几乎等效。仅在参数已声明且为空时（如上文所示）才会产生区别。

9.3. 参数替换

字符串长度（$var 中的字符数）。

${var%pattern}, ${var##pattern} 从 $var 中删除匹配 $pattern 开头的最短/最长部分。来自示例 A–7 的用法说明：

```bash
# 来自 "days-between.sh" 示例的函数。
# 从传递的参数中删除前导零。
strip_leading_zero () {
    # 最好删除日期或月份可能的前导零
    val=${1#0} # 否则 Bash 将其解释为八进制值 (POSIX.2, 9.2.1 节)。
    return $val
}
```

另一个用法说明：

```bash
echo "basename $PWD" # 当前工作目录。
echo "$PWD##*/" # 当前工作目录。
echo "basename $0" # 脚本名。
echo $0 # 脚本名。
echo "${0##*/}"      # 脚本名。
filename=test.data          # data
echo "${filename##*.}"    # 文件扩展名。
```

$varpattern 从 var 中删除匹配 $pattern 结尾的最短/最长部分。Bash 版本 2 增加了选项。

# 示例 9–14. 参数替换中的模式匹配

```bash
#!/bin/bash
# 使用 # 和 % 参数替换运算符进行模式匹配。
var1=abcd12345abc6789
pattern1=*c # (通配符) 匹配 a 到 c 之间的所有内容。

echo var="$var1" # abcd12345abc6789
echo "$var1" (另一种形式) abcd12345abc6789
echo "Number of characters in ${var1}" = ${#var1}
echo pattern1=$*c ('a' 和 'c' 之间的所有内容)
echo

echo "${var1$pattern1}" = '${var1$pattern1}' # dcd12345abc6789
# 短匹配，删除前 3 个字符 abcd12345abc6789
^^^^
echo '${var1#$pattern1}' = '${var1#$pattern1}' # 6789
# 最长匹配，删除前 12 个字符 abcd12345abc6789
^^^^^^^^^^^^
```

```bash
echo;
pattern2=b*9 # 'b' 和 '9' 之间的所有内容
echo var="$var1" # 仍为 abcd12345abc6789
echo pattern2=$pattern2
echo

echo "${var1%pattern2}" = '${var1%pattern2}' # abcd12345a
# 短匹配，删除 6 个字符 abcd12345abc6789
^^^^^^
echo '${var1%%pattern2}' = '${var1%%pattern2}' #
# 最长匹配，删除最后 12 个字符 abcd12345abc6789
^^^^^^^^^^^^
```

# 记住，# 和 ## 从字符串左端开始工作，
# % 和 %% 从右端开始工作。

# 示例 9–15. 重命名文件扩展名：

```bash
#!/bin/bash
```

