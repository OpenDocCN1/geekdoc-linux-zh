

# 表 9-13 bash 特性（续）

| 特性 | 说明 | 语法 | 替代语法 |
| --- | --- | --- | --- |
| history | 启用命令历史（默认开启；第 330 页）。 | set –history | |
| huponexit | 指定当交互式登录 shell 退出时，bash 向所有作业发送 SIGHUP 信号。 | shopt –s huponexit | |
| ignoreeof | 指定 bash 在退出前必须接收十个 EOF 字符。对于嘈杂的拨号线路有用。 | set –o ignoreeof | |
| monitor | 启用作业控制（默认开启，第 307 页）。 | set –monitor | set –m |
| nocaseglob | 使模糊的引用引用（第 256 页）在不区分大小写的情况下匹配文件名（默认关闭）。 | shopt –s nocaseglob | |
| noclobber | 帮助防止覆盖文件（默认开启；第 248 页）。 | set –o noclobber | set –C |
| noglob | 禁用路径名扩展（默认关闭；第 256 页）。 | set –o noglob | set –f |
| notify | 在启用作业控制（第 307 页）时，立即报告后台作业的终止状态。默认行为是显示状态直到下次提示。 | set –o notify | set –b |
| nounset | 当在交互式 shell 中使用未定义的变量时，显示错误并退出 shell 脚本。默认对未定义的变量显示空值。 | set –o nounset | set –u |
| nullglob | 使 bash 扩展不匹配空字符串的文件名引用（第 256 页）。默认情况下，bash 直接传递这些引用而不对其进行扩展。 | shopt –s nullglob | |
| posix | 在 POSIX 模式下运行 bash。 | set –o posix | |
| verbose | 在 bash 读取命令行时显示该命令行。 | set –o verbose | set –v |
| vi | 指定使用 vi 模式进行命令行编辑（第 340 页）。 | set –o vi | |
| xpg_echo | 使内置的 echo 命令在不需要使用 –e 选项的情况下扩展转义序列（第 980 页）。 | shopt –s xpg_echo | |
| xtrace | 开启 shell 调试（第 966 页）。 | set –o xtrace | set -x |

# 处理命令行

无论你是进行交互式操作还是运行 bash 脚本，bash 在开始处理命令行之前都需要读取该命令行——bash 在处理命令之前总是至少会读取一行。某些 bash 内置命令（如 `if` 和 `case`）以及函数和引用字符串跨越多行。当 bash 识别出一个包含超过一行的命令时，它会在处理之前读取整个命令。在交互式会话中，每当你输入多行命令的每一行时，bash 会提示次级提示符（PS2，默认为 >；第 322 页），直到识别出命令的结束：

```
$ echo 'hi
> end'
hi
end
$ function hello () {
> echo hello there
> }
$
```

在读取命令行后，bash 会对该行执行历史扩展和别名替换。

# 历史扩展

第 332 页的“重新执行和编辑命令”讨论了你可以提供的用于修改和重新执行历史列表中命令行的命令。历史扩展是 bash 用于将历史命令转换为可执行命令的过程。例如，当你给出命令 `!!` 时，历史扩展会更改该命令行，使其与上一个命令相同。历史扩展在交互式 shell 中默认开启；使用 `set +o histextend` 可以将其关闭。历史扩展不适用于非交互式 shell（shell 脚本）。

# 别名替换

别名（第 346 页）用字符串替换简单命令的单词。默认情况下，交互式 shell 开启别名，非交互式 shell 关闭。执行命令 `opt -u expand_aliases` 可以关闭别名。

# 解析和扫描命令行

在处理历史命令和别名之后

```
$ cp ~/letter .
```

在执行命令之前分离标记（tokens）之后，shell 会扫描这些标记并执行命令行扩展。

# 命令行扩展

交互式和非交互式 shell 在将命令行传递给调用的程序之前，都会使用命令行扩展转换命令行。你可以在不了解许多命令行扩展的情况下使用 shell，但理解这个主题后，可以更好地利用 shell 提供的功能。本节介绍了 Bourne Again Shell 的命令行扩展。

Bourne Again Shell 按照以下顺序对每个标记进行各种类型的扩展和替换。这些过程中的大多数将一个单词扩展为单个单词。只有大括号扩展、单词分割和路径名扩展可以改变命令中单词的数量（变量 @ 的扩展除外——见第 1000 页）。

1. 大括号扩展（第 358 页）
2. 波浪号扩展（第 359 页）
3. 参数和变量扩展（第 360 页）
4. 算术扩展（第 360 页）
5. 命令替换（第 362 页）
6. 单词分割（第 363 页）
7. 路径名扩展（第 363 页）
8. 进程替换（第 365 页）

> 去除引号：在 bash 完成上述列表后，它会从命令行移除单引号、双引号以及不是扩展结果的反斜杠。这个过程被称为去除引号。

# 扩展顺序

bash 执行这些步骤的顺序会影响解释。例如，如果你使用大括号表示法的命令，shell 会扩展大括号内的内容。

```
$ echo chap_{one,two,three}
chap_one.txt chap_two.txt chap_three.txt
```

shell 将 echo 命令中大括号内逗号分隔的字符串扩展为空格分隔的字符串列表。列表中的每个字符串前面加上 `chap_`（称为前缀），后面加上 `.txt`（称为后缀）。前缀和后缀都是可选的。大括号内字符串从左到右的顺序在扩展中得以保留。为了 shell 特殊处理左右大括号并发生大括号扩展，大括号内必须至少有一个逗号且没有空格字符。你可以嵌套大括号。

# 大括号扩展

大括号扩展源于 C Shell，在路径名扩展不适用提供了一种指定文件的方便方法。虽然大括号扩展通常用于指定文件名，但该机制可以生成任意字符串；shell 不尝试将大括号表示法与现有文件进行匹配。

大括号扩展默认对交互和非交互式 shell 开启；可以使用 `set +expand` 将其关闭。shell 还使用括号来隔离变量（第 316 页）。

下面的示例说明了大括号扩展的工作原理。ls 命令没有显示任何输出，因为工作目录下没有文件。内置的 echo 显示了 shell 通过大括号扩展生成的字符串。在这种情况下，这些字符串与文件名不匹配。

```
$ echo chap_{one,two,three}.txt
chap_one.txt chap_two.txt chap_three.txt
```

大括号扩展在有长前缀或后缀时非常有用。下面的示例将 /usr/local/src/C/ 目录下的 main.c、f1.c、f2.c 和 tmp.c 复制到工作目录：

```
$ cp /usr/local/src/C/{main,f1,f2,tmp}.c
```

你还可以使用大括号扩展创建命名相关的目录：

```
$ ls -F
file1 file2 file3
$ mkdir vrs{A,B,C,D,E}
$ ls -F
file1 file2 file3 vrsA/ vrsB/ vrsC/ vrsD/ vrsE/
```

