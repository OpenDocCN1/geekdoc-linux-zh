
从技术上讲，引号仅在保留值内部的空格是必要的，但它可以有助于读性。

变量可以包含命令的输出。将变量设置为命令的输出的好处是，你可以利用在特定条件下变化的信息。在这个示例中，`MACHINE` 变量被设置为 `uname -n` 命令的输出。这将始终将 `MACHINE` 设置为你当前计算机的名称，如下：

```
MACHINE=`uname -n`
```

反引号包含的命令在子壳（subshell）中执行，输出存储在变量名中。

变量还可以取其他变量的值。这是在 Shell 脚本运行时利用变化信息的一种方法。例如，Shell 脚本可以确定账户余额 (`$CurrentBalance`)，然后将该值存储在 `BALANCE` 变量中，从而允许按所示保存值：

```
BALANCE=$CurrentBalance
```

赋值时，只需要变量名。在引用时，变量名之前必须带有一个美元符号 (`$`)。

# 执行算术求值

虽然 Shell 脚本中的变量可以包含数字，除非通过内置 `types` 命令指示，否则所有值都将被视为数字字符串。可以使用内置的 `let` 命令或通过外部 `expr` 命令执行整数算术运算。例如，假设变量 `BIGNUM` 包含值 1024，以下两条命令都将在 `RESULT` 中存储值 64：

```
let Result=$BIGNUM/16
```

```
Result=`expr $BIGNUM 16`
```

虽然 Shell 脚本的大部分元素是相对自由格式的（空格等空白字符并不重要），但上述两个命令对空格都非常敏感。`let` 命令强制操作数和运算符之间不能有空格，而 `expr` 命令则需要空白符。

`bash` 的 `let` 命令中可用的有效数学运算列表 12-1，按优先级从高到低排列。同一行中的多个运算符表示优先级相同。表 12-2 列出了 `expr` 命令的有效运算符。

# 第 12 章 系统任务自动化 381

| 运算符 | 描述 |
|---|---|
| & | 位与 |
| ^ | 位异或（互斥或） |
| | | 位或 |
| && | 逻辑与 |
| \|\| | 逻辑或 |
| = *= % += - <= &= ^ = | 赋值 |

# 表 12-2
expr 中的数学运算

| 运算符 | 描述 |
|---|---|
| * / % | 乘法、除法和模（余数） |
| - | 加法和减法 |
| < <= > ! = -- | 比较：小于；小于等于；大于等于；大于；不等于；以及两种相等的表示方式 |
| & | 逻辑与 |
| | | 逻辑或 |

# 使用程序结构

使 Shell 脚本如此强大特性之一是它们实现了与编译后编程语言中类似的循环结构。根据你的需求，可以使用几种不同类型的循环。

## for...do 循环

常用的循环之一是 `for...do` 循环。它遍历一个值列表，为列表中的每个元素执行循环体。语法和示例如下所示：

```
for VAR in LIST
do
  ( body )
done
```

`VAR` 可以由任何有效的变量名指定。`LIST` 可以由任何可以枚举的内容（数字、字母、路径名、日期等）组成，因为每个

表 12-3 列出了在 `if` 语句括号之间可以存在的左侧测试表达式。左括号本身标志着语句的“测试”部分。事实上，上述每个 `if` 语句都可以重写为不带括号的形式，如下所示：

```bash
if test expression
```

当对表达式进行求值时，结果结果为 0（表示“真”）或 1（表示“假”）。

| 表 12-3 | 测试表达式的各种符 |
| :--- | :--- |
| 操作符 | 测试的是什么？ |
| -b file | 文件是否为特殊块（例如，块设备）？用于识别磁盘和磁带设备。 |
| -c file | 文件是否为特殊字符设备（例如，字符设备）？用于识别串口线和终端设备。 |
| -d file | 文件是否为目录？ |

# 第 12 章 ✦ 自动化系统任务 383

