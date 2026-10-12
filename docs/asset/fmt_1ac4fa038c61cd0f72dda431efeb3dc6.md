
## 使用特殊变量

以下代码展示了一个使用所有特殊变量的脚本示例。

```bash
#!/bin/sh
echo "脚本的名称是 $0"
echo "参数的个数是 $#"
echo "第一个参数的值是 $1"
echo "第二个参数的值是 $2"
echo "所有参数的值为: $@"
echo "当前进程 id 是 $$"
uptime
echo "命令 uptime 的退出状态为 $?"
notexisting
echo "命令 notexisting 的退出状态为 $?"
```

图 12.4 显示了当向名为 `example4.sh` 的脚本传递三个参数时的示例输出：

```
$agonzalez@ubuntu:~$ ./example4.sh alberto gonzalez rodriguez
脚本的名称是 ./example4.sh
参数的个数是 3
第一个参数的值是 alberto
第二个参数的值是 gonzalez
所有参数的值为: alberto gonzalez rodriguez
当前进程 id 是 17247
15:16:59 up 21:00, 1 user, load average: 0.00, 0.00, 0.00
命令 uptime 的退出状态为 0
./example4.sh: 10: notexisting: not found
命令 notexisting 的退出状态为 127
```

图 12.4：在 shell 脚本中使用特殊变量

## 使用条件语句

使用 shell 脚本最大的优势之一是可以使用条件。条件允许应用程序根据指示的变量或不同表达式做出决策。以下是这些条件判断的语法：

### `if/else` 语句
它评估 `if` 中指定的表达式，如果为真，则执行其内部指定的操作。如果表达式为假，则执行 `else` 块内部的指令。其语法如下：

```
if EXPRESSION; then
if_statements
else
else_statements
fi
```

### `if/elif/else` 语句
与上一个相同，但 `elif` 元素评估的表达式与 `if` 不同。语法如下，它可以包含若干个 `elif` 元素：

```
if EXPRESSION then
if_statements
elif EXPRESSION2 then
elif_statements1
elif EXPRESSION3 then
elif_statements2
else
else_statements
fi
```

### `case/esac` 语句
它评估一个表达式并匹配定义的不同模式。如果其中一个模式匹配，将执行定义的语句。其语法如下：

```
case EXPRESSION in
PATTERN_1)
STATEMENTS
  ;
PATTERN_2)
STATEMENTS
  ;
*)
STATEMENTS
  ;
esac
```

## 表达式与比较

作为条件评估的表达式是基于内置函数 `test` 的可用表达式。该表达式可以使用方括号 `[ ]` 包裹，也可以跟在单词 `test` 之后。以下代码展示了这两种语法的等效示例：

```
if [ $# -ne 1 ]; then
echo "Number of arguments should be one"
fi
if test $# -ne 1; then
echo "Number of arguments should be one"
fi
```

这些表达式用于检查和比较。在前面的代码中，检查项 `-ne` 表示“不等于”。可常用的检查和比较及其相应的描述如表 12.2 所示：

| Check | 描述 |
| :--- | :--- |
| `-n STRING` | `STRING` 的长度不为零 |
| `-z STRING` | `STRING` 的长度为零 |
| `STR1 = STR2` | 两个字符串相等 |
| `STR1 != STR2` | 两个字符串不相等 |
| `INT1 -eq INT2` | 两个整数相等 |
| `INT1 -ge INT2` | 第一个整数大于或等于第二个 |
| `INT1 -gt INT2` | 第一个整数大于第二个 |
| `INT1 -le INT2` | 第一个整数小于或等于第二个 |
| `INT1 -lt INT2` | 第一个整数小于第二个 |
| `INT1 -ne INT2` | 第一个整数不等于第二个 |
| `FILE1 -nt FILE2` | `FILE1` 比 `FILE2` 新（修改日期） |
| `FILE1 -ot FILE2` | `FILE1` 比 `FILE2` 旧 |
| `-d FILE` | 指定的文件存在且是一个目录 |
| `-e FILE` | 指定的文件存在 |
| `-f FILE` | 指定的文件存在且是一个普通文件 |
| `-L FILE` | 指定的文件存在且是一个符号链接 |
| `-r FILE` | 指定的文件存在且已授予读权限 |
| `-s FILE` | 指定的文件存在且大小大于零 |
| `-w FILE` | 指定的文件存在且已授予写权限 |
| `-x FILE` | 指定的文件存在且已授予执行权限 |

表 12.2：选项组及描述

可以在检查项前加上感叹号（`!`）来反转条件。以下代码展示了一个检查文件不存在的示例：

```
if [ ! -f /etc/backup.cfg ]; then
echo "Backup configuration doesn't exist"
fi
```

表达式可以是不同检查的组合，使用 `-a` 表示“与”（and），或使用 `-o` 表示“或”（or）。也可以使用双安培符号（`&&`）表示与条件，双竖线（`||`）表示或条件。以下代码展示了一个使用四种选项语法的示例：

```
if [ $1 != "show" -a $1 != "display" ]; then
echo "First argument should be 'show'"
fi
```

```bash
case $OPTION in
1)
who
;
2)
echo "Uptime: "
uptime
;
*)
echo "Invalid option indicated"
;
esac
read -p "Select an option: " OPTION
done
```

## 循环

上一个示例可以重写为使用 `until`，如下所示：

```bash
until [ $OPTION -eq 3 ]; do
    statements
done
```

可以使用 `break` 语句退出循环并继续进入下一次迭代。以下代码显示了一个用法示例：
