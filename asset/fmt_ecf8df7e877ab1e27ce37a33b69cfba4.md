
# 示例 10–5. for 循环中缺失 [list]

第 10 章 循环与分支 104

# 高级 Bash 脚本指南

```bash
#!/bin/bash

# 分别带参数和不带参数调用，查看会发生什么

for a
do
  echo -n "$a "
done

# 缺少 'in list'，因此循环对 '$@' 操作
#（命令行参数列表，包括空格）

echo

exit 0
```

可以使用命令替换来生成 for 循环中的 [list]。请参见另示例 12–34、示例 10–10 以及示例 12–31。

# 示例 10–6. 使用命令替换在 for 循环中生成 [list]

```bash
#!/bin/bash
# 使用命令替换生成 [list] 的 for 循环。

NUMBERS="9 7 3 8 37.53"

for number in `echo $NUMBERS` # for number in 9 7 3 8 37.53
do
  echo -n "$number "
done
echo
exit 0
```

这是一个使用命令替换创建 [list] 的较复杂的示例。

# 示例 10–7. 针对二进制文件的 grep 替换

```bash
#!/bin/bash
# bin-grep.sh 在二进制文件中查找匹配的字符串。

# 针对二进制文件的 "grep" 替换方案。
# 效果与 "grep -a" 相似。

E_BADARGS=65
E_NOFILE=66

if [ $# -ne 2 ]
then
  echo "Usage: `basename $0` string filename"
  exit $E_BADARGS
fi

if [ ! -f "$2" ]
then
  echo "File \$2" does not exist."
  exit $E_BADARGS
fi

# 第 10 章 循环与分支 109

# 高级 Bash 脚本指南
```

# 高级 Bash 脚本指南

请参见示例 26–7、示例 26–8 和示例 A–6。

现在，我们在“真实生活”场景中使用 `for-loop`（for 循环）。

# 示例 10–13. 使用批量模式下的 efax

```bash
#!/bin/bash

EXPECTED_ARGS=2
E_BADARGS=65

if [ $# -ne $EXPECTED_ARGS ]
  # 检查命令行参数是否正确。
then
  echo "Usage: $basename $0# phone text-file"
  exit $E_BADARGS
fi

if [ ! -f "$2" ]
then
  echo "File $2 is not a text file"
  exit $E_BADARGS
fi

fax make $2                     # 从文本文件创建传真格式的文件。

for file in $(ls $2.0*) # 合并转换后的文件。
  # 在变量列表中通配符。
do
  file="$file$file"
done

efax -d /dev/ttyS3 -ol -t "T1" $file # 执行工作。

# 正如 S.C 指出的，for-loop 可以被消除
# efax -d /dev/ttyS3 -ol -t "T1" $2.0
# 但这样并不十分具有启发性 [笑]。

exit 0
```

## while

这在循环顶部构建了一个测试，只要条件为真（返回退出状态 0），它就会继续循环。与 for 循环相比，`while loop`（while 循环）用于预先未知循环重复次数的情况。

```bash
while [condition]
do
  command...
done
```

与 for/in 循环一样，将 `do` 置于条件测试放在同一行需要一个分号（;）。

```bash
while [condition] ; do
```

注意，某些特殊的变量循环（例如 `getopts` 结构）在 particular 处与标准模板有所不同。

### 示例 10–14. 简单的 while 循环

```bash
#!/bin/bash
var0=0
LIMIT=10

while [ "$var0" -lt "$LIMIT" ];
do
    echo -n "$var0 "      # -n 抑制换行。
    var0=$(expr $var0 + 1)  var0=$((var0+1)) 同样有效。
done
echo
exit 0
```

### 示例 10–15. 另一个 while 循环

```bash
#!/bin/bash
echo
while [ "$varl" != "end" ];  # while 测试 "$varl" != "end"
do
    # 同样有效。
    echo "Input variable #1 (end to exit)"
    read varl                        # 没有读取 '$varl'（为什么？）。
    echo "variable #1 $varl"         # 因为 "#" 需要引号
    # 如果输入是 'end'，则在此处回显它。
    # 在循环顶部之前不会测试终止条件。
echo
done
exit 0
```

一个 while 循环可以有多个条件。只有最后一个条件决定循环是否终止。然而，这需要略有不同的循环语法。

### 示例 10–16. 带有多个条件的 while 循环

