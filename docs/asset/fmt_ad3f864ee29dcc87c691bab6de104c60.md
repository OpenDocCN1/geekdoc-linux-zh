
```
{ sum += $7 } END { print sum }
```

（`END` 标签表示一段指令块，仅在所有行读取完毕后才运行）。

```
# find / -user taylor -type f -ls | \
awk '{ sum += $7 } END { print sum }'
27869349
```

看看；这是以字节为单位的，所以除以 `1024×1024` 会显示这是 26 兆字节。磁盘空间并不多，即使这个数字看起来确实很大！

当然，`awk` 也能做这个数学运算，

```
# find / -user taylor -type f -ls | \
awk '{ sum += $7 } END { print sum / (1024*1024) }'
26.5783
```

```
find / /usr /var /home -user $name -xdev -type f -ls | \
awk '{ sum += $7 } END { print sum / (1024*1024) " Mbytes " }'

done

exit 0
```

这里关于脚本有几件事值得提及。首先，`for` 循环被提供了一个 UID 大于等于 100 的用户名列表，以筛选出系统账户。这是通过更复杂的 `awk` 表达式完成的，如你所见。然后，我们将 `find` 限制在我们感兴趣检查的文件系统上，并使用 `-xdev` 确保它不会检查不感兴趣的系统。

这个版本的 `fquota` 的输出是

```
# fquota
User mthorne exceeds disk quota. Disk usage is: 0.0558786 Mbytes
User mdella exceeds disk quota. Disk usage is: 0.700355 Mbytes
User taylor exceeds disk quota. Disk usage is: 26.5783 Mbytes
User testdud exceeds disk quota. Disk usage is: 0.554475 Mbytes
```

- 4. 添加仅列出磁盘使用量超过 `MAXDISKUSAGE` 配额的用户的最后一步，是通过将整个 `for` 循环用子 shell 括号括起来，然后再次将输出传递给 `awk` 进行过滤来实现的：

```
#!/bin/sh

# FQUOTA - Disk quota analysis tool for Unix.
#          Assumes that all user accounts are >= UID 100.

MAXDISKUSAGE=20

( for name in `cut -d: -f1,3 /etc/passwd | awk -F: '$2 >= 99 { print $1 }'`
do
  echo -n "User $name exceeds disk quota. Disk usage is: "
  find / /usr /var /home -user $name -xdev -type f -ls | \
  awk '{ sum += $7 } END { print sum / (1024*1024) " Mbytes " }'
done ) | awk '{$9 > $MAXDISKUSAGE { print $0 } }'
exit 0
```

当运行这个版本的程序时，它会正确报告整个文件系统中哪些用户的磁盘配额超额：

```
# fquota
User taylor exceeds disk quota. Disk usage is: 26.5783 Mbytes
```

再多做一点工作，这就可以自动向用户发送电子邮件，温和地提醒他们压缩或删除一些文件，并为其他人腾出磁盘空间。

- 5. 那么如何让这个 Linux 脚本在 Mac OS X 上工作呢？令人惊讶的是几乎不需要更改。我们只需要省略 `-xdev`，因为 Apple 版本的 `find` 不理解它。当然，还有一些其他文件需要考虑：

```
# find / -user taylor -ls | wc -l
87308
```

主要问题是用户需要从 NetInfo 数据库中提取，而不是 `/etc/passwd`，因此我们需要使用 `ni report`，正如在第 5 小时“使用用户账户”中广泛讨论的那样。

把这一切结合起来，修改后的脚本看起来像这样：

```
#!/bin/sh

# FQUOTA - Disk quota analysis tool for Unix.
# Assumes that all user accounts are >= UID 100.

MAXDISKUSAGE=20

( for name in `ni report . /users name uid | awk '$2 > 99 { print $1 }'`
do
    echo -n "User $name exceeds disk quota. Disk usage is: "
    find / -user $name -xdev -type f -ls | \
    awk '{ sum += $7 } END { print sum / (1024*1024) " Mbytes" }'
done ) | awk '\$9 > $MAXDISKUSAGE { print \$0 }'

exit 0
```

