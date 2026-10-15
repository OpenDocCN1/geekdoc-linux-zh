

## 示例 12.39（续）

```
1 COLUMNS=60
2 LINES=1
3 PS3="Please enter the terminal type: "
4 select choice in wyse50 vt200 vt100 sun
   do
5   case $REPLY in
   1)
6     export TERM=$choice
     print "TERM=$choice"
     break;
          # break out of the select loop
   2 | 3 )
     export TERM=$choice
     print "TERM=$choice"
     break;
   4)
     export TERM=$choice
     print "TERM=$choice"
     break;
   *)
7     print "$REPLY is not a valid choice. Try again" 1>&2
     ;;
8 done
```
（命令行）
```
$ ttype
1) wyse50  2) vt200  3) vt100  4) sun
Please enter the terminal type : 4
TERM=sun

$ ttype
1) wyse50  2) vt200  3) vt100  4) sun
Please enter the terminal type : 3
TERM=vt100

$ ttype
1) wyse50  2) vt200  3) vt100  4) sun
Please enter the terminal type : 7
7 is not a valid choice. Try again.
Please enter the terminal type: 2
TERM=vt200
```

## 解释

- 1 COLUMNS 变量被设置为终端显示的宽度，以列为单位，用于 select 循环创建的菜单。默认值为 80。
- 2 LINES 变量控制 select 菜单在终端上的垂直显示。默认值为 24 行。通过将 LINES 值改为 1，菜单项将在一行上打印，而不是像上一个示例中那样垂直打印。
- 3 PS3 提示符被设置，并在菜单选项下方出现。
- 4 select 循环将打印一个包含四个选择的菜单：wyse50、vt200、vt100 和 sun。变量 choice 将根据保存在 REPLY 变量中的用户响应被赋值为这些值之一。如果 REPLY 为 1，则 choice 被赋值为 wyse50；如果 REPLY 为 2，则 choice 被赋值为 vt200；如果 REPLY 为 3，则 choice 被赋值为 vt100；如果 REPLY 为 4，则 choice 被赋值为 sun。
- 5 REPLY 变量计算为用户的输入选择。
- 6 终端类型被赋值、导出并打印。
- 7 如果用户未输入 1 到 4 之间的数字，他或她将被再次提示。请注意，菜单不会出现，只会出现 PS3 提示符。要使菜单重新出现，请将 REPLY 变量设为空。在第 8 行上方输入：REPLY =
- 8 select 循环的结束。

### 12.6.6 循环控制命令

如果发生某些条件，您可能想要跳出循环、返回到循环顶部，或提供一种停止无限循环的方法。Korn shell 提供了循环控制命令来控制循环。

shift 命令。shift 命令将参数列表向左移动指定的次数。不带参数的 shift 命令将参数列表向左移动一次。列表移动后，参数将被永久移除。shift 命令通常在 while 循环中使用，用于遍历位置参数列表。

# 格式

```
shift [n]
```

## 示例 12.40

```
(without a loop)
(The Script)
#!/bin/ksh
# Scriptname: doit
1 set joe mary tom sam
2 shift
```

## 示例 12.40（续）

```
3 print $5
4 set $(date)
5 print $*
6 shift 5
7 print $*
8 shift 2
```
（输出）

```
$ doit0
3 mary tom sam
5 Sun Sep 9 10:00:12 PDT 2004
7 2004
8 ksh: shift: bad number
```

## 解释

- 1 set 命令设置位置参数。$1 被赋值为 joe，$2 被赋值为 mary，$3 被赋值为 tom，$4 被赋值为 sam。
- 2 shift 命令将位置参数向左移动；joe 被移出。
- 3 在 shift 之后打印参数列表。$* 表示所有参数。
- 4 set 命令将位置参数重置为 UNIX date 命令的输出。
- 5 打印新的参数列表。
- 6 这次列表向左移动五次。
- 7 打印新的参数列表。
- 8 通过尝试移动的次数超过参数数量，shell 会向标准错误发送一条消息。

## 示例 12.41

（带循环）

（脚本）

```
#!/bin/ksh
# Usage: doit [args]
1 while (( $# > 0 ))
do
2     print $*
3     shift
4 done
```

## 示例 12.41（续）

```
(The Command Line)
$ doit a b c d e
 a b c d e
 b c d e
 c d e
 d e
 e
```

## 解释

- 1. while 命令测试数值表达式。如果位置参数的数量（$#）大于 0，则进入循环体。位置参数来自命令行作为参数。有五个。
- 2. 打印所有位置参数。
- 3. 参数列表向左移动一次。
- 4. 循环体在此结束；控制返回到循环顶部。参数列表减少了一个。第一次移动后，$# 为四。当 $# 减少到 0 时，循环结束。

break 命令。内置的 break 命令用于强制立即退出循环，但不退出程序。 （要离开程序，使用 exit 命令。）执行 break 命令后，控制从 done 关键字之后开始。break 命令导致退出最内层的循环，因此如果您有嵌套循环，break 命令接受一个数字作为参数，允许您退出任意数量的外层循环。break 对于退出无限循环很有用。

# 格式

```
break [n]
```

## 示例 12.42

```
1  while true; do
2    read answer? Are you ready to move on\?
3    if [[ $answer = [Yy]* ]]; then
4      break
    else
      ....commands...
    fi
5  done
6  print "Here we are"
```

