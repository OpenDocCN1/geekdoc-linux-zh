

## 解释

+   1 变量 hour 被初始化为 0。
+   2 let 命令 (( )) 测试算术表达式，判断小时是否大于 24。如果小时不大于 24，则进入循环体。until 循环在其后的命令返回非零退出状态时进入。直到条件为真，循环才会继续迭代。
+   3 case 命令评估 hour 变量并测试每个 case 语句是否匹配。
+   4 在控制返回到循环顶部之前，hour 变量会被递增。
+   5 done 命令标记循环体的结束。

## 14.6.5 select 命令和菜单

here 文档是创建菜单的一种简便方法，但 bash 引入了另一种循环机制，称为 select 循环，主要用于创建菜单。数字列出的菜单项会显示到标准错误。PS3 提示符用于提示用户输入；默认情况下 PS3 为 #?。在显示 PS3 提示符后，shell 会等待用户输入。输入应为菜单列表中的其中一个数字。输入会存储在特殊的 shell 变量 REPLY 中。REPLY 变量中的数字与选择列表中括号右侧的字符串相关联。

case 命令与 select 命令一起使用，允许用户从菜单中进行选择，并基于该选择执行命令。LINES 和 COLUMNS 变量可用于确定在终端上显示的菜单项布局。 （这些变量内置于 bash 2.x 版本中，但在更早版本中未内置；如果未定义，可以在 .bash_profile 中定义并导出它们。）输出显示到标准错误，每个项目前面都有一个数字和右括号，PS3 提示符显示在菜单底部。由于 select 命令是循环命令，因此请务必记住使用 break 命令退出循环，或使用 exit 命令退出脚本。

## 格式

```
select var in wordlist
 do
   command(s)
 done
```

## 示例 14.42

（脚本）
#!/bin/bash
# Scriptname: runit

```
1 PS3="Select a program to execute: "
2 select program in 'ls -F' pwd date
3 do
4   $program
5 done
```

（命令行）

```
Select a program to execute: 2
1) ls -F
2) pwd
3) date
/home/ellie
Select a program to execute: 1
1) ls -F
2) pwd
3) date
12abcry abc12 doit+ progs/ xyz
Select a program to execute: 3
1) ls -F
2) pwd
3) date
Sun Mar 12 13:28:25 PST 2004
```

## 解释

+   1 PS3 提示符被赋值为 select 循环显示的菜单下方出现的字符串。此提示符默认为 $# 并发送到标准错误，即屏幕。
+   2 select 循环由一个名为 program 的变量和将在菜单中显示的三个词列表组成：ls -F、pwd 和 date。此列表中的词是 UNIX/Linux 命令，但它们可以是任何词（例如，red、green、yellow 或 cheese、bread、milk、crackers）。如果词中包含空格，则必须加引号（例如，'ls -F'）
+   3 do 关键字开始 select 循环的循环体。
+   4 当用户在菜单中选择数字时，该数字将与括号后数字右侧的词值相等。例如，如果用户选择数字 2，则它与 pwd 相关联，并且 pwd 存储在 program 变量中。$program 求值为可执行命令 pwd；该命令被执行。
+   5 done 关键字标记 select 循环中语句体的结束。控制将返回到循环顶部。此循环将继续执行，直到用户按下 ^C。

## 示例 14.43

（脚本）

```
#!/bin/bash
# Scriptname: goodbye
1 PS3="Please choose one of the three boys : "
2 select choice in tom dan guy
3 do
4   case "$choice" in
      tom)
      echo Tom is a cool dude!
5     break;;        # break out of the select loop
6   dan | guy )
      echo Dan and Guy are both wonderful.
      break;;
      *)
7     echo "$REPLY is not one of your choices" 1>&2
      echo "Try again."
8     ;;
9   esac
done
```

（命令行）

```
$ goodbye
1) tom
2) dan
3) guy
Please choose one of the three boys : 2
Dan and Guy are both wonderful.
$ goodbye
1) tom
2) dan
3) guy
Please choose one of the three boys : 4
4 is not one of your choices
Try again.
Please choose one of the three boys : 1
Tom is a cool dude!
$
```

## 解释

+   1. PS3 提示符将在第 2 行的 select 循环创建的菜单下方打印。
+   2. 进入 select 循环。它会导致其列表中的词以编号菜单的形式显示。
+   3. 循环体从此处开始。