输出很有趣：

```
# fquota
User taylor exceeds disk quota. Disk usage is: 17162.5 Mbytes
```

那个 `taylor` 小子用了大量的磁盘空间！！我得跟他谈谈！

在 Unix 中编写一个简单的配额管理系统并不特别困难。毕竟，有数百种不同的实用程序随时待命，坦白说，几乎没有什么你拼凑不出来的！

然而，如果你的系统有内置的配额系统，让文件系统本身强制执行配额限制是有优势的，特别是如果你担心失控的用户可能会在周末下载 MP3 并完全填满磁盘。

#### 摘要

本小时探讨了磁盘配额的概念，以及使用内置工具与使用文件系统一部分的系统工具之间的区别。每种解决方案都有利有弊，当然，如果你忽略磁盘配额并用完磁盘空间，也会潜伏潜在问题。如同许多管理问题一样，没有简单的答案。

#### 问答

**Q 配额不是坏事吗？我的意思是，美国最高法院不是投票说配额违反了美国宪法吗？**

**A** 嗯，即使在这个加速的 24 小时格式下，你可能也有太多空闲时间了。美国最高法院确实推翻了配额，最著名的是 1978 年的加州大学董事会诉 Bakke 案，但，真的，这相关吗？

**Q 为什么这么多系统管理员反对配额？**

**A** 这在某种程度上与前一个问题有关，并且肯定与黑客社区的无政府主义倾向有关，许多系统管理员确实强烈反对配额或任何其他人为施加的使用限制。然而，即使磁盘空间一美分一兆字节，也不可能让每个人都使用他们想要的任意空间。必须有一些限制，如果是这样，配额是一个相当优雅的，而且肯定是平等主义的解决方案。

**Q Windows 上使用磁盘配额系统吗？**

**A** 是的。你可以为几乎任何版本的 Windows 获取磁盘配额管理系统。Shareware 仓库 Download.com 有九个，包括 Northern.Net 的 slick Quota Server（但请注意，它要价 900 美元）。

#### 工作坊

##### 测验

- 1. 硬配额限制和软配额限制有什么区别？
- 2. 启用磁盘配额之前的第一步是什么？
- 3. 系统内置配额的一个主要限制是....
- 4. `wall` 命令的目的是什么？
- 5. 添加 `quota` 命令调用的推荐位置在哪里？

![](img/5ced0c78d748bd190e9027e5549a3622_259_0.png)

##### 答案

- 1. 软限制是用户在没有任何警告的情况下可以消耗的最大磁盘空间量。当他们超出软限制时，系统会抱怨但仍允许他们继续。硬限制是不可违抗的约束，系统将拒绝用户添加新文件甚至扩大文件的尝试。
- 2. 第一步是编辑 `/etc/fstab`（或 Solaris 上的 `vfstab`）以在挂载时启用配额。
- 3. 一个主要限制是配额系统不跨多个文件系统，因此虽然可以限制用户每个设备的特定空间量，但没有内置机制来限制整体磁盘使用。
- 4. `wall` 命令允许你向当时登录的每个用户发送即时消息。
- 5. 如果你启用配额，在每个用户的 `.login` 或 `.bash_profile` 中添加对 `quota`（或根据需要 `quota -v`）的调用是非常明智的做法。

在下一小时，我们将转换思路并开始查看进程和系统控制。我们将重点关注 Unix 系统的启动和关闭，包括对运行级别和 `init` 状态的广泛讨论。这是任何系统管理员必读的内容！

![](img/5ced0c78d748bd190e9027e5549a3622_261_0.png)

## 第五部分

## 进程与系统控制

## 小时

- 13 更改系统状态 247
- 14 探索进程 265
- 15 将作业运行在未来 285
- 16 管理你的日志文件 301
