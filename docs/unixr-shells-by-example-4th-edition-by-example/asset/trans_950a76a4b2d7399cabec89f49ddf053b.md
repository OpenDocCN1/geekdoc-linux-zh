

## 示例 14.31

（来自 .bash_profile 文件）

```
echo "Select a terminal type: "
1 cat << ENDIT
1) unix
2) xterm
3) sun
2 ENDIT
3 read choice
4 case "$choice" in
5 1) TERM=unix
export TERM
;;
2) TERM=xterm
export TERM
;;
6 3) TERM=sun
export TERM
;;
7 esac
8 echo "TERM is $TERM."
```

（命令行和输出）

```
5 .bash_profile
Select a terminal type:
1) unix
2) xterm
3) sun
2      <-- User input
TERM is xterm.
```

## 解释

+   1 如果将这段脚本放入 .bash_profile 中，登录时你将有机会选择合适的终端类型。这里文档用于显示选项菜单。
+   2 用户定义的 ENDIT 终止符标记这里文档的结束。
+   3 read 命令将用户输入存储在变量 TERM 中。
+   4 case 命令评估变量 TERM 并将该值与右括号前的其中一个值进行比较：1、2 或 3。
+   5 第一个被测试的值是 1。如果匹配，终端将被设置为 unix。TERM 变量被导出，以便子 shell 可以继承它。
+   6 不需要默认值。TERM 变量通常在登录时在 /etc/profile 中分配。如果选择为 3，则终端将被设置为 sun。
+   7 esac 终止 case 命令。
+   8 case 命令完成后，此行被执行。

## 14.6 循环命令

循环命令用于执行命令或一组命令固定次数或直到满足特定条件。bash shell 有三种类型的循环：for、while 和 until。

### 14.6.1 for 命令

for 循环命令用于对一组项目执行命令有限次数。例如，你可能会使用此循环对一组文件或用户名执行相同的命令。for 命令后面跟着用户定义的变量、关键字 in 和一个词列表。循环第一次执行时，词列表中的第一个词被分配给变量，然后从列表中移出。一旦词被分配给变量，就会进入循环体，并在 do 和 done 关键字之间的命令被执行。循环下一次执行时，第二个词被分配给变量，以此类推。循环体从 do 关键字开始，到 done 关键字结束。当列表中的所有词都被移出后，循环结束，程序控制继续在 done 关键字之后。

## 格式

```
for variable in word_list
 do
   command(s)
 done
```

## 示例 14.32

```
（脚本）
#!/bin/bash
# Scriptname: forloop
1  for pal in Tom Dick Harry Joe
2  do
3      echo "Hi $pal"
4  done
5  echo "Out of loop"

（输出）
Hi Tom
Hi Dick
Hi Harry
Hi Joe
Out of loop
```

## 解释

+   1 此 for 循环将遍历名字列表 Tom、Dick、Harry 和 Joe，将每个名字从左移出并将其值分配给用户定义的变量 pal，使用后即分配。一旦所有词都被移出且词列表为空，循环结束，执行从 done 关键字之后开始。循环第一次执行时，变量 pal 将被分配单词 Tom。第二次循环时，pal 将被分配 Dick，下一次 pal 将被分配 Harry，最后一次 pal 将被分配 Joe。
+   2 在词列表之后需要 do 关键字。如果它与同一行使用，列表必须以分号终止。例如：for pal in Tom Dick Harry Joe; do
+   3 这是循环体。Tom 被分配给变量 pal 后，循环体中的命令（即 do 和 done 关键字之间的所有命令）将被执行。
+   4 done 关键字结束循环。一旦列表中最后一个词（Joe）被分配并移出，循环退出，执行从第 2 行开始。
+   5 循环退出时控制在此恢复。

## 示例 14.33

（命令行）

```
1 $ cat mylist
tom
patty
ann
jake
```

（脚本）

```
#!/bin/bash
# Scriptname: mailer
2 for person in $(cat mylist)  # `cat mylist` command substitution the alternate way
do
3   mail $person < letter
  echo $person was sent a letter.
4 done
5 echo "The letter has been sent."
```

## 解释

+   1 显示名为 mylist 的文件的内容。
+   2 执行命令替换，mylist 的内容成为词列表。循环第一次执行时，tom 被分配给变量 person，然后被移出以被 patty 替换，依此类推。
+   3 在循环体中，每个用户都会收到一份名为 letter 的文件副本。

