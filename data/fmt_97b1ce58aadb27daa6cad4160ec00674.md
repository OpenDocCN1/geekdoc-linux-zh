
root 用户使用 `hdparm` 工具设置和调优 IDE 硬盘的设置。你可以借此调优驱动器以获得最佳性能。在之前需要内核补丁和安装相关支持程序后，`hdparm` 程序现在包含在 Ubuntu 中。你应该只对只读挂载的文件系统进行实验，因为某些设置在使用不当时可能会损坏某些文件系统。`hdparm` 命令也适用于 CD-ROM 驱动器和某些 SCSI 驱动器。

命令的通用格式为：

```
matthew@semour:~$ hdparm [options] device
```

以下命令测试：

```
matthew@semour:~$ hdparm -T /dev/sda
```

你必须将 `/dev/sda` 替换为你的磁盘的位置。以下命令运行计时测试：

```
matthew@semour:~$ hdparm -t /dev/sda
```

以下命令运行缓冲读取测试：

```
matthew@semour:~$ hdparm -t /dev/sda
```

以下命令运行未缓冲读取测试：

```
matthew@semour:~$ hdparm -c /dev/sda
```

## 硬盘

`-m` 选项通过较低的值来设置预留块百分比，从而释放空间，但代价是 `fsck` 写入任何恢复文件的空间会变小。

使用 `-O sparse_super` 选项减少超级块数量以节省空间（现代文件系统默认使用此选项）。在更改数值后，请务必运行 `efsck`。

通过 `-r` 选项设置预留（根）块的数量，可以释放更多空间。

请注意，`tune2fs` 的大多数此类用法都是以释放磁盘空间为代价，牺牲了 `fsck` 恢复数据的能力。除非你接受默认值；现在的硬盘已经相对廉价了。

## e2fsck 命令

该实用程序检查 ext2/ext3 文件系统。从 `e2fsck` 中提取的一些有用参数如下：

- `-c` - 检查坏块并将它们标记为坏块
- `-f` - 强制对干净的文件系统进行检查
- `-v` - 详细模式

## badblocks 命令

虽然 `badblocks` 本身不是性能调优程序，但该实用程序会（优先地）检查未挂载分区的坏块。不建议单独运行此命令，而是让它被 `fsck` 调用。如果你准确指定了块大小，则应直接使用它；不要猜测或假设任何内容。

`badblocks` 的选项在主页中有详细说明。它们允许对文件系统进行非常底层的操作，这对于文件系统专家的数据恢复或系统黑客非常有用，但这些已超出了本章和普通用户的范围。

## 禁用文件访问时间

每当 Linux 读取文件时，它都会更改最后访问时间（称为 `atime`）。这对于你的 Web 服务器也是如此：如果你每秒受到 50 次请求，你的硬盘每秒就会更新 50 次 `atime`。你真的需要知道文件最后被访问的时间吗？如果不需要，可以通过输入以下命令禁用目录的设置：

```
mathew@seymour:~$ chatter -R +A /path/to/directory
```

`chatter` 命令更改文件属性，其中“不更新 atime”就是一种。要设置该项，请使用 `+A` 并指定 `-R` 以进行递归。`/path/to/directory` 会被更改，其包含的所有文件和子目录也是如此。

## 内核

随着 Linux 时间的推移，开发者寻求一种方法来精调某些内核参数。在 `sysctl` 之前，这些参数必须在内核配置中更改，然后必须重新编译内核。

`sysctl` 命令可以更改运行中内核的一些参数。它通过 `/proc` 文件系统实现，`/proc` 是进入内核的“虚拟窗口”。尽管 `/proc` 下似乎存在一组目录和文件，但那只是内核部分内容的表示。当你是 root（或使用 `sudo` 命令）时，可以读取并向这些“文件”写入值，这些文件被称为变量。你可以像下面所示显示变量列表。（呈现的是简略列表，因为完整列表中大约有 250 个或更多项目。）

```
matthew@semour:- sysctl -A
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_rfc1337 = 0
net.ipv4.tcp_strug = 0
net.ipv4.tcp_abort_on_overflow = 0
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_syn_cookies = 0
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_retries2 = 15
net.ipv4.tcp_retries1 = 3
net.ipv4.tcp_keepalive_int = 75
net.ipv4.tcp_keepalive_probes = 9
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.ipfrag_time = 30
```

显示的项目是网络参数，调整这些值超出了本书的范围。然而，如果你想更改某个值，可以使用 `-w` 参数：

```
matthew@semour:- sysctl -w net.ipv4.tcp_retries2=20
```

这增加了该特定内核参数的值。

如果你发现某个设置有用，可以将其输入 `/etc/sysctl.conf` 文件中。格式如下（使用之前的示例）：

```
net.ipv4.tcp_retries 2=20
```

对于内核黑客来说，比普通用户更有趣的是，`sysctl` 是一个潜在的强大工具，仍在不断开发和编写文档。

> 内核在平衡图形系统性能方面做得很好，因此你无法做很多事情来调整你的桌面使其运行得更快。

