
`case` 命令查看 `word` 的值（在我们的示例中是 `REPLY`），然后尝试将其与模式进行匹配。找到匹配，则执行与该模式相关的命令。一旦找到匹配，将不再尝试其他匹配。

# 模式 (Patterns)

`case` 使用的模式与路径扩展相同。模式以 `)` 字符结束。表 31-1 描述了一些模式。

# 表 31-1: case 模式示例

| 模式 | 描述 |
|---|---|
| a) | 如果 *word* 等于 a。 |
| [[:alpha:]]) | 如果 *word* 是单个字母。 |
| ???)) | 如果 *word* 恰好为三个字符。 |
| *.txt | 如果 *word* 以 .txt 结尾 |
| *) | 匹配 *word* 的任何值。在 `case` 命令中将其作为最后一个模式是良好的习惯，以捕捉任何未匹配之前模式的值。 |

这里有一个模式工作的示例：

```bash
#!/bin/bash

read -p "enter word: "
case "$REPLY" in
  [[:alpha:]]) echo "是单个字母."; 
  [ABC][0-9]) echo "是 A, B, 或 C 后面跟着一个数字."; 
  ???) echo "是三个字符."; 
  *.txt) echo "是以 .txt 结尾的单词"; 
  *) echo "是其他内容."; 
esac
```

还可以使用竖线作为分隔符组合多个模式。这创建了一个“或”条件模式。这对于处理大小大小写字母的情况非常有用。这里有一个例子：

```bash
#!/bin/bash
# case-menu: 一个菜单驱动的系统信息程序
clear
echo ""
echo "Select:"
echo "A. Display System Information"
echo "B. Display Disk space"
echo "C. Display Space Utilization"
echo "Q. Quit"
read -p "Enter selection [A, B, C or Q]: " 
case "$REPLY" in
  q|Q) echo "Program terminated."
    exit
  a|A) echo "Display System Information"
    ;;
  b|B) echo "Display Disk space"
    ;;
  c|C) echo "Display Space Utilization"
    ;;
  *) echo "Invalid entry" >&2
    exit 1
    ;;
esac
```

```bash
b|B)   ;
      df -h
      ;
c|C) if [[ "$($id -u)" -eq 0 ]]; then
        echo "Home Space Utilization (All Users)"
        du -sh /home/*
      else
        echo "Home Space Utilization ($USER)"
        du -sh "$HOME"
      fi
      ;
*)   ;
echo "Invalid entry" >&2
      exit 1
      ;
esac
```

在这里，我们修改了 `case` 菜单程序，使其使用字母而不是数字进行菜单选择。注意看新模式如何允许输入大写和小小写字母。

## 执行多个操作

在 `bash` 4.0 之前的版本中，`case` 仅在匹配成功时允许执行一个操作。匹配成功后，命令就会终止。这里我们看到一个测试字符的脚本：

```bash
#!/bin/bash
```

```bash
# case4-1: test a character > 
read -n 1 -p "Type a character > " 
echo
case "$REPLY" in
  [:upper:]]) echo "$REPLY is upper case."; ;
  [:lower:]]) echo "$REPLY is lower case."; ;
  [:alpha:]]) echo "$REPLY is alphabetic."; ;
  [:digit:]]) echo "$REPLY is a digit."; ;
  [:graph:]]) echo "$REPLY is a visible character."; ;
  [:punct:]]) echo "$REPLY is a punctuation symbol."; ;
  [:space:]]) echo "$REPLY is a whitespace character."; ;
  [:xdigit:]]) echo "$REPLY is a hexadecimal digit."; ;;
esac
```

运行此脚本会产生：

```bash
me@linuxbox ~$ case4-1
Type a character > a
'a' is lower case.
```

该脚本在大多数情况下可以工作，但如果字符匹配了 POSIX 字符类之一，就会失败。例如，该字符既是小写字母又是字母，还是十六进制数字。在 4.0 之前的之前的 `bash` 中，没有方法同时匹配多个测试。现代版本的 `bash` 引入了 `;&;` 符号表示结束每个操作，因此现在我们可以这样做：

```bash
#!/bin/bash
```

```bash
# case4-2: test a character
read -n 1 -p "Type a character > " 
echo
case "$REPLY" in
  [[:upper:]]]) echo "$REPLY is upper case." ;;&  
  [[:lower:]]]) echo "$REPLY is lower case." ;;&  
  [[:alpha:]]]) echo "$REPLY is alphabetic." ;;&  
  [[:digit:]]]) echo "$REPLY is a digit." ;;&  
  [[:graph:]]]) echo "$REPLY is a visible character." ;;&  
  [[:punct:]]]) echo "$REPLY is a punctuation symbol." ;;&  
  [[:space:]]]) echo "$REPLY is a whitespace character." ;;&  
  [[:xdigit:]]]) echo "$REPLY is a hexadecimal digit." ;;&
esac
```

当我们运行此脚本时，我们得到：

```bash
me@linuxbox ~$ case4-2
Type a character >
  'a' is lower case.
  'a' is alphabetic.
  'a' is a visible character.
  'a' is a hexadecimal digit.
```

`;;&` 语法的添加允许 `case` 继续进行下一个测试，而不是简单地终止。

## 总结

`case` 命令是我们编程技巧箱中一个非常实用的补充。正如我们在下一章中看到的，它是处理某些类型问题的完美工具。

# 32

## 位置参数 (POSITIONAL PARAMETERS)

到目前为止我们的程序中缺失的一个功能是接受和处理命令行选项和参数。在本章中，我们将研究允许程序访问命令行内容的 shell 特性。

## 命令行参数

`shell` 提供一组名为位置参数的变量，包含了命令行中的每一个单词。这些变量通过 `$0` 到 `$9` 来访问。`$0` 是脚本本身，而 `$1` 到 `$9` 分别代表命令行中的第一个到第九个参数。

可以使用下面的脚本：

```bash
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "Third argument: $3"
echo "Fourth argument: $4"
echo "Fifth argument: $5"
echo "Sixth argument: $6"
echo "Seventh argument: $7"
echo "Eighth argument: $8"
echo "Ninth argument: $9"
```

如果你运行这个脚本：

```bash
bash script.sh a b c d e f g h i j k l m n
```

输出将是：

```
Script name: ./script.sh
First argument: a
```
