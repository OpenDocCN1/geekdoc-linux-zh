

周日的 dump 命令可能如下，假设你需要将 `/`、`/usr` 和 `/var` 备份到位于 `/dev/nst0` 的 SCSI 磁带单元：

```
# dump out /dev/nst0 /
# dump out /dev/nst0 /usr
# dump out /dev/nst0 /var
```

周内其余几日的 dump 命令如下：

```
# dump 5uf /dev/nst0 /
# dump 5uf /dev/nst0 /usr
# dump 5uf /dev/nst0 /var
```

你也可以使用任何非 0 的 dump 级别进行增量备份。级别 5 让你具备了足够的灵活性，如果有某些关键文件需要备份，可以使用更高的级别来执行非计划的差异备份。如果你在周初做了许多不想在后续备份的修改，你也可以执行一次增量备份来重置正常的增量文件计数。当然，如果你偏离了通常的备份计划，应该仔细地标记磁带以防混淆。

作为一个示例，让我们来看对 `/usr/local/bin` 进行 dump 输出，因为 dump 量较小，输出内容比较容易管理。我们将使用的命令是：

```
# dump out /dev/nst0 /usr/local/bin
```

输出如下：

```
DUMP: Date of this level 0 dump: Thu Sep 21 08:09:35 2000
DUMP: Date of last level 0 dump: the epoch
DUMP: Dumping /dev/hdb1 (/) to /dev/nst0
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 120147 tape blocks.
DUMP: Volume 1 started at: Thu Sep 21 08:09:41 2000
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: DUMP: 230552 tape blocks on 1 volumes(s)
DUMP: finished in 148 seconds, throughput 1557 KBytes/sec
```

DUMP: Volume 1 completed at: Thu Sep 21 08:12:09 2000
DUMP: Volume 1 took 0:02:28
DUMP: Volume 1 transfer rate: 1557 KB/s
DUMP: level 0 dump on Thu Sep 21 08:09:35 2000
DUMP: DUMP: Date of this level 0 dump: Thu Sep 21 08:09:35 2000
DUMP: DUMP: Date this dump completed: Thu Sep 21 08:12:09 2000
DUMP: DUMP: Average transfer rate: 1557 KB/s
DUMP: Closing /dev/nst0
DUMP: DUMP IS DONE
```

此输出非常直观易懂。dump 在 148 秒内将 230,552 个块写入了一卷磁带。

## 远程备份

通过修改 dump 设备文件名的格式，可以使用 dump 指定远程备份服务器。你不能只指定简单的设备文件，而必须指定备份服务器的名称、冒号以及该服务器上的设备文件名，如下：

```
# dump out server:/dev/nst0 /usr
```

但在某些网络上，这可能导致备份缓慢。一个更好的选项可能是通过 rsh 管道传输备份：

```
# dump out -usr | rsh server
```
这意味着备份服务器必须运行 rsh（或 .rsh），即远程 shell 守护进程。该工具在安全方面存在巨大的问题风险，特别是对于任何连接到互联网的系统。更糟糕的是，你通常需要带 `-h` 参数运行 rsh 以允许 root 访问，这增加了安全问题的潜在风险。总的来说，只有在备份服务器受到防火墙良好保护的情况下，最好才使用这种访问方法。理想情况下，备份服务器不应有其他网络任务，除了维护它所需的用户外不应有其他用户，并且在发生最坏的情况下，不应包含任何黑客可能用来渗透网络的软件。

历史上，dump 的远程使用是通过一个独立的 rdump 工具实现的。在今天大多数 Linux 系统上，rdump 是指向普通 dump 工具的符号链接，该工具已经获取了 dump 的网络功能。

## restore

使用 restore 工具提取使用 dump 制作的备份。restore 有两种模式：交互式和非交互式。交互模式允许你选择一个或多个文件进行恢复，而非交互模式则恢复整个备份。如果你有多个归档，必须使用非回绕磁带设备。

### 交互式恢复

假设我们需要从之前用 dump 做的备份中恢复 `/usr/local/bin`。加载相应的备份磁带并运行以下命令：

```
# restore -i -f /dev/nst0
```

`-i` 标志告诉 restore 开始交互会话。当此命令执行时，你将得到 `restore>` 提示符。使用 `ls` 命令选择要恢复的文件。

```
restore> ls
```
由于我们知道该目录存在，我们可以添加想要的内容：

```
restore> add
```

### 非交互式恢复

要进行批量恢复，首先更改你想要的位置。如果磁带包含多个归档，你可以使用 `-s` 选项。例如，

```
restore> extract
```
这是在磁带上的。

