
## 表 17.4 继续

## 挂载选项

| 选项 | 描述 |
|---|---|
| cacheid=<ID> | ID 是一个字符串，用于指定缓存的特定实例。如果未指定缓存 ID，CacheFS 会构造一个。 |
| demandconst | 仅在明确请求时验证缓存一致性，而不是默认执行的定期检查。您可以使用 cfsadmin 命令的 -s 选项请求一致性检查。此选项适用于更改不频繁的后端文件系统，例如 /usr/openwin。demandconst 和 noconst 互斥。 |
| local-access | 导致前端文件系统解释用于访问检查的模式位，而不是由后端文件系统验证访问权限。不要将此参数与安全 NFS 一起使用。 |
| noconst | 禁用缓存一致性检查。默认情况下，定期一致性检查已启用。仅在您确定后端文件系统不会被修改时才指定 noconst。使用 cfsadmin -s 尝试执行缓存一致性检查会导致错误。demandconst 和 noconst 互斥。 |
| purge | 清除指定文件系统的任何缓存信息。 |
| ro | rw | 为只读或读写（默认值）。 |
| suid | nosuid | 允许（默认值）或禁止 setuid 执行。 |
| write-around | non-shared | CacheFS 的写入模式。写入绕过模式（默认值）与 NFS 相同处理写入。换句话说，写入操作会写入后端文件系统，受影响的文件会从缓存中清除。当您确定没有其他人会写入缓存的文件系统时，可以使用非共享模式。在此模式下，所有写入都会同时写入前端和后端文件系统，并且文件保留在缓存中。 |
| -O | 覆盖挂载。允许文件系统挂载到现有挂载点之上，使底层文件系统无法访问。如果您尝试在预先存在的挂载点上挂载而未设置此标志，mount 将失败并出现以下错误：mount -F cachefs: mount failed Device busy。 |

以下示例创建挂载点 /sparc21data 并将 NFS 文件系统 sparc21:/data 作为名为 /sparc21data 的缓存文件系统挂载到名为 /local/cache1 的缓存中：

```
mkdir /sparc21data
mount -F cachefs -o backfstype=nfs,cachedir=/local/cache1 sparc21:/data /sparc21data
```

现在 CacheFS 挂载点 /sparc21data 可以像任何其他挂载文件系统一样访问。

要使挂载点永久生效，请按如下方式将以下行添加到您的 /etc/vfstab 文件中：

```
sparc21:/data  /local/cache1  /sparc21data  cachefs  3  yes  backfstype=nfs, cachedir=/local/cache1
```

使用以下命令验证您创建的缓存是否实际已挂载：

```
cachefsstat /sparc21data
    /sparc21data
    cache hit rate:      0%      (0 hits, 8 misses)
    consistency checks:  7       (5 pass, 2 fail)
    modifies:            0
    garbage collection:  0
```

如果文件系统未挂载到缓存中，您将收到类似以下内容的错误消息：

```
cachefsstat /sparc21data
cachefsstat: /sparc21data: not a cachefs mountpoint
```

在初始引用 CacheFS 文件系统中的数据时（与缓存填充相关）会产生一些开销，但随后对相同数据的引用可以在不访问后端文件系统的情况下得到满足。预热缓存提供的性能接近本地文件系统，而无需与本地文件系统相关的管理和开销。对于访问慢速网络链路或负载较重的服务器的客户端，CacheFS 文件系统相对于传统 NFS 挂载的性能要快得多。

您也可以在同一缓存中缓存多个文件系统。无需为每个 CacheFS 挂载创建单独的缓存。换句话说，您只需运行一次 cfsadmin -c 即可为所有 CacheFS 挂载创建一个缓存。

许多类型的后端文件系统都可以潜在地进行缓存。例如，使用 CacheFS 将 CD-ROM 缓存在更快的硬盘上等慢速介质的缓存可以带来性能优势。然而，本地文件系统（UFS）通常不会被缓存。

任何“主要为只读”的文件系统都是缓存的可能候选者。/usr/share/man 是缓存的优秀候选者的一个例子。通常只读取一次的文件系统，例如 /var/mail，并不适合缓存，因为数据通常只读取一次就被丢弃。在这种情况下，您承担了缓存填充的成本，却得不到后续缓存访问的任何好处。

CacheFS 对写操作没有好处。这是因为 CacheFS 严格来说是一个“写穿透”缓存。CacheFS 的写性能永远不会优于后端文件系统。

CacheFS 不是 NFS 性能加速器。单个客户端可能不会从缓存中获得太多性能提升，尤其是在负载较轻的快速局域网中，服务器是功能强大的机器且磁盘快速且负载不大。缓存的好处在繁忙的网络和负载较重的服务器上体现出来。

## 监控缓存

您可以使用 CacheFS 统计信息来监控缓存的性能以确定适当的缓存大小。表 17.5 中列出的三个命令可帮助您确定缓存大小与所需缓存性能之间的权衡。

## 表 17.5

### CacheFS 统计命令

| 命令 | 描述 |
|---|---|
| cachefslog | 指定日志文件的位置。此命令还显示统计信息当前记录的位置，并允许您停止记录。 |
| cachefswssize | 解析日志文件以给出推荐的缓存大小。 |
| cachefsstat | 显示特定文件系统或所有缓存文件系统的统计信息。此命令输出提供的信息直接取自缓存。 |

cfsadmin 使用的缓存参数的默认值是缓存使用整个前端文件系统进行缓存。如果缓存仅限于前端文件系统的一部分，则应更改参数值。cfsadmin 命令允许您指定表 17.6 中列出的选项。

## 表 17.6

## cfsadmin 选项

| 选项 | 描述 |
|---|---|
| maxblocks | 设置 CacheFS 在前端文件系统中允许占用的最大块数。它不保证资源可供 CacheFS 使用。默认值为 90%。注意：如果 UFS 文件系统超过 90% 容量，性能会显著下降。 |
| minblocks | 与 threshblocks 一起工作。它不保证最低资源水平的可用性。默认值为 0%。 |
| threshblocks | 与 minblocks 一起工作。此值在达到 minblocks 值之前会被忽略。CacheFS 只有在前端文件系统中可用块的百分比大于 threshblocks 时才能占用超过 minblocks 的块。此值适用于整个前端文件系统，而不仅仅是缓存部分。默认值为 85%。 |
| maxfiles | 设置 CacheFS 可以占用的最大文件数（inode）。它不保证资源可供 CacheFS 使用。默认值为 90%。 |
| minfiles/threshfiles | 与 minblocks 和 threshblocks 相同的方式一起工作。minfiles 默认值为 0%，threshfiles 默认值为 85%。 |

您不需要更改这些参数值。它们设置为默认值以实现最佳缓存行为。然而，如下一个示例所示，如果前端文件系统中存在缓存未使用的空间并且您想将其用于其他文件系统，则可能需要修改 maxblocks 和 maxfiles 设置。以下示例创建一个名为 /local/cache1 的缓存，该缓存最多可以使用前端文件系统中 80% 的磁盘块。它可以在不受限制的情况下增长到使用前端文件系统块的 55%，除非前端文件系统块已使用 60%（或更多）：

```
cfsadmin -c -o maxblocks=80,minblocks=55,threshblocks=60 \
/local/cache1
```
