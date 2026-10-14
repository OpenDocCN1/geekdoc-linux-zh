

自安装 TruCluster Server 软件并创建集群以来添加到系统中的内容。

回到我们关于引导分区的讨论：如果内核和 osf_boot 文件现在位于 `./local/./boot_partition`，那么我们是否改变了通常查找这些文件的位置，对吧？嗯，既是也不是。虽然这些文件从技术上讲位于不同的位置，我们仍然可以从它们在根目录中的先前位置引用它们，因为那里有 CDSL。

```
# find / | grep boot_partition
genunix -> cluster/members/(memb)/boot_partition/genunix
osf_boot -> cluster/members/(memb)/boot_partition/osf_boot
vmunix -> cluster/members/(memb)/boot_partition/vmunix
```

## 12.2.1 CDSL 与 mv(1) 命令

正是由于上一个示例的输出，我们不得不讨论在替换作为 CDSL 的文件时不要使用 mv 命令的重要性。如你所见，内核（/vmunix）现在是一个 CDSL。多年来，我们都会构建新内核，然后将其从构建位置移动到根目录。事实上，过去就是这样教的。我们现在必须摒弃所学，改用 cp(1) 命令。

像往常一样构建内核。

```
# doconfig -c MOLARI
*** KERNEL CONFIGURATION AND BUILD PROCEDURE ***
Saving /sys/conf/MOLARI as /sys/conf/MOLARI.bck
Do you want to edit the configuration file? (y/n) [n]:
*** PERFORMING KERNEL BUILD ***
Working...Mon Dec 17 11:59:58 EST 2001
The new kernel is /sys/MOLARI/vmunix
```

复制内核。

```
# cp /sys/MOLARI/vmunix /
```

从构建目录中移除内核，并记住该内核是一个硬链接。

```
# cd /sys/MOLARI ; ls -i vmunix* | sort
26247 vmunix.swap
26711 vmunix
26711 vmunix.MOLARI
26711 vmunix.sys
```

```
# rm vmunix vmunix.MOLARI vmunix.sys
```

## 12.2.2 修复损坏的 CDSL

如果你意外（或以其他方式）移除了 CDSL，可以使用 mkcdsl(8) 命令修复它。

例如，我们出于习惯不小心将新内核移动到了根目录。

```
# mv /sys/MOLARI/vmunix /
```

内核现在位于根目录中，而 vmunix 不再是 CDSL。

```
# file /vmunix
/vmunix:
COFF format alpha executable or object module not stripped - version 3.13-14
```

我们知道 /vmunix 应该是一个 CDSL，但如果我们不知道这一点呢？那么，我们可以运行 cdslinvchk(8) 命令，它会告诉我们存在一个缺失的链接以及该链接应该是什么。还应注意，clu_check_config(8) 也会执行 cdslinvchk。

```
# cdslinvchk
Failed CDSL inventory check. See details in /var/adm/cdsl_check_list
```

```
# cat /var/adm/cdsl_check_list
Expected CDSL: /vmunix -> cluster/members/(memb)/boot_partition/vmunix
An administrator or application has replaced this CDSL with:
-rwxr-xr-x 1 root system 21009120 Dec 17 12:00 /vmunix
```

既然我们知道链接应该是什么，就可以使用 mkcdsl 命令修复它。我们将使用 “-b” 选项创建 CDSL，使其指向 boot_partition，并使用 “-c” 选项将文件复制到 CDSL 指向的位置。

```
# mkcdsl -bc /vmunix
```

验证该过程是否成功。

```
# cdslinvchk
Successful CDSL inventory check
```

有关 CDSL 以及 cdslinvchk 和 mkcdsl 命令的更多信息，请参阅第 6 章和/或 cdslinvchk(8) 和 mkcdsl(8) 参考手册页。

## 12.3 硬件管理再讨论

在集群中，硬件管理与独立系统相比大体上没有变化。但话又说回来，Tru64 UNIX（从版本 5.0 开始）中硬件处理方式的重新设计，正是为了满足两件事：

-   到存储设备的多路径。
-   TruCluster Server。

不过，有几点已经发生了变化，我们认为最好让您了解这些差异。

### 12.3.1 硬件管理数据库再讨论

创建集群时出现的第一个小变化是，一些以前位于 /etc 目录中的硬件数据库已被迁移到每个成员的引导分区，并被 CDSL 取代（参见图 12-2）。

表 12-2 列出了这些数据库及其在集群或独立系统中的相应位置。

### 12.3.2 hwmgr(8) 命令再讨论

hwmgr 命令具有集群感知能力。但是，必须将焦点放在集群上，才能查看整个集群范围内的结果，否则你将只会看到特定成员的信息。例如，如果你想查看集群上的设备，可以使用 “hwmgr -view device” 命令。

![](img/a0df85c2e542a8d6c913113908553aa4_310_0.png)

