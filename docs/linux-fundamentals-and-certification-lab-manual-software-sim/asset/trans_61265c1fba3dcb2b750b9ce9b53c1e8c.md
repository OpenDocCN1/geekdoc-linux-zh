
更多信息可能会被保存到磁盘上。软限制允许用户在仅收到警告的情况下超出其限制。软限制应小于硬限制，以便用户在完全耗尽空间之前收到警告。

大多数发行版中的 Linux 操作系统会自动安装 quota 应用程序及其实用工具。quota 工具用于显示用户的磁盘使用情况以及限制。quota 应用程序使用 /etc/fstab、/home/quota.user（如有需要则创建）和 /home/quota.group（如有需要则创建）文件作为配额系统的配置文件和数据文件。

## 配置配额

配置 Linux 操作系统使用配额涉及几个步骤。第一步是更改将应用配额的文件系统的挂载选项。为了设置用户配额，必须将 usrquota 选项添加到要配置的文件系统中。为了设置组配额，请向该文件系统添加 grpquota 选项。

在第 8 章中讨论的 /etc/fstab 文件包含文件系统的挂载信息。以下对该文件的展示显示了针对 /dev/hda3 文件系统所做的更改。添加了 usrquota 选项。要为组配额添加选项，只需在该行中加上 grpquota 选项即可。

```
# cat /etc/fstab
LABEL=/              /                 ext3    defaults              1 1
LABEL=/boot           /boot             ext3    defaults              1 2
none                  /dev/pts          devpts  gid=5,mode=620        0 0
/dev/hda3             /newDrive         ext3    defaults,usrquota     1 2
none                  /proc             proc    defaults              0 0
none                  /dev/shm          tmpfs   defaults              0 0
/dev/hda5             swap              swap    defaults              0 0
/dev/cdrom            /mnt/cdrom        udf,iso9660 noauto,owner,kudzu,ro 0 0
/dev/fd0              /mnt/floppy       auto    noauto,owner,kudzu    0 0
/dev/cdrom1           /mnt/cdrom1       udf,iso9660 noauto,owner,kudzu,ro 0 0
#
```

准备好文件系统后，必须在该文件系统的根目录 (/) 中拥有一个配额数据库。一旦配额系统使用该数据库，它将不再是人类可读的格式。你只需创建一个空文件供使用即可。使用 touch 命令创建空文件。用户配额的数据库名称是 **quota.user**，组配额的名称是 **quota.group**。`touch /newDrive/quota.user` 命令在 /newDrive (/dev/hda3) 的根目录中创建 quota.user 文件。

要向刚刚创建的 quota.user 文件添加条目，请使用 **quotacheck** 命令。quotacheck 命令检查每个文件系统，构建当前磁盘使用情况的表格，并将该表格与记录在该文件系统的磁盘配额文件中的表格进行比较。如果存在差异，则会更新配额文件。默认情况下，会检查用户配额。使用 `man quotacheck` 命令可查看完整的选项列表。一些更常用的选项包括以下内容：

- **-v**   使命令产生详细的输出。
- **-a**   表示检查所有已挂载的非 NFS 文件系统。
- **-u**   使 quotacheck 明确检查用户配额。
- **-g**   使 quotacheck 明确检查组配额。

要让 quotacheck 检查所有文件系统的用户配额（默认行为）并提供详细列表，请使用以下命令：

```
# quotacheck -av
quotacheck: Scanning /dev/hda3 [/newDrive] done
quotacheck: Checked 6 directories and 18 files
#
```

系统的配额尚未实际设置，但你可以使用 **repquota** 命令查看到目前为止生成的信息。repquota 命令打印文件系统磁盘使用情况配额的摘要。它基本上使用与 quotacheck 命令相同的选项。要查看当前使用情况的报告，请使用以下命令：

```
# repquota -av
*** Report for user quotas on device /dev/hda3
Block grace time: 7days; Inode grace time: 7days
```

| 用户 | 已使用 | 软限制 | 硬限制 | 宽限期 | 已使用 | 软限制 | 硬限制 | 宽限期 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | | 块限制 | | | 文件限制 | | | |
| root | -- | 28 | 0 | 0 | | 3 | 0 | 0 |
| dangle | -- | 77608 | 0 | 0 | | 4 | 0 | 0 |
| jsmith | -- | 16740 | 0 | 0 | | 11 | 0 | 0 |
| rbrown | -- | 7092 | 0 | 0 | | 3 | 0 | 0 |
| ksmith | -- | 7092 | 0 | 0 | | 3 | 0 | 0 |

# 管理配额

配置好配额后，你需要启用配额，设置用户/组限制，并设置宽限期。启动或重新开始使用配额的命令是 **quotaon**。quotaon 命令拥有与 quotacheck 相同的可用选项。

```
# quotaon -auv
/dev/hda3: user quotas turned on
```

设置限制是通过 **edquota** 命令完成的。这将调出编辑器（默认为 vi），并显示所选用户的数值。使用 **edquota -u jsmith** 命令来编辑 jsmith 的数值。图 11-11 显示了配额表中 jsmith 的条目。

