

### 格式

```
case variable in
value1)
command(s)
;;
value2)
command(s)
;;
*)
command(s)
;;
esac
```

### 示例 8.23

(The Script)

```
#!/bin/sh
# Scriptname: colors
1 echo -n "Which color do you like?"
2 read color
3 case "$color" in
4 [Bb]l??)
 echo I feel $color
 echo The sky is $color
5 ;;
6 [Gg]ree*)
 echo $color is for trees
 echo $color is for seasick;;
7 red | orange)   # The vertical bar means "OR"
 echo $color is very warm;;
8 *)
9 echo No such color as $color;;
10 esac
11 echo "Out of case"
```

### 解释

1. 用户被要求输入。输入被赋给变量 color。
2. case 命令计算表达式 $color。
3. 如果颜色以 b 或 B 开头，后跟字母 l 和任意两个字符，则 case 表达式匹配第一个值。值以单个右括号终止。通配符是用于文件名扩展的 shell 元字符。
4. 如果第 3 行的值与 case 表达式匹配，则执行语句。
5. 在此命令块的最后一个命令之后需要双分号。到达分号时控制跳转到第 10 行。如果分号单独成行，脚本更易于调试。
6. 如果 case 表达式匹配 G 或 g，后跟字母 ree 并以零个或多个任意其他字符结尾，则执行 echo 命令。双分号终止语句块并使控制跳转到第 10 行。
7. 垂直线用作 OR 条件运算符。如果 case 表达式匹配 red 或 orange，则执行 echo 命令。
8. 这是默认值。如果上述值均不匹配 case 表达式，则执行 *) 后的命令。
9. esac 语句终止 case 命令。
10. 在匹配其中一个 case 值后，执行继续到此处。

### 8.5.10 使用 here 文档和 case 命令创建菜单

here 文档和 case 命令经常一起使用。here 文档用于创建将显示到屏幕上的选项菜单。用户将被要求选择其中一个菜单项，而 case 命令将根据一组选择进行测试以执行适当的命令。

### 示例 8.24

```
(The .profile file)
echo "Select a terminal type:"
1 cat << ENDIT
    1) vt120
    2) wyse50
    3) sun
2 ENDIT
3 read choice
4 case "$choice" in
5 1) TERM=vt120
    export TERM
    ;;
2) TERM=wyse50
    export TERM
    ;;
6 3) TERM=sun
    export TERM
    ;;
7 esac
8 echo "TERM is $TERM."
```

(The Output)

```
$ .profile
Select a terminal type:
1) vt120
2) wyse50
3) sun
3
TERM is sun.
```

### 解释

1. 如果将此脚本段放入 .profile 中，登录时您将有机会选择正确的终端类型。here 文档用于显示选项菜单。
2. 用户定义的 ENDIT 终止符标记 here 文档的结束。
3. read 命令将用户输入存储在变量 choice 中。
4. case 命令计算变量 choice 并将该值与右括号前的其中一个值进行比较：1、2 或 3。
5. 第一个测试的值是 1。如果匹配，则终端设置为 vt120。TERM 变量被导出，以便子 shell 继承它。
6. 不需要默认值。TERM 变量通常在登录时在 /etc/profile 中分配。如果选择为 3，则终端设置为 sun。
7. esac 终止 case 命令。
8. 在 case 命令完成后，执行此行。

## 8.6 循环命令

循环命令用于执行命令或一组命令固定次数或直到满足特定条件。Bourne shell 有三种类型的循环：for、while 和 until。

### 8.6.1 for 命令

for 循环命令用于在项目列表上有限次数地执行命令。例如，您可能会使用此循环在文件列表或用户名列表上执行相同的命令。for 命令后面跟一个用户定义的变量、关键字 in 和一个单词列表。循环第一次时，单词列表中的第一个单词被赋给变量，然后从列表中移出。一旦单词被赋给变量，就会进入循环体，命令在 do 之间

