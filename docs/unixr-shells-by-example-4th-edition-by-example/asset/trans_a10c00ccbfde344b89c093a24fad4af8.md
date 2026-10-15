

# 示例 12.28

（.profile 文件）

```
print "Select a terminal type."
1 cat << EOF
    1) vt120
    2) wyse50
    3) ansi
    4) sun
2 EOF
3 read TERM
4 case "$TERM" in
1) export TERM=vt120
    ;;
2) export TERM=wyse50
    ;;
3) export TERM=ansi
    ;;
*) export TERM=sun
    ;;
5 esac
print "TERM is $TERM"
```

## 说明

- 1. 此处文档（here document）用于显示一个选项菜单。
- 2. EOF 是用户自定义的终止符。此处文档的输入到此为止。
- 3. read 命令等待用户输入，并将其赋给 TERM 变量。
- 4. case 命令对变量 TERM 求值，并将其与列表中的某个数字进行匹配。如果找到匹配项，就设置终端类型。
- 5. case 命令以 esac 结束。

## 12.6 循环命令

循环命令用于按指定次数执行一条或一组命令，或者一直执行到满足某个条件为止。Korn shell 有四种循环类型：for、while、until 和 select。

### 12.6.1 for 命令

for 循环命令用于对一组参数中的每个成员执行命令。你可以用该循环对文件列表或用户名列表执行相同的命令。for 命令后面跟着一个用户自定义变量、关键字 in 和一个单词列表。第一次进入循环时，将单词列表中的第一个单词赋给该变量，然后将其移出列表。下一次进入循环时，将第二个单词赋给该变量，依此类推。循环体从 do 关键字开始，到 done 关键字结束。当列表中的所有单词都被移出后，循环结束，程序控制流从 done 关键字之后继续执行。

## 格式

```
for variable in wordlist
do
    command(s)
done
```

# 示例 12.29

（脚本）

```
1  for pal in Tom Dick Harry Joe
2  do
3      print "Hi $pal"
4  done
5  print "Out of loop"
```

（输出）

```
Hi Tom
Hi Dick
Hi Harry
Hi Joe
Out of loop
```

## 说明

- 1 这个 for 循环会遍历名字列表 Tom、Dick、Harry 和 Joe，在每次将名字赋给变量 pal 后将其移出（左移）。当所有单词都被移出且单词列表为空时，循环结束，并从 done 关键字之后开始执行。for 命令后面的单词 pal 是一个变量，每次循环迭代时，它都会被赋值为 in 关键字之后的值中的一个。第一次进入循环时，变量 pal 被赋值为 Tom；第二次进入循环时，pal 被赋值为 Dick；下一次被赋值为 Harry；最后一次被赋值为 Joe。
- 2 在单词列表之后必须使用 do 关键字。如果 do 与列表在同一行，则列表必须以分号结束。例如：
  for pal in Tom Dick Harry Joe; do
- 3 这是循环体。将 Tom 赋给变量 pal 之后，执行循环体中的命令，即 do 与 done 关键字之间的所有命令。
- 4 done 关键字结束循环。如果第 1 行的单词列表中没有剩余待处理的单词，循环退出，并从第 5 行开始执行。
- 5 当循环终止时，执行该行。

# 示例 12.30

```
(The Command Line)
1 $ cat mylist
tom
patty
ann
jake

(The Script)
2 for person in $(< mylist)    #same as for person in `cat mylist`
do
3   mail $person < letter
  print "The letter was sent a letter."
4 done
5 print "The letter has been sent."
```

## 说明

- 1. 显示文件 mylist 的内容。
- 2. 执行命令替换，mylist 的内容成为单词列表。第一次进入循环时，将 tom 赋给变量 person，然后将其移出，之后替换为 patty，依此类推。
- 3. 在循环体中，向每个用户发送名为 letter 的文件的副本。
- 4. done 关键字标志着本次循环迭代的结束。
- 5. 当列表中的所有用户都已发送邮件后，循环退出，并执行这一行。

# 示例 12.31

```
1 for file in *.c
2 do
  if [[ -f $file ]]; then
    cc $file -o ${file%.c}
  fi
done
```

## 说明

- 1. 单词列表由当前工作目录中所有以 .c 为扩展名（C 源文件）的文件组成。每次循环迭代时，每个文件名将依次赋给变量 file。
- 2. 进入循环体后，将测试该文件以确保它存在且是真实文件。如果是，就编译它。${file%.c} 会展开为去掉扩展名后的文件名。

