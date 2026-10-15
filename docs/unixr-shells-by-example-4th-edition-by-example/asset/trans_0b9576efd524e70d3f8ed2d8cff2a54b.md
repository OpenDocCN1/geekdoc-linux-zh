

# 表 2.4 Bash Shell 语法和结构（续）

| 数组（续） | 示例 |
|---|---|
|  | `set apples pears peaches   (positional parameters)`<br>`echo $1 $2 $3`<br><br>`declare -a array_name=(word1 word2 word3 ...)`<br>`declare -a fruit=( apples pears plums )`<br>`echo ${fruit[0]}` |
| 命令替换 | 与 C/TC shell 和 Bourne shell 类似，UNIX/Linux 命令的输出可以通过用反引号括住该命令来赋给变量，或作为字符串中命令的输出使用。Bash shell 还提供了一种新的语法。不是将命令放在反引号之间，而是将其用一对括号括起来，并在前面加上美元符号。<br><br>**示例**<br><br>`variable_name=`command``<br>`variable_name=$( command )`<br>`echo $variable_name`<br><br>`echo "Today is `date`"`<br>`echo "Today is $(date)"` |
| 算术 | Bash shell 支持整数运算。`declare -i` 命令将声明一个整数类型变量。Korn shell 的 `typeset` 命令也可以用于向后兼容。这样声明的变量可以进行整数运算。否则使用 `(( ))`（`let command`）语法进行算术运算。<br><br>**示例**<br><br>`declare -i variable_name      used for bash`<br>`typeset -i variable_name      can be used to be compatible with ksh`<br><br>`(( n=5 + 5 ))`<br>`echo $n` |
| 运算符 | Bash shell 使用内置 test 命令运算符来测试数字和字符串，与 C 语言运算符类似。<br><br>**示例**<br><br>相等：                逻辑：<br>`==`      等于          `&&`      与<br>`!=`      不等于      `||`      或<br>                              `!`       非<br><br>关系：<br>`>`       大于<br>`>=`      大于等于<br>`<`       小于<br>`<=`      小于等于 |

# 表 2.4 Bash Shell 语法和结构（续）

## 条件语句

if 结构后面跟着用括号括起来的表达式。运算符与 C 运算符类似。then 关键字放在右括号之后。if 必须以 endif 结束。新的 [[ ]] 测试命令现在被用来允许在条件表达式中进行模式匹配。旧的 ( ) 测试命令仍然可用，以保持与 Bourne shell 的向后兼容性。case 命令是 if/else 的替代方案。

### 示例

```
The if construct is:
if command
then
  block of statements
fi

if [[ expression ]]
then
  block of statements
fi

if (( numeric expression ))
then
  block of statements
else
  block of statements
fi

The if/else construct is:
if command
then
  block of statements
else
  block of statements
fi

if [[ expression ]]
then
  block of statements
else
  block of statements
fi

if (( numeric expression ))
then
  block of statements
else
  block of statements
fi
```

```
The if/else/else if construct is:
if command
then
  block of statements
elif command
then
  block of statements
else if command
then
  block of statements
else
  block of statements
fi
-----------------------------
if [[ expression ]]
then
  block of statements
elif [[ expression ]]
then
  block of statements
else if [[ expression ]]
then
  block of statements
else
  block of statements
fi
-----------------------------
if (( numeric expression ))
then
  block of statements
elif (( numeric expression ))
then
  block of statements
else if ((numeric expression))
then
  block of statements
else
  block of statements
fi
```

# 表 2.4 Bash Shell 语法和结构（续）

| 条件语句（续） | case 结构是：<br>case variable_name in<br>  pattern1)<br>    statements<br>    ;;<br>  pattern2)<br>    statements<br>    ;;<br>  ...<br>  patternN)<br>    ;;<br>esac<br><br>case "$color" in<br>  blue)<br>    echo $color is blue<br>    ;;<br>  green)<br>    echo $color is green<br>    ;;<br>  red|orange)<br>    echo $color is red or orange<br>    ;;<br>  *) echo "Not a match"<br>    ;;<br>esac |
|---|---|

## 循环

有四种类型的循环：while、until、for 和 select。

while 循环后面跟着用方括号括起来的表达式、do 关键字、一组语句，并以 done 关键字终止。只要表达式为真，do 和 done 之间的语句体就会被执行。复合测试运算符 [[ ]] 是 Bash 的新特性，旧式的测试运算符 [ ] 仍可用于评估条件表达式，以保持与 Bourne shell 的向后兼容性。

until 循环与 while 循环类似，只是只要表达式为假，循环体就会被执行。

for 循环用于遍历一组单词，处理一个单词然后将其移出，以处理下一个单词。当所有单词都从列表中移出时，它结束。for 循环后面跟着变量名、in 关键字、单词列表，然后是一组语句，并以 done 关键字终止。

select 循环用于提供提示和编号项目的菜单供用户选择。输入将存储在特殊的内置 REPLY 变量中。select 循环通常与 case 命令一起使用。

循环控制命令是 break 和 continue。break 命令允许控制在到达循环末尾之前退出循环，而 continue 命令允许控制在到达末尾之前返回到循环表达式。

