
# Map map for automounter

```
+auto_master
/net            -hosts -nosuid,nobrowse
/home           auto_home -nobrowse
/xfn            -xfn
/-              auto_direct
```

如前所述，`/net` 和 `/xfn` 条目引用内置映射。`/home` 条目引用间接映射 `/etc/auto_home`，而 `/-` 条目引用直接映射 `/etc/auto_direct`。

**hosts** 内置映射使用 hosts 数据库。**-xfn** 内置映射使用通过联邦命名服务 (FNS) 共享的资源。

## 直接映射 (Direct Maps)

直接映射同时提供挂载点和 NFS 资源。直接映射中的条目由三个字段组成：

- **键（Key）**——通常用作挂载点的完整路径。
- **挂载选项（Mount options）**——零或多个（用逗号分隔）的 NFS 特有挂载选项，如前文表 18.3 所示。
- **NFS 资源（NFS resource）**——格式为 `server:file system` 的文件，标识由系统服务器共享的文件系统。多个 NFS 服务器提供相同的资源，可以指定多个资源（空格分隔）。使用第一个可用资源。

以下列表显示了 `/etc/auto_master` 文件中引用的 `/etc/auto_direct` 文件的内容：

```
/usr/local/bin    nsserver:/usr/local/bin
/usr/games      ro  nsserver:/usr/games
```

在此示例中，名为 **nsserver** 的主机共享的 `/usr/local/bin` 和 `/usr/games` 目录挂载在本地系统的同名挂载点。

初始直接映射的默认名称为 `auto_direct`。

## 间接映射 (Indirect Maps)

间接映射同时提供挂载点和 NFS 资源。间接映射中的条目由三个字段组成：

- 键（Key）——通常用作挂载点的完整路径。
- **挂载选项（Mount options）**——零或多个（用逗号分隔）的 NFS 特有挂载选项，如前文 18.3 所示。
- **NFS 资源（NFS resource）**——格式为 `server:file system` 的文件，标识由服务器共享的文件系统。

以下列表显示了 `/etc/auto_home` 文件的内容：

```
dla          solaris:export/home
guest      -rw,nosuid nsserver:/export/guest
```

在此示例中，间接映射被 `auto_master` 文件引用。它包含两个条目。第一个条目标识 dlaa，通过 solaris 挂载 `/export/home`；第二个条目标识 guest，通过 nsserver 挂载 `/export/guest`。

## 运行 automount 命令

对 AutoFS 映射进行更改时，可能需要手动执行 `automount` 命令以生效。当对直接映射进行添加或删除时，也执行该命令。

## 缓存文件系统服务

缓存文件系统 (CacheFS) 是一种客户端服务，用于在 NFS 客户端上缓存远程访问的 NFS 资源。这不仅可以加快数据访问速度，还可以减少网络流量和 NFS 服务器的负载。

创建缓存后，可以将远程 NFS 资源挂载到缓存中。第一次访问 NFS 资源时，数据从远程 NFS 服务器复制到本地缓存。后续访问将从本地缓存而非远程服务器进行。

注意根 (`/`) 和 `/usr` 文件无法被 CacheFS 机制缓存。然而，这两个文件可以通过 AutoClient 配置进行缓存，见第 13 章。

## 配置缓存

`fsadmin(1M)` 命令用于创建、检查、调整和删除缓存。`cachefsstat(1M)` 命令也可显示缓存统计信息。

你指定 `-c` 命令行参数创建缓存，后跟用于缓存的目录完整路径。此外，可以使用 `-o` 命令行参数指定多个选项（用逗号分隔）。以下使用 `fsadmin` 命令在 `/cache` 目录下创建一个缓存。可缓存的最大文件大小设置为 10MB：

```
# fsadmin -c -o maxfilesize=10 /cache
```

要列出挂载在缓存中的文件系统和缓存状态，请使用 `-l` 命令行参数。其他命令行参数还包括 `-s` 执行一致性检查、`-u` 更新缓存参数以及 `-d` 删除缓存。所有这些命令行参数后面都应该紧跟缓存目录的完整路径。

