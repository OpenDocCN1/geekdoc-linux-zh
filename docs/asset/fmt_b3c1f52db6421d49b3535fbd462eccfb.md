
## BASH_SOURCE, FUNCENAME, LINENO AND BASH_LINENO

`BASH_SOURCE`、`FUNCENAME`、`LINENO` 和 `BASH_LINENO` 是极其有用的调试变量，即使在你使用多个文件时，它们也能告诉你处于脚本的什么位置。`LINENO` 仅给出脚本中的当前行号：

```bash
$ cat funcname.sh
#!/bin/bash

echo "Hello, World"
echo "This is line $LINENO"
$ ./lineno.sh
Hello, World
This is line 4
$
```

这对于调试以及实际上从终端用户那里获取有用信息非常有帮助。与其报告“在第四个调试点发生错误”，不如你的脚本可以给出精确的行号，让你能够精确定地诊断脚本中的任何问题。然而，知道你当前处于哪个函数中很有用，而 `FUNCENAME` 正告诉了你这一点。它还提供了完整的堆栈，显示了你最初是如何进入该函数的：

```bash
$ cat funcname.sh
#!/bin/bash

function func1() {
  echo "func1: FUNCENAME0 is ${FUNCNAME[0]}"
  echo "func1: FUNCENAME1 is ${FUNCNAME[1]}"
  echo "func1: FUNCENAME2 is ${FUNCNAME[2]}"
  echo "func1: LINENO is ${LINENO}"
}

function func2() {
  echo "func2: FUNCENAME0 is ${FUNCNAME[0]}"
  echo "func2: FUNCENAME1 is ${FUNCNAME[1]}"
  echo "func2: FUNCENAME2 is ${FUNCNAME[2]}"
  echo "func2: LINENO is ${LINENO}"
}
}
```

```bash
$ ./funcname.sh
func1: FUNCTIONNAME0 is func1
func1: FUNCTIONNAME1 is main
func1: FUNCTIONNAME2 is 8
func1: LINENO0 is func2
func2: FUNCTIONNAME1 is func1
func2: FUNCTIONNAME2 is main
func2: LINENO is 17
$
```

因此在 `func2` 中，你可以看到 `FUNCTIONNAME[0]` 是你所处的函数名称，`FUNCTIONNAME[1]` 是调用你的函数，而 `FUNCTIONNAME[2]` 是调用 `func1` 的函数（实际上是主脚本，因此是特殊的 "main"）。这非常有用且有趣，但当你有包含不同函数的各种库文件时该如何处理？

```bash
$ cat main1.sh
#!/bin/bash
. lib1.sh
. lib2.sh
```

```bash
$ cat lib1.sh
function func1()
{
echo "func1: FUNCTIONNAME0 is ${FUNCTIONNAME[0]}"
echo "func1: FUNCTIONNAME1 is ${FUNCTIONNAME[1]}"
echo "func1: FUNCTIONNAME2 is ${FUNCTIONNAME[2]}"
echo "func1: BASH_SOURCE0 is ${BASH_SOURCE[0]}"
echo "func1: BASH_SOURCE1 is ${BASH_SOURCE[1]}"
echo "func1: BASH_SOURCE2 is ${BASH_SOURCE[2]}"
echo "func1: LINENO is ${LINENO}"
func2
}
```

```bash
$ cat lib2.sh
function func2()
{
echo "func2: FUNCTIONNAME0 is ${FUNCTIONNAME[0]}"
echo "func2: FUNCTIONNAME1 is ${FUNCTIONNAME[1]}"
echo "func2: FUNCTIONNAME2 is ${FUNCTIONNAME[2]}"
echo "func2: BASH_SOURCE0 is ${BASH_SOURCE[0]}"
echo "func2: BASH_SOURCE1 is ${BASH_SOURCE[1]}"
echo "func2: BASH_SOURCE2 is ${BASH_SOURCE[2]}"
echo "func2: LINENO is ${LINENO}"
}
```

## TIMEFORMAT

`time` 命令通常输出一种机器易于读取的格式，但其描述并不十分详尽。虽然可以编写额外的脚本来解释并重新格式化数据，但 `TIMEFORMAT` 变量已经为你完成了大多数你可能遇到的场景处理。它的格式与 `printf` 类似，其中 `%` 符号标记特殊字符，并替换为相应的值。`%s` 显示进程在用户模式（非操作系统系统调用）下花费的时间，`%S` 显示在系统模式下的时间，`%R` 显示总运行时间。这些每一项都可以通过添加 "l"（小写 "L"）进行修改，将时间扩展为分钟和秒，并/或添加精度修饰符（0-3），显示你希望秒精确到几位小数。

