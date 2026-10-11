
`-O nounset` 选项会在引用未设置（或不存在）的变量时终止并报告错误。此选项用于报告拼写错误的变量名。`nounset` 并不保证能识别出所有的拼写错误（见清单 8.1）。

## 清单 8.1 nounset.bash

```bash
#!/bin/bash
#
# A simple script to list files

shopt -O -s nounset
declare -i TOTAL=0

let "TOTAL=TOTAL+1"      # not caught
printf "%s\n" "$TOTAL"

if [ $TOTAL -eq 0 ] ; then  # caught
   printf "TOTAL is %s\n" "$TOTAL"
fi
```

`-O xtrace` 选项会在执行每条命令前显示该命令。该命令中的所有替换和扩展均已完成。

```bash
declare -i TOTAL=0
if [ $TOTAL -eq 0 ] ; then
   printf "%s\n" "$TOTAL is zero"
fi
```

如果此脚本片段在 `xtrace` 选项下运行，您应该看到类似以下结果：

```text
+ alias 'rm=rm -i'
+ alias 'cp=cp -i'
+ alias 'mv=mv -i'
+ '\. /etc/bashrc \'
+ . /etc/bashrc
+++ id -gn
+++ id -u
++ '[' root = root -a 0 -gt 99 ']'
++ umask 022
++ '[' '' ']'
+ declare -i TOTAL=0
+ '[' 0 -eq 0 ']'
+ printf '%s\n' '0 is zero'
0 is zero
```

前 11 行是 Linux 发行版配置文件脚本中执行的命令。加号的数量表示脚本嵌套的层级。最后四行是 Bash 完成所有替换和扩展后的脚本片段。请注意，复合命令（如 `if` 命令）被省略了（见清单 8.2）。

## 清单 8.2 bad.bash

```bash
#!/bin/bash
#
# bad.bash: A simple script to list files

shopt -o -s nounset
shopt -o -s xtrace

declare -i RESULT
declare -i TOTAL=3

while [ $TOTAL -ge 0 ] ; do
    let "TOTAL--"
    let "RESULT=10/TOTAL"
    printf "$d\n" "$RESULT"
done
```

`xtrace` 展示了脚本逐行的执行进度。在这种情况下，脚本包含一个错误，导致 `while` 循环多执行了一次。使用 `xtrace`，您可以检查变量并发现应将 `-ge` 替换为 `-gt`，以防止在 TOTAL 为零时出现无限循环。

```text
$ bash bad.bash
+ declare -i RESULT
+ declare -i TOTAL=3
+ '[' 3 -ge 0 ']'
+ let TOTAL--
+ let RESULT=10/TOTAL
+ printf '$d\n' 5
5
+ '[' 2 -ge 0 ']'
+ let TOTAL--
+ let RESULT=10/TOTAL
+ printf '$d\n' 10
10
+ '[' 1 -ge 0 ']'
+ let TOTAL--
+ let RESULT=10/TOTAL
bad.sh: let: RESULT=10/TOTAL: division by 0 (error token is "lr")
+ printf '$d\n' 10
10
+ '[' 0 -ge 0 ']'
+ let TOTAL=0
+ let RESULT=10/TOTAL
+ printf '%d\n' -10
-10
+ '[' -1 -ge 0 ']'
```

您可以通过为 `PS4` 变量赋值来更改跟踪加号提示。将提示设置为包含变量 `LINENO` 将显示脚本或 shell 函数中的当前行。在脚本中，`LINENO` 显示脚本的当前行号，从第一行的 1 开始。当在 shell 提示符下与 shell 函数一起使用时，`LINENO` 从函数的第一行开始计数。

### 调试陷阱

内置的 `trap` 命令（在第 10 章“作业控制与信号”中有更详细的讨论）可用于在 Bash 处理完每一行后执行调试命令。通常，调试陷阱与跟踪结合使用，以提供跟踪中未列出的额外信息。

当调试陷阱与跟踪结合时，调试陷阱本身在执行时也会列在跟踪中。这使得使用 `printf` 变得有些冗余，因为命令在执行 `printf` 之前已经显示出了所有变量替换完成后的状态。相反，使用空命令 `:` 可以在不执行任何 shell 命令的情况下显示变量（见清单 8.3）。

## 清单 8.3 debug_demo.sh

```bash
#!/bin/bash
#
# debug_demo.sh : an example of a debug trap

trap ': CNT is now $CNT' DEBUG

declare -i CNT=0

while [ $CNT -lt 3 ] ; do
    CNT=CNT+1
done
```

