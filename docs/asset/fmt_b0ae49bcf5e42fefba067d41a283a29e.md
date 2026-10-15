
```
didymus.home.com:/usr
didymus.home.com:/docs
chips.home.com:/usr
chips.home.com:/src
```

显示了两个从 `bedrock` 挂载文件系统的客户端系统。第一个客户端 `didymus` 挂载了 cả `/usr` 和 `/docs` 文件系统。第二个系统 `chips` 分别挂载了 `/usr` 和 `/src` 文件系统。`showmount` 命令也可以用于显示本地 NFS 服务器上可用的挂载文件系统。例如，如果在 `bedrock` 系统上带 `-d` 选项运行 `showmount` 命令，将显示如下：

```
/docs
/usr
```

上述输出显示了所有对 NFS 客户端可用的文件系统。在这种情况下，输出与 `share` 命令提供的类似。

## nfsstat

`nfsstat` 命令提供基于 NFS 服务器的 NFS 活动的统计和性能信息。可以显示以下类别的信息：

- 服务器 RPC 统计
- 服务器 NFS 统计
- 客户端 RPC 统计
- 客户端 NFS 统计

显示的统计数据由命令行选项决定，如表 17-4 所示。不带任何参数执行命令将激活 `-csnrc` 选项并产生每个统计数据的相应输出。

| 选项 | 描述 |
| - | - |
| `-a` | 显示访问控制列表 (ACL) 信息。 |
| `-c` | 显示 NFS、RPC 和 ACL 的客户端信息。 |
| `-m` | 显示每个 NFS 挂载文件系统的配置和统计。 |
| `-n` | 显示特定的 NFS 活动。 |
| `-r` | 显示重传统计数据。 |
| `-s` | 显示服务器端统计。 |
| `-z` | 显示计数器。 |

**表 17-4** `nfsstat` 选项

## 17.3 使用 NFS

关于硬挂载和软挂载（hard soft mounts），当在客户端系统上使用硬挂载时，如果服务器发生导致 NFS 服务中断的问题，客户端可能会锁定，直到服务器问题得到解决。解决此问题的方案是使用软挂载。然而，尽管使用软挂载有助于解决问题，但它并没有专门解决任何服务器问题，任何挂起的 NFS 活动将简单超时。当发生超时时，客户端系统将生成一个或多个错误消息。

## 第 17 节：使用网络文件系统 525

系统维护了一个计数器。此外，对于每个计数器，都会计算接收到的总事务数的百分比。例如，`getattr` 属性占服务器接收到的总事务数的35%。当 NFS 客户端系统需要特定信息时，就会使用 `getattr`。

服务器 nfs:

calls badcalls

47088 5

Version 2: (14 calls)

null getattr setattr root lookup reread

0 0% 5 35% 0% 0% 0% 0% 0 0%

read wrcache create remove rename

0 0% 0% 0% 0% 0% 0 0%

link symlink mkdir rmdir readdir stats

0 0% 0% 0% 0% 3 21% 6 42%

Version 3: (47074 calls)

null getattr setattr lookup reread

1 0% 23% 0% 57321 11 41486 82% 2058 0%

read write create symlink knod

0 0% 0% 0% 0% 0% 0%

remove rmdir rename link readdirplus

0 0% 0% 0% 0% 0% 3943 0% 1 0%

fsstat fsinfo pathconf commit

24 0% 21% 0% 0% 0%

表 16（表 17-6）提供了各个单独计数器字段的列表和描述。

客户端 nfs:

calls badcalls clgets cto-any ctoomany

79 1 79 0

Version 2: (63 calls)

null getattr setattr root lookup reread

0 0% 55 87% 0% 0% 7 11% 0 0%

read wrcache create remove rename

0 0% 0% 0% 0% 0% 0 0%

link symlink mkdir rmdir readdir stats

0 0% 0% 0% 0% 0% 1 1%

Version 3: (15 calls)

null getattr setattr lookup reread

