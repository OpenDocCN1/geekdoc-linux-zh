

在危机期间。有一条原则应适用于所有关于计算机管理的脚本和程序，即 KISS——保持简单！最优雅的面向对象 Perl 脚本如果需要大约五分钟才能弄清楚启动后会做什么，那就完全无用。

## 3.1.5 监控磁盘空间

每个 *NIX 系统都自带 df 和 du 命令。它们用于显示每个分区已使用空间的百分比（df），以及在其他用途中查找目录的当前大小（du）。

清单 3.2 中的脚本会定期记录文件系统的可用空间并存储数据，以便日后分析。

### LISTING 3.2 Registering Free Hard Disk Space

```
#!/usr/bin/perl
# $Id$
######################################
#
#    file:          base_df.pl
#
#    purpose:       display filesystems and
#                   used space
#
#    author:        Erik Keller
#
#    parameters:    none
#
######################################

#Variables
$varpath="/export/home/users/erikk/work/baselines/var*";

# get output of df -k
open(MY_DF, "df -k |") or die "$0: couldn't get df: $!";
while(<MY_DF>)
{
    chop;
    if(/\/dev\//)
    {
        @myrec = split(" ", $_);
        $free = int($myrec[3]/1024);
        #print "$myrec[5] $myrec[4] $free MB free\n";
        $fsname = $myrec[5];
```

```
$fname =~ s!/\!/\!/g;
$logname = "df_".$fname.".log";
open(MY_LOG, ">>\$varpath/$logname")
    or die "problem opening file: $!";
print MY_LOG "$free\n";
close(MY_LOG);
}

close(MY_DF);

# EOF
```

该脚本分析 df 的输出并提取在设备上找到的所有文件系统。在 $varpath 指向的目录中为找到的每个文件系统创建一个文件，并以文件系统所在挂载点命名，并将可用空间量写入该文件。文件名按以下方案构造：/export/home 变为 _export_home，并且字符串 df_ 位于名称之前，因为 *NIX 中不允许文件名以 / 开头。如果还有另一块硬盘挂载，所有在其上找到的文件系统也将被评估。

文件系统开始填满这一事实并不一定能让你确定原因或该行为的来源。需要一个脚本来记录单个目录或目录树的更改；清单 3.3 显示了此类脚本的一种可能方法。

### LISTING 3.3 Script to Monitor Directories

```
#!/usr/bin/perl
# $Id: dirwatch.pl,v 1.4 2004/08/23 15:56:25 erikk Exp erikk $
# ############################################
#
#    file:        dirwatch.pl
#
#    purpose:     display size of subdirectories
#                 script ignores directories
#                 if the user doesn’t have the
#                 rights to scan them, this is
#                 intentional
#
#    author:      Erik Keller
#
#    parameters:  -d <directory to scan>
#                 -k use KB instead of MB
```

```
#
###################################
use Getopt::Std;
# Variables
$varpath="/export/home/users/erikk/work/baselines/var/dirwatch";
# get directory to watch
getopt('d');
if($opt_d eq '')
{
    usage();
}
open(MY_DIRS, " du -sk $opt_d/* |")
    or die "$0: du failed: $!";
while(<MY_DIRS>)
{
    chop;
    @myrec = split(" ", $_);
    $dirname = "dw_" . $myrec[1];
    $dirname =~ s/\/\//g;
    if($opt_k)
    {
        # use KB
        $mysize = $myrec[0];
    }
    else
    {
        # use MB
        $mysize = int($myrec[0]/1024);
    }
    open(MY_LOG, ">>$varpath/$dirname")
        or die "$0: error using file: $!";
    print MY_LOG "$mysize\n";
    close(MY_LOG);
}
close(MY_DIRS);
sub usage()
{
```

```
print "\nScans the subdirectories and reports the\n";
print "amount of space used by them.\n";
print "Directories the executing user has no rights\n";
print "to scan are ignored.\n\n";
print "Usage:\n";
print "$0 -d <dirname>\n\n";
exit(1);
}
# EOF
```

将单位切换为 KB 的功能在可用的硬盘空间方面似乎已过时，但如果以 MB 为单位测量大小，微小的变化需要很长时间才会显现出来。同样，使用 df 和 du 中的 -h 选项：为了获得总体概览，使用 MB 和 GB 就足够了；跟踪细微变化需要更精细的测量单位，从而让你更仔细地观察正在发生的事情。请随意直接在代码中输入包含要扫描目录的主目录。为此，你可以简单地更改提供给 du -sk 的参数或创建一个变量来保存路径。

由于该脚本可能创建大量日志文件，将其输出存储到基线层次结构中的通用 var 目录并不是一个明智的选择；应使用子目录代替。如脚本注释中已提到的，在当前用户上下文中无法访问的目录将被忽略。尽管如此，该脚本应仅对超级用户可访问，因为它可用于轻松映射目录，从而显示机密信息。该脚本也可用于进行比较（按大小），在应用更新和补丁或安装软件之前和之后。你只需记住将这些扫描存储在另一个目录中；用于保存常规扫描的目录可能会变得非常杂乱，从而使其在日常使用中不那么实用。

## 3.1.6 监控 CPU

SMP 系统上 CPU 或多个 CPU 的负载是机器当前负载程度的明确指标——还是吗？这个问题没有你想象的那么明确，但至少记录该值可以让你对系统负载情况有所了解。

获取此数据的最简单方法是使用系统活动报告器 sar。该软件包在大多数 NIX 系统上可用，但不一定默认安装。更常见的是，它“隐藏”在记账软件包或 sysstat 软件包中；在安装该软件包后通常可以获得 sar。输出数据的命令是 sar。它默认显示 CPU 负载，按用户、系统、空闲划分，并且除 GNU-Linux 外，还包括 wio（等待 I/O）。如果你通过 crontab 机制定期启动 sar，则可以获得

