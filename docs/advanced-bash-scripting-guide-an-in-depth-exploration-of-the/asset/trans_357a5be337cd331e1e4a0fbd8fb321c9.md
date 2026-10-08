

# 高级 Bash 脚本指南

```
######################################################################
mplayer "$1" -ao pcm:file=$OUTFILE
oggenc "$OUTFILE" # oggenc 自动添加了正确的文件扩展名
######################################################################

rm "$OUTFILE"      # 删除中间 *.wav 文件。
# 如果你想保留它，请注释掉上面那行。

exit $?

# 注意：
#-
# 在网页上，只需点击 *.ram 流媒体音频文件
## 通常只会下载实际 *.ra 音频文件的 URL。
# 随后你可以使用 "wget" 或类似的工具
## 下载 *.ra 文件本身。

#-
# 练习题：
# 目前，此脚本转换 *.ra 文件名。
## 通过允许使用 *.ram 和其他文件名来增加灵活性。
#
# 如果你真的野心勃勃，可以扩展脚本
## 实现对流媒体音频文件的自动下载和转换。
# 给定一个 URL，批量下载流媒体音频文件（使用 "wget"）
## 并即时转换它们。
```

一个使用子串提取结构的 `getopt` 简单示例。

# 示例 10-5. 模拟 getopt

```bash
#!/bin/bash
# getopt-simple.sh
# 作者：Chris Morgan
# 经许可用于 ABS Guide。

getopt_simple() {
	echo "getopt_simple()"
	echo "Parameters are '$*'"
	while [ -n "$1" ]
	do
		echo "Processing parameter of: '$1"
		if [ "${1:0:1}" = "-" ]; then
			tmp=${1#*/}      # 去除开头的 '/' 和 .
			parameter=${tmp#*=}      # 提取名称。
			value=${tmp#*=}          # 提取值。
			echo "Parameter: '$parameter', value: '$value'"
			eval parameter=$value
		fi
		shift
	done
}
```

第 10 章 变量操作

# 高级 Bash 脚本指南

```
# 将所有选项传递给 getopt_simple()。
getopt_simple "$@"
echo test is '$test'
echo test2 is '$test2'
exit 0 # 另参见 UseGetOpt.sh，该脚本的修改版本。
```
```

```
sh getopt_example.sh /test=value1 /test2=value2

Parameters are '/test=value1 /test2=value2'
Processing parameter of: '/test=value1'
Parameter: 'test', value: 'value1'
Processing parameter of: '/test2=value2'
Parameter: 'test2', value: 'value2'
test is 'value1'
test2 is 'value2'
```

# 子串替换

${string/substring/replacement}
将 $substring 的第一个匹配替换为 $replacement。

${string//substring/replacement}
将 $substring 的所有匹配替换为 $replacement。

```
stringZ=abc123ABCabc      # xyz123ABCabc
echo ${stringZ/abc}       # 将第一个匹配的'abc'替换为 'xyz'。

