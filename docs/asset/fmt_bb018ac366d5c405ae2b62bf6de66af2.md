
# mount -o server_only tcrhb@fafrak /fafrak

```
```

[sheridan]

# mount extra@kits /fafrak/kits

extra#kits on /fafrak/kits: Permission denied

```

## 13.4.2.5 尝试更新挂载

你不能通过更新挂载（`mount update`）来使其变为“-o server_only”。例如：

```
[sheridan]

# umount /fafrak
```

```
[sheridan]

# mount -u -o server_only@fafrak
```

Cannot updating existing mount to be server-only.

如果你想将已挂载的文件系统从集群范围挂载更改为分区挂载，你必须卸载该文件系统并使用“-o server_only”重新挂载。

然而，你可以通过更新挂载将文件系统从只读模式改为读写模式。让我们重新挂载 `tcrhb@fafrak` 文件系统“-o server_only, ro”，这样我们就可以尝试将挂载更新为读写。

```
[sheridan]

# umount /fafrak
```

```
[sheridan]

# mount -o server_only,ro tcrhb@fafrak /fafrak
```

```
[sheridan]

# mount | grep fafrak
```

ntcrhb@fafrak on /fafrak type advfs (ro, server_only)

```
[sheridan]

# mount -u /fafrak
```

WARNING: Domain is already specified server_only so this mount will be.

```
[sheridan]

# mount | grep fafrak
```

tcrhb#fafrak on /fafrak type advfs (rw, server_only)

## 13.5 配额 (Quotas)

Tru64 UNIX 提供三个级别的配额支持：

- 用户 (User)
- 组 (Group)
- 文件集 (Fileset，仅限 AdVFS)

TruCluster 一直支持文件配额，但直到 V5.1A 才增加了用户和组配额支持。

为了防止配额支持影响集群文件系统的性能，在配额执行上做了一个折中。折中方案的用户或组可以通过 cfs 子系统中的 `quota_excess_blocks` 属性超过其配额。默认情况下，此值设置为每个成员 1 MB —— 因此在八节点集群上，任何用户或组的配额都可能超出多达 8 MB。`quota_excess_blocks` 属性可以在系统运行时重新配置（注意“R”中的“R”）。

# 343

注意，“集群感知”（cluster unaware）一词用于表示该方法不会让你的应用程序“感知”到它正处于集群中。换句话说，它不是 TruCluster Server 特有的 API。事实上，为了支持 CFS 中的 POSIX 和 X/OPEN API，为在独立系统上使用这些标准 API 进行文件锁定而编写的应用程序，可以直接移动到集群中，它将提供集群范围的文件锁定。不需要任何特殊的修改，这确实非常方便！

令牌（token）的作用是保证成员的缓存在任何特定时刻都不会包含对文件的不同视图。

这是一个简化的示例（注意，我们没有指示令牌类型，仅指示令牌模式）。在此示例中，Member1 是节点 sheridan，Member2 是节点 molari。

| 令牌模式: | Member1 | Member2 |
|---|---|---|
| | READ/WRITE | 无令牌 |

在成员1 上，使用你喜喜欢的编辑器打开一个新文件。将文件写入磁盘但不退出编辑器。

```
[sheridan]

# vi MyDataFile
```

i

La Dee Da

Yadda yadda yadda

Ex:w

| 令牌模式: | Member1 | Member2 |
|---|---|---|
| 令牌降级为 READ。 | READ | |
| 缓存已刷新。 | | |

在成员2 上，输出文件内容。

```
[molari]

# cat MyDataFile
```

La Dee Da

Yadda yadda yadda

两个成员对文件的视图完全相同。

| 令牌模式: | Member1 | Member2 |
|---|---|---|
| 令牌被撤销。缓存已刷新并失效。 | | READ/WRITE |

在成员2 上，向文件追加一些信息。

```
[molari]

# cat >> MyDataFile
```

toodle loo

^D

# 第 13 章

# 344

| 令牌模式: | Member1 | Member2 |
|---|---|---|
| | READ | 令牌降级为 READ。缓存已刷新。 |

在两个成员上，均显示文件。

```
[molari]

# cat MyDataFile
```

La Dee Da

Yadda yadda yadda

toodle loo

```
[sheridan]

# cat MyDataFile
```

La Dee Da

Yadda yadda yadda

toodle loo

两个成员对文件的视图仍然相同。

| 令牌模式: | Member1 | Member2 |
|---|---|---|
| | READ/WRITE | 令牌被撤销。缓存已刷新并失效。 |

在成员1 上，再次将文件写入磁盘。记住，我们仍在编辑器中。

```
[sheridan] - 仍在 vi 中

:W
```

| 令牌模式: | Member1 | Member2 |
|---|---|---|
| | READ | 令牌降级为 READ。缓存已刷新。 |

在成员2 上，再次输出文件内容。

```
[molari]

# cat MyDataFile
```

La Dee Da

Yadda yadda yadda
