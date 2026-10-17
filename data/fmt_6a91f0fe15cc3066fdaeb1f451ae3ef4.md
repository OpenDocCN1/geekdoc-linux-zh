
`chkconfig amidtape on`

`chkconfig amandaix on`

`service xinetd restart`

然后重启 `xinetd` 守护进程以使其立即生效。为了让客户端能够从服务器恢复备份，必须将客户端的主名放在 Amanda 用户目录下的 `amandahosts` 文件中。在 Fedora Core 4 上，该目录为 `/var/lib/amanda`。在服务器上，`/var/lib/amanda/amandahosts` 将列出所有由 Amanda 备份的主机。

## Amanda 主机

每个主机都必须允许 Amanda 服务器访问。为了做到这一点，你需要将 Amanda 服务器的主名放在每个客户端的 `amandahosts` 点文件中。该文件位于 Amanda 用户的主目录中。在 Fedora Core 4 系统上，这是 `/var/lib/amanda` 目录。

每个主机都需要运行 Amanda 守护进程客户端 `amanda`，它也运行在 `xinetd` 下。使用 `chkconfig` 或 `system-config-services` 将其开启。

```bash
chkconfig amanda on
```

> 提示：如果你的服务器和主机有防火墙，你需要允许通过 Amanda 使用的端口（通常是 `10080`、`10082` 和 `10083`）。

## 使用 Amanda

备份通过 `amdump` 命令执行。

```bash
amdump DailySet
```

每个备份的 `amdump` 命令都存放在 Amanda 的 crontab 文件中。运行 `amcheck` 操作以确保磁带已就绪是有帮助的。

```bash
0 16 * * 1-5 /usr/sbin/amcheck -m DailySet
45 0 * * 2-6 /usr/sbin/amdump DailySet
```

在使用磁带之前，你必须使用 `amlabel` 对其进行标记。Amanda 使用标签来决定应该将哪种磁带用于备份。以 Amanda 用户（而不是 root）身份登录并标记磁带以便使用。

```bash
amlabel DailySet
```

客户端可以使用 `amrecover` 恢复备份。这需要以 root 用户身份运行，而不是 Amanda 服务器。`amrecover` 命令通过类似于 `ftp` 的交互式 shell 工作，允许你列出可用文件并选择它们进行还原。在 `amrecover` shell 中，`ls` 命令将列出备份，`add` 命令将选择其中一个，提取过程将还原它。`lcd` 命令允许你更改目录；

![](img/70a65fc8f3408711ddea7ea368f31720_776_0.png)

`amrecover` 将使用 `DailySet` 作为默认，对于其他配置，你需要使用 `-C` 选项指定配置目录。如果你有多个 Amanda 服务器，可以使用 `-t` 选项列出你想要的。

```bash
amrecover -C DailySet
```

要恢复全系统备份，你使用 `amrestore` 命令并指定磁带设备和主机名。

```bash
amrestore /dev/rmt1 rabbit
```

要选择某些文件，你可以将输出管道传输到恢复命令（如 `restore`，将在下一节讨论）。

```bash
amrestore -p /dev/rmt1 amrestore mydir | restore -ibvf 2 -
```

## 使用 dump 和 restore 进行备份

你可以使用 `dump` 和 `restore` 工具备份和恢复你的系统。`dump` 可以备份你的整个系统，也可以执行增量备份（仅保存自上次备份以来更改的文件）。`dump` 支持多种用于管理备份操作的选项，例如指定备份操作的大小和存储介质长度（见表 36）。

注意：还有几种 dump 工具可用。`dump` 命令可以格式化磁带。查看帮助页获取详情。

### dump 级别

`dump` 工具使用级别来决定备份的程度。级别 0 会备份整个文件系统。剩余级别执行增量备份。

