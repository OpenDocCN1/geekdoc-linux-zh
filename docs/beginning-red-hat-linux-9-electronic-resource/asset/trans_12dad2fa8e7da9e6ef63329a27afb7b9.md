
## 应用 3：我的系统负载是多少？

在典型的单用户环境中，如果系统管理员也是唯一的用户，我们不必过多关注操作系统的管理、监控和优化。然而，多用户系统的情况则截然不同：随着依赖系统良好运行的人数增加，风险也随之升高。我们可以使用许多诊断应用程序来监控系统的状态。例如，`uptime` 程序可以返回许多有用的信息，包括系统已正常运行多久、当前登录的用户数量以及过去 1、5 和 15 分钟的负载平均值：

```
2:06pm  up 30 days, 21:56, 7 users, load average: 1.41, 0.93, 0.26
```

如果你想要优化系统，通常需要在一段时间内跟踪系统活动和指标。这些活动可以包括登录用户的数量、他们正在运行的应用程序、平均系统负载以及消耗的内存量。这允许你分析数据并查找特定的模式。例如，你可能会发现每周一早晨在每周工程会议之前，系统负载都会出现大幅激增。然后，你可以确定如何最好地处理这个问题：不要在周一早晨运行其他任务，增加更多 RAM，或升级处理器。

本着这一理念，我们将创建一个应用程序来存档系统负载平均值和活跃用户数量。然而，为了使任何数据分析有效，我们需要拥有足够多的数据来捕捉各种状况。做到这一点的最佳方法是设置一个 cron 作业，以自动在周一至周五每小时运行此应用程序，如下所示：

```
00 * * * 1-5 /home/nutt/uptime_monitor.pl /home/nutt/uptime.log
```

尽管该应用程序只有十行代码，但你仍然会学到足够的先进 Perl 开发技术，使其物有所值。更具体地说，你将学习如何调用外部程序、获取其输出、从中提取特定信息并将格式化输出写入日志文件。由于 Linux 中存在许多有用的实用程序和程序，能够在 Perl 内部与这些工具交互的能力将使你能够开发一些非常有趣的应用程序。

现在，让我们看看代码。

```perl
#!/usr/bin/perl

###
##   uptime_monitor.pl: archive system load averages to file
##-

use strict;                                     ## Enable "strict" pragma

my ($file, $uptime, $users, $load1, $load2, $load3);
$file = $ARGV[0] || '/var/log/uptime.log'; ## Path to log file
$uptime = `/usr/bin/uptime`;
## Store output from uptime

###++
### Parse the output of the uptime command and store the numbers of
### users and the three system load averages into: $users, $load1,
### $load2 and $load3.
###--

$uptime =~ /(\d+) +user.+?(\d.+?), +(.+?), +(.+?)/;
$users = $1;
$load1 = $2;
$load2 = $3;
$load3 = $4;

###++
### We can also write the above like this:
###
###
$uptime =~ /(\d+) +user.+?(\d.+?), +(.+?), +(.+?)/;
### ($users, $load1, $load2, $load3) = ($1, $2, $3, $4);
###
### or even:
###
###
($users, $load1, $load2, $load3)
### = $uptime =~ /(\d+) +user.+?(\d.+?), +(.+?), +(.+?)/;
###--

###++
### Store the data in a log file; open modes:
###
### >> = append, > = write, < (or nothing) = read
###--

open (FILE, ">>$file") || die "Cannot append uptime data to $file: $!\n";
print FILE join (':', time, $users, $load1, $load2, $load3), "\n";
close (FILE);

exit (0);
```

在开始讨论代码之前，有一点需要注意。我们的应用程序接受一个命令行参数，并使用其值来确定在哪里存档负载平均值数据。这使我们能够不修改任何代码就将数据存档到不同的文件中。如果你对上述 crontab 条目中 `/home/nutt/uptime.log` 文件的重要性感到好奇，现在你知道了；它指的是日志文件。

## 获取命令行参数

