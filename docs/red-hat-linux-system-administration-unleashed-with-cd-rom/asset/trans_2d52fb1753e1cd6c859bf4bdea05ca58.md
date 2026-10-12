
比其他更受欢迎。本节探讨了这个问题，并通过提供监控方法来帮助减轻任务负担。它还探讨了如何使用配额来管理文件系统，并确保用户不会通过填满文件系统来滥用其权限。

## 监控空间使用情况

监控空间使用的一种简单方法是使用定期运行 df 并在空间低于用户定义阈值时通知你的脚本。这些脚本可以非常简单，也可能非常复杂，正如以下示例所示。列表 7.2 包含我用于监控我维护的多个系统磁盘空间使用情况的脚本。该脚本用 Perl 编写，旨在从 cron 作业每小时运行一次，或根据需要更频繁地运行。它使用随 Red Hat Linux 提供或可从本地 CPAN 镜像获取的模块。

### 列表 7.2 checkspace.pl
```
#!/usr/bin/perl
#
# $Id: 755907.txt,v 1.5 1999/09/17 11:43:34 tschenk Exp $
#
# checkspace.pl - perl script to check for filesystems that are nearing 100%
#                 utilization
#
use Sys::Hostname;
use Getopt::Std;
use POSIX;
use strict;
#use vars qw($SystemLevels $ENotify $PNotify);

########
# MAIN
########

# -*-perl-*-
# This hash contains the notification levels and is keyed by the hostname
# and filesystem to check.  The filesystems with default as the hostname
# are checked on every host that this script runs on.
my %SystemLevels = (
    'nomad:/v/v10'  =>  'b:94:97:99',
    'nomad:/v/v12'  =>  'b:94:97:99',
    'quicksilver:/usr/local'  =>  'b:94:97:99',
    'quicksilver:/home'  =>  'b:94:97:99',
    'wizard:/opt' => 'i:94:97:99',
    'wizard:/usr/local' => 'i:94:97:99',
);

# The list of people to notify by e-mail at each level, separated by colons.
# There should be one entry here for each entry in the SystemLevels hash
# with a matching key.
my %ENotify = (
'nomad:/v/v10' => 'tschenk:siteops:siteops',
'nomad:/v/v12' => 'tschenk:siteops:siteops',
'quicksilver:/usr/local' => 'tschenk:siteops:siteops',
'quicksilver:/home' => 'tschenk:siteops:siteops',
'wizard:/opt' => 'tschenk:siteops:siteops',
'wizard:/usr/local' => 'tschenk:siteops:siteops',
);

# The list of people to notify by pager at each level, separated by colons.
# There should be one entry here for each entry in the SystemLevels hash
# with a matching key.
my %PNotify = (
'nomad:/v/v10' => 'tschenk-page:meb-page:tschenk-page,bmcfarla-page',
'nomad:/v/v12' => 'tschenk-page:meb-page:tschenk-page,bmcfarla-page',
'quicksilver:/usr/local' => 'tschenk-page:meb-page:tschenk-page,bmcfarla-page',
'quicksilver:/home' => 'tschenk-page:meb-page:tschenk-page,bmcfarla-page',
'wizard:/opt' => 'tschenk-page:meb-page:tschenk-page,bmcfarla-page',
'wizard:/usr/local' => 'tschenk-page:meb-page:tschenk-page,bmcfarla-page',
);

# Parse the command line options
my $options = &parse_cmd_line;

if (defined($options{Error})) {
    print STDERR "Options{Error}\n";
    &print_usage;
    exit(1);
}

# Perform the checks
my $hostname = hostname();
$hostname =~ s/\.alchemy.net//;

foreach my $value (keys(%SystemLevels)) {
    my ($host, $filesystem) = split(/:/, $value);

    if (($host eq $hostname) or ($host eq 'default')) {
        &checkspace($hostname, $filesystem, $SystemLevels{$value},
            $ENotify{$value}, $PNotify{$value});
    }
}

# Exit
exit(0);

#############
# SUBROUTINES
#############

sub print_usage {
    my $USAGE = "Usage: $0 [options]
where options are:
    -n    Run the script, but don't actually send notifications
    -v    Be verbose in your reporting
    -h    Print this usage statement\n";

    print STDERR $USAGE;
}

sub parse_cmd_line {
    my %opts;

    getopts('nvh');

    $opts{Dryrun} = (defined($::opt_n) ? $::opt_n : 0);
    $opts{Verbose} = (defined($::opt_v) ? $::opt_v : 0);

    if ((scalar(@ARGV) > 0) || (defined($::opt_h))) {
        &print_usage;
        exit(1);
    }

    return %opts;
}

sub checkspace {
    my $host = shift;
    my $fs = shift;
    my $levelstr = shift;
    my $emailstr = shift;
    my $pagestr = shift;

    my @levels = split(/:/, $levelstr);
    my $checktype = undef;
    my @email = split(/:/, $emailstr);
    my @pager = split(/:/, $pagestr);

    $levels[0] == 'i' ? $checktype = '-i' : $checktype = undef;
    shift @levels;

    my $level;
    for ($level = (scalar(@levels) - 1); $level >= 0; $level--) {
        if ($options{Verbose}) {
            print "Checking space on $fs.\n";
        }
    }

    my $used = `df $checktype $fs | tail -1 | awk '{print $5}' |
 sed -e 's/%//' `;
    chomp $used;
    my $fsname = $fs;
    $fsname =~ tr/:/_/;
    my $lockfile = '/tmp/checkspace_' . $fsname . '_' . $levels[$level]
        . '.lock';

    if (-f $lockfile) {
        if ($used < $levels[$level]) {
            if ($options{Dryrun}) {
                print "Removing lockfile $lockfile.\n";
            } else {
                unlink($lockfile);
            }
        } else {
            last;
        }
    } else {
        if ($used >= $levels[$level]) {
            open(LOCKFILE, ">$lockfile");
            print LOCKFILE $$;
            close(LOCKFILE);
            if ($email[$level] ne "none") {
                &notify_email($hostname,$fs,$level,$used,$email[$level]);
            }
            if ($pager[$level] ne "none") {
                &notify_pager($hostname,$fs,$level,$used,$pager[$level]);
            }
            last;
        }
    }
}

sub notify_email {
    my $host = shift;
    my $fs = shift;
    my $level = shift;
    my $used = shift;
    my $recipients = shift;

    my @subjstr = ("[WARNING]", "[CRITICAL]", "[CRISIS]");

    my $msg = `df $fs`;

    if ($options{Verbose}) {
        print "Sending e-mail notification to $recipients.\n";
    }
    if (! $options{Dryrun}) {
        open(SENDMAIL, "|/usr/sbin/sendmail $recipients");
        print SENDMAIL <<EOF;
Subject: $subjstr[$level] $host:$fs $used% full

Notification from checkspace.pl:

$msg

EOF
        close(SENDMAIL);
    } else {
        print "$msg\n";
    }
}

sub notify_pager {
    my $host = shift;
    my $fs = shift;
    my $level = shift;
    my $used = shift;
    my $recipients = shift;

    my @subjstr = ("[WARNING]", "[CRITICAL]", "[CRISIS]");

    if ($options{Verbose}) {
        print "Sending pager notification to $recipients.\n";
    }
    if (!$options{Dryrun}) {
        open(SENDMAIL, '|/usr/sbin/sendmail $recipients');
        print SENDMAIL <<EOF;
Notification from checkspace.pl: $subjstr[$level] $host:$fs $used% full

EOF
        close(SENDMAIL);
    } else {
        print "$subjstr[$level] $host:$fs $used% full\n";
    }
}
```

