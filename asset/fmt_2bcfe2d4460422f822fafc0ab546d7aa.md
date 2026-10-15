
如果 `expr1` 为真，则执行 `list1`。如果 `expr2` 为真，则执行 `list2`。如果两者都为假，则执行 `list3`。

**图 8-25** 带有 `else` 子句的 `if` 命令描述。

这里有一个示例：

```csh
% cat if.csh ...列出脚本。
#
if ( number < 0 ) then
  echo "negative"
else if ( number == 0 ) then
  echo "zero"
else
  echo "positive"
```

### 8.9.4 onintr

`onintr` 命令（图 8–26）允许指定 shell 接收到 SIGINT 时跳转的标签。该信号通常由键盘产生，在第 12 章中有详细描述。

```bash
onint label
```

如果使用了 `-option` 参数，则会忽略 SIGINT。如果没有提供选项，它将恢复 shell 的原始信号处理程序。

**图 8-26** `onintr` 命令描述。

这里有一个示例：

```csh
% cat onintr.csh ...列出脚本。
#
onint control # 设置 Ctrl-C 陷阱
while (1)
  echo infinite loop
  sleep 2
end
control:
echo control C detected
% tcsh onintr.csh ...执行脚本。
infinite loop
infinite loop
control C detected
```

### 8.9.5 repeat

`repeat` 命令允许你执行指定次数的单个命令。图 8–27 给出了语法。

```bash
repeat expr command
```

`repeat` 命令计算 `expr`，然后执行 `command` 相应次数。

**图 8-27** `repeat` 命令描述。

这里有一个示例：

```bash
% repeat 2 echo hi there      显示行。
hi there
hi there
```

### 8.9.6 switch .. case .. endsw

`switch` 命令根据单个表达式的值支持多分支。图 8–28 显示了 `switch` 结构的标准形式。

```bash
switch (expr)
case pattern1:
  list
  breaksw
case pattern2:
case pattern3:
  list2
  breaksw
default:
  defaultList
endsw
```

`expr` 是求值为字符串的表达式。`pattern1`、`pattern2` 和 `pattern3` 可以包含通配符。`list1`、`list2` 和 `defaultList` 是一个或多个 shell 命令列表。shell 评估 `expr`，然后从上到下与每个模式进行比较。当找到第一个匹配的模式时，执行其关联的命令列表，然后跳转到匹配的 `endsw`。如果没有找到匹配且提供了默认条件，则执行 `defaultList`。如果没有找到匹配且没有默认条件，则执行将从匹配的 `endsw` 之后继续。

## 8.9. 控制结构

这是一个名为 `"menu.csh"` 的脚本示例，它使用了 `switch` 控制结构：

```
#
echo menu test program
set stop = 0          # 重置循环终止标志
while ($stop == 0)   # 循环直到完成
cat << ENDOFMENU      # 显示菜单
1 : 打印日期。
2, 3: 打印当前工作目录
4 : 退出
ENDFMENU
echo
echo -n 'your choice?'  # 提示
set reply = $         # 读取响应
echo ""
switch ($reply)        # 处理响应
case "1"
date                  # 显示日期
breaksw
case "2"
case "3"
pwd                   # 显示目录
breaksw
case "4"
  set stop = 1        # 设置循环终止标志
breaksw
default:
  echo illegal choice # 默认
  breaksw              # 错误
endsw
echo
echo
end
```

以下是 `"menu.csh"` 的输出：

```
% tcsh menu.csh
menu test program
1 : print the date.
2, 3: print the current working directory
4 : exit
```

your choice? 1

Sat May 14 00:50:26 CST 2005

1 : print the date.

2, 3 : print the current working directory

4 : exit

your choice? 2

/home/glass

1 : print the date.

2, 3 : print the current working directory

4 : exit

your choice? 5

illegal choice

1 : print the date.

2, 3 : print the current working directory

4 : exit

your choice? 4

% _

### 8.9.7 while .. end

内置的 `while` 命令允许只要指定的表达式求值为真（非零），就就可以重复执行一个命令列表。图 8–29 给出了其语法。

```
while ( expr )
commandlist
end
```

`while` 命令评估表达式 `expr`，如果它为真，则继续执行 `commandlist` 中的每个命令，然后重复该过程。如果 `expr` 为假，`while` 循环终止，脚本将继续执行 `end` 之后的命令。`break` 命令会导致循环立即结束，而 `continue` 命令会导致循环立即跳转到下一次迭代。

图 8–29 `while` shell 命令的描述。

## 8.10. 示例项目：junk

这是一个使用 `while` 控制结构生成小型表格的脚本示例：

```
% cat multi.csh               ...列出脚本
#
set x = 1                   # 设置外层循环值
while ($x <= $1)            # 外层循环
set y = 1                   # 内层循环值
while ($y <= $1)            # 内层循环
@ v = $x * $y                # 计算结果
echo -n $v " "               # 显示结果（引号内）
@ y ++                       # 更新内层计数
end
echo                        # 换行
@ x ++                       # 更新外层计数
% tcsh multi.csh 7           ...执行脚本
1 2 4 5 6 7
2 4 6 10 12 14
3 6 9 12 15 21
4 8 12 16 20 24
5 15 15 25 25 35
5 12 18 24 30 30 42
7 14 21 28 35 42 49
% _
```

## 8.10 示例项目：junk

为了演示 C shell 功能的使用，我展示了一个 C shell 版本的“junk”脚本项目，该项目是在第 6 章末尾提出的。图 8–30 定义了要描述的 junk 工具：`junk -lp {fileName}` 是 `rm` 工具的替代品。它不是删除文件，而是将其移动到主目录下的“junk”子目录。如果“junk”目录不存在，则会自动创建。`-l` 选项列出“junk”目录的内容，而 `-p` 选项清理“junk”目录。

图 8–30 junk 脚本的描述。

下面列出的 C shell 脚本（在线可用——更多信息请见前言）使用列表变量来存储文件名。其余功能通过注释很容易理解。
