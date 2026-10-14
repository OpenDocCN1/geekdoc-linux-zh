

然后执行 "swapon -a" 如果你是在添加额外的交换空间。如果你在替换主要的交换空间，则需要重启才能使此更改生效，因为你无法从操作系统中强行夺走一个交换分区。需要注意的是，将交换空间移动到本地磁盘有利于性能并减少对共享总线的 I/O，但它也会使该交换分区更容易受到控制器问题的威胁。如果交换被移动到本地分区并且该路径出现故障，可能会导致系统挂起或崩溃。如果交换分区位于共享磁盘上，只要至少有一个成员仍能访问该磁盘，你就不会遇到此问题。共享总线上拥有交换的另一个好处是，如果该成员崩溃并且由于某种原因无法启动，崩溃转储可以由另一个集群成员处理，并且在原始成员甚至尚未启动之前就可以开始崩溃分析。例如，如果我们知道 dsk6b 是另一个成员的交换分区并且该分区足够大以容纳崩溃转储，我们可以处理转储并创建所需的 vmunix.0 和 vmzcore.0 文件（并且从中创建 crash-data.0 如果我们愿意的话）。

```
# /sbin/savecore -d /dev/disk/dsk6b .
System went down at Thu Jun 27 23:11:13 2002
Saving 23949312 bytes of image in vmzcore.0
```

```
# /usr/bin/crashdc vmunix.0 vmzcore.0 > crash-data.0
```

```
# ls
crash-data.0    vmunix.0    vmzcore.0
```

要查看交换当前是如何配置的，请执行 "swapon -s" 命令：

```
# swapon -s
Swap partition /dev/disk/dsk16b (default swap):
  Allocated space:     211639 pages (1.61GB)
  In-use space:        129 pages ( 0%)
  Free space:          211510 pages ( 99%)

Swap partition /dev/disk/dsk4b:
  Allocated space:     124063 pages (969MB)
  In-use space:        129 pages ( 0%)
  Free space:          123934 pages ( 99%)

Total swap allocation:
  Allocated space:     335702 pages (2.56GB)
  Reserved space:      11873 pages ( 3%)
  In-use space:          258 pages ( 0%)
  Available space:    323829 pages ( 96%)
```

在此示例中有两个交换分区。

根据跨成员文件系统流量来平衡它们。例如，查看此输出并根据最近的过去判断 /usr/staff 文件系统是否应被重新定位，如果需要则应重新定位到哪个成员。

```
# cfs -s /usr/staff
/usr/staff [staff#staff] (dsk13c):
        read    write   lookup  getattr readlink access   other
-------- ------ ------ ------ ------ ------ ------ ------
batra:       0       0      26      0       0       1       5
* gamara:    0       0      26     27       0       1       5
mothra:     13      40      47      0       0      20      51
rodan:     225    12880     63      3       0      21      31
total:     238    12920    162     30       0      43      92
```

正如我们所见，成员 rodan 是对 /usr/staff 文件系统读写最重的成员，将其从 gamara 重新定位到 rodan 可能有益（上面的 cfs 输出中“*”表示 gamara 是 CFS 服务器）。如果认为过去的行为是未来行为的指标，这是一个好主意，但正如大多数股票经纪人会告诉你的，不要押上全部身家。基于你对集群的了解并辅以上述统计数据来进行这些 CFS 调整。

现在，让我们继续看示例脚本。在 HP 提供的解决方案出现之前，此脚本应能使管理 CFS 变得更容易。cfsldb 脚本提供了在本书网站上（参见附录 B），它从成员特定的 rc.config 文件中读取 CFSSVR 配置变量。该脚本将根据 CFSSVR 变量的内容重新定位文件系统。CFSSVR 是一个以空白分隔的挂载点列表，成员应提供这些挂载点。如果文件系统已由该成员提供服务，则跳过它。该脚本还在 /cluster/admin 中写入一个日志，名为 cfsldb_<hostname>.log，每次运行程序时都会被覆盖。

例如，要让一个成员提供服务 root、/usr 和 /var：

```
# rcmgr set CFSSVR ""/ /usr /var""
```

```
# ./cfsldb start
cfsldb: Relocating / from sheridan to molari...done!
cfsldb: Relocating /usr from sheridan to molari...done!
cfsldb: Relocating /var from sheridan to molari...done!
```