标准时间格式如下：

```bash
$ time ls > /dev/null
real 0m.007s
user 0m.001s
sys 0m.001s
```

实际上，使用这种格式是因为当 `TIMEFORMAT` 未设置时，`bash` 会使用以下设置：

```bash
'nreal%3R%nuser%3LU%nsys%3S'
```

如果 `TIMEFORMAT` 未设置，`time` 将完全没有任何输出。

POSIX 时间格式是标准格式，通过 `-p` 参数访问：

```bash
$ time -p ls > /dev/null
real 0.00
user 0.00
sys 0.00
```

为了以更易读的格式显示 CPU 占用率，可以如下设置 `TIMEFORMAT` 变量：

```bash
$ TIMEFORMAT="%2U user + %2S system / %2R elapsed = %%%f CPU Utilisation"
$ time sleep 2
0m.00s user + 0m.00s system / 0m.02s elapsed = 0.04% CPU Utilisation
$ time -R /var > /dev/null
0m.07s user + 0m.05s system / 0m.31s elapsed = 9.97% CPU Utilisation
$ time ls > /dev/null
0m.00s user + 0m.00s system / 0m.00s elapsed = 100.00% CPU Utilization
```

同样，`TIMEFORMAT` 可以用来比标准时间输出更自然的方式显示经过的时间。

```bash
$ TIMEFORMAT="%U user + %1S system = %1R elapsed time"
$ time ls -R /var > /dev/null&1
0m.036s user + 0.020s system 0m.056s elapsed time
$
```

`sleep` 不消耗太多用户时间或系统时间，因此数字并不完全对等。剩余的时间将用于等待系统处理任务：

```bash
$ time sleep 1
0.001 user + 0.000 system total = 0m.002s total elapsed time
$ time expr 123 \*321
39483
0.001 user + 0.002 system = 0m.043s total elapsed time
```

从 `/dev/urandom` 读取 512MB 需要花费大量时间。这是因为 `/dev/urandom` 提供的是从环境中生成的随机数据，而足够的随机性可能需要时间来排序。

```bash
$ time dd if=/dev/urandom of=randomfile bs=1024 count=512
512=0 records in
512=0 records out
536870912 bytes (512 MB) copied, 63.5919 seconds, 8.4 MB/s
0.003 user + 56.113 system = 1m.614s elapsed time
$
```

## PPID

`PPID` 设置为调用此 shell 脚本的进程 ID。`$$` 是另一个特殊变量，提供 shell 自身的进程 ID。`$$` 是创建临时文件（唯一文件名）的一种几乎安全的方法。`$$` 对于对于脚本在多个副本同时运行时识别自身也非常有用：

> `mkdir`（在第 12 章介绍）通常是创建临时文件的更好方法。

```bash
$ cat pid.sh
#!/bin/bash
echo "Process $$: Starting with arguments $0 for my parent, $$PPID"
sleep 10
$ ./pid.sh 1 & ./pid.sh 2 & ./pid.sh 3
[1] 2529
[2] 2530
Process 2531: Starting with arguments 3 for my parent, 2484
Process 2529: Starting with arguments 1 for my parent, 2484
Process 2530: Starting with arguments 2 for my parent, 2484
[1]- Done
$ ./pid.sh 1
[2]+ Done ./pid.sh
$
```

## RANDOM

`RANDOM` 产生一个 0 到 32767 之间的随机数。这个简单的配方产生 200 到 500 之间的随机数：

```bash
$ cat random.sh
#!/bin/bash
MIN=200
MAX=500
let scope = $MAX - $MIN
if [ $scope -le "0" ]; then
  echo "Error - MAX is less than MIN!"
fi
for i in $(seq 10)
do
  let result=$RANDOM % $scope + $MIN
  echo "A random number between $MIN and $MAX is $result"
done
$ ./random.sh
A random number between 200 and 500 is 462
A random number between 200 and 500 is 400
A random number between 200 and 500 is 350
A random number between 200 and 500 is 279
A random number between 200 and 500 is 339
A random number between 200 and 500 is 401
A random number between 200 and 500 is 465
A random number between 200 and 500 is 320
A random number between 200 and 500 is 290
A random number between 200 and 500 is 277
```

首先使用取模运算符计算范围（`scope`），以确保值在范围内。然后将 `$MIN` 值加到随机数，以产生范围内的数字。

## REPLY

在未提供变量时，`REPLY` 是 `read` 的默认变量名。

