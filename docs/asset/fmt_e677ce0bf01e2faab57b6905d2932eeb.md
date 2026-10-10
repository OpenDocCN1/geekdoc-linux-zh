
必须是 `root` 用户才能在主机级别配置信任访问。此项配置涉及编辑 `/etc/hosts.equiv`。`/etc/hosts.equiv` 中的每个条目指定了你信任的远程系统。`root` 账户可以通过 `/etc/hosts.equiv` 中的条目等效实现。如果网络连接到互联网，出于安全考虑，请始终在该文件中使用完全限定的主机名。

## 配置信任用户访问

信任用户访问（Trusted user access）允许系统上的用户通过他们信任的另一个系统使用其账户执行 `login`、`rpc` 和 `rcmd` 命令，而无需提供密码。与信任主机访问不同，为不同机器上具有不同登录名的用户创建。

人们可以通过在用户主目录中创建或修改名为 `.hosts` 的文件，为用户配置信任用户访问，或为自己配置。其格式与 `/etc/hosts.equiv` 文件相同。

## TCP/IP 性能调优

与 TCP/IP 相关的性能问题通常是由于流量过大导致的。流量产生可能涉及多个因素：

- 物理层性能。
- 网卡性能。
- 机器性能。
- 网络负载。
- 数据损坏。
- 资源向适当节点和网络的分配。

如果网络性能看起来糟糕，上述因素的任何组合都可能是可能源。

## 数据损坏

数据可以通过多种方式被损坏：

- 通过回声。
- 电缆终止不当。
- 使用电缆扫描仪检测回声。
- 数据包传输到主机的速度快于网卡缓存数据包的速度。
- 流量增加。

网络性能问题也可能是由于物理层能力负载。诊断性能问题的工具包括 `Ping-f`。

## UNIX

使用的命令：

- `netstat -i` 列出显示所有者的文件。
- `netstat -l` 显示每个网络接口的统计信息。
- `netstat -s` 显示数据包统计。

### 网络文件系统

`NFS` 允许将一台主机上的文件系统或目录供许多其他主机使用，这些主机将磁盘空间视为自己的。

磁盘上的文件系统是如何挂载的？手动使用 `mount(ADFM)` 命令，以及在启动时通过 `/etc/default/filesys` 文件中的条目自动挂载。这相当于 Berkeley 和 System V 系统中找到 `/etc/fstab` 文件。

```
passwd=string* / 在挂载请求时提示的可选密码
time=*
fsck=yes,no, dirty, prompt
cmount=yes,no, prompt
fstype=type
nfsopts=opts
```

`mount` 命令也可用于将远程计算机的文件系统或目录挂载到本地主机的挂载点上。实现此目标必须满足两个条件：

- 两之间必须建立网络通信。
- 远程主机必须允许本地主机挂载其文件系统的权限。

`fsck` 检查文件完整性。当文件系统挂载到挂载点目录时，它会用其根目录替换挂载目录。

## 服务器配置

服务器配置涉及出服务器应该导出哪些目录以及向哪些客户端导出。查看 `/etc/exports` 文件以了解如何处理匿名 UID，并查看 NFS 服务器愿意与其他系统共享的文件系统列表以及其共享方式。启动 NFS 守护进程（daemons）的脚本是 `/etc/nfs`。如果 `/etc/export` 文件存在，该脚本将只启动必要的守护进程。通常会创建一个空的 `/etc/export` 文件，以便在将来需要 NFS 服务器时，守护进程已经在运行。然而，一个空的

## 网络文件系统性能

通过输入 `nfsstat -z` 显示 NFS 统计信息。使用 NFS 会使系统面临额外的安全风险，所有这些都是可管理且已过处理的。NFS 安全问题包括以下：

- NFS 服务器上文件系统上的 `setuid` 和 `setgid` 位。标记有 `setuid` 和 `setgid` 位的文件对通过类似方式挂载这些文件的远程系统构成了风险。

## 维护网络安全

它们物理上所在的本地系统。此外，NFS 服务器可能拥有 `setuid` 文件，你不希望这些文件在 NFS 客户端上是 `setuid` 的。因此，请确保在 `mount` 命令中指定 `nosuid` 选项。指定此标志后，NFS 将不会尊重通过 NFS 访问的文件的 `setuid` 权限。

