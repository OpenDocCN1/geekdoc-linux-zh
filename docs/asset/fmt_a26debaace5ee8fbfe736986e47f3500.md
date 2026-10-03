
# 考试答案解析

## 问题 42

答案 c 是正确的。`/etc/defaultdomain` 文件用于存储默认系统域。如果使用了此文件，则不需要在每次重启后重新定义域名。因此，答案 a 是错误的。`domainname` 命令不支持 `-p` 命令行参数。因此，答案 b 是错误的。

## 问题 43

答案正确。`bootparams` 文件包含一个为网络/安装客户端提供启动、根分区和交换区的服务器（及路径）列表。其中一个包含网络客户端的以太网地址和关联主机名。因此，答案 b 错误。网络客户端时区信息。因此，答案 c 错误。hosts 系统文件包含系统主机名和 IP 地址。因此，答案 d 错误。`fstab` 包含要自动挂载的文件系统列表。因此，答案 e 错误。

## 问题 44

正确答案是 Web-NFS。

## 问题 45

答案 c 正确。`fsck` 命令用于检查和修复文件系统。`mount` 命令用于挂载文件系统。因此，答案 a 错误。`newfs` 命令用于在格式化后创建文件系统。因此，答案 b 错误。`format` 命令用于格式化文件系统。因此，答案 d 错误。

## 问题 46

答案 d 正确。NFS 服务器程序在运行级别 3 启动。运行级别 0 是电源状态；在此状态下服务正在关闭。因此，答案 a 错误。运行级别 4 用于管理，不允许用户访问系统。因此，答案 b 错误。除 NFS 服务器外，所有网络服务都在运行级别 2 启动。因此，答案 c 错误。运行级别 6 是重启状态，系统正在重启。因此，答案 e 错误。

## 问题 47

答案 a、b、c 和 d 都正确。从最小到大，软件组为：终端用户支持、开发者系统支持、整个发行版以及 OEM 系统支持。

## 问题 48

正确答案是 Solaris Management Console。

## 问题 49

答案 c 和 d 正确。Volume Manager 包括性能分析工具和动态在线调优，而 DiskSuite 不包括。Volume Manager 和 DiskSuite 都提供图形管理工具和命令行实用程序。因此，答案 a 和 b 错误。

## 问题 50

正确答案是 `-b`。

## 问题 51

正确答案是 `/etc/syslog.conf`。

## 问题 52

答案 c 正确。AdminSuite 包含用于管理网络客户端的主机管理器，而不是网络客户端管理器。数据库管理器、存储管理器和串口管理器都包含在 AdminSuite 中。因此，答案 a、b 和 d 错误。

## 问题 53

答案 d 正确。`/etc/dfs/sharetab` 文件应包含当前共享的 NFS 资源。答案 a 和 b 中的文件不存在。`/etc/dfs/dfstab` 文件包含在系统启动或使用 `shareall` 命令时应自动共享的资源。因此，答案 c 错误。

## 问题 54

答案 a 正确。路径 `/dev/dsk` 与标准 Solaris 文件系统关联。`/dev/vx/dsk` 与 Volume Manager 虚拟文件系统关联。因此，答案 b 错误。`/dev/md/dsk` 与 DiskSuite 虚拟文件系统关联。因此，答案 c 错误。答案 d 中的路径不存在。

## 问题 55

正确答案是 syslog 或 syslog。

## 问题 56

答案 a、b、c 和 d 都正确。这些关键词都可以在配置文件中定义。`install_type` 关键字必须定义，且必须是配置文件中的第一个条目。

## 问题 57

答案 b 正确。Intel 客户端通常从本地软磁盘或本地 CD-ROM 获取启动镜像。只有 SPARC 客户端使用 TFTP 获取启动镜像。因此，答案 a 和 c 错误。Intel 客户端可以配置使用远程加载（RPL）。子网对 TFTP 的使用没有影响。因此，答案 d 错误。

## 问题 58

答案 a-4、b-5、c-1、d-2 和 e-3 正确。TCP/IP 网络模型从高到低层为：应用层、传输层、网络层、数据链路和物理层。

