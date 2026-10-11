
## 捎带确认（ACKs）

- 最小化协议开销（帧头）
- 限制负载较轻时的延迟（例如定时器和 TCP ACK 设置）
- 检查会话建立和认证开销

评估因配置更改而可能带来的性能提升的常见方法如下：

1.  选择一个文件复制工作负载或基准测试。
2.  多次执行测试以预热缓存并平滑变化；在负载较轻的网络上执行测试。
3.  将初步结果与基线（例如在本地执行相同的测试，或通过另一个网络文件系统或 FTP 执行）进行比较，以验证目标是否合理。
4.  逐渐增加基准负载，直到达到最大总体吞吐量。
5.  更改服务器或客户端配置设置并重新测试，测量性能和网络流量（如帧数和平均响应时间）的变化。
6.  通过仔细检查网络跟踪数据（例如使用 Ethereal 网络分析器）来分析配置更改的副作用。
7.  分而治之。使用两个较小的测试来模拟测试：一个用于本地文件调用，另一个用于网络套接字调用。专注于更窄子系统的性能优化（例如，在服务器上本地运行 dbench 和 tbench，而不是在网络上运行更大的 NetBench 模拟器）。

## NFS

对于 NFS 客户端，默认的 rsize 和 wsize 可以在挂载时指定。典型值范围在 4K 到 32K 之间。对于 NFS 版本，它们受服务器约束，并随着基于 TCP 的 NFS 服务器实现的支持 32K 而改变。Linux 客户端支持最大 32K 的 rsize/wsize。设置大于 MTU（通常为 1500 字节）的 rsize 会导致更高级别的 SunRPC 帧在多个 TCP 帧之间进行分片和重组，在某些情况下会减慢性能。你可以使用 iozone 和 bonnie 进行实验以确定最佳值。netstat 和 nfsstat 工具可以分别用于获取有用的 TCP 和 NFS 统计信息，以便与基准吞吐量和计时结果进行关联，并且 tracepath 可用于确定网络帧大小（可以通过 ifconfig MTU 选项更改）。2.6 内核增加了配置 NFS/SunRPC 使用 TCP 的能力，这比默认配置（NFS/SunRPC over TCP）略慢。NFS over UDP 通常用于局域网，但如果 `nfsstat` 命令报告的超时过多，请考虑增加 NFS `mount` 选项 retrans 和 timeo 的值。nfss 的服务器实例数量可能会极大地影响性能，并且可以在 Linux 服务器系统的启动脚本中进行调整。Linux NFS 服务器可以使用 'sync' 或 'async' 标志导出数据，后者由于服务器上的写回机制而具有更好的性能，但在服务器故障时存在数据完整性风险。

## Samba

三个配置设置显著影响 Samba 性能，并应在服务器的 `smb.conf` 文件中检查：

- `Sendfile`。Sendfile 是一种减少传出文件数据复制操作次数的机制。Samba 可以配置 `with-sendfile` 选项，使其能够将数据直接从服务器文件系统发送到网络适配器，从而提高吞吐量并降低服务器利用率。
- *部分通配符搜索的大小写敏感文件匹配*。目录条目的缓存在 Samba 中很复杂，因为 CIFS（Windows/DOS/OS2）通常请求大小写不敏感的文件匹配，而 Linux 服务器上的 POSIX 文件 API 仅提供大小写敏感的文件搜索。作为一个例子，在大小写不敏感的文件系统上进行 CIFS 搜索文件 `\\server\\share\\file*.exe` 只需要执行相对少量的服务器操作。然而，Linux 上的 Samba 需要检查 "file" 和 "exe" 的所有形式的匹配，包括 "File1.Exe"、"FILE2.EXE"、"file3.EXE" 和 "FILE4.exe"。Samba 3 服务器将路径与包含等效小写文件名列表的缓冲区（即 "sbat 缓存"）进行匹配，以提高这些操作的性能，但这种方法对于大型目录效果不佳（尽管在 Samba 3.0.12 及更高版本中已有很大改进）。通过使用 Linux xattrs 存储保留大小写的文件名，Samba 4 可以更高效地处理大型目录上的搜索操作。即使在 Samba 3 版本中，通过在 Samba 配置文件 `smb.conf` 中启用大小写敏感搜索，也可以极大地提高部分通配符搜索的性能（在某些基准测试中性能提升超过 5%）。在 `smb.conf` 中设置 `case sensitive = on` 可能会影响 Windows 应用程序的行为（因为它们期望大小写不敏感的文件匹配行为），除非导出的共享位于已格式化为大小写敏感的分区上（如 VFAT）。可以通过向 `mkfs.jfs` 工具传递 `-o format` 选项来创建大小写不敏感的 JFS 分区。
- *SMB 日志记录*。在较高日志级别下，SMB 日志记录可能会造成严重的性能损耗。将 `smb.conf` 中的日志级别降至 0 或 1 可能会带来可测量的性能提升。

