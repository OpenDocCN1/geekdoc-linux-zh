
## 配置 X 第 11 章

239

```
lucidasans-8
lucidans-bold-10
```

13. `cat /etc/passwd|sort|tail -5|cut -d - -f 1,3 | last-users-system.txt`

14. 在此答案中，请将 `join` 替换为你的用户名。如果你的用户名是 `cat` `init`，它将无法正常工作：它们会尝试杀死你所有的进程。注意，可能会出现关于无法杀死某个不存在的进程的报错；这里的 `process` 是指你正在运行的用于查找名为 `cat` 进程的 `grep` 命令。最后，你可能需要输入命令 `fg` 让 `cat` 意识到它已经被杀死。为了一个练习题，竟然有这么多复杂性；你能相信吗？

对于 `SYSV` 系统的 `ps`：`ps -ef | grep jon | grep cat | awk '{ print $2}' xargs kill`

对于 `BSD` 版本的 `ps`：`ps aux | grep jon | grep cat|awk '{ print $2}' xargs kill`

# 第 5 章习题答案

- 1. `:set number`
- 2. `:set wrapmargin=12`
- 3. `:map <F7> :q!`
- 4. `:map|<F7> :wq!` 若要输入冒号前的转义字符，请按 `Control-V` 然后按 `Esc`。
- 5. `:map <F8> 1G|Gsort^M` 若要输入 `Control-M`，请按 `Control-V` 然后按 `Enter`。
- 6. `:map <F9> 1G|Gsort^M|uniq^M`
- 7. `grep '$'`
- 8. `grep '?'`
- 9. `grep '[^?$]'` 在任何正则表达式引擎中都应该有效。其他的正则效果等等。
- 10. `grep '[kitten puppy]'`
- 11. `grep '[ \][t]he'` 在看似方括号内同时存在制表符和空格。
- 12. `sed '/s/yes/no/gi'`
- 13. `sed '/s/(Yes).*\*/(No)\/2\1/gi'`
- 14. `sed '/s/(No .*/No/Yes/'` 除了斜杠以外的任何字符都可以替换 `#`。
- 16. `sed '/s/[0-9]\{3\}/know/'` 其他表达式也可以实现相同的效果。
- 17. `:s/whale/monster/`
- 18. `:s/whale/Jonah/g`
- 19. `:g/whale/s//krill/g` or `:1,$s/whale/krill/g`
- 20. `:g/start$/s//finish/gi`

# 第 6 章习题答案

- 1. 答案是 `history | wc -1` 返回的值。
- 2. `echo !!`
- 3. `echo !!-4`
- 4. `echo "?cat?"`
- 5. `"cat@dog"`
- 6.

```
[ jon@razorback $ rev
Control-Z
[ jon@razorback $ Enter
[1]+ Stopped rev
[ jon@razorback $ tac
Control-Z
[ jon@razorback $ Enter
[2]+ Stopped tac
[ jon@razorback $ jobs
[1]- Stopped rev
[2]+ Stopped tac
```

- 7. `bg %1` 本部分的所有答案均假设你在回答这些问题之前没有其他挂起的的作业。
- 8. `kill -STOP %1` or `kill -19 %1`
- 9. `kill % %2`
- 10.

```
[ jon@razorback $ cat &
n[1] 1414
[ jon@razorback $ fg
Control-C
cat
[ jon@razorback $ ]
```

# 第 7 章习题答案

- 1. `EXTRPATH=$SPATH`
- 2.

```
[jon@frogbog jon]$ mkdir bin
[jon@frogbog jon]$ PATH=$SPATH:HOME$SPATH
```

- 3.

```
[jon@frogbog jon]$ THIRDARM=$SPATH
[jon@frogbog jon]$ export THIRDARM
```

- 4. `PATH=$EXTRAPATH`
- 5.

```
[jon@frogbog jon]$ unset THIRDARM
[jon@frogbog jon]$ export THIRDARM
```

- 6. `PS1='\n'`
- 7. `PS1='\W [!]'`
- 8.

```
[jon@frogbog jon]$ THIRDARM=4
[jon@frogbog jon]$ echo "My third arm is number THIRDARM out of1000"
My third arm is number 4 out of1000
[jon@frogbog jon]$
```

- 9. `echo 'The serial number of my third arm is stored in variable THIRDARM'`
- 10. `echo 'Today's date is: date'`
- 11. `DATELINE=`Today's date is: date``
- 12. `DATELINE='Today dates is: date``

# 第 8 章习题答案

- 1. `mkdir theoretical && cd theoretical`
- 2. `touch test ; cd .. ; rmd theoretical 2>/dev/null || echo 'Theoretical is actual'`
- 3. `! cd not-really-a-directory 2>/dev/null && echo "not really a directory"`

```
4. if -f passwordlists -w ]; then
cat /etc/passwd = passwordlists
fi
```

```
5. if -f passwordlists -w ]; then
cat /etc/passwd = passwordlists
else
echo "No file passwordlists or not writable"
fi
```

# 附录 A 习题答案

- 6.

```
if -f passwordlists -a -w ]; then
cat /etc/passwd >> passwordlists
elif -f passwordlists ]; then
    touch passwordlists
else
    echo "File not writable"
fi
```

- 7. `[ -L /dev/mouse ] && echo "That's not a mouse!"`

```
8. case AUTHOR in
L)
    echo "That's a great book!"
;)
    echo "That's a pretty book."
*)
    echo "I haven't read that book."
esac
```

- 9.

```
for foo in $HOME/* do
[ -d foo ] && echo "foo is a directory"
done
```

- 10.

```
for foo in a b c e f g i j l m p q s u v x z do
echo foo:
ls -d foo
done
```

- 11.

```
[jon@frogbog jon]$ mkdir signal
while [ -d signal ]
do
echo "Signal exists"
done
```

- 12.

```
[jon@frogbog jon]$ mkdir signal
until [ -d signal ]
do
echo "Signal exists"
done
```

# 第 9 章习题答案

- 1. `alias mc="mv"`
- 2. `alias mc="echo 'I think you mean.'; mv`
- 3. `unalias mc`
- 4.

```
function mc{
echo 'I think you mean.';
mv $1 $2
}
```

- 5.

```
function vm{
mv $1
}
```

- 6.

```
[jon@frogbog jon]$ cat
#!/bin/sh
if [ -f $1 ]
then
echo "$1 is not a regular file."
exit 1
fi
cat $1 | tac | rev
```

- 7.

```
[jon@frogbog jon]$ cat
#!/bin/sh
if [ -z "$1" -o "$1" = "." ]
then
cat | tac | rev
elif [ -f $1 ]
then
echo "$1 is not a regular file."
exit 1
else
cat $1 | tac | rev
fi
```

- 9.

```
[jon@frogbog jon]$ cat
#!/bin/sh
read FOO
echo $FOO|sed 's/_/g'
```

- 10.

```
[jon@frogbog jon]$ cat
#!/bin/sh
[ -t 0 ] && echo "Please input line of text:"
read FOO
echo $FOO|sed 's/_/g'
```

- 11.

```
[jon@frogbog jon]$ cat
#!/bin/sh
[ -t 0 ] && echo "Please input text:"
while read FOO
do
echo $FOO|sed 's/_/g'
done
```
