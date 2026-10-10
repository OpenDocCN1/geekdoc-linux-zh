

# 串行端口

在虚拟控制台中，你可以使用 **Ctrl-Up**、**Ctrl-Down**、**Ctrl-PageUp** 和 **Ctrl-PageDown** 在日志中上下移动。

**Ctrl-Alt** 切换鼠标和键盘抓取。

在仿真期间，如果你使用了 **-nographic** 选项，请使用 `Ctrl-a h` 获取终端命令：

- **Ctrl-a h**
  打印此帮助信息
- **Ctrl-a ?**
  打印此帮助信息
- **Ctrl-a x**
  退出模拟器
- **Ctrl-a s**
  将磁盘数据保存回文件（如果使用 -snapshot）
- **Ctrl-a t**
  切换控制台时间戳显示
- **Ctrl-a b**
  发送中断信号（在 Linux 中为魔法系统请求键）
- **Ctrl-a c**
  在控制台和监视器之间切换
- **Ctrl-a Ctrl-a**
  发送 Ctrl-a

以下选项专用于 PowerPC 仿真：

- **-g WxH[xDEPTH]**
  设置初始 VGA 图形模式。默认为 800x600x32。
- **-prom-env** *string*
  在 NVRAM 中设置 OpenBIOS 变量，例如：
  `qe-system-ppc -prom-env 'auto-boot?=false' \ -prom-env 'boot-device=hd:2,\yaboot' \ -prom-env 'boot-args=config=hd:2,\yaboot.conf'`
  这些变量不被 Open Hack'Ware 使用。

以下选项专用于 Sparc32 仿真：

- **-g WxH[xDEPTH]**
  设置初始图形模式。对于 tcx，默认为 1024x768x8，可选 1024x768x24。对于 cgthree，默认为 1024x768x8，可选 1152x900x8 供希望使用 OBP 的用户使用。
- **-prom-env** *string*
  在 NVRAM 中设置 OpenBIOS 变量，例如：
  `qe-system-sparc -prom-env 'auto-boot?=false' \ -prom-env 'boot-device=sd(0,2,0):d' -prom-env 'boot-args=linux single'`

**-M [SS-4|SS-5|SS-10|SS-20|SS-600MP|LX|Voyager|SPARCClassic] []|SPARCbook]**
设置仿真的机器类型。默认为 ss-5。

以下选项专用于 Sparc64 仿真：

**-prom-env** *string*
在 NVRAM 中设置 OpenBIOS 变量，例如：
`qe-system-sparc64 -prom-env 'auto-boot?=false'`

**-M [sun4u|sun4v|Niagara]**
设置仿真的机器类型。默认为 sun4u。

## 另请参阅

有关更详细的信息，请参见 **QEMU** 的 *HTML* 文档，以及 **Linux** 用户模式 *模拟器* 的调用方式。

# 作者

Fabrice Bellard

# QUOTA（配额）

## 名称

quota - 显示磁盘使用情况和使用限制

## 概要

```
quota [-F format-name] [-guqvswi] [-l|-Q|-A|-m]
quota [-F format-name] [-qvswi] [-l|-Q|-A|-m] -u user...
quota [-F format-name] [-qvswi] [-l|-Q|-A|-m] -g group...
quota [-F format-name] [-qvswugQm] -f filesystem...
```

## 描述

**quota** 显示用户的磁盘使用情况和使用限制。默认情况下仅打印用户配额。默认情况下，空间使用情况和使用限制以千字节显示（出于历史原因，它们被称为块）。

**quota** 报告在 **/etc/mtab** 中列出的所有文件系统的配额。对于通过 NFS 挂载的文件系统，将在服务器机器上调用 rpc.rquotad 以获取信息。

## 选项

- **-F, --format**=*format-name*
  显示指定格式的配额（即，不执行格式自动检测）。可能的格式名称包括：**vfso1** 原始配额格式，具有 16 位 UID / GID；**vfsv0** 具有 32 位 UID / GID、64 位空间使用量、32 位 inode 使用量和限制的配额格式；**vfsv1** 具有 64 位配额限制和使用量的配额格式；**rpc** （NFS 上的配额）；**xfs** （XFS 文件系统上的配额）
- **-g, --group**
  打印用户所属组的组配额。可选的 **group** 参数将显示限制为指定的组。
- **-u, --user**
  此标志等同于默认行为。
- **-v, --verbose**
  显示未分配存储空间的文件系统上的配额。
