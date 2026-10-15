
Hope you have a nice day, Guy!

Subscript out of range

```
# 解释

- 1. 脚本名称和前三个位置参数将被显示。因为从命令行传入的只有两个位置参数，Guy 和 Quigley，所以 `$1` 变为 `Guy`，`$2` 变为 `Quigley`，而 `$3` 未定义。
- 2. `awk` 命令用单引号引用，这样 `shell` 就不会将 `awk` 的字段号 `$1`、`$2` 和 `$3` 与位置参数混淆。（不要将 `awk` 的字段指示符 `$1`、`$2` 和 `$3` 与 `shell` 的位置参数混淆。）
- 3. `argv` 数组被分配从命令行传入的值。`Guy` 被分配给 `argv[1]` 并且其值被显示。你可以使用 `argv` 数组在脚本中表示命令行参数，也可以使用位置参数。区别在于，如果引用一个没有值的参数，位置参数不会产生错误，而未分配的 `argv` 值会导致脚本以 `Subscript out of range` 错误消息退出。
- 4. `shell` 打印错误消息 `Subscript out of range`，因为 `argv[3]` 没有值。

# 10.6 条件构造和流程控制

在做出决策时，使用 `if`、`if/else`、`if/else if` 和 `switch` 命令。这些命令通过允许基于表达式为真或为假的决策来控制程序的流程。

## 10.6.1 测试表达式

表达式由一组操作数和运算符分隔组成。运算符和优先级分别列在表 10.5 和 10.6 中。要测试一个表达式，表达式会被括号包围。C shell 会计算表达式，结果为零或非零数值。如果结果为非零，则表达式为真；如果结果为零，则表达式为假。

### 表 10.5 比较和逻辑运算符

| Operator | Meaning | Example |
|---|---|---|
| == | Equal to | `$x == $y` |
| != | Not equal to | `$x != $y` |
| > | Greater than | `$x > $y` |
| >= | Greater than or equal to | `$x >= $y` |
| < | Less than | `$x < $y` |
| <= | Less than or equal to | `$x <= $y` |
| =~ | String matches | `$ans =~ [Yy]*` |
| !~ | String does not match | `$ans !~ [Yy]*` |
| ! | Logical NOT | `! $x` |
| \|\| | Logical OR | `$x \|\| $y` |
| && | Logical AND | `$x && $y` |

在用逻辑 AND (`&&`) 评估表达式时，`shell` 从左到右进行评估。如果第一个表达式（`&&` 之前）为假，`shell` 会将整个表达式的结果指定为假，永远不会检查剩余的表达式。围绕逻辑 `&&` 运算符的两个表达式都必须为真，整个表达式才会被评估为真。

```
( 5 && 6 )    Expression is true

( 5 && 0 )    Expression is false

( 0 && 3 && 2 )    Expression is false
```

在用逻辑 OR (`||`) 评估表达式时，如果 `||` 左侧的第一个表达式为真，`shell` 会将整个表达式指定为真，并且永远不会进一步检查。在逻辑 `||` 表达式中，只需要其中一个表达式为真。

```
( 5 || 6 )  Expression is true

( 5 || 0 )  Expression is true

( 0 || 0 )  Expression is false

( 0 || 4 || 2 )  Expression is true
```

逻辑 NOT 是一个一元运算符；也就是说，它评估一个表达式。如果 NOT 运算符右侧的表达式为真，则表达式变为假。如果为假，则表达式变为真。

```
! 5  Expression is false

! 0  Expression is true
```

## 10.6.2 优先级和结合性

像 C 一样，C shell 在测试表达式时使用优先级和结合性规则。如果表达式中混合了不同运算符，例如以下示例，`shell` 会按特定顺序读取运算符：

```
@ x = 5 + 3 * 2

echo $x

11
```

优先级指的是运算符的重要性顺序。结合性指的是当优先级相等时，`shell` 是从左到右还是从右到左读取表达式。2 除算术表达式外（反正 `shell` 脚本中也不太需要），如果优先级相等，结合性顺序是从左到右。你可以通过使用括号来改变顺序。 （参见表 10.6。）

```
@ x = ( 5 + 3 ) * 2

echo $x

16
```

表达式可以是数值、关系或逻辑。数值表达式使用以下算术运算符：

```
+ - * / ++ -- %
```

关系表达式使用产生真（非零）或假（零）结果的运算符：

```
> < >= <= == != 
```

逻辑表达式使用这些也产生真或假的运算符：

```
! && ||
```

2. 在算术表达式中，结合性在优先级相等的情况下是从右到左。

### 表 10.6 运算符优先级

| Operator | Precedence | Meaning |
|---|---|---|
| () | High | Change precedence: group |
| ~ | | Complement |
| ! | | Logical NOT, negation |
| * / % | | Multiply, divide, modulo |
| + - | | Add, subtract |
| << >> | | Bitwise left and right shift |
| > >= < <= | | Relational operators: greater than, less than |
| == != | | Equality: equal to, not equal to |
| =~ !~ | | Pattern matching: matches, does not match |
| & | | Bitwise AND |
| ^ | | Bitwise exclusive OR |
| \| | | Bitwise inclusive OR |
| && | Low | Logical AND |
| \|\| | Low | Logical OR |

最简单的条件形式是 `if` 语句。在 `if` 表达式被测试为真之后，`then` 关键字之后的命令会被执行，直到遇到 `endif`。`endif` 关键字终止该块。`if` 语句可以嵌套，只要每个 `if` 语句都以匹配的 `endif` 终止即可。`endif` 与最近的包含 `if` 配对。

```
if ( expression ) then

command

command

endif
```

# 解释

- 1 用户被要求输入。如果用户仅按下 Enter，变量名会被设置，但它被设置为 null。
- 2 变量使用双引号，以便如果用户在 `name` 中输入多个单词，表达式仍会被求值。如果去掉引号且用户输入了名和姓，`shell` 将会以错误信息退出脚本：表达式语法。空双引号代表空字符串。

## 10.6.5 if/else 语句

`if/else` 结构是一种双向分支控制结构。如果 `if` 后面的表达式为真，则其后的语句会被执行；否则，`else` 后的语句会被执行。`endif` 与最内层的 `if` 语句匹配并终止该语句。

# 格式

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
