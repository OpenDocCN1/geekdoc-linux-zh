

out about the open ports on your systems or to render the services on your systems useless. This is called a DOS attack (pun intended), spelled out denial-of-service.

如果网络内部启用了 IDS 系统（有关入侵检测系统的更多内容请参见第 7 章），那么此类尝试不应被忽视。但除表明正在进行攻击之外，SYN 状态连接的增长也可能意味着您网络中连接了一个故障设备，从而减慢已建立的连接。正确使用基线统计数据可以让您可视化这些变化（对于 TIME_WAIT 状态的连接同样适用）并据此做出反应。因此，监控这些计数器不仅是为了防御自身，也是为了获知网络行为的变化，从而让您对网络状态做出假设。

清单 3.13 演示了用于记录处于上述 SYN 状态的连接数量的脚本。

## LISTING 3.13 Recording the Number of Connections Regarding the SYN State

```
#!/usr/bin/perl
# $Id: base_syn.pl,v 1.1 2004/08/24 10:08:50 erikk Exp erikk $
##################################################
#
#    file:          base_syn.pl
#
#    purpose:       count number of network
#                   connections in SYN state
#
#    author:        Erik Keller
#
#    parameters:    -4   counts inet4
#                   -6   counts inet6
#                   -i   incoming connections
#                   -o   outgoing connections
#                   none counts all
#
##################################################

use Getopt::Std;

# Variables
# path and files !!!!! change for every system
$varpath="/export/home/users/erikk/work/baselines/var";
$thelogfile="base_syn.log";
```

```
# connection counter
$syn_conns = 0;

# check for options on cmdline
# netstat options work on Solaris and OS/X
# Linux needs -A <family>, check man-page
getopt('');
if($opt_4)
{
    $netstatcmd = "netstat -f inet";
}
elsif($opt_6)
{
    $netstatcmd = "netstat -f inet6";
}
else
{
    $netstatcmd = "netstat";
}
# check if all, incoming or outgoing
if($opt_i)
{
    # incoming
    $nstate = "SYN_RECEIVED";
}
elsif($opt_o)
{
    # outgoing
    $nstate = "SYN_SENT";
}
else
{
    $nstate = "SYN";
}

# open the input stream from netstat
open(MY_NETSTAT, "$netstatcmd |") or die "$0: couldn't run: $!";
while(<MY_NETSTAT>)
{
    chop;
    if(/$nstate/)
    {
        $syn_conns++;
    }
}
```

```
}

close(MY_NETSTAT);

# write to file
open(MY_LOG,">>$varpath/$thelogfile")
    or die "$0: couldn't open log file: $!";
print MY_LOG "$syn_conns\n";

close(MY_LOG);

# EOF
```

该脚本能够在需要时仅记录传入（选项 -i）或传出（选项 -o）连接的数量。在正常操作期间，不应有大于零的值。

## 3.1.11 Creating the Graphs

日志文件中记录的数字用途有限。巨大的偏差可能会变得可见，但只有当偏差足够大时才行；几乎不可能发现演变趋势。要可视化由 sar 收集的数据，您可以使用程序 sag，但该程序远非用户友好；有时需要在使用特殊 Tektronix 仿真模式的 x-term 中运行它。这里的另一个问题是它无法用于可视化其他脚本记录的数据。

考虑到这一点，剩下两个选择：要么您使用电子表格程序（如 OpenOffice Calc 或 MS Excel 等），能够将数字列转换为有意义的图形，要么使用程序 gnuplot。gnuplot 的缺点——同样适用于 OpenOffice Calc——是除了 GNU-Linux 和 Solaris 之外，该程序需要先获取并安装（要为其他 *NIX 品牌获取 gnuplot，您可以使用本书附录 C 中的 Internet 地址）。该程序通常以二进制形式提供，可直接安装使用；无需先编译。

没有必要真正解释电子表格程序的使用，但关于 gnuplot 有几条说明是合适的。该程序是自由软件；它可在几乎所有可用的操作系统上运行，并使您能够绘制函数以及——对本任务更有趣的是——数据集。该名称与 GNU 毫无关系；事实上，正确发音时名称应听起来像“newplot”。如果您对该程序的历史感兴趣，那么 http://www.gnuplot.info/faq/faq.html 是了解该程序诞生过程的去处。

在系统上安装程序后，可以通过在命令行执行 gnuplot 来启动它。清单 3.14 显示了结果。