echo ${stringZ//abc}       # xyz123ABCxyz
# 将所有匹配的 'abc'替换为 'xyz'。

echo
echo "$stringZ"         # abc123ABCabc
echo                      # 字符串本身没有被修改！

# 匹配和替换字符串可以参数化吗？
match=abc
repl=000
echo ${string}/$match/${repl} # 000ABC123ABCabc
echo ${string//$match/${repl} # 000ABC123ABC000
# 可以！
echo
# 如果不提供替换字符串会怎样？
echo ${string/abc}         # 123ABC
echo ${string//abc}        # 123ABC
```

${string/substring/replacement}
如果 $substring 匹配 $string 的开头，则用 $replacement 替换 $substring。
${string%substring/replacement}
如果 $substring 匹配 $string 的结尾，则用 $replacement 替换 $substring。

# 第 10 章 变量操作

# 高级 Bash 脚本指南

| stringZ=abcABC23abc | |
|---|---|
| echo ${stringZ#*abc} | # ABC23abc 替换 'abc' 的开头匹配。 |
| echo ${stringZ%*abc} | # abcABC23 替换 'abc' 的结尾匹配。 | |

# 10.1.1. 使用 awk 处理字符串

Bash 脚本可以使用 awk 的字符串处理功能作为替代。

# 10-6. 提取子串的替代方法

```bash
#!/bin/bash
# substring-extraction.sh

String=23skid
# 0123456789
# 注意不同的索引：
# Bash 中字符串的第一个字符为 0。
# awk 中字符串的第一个字符为 1。
echo ${String:2:4} # skid
# 从位置 2 开始，长度为 4。 (1-2)

# ${string:pos:length} 等同于 awk substr(pos,length)
echo | awk {
  print substr("${String}",3,4) # skid
}

# 向 awk 传递空字符串 "echo"
# 这使得不需要提供文件名。
echo ""

# 像这样：
echo | awk {
  print substr("${String}",3,"4") # 3
  # (从位置 3 开始)
}

exit 0

# 10.1.2. 引用

关于脚本中字符串处理的更多信息，请参考第 10.2 节。

脚本示例：

- 1. Example-6
- 2. Example-9
- 3. Example-10
- 4. Example-11
- 5. Example-13
- 6. Example A-36
- 7. Example A-41

# 10.2. 参数替换

操作和扩展变量

${parameter}
同于 $parameter，即变量的值。在某些上下文中，这种无歧义的形式有效。可用于与字符串拼接。

```bash
your_id=${parameter:-opt/bin}
echo "Old PATH = $PATH"
# 为脚本期间 PATH 添加 /opt/bin。
echo "New PATH = $PATH"
```

${parameter:-default}
如果没有设置，使用默认值。

```bash
var=1
var=2
# var3 未设置。
echo ${var1:-var}    # 1
echo ${var3:-2}      # 2
# 注意前缀。
echo ${parameter='whoami'}
# 如果变量未设置，则输出结果。
# 因为使用了 :- 而仅仅在条件中。
# 与上面的实例比较。

# 再次：
variable=
# variable 已经声明，但设置为空。
echo "${variable:-0}" # (无输出)
echo "${variable:-1}" # 1
unset variable
echo "${variable:-2}" # 2
echo "${variable:-3}" # 3

exit
```

默认参数构造用于脚本中提供“缺失”的命令行参数。

```bash
DEFAULT_FILENAME=generic,data
filename=${1:-DEFAULT_FILENAME}
# 如果没有指定，命令块作用于文件 "generic.data"。
# 开始命令块
# #
# 结束命令块
```

```bash
# 来自 hanoi2.bash 示例：
DISKS=${1:-E_NOPARAJ} # 指定数量。
# 将 DISKS 设置为 $1，
# 如果未设置则设置为 $E_NOPARAJ。
# 另参见示例 3-4 和示例 A-6。
```

比较这种方法和使用列表提供默认命令行参数。
${parameter=default}. ${parameter:=default}

如果参数未设置，将其设置为默认值。

# 高级 Bash 脚本指南

两种形式几乎等价。当 $parameter 已声明且为空时，: 会产生区别，如上。

```bash
echo $(var=abc)      # abc
echo $(var=xyz)      # abc
# $var 已设置为 abc，所以没有变化。
```

# ${parameter+alt_value}, ${parameter:+alt_value}

如果设置，使用 **alt_value**，否则使用空字符串。

两种形式几乎等价。当参数已声明且为空时，: 会产生区别，见下文。

```bash
# $(parameter+alt_value)
a=${param1+xyz}
echo "a = $a"

param2=
a=${param2+xyz}
echo "a = $a"

param3=123
a=${param3+xyz}
echo "a = $a"

# $(parameter:+alt_value)
a=${param4+xyz}
echo "a = $a"

param5=
a=${param5+xyz}
echo "a = $a"
# 与 a=${param5+xyz} 结果不同。

param6=123
a=${param6+xyz}
echo "a = $a"
```

# ${parameter?err_msg}, ${parameter:+err_msg}

如果参数设置，使用它，否则打印 err_msg 并以退出状态 1 退出脚本。

两种形式几乎等价。当参数已声明且为空时，如上。

示例 10-7. 使用参数替换和错误消息

```bash
#!/bin/bash

# 检查系统的一些环境变量。
# 这是良好的预防性维护。
# 如果例如 USER（控制台用户名称）未设置，
# 机器将无法识别你。
```

