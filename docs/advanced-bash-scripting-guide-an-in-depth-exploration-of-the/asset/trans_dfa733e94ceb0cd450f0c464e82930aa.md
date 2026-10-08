

# 高级 Bash 脚本指南

功能：
作为赋值的右侧，保留硬引号，以在赋值期间保护字面量的内容。

说明：
使用奇特的名称 (*) 是为了避免在将其作为库加载（source）时，覆盖用户所定义的名称。

```
_Protect_Literal_String_Doc
# “仅用于演示”的函数形式
_protect_literal_str() {
# 选择一个未使用的非打印字符作为本地 IFS。
# 虽然不是必须，但显示了我们忽略了它。
  local IFS=$'x1B' # ESC 字符
# 在赋值期间将所有元素封装在硬引号中。
  local tmp=$'x27$\\\\'x27'
  local tmp=$'x27$\\\\''' # 更丑了。
  local len=$($tmp) # 仅供信息。
  echo $tmp is len. # 输出和信息。
}
```

```
# 这是短名称版本。
is() {
  local IFS=$'x1B' # ESC 字符（不是必须）
  echo=$'x27$\\\\'x27' # 硬引号参数通配符
}
```

```
# <<:'_Protect_Literal_String_Test'
# # 删除上方内容以禁用此功能。 # #
```

![](img/6708c6acfe5323a14123aff0b128abcb_633_0.png)

```
查看打印出来的效果如何。
echo " - Test One - "
_protect_literal_str 'Hello ${user}'
_protect_literal_str 'Hello ${username}'
echo
```

```
产生如下：
# - Test One
# 'Hello ${user}' is 13 long.
# 'Hello ${username}' is 21 long.
```

```
# 看起来符合预期，但为什么要费这么多劲？
# 区别隐藏在 Bash 内部的操作顺序中。
# 当你将在赋值的右侧使用它时就会显示。
```

```bash
# 为测试值声明数组。
declare -a array2
```

```bash
# 使用各种类型的引号和转义字符赋值元素。
array2=$(_pls ${Me})' 'Hello ${You}'\'Pass: ${pw}\' )
```

```bash
# 现在列出数组看看里面有什么。
echo " - Test Two - -
```

```bash
for (( i=0; i<${#array[@]}; i++ ))
do
    echo Element: ${array[$i]} is: ${array[$i]}
done
```

```bash
# 产生：
# Test Two # 我们的标记元素
# Element 0: zero is 4 long.
# Element 1: 'Hello($Me)' is: 13 long. # 我们的 "${pls '......'"
# Element 2: Hello $(You) is: 12 long. # 缺少了引号
# Element 3: '\\' is: 10 long. # $(pw) 展开为空
```

现在用该结果进行赋值。
declare - array2=(${array[@]})

```bash
# 并打印发生了什么。
echo "-- Test Three --"
for (( i=0; i<${#array[@]}; i++ ))
do
    echo Element: ${array[$i]} is: ${array[$i]}
done
```

```bash
# 产生：
# Test Three -- 我们的标记元素。
# Element 0: zero is 4 long. # 预期结果。
# Element 1: Hello $(Me) is: 11 long. # $(You) 展开为空。
# Element 2: Hello is: 5 long. # 在空格处拆分。
# Element 3: 'Pass' is: 6 long. # 结束在这里。
# Element 4: ' ' is: 1 long.
```

我们的 Element 1 删除了前后的引号。
虽然没有显示，但前后的空格也被删除了。
现在字符串已经设置好，Bash 在其操作期间也会
保留硬引号。

为什么呢？
考虑 `"${pls 'Hello($Me)}"` 结构：
"*" -> 展开结果，去除引号。
$(...) -> 替换为... 的结果。
_pls '...' -> 带参数的调用，去除引号。
结果包含硬引号；在上述处理完成后，它们变成了值的一部分。
同样，在操作字符串变量时，
(result) 生存了（直到显式评估字符串）。

