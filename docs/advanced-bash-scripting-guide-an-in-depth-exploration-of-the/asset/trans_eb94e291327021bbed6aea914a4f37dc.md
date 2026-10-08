

# 高级 Bash 脚本指南

```
# Stephane Chazelas 指出，上述代码将失败
+# 如果找到的文件过多
+# 或者如果任何文件名包含空白字符。

# 他建议了以下替代方案：
# - find -mtime -1 -type f -print0 | xargs -0 tar vf "$archive.tar"
# 使用 GNU 版本的 "find"。

# find -mtime -1 -type f -exec tar rvf "$archive.tar" '{}' \
# 可移植到其他 UNIX 变体，但速度慢得多。

exit 0
```

以 "-" 开头的文件名在与 "-" 重定向符配合使用时可能会引起问题。脚本应该检查此点，并为此类文件名添加适当的前缀，例如 `./-FILENAME`、`$PWD/-FILENAME` 或 `$PATHNAME/-FILENAME`。

如果变量的值以 - 开头，这可能会产生问题。

```bash
var="-n"
echo $var
# 效果相当于 "echo -n"，并且不输出任何内容。
```

上一个工作目录。`cd -` 命令切换到上一个工作目录。这使用了环境变量 `$OLDPWD`。

> 不要将此意义下使用的 "-" 与刚才讨论的 "-" 重定向符混淆。"-" 的解释取决于它所处的上下文。

减（Minus）。算术运算中的减号。

等号（Equals）。赋值运算符。

```bash
a=28
echo $a # 28
```

在不同的上下文中，“=" 是字符串比较运算符。

加号（Plus）。加法算术运算符。

在不同的上下文中，“+" 是正则表达式运算符。

选项（Option）。命令或过滤器的选项标志位。

某些命令和内置命令使用 `+` 来启用选项，使用 `-` 来禁用它们。通过参数替换，`+` 为变量扩展后的备选值。

取模（modulo）。取模（除法的余数）算术运算。

## 第 3 章 特殊字符

```bash
let "z = 5 % 3*"
echo $ # # 2
```

在不同的上下文中，"%" 是模式匹配运算符。

主目录 [波浪号 ~]。这对应于内部变量 `$HOME`。`~bozo` 是 bozo 的主目录，`~bozo` 列出其内容。`~/` 是当前用户的主目录，`~ls` 列出其内容。

```bash
bash$ echo -bozo
/home/bozo

bash$ echo ~
/home/bozo/

bash$ echo ~:
/home/bozo:

bash$ echo -nonexistent-user
-nonexistent-user
```

当前工作目录。这对应于内部变量 `$PWD`。

上一个工作目录。这对应于内部变量 `$OLDPWD`。

正则表达式匹配。该运算符是在 Bash 3 版本中引入的。

行首（beginning-of-line）。在正则表达式中，“^" 指行的开头。

参数替换中的大写转换（在 Bash 4 版本中添加）。

更改终端或文本显示的行为。控制字符是 CONTROL + 键的组合（同时按下）。控制字符也可以在转义字符后以八进制或十六进制表示表示。

控制字符在脚本内部通常没有用。

- Ctrl-A：将光标移动到文本行的行首（在命令行上）。
- Ctrl-B：退格（非破坏性）。
- Ctrl-C：中断。终止一个前台作业。
- Ctrl-D：从 shell 注销（类似于 exit）。
- EOF（文件结束）。这也会终止来自标准输入的输入。

在控制台或 xterm 窗口中打字时，Ctrl-D 会擦除光标下的字符。当没有字符时，Ctrl-D 会如预期般注销会。在 xterm 窗口中，这具有关闭窗口的效果。

- Ctrl-E：将光标移动到文本行的行尾（在命令行上）。
- Ctrl-F：将光标向前移动一个字符（在命令行上）。
- Ctrl-G：响铃（BEL）。在旧式的电打字终端上，这实际上会响铃。在 xterm 中它会发出哔声。
- Ctrl-H：删除（Rubout，破坏性退格）。擦除光标退格时经过的字符。

```bash
#!/bin/bash
# 在字符串中嵌入 Ctrl-H。
a="^H^H"                                     # 两个 Ctrl-H -- 退格
echo "abcdef"                             # 使用 vi/vim 中的 ctrl-V ctrl-H
echo                                     # abcdef
echo -n "abcdef$a "                       # abcd f
# 结尾有空格                              ^ 退格两次。
echo at end
echo -n "abcdef$a"                        # abcdef
# 结尾没有空格                           # 没有退格（为什么？）。
# 结果可能不完全符合预期。
# Constantin Hagemeier 建议尝试：
# ='\x10\x10'
# ='\b\b'
# ='\x08\x08'
# 但并没有改变结果。
********************************************
```

现在，尝试这个。

rubout=-n "^H^H" # Ctrl-H 效果

```bash
echo -n "1234567"
sleep 2
echo $rubout "12345"
```

- Ctrl-I：水平制表。
- Ctrl-J：换行（回车）。
- Ctrl-K：删除从光标到行尾的内容。
- Ctrl-D：换行符（删除键/回车）。

在控制台或 xterm 窗口中打字时，Ctrl-D 会擦除光标下的字符。当没有字符时，Ctrl-D 会如预期般注销会。在 xterm 窗口中，这具有关闭窗口的效果。

- Ctrl-E：将光标移动到文本行的行尾（在命令行上）。
- Ctrl-F：将光标向前移动一个字符（在命令行上）。
- Ctrl-G：响铃（BEL）。在旧式的电打字终端上，这实际上会响铃。在 xterm 中它会发出哔声。
- Ctrl-H：删除（Rubout，破坏性退格）。擦除光标退格时经过的字符。