在启用跟踪运行时，CNT 的值会在每一行之后显示。

```text
+ '[ 0 -lt 3 '
++ : CNT is now 0
+ CNT=CNT+1
++ : CNT is now 1
+ '[ 1 -lt 3 '
++ : CNT is now 1
+ CNT=CNT+1
++ : CNT is now 2
+ '[ 2 -lt 3 '
++ : CNT is now 2
+ CNT=CNT+1
++ : CNT is now 3
+ '[ 3 -lt 3 '
++ : CNT is now 3
```

### 版本控制 (CVS)

在商业环境中，金钱和职业生涯都受到威胁，创建一个无瑕疵的程序是不够的。总有一些最后时刻的更改会导致程序产生错误结果甚至崩溃。当这种情况发生时，需要尽快撤销或修正这些更改，且不能丢失数据。

*版本控制系统*是一种维护数据文件、脚本和源程序主副本的程序。这个主副本存储在一个称为*存储库*的目录中。每次添加或修改程序时，都会将其重新提交到存储库，并记录哪些更改被做出、谁做出的以及何时做出。

*CVS* (*Concurrent Versions System*) 是大多数 Linux 发行版提供的版本控制软件。它基于一个名为 RCS (*Revision Control System*) 的旧程序，CVS 可以在多个程序员之间共享脚本并记录任何更改。它可以处理单个文件、整个目录或大型项目。这些文件可以组织成称为*模块*的文件组。CVS 为文件添加时间戳，维护版本号，并在两个程序员同时更新程序的同一部分时识别潜在问题。

CVS 在开源开发中也非常流行。它可以配置为允许世界各地的程序员共同参与项目开发。

要使用 CVS，项目负责人或团队领导必须创建一个目录作为版本控制存储库，以及一个名为 *CVSROOT* 的子目录。然后您定义一个名为 *CVSROOT* 的环境变量，以便 CVS 知道在哪里找到存储库目录。例如，要将 /home/repository 设置为您团队的存储库，请在 Bash 中如下设置 *CVSROOT*：

```bash
$ declare -rx CVSROOT=/home/repository
```

存储库保存项目中所有文件的副本、更改日志以及其他共享资源。

添加到存储库的软件没有特殊要求。然而，当程序被添加或更新时，CVS 会读取文件以查找特殊字符串。如果存在这些字符串，CVS 会用关于该程序副本的最新信息替换这些字符串。CVS 文档将这些字符串称为*关键字*，尽管它们在 Bash 意义上不是关键字。

- `$Author$`—签入该修订版本的用户的登录名。
- `$Date$`—修订版本签入的日期和时间（UTC）。
- `$Header$`—一个标准头部，包含 RCS 文件的完整路径名、修订号、日期（UTC）、作者等。
- `$Id$`—与 `$Header$` 相同，只是 RCS 文件名不包含路径。
- `$Name$`—如果使用标签，这是签出此文件时使用的标签名。
- `$Locker$`—锁定该修订版本的用户的登录名（如果未锁定则为空，这是正常情况，除非使用 *cvs admin -l*）。
- `$Log$`—提交期间提供的日志消息，前面有一个包含 RCS 文件名、修订号、作者和日期（UTC）的头部。现有的日志消息不会被替换。相反，新的日志消息插入在 *$Log$* 之后。
- `$RCSfile$`—不带路径的 CVS 文件名。
- `$Revision$`—分配给该修订版本的修订号。
- `$Source$`—CVS 文件的完整路径名。
- `$State$`—分配给该修订版本的状态。

CVS 关键字可以添加到脚本的任何位置，但如果不在注释中，它们应该出现在注释或引号字符串中。这样可以防止关键字被当作可执行的 shell 命令处理。

```bash
# CVS: $Header$
```

当脚本添加到存储库时，CVS 会填充头部信息。

```bash
# CVS: $Header: /home/repository/scripts/t.sh,v 1.1 2001/03/26 
20:35:27 kburch Exp $
```

CVS 关键字头部应放置在脚本的头部。

```bash
#!/bin/bash
#
# flush.sh: Flush disks if nobody is on the computer
#
# Ken O. Burch
# CVS: $Header$
```

CVS 使用 Linux 的 *cvs* 命令进行控制。*cvs* 后面总是跟随一个 CVS 命令词以及该命令的任何参数。