提示：查看当硬引号 (''') 被替换为软引号时发生了什么。
有趣的是，移除任何引号。
```
_Protect_Literal_Test
# # 删除上方 " " 以禁用此代码。 # #
```

```
exit 0
```

但是，如果你想让 shell 展开字符串呢？

# 取消字符串
#! /bin/bash
# unprotect_literal.sh

# set -vx
:<<-'Protect_Literal_String'

Copyright (c) Michael S. Zick,2003; 版权所有
License: 任何形式、任何目的的无限制使用。
Warranty: 无
Revision:

文档到Bash 无操作。当脚本首次读取时，Bash 会清空此块。（这就是为什么最初要保护它的原因。）

Me="to the array guy."

用法：
`${_pls 'Literal String'` 函数。（见示例。）
StringVar=${ProtectedString}

功能：
在赋值的右侧使用时；会进行字符串嵌入的替换。

说明：
奇特的名称 (*) 是为了避免在将其作为库加载时，覆盖用户所定义的名称。

```
_Protect_Literal_String_Doc
_ups() {
    local IFS='$x1B' # ESC 字符（不是必须）
    eval $0          #  替换。
}
```

```bash
# <<-'Protect_String_Test'
# # 删除上方 " " 以禁用此代码。 # #
```

```bash
_pls() {
    local IFS='$x1B' # ESC 字符（不是必须）
    echo "\x27$@\x27" # 硬引号
}
```

```bash
# 为测试值声明数组。
declare -a array2
```

```bash
# 使用各种类型的引号和转义字符赋值。
array2=("_pls 'Hello ${Me}'" "Hello ${You}" "Pass: ${pw}")
```

```bash
# 现在用该结果进行赋值。
declare array2=("${array2[@]}")
```

```
# 产生了：
# Test Three
# Element 0: zero is 4 long.
# Element 1: Hello ${Me} is 11 long.
# Element 2: Hello is 5 long.
# Element 3: 'Pass: is: 6 long.
# Element 4: ' ' is 1 long

# 我们的标记元素。
# 预期结果。
# $(You) 展开为空。
# 在空格处拆分。
# 结束引号现在在这里。

set -vx
# 初始化 'Me' 为某个值用于嵌入的 ${Me} 替换。
# 这需要在评估受保护字符串之前完成。

# 将字符串变量目标设置为结果。
newVar=${_ups array[1]}

# 显示内容。
echo $newVar

# 我们真的需要一个函数来做这个吗？
newVar=$(echo "${array[1]}")
echo $newVar

# 我猜不需要，但工具为我们提供了一个挂载文档的地方。当我们忘记 $(eval echo ... ) 这种结构时很有帮助。

# 如果评估脚本时没有设置 Me 会怎样？
unset Me
newVar=${_ups array[2]}
echo $newVar

# 直接消失，没有提示，没有运行，没有错误。

# 为什么？
# 设置包含 Bash 含义的字符串变量内容是脚本编程中的通用问题。这个问题现在通过八行代码（以及四页描述）解决了。

# 这些内容都去向哪里？
# 动态内容网页作为 Bash 字符串数组。
# 内容通过对存储页面模板执行 Bash 'eval' 命令按请求设置。不是为了替换 PHP，只是一个很有趣的事。

###
# 没有服务器应用程序？
# 没问题，检查 Bash 的示例目录；那里也有对应的 Bash 脚本。

_Protect_Literal_String_Test
# # # 删除上方 " " 以禁用此代码。 # #

exit 0
这个有趣的脚本有助于打击垃圾邮件。

# 附录 A. 贡献脚本

# 示例 A-28. 垃圾邮件识别

```bash
#!/bin/bash

# SId: is_spammer.bash v1.12.2.11 2004/10/01 21:42:33 mszick
# 上行是 RCS 信息。

# 此脚本的最新版本可以在 http://www.morethan.org 获取。
# 垃圾邮件识别
# Michael S. Zick 编写
# 经许可在 ABS Guide 中。

###############################################################
# 文档
# 另见脚本末尾的“快速开始”
###############################################################
:<<-'is_spammer_Doc

Copyright (c) Michael S. Zick, 2004
License: 任何形式、任何目的的无限制使用。
Warranty: -无（其脚本；用户自负责任）-

立即：
应用代码：前往 "# 寻找垃圾邮件程序 # #"
示例输出：":<<-_is_spammer_outputs-"

提供
给定域名或 IP(v4) 地址作为：

执行一组详尽查询以查找关联网络资源（不递归 TLD）。

对发现的 IP (v4) 地址检查黑名单域名服务器。

如果发现是黑名单 IP(v4) 地址，则报告黑名单文本记录。（通常带有特定报告的链接）。

需要
良好的互联网连接。
（练习：运行脚本时如果未上线则检查或中止。）
支持数组的 Bash (2.05b+)。

外部程序 'dig'
随 'bind' 程序包提供的工具程序。
具体来说是 Bind 9.x 系列的版本。
见：http://www.isc.org

所有 'dig' 的用法都限于封装函数，这些函数可以根据需要重写。详情见：dig_wrappers.bash。
（额外文档） -- 以下

用法
脚本需要单个参数，可以是：

# 附录 A. 贡献脚本

```