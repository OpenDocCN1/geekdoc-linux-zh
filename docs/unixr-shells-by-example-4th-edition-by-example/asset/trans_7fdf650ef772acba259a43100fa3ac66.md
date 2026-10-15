

## EXPLANATION (CONTINUED)

- 4 变量 choice 被赋值为列表中的第一个值，之后该值从列表中移出，下一个项目将成为第一个。
- 5 break 语句将循环控制发送到第 9 行之后。
- 6 如果选择了 dan 或 guy，则执行以下 echo 命令，然后执行 break 命令，将控制发送到第 9 行之后。
- 7 内置的 REPLY 变量包含当前列表项的编号：即 1、2 或 3。
- 8 这标志着 case 命令的结束。
- 9 done 标志着 select 循环的结束。

## EXAMPLE 14.44

(The Script)
```
#!/bin/bash
# Scriptname: ttype
# Purpose: set the terminal type
# Author: Andy Adrin

1 COLUMNS=60
2 LINES=1
3 PS3="Please enter the terminal type: "
4 select choice in wyse50 vt200 xterm sun
do
5   case "$REPLY" in
6     1)
        export TERM=$choice
        echo "TERM=$choice"
        break;;      # break out of the select loop
    2 | 3 )
        export TERM=$choice
        echo "TERM=$choice"
        break;;
    4)
        export TERM=$choice
        echo "TERM=$choice"
        break;;
    *)
7       echo -e "$REPLY is not a valid choice. Try again\n" 1>&2
8       REPLY=   # Causes the menu to be redisplayed
        ;;
9 done
```

## EXAMPLE 14.44 (CONTINUED)

(The Command Line)

```
$ ttype
1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type : 4
TERM=sun
```

```
$ ttype
1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type : 3
TERM=xterm
```

```
$ ttype
1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type : 7
7 is not a valid choice. Try again.

1) wyse50   2) vt200   3) xterm   4) sun
Please enter the terminal type: 2
TERM=vt200
```

## EXPLANATION

- 1. COLUMNS 变量被设置为使用 select 循环创建的菜单的终端显示列宽。默认值为 80。
- 2. LINES 变量控制 select 菜单在终端上的垂直显示。默认值为 24 行。当你将 LINES 值改为 1 时，菜单项将在一行上打印，而不是像上一个示例中那样垂直打印。
- 3. PS3 提示符被设置，并在菜单选项下方出现。
- 4. select 循环将打印一个包含四个选择的菜单：wyse50、vt200、xterm 和 sun。变量 choice 将根据保存在 REPLY 变量中的用户响应被赋予这些值之一。如果 REPLY 为 1，则 choice 被赋值为 wyse50；如果 REPLY 为 2，则 choice 被赋值为 vt200；如果 REPLY 为 3，则 choice 被赋值为 xterm；如果 REPLY 为 4，则 choice 被赋值为 sun。
- 5. REPLY 变量计算为用户的输入选择。
- 6. 终端类型被赋值、导出并打印。
- 7. 如果用户未输入 1 到 4 之间的数字，他或她将被再次提示。请注意，菜单不会出现，只会出现 PS3 提示。
- 8. 如果 REPLY 变量被设为空（例如 REPLY=），菜单将被重新显示。
- 9. select 循环的结束。

## 14.6.6 Looping Control Commands

如果发生某些条件，你可能想要跳出循环、返回到循环顶部，或提供一种停止无限循环的方法。bash shell 提供了循环控制命令来处理这些情况。

### The shift Command.

shift 命令将参数列表向左移动指定的次数。没有参数的 shift 命令将参数列表向左移动一次。列表移动后，参数将被永久移除。通常，shift 命令在 while 循环中用于遍历位置参数列表。

### FORMAT

```
shift [n]
```

## EXAMPLE 14.43

(without a loop)
(The Script)
```
#!/bin/bash
# Scriptname: shifter
1 set joe mary tom sam
2 shift
3 echo $*
4 set $(date)
5 echo $*
6 shift 5
7 echo $*
8 shift 2
```

(The Output)
```
3 mary tom sam
5 Thu Mar 18 10:00:12 PST 2004
7 2002
8 shift: shift count must be <= $#
```

## EXPLANATION

- 1 set 命令设置位置参数。$1 被赋值为 joe，$2 被赋值为 mary，$3 被赋值为 tom，$4 被赋值为 sam。$* 代表所有参数。
- 2 shift 命令将位置参数向左移动；joe 被移出。
- 3 shift 后的参数列表被打印。
- 4 set 命令将位置参数重置为 UNIX date 命令的输出。
- 5 新的参数列表被打印。
