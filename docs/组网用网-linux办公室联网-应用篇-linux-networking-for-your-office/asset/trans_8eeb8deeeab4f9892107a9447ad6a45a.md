

## 使用 nfsd 选项

除了 /etc/exports 中的选项外，您还可以通过在启动程序时指定的选项来控制 NFS 守护进程的某些方面。在 Red Hat 6.0 系统中，NFS 守护进程在控制脚本 /etc/rc.d/init.d/nfs 中启动。您可以编辑此脚本以更改 NFS 选项，其中包括以下内容：

- -f 或 --exports-file—导出的文件名称。默认值为 /etc/exports。
- -l 或 --log-transfers—将传输记录到系统日志。此选项可能会大幅增加 NFS 服务器上系统日志的大小，但在您想要详细监控网络活动时可能很有用。
- -n 或 --allow-non-root—允许来自 1024 以上端口号的连接。这与 /etc/exports 中的 insecure 选项类似。
- -p 或 --promiscuous—服务器为网络上的任何主机提供服务。
- -r 或 --re-export—允许服务器导出从其他地方导入的文件系统。
- -t 或 --no-spoof-trace—关闭对从未经授权的来源挂载导出尝试的记录。通常，nfsd 会记录失败的挂载尝试，以便您能够知晓。

请查看 nfsd 的 manpage 以获取更多选项，其中大多数与在命令行启动程序时返回报告信息有关。

脚本 /etc/rc.d/init.d/nfs 在使用 start 和 stop 参数分别运行脚本时启动和停止守护进程。这通常发生在系统启动和关闭时，但如果您需要更改 NFS 配置，可以关闭 nfsd，然后通过执行此脚本重新启动它。您也可以使用 restart 和 reload 命令分别让 NFS 完全重新启动或重新加载其配置文件。

## 使用 linuxconf 配置 NFS

与许多 Red Hat Linux 网络功能一样，您可以使用 linuxconf 配置 NFS。选择 Config, Networking, Server tasks, Exported file systems (NFS) 以获取主 NFS 配置屏幕，如图 10.1 所示。您可以从此屏幕添加新条目或编辑现有条目；在任何一种情况下，您都会得到如图 10.2 所示的 One exported file system 选项卡。

![](img/5d4d3092919d1d16884788127447cc6d_268_0.png)

### FIGURE 10.1

您可以选择现有条目以更改其属性，或单击 Add 以添加新条目。

![](img/5d4d3092919d1d16884788127447cc6d_268_1.png)

### FIGURE 10.2

您可以选择一个导出路径，然后指定一组客户端，每个客户端都可以具有其独特的选项集。

## NFS 中的权限如何工作

由于 NFS 是为多用户操作系统（OS）之间的文件共享而设计的，因此 NFS 客户端和服务器需要通信用户信息。它们通过使用用户和组 ID 号来实现，这可能会导致一些有趣的效果。

### 远程用户和本地用户

假设您有两台 Linux 计算机，机器上为多个用户设置了账户，如表 10.1 所示。默认情况下，NFS 以一种令人困惑的方式映射用户 ID，至少令人困惑，最坏的情况是安全问题。例如，使用表 10.1 的信息，唯一能在两台计算机上正确访问其文件的是 carljones，因为他的用户 ID 在两台计算机上是相同的。如果计算机 teela 将文件系统导出到 nessus，那么从 nessus 看，jimbrown 将能够访问 teela 上 bevsmith 的文件，而 bevsmith 将能够访问 susadams 的文件。另一方面，如果计算机 nessus 将文件系统导出到 teela，jimbrown 将能够从 teela 访问 susadams 在 nessus 上的文件。类似的问题也可能发生在组 ID 上。

### TABLE 10.1 两台计算机上的假设用户和组 ID

| User | User ID on nessus | User ID on teela |
|---|---|---|
| jimbrown | 501 | 504 |
| carljones | 502 | 502 |
| bevsmith | 503 | 501 |
| susadams | 504 | 503 |

### NOTE

> 实际的用户名并不重要。例如，如果 jimbrown 在一个系统上被称为 jbrown，相同的原则适用，包括相同的解决方案。

不用说，像这样的用户映射问题在最好情况下也是不可取的。解决它们的一种方法是同步两台机器上的用户和组 ID。这对于从头开始配置少量计算机的小型网络来说当然是最简单的解决方案；您只需确保每个用户在所有系统上获得相同的用户和组 ID。如果机器上已有用户账户，则此解决方案会更棘手。如果您想尝试实施它，您有两个选择：

