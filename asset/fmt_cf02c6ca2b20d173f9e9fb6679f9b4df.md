
[me@linuxbox]$ deletion-script

preparing to delete files

deleting files

file deletion complete

[me@linuxbox]$
```
`bash` 还提供了一种追踪方法，通过 `-x` 以及带有 `-x` 的 `set` 命令实现。使用我们之前的故障脚本，可以通过在第一行添加 `-x` 来激活整个脚本的追踪：

```bash
#!/bin/bash -x

### trouble: script to demonstrate common errors

number=1
```

## 30 – 故障排除

```bash
if [ $number = 1 ]; then
    echo "Number is equal to 1."
else
    echo "Number is not equal to 1."
fi
```

执行时，结果如下：

```
me@linuxbox ~]$ trouble
+ number=1
+ ['' 1 = '1']
+ echo 'Number is equal to 1'
Number is equal to 1
```

启用追踪后，我们可以看到实际执行的命令。开头的加号表示追踪显示，以便将其与输出行区分开。加号是追踪输出的默认字符。它包含在 `PS4`（提示符字符串 4）变量中。可以调整该变量的内容使提示符更有用。在这里，我们修改变量的内容，以包含执行追踪时脚本中的当前行号。注意，需要单引号来防止在提示符实际使用之前进行展开：

```
me@linuxbox ~]$ export PS4=$LINEENO + ' \'
me@linuxbox ~]$ trouble
5 + number=1
7 + ['' 1 = '1']
8 + echo 'Number is equal to 1'
Number is equal to 1
```

为了对脚本的选部分进行追踪而不是整个脚本，可以使用带有 `-x` 的 `set` 命令：

```bash
#!/bin/bash

### trouble: script to demonstrate common errors

number=1

set -x # 开启追踪

if [ $number = 1 ]; then
    echo "Number is equal to 1."
```

426

```
else
    echo "Number is not equal to 1."
fi
    set +x # 关闭追踪
```

我们使用 `set` 命令配合 `-x` 选项激活追踪，配合 `+x` 选项禁用追踪。这种技术可以用于检查故障脚本的多个部分。

### 在执行期间检查值

在追踪的同时，显示变量的内容对于查看脚本执行期间的内部机制通常有用。添加额外的 `echo` 语句通常可以奏效：

```bash
#!/bin/bash

### trouble: script to demonstrate common errors

number=1

echo "number=$number" # DEBUG

set -x # 开启追踪

if [ $number = 1 ]; then
    echo "Number is equal to 1."
else
    echo "Number is not equal to 1."
fi

    set +x # 关闭追踪
```

在这个简单的示例中，我们仅显示了变量 `number` 的值，并为添加的行标记注释，以便稍后识别和删除。这种技术在观察脚本中循环和算术运算的行为时特别有用。

### 总结

在本章中，我们查看了脚本开发过程中可能发生的几个问题。当然，还有很多其他问题。这里描述的技术将能够发现大多数常见的 bug。调试是一门艺术，可以通过经验培养，既包括了解如何避免 bug（在整个开发过程中不断测试），也包括发现 bug（有效利用追踪）。

### 扩展阅读

- *维基百科有几篇关于语法和逻辑错误的短文：*
  http://en.wikipedia.org/wiki/Syntax_error
  http://en.wikipedia.org/wiki/Logic_error
- 有许多关于 `bash` 编程技术方面的在线资源：
  http://mywiki.wooodle.org/BashPitfalls
  http://tdlp.org/LDP/abs/html/gotchas.html
  http://www.gnu.org/software/bash/manual/html/Reserved-Word-Index.html
- Eric Raymond 的《Unix 编程艺术》（Art of Unix Programming）是学习良好的 Unix 程序中基础概念的极佳资源。这些思想许多适用于 shell 脚本：
  http://www.faqs.org/docs/artu/
  http://www.faqs.org/docs/ch01s06.html
- 对于高强度调试，有 Bash 调试器：
  http://bash.net/

### 流程控制：使用 case 分支

在本章中，我们将继续查看流程控制。在第28章中，我们使用简单的 `if` 语句来识别选择了哪些选项。为了这一点，我们使用 `case` 命令，它出现在程序中。`case` 命令查看 `word` 的值（在示例中为 `REPLY` 变量的值），然后尝试将其与指定的模式进行匹配。当匹配成功时，将执行与指定模式相关的命令。一旦找到匹配项，将不再尝试其他匹配。它的语法如下：

```
case word in
  pattern...) commands ;;
esac
```

这是一个模式工作的示例：

```bash
#!/bin/bash

### case-menu: 一个菜单驱动系统程序

clear

echo "请选择：
1. 显示信息
2. 显示磁盘空间
3. 显示主目录占用
0. 退出
read -p "输入选择 [0-3]: "

case $REPLY in

0)
    echo "程序终止。"
    exit
    ;;

1)
    echo "主机: $HOSTNAME"
    uptime
    ;;

2)
    df -h
    ;;

3)
    if [[ $(id -u) -eq 0 ]]; then
        echo "用户占用（所有用户）"
        du -sh /home/*
    else
        echo "用户占用（USER）"
        du -sh $HOME
    fi
    ;;

*)
    echo "无效输入" >&2
    exit 1
    ;;

esac
```

### 模式

`case` 使用的模式与路径扩展（pathname expansion）使用的模式相同。模式以 `)` 字符结束。以下是一些有效的模式：

| 模式 | 描述 |
|---|---|
| [[:alpha:]] | 如果单词是单个字母则匹配。 |
| ??? | 如果单词长度正好为三个字符则匹配。 |
| *.txt | 如果单词以 ".txt" 结尾则匹配。 |
| *) | 匹配任何值。在 `case` 命令最后包含此模式是一个良好的习惯，以捕获未匹配之前模式的任何值；即捕获所有可能的无效值。 |

## 31 – 分流控制：使用 case 进行分支

```bash
#!/bin/bash

read -p "输入单词 > " 

case $REPLY in
  [:alpha:]]]) echo "是一个单个字母字符."; 
  [ABC][0-9]) echo "是以 A、B 或 C 开头后跟一个数字."; 
  ???) echo "长度为三个字符."; 
  *.txt) echo "是以 .txt 结尾的单词"; 
  *) echo "是其他内容。"
esac
```

还可以使用竖线字符 `|` 作为分隔符来组合多个模式。这创建了一个“或”逻辑条件模式。这对于诸如同时处理大写和小写字符非常有用。例如：

```bash
#!/bin/bash

### case-menu: 一个菜单驱动的系统信息程序

clear

echo ""

请选择：

A. 显示系统信息

B. 显示磁盘空间

C. 显示主空间利用率

Q. 退出

"
read -p "输入选择 [A, B, C 或 Q] > " 

case $REPLY in
  q|Q) echo "程序终止。"
    exit
    ;
a|A) echo "主机名: $HOSTNAME"
    uptime
    ;
b|B) df -h
    ;
c|C) if [[ $(id -u) -eq 0 ]]; then
    echo "主空间利用率（所有用户）"
    du -sh /home/*
