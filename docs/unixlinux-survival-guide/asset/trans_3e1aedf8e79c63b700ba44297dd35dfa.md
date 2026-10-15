

始终触手可及，因为在安装包含 sar 的软件包期间，crontab 通常会被修改以实现此目的。如果没有，您可以像往常一样，查看 manpage 以了解如何启用数据的持续收集并微调设置。清单 3.4 显示了将此数据收集到单独日志文件的脚本。

## LISTING 3.4 Creating Log Files from sar Output

```
#!/usr/bin/perl
# $Id: base_cpu.pl,v 1.2 2003/06/03 10:32:54 erikk Exp $
#####################################
#
#    file:        base_cpu.pl
#
#    purpose:     save the current sar values
#                 to files
#
#    author:      Erik Keller
#
#    parameters:  none
#
#####################################

# Variables
$WORKDIR = "/export/home/users/erikk/work/baselines/var";

# create the 4 outfiles for gnuplot
open(SG_USRH, "$WORKDIR/sar_usr.log")
    or die "$0: couldn't create file: $!";
open(SG_SYSH, "$WORKDIR/sar_sys.log")
    or die "$0: couldn't create file: $!";
open(SG_WIOH, "$WORKDIR/sar_wio.log")
    or die "$0: couldn't create file: $!";
open(SG_IDLH, "$WORKDIR/sar_idl.log")
    or die "$0: couldn't create file: $!";

# get the stored values from sar for CPU
open(THE_SAR, "sar |") || die "$0: couldn't run sar: $!";

while(<THE_SAR>)
{
    if (/^[0-9]/)
    {
        @myrec = split(",", $_);
        if($myrec[1] ne "\%usr")
```
```
{
    print SG_USRH "$myrec[1]\n";
    print SG_SYSH "$myrec[2]\n";
    print SG_WIOH "$myrec[3]\n";
    print SG_IDLH "$myrec[4]\n";
}
}

close(THE_SAR);

close(SG_IDLH);
close(SG_WIOH);
close(SG_SYSH);
close(SG_USRH);

# EOF
```

该脚本将用户、系统、等待 I/O 和空闲的值写入四个日志文件。它创建了当前数据的临时快照。对数据的进一步处理在第 3.1.11 节“Creating the Graphs”中进行。

另一个有趣的计数器是运行队列大小，即等待在主内存中执行的进程队列。清单 3.5 演示了如何将此计数器的数据收集到日志文件中。

## LISTING 3.5 Script to Store the rung Size

```
#!/usr/bin/perl
# $Id: base_runq.pl,v 1.1 2004/08/27 03:44:21 erikk Exp erikk $
########################################################
#
#    file:          base_runq.pl
#
#    purpose:       save the current size of the
#                   run-queue to a file
#
#    author:        Erik Keller
#
#    parameters:    none
#
########################################################

# Variables
```
```
#
#   parameters:   -4   counts inet4
#               -6   counts inet6
#               none counts all
#
##################################################

use Getopt::Std;

# Variables
# path and files !!!!! change for every system
$varpath="/export/home/users/erikk/work/baselines/var";
$thelogfile="base_netconns.log";

# connection counter
$active_conns = 0;

# check for options on cmdline
# netstat options work on Solaris and OS/X
# Linux needs -A <family>, check man-page
getopt('4-6');
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

# open the input stream from netstat
open(MY_NETSTAT, "$netstatcmd |") or die "$0: couldn't run: $!";
while(<MY_NETSTAT>)
{
    chop;
    if(/ESTABLISHED/)
    {
        $active_conns++;
    }
}
```
```
close(MY_NETSTAT);

# write to file
open(MY_LOG,">>$varpath/$thelogfile")
    or die "$0: couldn’t open log file: $!";
print MY_LOG "$active_conns\n";

close(MY_LOG);

# EOF
```

在修改路径后，该脚本可立即在 Solaris 和 OS X 上使用。其他 *NIX 变体需要测试以确定 netstat 程序是否知道 -f <Address-Family> 参数。如果脚本不带参数调用，它应该几乎可以在任何地方运行。使用该脚本最简单的方法是通过 crontab。脚本需要调用的频率在很大程度上取决于要检查的系统提供的服务。每 30 分钟一次应该足以对系统上的网络负载有一个大致的了解。如果需要更精细的分辨率，则每 10 分钟运行一次脚本一次。根据要求，您的最后一个选择是手动以所需频率连续启动脚本并检查生成的日志文件。

## 3.1.8 Network Retransmissions

TCP/IP 出于历史原因具有极强的容错性；因此，与网络基础设施相关的问题往往会未被察觉，至少在一段时间内如此。该协议具有自愈能力；这意味着它能够通过避免网络物理结构中的缺陷组件来保持服务运行。其中一种行为的结果最好用以下场景来解释：假设有一个由几个路由器组成的网络。如果其中一个路由器发生故障，则协议会尝试为数据包寻找替代路由，并且故障最初不会被注意到。故障可能会在路由服务的用户开始抱怨连接缓慢或响应时间差时变得明显。

![](img/e121d664a879353483b8ef78e54b87ea_83_0.png)

> *作者曾在一家在世界各地设有分支机构的公司工作。*
> 
> *有一天，重传次数突然开始呈指数级增长。几分钟后电话响了，内部用户开始抱怨响应缓慢。快速运行 tcpdump 显示， supposed to go*