使用 `mount` 命令在缓存中挂载 NFS 资源，需要指定远程文件系统、本地缓存和本地挂载点。

应使用 `-F` 命令行参数来标识文件系统类型为 CacheFS。此外，必须使用 `-o` 命令行参数指定至少两个缓存特定的选项：`backftype`（用于识别正在挂载并被缓存的文件类型，通常为 NFS）和 `cachedir`（用于识别缓存目录）。以下列表使用 `mount` 命令管理从主机 `sparc20` 挂载到 `/home` 挂载点的 `/export/home` 文件系统（下文统称为该文件系统），并使用 `/cache` 作为缓存目录。为了提高可读性，该行进行了换行处理：

```
# mount -F caches -o backftype=nfs,cachedir=/cache
sparc20:/export/home /home
```

## 检查缓存状态

要显示缓存文件系统的状态，请使用 `cfsadmin` 命令并指定 `-l` 命令行参数，后跟缓存名称。

显示以下关于缓存的信息：

- maxblocks——缓存可以使用的最大存储空间（以前端文件系统块的百分比表示）。
- minblocks——缓存可以使用的最小存储空间（以前端文件系统块的百分比表示）。
- threshblocks——达到 minblocks 后无法再获取额外资源的阈值（以前端文件系统块的百分比表示）。
- maxfiles——缓存可以使用的最大文件数（以前端文件系统块的百分比表示）。
- minfiles——缓存可以使用的最小文件数（以前端文件系统块的百分比表示）。
- threshfiles——达到 minfiles 后无法再获取额外 inode 的阈值（以前端文件系统 inode 总的百分比表示）。
- maxfilesize——缓存中允许的最大文件大小。
- mount info——正在被挂载的资源及其本地挂载点。斜杠（/）字符显示为下划线（_）字符。

可以使用 `cfsadmin -u` 命令修改最大、最小和阈值参数。以下列表使用 `cfsadmin -l` 命令显示缓存状态：

```
# cfsadmin -l /cache
cfsadmin: list cache FS information
maxblocks 90%
minblocks 0%
threshold 85%
maxfiles 90%
minfiles 0%
thresholdfiles 85%
maxfilesize 3MB
sparc20:export_home:_home
#
```

## 显示缓存统计数据

要显示缓存文件系统的性能统计信息，请使用 `cachefsstat(1M)` 命令并指定缓存文件系统的挂载点。

显示以下关于缓存文件的统计信息：

- cache hit rate——在缓存文件系统中查找文件或目录的尝试成功百分比，随后是实际命中和未命中的计数。
- consistency checks——执行一致性检查次数，随后是通过和失败检查的计数。
- modifies——修改操作次数。
- garbage collection——回收不再使用的尝试次数。

以下列表使用 `cachefsstat` 命令显示缓存文件系统统计数据：

```
# cachefsstat /home
/home
cache hit rate: 57% (8 hits, 6 misses)
consistency checks: 14 (14 pass, 0 fail)
modified: 0
garbage collection: 0
#
```

请注意，`cfsadmin -l` 命令报告的是缓存的配置状态（可调参数），而 `cachefsstat` 的是缓存的内容（缓存文件系统统计数据）。

## 检查缓存的一致性

为了确保缓存中的信息是最新的，会自动执行定期一致性检查。这些检查可能会产生大量的网络活动。为了减少网络流量，您可以禁用自动一致性检查并手动（按需）检查一致性。

禁用自动一致性检查（即请求按需一致性检查），在挂载文件系统时指定 `demandcost`。为了提高可读性，该行进行了换行处理。

```
# mount -F cachefs -o backype=nfs,cachedir=/cache,demandconst
sparc20:/export/home /home
#
```

要按需执行一致性检查，请使用 `cfsadmin -s` 后跟缓存文件系统的挂载点作为命令行参数：

```
# cfsadmin -s /home
#
```

## 管理缓存日志