![](img/37f079cee226b270f2e09b37a2e4a05d_317_0.png)

要设置限制，请调整软限制和硬限制的值。显示的值表明软限制设置为 50 MB，硬限制设置为 75 MB。

宽限期使用带有 **-t** 选项的 edquota 进行设置。此命令会调出编辑器并允许你更改宽限期值。图 11-12 显示了宽限期值。

# 更多管理任务

**图 11-12**

![](img/37f079cee226b270f2e09b37a2e4a05d_318_0.png)

## 目标 4.13 限制用户资源限制

限制用户的磁盘空间只是 Linux 操作系统众多资源之一。**ulimit** 命令可在 bash shell 中使用，以对其它资源施加限制。可以针对一个或多个用户定义 core 文件的最大尺寸、内存使用量、打开的文件描述符以及其他值。例如，命令 **ulimit -Sc 0** 将禁用 core 转储，**ulimit -Su 100** 将设置 100 个进程的软限制，而 **ulimit -Hu 150** 定义 150 个进程的硬限制。键入 **help ulimit** 可查看 **ulimit** 可用选项的综合列表。

```
# help ulimit
ulimit: ulimit [-SHacdflmnpstuv] [limit]
Ulimit provides control over the resources available to processes started by the shell, on systems that allow such control. If an option is given, it is interpreted as follows:
-S use the 'soft' resource limit
-H use the 'hard' resource limit
-a all current limits are reported
-c the maximum size of core files created
-d the maximum size of a process's data segment
-f the maximum size of files created by the shell
-l the maximum size a process may lock into memory
-m the maximum resident set size
-n the maximum number of open file descriptors
-p the pipe buffer size
-s the maximum stack size
-t the maximum amount of cpu time in seconds
-u the maximum number of user processes
-v the size of virtual memory
```

若要使用 **ulimit** 限制单个用户的资源，请将命令包含在用户的 **.bash_profile** 文件中（注意名称开头的点）。若要限制用户最多 100 个进程，请输入以下行：

```
ulimit -H -u 100
```

若要限制所有用户为相同值，请将相同命令输入到 /etc/profile 中。

## 目标 6.4

# 高级电源管理——高级配置和电源接口

高级电源管理 (APM) 是一个应用程序接口 (API)。API 是一组例程、协议和工具，用于构建访问由较低层模块（如操作系统或 JVM）提供的服务的应用程序。APM 是由 Intel 和 Microsoft 开发的 API，使开发人员能够在 BIOS 中纳入电源管理功能。APM 在硬件和操作系统之间定义了一层，有效地屏蔽了程序员无需关心的硬件细节。

高级配置和电源接口 (ACPI) 是由 Hewlett-Packard、Intel、Microsoft、Phoenix 和 Toshiba 开发的开放行业电源管理规范。ACPI 使操作系统能够控制提供给连接到计算机的每个设备的电源量。这使得操作系统能够在未使用时关闭外围设备。ACPI 旨在取代较旧的 APM 标准，并为识别和配置硬件设备提供通用接口。

ACPI 规范于 1996 年发布。最新版本为 2.0c，3.0 规范正在开发中（参见 www.acpi.info）。最新版本扩展到了支持 64 位和 36 位寻址的计算机平台。

## 使用 APM

要使 APM 正常工作，机器中的系统 BIOS 必须支持 APM 标准。要使 APM 与 Linux 操作系统配合工作，系统 BIOS 必须至少支持 APM 版本 1.0。你可以使用 **dmesg** 命令获取有关 APM 版本或支持的信息。以下是两台不同机器的 dmesg 输出的摘录。这些输出表明第一台机器的 BIOS 不支持 APM，而第二台机器支持 APM BIOS 版本 1.2。

### 机器 #1

```
Based upon Swansea University Computer Society NET3.039
Initializing RT netlink socket
apm: BIOS not found.
Starting kswapd
```

### 机器 #2

```
Based upon Swansea University Computer Society NET3.039
Initializing RT netlink socket
BIOS version 1.2 Flags 0x03 (Driver version 1.16)
Starting kswapd
```

apm 命令告诉 Linux 操作系统如何使用电源管理功能。其语法为 **apm -options**，其中 options 是下列列出的一个或多个选项。

- `-V, --version` 打印 apm 程序版本并立即退出。
- `-v, --verbose` 打印有关 APM BIOS 版本和 Linux APM 驱动程序版本的信息。
- `-m, --minutes` 以总分钟数打印剩余时间，而不是使用 hh:mm 格式。
- `-s, --suspend` 将机器置于挂起模式。
- `-S, --standby` 将机器置于待机模式。
- `-i, --ignore` 在交流电源上忽略 APM 挂起和待机事件。
- `-n, --noignore` 在交流电源上不忽略 APM 挂起和待机事件。

通过键入 **apm -s** 进入的挂起模式，指示系统关闭大多数设备，保留 CPU 和内存运行。通过键入 **apm -S** 进入的待机模式，指示