```bash
$ read
hello world
$ echo $REPLY
hello world
```

## SECONDS

`SECONDS` 返回 shell 运行的秒数（整数）。对于 shell 脚本，这是脚本本身的运行时间，而不是调用它的 shell 的运行时间。如果你将 `SECONDS` 的值改为非整数，它将将其设置为零。如果你取消设置 `SECONDS`，它将失去特殊功能并变成一个普通变量，即使你之后再次设置它。

`SECONDS` 有很多用途，而不只是计时：如果 shell 脚本需要偶尔且不可预测的数字，它可以使用 `(sleep 1; echo $SECONDS)` 获取一个之前未使用过的数字。`SECONDS` 的另一个用途是由于 `timeout(1)` 命令返回它执行的命令的退出状态，除非它超时，此时它会返回 124。因此，无法判断命令是实际上超时了，还是它本身返回了 124。`SECONDS` 可以帮你准确判断命令是否超时：

```bash
#!/bin/bash
SECONDS=0
timeout 60s slow_command
timeout_res=$?
# 如果超时则返回 124，但 124 也可能是 slow_command 的返回码
if [ "$SECONDS" -ne 0 ]; then
  # 它没有超时；值来自 slow_command。
  echo "The command did not time out; it returned $SECONDS seconds."
fi
```

### 秒钟 | 61

![](img/5be99b1df3e454de85e6ef3c64fc3870_96_0.png)

这涉及到更复杂的匹配匹配，如图 3-2 所示：

![](img/5be99b1df3e454de85e6ef3c64fc3870_96_1.png)

**图 3-2**

在图 3-2 中，第一个 `ls` 显示目录中的文件。目录 `FOO/*.php` 表示 `echo $FOO` 将匹配所有的 .php 文件。设置 `GLOBIGNORE=*.php` 意味着 `echo $FOO` 就像没有找到匹配的文件一样——它输出实际的、意外之外的值，即字符串 "*.php"。

当你设置 `GLOBIGNORE=a*` 时，`echo $FOO` 会忽略以 "a" 开头的文件，而设置 `GLOBIGNORE=*.php` 则会导致任何匹配这些模式之一的文件被忽略。

这在使用版本控制系统时也很有用。例如，图 3-3 显示了一些带有 "~" 后缀的备份文件：

### 第 3 章 变量

![](img/5be99b1df3e454de85e6ef3c64fc3870_97_0.png)

**图 3-3**

## HOME

`HOME` 是当前用户主目录的路径。如果你单独运行 `cd`，它将切换到 `$HOME` 的值。`$HOME` 也可以被表示为 "~"，所以这些命令指向 `HOME` 变量的值：

```bash
cd ; grep proxy .wgetrc
cd $HOME ; grep proxy .wgetrc
grep proxy ~/.wgetrc
grep proxy $(HOME)/.wgetrc
```

所有这些都会在当前用户的 `$(HOME)/.wgetrc` 文件中进行 `grep`。

## IFS

`IFS` 是内部字段分隔符（Internal Field Separator）：它列出了可能用作空白字符的字符集。它的默认值是换行符 `<newline>`。当你在本章之前查看 `VAR` 时，你会看到 `read firstname lastname` 可以用于第一个单词（`firstname`），后面跟着零或多个序列（所有序列都被读入 `lastname` 变量）。这是由于 `IFS` 的原因，如果你将 `IFS` 改为其他内容，你就可以改变它的工作方式。这非常有用，例如在读取冒号分隔的 `/etc/passwd` 文件，或读取由点号分隔的 IP 地址时：

```bash
$ cat ifs1.sh
#!/bin/bash
# 保存原始 IFS
IFS=$IFS
IFS=": "
# /etc/passwd 仅由冒号分隔。
while read login password uid home shell
do
# 忽略那些使用 /bin/false 或主目录在 /var 下的账户
if [ "$shell" = /bin/false ] && [ -z "$home/var*" ]; then
echo "User $login ($(name)) lives in $home and uses $(basename $shell)"
fi
done < /etc/passwd
# 虽然不需要，因为我们正在编辑脚本，但这是一个良好的习惯；
# 后续命令将需要正常的 IFS 值。
IFS=$IFS
$ ./ifsl.sh
User root (root) lives in /root and uses bash
User daemon (daemon) lives in /usr/sbin and uses sh
User bin (bin) lives in /bin and uses sh
User sys (sys) lives in /dev and uses sh
User sync (sync) lives in /bin and uses sync
User game (games) lives in /usr/games and uses sh
User proxy (proxy) lives in /bin and uses sh
```