`cachelog(1M)` 命令用于设置、验证和停止 CacheFS 日志。`cachefwssize` 命令用于分析日志，以确定缓存的建议工作集大小。缓存太小会导致访问延迟和更高的网络流量（低命中率）。缓存太大则会浪费文件系统空间。

要设置 CacheFS 日志，请使用 `cachelog` 命令并配合 `-f` 命令行参数，后跟日志文件名以及缓存文件系统挂载的目录名称（即缓存本身的名称）。例如，设置一个名为 `var/tmp/home` 的日志：

```
# cachelog -f var/tmp/home /home
```

要验证日志记录，使用 `cachelog` 命令并指定缓存文件系统的挂载点：

```
# cachelog -v /home
```

要停止日志记录，使用 `cachelog` 命令配合 `-h` 参数，后跟缓存文件系统的挂载点：

```
# cachelog -h /home
```

确定缓存的大小，使用 `cachefwssize` 命令配合日志文件：

```
# cachefwssize /var/tmp/home
```

停止时的结束大小和高水位大小（最大大小）会显示每个文件系统。初始大小包含缓存。如果高水位大小等于初始大小，则缓存太小。如果高水位大小远小于初始大小，则缓存可能太大。

## 练习题

### 题 1

以下哪个命令可以将来自 Solaris 系统（IP 地址为 192.168.0.7）的 `/export/home` 文件系统挂载到 `/mnt` 挂载点？

- a. `mount -F nfs -h /export/home /mnt`
- b. `mount -F nfs 192.168.0.7:/export/home /mnt`
- c. `mount -F nfs /mnt solaris:/export/home`
- d. `mount -F nfs /export/home@solaris /mnt`

答案 b 正确。第一个参数应该是主机或 IP 地址。其他答案均未使用正确的语法。因此，答案 a、c 和 d 都是错误的。

### 题 2

用于在本地磁盘临时存储远程 NFS 资源的文件系统名称。

正确答案是 CacheFS。

### 题 3

哪些是 AutoFS 映射的类型？多选题

- a. direct（直接）
- b. indirect（间接）
- c. linked（链接）
- d. auto_master
- e. auto_home

答案 a、b 和 d 正确。直接、间接和 auto_master 是 AutoFS 映射的类型。linked 名称与 AutoFS 功能无关。因此，答案 c 是错误的。auto_home 是间接映射的常用名称。因此，答案 e 是错误的。

### 题 4

在以下哪种情况下，必须手动执行 `automount` 命令？[选择所有适用项]

- a. 向 `auto_master` 添加条目
- b. 从 `auto_master` 中删除条目
- c. 从直接映射中删除
- d. 向直接映射添加条目
- e. 向间接映射添加条目
- f. 从间接映射中删除

答案 a、b、d 和 e 正确。在 `auto_master` 或直接映射中添加或删除后，必须手动执行 `automount`。间接映射的更改不需要运行 `automount` 命令。因此，c 和 f 是错误的。

### 题 5

使用以下哪个命令来创建 CacheFS 配置？

- a. `cachefsadm`
- b. `cachefsinit`
- c. `cachefsadmin`
- d. `newcache`
- e. `cachefscreate`

答案 c 正确。`cachefsadm` 命令创建 CacheFS 配置。其他命令均不存在。因此，答案 a、b、d 和 e 是错误的。

### 题 6

识别用于使 NFS 资源可用供挂载，或列出已可用的资源的命令。

正确答案是 `share`。

### 题 7

将每个命令与其操作进行匹配：

- a. `cachefssize` 1. 显示缓存文件系统统计信息
- b. `cachelog -h` 2. 显示缓存状态
- c. `cachelog -f` 3. 显示缓存工作集大小
- d. `cachefsstat` 4. 开始缓存日志
- e. `cachefsadm -l` 5. 停止缓存日志

答案 a-3、b-5、c-4、d-1 和 e-2 正确。`cachefssize` 命令显示缓存工作集的大小。对于 `cachelog` 命令，`-h` 停止日志，`-f` 开始日志。

`cachefsstat` 命令显示与缓存内容相关的统计信息，而 `cfsadmin -l` 显示缓存本身的状态。