## 问题 59

答案 a 正确。应指定只读（ro）NFS 挂载选项以设置故障转移。因此，答案 b、c 和 d 错误。

## 问题 60

正确答案是 root。`root=list` 命令行参数用于指定具有 root 权限的客户端列表。

## 问题 61

答案 b、c 和 d 正确。`swap` 命令用于添加、列出和删除交换空间。`mkfile` 命令用于创建交换空间。因此，答案 a 错误。

# 备习指南

本备习指南包含了关于 Solaris 8 系统管理员考试的精炼关键事实。在进入考场前最后回顾这些信息，特别关注你最需要复习的领域。你可以在考试开始前将这些事实中的任何内容写在空白纸上。

## 第一部分：安装与维护

### 1. 软件分发

- 软件组——核心、终端用户支持、开发者系统支持、整个发行版、整个 Plus OEM 支持。
- 簇是包的集合；包是安装程序或产品；补丁是修复问题的更新软件。
- `pkgadd` 安装包，`pkgrm` 删除包，`pkginfo` 列出所有已安装包。默认目录为 `/var/spool/pkg`。也可以使用 `admintool` 安装包。
- `patchadd` 安装补丁，`patchrm` 删除补丁，`showrev -p` 列出所有已安装补丁。

### 2. 在线参考

- `swap` 命令用于添加、列出和删除交换空间。`mkfile` 命令用于创建交换空间。

### 3. 安装过程

- `pkgadd` 安装包，`pkgrm` 删除包，`pkginfo` 列出所有已安装包。默认目录为 `/var/spool/pkg`。也可以使用 `admintool` 安装包。

### 4. 系统支持

- TCP/IP 网络模型从高到低层为：应用层、传输层、网络层、数据链路和物理层。

### 5. 启动过程

- `/etc/dfs/sharetab` 文件应包含当前共享的 NFS 资源。`/etc/dfs/dfstab` 文件包含在系统启动或使用 `shareall` 命令时应自动共享的资源。

### 6. 运行级别控制

- NFS 服务器程序在运行级别 3 启动。运行级别 0 是电源状态；在此状态下服务正在关闭。运行级别 4 用于管理，不允许用户访问系统。除 NFS 服务器外，所有网络服务都在运行级别 2 启动。运行级别 6 是重启状态，系统正在重启。

### 7. 文件权限

- AdminSuite 包含用于管理网络客户端的主机管理器，而不是网络客户端管理器。数据库管理器、存储管理器和串口管理器都包含在 AdminSuite 中。

### 8. 用户与组

- AdminSuite 包含用于管理网络客户端的主机管理器，而不是网络客户端管理器。数据库管理器、存储管理器和串口管理器都包含在 AdminSuite 中。

### 9. 初始化文件

- Intel 客户端通常从本地软磁盘或本地 CD-ROM 获取启动镜像。只有 SPARC 客户端使用 TFTP 获取启动镜像。Intel 客户端可以配置使用远程加载（RPL）。子网对 TFTP 的使用没有影响。

### 10. 查看与终止

- `swap` 命令用于添加、列出和删除交换空间。`mkfile` 命令用于创建交换空间。

- 当使用卷管理时，CD-ROM 会自动挂载。使用 `eject cdrom` 手动卸载。
- 软盘使用 `vol` 挂载，并使用 `eject` 卸载（不带命令行参数）。

### 16. 文件与目录

- 文件类型有普通文件 (`-`)、链接 (`l`)、块设备 (`b`)、字符设备 (`c`)、目录 (`d`)、FIFO (`p`) 和套接字 (`s`)。
- 使用 `link` 或 `ln` 创建硬链接（限制在文件系统中）。使用 `ln -s` 创建软链接。使用 `unlink`、`rm` 或 `rmdir` 删除任何链接文件。
- 使用 `compress` (`uncompress`)、`gzip` (`gunzip`) 或 `zip` (`unzip`) 来压缩（解压）文件。只有 `zip` 可以对一组文件/目录进行压缩。