| 选项 | 描述 |
| :--- | :--- |
| `-0` 到 `-9` | 指定 dump 级别。级别 0 是全备份，复制整个文件系统。0 以上的级别执行增量备份，备份自上次备份以来创建或修改的文件。 |
| `-B` | 允许你指定卷中的块数，覆盖结束介质检测。 |
| `-a` | 允许 dump 绕过任何长度计算并等待检测结束介质。推荐用于现代驱动器。 |
| `-bsize` | 允许你指定每个 dump 记录的字节数。使用此选项可以创建更大的块，从而加快备份。 |
| `-d` | 指定磁带密度（1600 DPI）。 |
| `-h` | 带有用户 标记的文件将不在指定的级别及以上备份。默认值为 1。 |
| `-f` | 将文件系统备份到指定的文件或设备。可以是文件或磁带驱动。你可以指定多个文件名，用逗号分隔。远程设备或文件可以通过前置的主名引用，`hostname:file`。 |
| `-k` | 使用 Kerberos 身份验证与远程服务器通信。 |
| `-M` | 实现多卷备份，写入的文件被视为前缀，后续文件使用数字序列作为后缀，例如 `file001`、`file002` 等。当备份文件需要大于 Linux ext3 2GB 文件大时非常有用。 |
| `-n` | 当备份需要注意时通知操作员。 |
| `-s` | 指定磁带长度（英尺）。当达到长度时，dump 将提示更换新磁带。 |
| `-T` | 估计执行备份所需的空间。允许你指定自己的日期而不是使用 `/etc/dumpdates` 文件。在成功更新后在 `/etc/dumpdates` 中写入条目。 |
| `-W` | 检测并显示需要备份的文件系统。此信息取自 `/etc/dumpdates` 和 `/etc/stab` 文件。 |
| `-w` | 检测并显示需要备份的文件系统，仅从 `/etc/fstab` 提取信息。 |

## 备份记录

备份记录在 `/etc/dump` 文件中。该文件将列出之前的所有备份，并指定执行备份的文件系统、执行日期以及使用的 dump 级别。你可以使用这些信息从指定的备份恢复文件。请记住，`/etc/stab` 文件也记录了每个文件系统的 dump 级别以及推荐的备份频率。使用 `-w` 选项，`dump` 将同时分析 `/etc/dump` 和 `/etc/stab` 文件以确定哪些文件系统需要备份。带有 `-w` 选项的 `dump` 命令仅使用 `/etc/stab` 来恢复准备好备份的文件系统。

## 使用 dump 操作

`dump` 命令的参数包括：dump 级别、存储备份的设备以及正在备份的文件系统的设备名称。如果存储介质（如磁带）太小无法容纳备份，`dump` 将暂停并让你插入另一块。`dump` 支持多卷备份。`-u` 选项会将备份记录在 `/etc/dump` 文件中。在以下示例中，对 `/dev/hda3` 硬盘分区上的文件系统执行整个备份（dump 级别 0）。备份存储在磁带设备 `/dev/tape` 上。

```
dump -0u -f /dev/tape /dev/hda5
```

> 注意：你可以使用 `mt` 命令来控制磁带设备；`mt` 具有倒带、擦和定位磁带的选项。`omt` 命令控制远程磁带设备。

存储设备可以是另一个硬盘分区。当你安装系统时，系统很可能检测到了该设备并将 `/dev/tape` 设置为指向它的链接，就像处理 CD-ROM 一样。如果没有设置链接，你必须自行创建或使用设备名称。磁带设备具有不同的名称，取决于型号或接口。SCSI 磁带设备以 `st` 为前缀，并带有特定设备的数字：`st0` 是第一个 SCSI 磁带设备。在 `dump` 命令中使用它，只需指定其名称即可。

```
dump -0u -f /dev/st0 /dev/hda5
```

如果你需要备份位于网络上另一个系统上的设备，必须指定该系统的主机名和设备名称。主机名输入设备名称之前，并用冒号分隔。在以下示例中，用户将文件系统 `/dev/hda5` 备份到 `rabbit.mytrek.com` 系统中名为 `/dev/st1` 的 SCSI 磁带设备：

```
dump -0u -f rabbit.mytrek.com:/dev/st0 /dev/hda5
```
