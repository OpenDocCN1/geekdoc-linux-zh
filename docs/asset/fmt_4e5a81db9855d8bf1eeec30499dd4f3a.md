
Korn shell 对 `-x` 和 `-v` 的实现类似，但包含了一些实用的扩展。第一个允许你交互式地设置 `-x` 或 `-v` 的效果，以便你发的所有命令都会被跟踪，包括立即执行的命令和在你调用的脚本中的命令。第二个扩展使跟踪的命令更加突出。

### UNIX (Korn shell)

格式：

`$ set -x # 开启带变量替换的跟踪`

`$ set -o xtrace # 等同于 set -x`

`$ set -v # 在读取命令时开启跟踪`

`$ set -o verbose`

`# 等同于 set -v`

格式：

`* PS4:string # 跟踪指示字符串`

示例：

```
$ cat test_script
print
"Listing directory
$i"
is -i $i
$ PS4="From test script> "
$ set -o xtrace
$ test_script
mathcounts
From test_script>
print "Listing directory mathcounts"
Listing directory mathcounts
From test_script>
is -i mathcounts
-rwxr-xr-x
1 McK 65536 Jan 8 19:19 practice
examples
$ rm test_script
```

### 总结

```
From test_script>
rm test_script
$ set +o xtrace
```

在这个示例中，我们将默认的跟踪指示字符串 `+` 替换为我们特定需要的 `From test_script>`。然后我们开启了已执行变量替换的跟踪。当我们执行脚本 `test_script` 时，我们首先看到变量被替换后的每一行，因为它们已准备好执行。该行之前有一个跟踪指示字符串。接下来我们看到执行该行的结果。在脚本完成后，该设置仍然有效。此时，跟踪指示字符串意义不大，尽管它仍然保持不变。最后，使用 `set +o xtrace` 关闭跟踪。

Perl 没有提供类似于 shell `-x` 和 `-v` 选项的机制，这是因为其工作方式：脚本首先被翻译成中间代码，然后才执行。这样做是为了优化脚本的执行速度，但生成的中间代码并不是人类想要阅读的。然而，Perl 确实提供了一个调试选项 `-d`，可以在命令行或脚本内部调用。这是一个强大的交互式调试器，类似于适用于编译语言的调试器，它允许用户在程序执行时逐语句地单步程序源代码。所有典型的调试器功能都是可用的，例如在执行期间设置断点和检查变量。更多信息请参阅 `perl` man 页面。

对三个带注释脚本文件和一个 Perl 脚本的讨论总结了本章介绍的功能。第一个脚本文件 `run_program` 请求用户对多个问题做出回答并创建一个名为 `prolsq` 的脚本文件。脚本流取决于用户是否将参数作为命令行的一部分。如果用户未指定参数，系统将提示相应的输入。UNIX `run_program`：使用符号链接将数据文件与 `PROLSQ` 相关，然后执行程序。

```
# 显示横幅消息
echo "Prolsq Submission Procedure"
echo "
if ($i == "help")
then
# 如果需要帮助则重定向
goto info
endif
if ($i == " ") then
echo "Interactive input mode..."
# 确定第一个参数是否定义
# 是: 假设所有参数已定义
echo ....
# 否: 交互式提示参数
else
echo "Predefined input mode..."
echo ....
if ($7 == " ") then
# 如果未定义7个参数
echo "Incorrect number of arguments"
exit
endif
set card1 = $i
# 将变量赋值给输入
set card2 = $2
set card3 = $3
set card4 = $4
set card5 = $5
set card6 = $6
set card7 = $7
goto start_execution
# 跳转到执行阶段
endif
# 开始交互式输入阶段
echo -n "CONTROL DATA FILE = prolsq.dat)
set card1 = $1
# 为每个变量赋值
# 如果你没有使用 C shell 的快速启动
# own赋值一个默认值
if ($card1 == "") then
set card1 = "prolsq.dat"
endif
echo -n "INPUT RESTRAINTS FILE = atmdst.dat)
set card2 = $2
# 对剩余参数重复此操作
if ($card2 == "") then
set card2 = "atmdst.dat"
endif
echo -n "INPUT SHIFTS FILE = shift.in)
set card3 = $3
if ($card3 == "") then
set card3 = "shift.in"
endif
echo -n "OUTPUT SHIFTS FILE = shift.out)
set card4 = $4
if ($card4 == "") then
set card4 = "shift.out"
endif
echo -n "REFLECTION INPUT FILE = prolsq.hkl)
set card5 = $5
if ($card5 == "") then
set card5 = "prolsq.hkl"
endif
echo -n "STRUCTURE FACTOR OUTPUT FILE = prolsq.fofc)
set card6 = $6
if ($card6 == "") then
set card6 = "prolsq.fofc"
endif
echo -n "COORDINATE OUTPUT FILE = xyz.out)
set card7 = $7
if ($card7 == "") then
set card7 = "xyz.out"
endif
# start_execution:
# 将所有参数写入脚本文件
echo "csh" > runscript.scr
echo "set -x" >> runscript.scr
echo "set -v" >> runscript.scr
echo "PS4=\"From test_script> \"" >> runscript.scr
echo "cat $card1" >> runscript.scr
echo "cat $card2" >> runscript.scr
echo "cat $card3" >> runscript.scr
echo "cat $card4" >> runscript.scr
echo "cat $card5" >> runscript.scr
echo "cat $card6" >> runscript.scr
echo "cat $card7" >> runscript.scr
echo "prolsq.exe < $card1 > $card7"" >> runscript.scr
chmod +x runscript.scr
./runscript.scr
# 输出被写入 stdout
echo "Execution finished"
exit
```

### 10.1 总结

在命令行中执行且不需要交互式提示。程序流传递到一个语句，检查是否已指定所有七个必要的参数。如果已指定，控制权将传递到标记 `start_execution` 的语句。如果七个参数都没有定义，脚本将带有错误消息并终止。如果没有指定任何参数，脚本将提示用户输入相应的输入，并提供默认响应。