| 操作符 | 测试的是什么？ |
| :--- | :--- |
| -e file | 文件是否存在？ |
| -f file | 文件是否存在且是否为普通文件（例如，不是目录、套接字、管道、链接或设备文件）？ |
| -g file | 文件是否设置了 set-group-id 位？ |
| -G file | 文件是否存在且其组所有权与当前用户的主组相同？ |
| -k file | 文件是否设置了粘位（sticky bit）？ |
| -L file | 文件是否为符号链接？ |
| -n string | 字符串长度是否大于 0 字节？ |
| -O file | 文件是否存在且由当前用户所有？ |
| -p file | 文件是否为命名管道？ |
| -r file | 文件是否存在且可读？ |
| -s file | 文件是否存在且是否大于 0 字节？ |
| -t fd | 文件是否存在且是否为套接字？ |
| -u file | 描述符是否打开？ |
| -w file | 文件是否设置了 set-user-id 位？ |
| -x file | 文件是否存在且可执行？ |
| -z string | 字符串长度是否为 0 字节？ |
| expr1 -a expr2 | 第一个表达式和第二个表达式是否都为真？ |
| expr1 -o expr2 | 两个表达式是否有一个为真？ |
| file1 -nt file2 | 第一个文件是否比第二个文件新（使用修改时间）？ |
| file1 -ot file2 | 第一个文件是否比第二个文件旧（使用修改时间）？ |
| file1 -ef file2 | 两个文件是否通过链接（硬链接或符号链接）关联？ |
| var1 -eq var2 | 第一个变量是否等于第二个变量？ |
| var1 -ge var2 | 第一个变量是否大于或等于第二个变量？ |
| var1 -gt var2 | 第一个变量是否大于第二个变量？ |
| var1 -le var2 | 第一个变量是否小于或等于第二个变量？ |
| var1 -lt var2 | 第一个变量是否小于第二个变量？ |
| var1 -ne var2 | 第一个变量是否不等于第二个变量？ |

# 第三部分 管理 Red Hat Linux

以下是演示 `if` 语句和测试表达式用的一些示例：

```bash
if [ -x /usr/sbin/ifconfig ]
if [ $4 = "nl" ]
if [ $# -gt 2 ]
if [ -z $HOSTNAME ]
```

在前面的示例中，第一个语句检查 `/usr/sbin/ifconfig` 程序是否可执行。第二个示例将字符串值 `nl` 与存储在 `$4`（第四个命令行参数）中的值进行比较。下一行检查命令行参数的数量（用 `$#` 表示）是否大于二。最后一个示例演示变量 `$HOSTNAME` 是否为空。

## 用于嵌套 if 语句的 case 命令

另一个有用的结构是 `case` 命令。它类似于编程语言中的 `switch` 语句，可以替代多个嵌套语句。`case` 语句的一般形式如下：

```bash
case "VAR" in
  Result1) { body }
    ;;
  Result2) { body }
    ;;
  *) { body }
esac
```

下面是一个 `case` 命令的示例。这段代码片段根据 `/etc/passwd` 文件中第七个（逗号分隔的）字段报告的用户默认 shell 来设置 `TYPE` 和 `RCFILE`：

```bash
Shell=$(grep "^USER:" /etc/passwd | awk -F: '{ print $7 }')
case "$SHELL" in
  /bin/sh)
    Type=Bourne
    RCFILE="profile"
    ;;
  /bin/csh)
    Type=C
    RCFILE=".cshrc"
    ;;
  /bin/bash)
    Type=Bourne
    RCFILE=".bashrc"
    ;;
  /bin/tcsh)
    Type=C
    RCFILE="tcshrc"
    ;;
  *)
    Type=other
    RCFILE="unknown"
esac
```

## while ... do 和 until ... do 循环

另外两种可能的循环结构是 `while ... do` 循环和 `until ... do` 循环。它们的结构如下所示：

