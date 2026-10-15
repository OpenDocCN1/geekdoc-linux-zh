

NOTE: This is NOT the log message!
>> check df output for volumes filled > 70%
>> 'D
initial revision: 1.1
done

为了使输出更易读，会插入一个冒号；由于该脚本已经可以正常工作，因此将其纳入版本控制。

## 2.2.2 使用变量

该脚本在创建和测试的系统上运行没有问题。它应该在类似的系统上甚至在不同的 *NIX 发行版上也能正常工作，但你必须确保所需的程序可以通过 $PATH 变量找到。awk 尤其可能引起混淆，因为在大多数现代系统上该程序有两个版本：很久以前创建的原始版本，以及一个更新的版本称为 nawk。后者知道如何定义函数，例如。如果你按上述方式使用该程序，不应该有任何问题，但仍应意识到这一事实。要查明，只需尝试启动程序 nawk 并观察输出。如果它看起来像下面这样，则系统上可用的是较新版本。

```
Usage: nawk [-f programfile | 'program'] [-Ffieldsep] [-v var=value] [files]
```

为了确保脚本使用预期的程序，你应该使用完整路径。每次在脚本中使用程序时都输入 /usr/bin/awk 容易出错。因此，为了创建一个在需要时可以更改的单一条目，你可以使用变量来存储程序的路径和名称。清单 2.11 展示了如何操作。

### LISTING 2.11 The df_check.sh Script Using Variables

```
#!/bin/sh
## $Id: df_check.sh,v 1.1 2004/08/03 10:25:34 erikk Exp erikk $
###########################################################
#
#       file:            df_check.sh
#       purpose:         script to monitor the status
#                        of mounted volumes
#       author:          Erik Keller
#
#     parameters:
#
########################################

# Variables
DF="/usr/bin/df"
GREP="/usr/bin/grep"
AWK="/usr/bin/awk"

$DF -h | $GREP % | $AWK '$5 >= 70 {print $6":", $5}'
# EOF
"df_check.sh" 23 lines, 451 characters

erikk@unixhost$ ./df_check.sh
/ : 73%
/var : 78%
erikk@unixhost$ ci -l df_check.sh
RCS/df_check.sh,v <--  df_check.sh
new revision: 1.2; previous revision: 1.1
enter log message, terminated with single '.' or end of file:
>> added variables for executables
>> 'D
done
```

如清单 2.11 所示，所有使用程序的变量都已创建。在创建变量时，你可能会遇到一些障碍。首先，请注意，在定义变量时不使用 $ 字符——仅在访问内容时使用。其次，如果你在定义时错误地在 = 周围使用了空格，就会遇到另一个障碍。如果有空格，变量将不包含任何值（作者的老师常说“使用空格来创建空白变量”）。测试后，程序再次签入版本控制以记录对其所做的更改。关于日志消息，请尽可能详细地描述。当以后尝试弄清更改了什么以及为什么时，你会感激这一点。要列出现有版本，你可以使用命令 rlog，如清单 2.12 所示。

### LISTING 2.12 Using rlog to List the Existing Versions

```
erikk@unixhost:$ rlog df_check.sh
RCS file: RCS/df_check.sh,v
Working file: df_check.sh
head: 1.2
branch:
locks: strict
  erikk: 1.2
access list:
symbolic names:
keyword substitution: kv
total revisions: 2;  selected revisions: 2
description: check df output for volumes filled > 70%
filtering complete
-----------------------------
revision 1.2  locked by: erikk;
date: 2004/08/03 10:29:54;  author: erikk;  state: Exp;  lines: +7 -2
added variables for executables
-----------------------------
revision 1.1
date: 2004/08/02 15:00:15;  author: erikk;  state: Exp;
Initial revision
==================================================================
=====
erikk@unixhost:>
```

rlog 在不使用任何选项的情况下显示查询文件的修订历史以及用于维护修订的数据和设置。修订按“新”到“旧”的顺序列出，包括谁签入了修订以及何时签入。这里有趣的部分是日志消息。最新修订版 1.2 由 erikk 签入，日志条目（希望）解释了更改了什么以及为什么。这些条目的详细程度取决于注释的作者：甚至可以将其留空。出于实际原因，日志条目应使你能够理解发生了什么——确保你能一目了然地抓住要点。

如果允许不止一个人修改脚本，或者只是对最后一次更改感兴趣，可以使用选项 -r 来使用 rlog。清单 2.13 描述了该过程。

### LISTING 2.13 Displaying the Last Modification Using rlog

```
erikk@unixhost:> rlog -r df_check.sh
RCS file: RCS/df_check.sh,v
Working file: df_check.sh
head: 1.2
branch:
locks: strict
  erikk: 1.2
access list:
```
