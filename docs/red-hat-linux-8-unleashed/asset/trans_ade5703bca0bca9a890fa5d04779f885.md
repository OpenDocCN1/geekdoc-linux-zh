
注意
默认情况下，Red Hat Linux 使用系统 `/etc/crontab.daily` 目录中的 logwatch 监控命令（实际上是一个 Perl 脚本）在每天 04:02（凌晨 4:02）生成各种报告。通过编辑 `/etc/log.d/logwatch.conf` 文件可以配置 logwatch。包含其他系统监控工具，例如 tripwire。可以通过编辑 `/etc/syslog.conf` 来控制系统日志。

你可以通过手动运行该脚本并向系统日志 `/var/log/messages` 提供一个关键字和路径来测试该脚本：

```bash
# greplog failure /var/log/messages
```

注意，你的系统应该运行 `syslogd` 守护进程。如果系统发生任何登录失败，root 操作员可能会收到一封类似这样的邮件：

```
Date: Tue, 27 Aug 2002 17:22:53 -0400
From: root <root@shuttle.home.org>
To: root@shuttle.home.org
Subject: failure
```

```
================ SYSTEM MONITOR LOG ================
Linux shuttle.home.org 2.4.18-3 #1 Apr 18 07:31:07 EDT i2686 unknown
Log report for shuttle.home.org on Tue 27 Aug 2002 05:22:53 PM EDT
======================================================
```

```
Search for failure starting 05:22:53 PM
```

```
Aug 27 15:51:54 shuttle su(pam_unix)[8127]: authentication failure;
logname=bball uid=500 eid=0 tty= user=bball rhost= user=root
```

```
End of failure.log.82702 at 05:22:53 PM
```

为了进一步实现该过程，你可以在另一个脚本中包含该脚本的命令行，以生成一系列搜索和报告。

# 内置变量

内置变量是为 Linux shell 提供的特殊变量，用于在 shell 程序中进行决策。你不能在 shell 程序中修改这些变量的值。

# 特殊字符

这些变量中的：

- $#—传递给 shell 程序的的位置参数数量
- $?—在 shell 程序中执行的上一个命令或 shell 程序的完成代码（返回值）
- $0—shell 程序的名称
- $*—调用 shell 程序时传递的所有参数的单个字符串

为了展示这些内置变量的用法，这里有一个名为 `mypgm2` 的示例程序：

```bash
#!/bin/sh
# my test program
echo "Number of parameters is $#"
echo "Program name as a single string $*"
echo "Parameters as a single string $*"
```

如果你在 pdksh 命令行中按如下方式执行 `mypgm2`：

```bash
$ bash mypgm2 Sanjiv Guha
```

你将获得以下结果：

Number of parameters is 2
Program name is mypgm2
Parameters as a single string is Sanjiv Guha

# 特殊字符

某些字符对 Linux shell 有特殊含义；这些字符代表命令、指定周围文本的特定用途或提供搜索参数。特殊字符通过将这些复杂的含义整合到简单的字符中，提供了一种简便的方法。表 22.2 显示了部分特殊字符。

# 表 22.2 特殊字符

| 字符 | 解释 |
|---|---|
| $ | 表示 shell 变量名的开始 |
| | | 将标准输出管道到下一个命令 |
| # | 开始注释 |
| & | 在后台执行进程 |
| ? | 匹配一个字符 |
| * | 匹配一个或多个字符 |
| > | 输出重定向运算符 |
| < | 输入重定向运算符 |

# 表 22.2 续

| 字符 | 解释 |
| --- | --- |
| >> | 命令替换（反引号或反引号——大多数键盘上 Tab 键上方的键） |
| << | 输出重定向运算符（追加到文件） |
| [ | 等待直到输入结束字符串（HERE 运算符） |
| ] | 字符范围 |
| [a-z] | 从 a 到 z 的所有字符 |
| [a,z] or [az] | 字符 a 或 z |
| Space | 单词之间的分隔符 |

在创建 shell 脚本时，特殊字符非常有用，但如果你不小心将特殊字符作为变量名或字符串的一部分，你的程序将将会异常。正如你在本节后续部分所学到的，如果你在字符串中的特殊字符前面加上转义字符（\ 或反斜杠），就可以指示它没有被当作特殊字符使用，程序也不应将其视为。

有几个字符值得特别注意。它们是双引号（"）、单引号（'）、反斜杠（\）和反引号（``）——将在后续章节中进行讨论。

# 使用双引号解析包含嵌入空格字符串中的变量

如果字符串包含嵌入空格，你可以将字符串包含在双引号（"）中，这样 shell 将整个字符串解释为一个实体，而不是多个。

例如，如果你在 shell 程序中如下将 `abc def`（abc 后面跟一个空格，然后是 def）的值赋值给变量 `x`，你会得到错误，因为 shell 会尝试将 `def` 执行一个独立的命令。