### 题 8

可以使用以下哪个命令确定任何已挂载的 NFS 资源？[选择所有适用项]

- a. `share`
- b. `dfmounts`
- c. `nfsmounts`
- d. `mount`

答案 b 和 d 正确。你可以使用 `dfmounts` 和 `mount` 命令确定任何已挂载的 NFS 资源。`share` 用于共享 NFS 资源。因此，答案 a 是错误的。`nfsmounts` 不存在。因此，答案 c 是错误的。

### 题 9

在使用 NFS 时，以下哪些结果是正确的？[选择所有适用项]

- a. 引入冗余
- b. 提高一致性
- c. 减少管理工作
- d. 减少网络流量

答案 b 和 c 正确。使用 NFS 可以提高一致性并减少管理工作。NFS 通过为多个客户端提供数据的单份副本来消除冗余。因此，答案 a 是错误的。NFS 是一个网络应用程序，使用它会增加网络流量。因此，答案 d 是错误的。

### 题 10

识别在 `share` 命令的命令行参数 `-o` 中用于更改公共文件句柄的 NFS 特定选项。

正确答案是 `public`。

### 题 11

哪个文件包含与 `shareall` 命令一起使用的一个或多个 `share` 命令？

- a. `/etc/nfs/stab`
- b. `/etc/nfs/shares`
- c. `/etc/dfs/dfstab`
- d. `/etc/dfs/sharetab`

答案 c 正确。`/etc/dfs/dfstab` 文件包含与 `shareall` 命令一起的一个或多个 `share` 命令。`/etc/nfs/stab` 和 `/etc/nfs/shares` 文件不存在。因此，答案 a 和 b 是错误的。`/etc/dfs/dfstab` 是包含共享资源信息的文件。因此，答案 d 是错误的。

### 题 12

命令 `fsadmin -s xyz` 执行失败。以下可能的原因是什么？

- a. xyz 是一个挂载点。它应该是缓存名称。
- b. 在挂载 xyz 时没有指定 `demandconst` 选项。
- c. 日启动缓存日志。
- d. 缓存的大小太小。

答案 b 正确。`fsadmin -s xyz` 命令失败可能是因为在挂载 xyz 时没有指定 `demandconst` 选项。`xyz` 必须是一个挂载点，而不是缓存名称。因此，答案 a 是错误的。`-s` 命令行参数执行一致性检查；与日志或缓存大小无关。答案 c 和 d 是错误的。

# 了解更多？

Stern, Hal, Managing NFS and NIS (O'Reilly & Associates, Sebastopol, CA, 1991), ISBN 0-937175-75-7.

Sun Micros, System Administration Guide, Volume 1. 有印刷版（部件号 805-7228-10），可在 Web 端 docs.sun.com 查看，以及通过 Solaris 8 操作系统提供的在线文档 AnswerBook2。

Sun Micros, System Administration Guide, Volume 3. 有印刷版（部件号 806-0916-10），可在 Web 端 docs.sun.com 查看，以及通过 Solaris 8 操作系统提供的在线文档 AnswerBook2。

Sun Microsystems, System Reference Manual, Section 1M - Administration Commands. 有印刷版（部件号 806-0625-10），可在 Web 端 docs.sun.com 查看，以及通过 Solaris 8 操作系统提供的在线文档 AnswerBook2。

Sun Microsystems, System Reference Manual, Section 4 - File Formats. 有印刷版（部件号 806-06333-10），可在 Web 端 docs.sun.com 查看，以及通过 Solaris 8 操作系统提供的在线文档 AnswerBook2。

Solaris 提供的 DNS 服务器是 8.1.2 伯克利互联网命名域名（BIND）程序，称为 Internet 名称守护进程（in.named）。

命名空间的信息存储在文本文件中，使用称为“记录”（records）的预定义语法。in.named 程序使用以下数据文件：

- `/etc/named.conf`——BIND 配置文件，用于标识 DNS 服务器具有权威性的区域以及相关的数据文件。