除了上述内容外，启用内核 oplocks（而不是让 Samba 服务器内部管理 oplocks）以及在文件系统中启用 ACL 和 ACL 继承（这会给服务器的本地文件系统带来额外的负载以检索 xattrs）也会降低 Samba 性能。Samba 性能对 TCP 套接字选项的变化也很敏感（例如 `TCP_NODELAY`，可以在 `smb.conf` 参数 `socket_options` 中指定）。

## 性能测量

有许多用于性能测量的工具，可以与服务器利用率信息结合使用。有些工具现在可以通过 /proc 目录中的伪文件方便地以文本形式查看，以帮助评估性能权衡。测量文件 I/O 性能最常用的工具如下：

- *iozone*。用于测量网络文件 I/O 性能的出色基准测试，涵盖各种类别，如读取与写入、不同大小以及随机与顺序访问。
- *Bonnie*
- *NetBench*。由 Ziff Davis 实验室开发的经典 CIFS 基准测试已经显得有些过时。它需要大量昂贵的客户端才能充分负载现代 Linux Samba 服务器。
- *dbench, tbench, smborture*。这些工具分别提供了 NetBench 运行产生的文件活动、相应的网络套接字活动和 SMB 活动的更高效模拟。
- *spec cifs*。目前正在与 SNIA 和 SPEC 合作开发下一代 CIFS 基准测试。
- *specsfs*。常用于报告 NFS 版本 3 性能的最常见基准测试。
- *The Connectathon NFS 套件*。当使用 `runt est s a t` 运行时，它会生成关于常见操作有用且细粒度的计时信息。

这些工具在第 6 章“作为理解工作负载性能辅助的基准测试”中详细讨论。

## 用于改进容量规划的负载测量

CIFS 客户端可以通过在内核配置中启用 CIFS 统计信息并检查 /proc/fs/cifs/Stats 来测量常见请求的数量。这对于确定服务器何时响应缓慢非常有用。统计信息的一个示例如下：

```
Resources in use
CIFS Session: 2
Share (unique mount targets): 2
SMB Request/Response Buffer: 2
Operations (MIDs): 0

0 session 0 share reconnects
Total vfs operations: 550378 maximum at one time: 6

1) \\localhost\\stevf
SMBs: 11956 Oplock Breaks: 0
Reads: 89 Bytes 1145705
Writes: 3962 Bytes: 1888452
Opens: 868 Deleters: 934
Mkdirs: 118 Rmdirs: 118
Renames: 263 T2 Renames 0
2) \\192.168.0.4\\c5
SMBs: 365570 Oplock Breaks: 0
Reads: 124712 Bytes 456637519
Writes: 152198 Bytes: 613673810
Opens: 3 Deleters: 0
Mkdirs: 0 Rmdirs: 0
Renames: 0 T2 Renames 0
```

## 打印服务器性能

打印服务器性能受四个主要因素影响：

- 作业在哪里渲染
- 作业在通过网络传输并在服务器磁盘上存储时的大小
- 打印作业在服务器上经过多少层软件
- 打印设备的服务器驱动程序的效率

在 Windows 系统向 Linux 服务器打印的情况下，由于 Windows 打印驱动程序支持的广泛性，通常打印作业主要在客户端处理（而不是部分在客户端、部分在服务器上处理，这在 Windows 客户端向 Windows 服务器打印时通常会发生）。当打印作业在客户端渲染并作为原始打印文件发送到服务器时，打印网络打印作业所需的网络流量大得多，并且该文件可能会占用服务器上的大量磁盘空间，但打印该作业所需的服务器 CPU 较少。特别是当使用 Samba 作为打印服务器时，打印作业通常会在服务器上经过多个额外的层：CUPS 子系统，然后是 Ghostscript，最后可能是会减慢性能的打印驱动程序。
