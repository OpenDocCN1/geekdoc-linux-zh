
```
*run
Automatically selected Catalog: MyCatalog
Using Catalog "MyCatalog"
A job name must be specified.
The defined Job resources are:
        1: BackupClient1
        2: BackupCatalog
        3: RestoreFiles
        4: EtcBackup
Select Job resource (1-4): 4
Run Backup job
JobName: EtcBackup
Level: Full
Client: rhel-fd
FileSet: OnlyEtc
Pool: File (From Job resource)
Storage: bacula-sd (From Job resource)
When: 2022-11-12 19:34:22
Priority: 10
OK to run? (yes/mod/no): yes
Job queued. JobId=1
```

> 图 14.5：使用 `bconsole` 运行 `Bacula` 作业的示例

当作业完成，表明复制正确或报告任何错误时，可以使用命令`messages`获取最新信息。图 14.6 展示了一个输出示例：

```
12-Nov 20:14 bacula-dir JobId 13: Bacula Enterprise bacula-dir 13.0.1 (05Aug22):
Build OS:
x86_64-pc-linux-gnu-bacula-enterprise ubuntu 22.04
JobId:
13
Job:
EtcBackup.2022-11-12_20.14.52_03
Backup Level:
Full
Client:
"rhel-fd" 11.0.1 (05Feb20) x86_64-redhat-linux-gnu,redhat,Enterprise 9.0
FileSet:
"OnlyEtc" 2022-11-12 19:34:24
Pool:
"File" (From Job resource)
Catalog:
"MyCatalog" (From Client resource)
Storage:
"bacula-sd" (From Job resource)
Scheduled time:
12-Nov-2022 20:14:50
Start time:
12-Nov-2022 20:14:54
End time:
12-Nov-2022 20:14:55
Elapsed time:
1 sec
Priority:
10
FD Files Written:
1,003
SD Files Written:
1,003
FD Bytes Written:
21,126,497 (21.12 MB)
SD Bytes Written:
21,238,253 (21.23 MB)
Rate:
21126.5 KB/s
Software Compression:
None
Comm Line Compression:
62.7% 2.7:1
Snapshot/VSS:
no
Encryption:
no
Accurate:
no
Volume name(s):
Vol-0001
Volume Session Id:
1
Volume Session Time:
1668284067
Last Volume Bytes:
42,558,716 (42.55 MB)
Non-fatal FD errors:
0
SD Errors:
0
FD termination status:
OK
SD termination status:
OK
Termination:
Backup OK
```

> 图 14.6：使用 `bconsole` 显示消息的示例

要获取作业列表及其状态，需要执行的命令是`list jobs`。图 14.7 展示了输出示例：

| JobId | Name | StartTime | Type | Level | JobFiles | JobBytes | JobStatus |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `*` | `EtcBackup` | `2022-11-12 20:14:54` | `B` | `F` | `1,003` | `21,126,497` | `T` |

> 图 14.7：使用 `bconsole` 列出 `Bacula` 作业的示例

可以在不使用交互模式的情况下使用`bconsole`，通过管道将执行的操作发送到标准输入。在图 14.8 中，展示了一个使用管道获取客户端`rhel-fd`信息的示例。

### Relax-and-Recover (ReaR)

该软件是一个开源的裸机灾难恢复解决方案。它易于安装、配置和使用，用于恢复系统。此解决方案会生成一份随时可用的系统副本。它支持多种启动介质（`ISO`、`PXE`、`USB` 或 `eSATA`）和多种网络协议（`nfs`、`cifs`、`ftp` 或 `http`），以及各种备份策略（`Symantec Netbackup`、`EMC Networker` 等）。

生成的文件可以包含在另一个备份解决方案中，例如`Bacula`，以便在需要时使用。恢复是一个两步过程：挂载启动介质以及从中央服务器或存储设备传输数据。

使用`ReaR`的最大优势之一是该解决方案使用系统工具来执行备份。以下示例使用中央`NFS`存储来保存数据和`ISO`镜像以供使用。安装只需从软件仓库安装`rear`软件包即可。安装后，需要配置的文件是`/etc/rear/local.conf`，如下所示（以`Red Hat Enterprise Linux`系统为例）：

```bash
yum install -y rear
cat >/etc/rear/local.conf <<EOF
OUTPUT=ISO
BACKUP=NETFS
BACKUP_URL="nfs://ubuntu/storage"
EOF
```

`ReaR` 解决方案提供了`rear`命令以执行不同的操作。参数`mkbackup`将初始化备份过程，在上面的示例中，它将生成一个`ISO`镜像，并将数据复制到用于恢复过程中的使用。命令`rear mkbackup -v`的示例输出如下：
