
## 备份资源

| 网站 | 工具 |
| :--- | :--- |
| **rsync.samba.org** | rsync 远程复制备份 |
| **www.amanda.org** | Amanda 网络备份 |
| **dump.sourceforge.net** | dump 和 restore 工具 |

相反，如果你想保留文件的拥有者和权限，你会使用 **-a**（archive）选项。添加 **-z** 选项将压缩文件。** -v** 选项提供详细模式。

```
`rsync -avz /home/george/myproject rabbit:/backup`
```

源路径末尾的斜杠将复制目录的内容，而不是生成一个该名称的子目录。在这里，**myproject** 目录的内容被复制到 **george-project** 目录。

```
`rsync -avz /home/george/myproject/ rabbit:/backup/george-project`
```

**rsync** 命令默认配置为使用 SSH 远程 shell。你可以使用 **-e** 选项指定它或替代的远程 shell。为了安全传输，你可以使用 ssh 对复制操作进行加密。要么使用 **-e ssh** 选项，要么将 **RSYNC_RSH** 变量设置为 ssh。

```
`rsync -avz -e ssh /home/george/myproject rabbit:/backup/myproject`
```

与使用 **rcp** 时一样，你可以从远程主机复制到你所在的主机。

```
`rsync -avz lizard:/home/mark/mypics/ /pic-archive/markpics`
```

你还可以将 rsync 作为服务器守护进程运行。这将允许远程用户将他们系统中的文件副本与你的系统上的版本进行同步，只传输发生更改的文件，而不是整个目录。许多镜像和软件 FTP 站点作为 rsync 服务器运行，让你无需再次下载完整版本即可更新文件。rsync 作为服务器的配置信息保存在 */etc/rsyncd.conf* 文件中。在 Fedora 上，作为服务器的 rsync 通过 **xinetd** 进行管理，使用 */etc/xinetd.d/rsync* 文件，该文件以 **-e -daemon** 选项启动 rsync。在 */etc/services* 文件中，它被列在端口 873 上运行。默认情况下它是关闭的，但你可以通过 system-config-services 的 On Demand Services 面板或 **chkconfig** 来启用它。

```
`chkconfig rsync on`
```

> **提示** *虽然它是为在主机之间复制而设计的，但你也可以将 rsync 用于在你自己的系统内制作副本，通常是复制到另一个分区或硬盘上的目录。实际上，rsync 有八种不同的使用方法。请查阅 rsync 的手册页以获取每种方法的详细描述。*

## Amanda

为了备份连接到网络的主机，你可以使用 Advanced Maryland Automatic Network Disk Archiver (Amanda) 来归档主机。Amanda 使用 **tar** 工具将所有主机备份到作为备份服务器运行的单一主机上。备份数据由每个主机发送到作为 Amanda 服务器运行的主机，在那里被写入磁带等备份介质。使用 Amanda 服务器时，所有主机的备份操作都集中在一个服务器上，而不是每个主机都要执行自己的备份。任何需要恢复数据的主机只需向 Amanda 服务器发出请求，指定文件系统、日期和文件名即可。备份数据被复制到服务器的暂存磁盘，然后从那里复制到磁带上。详细的文档和更新在 **www.amanda.org** 上提供。对于服务器，请确保安装 amanda-server 软件包，而对于客户端，你会使用 amanda-clients 软件包。

Amanda 设计用于自动备份配置甚至操作系统可能非常不同的主机。你可以备份任何支持 GNU 工具的主机，包括通过 Samba 连接的 Mac OS X 和 Windows 系统。

### Amanda 命令

Amanda 拥有自己的对应于常见备份任务的命令，以“am”开头，例如 **amdump**、**amrestore** 和 **amrecover**。命令列于表 34-2 中。**amdump** 命令是主要的备份操作。

| 命令 | 描述 |
| :--- | :--- |
| amdump | 对 disklist 配置文件中列出的文件系统执行自动备份。 |
| amflush | 用于直接将数据从暂存磁盘备份到磁带。 |
| amcleanup | 如果服务器发生故障，进行清理。 |
| amrecover | 使用交互式 shell 选择要恢复的备份。 |
| amrestore | 恢复备份，可以是文件或完整系统。 |
| amlabel | 为 Amanda 标记备份介质。 |
| amcheck | 在备份操作前检查备份系统和文件以及备份磁带。 |
| amadmin | 备份管理任务。 |
| amtape | 管理备份磁带，装载和移除它们。 |
| amverify | 检查磁带格式。 |
| amverifyrun | 检查上一次运行的磁带，指定备份的配置目录。 |
| amrm tape | 从 Amanda 数据库中移除磁带，用于损坏的磁带。 |
| amstatus | 显示当前 Amanda 备份操作的状态。 |

**表 34-2** Amanda 命令

**amdump** 命令执行请求的备份；它并非为交互使用而设计。对于交互式备份，你会直接使用像 **tar** 这样的归档工具。**amdump** 被放置在 cron 指令中，以便在指定时间运行。如果由于某种原因，**amdump** 无法将其所有数据保存到备份介质（磁带或磁盘），它会将数据保留在暂存磁盘上。稍后可以直接或使用 **amflush** 命令将数据写入。

你可以使用 **amrestore** 命令恢复特定文件以及完整系统。使用 **amrecover** 工具，你可以从备份列表中进行选择。

### Amanda 配置

配置文件放置在 /etc/amanda 中，日志和数据库文件放置在 /var/lib/amanda 中。在 Fedora 上安装 Amanda RPM 软件包时，这些文件会自动创建。你还需要创建一个目录用作暂存磁盘，备份在写入磁带之前保存在这里。这应该在一个可用空间非常大的文件系统上，足以容纳你最大整个主机的备份。

#### /etc/amanda

在 /etc/amanda 目录中，有为想要执行的不同类型备份创建的子目录。每个目录将包含其自己的 **amanda.conf** 和 **disklist** 文件。默认情况下，创建一个名为 **DailySet1** 的每日备份目录，其中包含默认的 **amanda.conf** 和一个示例 **disklist** 文件。要使用它们，你必须编辑它们以输入系统自身的设置。对于不同的备份配置，你可以创建一个新的目录，将 DailySet1 的 amanda.conf 和 disklist 文件复制进去，并对其进行适当编辑。当你发布如 **amdump** 这样的 Amanda 命令来执行备份时，你将使用 /etc/amanda 子目录的名称来表示想要执行的备份类型。

```
amdump DailySet1
```

/etc/amanda 目录还包含一个示例 cron 文件，**crontab.sample**，展示了 cron 条目应该是什么样子的。

#### amanda.conf

**amanda.conf** 文件包含基本配置参数，如磁带类型、日志文件以及暂存文件位置。在大多数情况下，你可以直接使用 DailySet1/amanda.conf 文件中列出的默认值。该文件有详细的注释，告诉你哪些条目需要更改。你需要将 tapedev 条目设置为你使用的磁带设备，并将磁带类型条目设置为你磁带驱动器的类型。在暂存磁盘部分，你需要指定要使用的暂存磁盘的分区和目录。有关各种选项的详细信息，请参阅 amanda 手册页和文档。

#### disklist

**disklist** 文件是用于指定要备份的文件系统和分区的地方。一个条目列出了主机、分区和 dump 类型。可能的 dump 类型在 **amanda.conf** 中定义。dump 类型设置了某些参数，如备份的优先级以及是否使用压缩。comp-root 类型将使用压缩和低优先级备份根分区，而 always-full 类型将使用无压缩和最高优先级备份整个分区。你可以在 amanda.conf 中定义其他 dump 类型并用于不同的分区。