### 17. 备份与恢复

- 使用 `mt -f device` 命令控制磁带。如果没有给出设备，则假设为 `/dev/rmt0`。命令有：`fsf` 定位磁带，`bsf` 跳过 n 个向后标记，`fsf n` 标记向前标记，`rewind` 倒带和 `status` 状态。
- 使用 `ufsdump` 命令输出文件。命令 `0-9` 表示转储级别（0 为文件系统），`f` 输出文件，`v` 验证备份。如果没有给出命令，则假设为 `9f /dev/rmt0`。
- 使用 `ufsrestore` 恢复文件系统或选定的文件。如果没有给出 `backup_device`，则假设为 `/dev/rmt0`。
- 使用 `tar` 命令：`c` 创建，`r` 替换，`x` 提取，`v` 详细模式。使用 `f` 指定输入/输出文件或设备。
- 使用 `cpio` 创建/提取归档。`find` 可以根据修改日期、文件类型等生成包含在归档中的文件列表。

### 18. 目录导航

- 元字符 `?`（任意字符）、`*`（零或多个字符）和 `[ ]`（字符范围）可用于生成相对路径或绝对（从根目录）路径名。还可以使用当前目录 `.` 和父目录 `..`。

### 19. vi

- 模式：命令模式（默认）、输入模式（进入数据并以 `<ESC>` 结束）、末行模式（文件和搜索，在命令模式使用冒号、斜杠或问号进入）。
- 光标移动键：`<h>` 左，`<j>` 下，`<k>` 上和 `<l>` 右。

### 20. 远程访问

- 使用 `telnet` 或 `rlogin` 进行远程登录。使用 `ftp` 或 `rcp` 进行远程复制。使用 `rsh` 执行远程 shell 命令。
- `ftp` 子命令：`ascii`、`binary`；`get`；`put`；`hash`；`lcd`；`cd`；`mget`、`mput`。
- `rcp file user@host:path`（用户可选）。
- `rsh host command`。

## 第二部分：网络环境

### 1. TCP/IP 支持

- OSI 网络模型七层为：应用层、表示层、会话层、传输层、网络层、数据链路和物理层。
- TCP/IP 网络模型五层为：应用层、传输层、网络层、数据链路和物理层。
- 以太网地址由六字节 8 位数据（48 位）组成。
- 地址解析协议 (ARP) 将 IP 地址映射到以太网地址。反向 ARP 调用 (RARP) 从以太网地址映射。
- 配置文件有 `/etc/inet/hosts`（主机和 IP 地址）、`/etc/nodename`（本地主机）和 `/etc/hostname.interface`（本地主机或 IP 地址）。
- 使用 `ping` 和 `spray` 等命令检查连通性。使用 `ifconfig` 和 `netstat` 查看网络接口配置并检查网络统计。
- 远程过程调用 (RPC) 服务通过 `rpcbind` 注册，并可以使用 `rpcinfo` 查看。
- 网络服务由 `inetd` 控制并使用 `/etc/inet/inetd.conf` 文件配置。

### 2. Syslog 与审计

#### syslog

- `/etc/syslog.conf` 包含 `source.priority action` 语句。默认的 syslog 文件是 `/var/adm/messages`。
- 源有 `auth`、`cron`、`daemon`、`kern`、`lpr`、`local0-7`、`mail`、`mark`、`news`、`user` 和 `uucp`。
- `*` 用于指定除 `mark` 外的所有源。
- 优先级有 `alert`、`emerg`、`crit`、`err`、`warning`、`info`、`debug` 和 `none`。
- 动作有 `/filename`（追加到文件）、`@host`（发送到主机）、`用户名`（显示在终端上）和 `*`（在所有登录终端显示）。
- `m4` 宏可以在 `syslog.conf` 中包含条件语句。

## 高级磁盘管理

### 3. DiskSuite 和 Enterprise Volume Manager

- 都支持基于 RAID 配置的条带和拼接虚拟设备。
- DiskSuite 设备使用 `/dev/md/dsk` 和 `/dev/md/rdsk` 路径，而 Volume Manager 设备使用 `/dev/vx/dsk` 和 `/dev/vx/rdsk` 路径。
- Volume Manager 还包含性能分析工具和动态在线调优。