0 0% 30% 0% 1 16% 0 0%

read write create symlink knod

0 0% 0% 0% 0% 0% 0%

remove rmdir rename link readdirplus

0 0% 0% 0% 0% 0% 1 6%

fsstat fsinfo pathconf commit

8 53% 23% 0% 0% 0% 

## 526 UNIX 系统管理：入门指南

| 字段 | 描述 |
|---|---|-|
| calls | 接收到的 NFS 调用总数。 |
| badcalls | 被拒绝的 NFS 调用总数。 |
| null | 发出但未被收到的 NFS 调用总数。 |
| getattr | 执行的文件属性查找调用总数。例如，获取文件大小信息。 |
| setattr | 执行的文件属性设置调用总数。例如，更新文件的修改日期。 |
| root | 执行的 root 用户请求总数。 |
| lookup | 执行的文件/目录查找请求总数。 |
| readlink | 执行的 readlink（文件链接）请求总数。 |
| read | 执行的读取请求总数。 |
| wrcache | 执行的写入缓存的请求总数。 |
| write | 执行的写入请求总数。 |
| create | 执行的创建（文件或目录）请求总数。 |
| remove | 执行的删除请求总数。 |
| rename | 执行的重命名请求总数。 |
| link | 执行的链接（硬链接）请求总数。 |
| symlink | 执行的链接（符号链接）请求总数。 |
| mkdir | 执行的创建目录请求总数。 |
| rmdir | 执行的删除目录请求总数。 |
| readdir | 执行的读取请求总数。 |
| stats | 执行的 stats 请求总数。 |
| readdirplus | 执行的 readdirplus 请求总数。 |
| fsstat | 执行的 fsstat 请求总数。 |
| fsinfo | 执行的 fsinfo 请求总数。 |
| pathconf | 执行的 pathconf 请求总数。 |
| commit | 执行的 commit 请求总数。 |

**表 17-6 NFS 字段描述**

### 17.4 配置客户端

客户端组件维护了一个计数器。此外，对于每个计数器，都会计算接收到的总事务数的百分比。例如，`getattr` 属性占服务器接收到的总事务数的35%。当 NFS 客户端系统需要特定信息时，就会使用 `getattr`。

## 17: 使用网络文件系统 525

客户端组件维护了一个计数器。此外，对于每个计数器，都会计算接收到的总事务数的百分比。例如，`getattr` 属性占服务器接收到的总事务数的35%。当 NFS 客户端需要特定信息时，就会使用 `getattr`。

### 17.5 控制文件系统挂载

文件系统表语法用于指示当系统从单用户模式启动或重启到正常运行状态时如何挂载本地和远程文件系统。Linux 上使用 `/etc/fstab` 文件；而在 Solaris 和 HP-UX 上，使用 `/etc/vfstab` 文件。在两种情况下，这些文件的内容都是静态的，由系统管理员维护。当向系统添加新的文件系统或在网络上提供新的 NFS 卷时，必须更新这些文件以便客户端系统使用这些新文件系统。文件系统挂载表包含多个字段，描述了本地或从服务器挂载的文件系统。在 NFS 情况中，额外的选项用于控制文件系统的挂载方式。

# 模块 17：使用网络文件系统 529

NFS，这包含了 NFS 服务器的名称，随后是远程文件系统的名称——例如项 `bedrock:/usr`。

# 注意

冒号字符 (`:`) 需要作为字符串分隔符。

- mount_point: 挂载点代表文件系统将挂载的目录——例如 `/usr/docs`。目标目录应该是空的，且管理员在挂载之前应该检查现有目录的状态。

# 注意

如果将一个文件系统挂载到一个包含额外目录或文件的目录上，那么在新的文件系统挂载期间，这些内容将变得不可见。因此，要访问这些文件或目录，必须卸载该文件系统。

挂载点是文件系统关联的目录，用户通过它来导航挂载的文件系统。无论文件系统是本地的还是来自 NFS 服务器，目标目录的作用都是相同的。
