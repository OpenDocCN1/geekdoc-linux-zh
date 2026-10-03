
# rmvol /dev/disk/dsk2c domain_1

## showfdmn [options] [domain]

使用 `showfdmn` 显示文件域信息。如果文件域处于活动状态（至少有一个文件集已挂载），可以使用 `showfdmn` 命令显示该文件域及其包含的卷的详细信息。

例如，使用以下命令显示 `test_domain` 文件域域信息：

```
# showfdmn u01_domain
```

| Id | Date Created | LogPgs | Version | Domain Name |
|---|---|---|---|---|
| 3c080617.010006fa | Fri Nov 30 16:20:07 2001 | 512 | 4 | u01_domain |
| Vol | 512-Blks | % Used | Cmode | Rblks | Wblks | Vol Name |
|---|---|---|---|---|---|---|
| 1L | 55450096 | 517911168 | 7% | on | 512 | /dev/vol/rootdg/vol01 |

## showfsets [options] [domain]

使用 `showfsets` 命令显示 AvFS 域的文件集信息。

```
# showfsets u01_domain
```

```
u01
Id : 3c080617.010006fa.1.8001
Files : 108084, SLim: : 0, HLim: : 0
Blocks (512) : 185623940, SLim: : 0, HLim: : 0
Quota Status : user=off group=off
Object Safety : off
Fragging : on
DMAPI : off
```

## verify [options] [domain]

使用 `verify` 命令检查磁盘上结构。在 `verify` 期间会检查元数据表和内部结构。

检查活动域使用 `verify -a` 选项。

```
# /sbin/advfs -a u01
Domain verification
Id 3c080617.010006fa
Checking disks ...
Checking storage allocated on /dev/vol/rootdg/u01_volume
Scanning tags ...
Scanned a total of 4 tags.
Searching for lost files ...
Searched 4 tags, no lost files.
```

# 第 7 章 Oracle9i 安装

实时应用集群（RAC）扩展了以前版本提供的集群功能。Oracle9i 是一种提供了更好的可用性和扩展性的新架构。

Oracle9i 的重大变化是完整实现了 Cache Fusion，它在不产生昂贵 I/O 操作的情况下确保多个节点的一致性。高速集群互连用于在节点数据库缓存之间传递数据块。

Oracle 这一新版本引入了一些术语以更准确地描述产品功能。请见表 7-1。

## 表 7-1: Oracle9i 术语

| 术语 | 定义 |
|---|---|
| 集群 (Cluster) | 同时可从多个节点访问的单个数据库。与 数据库不同，在 Oracle9i 中数据仍然对单个节点可用。 |
| 全局缓存服务 (GCS) 全局队列服务 (GES) | GCS 和 GES 服务处理管理功能。以前的版本使用分布式管理器 (DLM)。 |
| 服务控制 (SRVCTL) | 实时应用集群使用名为 `srvctl` 的工具来管理实例。SRVCTL 是用于启动或停止所有数据库实例的接口。 |
| 全局服务守护进程 (GSD) | GSD 进程与 SRVCTL 通信执行数据库启动和关闭等任务。GSD 在集群的每个节点本地运行。 |
| 服务器管理 (SRVM) | SRVM 是 Oracle Enterprise Manager 的组件。OEM 提供 RAC 管理。SRVM 还包括作业调度、事件管理和统计。 |

## Oracle9i 安装摘要

- 验证最小平台要求
- 设置 Oracle 环境变量
- 创建 Oracle UNIX 账户
- 设置 Oracle 内参数
- OFA 标准
- 安装 Oracle9i
- 安装 Oracle 补丁

## Oracle9i 安装步骤

1. 验证 Oracle9i 的最小系统要求。

使用 `vmstat` 命令查看可用内存。Oracle9i 至少需要 256MB RAM。

```
rac1> /bin/vmstat -P | grep "Total Physical Memory"
Total Physical Memory = 1024.0 M
Total Physical Memory Use: 130732 /1021.34M
```

交换空间（Swap）设置为 RAM 的两倍或至少 400MB。使用 `swap` 命令查看可用交换空间。在本示例中，系统有 1GB 物理内存和 3.14GB 交换空间。

```
rac1> /usr/sbin/swapon -s
Swap partition /dev/disk/dsk94b (default swap):
    Allocated space: 411423 pages (3.14GB)
    In-use space: 1 pages (0%)
    Free space: 411422 pages (99%)
```

总交换分配：

Allocated space: 411423 pages (3.14GB)

Reserved space: 9994 pages (2%)

In-use space: 1 pages (0%)

Available space: 401474 pages (97%)

## Oracle9i 附加前提