```bash
#!/bin/bash
varl=unset
previous=$varl

while echo "previous-variable = $previous"
do
    echo
    previous=$varl
    [ $varl != ] # 记录 $varl 之前的值。
    # 针对 "while" 的条件，但只有最后一个控制循环。
    # *最后一个*退出状态才是起作用。
    echo "Input variable #1 (end to exit)"
    read var
    echo "variable #1 = $varl"
done

# 尝试弄清楚这这一切是如何工作的。
# 这有点复杂。
exit 0
```

与 for 循环一样，while 循环可能通过使用双括号采用类似 C 的语法。

# 10–17. while 循环中的类似 C 的语法

```bash
#!/bin/bash
echo
while [ "$varl" != "end" ];  # while 测试 "$varl" != "end"
do
    # 同样有效。
    echo "Input variable #1 (end to exit)"
    read varl                        # 没有读取 '$varl'（为什么？）。
    echo "variable #1 $varl"         # 因为 "#" 需要引号
    echo "variable #1 = $varl"
    # 如果输入是 'end'，则在此处回显它。
    # 在循环顶部之前不会测试终止条件。
echo
done
exit 0
```

## until

这种结构在循环顶部进行测试，并且只要条件为假（与 while 循环相反），就会继续循环。

```bash
until [condition]
do
  command...
done
```

注意，until 循环在循环顶部测试终止条件。与 for 循环一样，将 `do` 置于条件放在同一行需要一个分号。

```bash
until [condition] ; do
```

### 示例 10–18. until 循环

```bash
#!/bin/bash
until [ "$var" = end ] # 在此处测试条件。
do
  echo "Input variable #1 (end to exit)"
  read var
  echo "variable #1 $var"
done
exit 0
```

## 10.2. 嵌套循环

嵌套循环是循环中的循环，即外部循环体内部的循环。发生的情况是外部循环的第一次通过触发内部循环并执行完毕。外部循环的第二次通过再次触发内部循环。这会重复直到外部循环结束。当然，内部或外部循环中的 `break` 可能会中断这一过程。

### 示例 10–19. 嵌套循环

```bash
#!/bin/bash
# 嵌套的 "for" 循环。

outer=1      # 设置外部循环计数。
# 外部循环开始。
for a in 1 2 3 4 5
do
  echo "Pass $outer in outer loop."
  echo "----------------------"
  inner=1      # 重置内部循环计数。
  # 内部循环开始。
  for b in 1 2 3 4 5
  do
    echo "Pass $inner in inner loop."
    inner+=1 # 增加内部循环计数。
  done
  # 内部循环结束。
  outer+=1 # 增加外部循环计数。
  # 外部循环通过之间的输出。
done
# 外部循环结束。
```

请参见示例 26–4 关于嵌套 "while" 循环的说明，以及示例 26–5 查看嵌套在 "until" 循环内部的 "while" 循环。

## 10.3. 循环控制

### 影响循环的命令

`break` 和 `continue` 循环命令与其编程语言中的对应物完全对应。`break` 终止循环（跳出），而 `continue` 导致跳转到循环的下次迭代，跳过该特定循环中的剩余命令。

### 示例 10–20. 循环中 break 和 continue 的影响

```bash
#!/bin/bash
LIMIT=19 # 上限
echo
echo "Printing Numbers 1 through 20 (but 3 and 11)."

a=0
while [ "$a" -le $LIMIT ]
do
  a=$((a+1))

  if [ "$a" -eq 3 ] || [ "$a" -eq 11 ] # 排除 3 和 11
  then
    continue # 跳过本次迭代的剩余部分。
  fi

  echo -n "$a "
done

# 练习：
# 为什么循环打印到 20？
```

```bash
echo; echo
echo Printing Numbers 1 through 20, but something happens after 2.
######################################################
# 相同的循环，但将 'continue' 替换为 'break'
a=0
while [ "$a" -le "$LIMIT ]
do
  a=$((a+1))
  if [ "$a" -gt 2 ];
  then
    break # 跳过整个循环剩余部分。
  fi
  echo -n "$a "
done
echo; echo; echo
exit 0
```

`break` 命令可以可选地接受一个参数。普通的 `break` 只终止其嵌入的最内层循环，但 `break N` 会跳出 N 层循环。

### 示例 10–21. 跳出多层循环

```bash
#!/bin/bash
# break-levels.sh: 跳出循环。

# "break N" 跳出 N 层的循环。
for outerloop in 1 2 3 4 5
do
  echo -n "Group $outerloop: "
  for innerloop in 1 2 3 4 5
  do
    echo -n "$innerloop"
    if [ "$innerloop" -eq 3 ];
    then
      break # 尝试 break 2 看看发生什么。
      # （跳出内部和外部循环）。
    fi
  done
  echo
done
echo
exit 0
```

