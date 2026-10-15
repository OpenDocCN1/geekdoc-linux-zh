
```
# 64 bytes from 127.0.0.99: icmp_seq=0 ttl=61 time=0.14 ms
# 64 bytes from 127.0.0.99: icmp_seq=1 ttl=61 time=0.136 ms
# ---
# 127.0.0.99 ping statistics
# 2 packets transmitted
```

示例 2：我们将对本地服务器进行 `ping`：

良好: `127.0.0.1` 是可 ping 的。

完成。脚本：`./pipe.ksh`

```
PROGRAM: pipe.ksh
/bin/ksh
# PROGRAM: pipe.ksh
# 目的: 显示如何使用管道 ()。
# 程序员: Larry Smith. 修订于 __date___
# 难度: 中等
# 用法: 示例: ./pipe.ksh
# 注释: 此脚本包含了 "ps.ksh" 中找到的一些示例

清空用户的屏幕。
print "\nComment: 这是 script $0"
print "PURPOSE: Show how to use a pipe ()"
```

####################################################################################

print "\nEXAMPLE 1:"

print "正在查看 applicationzzz 是否正在执行。"

####################################################################################

# 我们的目标是使用 `ps` 命令来确定特定的应用程序

#（或守护进程或脚本）是否在系统中活动运行。

# 如果应用程序没有运行，我们将启动它。

# 你可以检查 "sendmail" 守护进程、你的 lp 打印机守护进程、

# 你的工资应用程序或任何程序。我们将检查

# 我们名为 `applicationzzz` 的应用程序之一。

# 知道它在休眠（这非常很好，非常……）是一回事。

# "&" 符号标记 `applicationzzz` 在后台

# 运行的命令子的结束。

```
# 命令 'tr -s " "' 将多个连续空格压缩为 1 个空格； 
# 提高输出的可读性更好。更多：tr.ksh
if [ $(ps -ef | grep 'applicationzzz' | grep -c v 'grep') -eq 0 ]; then SEE "ps.ksh"
print "\nAPPLICATIONzzz is NOT running on this server."
print "\nATTEMPTING TO BRING UP APPLICATION"
/home/larry/ROSETTA/applicationzzz.ksh >/dev/null 2>&1 &
sleep 5 # 给系统 2 秒
if [ $(ps -ef | grep 'applicationzzz' | grep -c v 'grep') -eq 0 ]; then
print "PROBLEM: APPLICATIONzzz is still NOT running on this server."
print "EXITING"
```

```
else
print "\nGOOD: APPLICATIONzzz is now running on this server."
print "Here's the applicationzzz process on this server:"
ps -ef | grep applicationzzz | grep -v tr -s [' ' ]
if [ $counter -ne inner_most_if_then ]; then
print "GOOD: applicationzzz IS running on this server."
print "Here's the applicationzzz process on this server:"
ps -ef | grep applicationzzz | grep -v tr -s [' ' ]
fi
print "END: else",
```

####################################################################################

print "\nEXAMPLE TWO:"

# 我们正在寻找 (`grep 'getty'`) `'getty'`

# `"getty"` 进程与 tty/s 终端连接

`counter=$(ps -ef | grep 'getty' | grep -c v 'grep')`

if (( `counter` == 0 )); then

print `"'getty' IS NOT running."`

elif (( `counter` == 1 )); then

print `"'getty' IS running."`

elif (( `counter` > 1 )); then

print `"'getty' IS running counter times."`

# 378

fi

print "Here are the results from our ps -ef in which we looked for 'getty ' \nps -ef | grep 'getty ' | grep -v grep | tr -s [ '']"

```

################################################################
# 示例三:
################################################################
print "example script 'find.pl'
# 关于 find 命令的更多信息，我们将使用系统 "find" 命令来列出
# 所有以 'get' 开头并 '.pl' 结尾的文件
# 我们将在 home/larry/ROSETTA/ 目录下，我们将使用
# 管道 (|) 来检查系统为我们获取的信息。
# 如果你还不 "find" 命令，你很快就会学会。
# 从命令行执行 find 命令如下：
# find /home/larry/ROSETTA -name '*.pl' -print
# 现在尝试这样运行：
# find -name '*.pl' -print
# 点 (.) 表示“当前目录”
# 很容易获取统计数据（例如字节单位的大小）
# 你在 "find" 中指定文件的完整路径

print "Here is the size and filename for each file that begins with 'getty':"
for filename in $(find /home/larry/ROSETTA -name '*' 2>/dev/null); then
  # $filename 包含绝对文件名（包括完整路径）。
  size=$(ls -l $filename | tr -s ' ' | cut -d ' ' -f3)
  print "$size BYTES $filename"

```

################################################################

# 示例四:

################################################################

print "在这个示例中，我们展示了如何作为命令执行

# 并使用 'tail -3':

ls -ltr /home/larry/ROSETTA/get* | tail -3 | tr -s ' '

# tr -s ' ' 允许我们将多个空格压缩为1个空格。

print "\nDONE. Script: $0"

OUTPUT: pipe.ksh

HOW THE SCRIPT EXECUTED: ./pipe.ksh.

OUTPUT follows:

Comment: 这是 script /pipe.ksh。

目的: 如何使用管道 (|)。

示例一:

正在查看 applicationzzz 是否正在执行。

注意: applicationzzz 没有在此服务器上运行。

现在启动 applicationzzz

良好: applicationzzz 现在正在此服务器上运行。

这是此服务器上的 applicationzzz 进程：

larry 4515 0 14:40 00:00 /bin/bash /home/larry/ROSETTA/applicationzzz

示例二:

'getty' 正在运行6 次。

这是我们通过 ps -ef 查找 'getty' 的结果：

root 3379 1 09:26 tty1 00:00 /sbin/mingetty tty1