- **-s, --human-readable**
  该选项将使 **quota** 尝试为显示限制、已用空间和已用 inode 选择适当的单位。
- **--always-resolve**
  即使名称仅由数字组成，也始终尝试将用户/组名称翻译为 uid / gid。
- **-p, --raw-grace**
  当用户处于宽限期时，报告自纪元以来其宽限时间到期（或已到期）的秒数。当没有生效的宽限时间时，该字段为 ‘0’。这在通过脚本解析输出时特别有用。
- **-i, --no-automfs**
  忽略仅由自动挂载器挂载的挂载点
- **-l, --local-only**
  仅报告本地文件系统上的配额（即，忽略通过 NFS 挂载的文件系统）。
- **-A, --all-nfs**
  即使报告在同一设备上，也报告所有 NFS 文件系统的配额。
- **-f, --filesystem-list**
  仅报告在命令行上指定的文件系统上的配额。
- **-m, --no-mixed-paths**
  目前，NFSv4 挂载点的路径在没有前导斜杠的情况下发送。**rpc.rquotad** 使用此特征识别 NFSv4 挂载并适当地在路径前添加 NFS 文件系统的伪根。如果你指定此选项，**quota** 将始终发送带有前导斜杠的路径。出于兼容性原因这可能有用，但请注意，如果你使用新的 **rpc.rquotad**，通过 RPC 的配额将会停止工作。
- **-q, --quiet**
  打印更简洁的消息，仅包含使用情况超过配额的文件系统的信息。
- **-Q, --quiet-refuse**
  如果到 **rpc.rquotad** 的连接被拒绝，则不打印错误消息（通常这发生在服务器上的 **rpc.rquotad** 未运行时）。
- **-w, --no-wrap**
  如果设备名称过长，请勿换行。这在通过脚本解析 **quota** 的输出时可能有用。
- **--show-mntpoint**
  还显示挂载点作为文件系统标识。
- **--hide-device**
  在文件系统标识中不显示设备名称。

同时指定 **-g** 和 **-u** 会同时显示用户配额和组配额（针对该用户）。

只有超级用户可以使用 **-u** 标志和可选的 **user** 参数来查看其他用户的限制。非超级用户可以使用 **-g** 标志和可选的 **group** 参数来查看他们所属组的限制。

**-q** 标志优先于 **-v** 标志。

## 诊断

如果 **quota** 以非零状态退出，则一个或多个文件系统超过了配额。

## 文件

**aquota.user** 或 **aquota.group**
位于文件系统根目录的配额文件（第 2 版配额，非 XFS 文件系统）。

**quota.user** 或 **quota.group**
位于文件系统根目录的配额文件（第 1 版配额，非 XFS 文件系统）。

**etc/mtab**
默认文件系统。

## 另请参阅

**mount**(2), **mtab**(5), **rpc.rquotad**(8), **squotadm**(8), **repquota**(8), **edquota**(8), **quotaon**(8), **quotaoff**(8)。

# QUOTASYNC（配额同步）

## 名称

quotasync - 将内核中的文件系统使用情况和使用限制同步到磁盘格式

## 概要

**quotasync** [ **-ug** ] *mount-point*...
**quotasync** [ **-ug** ] **-a**
**quotasync** **-h** | **-V**

## 描述

**quotasync** 将文件系统的使用情况和限制从内核内存刷新到存储在文件系统上的配额文件中。默认情况下仅同步用户配额。如果你希望使用解析配额文件的工具（如 **repquota**(8)）显示准确的配额，此工具可能很有用。

## 选项

- **-u, --user**
  同步用户的使用情况和限制。
- **-g, --group**
  同步组的使用情况和限制。
- **-a, --all**
  同步所有文件系统上的使用情况和限制。你必须指定此选项或指定所需的文件系统。
- **-V, --version**
  显示程序版本信息并退出。
- **-h, --help**
  显示程序用法并退出。

## 诊断

如果请求的同步失败，或者给出了无效选项，**quotasync** 将以非零退出代码终止。否则它将返回零。

## 文件

**aquota.user** 或 **aquota.group**
位于文件系统根目录的配额文件（第 2 版配额，非 XFS/GFS2 文件系统）。

**quota.user** 或 **quota.group**
位于文件系统根目录的配额文件（第 1 版配额，非 XFS/GFS2 文件系统）。

**/etc/mtab**
由用户空间维护的已挂载文件系统列表。

**/proc/mounts**
由内核维护的已挂载文件系统列表。

