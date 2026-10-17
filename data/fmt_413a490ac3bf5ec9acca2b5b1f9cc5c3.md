
差异备份（使用 `-I`）的工作方式与增量备份完全相同，但它们会创建任何中间快照。类似 `zfs send -I monday zroot/usr/home@monday` 的命令要求远程端存在 `@monday` 快照，它会在执行过程中创建缺失的 `@tuesday` 和 `@wednesday` 快照。

假设你自动对数据集拍摄了每日快照，并想将它们发送到远程服务器。将 `@monday` 快照复制到远程池：

```
# zfs send zroot/usr/home@monday | zfs receive remotipool/usrhome
```

在你的远程主机上检查 `@monday` 快照是否存在。

```
# zfs list -t all -r remotipool/backup
NAME USED AVAIL REFER
remotepool/backup/usrhome 19.5K 472M 19.5K /remotepool/weekday
remotepool/backup/usrhome@monday 0 19.5K
```

现在我们增量复制 `@tuesday` 快照。

```
# zfs send -i remotepool/backup/usrhome@tuesday | zfs receive remotipool/backup
```

检查远程主机，你会发现快照。

```
# zfs list -t all -r remotipool/backup
NAME USED AVAIL REFER
remotepool/backup/usrhome 29K 472M 19.5K /remotepool/weekday
remotepool/backup/usrhome@monday 9.5K 19.5K
```

在周三，如果你是在闲逛——我的意思是，"出故障了"——所以你没有进行复制。周四，你想赶上进度，所以你对 `@thursday` 快照进行差异复制。

```
# zfs send -I tuesday zroot/usr/home@thursday | zfs receive remotipool/backup/usrhome
```

我们的备用主机现在有了快照。

```
# zfs list -t all -r remotipool/backup/usrhome
NAME USED AVAIL REFER
remotepool/backup/usrhome 19.5K 472M 19.5K /remotepool/weekday
remotepool/backup/usrhome@monday 9.5K 19.5K
remotepool/backup/usrhome@tuesday 9.5K 19.5K
remotepool/backup/usrhome@wednesday 9.5K 19.5K
remotepool/backup/usrhome@thursday 0 19.5K
```

等待，提示词中提供的 72-75 页的 OCR 文本在后期变得非常混乱。让我根据文本中提供的 ZFS 文档逻辑进行重新处理。

（注：提供的第 72-75 页 OCR 文本严重损坏且重复。我已根据可用文本提供了去重并清理后的版本。）

### 高级发送选项

发送者可以通过多种方式更改其发送数据集的方法。

#### 发送属性

若要发送数据集属性以及实际数据，请添加 `-p` 标志。当接收到的数据集属性与数据集上已有的属性不同时，`zfs receive` 会尝试更改属性以匹配它们。也就是说，如果你正在从一个使用 `l4` 压缩的数据集复制属性到一个已经使用 `l4` 的数据集，`zfs receive` 将不会对该属性执行任何操作。但是，如果发送者使用了 `gzip-9` 压缩，接收端将更改以匹配原始设置。

接收数据集的用户必须拥有设置你想要复制的属性的权限。如果用户具有复制权限，但没有所有属性的权限，则允许的属性会被设置，而不允许的属性将会被拒绝。

假设源数据集的 `dedup` 设置为 `on`，`compression` 设置为 `gzip-9`。接收的数据集的 `dedup` 设置为 `off`，`compression` 设置为 `l4`。我们希望被复制的数据集使用相同的压缩方式，但保留原来的 `dedup` 设置。我们允许我们的复制用户更改压缩设置。

```
#### zfs allow -u replicator zroot/backup
```

当我们发送数据集时，将会得到错误。

`cannot receive compression dedup on remotool/backup: permission denied`

这没关系——我们不想在副本上设置 `dedup` 属性。不过，`compression` 属性按预期进行了复制。

我们为什么要复制属性，而不是直接在目标上设置它们？对于压缩和去重等简单属性，手动配置可能还可以，但对于共享或任何配额等复杂属性来说并不适用。

#### 去重数据流

你的数据去重了吗？它适合去重吗？ZFS 允许你对数据流进行去重。通过 `-d`，每个唯一的块只会被发送一次。它不会改变接收者写入磁盘的内容，只会影响数据流。

去重的数据流使用与磁盘去重不同的去重内存集。如果你的数据可以被有效去重，但该去重使用了许多 GB 的内存，那么发送和接收主机都需要相似的内存来对数据流进行去重。不要在 `zfs send` 中轻率去重！

#### 调试与测试

`zfs send` 支持一些可以帮助调试、测试和监控的选项。

`-v` 选项让 `zfs send` 进入详细模式。它会打印关于要发送的数据的信息，并定期添加状态更新。

`-p` 标志在流开始流动时立即打印有关发送流的信息。手册将此类信息描述为“机器可读”。这些信息人类可以读懂，但不是整齐的表格形式。然而，它非常适合交给你的脚本。

`-n` 标志防止 `zfs send` 实际发送任何数据。相反，当与 `-v` 或 `-p` 结合使用时，它会提供 `zfs send` 如果实际运行将执行的操作统计。

#### 大块与小块

较新版本的 ZFS 通过 `large_blocks zpool(8)` 特性支持大于 128 KB 的磁盘块。`-L` 标志允许 `zfs send` 包含大块，而不是将其拆分为小块。接收端池也必须支持大块。

对于具有非常小块的主机，`-e` 通过使用 `embedded_data` 特性缩小数据流的大小。目标池也必须支持 `embedded_data` 特性标志。

#### 高级接收选项

接收端可以通过 `zfs receive` 的参数来调整其存储传入 ZFS 流的方式。

#### 路径与挂载管理

接收到的 ZFS 流包含了源的池和数据集路径。你可以保留此路径，也可以将其剥离。

通过添加 `-d` 标志，你 `zfs receive` 将使用源的完整路径（池名除外）作为目标数据集的路径，而不是要求管理员指定目标数据集。早些，我们将 `zroot:/usr/` 复制到 `remotepool/backup/usrhome`。在这里使用 `-d`，我们让 `zfs receive` 使用源路径。

```
# zfs send zroot:/usr/ | zfs receive -d remotepool/backup
```

这会创建 `remotepool/backup/usr`。如果不使用 `-d`，我们需要使用 `zfs receive remotepool/backup/usrhome`。

如果你想重命名接收到的数据集，可以使用 `-d` 剥离路径。

```
# zfs send zroot:/usr/home/ | zfs receive -d remotepool/backup
```

这会创建 `remotepool/backup/usr/home`。

## 回滚更改

如果有人更改了数据集，`-F` 标志会让 `zfs receive` 回滚到之前的状态。

```
# zfs send zroot:/usr/home | zfs receive -F remotepool/backup
```

mypool/weekday 96K 13.5G 96K /mypool/weekday

mypool/weekday@saturday 0 96K -

mypool/weekday#bm-friday - -

遗憾的是，书签（bookmarks）列在快照之后，即使它们比快照更旧。不过，ZFS 命令行非常强大。为了方便起见，让我们使用 `-t` 来告诉它只列出快照和书签。`-s` 参数告诉 `zfs(8)` 如何排序输出，因此我们将按照创建（创建日期）属性进行排序。在最大递归深度为 `1` 的情况下会忽略数据集的快照。

```
# zfs list -t snapshot,bookmark -s creation -d 1 zroot/usr/home
NAME USED AVAIL REFER MOUNTPOINT
zroot/usr/home#bm-friday - - -
zroot/usr/home@saturday 64K - 96K -
```