## 伪文件系统

### 4. 基于内存的文件系统包括：

- 用于远程数据本地缓存的 CacheFS、用于进程状态的 PROCFS、用于交换空间的 SWAPFS 以及用于快速访问临时文件的 TMPFS。
- `proc` 工具用于显示存储在 PROCFS `/proc` 中的进程信息。这些包括 `ps`、`pflags`、`pfiles`、`pldd`、`pmap`、`prun`、`psig`、`pstack`、`ptime`、`ptree`、`pwait` 和 `pwdx`。
- 默认 TMPFS 包含 `/tmp` 和 `/var/run`。文件在关机或系统重启时丢失。

## 交换空间

### 5. 用于临时存储内存数据的磁盘存储空间。

- 使用 `mkfile` 配置更多交换空间。
- 使用 `swap` 用于启用 (`-a`)、列出 (`-l`)、删除 (`-d`) 和显示交换空间的统计 (`-s`)。

## 基于角色的访问控制 (RBAC)

### 6. RBAC 允许根据角色授予访问权限。

- 通过 `su` 命令访问特殊用户账户。
- 配置文件 是授予角色的权限集。
- 授权 是授予执行的操作。

### 7. RBAC 数据库由四个文件组成：

- `user_attr` 定义角色并将授权授予用户账户。字段为 `name`、`qualifier`、`reserved1`、`reserved2`。
- `prof_attr` 定义配置文件。字段为 `name`、`reserved1`、`reserved2`、`description` `attributes`。
- `auth_attr` 定义授权。字段为 `name`、`reserved1`、`reserved2`、`description` 和 `attributes`。
- `exec_attr` 定义执行操作。字段为 `name`、`policy`、`type`、`reserved1`。

## NFS

### 8. NFS 客户端在运行级别 2，服务器在运行级别 3。

- NFS 是默认文件系统类型，在 `/etc/dfs/fstypes` 中指定。
- NFS 资源通过 `share` 和 `shareall`（挂载 `/etc/dfs/dfstab` 中的所有资源）可用。通过 `unshare` 和 `unshareall`（卸载 `/etc/dfs/dfstab` 中的所有资源）失效。`dfshares` 可列出本地或远程共享。
- NFS 资源通过 `mount` 和 `mountall`（挂载 `/etc/vfstab` 中的所有资源）可用。通过 `umount` 和 `umountall`（卸载 `/etc/mnttab` 中的所有资源）失效。`dfmounts` 可列出本地或远程共享。
- 客户端自动 NFS 通过指定 `-ro`（只读）挂载选项、服务器（逗号分隔）进行配置。
- Web NFS 允许浏览器访问 NFS 资源。`share` 命令的命令行参数可以关联公共句柄 并指定用于替代目录的文件。

### 9. AutoNFS

- AutoNFS 资源按需加载并在空闲 10 分钟后卸载。
- 使用 `automount -t` 命令指定空闲秒数。
- 配置文件——`/etc/auto_master` 列出了直接和间接映射。直接映射文件提供完整的挂载点和资源列表。

### 10. CacheFS

- CacheFS 用于在客户端本地缓存 NFS 资源。
- 使用 `cfsadmin` 创建、检查、调优和删除缓存。
- 使用 `mount` 命令的选项将 NFS 资源挂载到缓存中。这些是 `-F` 指定资源类型 (NFS) 以及 `-o cachedir=` 指定缓存的完整路径。然后通过缓存访问资源，并根据需要更新。

## 命名服务

### 11. 域名系统 (DNS) 和轻量级目录访问协议 (LDAP) 是全局命名系统。其他所有都是企业命名系统。

### 12. DNS 是一种 Internet 服务并使用数据文件。

### 13. 网络信息服务 (NIS)

- NIS 使用映射。`ypinit -m` 用于初始化主服务器，`ypinit -s` 用于从服务器，`ypinit -c` 用于客户端。
