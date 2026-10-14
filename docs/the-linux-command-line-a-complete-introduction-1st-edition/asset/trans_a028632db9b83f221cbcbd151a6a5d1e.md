

```
${!prefix*}
${!prefix@}
```

此展开返回名称以 *prefix* 开头的现有变量的名称。根据 bash 文档，两种形式的展开执行效果相同。这里，我们列出环境中所有名称以 BASH 开头的变量：

```
[me@linuxbox ~]$ echo ${!BASH*}
BASH BASH_ARGC BASH_ARGV BASH_COMMAND BASH_COMPLETION BASH_COMPLETION_DIR
BASH_LINENO BASH_SOURCE BASH_SUBSHELL BASH_VERSINFO BASH_VERSION
```

## 字符串操作

有一组很大的展开可用于对字符串进行操作。其中许多展开特别适合对路径名进行操作。展开

```
${#parameter}
```

展开为 *parameter* 所包含的字符串的长度。通常，*parameter* 是一个字符串；然而，如果 *parameter* 是 @ 或 *，则展开结果为位置参数的数量。

```
[me@linuxbox ~]$ foo="This string is long."
[me@linuxbox ~]$ echo "$foo" is ${#foo} characters long.
This string is long. is 20 characters long.
```

```
${parameter:offset}
${parameter:offset:length}
```

此展开用于提取 *parameter* 中包含的字符串的一部分。提取从字符串开头算起的 *offset* 个字符处开始，直到字符串末尾，除非指定了 *length*。

```
[me@linuxbox ~]$ foo="This string is long."
[me@linuxbox ~]$ echo ${foo:5}
string is long.
[me@linuxbox ~]$ echo ${foo:5:6}
string
```

如果 *offset* 的值为负，则表示它从字符串末尾开始而不是从开头开始。请注意，负值必须前面加上一个空格以防止与 `${parameter:-word}` 展开混淆。*length*，如果存在，不得小于 0。

如果 *parameter* 是 @，则展开的结果是 *length* 个从 *offset* 开始的位置参数。

```
[me@linuxbox ~]$ foo="This string is long."
[me@linuxbox ~]$ echo ${foo: -5}
long.
[me@linuxbox ~]$ echo ${foo: -5:2}
lo
```

```
${parameter#pattern}
${parameter##pattern}
```

这些展开从 parameter 中包含的字符串中移除由 pattern 定义的前导部分。pattern 是像路径名展开中使用的那样通配符模式。两种形式的区别在于 # 形式移除最短的匹配，而 ## 形式移除最长的匹配。

```
[me@linuxbox ~]$ foo=file.txt.zip
[me@linuxbox ~]$ echo ${foo#*.}
txt.zip
[me@linuxbox ~]$ echo ${foo##*.}
zip
```

```
${parameter%pattern}
${parameter%%pattern}
```

这些展开与上面的 # 和 ## 展开相同，只是它们从 parameter 中包含的字符串末尾移除文本而不是从开头移除。

```
[me@linuxbox ~]$ foo=file.txt.zip
[me@linuxbox ~]$ echo ${foo%.*}
file.txt
[me@linuxbox ~]$ echo ${foo%%.*}
file
```

```
${parameter/pattern/string}
${parameter//pattern/string}
${parameter/#pattern/string}
${parameter/%pattern/string}
```

此展开对 parameter 的内容执行搜索和替换。如果找到与通配符 pattern 匹配的文本，则将其替换为 string 的内容。在普通形式中，仅替换 pattern 的第一次出现。在 // 形式中，替换所有出现。/# 形式要求匹配发生在字符串开头，/% 形式要求匹配发生在字符串末尾。/string 可以省略，这会导致 pattern 匹配的文本被删除。

```
[me@linuxbox ~]$ foo=JPG.JPG
[me@linuxbox ~]$ echo ${foo/JPG/jpg}
jpg.JPG
[me@linuxbox ~]$ echo ${foo//JPG/jpg}
jpg.jpg
[me@linuxbox ~]$ echo ${foo/#JPG/jpg}
jpg.JPG
[me@linuxbox ~]$ echo ${foo/%JPG/jpg}
JPG.jpg
```

参数展开是一个值得了解的好东西。字符串操作展开可以用作 sed 和 cut 等其他常用命令的替代品。展开通过消除外部程序的使用提高了脚本的效率。作为示例，我们将修改上一章中讨论的最长单词程序以使用参数展开。
