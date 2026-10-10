
#### 用户文件系统

在确定你能提供的资源级别之后，以可以在软件控制下轻松管理的方式构建物理资源。如果你的用户群在不断变化，你可能希望将用户`/home`文件系统与操作系统的其余部分隔离开来。这将使这些文件系统与操作系统升级和维护隔离开来。在不同的物理磁盘和卷组上设置用户文件系统。如果情况需要，这将便于在机器之间移动它们。使用用户文件系统挂载点的命名约定，使其易于记忆和识别。一种可能的方法是使用`/home<number>-<scheme on ADX>`。在分布式或集群环境中，你可能可以使用拥有该文件系统的机器名称的首字母后跟一个整数。不要太长！

为了减少在多个用户文件系统中管理用户主目录的影响，使用符号链接将每个文件系统中的顶级用户目录链接到通用的`/home`目录。无论特定用户的主目录物理位于何处，都可以通过`/home/<user name>`路径访问。在`/etc/passwd`文件中，也指定主目录字段的符号链接路径名称。这将允许你在用户文件系统中移动用户目录以平衡使用率，而无需每个用户学习新的主目录路径。

```
# In -a /etc/stimp y /home/stimp y
stimp y!: :1234: 30: Stimp son_ Cat: /home/stimp y: bin / ksh
```

你还需要确定用户文件系统的大小。如果很少使用大文件，则可能更倾向于多个小文件系统。小文件系统（小于`1GB`）会减少备份和恢复时间。它们可以轻松移动，并将你的用户访问社区分区，使得文件系统灾难不会影响你的整个用户群。

如果你没有大量分布式用户群，那么默认的`/home`文件系统就足够了。取决于用户在其主目录中执行的操作和存储的内容，`/home`可能会迅速增长，特别是在开发和生产支持环境中。偶尔，用户社区需要审查存储在`/home`中的内容是合适的。如你所知，大多数计算机用户是“松鼠”，必须保留所有内容的备份副本，但他们通常更频繁地使用`/home`进行此存储。当然，磁盘空间很便宜，因此你可能只希望将`/home`变成一个巨大的文件系统，让用户拥有他们想要的所有磁盘空间。这种需求因环境而异。

### UID 空间和组

用户账户名称实际上是`UNIX`下识别用户的人类便利性事项。`AIX`操作系统通过一个称为`UID`的无符号长整数来识别特定用户。`UID`映射到`/etc/passwd`文件中的用户名称。其他`UNIX`系统使用`UID`，但可能以其他整数格式表示。

将你的用户`UID`空间与系统守护进程的管理账户使用的`UID`隔离开来是个好主意。这简化了为会计和安全应用程序识别特权账户的任务。选择一个数字，如`1000`，来定义你的用户`UID`空间的底部用于分配。`UID`的一致性极其

在用户拥有多个机器账户的环境中，这一点尤为重要。一些示例包括`HACMP`集群（`HACMP`代表`High Availability Cluster Multi-Processing`；详情参见第 28 章）；在分布式环境中，或者如果您正在使用网络文件系统（`NFS`），您必须确保`UID`在所有系统中保持一致。*这里的一致*是指，如果用户`"stimpoy"`在主机 A 上是`UID 1234`，那么在系统中的其他任何地方，都应为`stimpoy`保留相同的`UID`。如果在集群、分布式和`NFS`环境中，相同的`UID`代表不同的用户，可能会出现所有权和权限问题。请记住，操作系统通过`UID`而不是用户名来识别用户。

在定义`UID`空间时，规划组 ID (GID) 空间也是一个好主意。组提供了在用户之间共享信息的粗粒度机制。文件和目录权限为所有用户（`world`）、组（`group`）和所有者（`owner`）提供读取、写入和执行权限。`AIX`和其他`UNIX`版本假定使用有限的组集合来实现访问权限。需要决定的是，您是否希望为特定的工作组或协作者实施其他`GID`集合。如果您的用户基数较小，这可以相对容易地完成。对于大量用户，管理`GID`集合可能是一项艰巨的任务。

