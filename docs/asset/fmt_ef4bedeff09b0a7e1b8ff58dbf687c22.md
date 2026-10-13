
`chattr` 命令更改文件系统属性，其中“不更新 atime”就是一种。要设置属性，请使用 `+A` 并指定 `-R` 以进行递归设置。`/path/to/directory` 会被更改，其包含的所有文件和子目录也会之改变。

# 内核

随着 Linux 内核随时间的发展，开发者寻求一种精调某些内核参数的方法。在 `sysctl` 之前，这些参数必须在内核配置中更改，然后重新编译内核。

`sysctl` 命令可以更改运行内核内核的一些参数。它通过 `/proc` 文件系统实现这一点，`/proc` 是一个指向运行内核的“虚拟窗口”。尽管 `/proc` 下似乎存在一组目录和文件，但它们是内核部分的表示。我们可以向这些被称为“变量”的“文件”读取值和写入值。我们可以像下面所示显示变量列表（带注释的列表中大约有 250 个[或更多]项目）。

```
# sysctl -A
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_rfc1337 = 0
net.ipv4.tcp_sturdg = 0
net.ipv4.tcp_abort_on_overflow = 0
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_syncookies = 0
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_retries2 = 15
net.ipv4.tcp_retries1 = 3
net.ipv4.tcp_keepalive_intvl = 75
net.ipv4.tcp_keepalive_probes = 9
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.ipfrag_time = 30
```

显示的项目是网络参数，实际上调优这些值超出了本书的范围。然而，如果我们想更改某个值，则使用 `-w` 命令：

```
# sysctl -w net.ipv4.tcp_retries 2=20
```

这增加了该特定内核参数的值。

# Apache 891

注意

Fedora Core 在 `system-config-proc` 中为 `sysctl` 命令提供了一个图形界面。它仍然是一个测试阶段的应用程序，必须从命令行启动。该界面本身平平无奇，它没有提供操作所有可能值的方法，但它为特定地址的内核变量提供了有用的帮助。

如果你发现某个特定设置很有用，你可以进入 `/etc/sysctl.conf` 文件。其格式如下（与之前的示例相同）：

```
net.ipv4.tcp_retries 2=20
```

对于内核黑客来说，比普通用户更感兴趣的是，`sysctl` 是一个持续开发和记录的潜在强大工具。

提示

内核在平衡图形系统性能方面做得很好，因此你无法做太多调优来让它运行得更快。

# MySQL

为 MySQL 服务器进行性能调优非常简单，这很大程度上是因为你只需要通过优化查询就能看到巨大的速度提升。尽管如此，只要你的系统有足够的 RAM，你就可以对服务器本身进行各种调优，以应对更高的负载。

关键在于理解它的缓冲区（buffers）——各种事务都有缓冲区和缓存（caches），找出它们的空满程度对于最大化利用性能至关重要。MySQL 在充分利用其缓冲区时性能最佳，而这会对系统 RAM 产生巨大需求。除非你的机器中拥有 4GB 或更多的内存，否则你没有足够的容量为所有缓冲区设置非常高值——你需要进行权衡选择。

## 衡量关键缓冲区的使用情况

当你向数据添加索引时，它能让 MySQL 更快地找到数据。然而，理想情况下，你希望这些索引存储在 RAM 中以获得最高速度，`key_buffer_size` 定义了 MySQL 可以为索引缓存分配多少 RAM。如果 MySQL 无法将索引存储在 RAM 中，你将会遇到性能问题。坦率地说，大多数数据库缓存的需求较小，但你应该测量你的使用情况，查看需要做哪些工作。

要做到这一点，在 MySQL 中输入 `SHOW STATUS LIKE 'key_read%';`。这会返回描述你的键缓冲区速率的所有状态字段——你应该会两行结果：`Key_reads` 和 `Key_read_requests`，它们分别是从磁盘读取的键的数量和从键缓冲区读取的键的数量。通过这两个数字，你可以使用这个简单的公式计算来自 RAM 和磁盘的请求百分比：

```
100 - (Key_reads / Key_read_requests) × 100
```

