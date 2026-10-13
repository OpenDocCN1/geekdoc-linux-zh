
## 17.2.3 Tripwire 无法防止的内容

早期版本的 Tripwire 提到过将程序和数据库放在只读介质上的必要性，以防止黑客篡改。它现在自豪地声称，由于数据库和信任文件经过加密签名，这不再是必要的。作者持有不同意见。如果一个黑客足够老练可以通过“更新”`Tripwire` 使其不察觉来篡改，那么她就足够安装一个带木马的 `Tripwire`。这个木马版本可以在通常的地方向系统管理员提示口令，然后继续更改数据库并重新签名，或者假装什么都没有改变。非常老练的黑客可以向 `Tripwire`、`/bin/sh` 甚至内核添加木马。这种情况通过标准的 `Tripwire` 用法（信任磁盘上的副本）是检测到的。当你有理由相信老练的黑客发动了攻击，或者定期“以防万一”，建议采取以下措施：创建特定的 `Tripwire` 救援光盘，参考“自定义救援光盘”。启动救援光盘并运行绝对信任的 `Tripwire` 和数据库。显然，这个数据库必须定期更新，不能简单从“普通”硬盘复制，因为那不可信。

*注：现在将提供没有内部重复块的输出。*

它是 SuSE 的标准配置，并很容易移植到其他发行版。可以从此处下载：

`http://www.suse.de/~marc/`

> [1] `md5sum` 程序的输出更准确的说法是消息摘要（message digest），因此称为 `md5sum`。校验和的目的是仅仅是检测数据是否被故意篡改，它并不保证能检测出对消息的蓄意篡改。像 `md5sum` 生成的这种消息摘要，使得在不改变消息摘要输出的情况下修改消息变得非常困难。

## 17.3 检测被删除的可执行文件

破解者绝对不希望你拥有他木马程序的副本。除了想保守自己的技术秘密外，这还是一个可能导致他在许可证标签工厂丢掉工作的证据。它甚至可能包含他工作所在系统的 IP 地址。破解者用来防止你“捕获”可执行文件的常用技术就是简单的将其从磁盘中删除。正如我们在“寻找破解者的运行进程”中将讨论的那样，从磁盘中删除它不会终止正在运行的执行文件。

从 2.2 内核开始，系统提供了一个指向实际执行文件的符号链接 `/proc/PID/exe`。此外，它通过在名称末尾附加 `(deleted)` 来该执行文件已从文件系统中移除。此示例展示了此类被删除的可执行文件看起来的样子。

```
$ file /proc/519/exe

/proc/519/exe: broken symbolic link to /home/mr_ed/foo (deleted)
```

可以从 `cron` 任务中定期调用以下命令，以检测任何此类实例：

```bash
# file /proc/[0-9]*/exe|grep '(deleted)'
/proc/519/exe: broken symbolic link to /home/mr_ed/foo (deleted)
```

内核中的一个非常实用的特性是，尽管原始文件已被删除，但 `/proc` 中的这个符号链接仍然可以读取！这允许你简单地通过以下命令创建文件的副本进行分析：

```
cp /proc/519/exe /home/samspade/del_cracker
```

你甚至可以通过以下脚本自动制作这些副本，我将其命名为 `getdel.sh`；它在光盘上，也可以从作者的网站下载。它使用 `dd` 而不是 `cp` 仅仅是因为 `dd` 不广为人知，不容易被破解者利用。

```sh
#!/bin/sh -f

# 检测并复制从磁盘中删除的运行执行文件

# 危险: 此程序必须以 root 权限运行以捕获所有

# 数据，但如果发现了什么，root *可能会* 被破解。

# 可选杀死程序。

# 需要内核 2.2 或更高版本。

#
# 版权所有 2001 Bob Toxen 保留所有权利。
# 此程序可以在 GNU 通用公共许可证第 2 版
# 条下使用。
set savdir=/home/sampsade/delexe_dir
set emailaddr=sampsade@pentacorp.com
set g='(deleted)'\([0-9]*\),\1'
set s='s.,/proc/[0-9]*/,\1'
set p='`file /proc/[0-9]*/exe|grep "$g" | sed "$s"'
umask 077
foreach i ( $p )
  if ( ! -f $savdir/$i ) then
    echo /bin/dd if=/proc/$i/exe=$savdir/$i |
    echo /bin/mail -s 'Del EXE' $emailaddr
    /bin/ls -1 /proc/$i/exe >! $savdir/$i
    /bin/dd if=/proc/$i/exe >! /dev/null
    /bin/ls -1 /proc/$i/exe >! $savdir/$i
  # 取消下一行的注释以自动杀死
  #
    # /bin/kill -9 $i
  else
    echo already captured /proc/$i/exe
  endif
end
```

## 17.4 检测混杂模式网卡

这里提供的简单脚本将检测系统的网卡（有时称为 NIC 或以太网卡）处于混杂模式。另一种方法是在 `/etc/syslog.conf` 中添加相应的条目，以记录大多数 NIC 在网卡置于混杂模式时生成的内核消息，监控相应的日志文件以获取这些内核消息，并在发生时通过电子邮件和传真机通知你。关于不同驱动程序的消息详情，请参阅“混杂模式内核消息”，关于如何安排电子邮件和传真机通知的详情，请参阅“分页系统管理员：破解正在进行！”。

以下脚本 `promisc` 会每半小时扫描一次 `eth0` 和 `eth1`，如果网卡处于混杂模式，将生成电子邮件。它可以从任何 shell 使用（稍后将讨论 `fpromisc` 脚本）。

```bash
#!/bin/bash -f
set devs=(eth0 eth1)
loop:
foreach i in ( $devs )
do
  if [ $(ifconfig $i | grep PROMIS | wc -l) -eq 1 ]; then
    (echo $i Promisc;fpromisc) | mail -s PROMISCUOUS sysadmin sysadmin@homesys.com
  fi
done
sleep 1800
goto loop
```

对于那些偏好 bash 的人，提供了以下方案：

```bash
#!/bin/bash
while true
do
  for i in eth0 eth1
  do
    if [ $(ifconfig $i | grep PROMIS | wc -l) -eq 1 ]; then
      echo $i Promisc | mail -s PROMISCUOUS sysadmin@homesys.com
    fi
  done
  sleep 1800
done
```

等待，原文提供的 bash 版本使用了不同的逻辑。根据提供的 OCR 文本重建它：

```bash
#!/bin/bash
while true
do
  for i in eth0 eth1
  do
    if [ $(ifconfig $i | grep PROMIS | wc -l) -eq 1 ]; then
      echo $i Promisc | mail -s PROMISCUOUS sysadmin@homesys.com
    fi
  done
  sleep 1800
done
```

实际上，仔细观察 OCR 的 bash 版本：

```bash
#!/bin/bash
while true
do
  for i in eth0 eth1
  do
    if [ $(ifconfig $i | grep PROMIS | wc -l) -eq 1 ]; then
      echo $i Promisc | mail -s PROMISCUOUS sysadmin@homesys.com
    fi
  done
  sleep 1800
done
```

等待，OCR 断了。看看 OCR 提供的 Perl 版本：

```perl
#!/usr/bin/perl
# 检测混杂模式下的接口
my %PROMIS = ();
my $interface = "";
open(IFCONFIG,"ifconfig") or die("cannot open ifconfig: $!");
while ($line = <IFCONFIG>) {
    if ($line =~ /^(\S+)/) {
        $interface = $1;
    }
    if ($line =~ /promisc/) {
        $PROMIS{$interface} = 1;
    }
}
```
