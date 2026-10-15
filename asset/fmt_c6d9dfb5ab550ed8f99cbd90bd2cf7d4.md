
```
% csh -x -v debugOptions.scr
set x = 5
set x = 5
y = $x + 2
y = 5 + 2

if ( $y == 10 ) then
if ( 7 == 10 ) then

echo \$y contains $y not 10
echo $y contains 7 not 10
$y contains 7 not 10
endif
endif

while ( $x != 0 )
while ( 5 != 0 )
echo Counting down: \$x is $x
echo Counting down: $x is 5
Counting down: $x is 5
@ x = $x - 1
@ x = 5 - 1
end

while ( $x != 0 )
while ( 4 != 0 )
echo Counting down: \$x is $x
echo Counting down: $x is 4
Counting down: $x is 4
@ x = $x - 1
@ x = 4 - 1
end

while ( $x != 0 )
while ( 3 != 0 )
echo Counting down: \$x is $x
echo Counting down: $x is 3
Counting down: $x is 3
```

# 第 17 章 • SHELL 编程

脚本 17.31 详细 `$x` `xtrace` 选项结合——续上

```
@ x = $x - 1
@ x = 3 - 1
end
while ( $x != 0 )
while ( 2 != 0 )
echo Counting down: \$x is $x
echo Counting down: $x is 2
Counting down: $x is 2
@ x = $x - 1
@ x = 2 - 1
end
while ( $x != 0 )
while ( 1 != 0 )
echo Counting down: \$x is $x
echo Counting down: $x is 1
Counting down: $x is 1
@ x = $x - 1
@ x = 1 - 1
end
while ( $x != 0 )
while ( 0 != 0 )
```

脚本 17.31 分析：再次，脚本语句是黑色的，脚本输出是彩色的。对于每条语句，首先以代码形式显示，然后用值替换变量名后重复显示。

# 17.9 脚本示例

在本节中，我们将演示一个完整的脚本。选择该应用程序是为了演示我们在本章中学到的某些技术。它起始于一组我们建议在生产脚本中使用的文档。（在整个章节开发的脚本中，我们一直在使用它的缩写形式。）此部分文档包含了作者姓名、脚本的摘要（类似于 UNIX 手册的摘要）、代码方法的描述以及退出值的解释。当脚本被修改时，我们也建议你在原始描述之后添加修改的日期和描述。

# 复制

在脚本 17.32 中，我们模拟了 `copy` 命令。我们首先验证参数数量是否正确，然后验证输入文件是否存在且输出文件不存在。修改脚本并询问用户是否覆盖输出文件将是一个好主意。我们将此更改留作章节末的练习。在确保一切无误后，我们简单地 `cat` 输入文件并将其重定向到输出文件。

# 17.32 脚本文件

```
| 1 | #/bin/ksh |
| 2 | #NAME:newCopy.scr |
| 3 | #TASK: 将文件复制到另一个 |
| 4 | #AUTHOR: |
| 5 | #DATE WRITTEN: |
| 6 | #SYNOPSIS: newCopy.scr file1 file2 |
| 7 | #DESCRIPTION: 使用 cat 命令复制文件 |
| 8 | #EXIT VALUE |
| 9 | 0 如果成功 |
| 10 | #1 如果参数错误 |
| 11 | #2 如果源文件不存在 |
| 12 | #3 如果目标文件已存在 |
```

```
if [ $argv[1] != 2 ]; then
    echo "Requires two file"
    echo "Usage: $0 from_file_to_file"
    exit 1
fi

if [ ! -f $argv[1] ]; then
    echo "The first file cannot be read"
    exit 2
fi

if [ -f $argv[2] ]; then
    echo "The second file already exists"
    exit 3
fi

cat $argv[1] > $argv[2]

%newCopy.scr
Requires file arguments
Usage: newCopy.scr from_file_to_file
% echo $status
1
%newCopy.scr file.bak
The first file cannot be read
% echo $status
2
%newCopy.scr file.bak
% echo $status
0

cat file.bak
****************
**
这是文件
**
****************
%newCopy.scr file.bak
```

17.32 脚本文件——续

第二个文件已存在

% echo $status

17.32 分析：在研究脚本并在查看测试结果之前，为每个需要测试的情况写下注释。不要忘记查找错误组合。在脚本 17.32 结束将你的列表与测试结果对比。

# 17.10 关键术语

- 参数 (argument)

- 验证 (validation)

- `break`

- C shell (C shell)

- `case` 命令 (`case` command)

- 注释 (comment)

- `continue` 语句 (`continue` statement)

- 调试 (debugging)

- `else`

- 结束 (end)

- `if`

- 可执行的脚本 (executable script)

- `exit` 命令 (`exit` command)

- 表达式 (expression)

- 文件表达式 (file expression)

- 文件运算符 (file operator)

- 参数 (parameter)

- 位置参数语句 (positional statement)

- `if-then-else` 语句 (`if-then-else` statement)

- 关系表达式 (relational expression)

- 解释器 (interpreter)

- 关系运算符 (relational operator)

- 解释器行 (interpreter designator line)

- 列表控制循环 (list-controlled loop)

- 重复 (repetition)

- 重复 (repetition)

- `set` 命令 (`set` command)

- shell 脚本 (shell script)

- 逻辑运算符 (logical operator)

- `shift` 命令 (`shift` command)

- 数学表达式 (mathematical expression)

- 特殊参数 (special parameter)

- 数学运算符 (mathematical operator)

- 特殊变量 (special variables)

- `switch` 选择 (`switch`-way selection)

- 嵌套 `if-then-else` (nested `if-then-else`)

- `then`

- 空命令 (null command)

- 双向选择 (two-way selection)

- 操作数 (operand)

- `while` 语句 (`while` statement)

- 运算符 (operator)

# 17.11 提示

1. 解释器行（例如 `#!/bin/csh`）必须是脚本的第一行。

2. 在执行之前使用 `chmod` 命令使脚本变为可执行。

3. C shell 包含九个位置参数。

4. 使用 `@` 命令计算数学表达式。

5. `@` 命令仅用于整数值。

6. `@` 命令要求的参数必须与其他及命令之间保持一个空格。

7. 除法 (`/`) 和取模 (`%`) 运算符之间存在差异。除法计算商数；取模计算余数。

8. 关系运算符对于整数和字符串是不同的。

9. 字符串只有两个关系运算符：等于 (`==`) 和不等于 (`!`)。其他关系运算符（大于、小于）必须在脚本中模拟。

10. 有两个关系运算符 `~` 和 `!`，用于判断字符串中是否匹配模式。

11. `if-then-else` 的 `else` 子句可以省略，但 `then` 子句不能。

12. 需要 `break` 来终止 `switch` 语句的每个部分。

13. `while` 循环需要一个表达式。

14. `foreach` 循环的测试表达式需要列表。
