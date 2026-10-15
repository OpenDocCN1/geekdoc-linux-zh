

### 解释
- 1 用户被要求输入。如果用户仅按下 Enter，变量名会被设置，但它被设置为 null。
- 2 变量使用双引号，以便如果用户在 name 中输入多个单词，表达式仍会被求值。如果去掉引号且用户输入了名和姓，shell 将会以错误信息退出脚本：表达式语法。空双引号代表空字符串。

## 10.6.5 if/else 语句

if/else 结构是一种双向分支控制结构。如果 if 后面的表达式为真，则其后的语句会被执行；否则，else 后的语句会被执行。endif 与最内层的 if 语句匹配并终止该语句。

### 格式

```
if ( expression ) then
    command
else
    command
endif
```

### 示例 10.14

```
1 if ( $answer =~ [Yy]*) then
2   mail bob < message
3 else
4   mail john < datafile
5 endif
```

### 解释
- 1 该行读作：如果 $answer 的值匹配 Y 或 y 后跟零个或多个字符，则转到第 2 行；否则，转到第 3 行。（* 是一个 shell 元字符。）
- 2 用户 bob 会收到文件 message 的内容。
- 3 如果第 1 行不为真，则执行 else 下的命令。
- 4 用户 john 会收到文件 datafile 的内容。
- 5 endif 块结束 if 块。

## 10.6.6 逻辑表达式

逻辑运算符为 &&、|| 和 !。AND 运算符 && 会先求值 && 左侧的表达式，如果为真，则测试 && 右侧的表达式且也必须为真。如果一个表达式为假，则表达式为假。OR 运算符 || 会求值 || 左侧的表达式；如果为真，则表达式为真；如果为假，则测试 || 运算符右侧的表达式。如果它为真，则表达式为真。如果两个表达式都为假，则表达式为假。NOT 运算符 ! 是一个一元运算符。它求值右侧的表达式，如果该表达式为真，则变为假，如果为假，则变为真。如果一个表达式为假，则表达式为假。

C/TC shell 的 -x 选项（称为回显）允许你在脚本执行时跟踪正在发生的情况。（参见第 15 章“调试 Shell 脚本”，第 967 页。）

### 示例 10.15

（脚本：使用逻辑表达式并检查值）

```
#!/bin/csh -f
# Scriptname: logical
set x = 1
set y = 2
set z = 3
if ( ( "$x" && "$y" ) || ! "$z" ) then
  # Note: grouping and parentheses
echo TRUE
else
echo FALSE
endif
```

（输出）

```
% csh -x logical
set x = 1
set y = 2
set z = 3
if ( ( 1 && 2 ) || ! 3 ) then
echo TRUE
TRUE
else
%
```

### 解释
- 1 正在求值逻辑表达式。第一个表达式用括号括起来（不是必需的，因为 && 的优先级高于 ||）。嵌套时括号不需要空格，但否定运算符 (!) 之后必须有空格。
- 2 如果表达式求值为真，则执行此行。
- 3 csh 程序使用 -x 开关执行。这会打开回显。脚本中的每一行在变量替换后都会回显给你。

## 10.6.7 if 语句和单个命令

如果表达式后面跟随单个命令，则不需要 then 和 endif 关键字。

### 格式

```
if ( expression ) single command
```

### 示例 10.16

```
if ($#argv == 0) exit 1
```

### 解释

表达式被测试。如果命令行参数的数量 $#argv 等于 0，则程序以状态 1 退出。

## 10.6.8 if/else if 语句

if/else if 结构提供了一种多路决策机制。可以测试多个表达式，当其中一个表达式求值为真时，其后的语句块会被执行。如果没有任何表达式为真，则执行 else 块。

### 格式

```
if ( expression ) then
  command
  command
else if ( expression ) then
  command
  command
else
  command
endif
```

### 示例 10.17