## /etc/group 和 /etc/security/group 文件

所有`GID`映射都维护在`/etc/group`和`/etc/security/group`文件中。`/etc/group`文件列出了每个组名称和`GID`，后跟成员列表或用户名。`/etc/security/group`文件为`/etc/group`文件中的每个组名称包含一个段落，指示该组是否允许由除`root`以外的用户进行管理，并通过用户名称识别管理员。组及其相关属性通过`SMIT`或`WebSM`进行管理，或者通过此处列出的一系列组管理命令进行管理：

```text
mkgroup        - 创建新组
chgrp         - 更改组属性
lsgr          - 列出组及其属性
chggrpm       - 更改组的管理员或成员
setgrps       - 重置用户当前的组集
newgrp        - 为会话设置组 ID
rmgr          - 删除组
```

下面是一些示例。第一个文件是`/etc/group`的示例；第二个文件是`/etc/security/group`的示例。

### /etc/group 文件示例

```text
system::0:root,ops
daemon::1::
bin::2:root,bin
sys::3:root,bin,sys
adm::4:bin,adm,kenn,root
user:!:5:uucp
mail:!:6:
security:!:7:root
cron:!:8:root
staff:!:10:root,ren,stimpy,daffy,huey,dewey
user:!:30:luge,acadmus,gw9neira,bungi
```

### /etc/security/group 文件示例

```text
system:
     admin = true
daemon:
     admin = true
bin:
     admin = true
sys:
     admin = true
adm:
     admin = true
uucp:
     admin = true
mail:
     admin = true
security:
     admin = true
cron:
     admin = true
staff:
     admin = false
     adma = ren,stimpy
user:
     admin = false
```

## 资源限制

您打算给每个用户多少份额？如何确保每个用户都不超过其公平份额？通过对应用组合进行剖析并估计并发用户数，您将得到一些大致数值。`AIX`提供了通过操作系统控制对每个用户可用的系统资源份额实施限制的功能。可以基于每个进程定义`CPU`、内存和磁盘利用率的上限。每个用户的并发进程总数由内核配置参数封顶。聚合文件系统使用情况可以通过在用户和组级别激活磁盘配额来管理。

### /etc/security/limits 文件

内核使用`setrlimit()`、`getrlimit()`和`vlimit()`系统调用管理每个进程的限制。每个进程都有一个相关的`rlimit`结构，该结构指示每种资源类型的软限和硬限。`rlimit`结构定义在`/usr/include/sys/resource.h`中。系统和用户的默认及资源限制在`/etc/security/limits`文件中指定。系统中定义的每个用户都由一个以用户名为标识的段落表示。对于没有覆盖用户段落下参数的每个用户，系统默认值是有效的。当进程超过指定的任一限制时，它将被终止。请查看这里的`/etc/security/limits`示例文件：

#### /etc/security/limits 文件示例

```text
*
* 尺寸以 512 字节块为单位，CPU 时间以秒为单位
* fsize - 软文件块数
* core - 软核心文件块数
* cpu - 软每进程 CPU 时间限制（秒）
* data - 软数据段块数
* stack - 软栈段块数
* rss - 软实际内存使用量（块）
* fsize_hard - 硬文件块数
* core_hard - 硬核心文件块数
* cpu_hard - 硬每进程 CPU 时间限制（秒）
* data_hard - 硬数据段块数
* stack_hard - 硬栈段块数
* rss_hard - 硬实际内存使用量（块）
*
* 下表包含如果未显式定义硬值时的默认硬值：
*
* 属性       值
* =========       =========
* fsize_hard      设置为 fsize
* cpu_hard        设置为 cpu
* core_hard       -1
* data_hard       -1
* stack_hard      -1
* rss_hard        -1
*
* 注意：值为 -1 意味着“无限制”
*

default:
		fsize = 2097151
		core = 2048
		cpu = -1
		data = 262144
		rss = 65536
		stack = 65536

root:
daemon:
bin:
sys:
adm:
uucp:
guest:
nobody:
lpd:
stmpy:
		fsize_hard = 10240
		cpu_hard = 3600
muucp:
```