```
while condition          until condition
do                       do
  ( body )               ( body )
done                     done
```

在 `while` 循环中，当条件为真时执行循环体；而在 `until` 循环中，当条件为假时执行循环体。`while` 循环通常用于读取文件直到文件结束（EOF）。以下是一个示例：

```bash
while read COL1 COL2
do
  echo "$COL1 $COL2"
done
```

在 `until` 循环中，当条件为真时停止循环。`until` 循环通常用于检查目录直到满足某个条件。以下是一个示例：

```bash
Count=1
until [ $Count -eq 4 ]
do
  DIR=/home/$Count
  if [ ! -d "$DIR" ];
  then
    mkdir "$DIR"
  fi
  let Count+=1
done
```

该脚本在 `/home` 目录中检查磁盘空间。如果条件满足，则会创建一个临时文件。

```bash
#!/bin/bash
Count=1
while :
do
  echo -n "$Count Continue? (y/n): "
  read ANS
  case "$ANS" in
		y|Y)    break
```

来自 `/home` 目录的输出值：

```bash
#!/bin/bash
TMPFILE=/tmp
for I in $(awk -F': '{ if ($3 > 500) print $6 }' /etc/passwd); do
  du -s "$I" > "$TMPFILE"
done
sort -rn "$TMPFILE"
rm "$TMPFILE"
```

该脚本通过 `/etc/passwd` 文件选择特定的信息。使用冒号作为分隔符（`-F:`），`awk` 检查每行的第三字段（用户 ID）是否大于或等于 500（默认情况下普通用户的起始点）。如果是，则返回用户的家目录（第六个字段）。`for` 循环遍历 `awk` 返回的列表，并对每个目录进行磁盘使用检查。结果存储在一个唯一的临时文件中（`$` 代表运行程序的 ID）。该临时文件将按数值排序，然后删除。上述程序的输出可能如下：

```
936890    /home/jsmith
489349    /home/oracle
20439     /home/wilhelm
748       /home/acorad
8         /home/gandalf
8         /home/johnson
8         /home/seitz
8         /home/buchanan
```

# 一个杀死进程的脚本

另一个可能频繁使用的示例是下面这个优雅杀死进程的脚本。该脚本为进程提供了每一个机会清理任何临时文件，通知父进程它正在退出，并静静地终止。

```bash
#!/bin/bash
#
for I in `echo $*`
do
    for J in 15 2 1 9
    do
        kill -$J $I && sleep 1
    done
done 0
```

此脚本会循环遍历命令行指定的进程 ID 列表。为了确保进程已终止，它会按严重程度递增的顺序向进程发送多个信号。尝试尝试的第一个信号是 15（信号号 15 是 SIGTERM），它请求终止进程。下一个信号是 2（信号 2 是 SIGINT），代表来自键盘的中断（即 Ctrl+C 或类似操作）。然后会尝试信号 1，SIGHUP，它试图通过指示控制终端已“挂断”来杀死进程，这是在串口控制台盛行时留下的遥测残留。

最后，向进程发送信号 9，SIGKILL。这个最后的手段信号不允许进程在退出时执行任何活动——它只是尝试“无忌惮地杀死”。只有在之前的杀死进程尝试失败时，才会触发一秒延迟，为进程留出一些时间捕获每个信号并正常退出。

有关信号完整列表，请参考信号 7 手页（输入 `man 7 signal`）。在本章后续中将检查更高级的脚本。

# 系统初始化

在启动过程中，从内核阶段（加载内核、探测设备和加载驱动程序）到 init 的转换由以下行指示：

```
INIT: version 2.74 booting
```

`init` 程序是 SysVinit-2.74-11 RPM 包的一部分，现在它接管了控制权。它被称为“所有进程之父”，`ps` 的输出将始终将 `init` 列为 PID（进程标识符） 1。它的动作由 `/etc/inittab` 文件指导，该文件复制如下：