用户可以通过命令行向任何 Perl 应用程序指定参数和信息，Perl 会通过特殊的 `@ARGV` 数组向我们提供它们。我们不一定需要在应用程序中使用这些参数，但它们在那里以备我们需要时使用。下面是一个简单的程序，说明命令行参数是如何处理的：

```perl
#!/usr/bin/perl

###
##  print_args.pl: display all command-line arguments
##-

use strict;

for (my $loop=0; $loop <= $#ARGV; $loop++) {  ##  $#ARGV returns the
                                               ##  last index of the
print "\$ARGV[$loop] = $ARGV[$loop]\n";         ##  array
}

exit (0);
```

你看到的是 `for` 循环在起作用。当你确切知道希望循环执行多少次时，应该使用这种结构。这与 `while` 循环非常不同，在使用 `while` 循环时，你可能不知道它应该运行多少次；你所知道的只是，一旦循环满足某些特定条件，它就应该停止。我们逐个遍历 `@ARGV` 数组，一次处理一个元素，显示其值。继续运行该程序，如下所示：

```
$ perl print_args.pl how are you this is a test
$ARGV[0] = how
$ARGV[1] = are
$ARGV[2] = you
$ARGV[3] = this
$ARGV[4] = is
$ARGV[5] = a
$ARGV[6] = test
```

我们可以像处理其他数组一样处理 `@ARGV` 数组，通过指定其索引来访问特定元素。回顾我们的主应用程序，我们获取第一个命令行参数，`@ARGV[0]`，并继续使用该值：

```
$file = $ARGV[0] || '/var/log/uptime.log';
```

你认为我们在尝试做什么？当然，我们之前见过这种类型的结构。如果你记得，这个巧妙的一行语句等同于下面的 `if`-`then` 块：

```perl
if ($ARGV[0]) {
    $file = $ARGV[0];
} else {
    $file = '/var/log/uptime.log';
}
```

我们使用从命令行传递的值作为日志文件的路径，将其存储在 `$file` 中，但前提是它已定义且具有真值。否则，我们将使用 `/var/log/uptime.log` 作为默认日志文件。我们在这章开头讨论过 Perl 的灵活性。好吧，这只是一个简单的例子来说明这一点。如果你不太习惯使用单行技术，你始终可以使用上述较长但更清晰的代码组。而且，如果你更冒险一些，也可以使用以下代码：

```perl
$file = ($ARGV[0]) ? $ARGV[0] : '/var/log/uptime.log';
```

我们刚刚看到了三种执行完全相同任务的不同技术。Perl 并不强制你使用一种方法而不是另一种；你可以自由使用你感觉舒适的任何一种方法。

## 调用 uptime 命令

我们现在可以调用 `uptime` 系统命令来获取我们所需的负载平均值数据。当你看到从 Perl 内部与外部应用程序通信有多简单时，你会非常惊讶。你准备好了吗？我们只需要将要执行的命令或应用程序的路径（连同任何必要的命令行参数）包含在一对反引号中。然后 Perl 将生成一个 shell 来执行该应用程序并将其输出返回给我们。在这种情况下，我们将该输出存储在 `$uptime` 变量中。难道不是很简单吗？

我们即将进行一次长途绕行，以更好地理解与外部应用程序通信的复杂过程。如果你现在对了解这些技术不感兴趣，你可以安全地跳转到“回到我们的程序...”部分，并在稍后返回此内容。

## 管道

反引号方法非常容易使用且非常方便。然而，它只应在你知道被调用应用程序产生的输出较小时使用。想象一下，如果一个应用程序产生数兆字节和数兆字节的输出会怎样？Perl 则必须将全部这些信息存储在内存中，这可能会造成相当大的问题。因此，Perl 通过管道为我们提供了另一种与应用程序通信的替代方案。例如，假设你想检索当前登录用户的列表，这里是该怎么做：

```perl
#!/usr/bin/perl

##++
##    current_users.pl: display list of current users
##--
```