内核根据内核配置参数`maxproc`限制每个用户的最小进程数。默认值`40`表示给定用户最多可以并发运行`40`个进程。通过多次登录系统不会超过此值。可以使用`SMIT`、`WebSM`或`chdev`命令更改`maxproc`的值（见图 20-1 中的`SMIT`面板）。

```text
# chdev -l sys0 -a maxproc=80
# smit chgys
```

![](img/82f851021955589d82b22750fb3b1646_454_0.png)

**图 20-1.** 更改/显示操作系统特性`SMIT`面板

磁盘配额限制用户或组在参与配额的文件系统中可能消耗的最大块数。`AIX`的磁盘配额实现基于`BSD`配额。系统管理员使用`edquota`命令设置用户和组的配额限制。磁盘块和`i-nodes`的配额限制由三个参数指定：软限制、硬限制和宽限期。用户可以在默认的一周宽限期内超过软限制。当宽限期结束时，软限制变为硬限制。

软限制的值指示用户或组开始收到软限制已超出的警告，并且硬限制即将接近的时间点。警告在登录时以及每次超出指定限制的关闭时提供。硬限制指定用户或组将不再能够分配额外磁盘空间或`i-nodes`的时间点。宽限期定义了一个时间段，在此期间用户或组必须将使用率降低到软限制值以下。如果在使用率未降低的情况下宽限期结束，软限制将作为硬限制强制执行。

要在文件系统中实施磁盘配额，请使用`chfs`命令编辑与文件系统名称关联的`/etc/filesystems`中的段落条目。在段落中添加参数`quota=<userquota>,<groupquota>`。`userquota`和`groupquota`值指示要强制执行的配额类型。每个用户或组的配额限制记录在名为`quota.user`或`quota.group`的顶级目录中的文件中。您可以通过在文件系统段落中包含`userquota=<pathname>`和`groupquota=<pathname>`参数来覆盖这些文件名。

使用以下命令将段落条目添加到`/etc/filesystems`：

```text
# chfs -a 'quota=userquota' -a 'userquota=/home1/user.quota' /home1
```

使用以下`more`命令检查`/etc/filesystems`段落：

```text
# more /etc/filesystems
/home1:
    dev = /dev/lv43
    vfs = jfs
    log = /dev/loglv00
    mount = true
    check = true
    options = rw
    quota = userquota
    userquota = /home1/user.quota
```

如果文件系统中不存在配额限制文件，您可以使用`touch`创建它们。

```text
# touch /home1/quota.user
```

使用`edquota`命令为系统中的某个用户创建用户配额。这些值可以作为模板用于设置系统中其他用户的限制。`edquota`命令将调用由环境变量`EDITOR`指定的默认编辑器，并显示配额值以供更新。

```text
# edquota stimpys
Quotas for user stimpys:
/home1: blocks in use: 50, limits (soft = 80, hard = 100)
    inodes in use: 11, limits (soft = 120, hard = 150)
/home2: blocks in use: 0, limits (soft = 80, hard = 100)
    inodes in use: 0, limits (soft = 120, hard = 150)
```

设置默认用户的软限制和硬限制后，调用`edquota -p <default-user> <new-user>`为系统中的每个额外用户克隆默认限制。

```text
# edquota -p stimpys ren
```

要启用配额系统，请执行`quotaon`命令。作为夜间系统维护的一部分，请通过运行`quotacheck`命令更新配额文件中的信息。可以使用`-a`标志来指示所有配额文件系统。以下是配额更新命令：