```
#
# inittab      此文件描述了 INIT 进程应该如何在特定的运行级别（run-level）
#               设置系统。
#
# Author:      Miquel van Smoorenburg, <miquel@drinkel.nl.mugnet.org>
#               由 Marc Ewing 和 Donnie Barnes 为 RHS Linux 修改
#
# 默认运行级别。RHS 使用的运行级别如下为：
# 0 - 停止 (不要将 initdefault 设置为此级别)
# 1 - 单用户模式
# 2 - 多服务器模式，不带 NFS (如果没有网络，则与 3 相同)
# 3 - 全多用户模式
# 4 - 未使用
# 5 - X11
# 6 - 重启 (不要将 initdefault 设置为此级别)
#
# id:3:initdefault:
# 系统初始化。
si::sysinit:/etc/rc/d/rc.sysinit

10:0:wait:/etc/rc/d/rc 0
11:1:wait:/etc/rc/d/rc 1
12:2:wait:/etc/rc/d/rc 2
13:3:wait:/etc/rc/d/rc 3
14:4:wait:/etc/rc/d/rc 4
15:5:wait:/etc/rc/d/rc 5
16:6:wait:/etc/rc/d/rc 6

# 在每个运行级别运行的项目。
ud::once:/sbin/update

# 捕捉 CTRL-ALT-DELETE
ca::ctrlaltld:/sbin/shutdown -t3 -r now

当我们的 UPS 告诉我们断电时，假设我们还有几分钟电。在 2 分钟后调度关机。
# 这当然假设你安装了电源且
# UPS 连接并工作正常。
p::powerfail:/sbin/shutdown -f -h +2 "Power Failure: System Shutting Down"

如果在关机启动前恢复电源，则取消它。
pr:12345:powerokait:/sbin/shutdown -c "Power Restored: Shutdown Cancelled"

# 在标准运行级别下运行 getty
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingtty tty5
6:2345:respawn:/sbin/mingtty tty6

# 在运行级别 5 下运行 xdm
# xdm 现在是一个独立的服务
x:5:respawn:/etc/X11/prefdm -nodemon
```

纯文本 `inittab` 文件包含了几个用冒号分隔的字段，格式如下：

```
id:runlevels:action:command
```

`id` 字段是一个唯一标识符，长度为一到四个字母数字字符。`runlevels` 字段包含命令将运行的运行级别列表。常见的运行级别有 0, 1, 2, 3, 4, 5 和 6（s 代表单用户模式，等同于 1）。运行级别 7、8 和 9 不是标准的；它们也可以用作与需求动作（a、b 和 c，等同于 A、B 和 C）关联的特殊运行级别。

在每个运行级别执行的动作如下：

| 动作 | 运行级别说明 |
| :--- | :--- |
| once | 在指定的运行级别运行一次 |
| respawn | 进程退出后重新启动 |
| wait | 等待命令完成 |
| ctrlaltld | 捕捉 Ctrl-ALT-DELETE |
| powerfail | 处理断电情况 |
| powerokait | 电源恢复后取消关机 |
| initdefault | 在运行级别下执行命令 |
| sysinit | 系统初始化 |

此脚本会循环遍历命令行指定的进程 ID 列表。为了确保进程已终止，它会按严重程度递增的顺序向进程发送多个信号。尝试的第一个信号是 15（信号号 15 是 SIGTERM），它请求终止进程。下一个信号是 2（信号 2 是 SIGINT），代表来自键盘的中断（即 Ctrl+C 或类似操作）。然后会尝试信号 1，SIGHUP，它试图通过指示控制终端已“挂断”来杀死进程，这是在串口控制台盛行时留下的遥测残留。

最后，向进程发送信号 9，SIGKILL。这个最后的手段信号不允许进程在退出时执行任何活动——它只是尝试“无忌惮地杀死”。只有在之前的杀死进程尝试失败时，才会触发一秒延迟，为进程留出一些时间捕获每个信号并正常退出。
