

请注意，术语“cluster unaware”用于表示此方法不会使您的应用程序“感知”到它处于集群中。换句话说，它并不是 TruCluster Server 独有的 API。事实上，由于 CFS 对 POSIX 和 X/OPEN API 的支持，一个为在独立系统上使用这些标准 API 进行文件锁定而编写的应用程序，可以将该应用程序迁移到集群中，它将提供集群范围的文件锁定。无需特殊修改，这确实很酷！

令牌的任务是保证成员的缓存在任何特定时间都不会对文件有不同的视图。

下面是一个简化示例（注意，我们不标明令牌类型，只标明令牌模式）。在此示例中，Member1 为节点 sheridan，Member2 为节点 molar1。

| Token Mode: | Member1 | Member2 |
|---|---|---|
| READ/WRITE | No Token. |

在 member1 上，使用您喜欢的编辑器打开一个新文件。将文件写入磁盘但不要退出编辑器。

```
[sheridan]
# vi MyDataFile
i
La Dee Da
Yadda yadda yadda
Esc
:w
```

| Token Mode: | Member1 | Member2 |
|---|---|---|
| Token downgraded to READ. Cache flushed. | READ |

在 member2 上，输出该文件。

```
[molar1]
# cat MyDataFile
La Dee Da
Yadda yadda yadda
```

两个成员对文件的视图是相同的。

| Token Mode: | Member1 | Member2 |
|---|---|---|
| Token revoked. Cache flushed & invalidated. | READ/WRITE |

在 member2 上，向文件追加一些信息。

```
[molar1]
# cat >> MyDataFile
toodle loo
'D
```

| Token Mode: | Member1 | Member2 |
|---|---|---|
|  | READ | Token downgraded to READ. Cache flushed. |

在两个成员上，显示文件。

```
[molar1]
# cat MyDataFile
La Dee Da
Yadda yadda yadda

toodle loo
```

```
[sheridan]
# cat MyDataFile
La Dee Da
Yadda yadda yadda

toodle loo
```

两个成员仍然对文件有相同的视图。

| Token Mode: | Member1 | Member2 |
|---|---|---|
|  | READ/WRITE | Token revoked. Cache flushed & invalidated. |

在 member1 上，再次将文件写入磁盘。
请记住，我们仍在编辑器中。

```
[sheridan] - still in vi
:w
```

| Token Mode: | Member1 | Member2 |
|---|---|---|
|  | Token downgraded to READ. Cache flushed. | READ |

在 member2 上，再次输出该文件。

```
[molar1]
# cat MyDataFile
La Dee Da
Yadda yadda yadda
```

这里使用令牌显示的行为应该对您很熟悉，因为这正是独立系统在没有令牌的情况下的行为。尝试在独立系统上使用两个进程进行此示例。结果将是相同的。

要收集有关令牌的更多信息，您可以使用 cfsstat(8) 命令。您可以通过使用 cfsstat 命令分别使用“tokens”和“tokstats”选项来获取令牌的一般信息和统计信息。要按客户端或服务器检索特定文件的特定令牌信息，请分别使用“clitok_log”和“svrtok_log”选项。

有关更多信息，请参阅 TruCluster Server Cluster Administration Guide 和 cfsstat(8) 参考页。

## 13.7 Direct I/O

Direct I/O 最早在 V5.0A⁵ 中引入。当文件以 Direct I/O 标志打开时，对该文件执行的所有 I/O 都将绕过 Unified Buffer Cache（UBC）。要为文件启用 Direct I/O，文件必须使用 open(2) 系统调用以 O_DIRECTIO 标志作为模式打开。

注意：

- Direct I/O 只能为 AdvFS 文件系统上的文件启用。
- Direct I/O 只能在文件上启用，而不能在整个文件系统上启用。
- 您不能 mmap(2) 使用 Direct I/O 打开的文件。

图 13-2 说明了启用 Direct I/O 时 I/O 的流程。请注意，尽管 I/O 是“直接的”，但该术语并不意味着 I/O 直接进入磁盘，而只是意味着它直接进入 CFS 服务器（尽管如果 CFS 服务器是执行 Direct I/O 的成员，则 I/O 将直接进入磁盘，绕过 UBC）。

虽然 Direct I/O 对于已经使用自己的缓存机制的应用程序（例如数据库）来说可能是一种性能增强，但通常不被视为性能增强，实际上可能导致性能下降，因为写入设备比写入内存慢得多。

对于绕过 UBC 并直接进入磁盘的 Direct I/O，您需要 Concurrent Direct I/O。

![](img/a0df85c2e542a8d6c913113908553aa4_340_0.png)

图 13-2：V5.0A 中的 Direct I/O

⁵ 适用于 TruCluster Server 产品。Tru64 UNIX 在 V5.0 的基本操作系统中添加了对 Direct I/O 的支持。

