
```
xfsdump: creating dump session media file 0 (media 0, file 0)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsdump: dumping non-directory files
xfsdump: ending media file
xfsdump: media file size 276971520 bytes
xfsdump: creating dump session media file 1 (media 0, file 1)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsdump: dumping non-directory files
xfsdump: ending media file
xfsdump: media file size 274022400 bytes
xfsdump: creating dump session media file 2 (media 0, file 2)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsdump: dumping non-directory files
xfsdump: ending media file
xfsdump: media file size 274022400 bytes
xfsdump: creating dump session media file 3 (media 0, file 3)
xfsdump: dumping ino map
xfsdump: dumping directories
xfsdump: dumping non-directory files
xfsdump: ending media file
xfsdump: media file size 204226560 bytes
xfsdump: dumping inventory
xfsdump: beginning inventory file
xfsdump: media file 4 (media 0, file 4)
xfsdump: ending inventory file
xfsdump: media file size 491520 bytes (wait, 491520)
xfsdump: I/O metrics: 3 by 240KB; 4186 (100%) streamed; 5266 B/s
xfsdump: dump size (non-dir files): 1006325552 bytes
xfsdump: dump complete: 2228 seconds
```

# 保存你的世界：制作磁带备份

一个用于 IRIX xfs 文件系统的 `xfsdump` 语句为流式备份提供了支持。在这个语句中，`-l` 是备份级别，`-b` 是块因子，`-m` 是指示磁带驱动器不是本地机器的标志，`-M` 是磁带名称，`-L` 是会话名称。要备份的文件系统是 `/1a`。使用 `xfsdump` 你也可以提供要备份的特定目录或文件。传统的 `dump` 只备份文件。你不需要为 `xfsdump` 提供任何特殊规格。在这里，块因子取决于你的需求，在这种情况下，只有当磁带设备不是本地时才需要。注意，传统的 `dump` 输出以 KB 为单位，而 `xfsdump` 以字节为单位。即使是最新版本的 IRIX，你也无法摆脱字节单位测量！

这是一个意外输出的示例：

```
xfsdump: WARNING: could not open regular file 5655013 mode 0x0000814:

Invalid argument: not dumped

xfsdump: WARNING: could not open regular file 5655019 mode 0x0000814:

Invalid argument: not dumped

xfsdump: WARNING: could not open regular file 5655025 mode 0x0000814:

Invalid argument: not dumped

xfsdump: WARNING: could not open regular file 5655036 mode 0x0000814:

Invalid argument: not dumped

xfsdump: WARNING: could not open regular file 5655046 mode 0x0000814:

Invalid argument: not dumped

xfsdump: WARNING: could not open regular file 5655056 mode 0x0000814:

Invalid argument: not dumped
```

我曾在不久后损坏的驱动器上得到类似的输出。如果你运行 `dump` 时遇到类似的输出，可能是时候该完整备份并开始买新的设备了。

# 故障排除 dump

如果 `dump` 在带有磁带驱动器的机器上工作，但在其他机器上不工作，你可能需要为带有磁带驱动器的机器创建一个 `.hosts` 文件。`.hosts` 文件应该包含每个允许访问磁带驱动器的机器的条目，格式如下：

```
mother.politically.correct.com root
```

此外，当你在 `/etc/inetd.conf` 中关闭服务时，可能禁用了 `rsh`。你应该只在带有磁带驱动器的机器上启用该服务，并在 `/etc/hosts.allow` 文件中添加如下条目：

```
in.rsh: 192.168.1.4
```

![](img/74418f52d5d454acca60721059dbdc99_390_0.png)

仅指定允许访问磁带驱动器的机器。因此，如果驱动器的机器应该允许你的三台机器集群访问它的磁带，那么你的 `/etc/hosts.allow` 文件将包含这三个 IP 地址：

```
in.rshd: 192.168.1.4 192.168.1.20 192.168.1.8
```

# 从磁带恢复到你的机器：使用 restore

让 `dump` 工作是一回事，从磁带上成功恢复是另一回事。在实际需要之前，在测试从磁带恢复数据时，请做好笔记。在系统的非关键位置进行测试。对你需要做什么有一个大致的了解。你最终可能无法恢复到你希望的确切位置，但你可以随时移动磁带。

# 准备恢复

对于传统的恢复，你可能需要的信息是块因子和磁带驱动器的名称。对于流式备份的恢复，你还需要包含要恢复的数据的会话名称。如果你选择交互式会话，你可能不需要担心太多的选项。使用 `dump` 时，请务必阅读你操作系统版本的 `restore` 手册页。

恢复时需要哪些磁带取决于你需要恢复的内容。如果你只需要恢复一个昨天更新过的文件，那么今天的 `dump` 和今天的磁带就足够了。但请记住，你可能需要从最近的完整备份、每月、每周和每日磁带的适当组合进行恢复。

# 备份你的世界：制作备份或磁带

## 执行传统的恢复

我将恢复一个从主目录中删除的目录。为了完成此任务，我需要最近的相应级别的磁带。在我这里，我需要最近的第 0 级、2 级和第 4 级磁带。

我将首先从第 0 级磁带恢复基础内容。我的标签显示我使用了 128 的块因子（blocking factor），并且我要的目录在磁带的第一个文件系统上。运气真好！

当我将磁带放入驱动器（在本例中位于设备 `/dev/rmt/on`）时，我决定先将其倒带一下：

```
Rosalyn joray 202 > -f /dev/rmt/on rewind
```

因为我需要的内容在磁带的开头。我不需要进一步导航。我可以继续执行恢复命令，在 Solaris 上该命令是 `fsrestore`：

```
Rosalyn joray 202 # fsrestore 1b2f /dev/rmt/on
```

我指定的选项分别是：`i` 表示交互式，`b` 表示分块，`f` 表示磁带设备。因为我选择了交互式恢复模式，我得到了一个提示，我可以在其中运行 `ls`，正如你预期的那样，它列出了磁带的内容：

```
fsrestore > ls
```

```
apache.tar college.tar joray.tar restoretable

andy/ ger/ jack/ testing/

college/ joray/ last+found/
```