该脚本非常灵活，包含基于三个使用级别的两种通知方法，即寻呼和电子邮件。此外，你可以让脚本检查 inode 耗尽而不是磁盘块消耗，并且通过调整配置参数，可以消除其中一种通知方法。

## 本地与共享文件系统

管理磁盘空间的另一个方面是决定在网络上共享哪些文件系统，哪些保留本地。其极端情况是无盘工作站，其中所有文件都物理位于网络服务器上，工作站从软盘或 bootrom 启动。另一极端是独立工作站，它已连接网络，但根本不共享任何文件系统。然而，最常见的情况介于两者之间，其中 /opt、/usr/local 和 /usr/share 等文件系统位于网络文件服务器上并在系统之间共享。

你可能会想知道网络文件系统与管理空间有什么关系。答案是共享文件系统通过减少需要担心磁盘填满或有扩展空间的系统数量，从而降低了管理磁盘空间的行政开销。有关设置共享文件系统资源的信息，请参阅第 15 章“共享资源（打印和文件服务）”。

## 建立文件系统配额

管理服务器磁盘空间的一种方法是使用文件系统配额。大多数用户对配额的想法感到厌恶，因为他们认为这是一种不必要的限制，旨在让他们的生活更困难。另一方面，许多系统管理员认为配额是文件系统管理所必需的一部分。用户的不便是一个小代价，换来的是安心，因为你知道没有一个用户会占用文件系统的所有空间。

在 Linux 下，配额主要有两种类型：用户级配额和组级配额。要在 Linux 系统上使用配额，你必须首先在内核配置中启用对它们的支持，并注意配额仅适用于扩展 2 文件系统类型。因此，在配置内核时，你必须对配额支持问题和扩展 2 文件系统回答“是”。Red Hat Linux 包含利用此内核支持所需的工具，但如果你想自己构建它们或查看是否存在新版本，可以从 ftp.funet.fi 获取最新的配额工具，网址为 ftp://ftp.funet.fi/pub/Linux/PEOPLE/Linus/subsystems/quota/all.tar.gz。该工具集包含五个实用程序，其用途在表 7.10 中描述。

### 表 7.10 配额实用程序

| 工具 | 描述 |
|---|---|
| quotaon | 打开配额核算。 |
| quotaoff | 关闭配额核算。 |
| quotacheck | 扫描文件系统以获取当前磁盘使用情况，并使用最新的使用统计信息更新 quota.user 和 quota.group 文件。 |
| repquota | 生成格式化的磁盘空间使用报告。 |
| edquota | 用于修改用户或组配额的工具。 |

一旦你在内核中启用了配额支持并确保已安装配额工具，现在就可以开始设置配额了。在进入实现细节之前，以下部分回顾了一些在讨论配额时使用的概念，需要理解这些概念才能有效地使用它们。