也就是说，将 `Key_reads` 除以 `Key_read_requests`，将结果乘以 100，然后从 100 中减去该结果。例如，如果你的 `Key_reads` 为 1000，`Key_read_requests` 为 100000，你将 100 除以 100000 得到 0.01；然后乘以 100 得到 1.0，再从 100 中减去得到 99。这就是来自 RAM 的键百分比，意味着你 99% 的键是从 RAM 提供的。

大多数人应该希望来自 RAM 的比例超过 95%，尽管主要的例外是你非常频繁地更新或删除键——MySQL 无法缓存更改。如果你的数据足够大，这个数字将在 98% 左右。较低的数字意味着你可能需要增加键缓冲区的大小。

如果你发现了问题，下一步是检查当前键缓冲区使用了了多少。使用 `SHOW VARIABLES` 命令并查找 `key_buffer_size` 变量的值。它可能是像 8388600 这样的数字，即 800 万字节，或 8MB。现在，使用 `SHOW STATUS` 命令并查找 `Key_blocks_used` 的值。

你现在可以通过将 `Key_blocks_used` 乘以 1024，除以 `key_buffer_size`，再乘以 100 来确定你的键缓冲区是如何使用的。例如，如果 `Key_blocks_used` 是 8000，你将其乘以 1024 得到 8192000；然后除以你的 `key_buffer_size` (8388600) 得到 0.97656，最后乘以 100 得到 97.656。因此，你几乎 98% 的键缓冲区被使用了。

现在，重点来了：你已经确定你正在从磁盘读取大量键，而且也知道从磁盘读取的原因几乎可以确定是因为没有为键缓冲区分配足够的 RAM。一个通用的规则是尽可能为键缓冲区分配大量 RAM，最高不超过系统 RAM 的 25%——在 512MB 的系统上，128MB 对于频繁读取键的系统来说是理想的。超过这个限制，由于系统必须为你的键缓冲区使用虚拟内存，你实际上会看到性能急剧下降。

在你的文本编辑器中打开 `/etc/my.cnf`，寻找包含 `key_buffer_size` 的行；如果没有该行，你需要创建一个——它应该在 `[mysql]` 这一行下方。当你设置新值时，不要随机选择一个非常高的数字。尝试设置你现在想做的任何值（如果还没有该行，就设置为 16MB）；然后看看效果如何。要将 16MB 设置为键缓冲区大小，你需要这样的一行：

```
[mysql]
set-variable = key_buffer_size=16M
datadir=/lib/mysql
```

使用 `service restart` 重启 MySQL 服务器，然后回到 MySQL 运行 `SHOW VARIABLES` 来查看 `key_buffer_size`。如果你将其设置为 16MB，它应该是 16773120。现在，MySQL 刚刚重置，它所有关于键命中和未中的值也将重置。

（注：原文后续部分存在重复，此处已按要求完成翻译逻辑）

参考 897

+   查找并修复慢查询。在你的 `/etc/my.cnf` 文件的 `[mysqld]` 节点下添加 `log-long-format` 和 `log-slow-queries = /var/log-slow-queries.log`，MySQL 将告诉你时间较长的查询。
+   使用 `OPTIMIZE TABLE tableName` 来整理表碎片并刷新索引。

# 参考

http://www.coker.com.au/bonnie—bonnie 的主页，一个磁盘基准工具。它还包含指向 RAID 基准测试工具和 Postal（一个用于 SMTP 服务器的基准工具）的链接。

http://httpd.apache.org/docs-2.0/perf-tuning.html—Apache 官方 Web 服务器调优指南。

http://dev.mysql.com/doc/mysql/mysql-optimization.html—直接从 MySQL手册学习如何优化 MySQL 服务器。

如果你运行大型网站，有一本特定的 MySQL 优化书籍将真正帮助你更好地利用系统，那就是 Jeremy Zawodny 和 Derek Balling 编写的《高性能 MySQL》（O'Reilly 出版），ISBN: 0-596-00306-4。

# 第 37 章

# 命令行大师课

## 本章内容

- * 为什么要使用 Shell？
- 基础命令
- 组合命令
- 多个终端
- 参考
