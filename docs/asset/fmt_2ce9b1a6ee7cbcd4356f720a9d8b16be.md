
^C ...按下 `Control-C`。

`control C detected`

%

```csh
repeat
```

`repeat` 命令允许你按指定的次数执行单条命令。其语法如图 7.28 所示。这里是 `repeat` 的用法示例：

```csh
% repeat 2 echo hi there ...显示两行。
hi there
hi there
%
```

`repeat expr` 命令
`repeat` 命令评估 `expr`，然后根据结果次数执行 `command`。

图 7.28

`repeat` shell 命令的描述。

```bash
switch (expr)
  case pattern1:
    list
    break
  case pattern2:
  case pattern3:
    list2
    break
  default:
    defaultList
endsw
```

`expr` 是一个求值为字符串的表达式，`pattern1/pattern2/pattern3` 可能包含通配符，而 `list1/list2/defaultList` 是一个或多个命令的列表。shell 评估 `expr` 并从上到下逐个与每个模式比较。当找到第一个匹配模式时，执行其关联的命令列表，然后 shell 跳到匹配的 `endsw`。如果没有找到匹配项且提供了默认命令，则执行 `defaultList`。如果未找到匹配项且不存在默认条件，则执行从匹配的 `endsw` 之后的命令开始继续执行。

图 7.29

`switch` shell 命令的描述。

## switch .. case .. endsw

`switch` 命令支持基于单个表达式的值进行多路分支。图 7.29 显示了 `switch` 结构的通用形式。这里有一个名为 `"menu.csh"` 的脚本示例，它使用了 `switch` 控制结构：

```csh
# echo menu 菜单测试程序
set stop = 0  # 重置循环终止标志
while ($stop == 0)  # 循环直到完成
  cat << ENDOFMENU  # 显示菜单
  1 : 打印日期。
  2, 3: 打印当前工作目录
  4 : 退出
ENDFOMENU
echo
```
# 280 第 7 章 C Shell

```csh
echo -n 'your choice?' ' # 提示
set reply = $< # 读取响应
echo ""
switch ($reply) # 处理响应
case "1":
  date
  breaksw
case "2":
case "3":
  pwd
  breaksw # 设置显示工作目录
case "4":
  set stop = 1 # 设置循环终止标志
  breaksw
default: # 默认
  echo illegal choice # 错误
  breaksw
endsw
```

这里是 `"menu.csh"` 脚本的输出：

```csh
% menu.csh
menu 菜单测试程序
1 : 打印日期。
2, 3 : 打印当前工作目录
4 : 退出
your choice? 1
Sat Feb 14 00:50:26 CST 1998
1 : 打印日期。
2, 3 : 打印当前工作目录
4 : 退出
your choice? 2
/home/glass
1 : 打印日期。
2, 3 : 打印当前工作目录
4 : 退出
your choice? 5
illegal choice
1 : 打印日期。
2, 3 : 打印当前工作目录
4 : 退出
```

## while .. end

内置的 `while` 命令只要指定的表达式为真（非零），就会重复执行命令列表。语法位于

# 示例项目: Junk 281

```bash
while ( expr )
  commandlist
end
```

`while` 命令评估 `expr`，如果为真，则执行 `commandlist` 中的每个命令并重复该过程。如果 `expr` 为假，`while` 循环终止，脚本从 `end` 之后的命令继续执行。`break` 命令导致循环立即结束，`continue` 命令导致循环跳转到下次迭代。

图 7.30

`while` 命令的描述。

图 7.30。这里是一个使用 `while` 控制结构生成乘法表的脚本示例：

```csh
% cat multi.csh               ...列出脚本。
#
set x = 1                               # 设置循环值
while ($stop == 0)  # 循环直到完成
  cat << ENDOFMENU  # 显示菜单
  1 : 打印日期。
  2, 3: 打印当前工作目录
  4 : 退出
ENDFOMENU
echo
```

图 7.26

带有 `else` 子句的 `if` 命令的描述。

`if` 命令的第二种形式支持多路分支。其通用语法如图 7.26 所示。这里是 `if` 第二种形式的一个示例：

```csh
% cat if.csh ...列出脚本。
#
echo -n 'enter a number: ' # 提示用户。
set number = $$ # 读取一行输入。
if ($number < 0) then
  echo negative
else if ($number == 0) then
  echo zero
else
  echo positive
endif
% if.csh ...执行脚本。
enter a number: -1
negative
% _
```

### onintr [- label]

`onintr` 命令允许你指定一个标签，当 shell 接收到 `SIGINT` 信号时跳转到该标签。该信号通常由 `Control-C` 生成，来自（此处不完整）

`onintr` 命令指示 shell 在接收到 `SIGINT` 时跳转到标签。如果使用了该选项，`SIGINT` 将被忽略。如果没有提供任何选项，则恢复 shell 原始的 `SIGINT` 句处理器。

图 7.27

`onintr` shell 命令的描述。

键盘和将在第 13 章中进行更详细的描述。`onintr` 的语法如图 7.27 所示。这里是一个示例：

```csh
% cat onintr.csh ...列出脚本。
#
onintr controlC # 设置 Control-C 陷阱。
while (1)
  echo infinite loop
  sleep 2
end
controlC:
  echo control C detected
% onintr.csh ...执行脚本。
infinite loop
infinite loop
^C ...按下 Control-C。
control C detected
%
```