GNOME 和 KDE 都是“重量级桌面系统”：它们都是全能的、功能丰富且华丽的环境，其功能远超浏览文件系统。缺点是它们体积巨大，导致在旧系统上运行缓慢。相反，Ubuntu 存储库中还有其他选择，如 Xce 和 LXDE 桌面，它们比另外两个更轻量、运行得更快。如果你发现 GNOME 和 KDE 仅仅打开一个文件管理器就很吃力，那么 Xce 或 LXDE 可能适合你。

## Apache

尽管是互联网上最流行的 Web 服务器，但 Apache 绝不是最快的。部分“问题”在于 Apache 的编写是为了遵循每一项适用的标准。

## MySQL 413

要执行此操作，登录 MySQL 并输入 `SHOW STATUS LIKE '%key_read%';`，这将返回所有描述你的键缓冲区命中率的状态字段。你应该会得到两行结果：`Key_reads` 和 `Key_read_requests`，它们分别是从磁盘读取的键的数量以及从键缓冲区中读取的键的数量。通过这两个数字，你可以使用这个简单的公式计算从 RAM 和磁盘填充的请求百分比：

```
100 - ((Key_reads / Key_read_requests) * 100)
```

也就是说，你将 `Key_reads` 除以 `Key_read_requests`，将结果乘以 100，然后从 100 中减去该结果。例如，如果你的 `Key_reads` 为 100，`Key_read_requests` 为 10000，你除以 10000 得到 0.01；然后乘以 100 得到 1.0，再从 100 中减去得到 99。这个数字就是从 RAM 提供服务的键百分比，意味着你 99% 的键是从 RAM 提供的。

大多数人应该寻求让 RAM 提供的比例超过 95%，尽管主要的例外是你非常频繁地更新或删除行——MySQL 无法缓存不断变化的数据。如果你的网站主要是只读的，这个数字应该在 98% 左右。如果数字较低，你可能需要增大键缓冲区的大小。

如果你发现了问题，下一步是检查你当前的键缓冲区使用了多少。使用 `SHOW VARIABLES` 命令并查找 `key_buffer_size` 变量的值。它看起来 own 8388600，即 800 万字节，或 8MB。现在，使用 `SHOW STATUS` 命令并查找 `key_blocks_used` 的值。

你可以通过将 `key_blocks_used` 乘以 1024，除以 `key_buffer_size`，再乘以 100 来确定你的键缓冲区使用了多少。例如，如果 `key_buffer_size` 为 (8388600)，你除法得到 0.97656，最后乘以 100 得到 97.656。因此，你几乎 98% 的键缓冲区都被使用了。

现在，到了重点部分：你已经确定你正在从磁盘读取大量键，并且你知道读取磁盘的原因几乎肯定是你没有为键缓冲区分配足够的 RAM。一个通用规则是尽可能为键缓冲区分配内存 RAM，最多可达系统 RAM 的 25%——在 512MB RAM 的服务器上，分配 128MB 对于频繁读取键的系统是理想的。超过这个范围，你实际上会看到性能大幅下降，因为系统必须使用虚拟内存作为键缓冲区。

在文本编辑器中打开 `/etc/my.cnf` 并寻找包含 `key_buffer_size` 的行。如果你没有，请创建一个。它应该位于 `[mysqld]` 行下方。当你设置新值时，不要随机选择一个非常高的数字。尝试将其增加一倍（如果还没有该行，则设为 16MB）；然后观察效果如何。要将 16MB 设置为键缓冲区大小，你需要像这样的一行：

```ini
[mysqld]
key_buffer_size = 16M
datadir=/var/lib/mysql
```

# 第 19 章 性能优化

使用 `service mysql restart` 重启你的 MySQL 服务，然后回到 MySQL 再次运行 `SHOW VARIABLES` 来查看 `key_buffer_size`。如果你将其设置为 16M，它应该是 16773120。现在，因为 MySQL 刚刚重置，它所有关于键命中及类似的值也会被重置。你需要让它运行一段时间，以便你评估变化了多少。如果你有测试系统的话，现在就是运行它的时机。

在你的数据库经过正常使用访问一短时间后（如果访问频繁，这可能只需要几分钟），重新计算键缓冲区的使用率。如果你得到了另一个分数，再次将大小翻倍，重启并重新测试。你应该不断重复这个过程，直到你的键缓冲区使用率达到 50%，或者你发现没有足够的 RAM 来增加缓冲区。记住，你永远不应该为键缓冲区分配超过系统 RAM 25% 的内存。

# 使用查询缓存

较新版本的 MySQL 允许你缓存查询结果，这样如果进来的新查询使用了相同的 SQL，就可以从 RAM 提供结果。在某些方面，查询缓存是非常智能的。例如，如果由于另一个查询导致部分结果发生变化，缓存的结果会被丢弃并在下次重新计算。但在其他方面，它又非常简单。例如，它只有在新查询与缓存查询完全相同时（甚至包括 SQL 的大小写）才会缓存结果。