`continue` 命令与 `break` 类似，可选地接受一个参数。普通的 `continue` 结束循环内的当前迭代并开始下次迭代。`continue N` 则终止该循环的所有剩余迭代，并继续上方 N 层循环的下次迭代。

### 示例 10–22. 在更高层循环中继续

```bash
#!/bin/bash
# "continue N" 命令，在第 N 层循环继续。

for outer in I II III IV V # 外部循环
  do
    echo; echo -n "Group $outer:"

    for inner in 1 2 3 4 5 6 7 8 9 10 # 内部循环
    do
      if [ "$inner" -eq 7 ];
      then
        continue 2 # 在第二层继续，即“外部循环”
        # 将上述行替换为简单的 "continue"
        # 查看正常的循环行为。
      fi
      echo -n "$inner "  # 8 9 10 永远不会回显。
    done
done
echo; echo

# 练习：
# 在脚本中为 "continue N" 想出一个有意义的用法。

exit 0
```

# 高级 Bash 脚本指南

```bash
case "$variable" in
  "$condition1"
    command...
    ;;
  "$condition2"
    command...
    ;;
esac
```

![](img/1ce1edffaa36e4f698a85430e71c6d3b_121_0.png)

- 给变量加引号不是强制的，因为不会发生单词拆分。

- 每个行测试行以右括号 `)` 结束。

- 每个条件块以双分号 `;;` 结束。

- 整个 case 块以 `esac` 结束（case 的反向拼写）。

# 示例 10–23. 使用 case

```bash
#!/bin/bash

echo "按下一个键，然后回车。"
read Keypress

case "$Keypress" in
  [a-z]) echo "小写字母";
  [A-Z]) echo "大写字母";
  [0-9]) echo "数字";
  *) echo "标点、空格或其他";
# 允许在 [方括号] 中使用字符范围
esac

# 练习：

# 目前脚本目前是，它接受单个按键，然后退出。
# 修改脚本使其接受连续输入，
# 报告每次按键的输入，并仅在按下 "X" 时才退出。
# 提示：将所有内容封装在 "while" 循环中。
exit 0
```

# 示例 10–24. 使用 case 创建菜单

```bash
#!/bin/bash

# 简单的地址数据库

clear # 清空屏幕。

echo "联系列表*"
echo "      ------ ---"
echo "选择以下人员之一："
echo
```

## 10.4. 测试与分支

# 高级 Bash 脚本指南

```bash
echo "[E]vans, Roland"
echo "[J]ones, Mildred"
echo "[S]mith, Julie"
echo "[Z]ane, Morris"
echo
```

read person

```bash
case "person" in
  # 注意变量加了引号。
  "E" | "e"
    # 接受大写或小写输入。
    echo
    echo "Roland Evans"
    echo "4321 Floppy Dr."
    echo "Hardscrabble, CO 80753"
    echo "(033) 734-3874"
    echo "(303) 734-9892 fax"
    echo "revans@zy.net"
    echo "业务伙伴 & 老朋友"
  # 注意用双分号结束
  # 每个选项。
  "J" | "j"
    echo
    echo "Mildred Jones"
    echo "249 E. 7th St., Apt. 19"
    echo "New York, NY 10009"
    echo "(212) 533-2912"
    echo "(213) 533-9972 fax"
    echo "milliej@loisaida.com"
    echo "女朋友"
    echo "生日: 2月11日"
  # 稍后添加 Smith & Zane 的信息。
  *)
    # 默认选项。
    # 空输入（按回车）也符合这里。
    echo
    echo "数据库中尚。"
esac
```

echo

# 练习：

# 修改脚本使其接受连续输入，

# 而在显示一个地址后就退出。

exit 0

case 的一种非常巧妙的用法是测试命令行参数。

```bash
#! /bin/bash
```

# 高级 Bash 脚本指南

```bash
case "$1" in
")") echo "用法: $0* <filename>"; exit 65; # 无命令行参数，
  # 或者第一个参数为空。
# 注意 $0#*) 是 ${var#pattern} 参数替换。结果是 $0。

-*) FILENAME=$1;
  # 如果作为参数 ($1) 传递的文件名以横杠开头，
  # 将其替换为 /$1
  # 这样后续命令就不会将其解释为选项。

*) FILENAME=$1;
  # 否则，使用 $1。
esac
```

# 示例 10-25. 使用常用替换生成 case 变量
