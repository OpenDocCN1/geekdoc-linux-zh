
（在上述 dump 输出中没有匹配到大小行）在这种情况下，显然需要修复 `/dev/sd0h` 上的权限。如果你通过查看日志来解决问题，可能需要查看 [Amanda](https://example.org) 的存档。

这些日期决定了包含了我们可能想要恢复的状态的磁带范围。

| 日期 | 主机 | 磁带 | 状态 |
|---|---|---|---|
| 1999-09-26 | zamboni | c0t0d0s | Podunk | 33 |
| 1999-09-25 | zamboni | c0t0d0s | Podunk | 41 |
| 1999-09-23 | zamboni | c0t0d0s | Podunk | 9 |
| 1999-09-22 | zamboni | c0t0d0s | Podunk | 32 |
| 1999-09-13 | zamboni | c0t0d0s | Podunk | 38 |
| 1999-09-12 | zamboni | c0t0d0s | Podunk | 37 |
| 1999-09-11 | zamboni | c0t0d0s | Podunk | 39 |
| 1999-09-10 | zamboni | c0t0d0s | Podunk | 72 |
| 1999-09-09 | zamboni | c0t0d0s | Podunk | 44 |
| 1999-09-08 | zamboni | c0t0d0s | Podunk | 88 |
| 1999-09-07 | zamboni | c0t0d0s | Podunk | 35 |
| 1999-09-06 | zamboni | c0t0d0s | Podunk | 33 |
| 1999-09-05 | zamboni | c0t0d0s | Podunk | 32 |
| 1999-09-04 | zamboni | c0t0d0s | Podunk | 51 |
| 1999-09-03 | zamboni | c0t0d0s | Podunk | 16 |
| 1999-09-02 | zamboni | c0t0d0s | Podunk | 19 |
| 1999-10-01 | zamboni | c0t0d0s | Podunk | 36 |
| 1999-09-30 | zamboni | c0t0d0s | Podunk | 15 |
| 1999-09-29 | zamboni | c0t0d0s | Podunk | 78 |
| 1999-09-28 | zamboni | c0t0d0s | Podunk | 99 |

`Amanda` 将决定我们需要哪些磁带。

# 第 10 章 备份

接下来，我们使用 `amrestore` 来实际恢复数据。我们将从磁带 `Podunk-509` 开始，因为它是层 0 备份。在将磁带插入带驱动器之前，我们可以运行

```bash
% amrestore -p /dev/rmt/0bn zamboni c00d0s7 | restore if -
```

来定位相应的记录并启动交互式恢复。`amrestore` 会查看输出中的每个 dump 镜像，直到找到我们要的，然后将 dump 镜像输出到标准输出，供 `restore` 命令读取。实际的恢复过程如第 180 页开始的描述所示。从层 0 磁带中提取后，我们对层 1 磁带重复此过程。

`amrestore` 可以识别出相应的 dump，因为 `Amanda` 在每个 dump 镜像前都放置了一个 32K 的头部，说明了它的来源以及是如何压缩的。如果使用了压缩，`amrestore` 会自动将磁带镜像通过通过适当的解压器。

搜索所有头部可能需要很长时间，因为 `amrestore` 可能需要跳过数百个文件系统。`amandin` 的输出显示了我们正在查找的文件，因此没有必要让 `amrestore` 完成所有这些工作。我们可以在运行 `amrestore` 之前简单地运行 `mst fs` 来快进磁带。

你必须在生成原始 dump 的相同操作系统和架构上运行恢复过程。`Amanda` 对 dump 的实际内容一无所知，无法保护你免受跨平台兼容性问题。

如果 `Amanda` 日志被删除，我们始终可以通过查看磁带标签找到需要的磁带。但如果 `amrestore` 本身被删除了呢？不要担心：`amrestore` 执行的操作并不比 `dd` 多。如果你查看要恢复的备份的 32K 头部，你会看到恢复它的指令。例如，这里是层 0 磁带的头部：

```
# mst -f /dev/rmt/0bn fs 99
# dd if=/dev/rmt/0bn bs=32k count=1
AMANDA: FILE 1990928 bamboni c0d0s7 level 0 .gz
```

要恢复，将磁带置于文件开头并运行：

```
df if=<tape> bs=1 skip=1 gzip | restore ... {}
```