- CD-ROM 兼容 ISO 9660。
- 有 4.7GB 磁盘空间用于产品二进制文件和最小数据库。
- 已安装补丁的 Tru64 UNIX 5.1 或 5.1A。
- `/var/tmp` 有 400MB 空间。必要时设置 `TMPDIR` 环境变量。

2. 使用 `adduser` 工具创建 Oracle UNIX 账户。必须以 root 身份运行此命令或具有 root 权限。

> **提示：** 对于组织内的 Oracle 安装，请开发一个适用于所有系统和 Oracle 账户的标准 UID。通常做法是大于 1000 的 UID，为 UNIX 操作系统保留下面的 UID。

```
rac1> adduser
为新用户输入登录名（例如 john）：oracle
为 (oracle) 输入 UID [15]: 1001
为 (oracle) 输入全名: Oracle Administrator
为 (oracle) 输入登录组 [users]: dba
未找到 dba 组。现有组有：

system        mail            lpr             tcb
ndedaemon      terminal        backup      adm
uucp       tty             cron        operator
mem           news            users       ris
kmmm          opr             sysadmin    nobody
bin           auth            tape        nobody
sec           lp

是否要将 dba 组添加到 /etc/group 文件中 ([y]/n)? y
正在将 dba 组添加到 /etc/group 文件中...

输入新的组号 [200]: 101
组 dba 已添加到 /etc/group 文件中。

输入 (oracle) 应该所属的另一个组。
（如果没有，仅按 <Return>）：<Return>
为 (oracle) 输入父目录 [/usr/users]: /home
```

Shell 有：

/usr/bin/sh /usr/bin/ksh /bin/sh /bin/ksh

usr/bin/csh /usr/bin/posix/sh /bin/csh

为 (oracle) 输入登录 shell [/bin/sh]: `/bin/ksh`

正在添加新用户...

你必须为 (oracle) 输入新密码。

正在更改 oracle 的密码。

新密码：

重新输入新密码：

未使用哈希数据库，仅更新了 `/u01/app/oracle/etc/passwd` 文件。

完成 (oracle) 用户账户添加。

## 验证 Shell环境变量

在运行 Oracle 安装程序之前，应设置以下环境变量。Oracle9i 的 shell 变量见第 3 节。参见第 87 页的“创建新的共享配置文件”。

## 表 7-2：Oracle 环境变量

| 变量 | 推荐设置 |
| :--- | :--- |
| `ORACLE_BASE` | `/u01/app/oracle` |
| `ORACLE_HOME` | `/u01/app/oracle/product/9.0.1` |
| `ORACLE_SID` | 设置为数据库名称，对于书中介绍的数据库，数据库名为 demo。`ORACLE_SID` 是一个节点特定变量，节点 rac1 设置为 demo1，节点 rac2 设置为 demo2 |
| `ORACLE_PATH` | `/u01/app/oracle/product/9.0.1/bin:/u01/app/oracle/product/9.0.1/backup/bin:/usr/lib:/opt/bin:/usr/bin:` |
| `LD_LIBRARY_PATH` | `/u01/app/oracle/product/9.0.1/lib:/usr/lib` |

3. 以 Oracle UNIX 用户身份登录并使用 `set` 命令验证表 7-2 所示的设置。

```bash
oracle@rac1 ~ set

LD_LIBRARY_PATH=/u01/app/oracle/product/9.0.1/lib:/usr/lib
ORACLE_BASE=/u01/app/oracle
ORACLE_HOME=/u01/app/oracle/product/9.0.1/bin: \
/u01/app/oracle/product/9.0.1/backup/bin:/usr/lib:/opt/bin:/bin:bin/bin..
```

## Oracle 内内核参数

修改 `/etc/sysconfigtab` 文件的推荐方法是使用 `sysconfigdb` 命令和配置文件。段文件（stanza file）是一个包含内核调优信息的文本文件，用于更新 `sysconfigtab` 文件。使用段文件配合 `sysconfigdb` 命令可以减少手动编辑 `/etc/sysconfigtab` 可能产生的错误或意外。

更多关于调优的信息请参阅：

Tru64 UNIX System Configuration and Tuning

型号：AA-RH9GB-TE, 2000年8月

Compaq Computer Corporation

对于 Oracle9i RAC，需要自定义以下子系统。这些默认参数对于 Oracle 来说是不够的。

- `ipc` — 进程通信
- `proc` — 进程管理子系统
- `rdg` — 可靠数据报
- `vm` — 虚拟内存管理子系统

提示：使用 `sysconfig -s` 命令查看运行内核中配置的所有子系统。查看子系统的详细信息使用 `sysconfig -q [subsystem]` —— 例如：

```bash
sysconfig -q ipc
```

要查看子系统或属性的最小值和最大值，请使用 `racli> sysconfig -Q ipc msg_max`

ipc:

```
msg_max - type=INT op min_val=0 max_val=2147483647
```

## Oracle 的 UNIX 内核参数

以下修改是 Tru64 UNIX 5.1A 上大多数 Oracle 安装配置的良好基准。在每个集群节点上对内核进行修改，完成后重启该节点。

## 表 7-3：Oracle9i 最小内核设置

| 内核参数 | 设置 | 描述 |
| :--- | :--- | :--- |
| `max_per_proc_stack_size` | 32MB, 或 33554432 | 处理器栈大小。不要设置大于 512MB。 |
| `per_proc_stack_size` | 32MB, 或 33554432 | 处理器栈大小。 |
| `shm_max` | 4GB 减 16MB 或 4278190080 | 共享内存的最大允许大小。 |
| `shm_min` | 1024 | 单个共享内存段的最大允许大小。 |
| `shm_mni` | 256 | 共享内存段的最大数量。 |
| `shm_seg` | 128 | 一个进程可以附加的共享内存段的最大数量。 |

如果你的系统上某些内核参数设置得更高，请使用较大的值。

4. 在 `/usr/local/` 创建名为 `sysconfig` 的目录。

```
raci> mkdir /usr/local/sysconfig
raci> cd /usr/local/sysconfig
```

5. 创建一个包含内核可调参数的新段文件。将其命名为 `sysconfig.stanza`。使用 vi 或等编辑器向段文件中添加以下 ipc 设置。

进程通信 (IPC) 设置了两个或多个进程之间共享的信息量。

```bash
raci> vi sysconfig.stanza
ipc:
msg_max = 8192
msg_mnb = 16384
msg_mni = 64
msg_ql = 40
shm_max = 21390540
shm_min = 1024
shm_mni = 256
shm_seg = 128
ssm_threshold = 0
```

6. 向 `sysconfig.stanza` 添加 proc 子系统的以下值。

注意：以下参数应应设置为总物理内存的 75% 到 100%。

- `per_proc_data_size`
- `max_per_proc_data_size`
- `per_proc_address_space`
- `max_per_address_space`

指定字节大小。例如，如果你的系统包含 2048MB 物理内存，则应将参数设置为：

```
2048MB * 1024 * 0.75 = 16106276
```

例如，如下更改：

```bash
per_proc_stack_size = 16106276

proc:
max_proc_per_user = 1024
max_threads_per_user = 4096
per_proc_data_size = (物理内存的 75%-100%)
max_per_proc_data_size = (物理内存的 75%-100%)
per_proc_stack_size = 33554432
max_per_proc_stack_size = 53687091
per_proc_address_space = (物理内存的 75%-100%)
max_per_address_space = (物理内存的 75%-100%)
```

7. 向段文件添加以下 rdq（可靠数据报）设置：

rdq:

```
max_objs = 8096
msg_size = 32768
max_async_req = 128
max_sessions = 2048
rdq_auto_wires = 0
```

8. 向段文件添加以下 vm（虚拟内存）设置：

vm:

```
new_wire_method = 0
buc_minpercent = 10
buc_maxpercent = 50
vm_swap_eager = 0
```

9. 向段文件添加 advfs, rt, vfs 和 rm 的剩余设置：

advfs:

AdvfsSyncMmapPages = 1

rt:

aio_task_max_num = 1040

vfs:

fifo_do_adaptive = 0

rm:

rm_check_for_ipl = 0

注意：如果未为 Oracle正确设置内核参数，将在安装或启动数据库时遇到问题。

10. 将更改保存到 `sysconfig.stanza` 文本。使用 `sysconfigdb` 命令更新集群所有节点上的 `sysconfigtab` 文件。进行更改后需要重启。

```bash
rac1> cd /usr/local/sysconfig
rac1> sysconfigdb -m -f sysconfig.stanza
rac1> reboot
```

```bash
rac2> cd /usr/local/sysconfig
rac2> sysconfigdb -m -f sysconfig.stanza
rac2> reboot
```

11. 挂载 Oracle CD-ROM。在 Tru64 UNIX 5.x 中，系统的第一个 CD-ROM 命名为 `cdrom0c`。如果你有多个 CD-ROM，它们将顺序编号，例如 `cdrom0c`, `cdrom1c`, `cdrom2c` 等。

```
rac1> mount -r /dev/disk/cdrom0c /cdrom
```

如果 `/cdrom` 目录不存在，可能会看到以下错误：

`/dev/disk/cdrom0c on /cdrom: 无文件或目录`

你可以创建一个 `/cdrom` 目录或将 CD-ROM 挂载到 `/mnt`。任何挂载目录均有效。

```bash
rac1> mkdir /cdrom
rac1> mount -r /dev/disk/cdrom0c /cdrom
```

## 优化架构 (OFA)