- Root 权限。所有 NFS 操作都使用从客户端到服务器的操作所需的 UID 和 GID。但是，如果 UID 为 0（即客户端上的进程以 `root` 身份运行），这可能是危险的。因此，如果客户端上的 UID 是 `root`，NFS 通常会将 UID -2 传递给 NFS 服务器。你可以通过指定：`/etc/exports` 完全限定主机名文件强制 NFS 将 UID 0 传递给服务器。检查强制使用 UID 0 以确定其合理性。

## 网络信息服务

网络信息服务 (NIS) 为提供了一种维护整个企业网络用户等效性的简单方法，包括与管理工具的完全集成。NIS 用户应该能够回答以下问题：

- 什么是 NIS？
- 如何配置它？
- 如何管理？
- NIS 的客户端-服务器架构是什么，包括各种类型的 NIS 服务器？
- 默认可配置的 NIS 映射（maps）有哪些？
- NIS 工具有哪些？

实现 NIS 的守护进程执行什么功能？

用户等效性的重要性可能被估。随着网络规模的扩大，管理员的维护能力变得不可能。NIS 的创建是为了高效地在整个范围内维护账户信息。默认情况下，NIS 分发以下文件：

- `etc/passwd`
- `etc/group`
- `etc/auto`

此外，NIS 信息可以包含在其他相关文件中：

- `etc/exports`
- `etc/hosts`
- `etc/master`

## NIS 安全问题

NIS 为网络打开了几个潜在的大安全漏洞。通过小心，这些漏洞可以被堵住。

如果所有运行 NIS 的机器的管理账户应该是相同的。这意味着如果破解了网络上某一台机器的 `root` 密码，他们将获得网络所有机器的密码。如果任何机器允许设置

## TCP/IP 管理

TCP/IP 功能通过以下内容配置：

- `//tcp` 文件初始化 TCP/IP 环境的作用。
- `inetd` 守护进程的功能。

TCP/IP 应该进行调优以获得更好的性能。

## 审计

审计允许记录对对象的访问。生成的记录可以显示诸如用户尝试获得超过许可的权限（即，超级用户）。通过检查审计可以监控系统活动。一旦你遵循了本节中关于安装新操作系统和转换为安全（信任）系统的程序，就可以开始审计了。审计子系统允许对选定用户特定类型的活动进行审计。用户通过与其审计 ID 的关联进行审计。审计 ID（范围从 0 到 60000）保留在 `/.secure/etc/passwd` 文件中，只有超级用户可以读取。当被审计的用户登录时，其执行的任何操作（也是已选定的审计操作）都可以通过审计 ID 进行追踪。

选择你想要监控的删除操作。选择审计你选择的任何操作：

- 当操作尝试且无论成功还是失败时。
- 仅当操作尝试且失败时。
- 仅当操作尝试且成功时。
- 需要监控的活动类型为：
    - 使用识别和验证机制作为登录。
    - 文件操作如打开、删除和创建。
    - 安全相关的操作如开启和关闭审计系统以及更改密码文件。
    - 打印。

# 审计 399

## 选择审计的事件类型

为了简化待审计操作的选择，具有相似行为的系统操作被归类为名为 `事件类型` 的。选择其中一种事件类型进行审计将自动开启该类型中所有进程的审计。然而，也可以单独选择审计系统调用而无需选择其所属的事件类型。此外，也可以移除由于关联特定事件类型而被选中审计的系统调用。

图 6.5 显示了可以用于审计的事件类型（及其关联进程）。

### 图 6.5 事件类型