查询缓存可以在许多场景下派上作用。如果你的网站读写比例均衡，缓存会尽力而为但并非最优。如果你的网站主要是读写写，会有更多的查询被缓存（且缓存时间更长），从而提高性能。

首先，你需要确定查询缓存是否已启用。要做到这一点，执行 `SHOW VARIABLES` 并查找 `have_query_cache` 的值。如果一切正常，你应该得到 YES，这意味着查询缓存已启用。接下来，查找 `query_cache_size` 和 `query_cache_limit` 的值。前者是分配给查询缓存的内存，后者是应该缓存的最大 own。接下来，输入 `SHOW STATUS LIKE 'qcache%'` 查看关于查询缓存的所有信息。

| 变量 | 值 |
| :--- | :--- |
| Qcache_blocks_free | [Value] |
| Qcache_free_memory | [Value] |
| Qcache_hits | [Value] |
| Qcache_inserts | [Value] |
| Qcache_lowmem_prunes | [Value] |
| Qcache_not_cached | [Value] |
| Qcache_queries_in_cache | [Value] |
| Qcache_total_memory | [Value] |

8MB 的查询缓存对大多数人来说足够了，较大的网站可能需要 16MB 或 32MB，但要注意 `Qcache_lowmem_prunes` 值以确保你有足够的 RAM。

使用查询缓存不会产生太大的性能影响。当 MySQL 正常计算查询结果时，它会丢弃结果。有了查询缓存，它跳过了丢弃过程，因此没有额外的开销。如果你的网站有很多更新和删除操作，务必检查缓存是否带来了任何速度提升。

# 其他微调

如果你已经调整了键缓冲区并优化了查询缓存但仍然发现很吃力，可以进行一些较小的调整来增加速度。

读取表时，MySQL 必须打开存储数据的文件。一次性打开多少文件由 `table_cache` 设置定义，默认值设置为 64。如果你有超过 64 个表，可以增加此值，但请注意 Ubuntu 对 MySQL 同时可以打开的文件数量有限制。除非你有一个特别依赖数据库的网站且完全清楚自己在做什么，否则不建议超过 256。

你可以调整的另一个东西是读取缓冲区的大小，由 `read_buffer_size` 和 `read_buffer_rnd_size` 控制。这两个值都是按连接分配的，这意味着在设置较大数值时要非常小心。无论你选择什么值，`read_buffer_rnd_size` 应该应该是 `read_buffer_size` 的三到四倍，所以如果 `read_buffer_size` 是 1MB（适用于非常大的数据库），`read_buffer_rnd_size` 应该是 4MB。

## 查询优化

通过重写你的 SQL 语句使其更加高效，可以获得最大的速度提升。如果你遵循这些提示，你的服务器会感谢你的：

- 尽可能少选择数据。与其使用 `SELECT *`，不如只选择你需要的字段。
- 如果你只需要几行，请使用 `LIMIT` 选择你需要的行数。
- 在创建表时将字段声明为 `NULL` 以节省空间并提高速度。
- 为字段提供默认值并在可能的情况下使用它们。
- 使用连接（joins）时要非常小心，因为它是编写低效查询最简单的方法。
- 如果你必须使用连接，请确保在已索引的字段上进行连接。这些字段最好使用整数类型，因为整数的比较速度比字符串快。
- 找到并修复慢查询。在 `/etc/my.cnf` 文件的 `[mysqld]` 节点添加 `log-log-format` 和 `log-slow-queries = /var/log/slow-queries.log`，MySQL 就会告诉你执行时间较长的查询。
- 使用 `OPTIMIZE TABLE typename` 来整理表碎片并刷新索引。

## 参考文献

- www.coker.com.au/bonnie/—磁盘基准测试工具 bonne 的主页。它还包含指向 RAID 基准测试工具和 SMTP 服务器基准测试工具 Postal 的链接。
- www.phoronix-test-suite.com/—Phorix Test Suite 由一个进行自动化性能调优和比较的网站创建，是一个值得考虑的质量基准软件。
- http://http.apache.org/docs-2.0/misc/perf-tuning.html—Apache Web 服务器调优官方指南。
- dev.mysql.com/doc/refman/5/en/optimization.html—直接从源 MySQL 手册学习如何优化你的 MySQL 服务器。
- 如果你运行大型网站，一本 MySQL 优化书籍将真正帮助你从系统中获取更多价值：《High Performance MySQL》，作者 Jeremy Zawodny 和 Derek Balling（O'Reilly 出版），ISBN: 0-596-00306-4。

# 第 20 章

## 内核与模块管理

内核是一个复杂的软件，负责管理操作系统内部发生的进程和交互。作为用户，你很少直接与它交互。相反，你操作的是内核所管理的应用程序。

Linux 内核就是 Linux。它是全球无数人员多年合作（有时也存在争议）工作的结果。虽然只有一个通用的内核源码，但每个 Linux 发行版都会对其版本进行微调补丁，以添加功能、性能或选项。每个 Linux 发行版（包括 Ubuntu）都带有自己的预编译内核以及内核源码，赋予了你对 Linux 操作系统的绝对权限。本章将介绍内核以及它为我们和操作系统做了什么。