```bash
# quotaoff -a      <---- 关闭所有文件系统的配额
# quotacheck -a    <---- 更新所有文件系统的配额信息
# quotaon -a       <---- 开启所有文件系统的配额
```

分别使用`quota`和`repquota`命令可以显示用户或汇总的配额限制，如下所示：

```bash
# quota ren
用户 ren (uid 4084) 的磁盘配额：
文件系统 块配额 限制 宽限期 文件配额 限制 宽限期
/home1 11836* 5120 6144 none 363 1000 2000
```

```bash
# repquota -u -a
用户 块限制 文件限制
已用 软限制 硬限制 宽限期 已用 软限制 硬限制 宽限期
root -- 31448 0 0 0 700 0 0
bin -- 57700 0 0 0 2037 0 0
sys -- 4 0 0 0 1 0 0
bi1bro -- 16 0 0 0 4 0 0
```

## 用户账户访问权限

谁获得账户，他们可以保留多久？访问和过期策略对于小型工作组来说可能看起来无关紧要；然而，歧义越少越好。如果将这些策略正式化并公开，还可以避免法律层面的影响。如果在大型用户群系统中明确定义了过期策略，就可以轻松自动化地实现账户过期和清理。`AIX`提供了一套机制用于使账户过期并执行清理维护工作。通过提供这两种功能，`AIX`允许你实施宽限期，即在账户过期与其实际从系统中移除之间的时间段。这可以纳入最后使用策略中。

## 用户账户环境

系统将向新用户呈现什么样的面貌？作为系统管理员，您负责为每个新账户设置默认环境。您希望在环境参数上保持一定程度的控制，但也希望允许用户自由定制自己的工作空间。`Shell`、编辑器、终端定义等属于信仰问题，最好留给信仰者！您无法阻止所有人自伤。您也不想打开水闸，导致支持超出能力的`Shell`环境数量。您可以提供一个简单、模块化的登录环境，当冒险的用户进行`Shell`实验失败时，可以简化恢复过程。

首先，为所有用户定义默认的环境变量。环境变量是`name=value`对，由`Shell`和命令读取以设置值或确定行为。例如，环境变量`EDITOR`指示应用程序应调用哪个编辑器。环境变量可能是命令或`Shell`特定的，并且可以由最终用户修改。表 20-1 列出了常见环境变量的列表。

要查看环境变量的当前值，使用`echo`或`print`，并在变量名前加美元符号，如下所示：

```bash
# echo $MANPATH
# print $MANPATH
```

### /etc/environment 和 /etc/profile 文件

`AIX`提供两个文件用于设置系统默认环境变量。`/etc/environment`文件包含由`exec()`系统调用为每个进程设置的默认变量。`/etc/profile`文件包含用户登录系统时将调用的环境变量和命令集。这些文件的内容在本地`Shell`启动文件之前读取，最好保持非`Shell`特定的特性。`AIX`提供的`/etc/environment`和`/etc/profile`文件为定制自己的默认设置提供了良好的基础。此处查看默认的`/etc/environment`文件。

| 变量 | 用途 |
| :--- | :--- |
| `PATH` | 搜索命令和文件的目录路径列表 |
| `LIBPATH` | 用于绑定的库路径列表 |
| `MANPATH` | 搜索 man 页文件的目录路径列表 |
| `PAGER` | 默认全屏幕分页器 |
| `EDITOR` | 默认编辑器 |
| `TZ` | 时区 |
| `TERM` | 终端类型 |
| `MAIL` | 传入邮件路径 |
| `MAILMSG` | 新邮件到达时的消息文本提示 |
| `LANG` | NLS 生效的本地名称 |
| `LOCPATH` | 包含本地文件的目录 |
| `NLSPATH` | NLS 目录的完整路径 |
| `USER` | 用户名 |
| `LOGNAME` | 用户名 |
| `HOME` | 主目录路径 |

表 20-1. 常见环境变量

### 默认系统 /etc/environment 文件