| 事件类型 | 操作描述 | 关联进程 |
|---|---|---|
| `Create` (创建) | 记录所有对象的（文件、目录、其他文件对象）创建 | `create(2)`, `mknod(2)`, `mkdir(2)`, `semget(2)`, `msgget(2)`, `shmget(2)`, `shmat(2)`, `pipe(2)` |
| `Delete` (删除) | 记录所有对象的（文件、目录、其他文件对象）删除 | `rmdir(2)`, `unlink(2)`, `msgsctl(2)` |
| `Moddac` (修改权限) | 记录所有对象的修改任意访问控制 | `chmod(2)`, `chown(2)`, `umask(2)`, `fchown(2)`, `fchmod(2)`, `setat(2)`, `fsetat(2)` |
| `Modadress` (修改地址) | 记录除任意访问控制以外的所有访问性修改 | `link(2)`, `unlink(2)`, `chdir(2)`, `setuid(2)`, `setgid(2)`, `chroot(2)`, `setgroups(2)`, `setresuid(2)`, `setresgid(2)`, `rename(2)`, `nmctl(2)`, `shmtd(2)`, `new uspr(1)` |
| `Open` (打开) | 记录所有文件的打开（文件打开、其他打开对象） | `open(2)`, `execve(2)`, `ptrace(2)`, `truncate(2)`, `ftruncate(2)`, `lpsched(1)` |
| `Close` (关闭) | 记录所有文件的关闭（文件关闭、其他关闭对象） | `close(2)` |
| `Process` (进程) | 记录所有对进程的操作 | `exit(2)`, `vfork(2)`, `kill(2)` |
| `Removable` (可移动) | 记录所有可移动介质事件（挂载和卸载事件） | `samount(2)`, `umount(2)`, `vfsmount(2)`, `rfa_renatun` |
| `Login` (登录) | 记录所有登录和注销 | `login(1)`, `init(1)` |
| `Admin` (管理) | 记录所有管理和特权事件 | `stime(2)`, `clone(2)`, `swapon(2)`, `setimeday(2)`, `sethisid(2)`, `setgrp(2)`, `setvent(2)`, `setaudproc(2)`, `auditswitch(2)`, `setaudit(2)`, `domainname(2)`, `reboot(2)`, `sam(1)`, `auditism(1)`, `audit(1)`, `audit(1)`, `chfn(1)`, `icsh(1)`, `passuid(1)`, `puck(1)`, `init(1)` |
| `Ipccreate` (IPC 创建) | 记录所有 `ipccreate` 事件 | `socket(2)`, `bind(2)`, `ipccreate(2)`, `ipcdest(2)` |
| `Ipcopen` (IPC 打开) | 记录所有 `ipcopen` 事件 | `connect(2)`, `accept(2)`, `ipclookup(2)`, `ipconnect(2)`, `ipcrecv(2)` |
| `Ipcclose` (IPC 关闭) | 记录所有 `ipcclose` 事件 | `shutdown(2)`, `ipcshutdown(2)` |
| `Ipcdiagram` (IPC 诊断) | 记录 `ipc` 数据事务 | `udp(7)` user data |
| `uevent 1`, `uevent 2` | 记录用户定义事件 | 参见下节“精简审计日志数据” |

## 精简审计日志数据

某些进程会调用一系列可审计的操作。为了减少收集的审计日志数据量，并在审计日志文件中提供更具意义的标记，某些进程被设计为：挂起其调用的操作的审计，并产生描述该发生进程的审计日志条目。这样编写的进程被称为 `自审计程序`。

例如，当日志程序被调用时，它会打开、读取并关闭几个文件，以收集用户登录系统所需的记录。这些进程中的每一个读取和关闭操作都可能是一个可审计的操作。然而，由于登录是一个自审计程序，审计子系统不会记录这些操作。它会在审计日志文件中创建一个条目，记录 `UserX` 已登录系统（参见图 6.6）。

以下进程具有自审计能力：

- `chfn(1)` 修改 finger 条目。
- `cssh(1)` 修改登录 shell。
- `login(1)` 登录工具。
- `newgrp(1)` 修改有效组。
- `passud(1)` 修改密码。
- `auditvent(1M)` 选择要审计的事件。
- `audisp(1M)` 显示审计数据。
- `audysys(1M)` 或停止审计系统。
- `audus(1M)` 选择要审计的用户。
- `init(1M)` 更改运行级别和用户注销。
- `lpsched(1M)` 调度行打印机请求。
- `pwck(1M)` 密码/组文件检查器。
- `sam(1M)` 系统管理管理器对某些安全相关任务执行自审计。

自审计程序对于精简系统上收集的审计数据非常有用。因此，留下了两个事件类型 `UEVENT1` 和 `UEVENT2`，供你可能想要编写的自审计程序使用。关于如何编写自审计程序的指南，请参阅下节。

图 6.6 自审计进程

![](img/e58c9dbdee5b0b2b9dfd3b7e0.png)

## 编写程序

### 审计审计

具有超级用户权限的用户可能希望编写自己的程序来精简审计。使用 `audswitch` 和 `audwrite` 调用来挂起进程的审计并生成审计记录。你可以挂起审计 (`audswitch(AUD_SUSPEND)`)，在程序的关键点生成审计记录 (`audwrite`)，然后恢复审计 (`audswitch(AUD_RESUME)`)。

#### 自审计程序

这是一个自审计程序的示例：

```c
#include <stdio.h>
#include <sys/audit.h>
void writrec();
struct self_audit_rec audrec;
main() {
    char *errmessage, *wr_string;
    int fd;
    /* 挂起此进程的审计 */
    if (audswitch(AUD_SUSPEND)) {
        fprintf(stderr,"You do not have privilege this command");
        exit(1);
    }

    /* 执行被审计的工作 */
    /* 打开测试文件 */
    if(create("test_file", 0666)==1) {
        errmessage="could not create test file\n";
        fprintf(stderr, errmessage);
        writrec(errmessage,3);
    }
    /* 向测试文件写入 "that's all folks" */
    wr_string="that's all folks\n";
    if(write(fd,wr_string,strlen(wr_string))==1) {
        errmessage="could not write to test file\n";
        fprintf(stderr,errmessage);
        writrec(errmessage,3);
    }
    /* 告诉用户我们做了什么 */
    errmessage="successfully created that's all folks\n";
    printf(errmessage);

    /* 写入审计记录 */
    writrec(errmessage,0);
}

/* 写入审计记录并退出的例 */
static void
writrec(mesg,err)
char *mesg;
int err;
{
extern struct self_audit_rec audrec;

/* 将消息拷贝到审计记录体 - audit_body.text */
strncpy(audrec.audit_body.text, mesg, MAX_AUD_TEXT);

/* 初始化审计记录头 */
/* 1. 将 ah_error 设置为返回值 */
/* 2. 将 ah_event 设置为事件类型 */
/* 3. 将 ah_len 设置为 audit_body.text 的长度 */
audrec.audit_head.ah_error = err;
audrec.audit_head.ah_event = EVENT_UEVENT;
audrec.audit_head.ah_len = strlen(mesg);

/* 恢复审计 */
audswitch(AUD_RESUME);

/* 写入审计记录 */
audwrite(&audrec);
exit(err);
}
```

注意：如果在程序运行时审计系统已关闭，`audwrite` 返回成功，但没有写入审计记录。有关如何编写自审计程序的更多信息，请参考 Unix 参考手册。

# 审计记录

对于每个审计的事件，审计日志文件中记录了以下信息：

- 事件日期。
- 生成事件的用户审计 ID。
- 主体（用户/进程）。
- 事件类型。
- 事件的成功或失败。
- 身份识别/认证事件的来源 (`tty`)。
- 从用户空间引入或删除的对象名称。
- 系统管理员对用户/系统安全数据库进行的修改描述。
- 与事件的其他信息。

## 审计日志文件

所有审计数据都写入审计日志文件。可以指定两个文件来收集审计数据：主日志文件和（可选的）辅助日志文件。这些文件应位于不同的文件系统中。审计溢出守护进程会密切监控这些文件（及其所在的文件系统）的增长，以确保不丢失审计数据。

主日志文件是开始收集审计记录的地方。当它接近预定义的容量（其审计文件切换 AFS 大小），或其所在的文件系统接近预定义的容量（其文件空间切换 FSS 大小）时，审计子系统会发出警告。当主文件的 AFS 或 FSS 时，审计子系统尝试切换到辅助日志文件记录审计数据。如果没有指定辅助日志文件，主日志文件将继续增长。图 6.7 和 6.8 显示了文件增长时发生的情况。

该示例假设：

- 只指定了主日志文件。
- 它位于没有其他用户竞争空间的的文件系统中。

主审计日志已达到其 AFS 大小的 90%。监控审计系统状态的 `Audoman` 向系统控制台显示所示警告消息。

主审计日志已通过第一个警告点并达到 AFS 大小。系统尝试切换到辅助日志文件，但由于未找到，向系统控制台发出指示消息。
