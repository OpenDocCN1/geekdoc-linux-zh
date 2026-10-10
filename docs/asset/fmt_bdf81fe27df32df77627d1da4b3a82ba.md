
使用 ZFS，在进行系统维护（如升级）之前创建快照是一个好主意。如果升级失败，你可以回滚到最后一个可用版本。为了调试失败的升级，将快照复制到测试系统进行调试，而你的生产系统保持运行在旧的操作系统版本上。

“启动环境”在系统维护之前打包成一个整洁的包。你不需要启动环境管理器来使用快照，但管理器让这些操作变得简单得多。FreeBSD 有一个启动环境管理器，`beadm`。

你现在准备好使用启动环境了。

### 查看启动环境

每个启动环境都是 `zroot/ROOT` 下的一个数据集。你刚刚安装了启动环境。使用 `beadm list` 查看所有启动环境。

```
#### beadm list
BE      Active  Mountpoint Space   Created
default NR        /        649.9M   2016-02-15 14:47
```

有一个名为 `default` 的环境，位于 `zroot/ROOT/default`。这是一个新安装的系统，这是符合预期的。

`Active` 列显示启动环境是否正在使用。`N` 表示该环境正在运行。`R` 表示该环境将被激活。

`Mountpoint` 列显示启动环境的位置。`Space` 列显示磁盘空间。`Created` 列显示创建环境的日期。

### 创建启动环境

在更改系统之前，创建一个启动环境。用补丁命名该环境。使用 `freebsd-update` 版本。

```
#### freebsd-version
```

等待，`Space` 列显示已用空间。`Created` 列显示创建环境的日期。

```
BE      Active  Mountpoint Space   Created
default NR        /        649.9M   2016-02-15 14:47
```

有一个名为 `default` 的环境，位于 `zroot/ROOT/default`。这是一个新安装的系统，这是符合预期的。

### 激活启动环境

假设你应用了最新的补丁，结果机器失控了。你的服务器崩溃了，内核恐了，或者小鬼精从 USB 端口跳出来偷走了你的勺子。通过激活启动环境并重启回退到旧版本。使用 `beadm` 激活启动环境。

```
#### beadm activate 10.3-release
Activated successfully
#### beadm list
```

`BE      Active  Mountpoint Space   Created`

`default N        /        308.1M   2016-05-19 10:04`

`10.3-release R -        457.1M   2016-05-19 14:13`

`default` 环境的 `Active` 标记为 `N`，意味着它正在运行。`10.3-release` 环境的 `Active` 标记为 `R`，所以重启后它将被激活。

重启系统，你突然回到了运行 `10.3-release` 环境，没有任何安全更新，并带有你最初安装的任何软件包。

空间。这些启动环境中的某些你可能再也不会使用了。

```
#### beadm list
| BE | Active | Mountpoint | Space | Created |
| :--- | :--- | :--- | :--- | :--- |
| default | NR | / | 3.6G | 2015-04-28 11:53 |
| install | | | 126.0M | 2015-04-28 12:19 |
| 10.3-p9 | | | 209.0M | 2015-05-14 08:01 |
| 10.3-p10 | | | 169.0M | 2015-05-24 11:02 |
| 10.3-p10-13Jun | | | 150.0M | 2015-06-10 14:24 |
| 10.3-p10-13Jun | | | 47.3M | 2015-06-13 06:19 |
| 10.3-p12 | | | 7.7M | 2015-06-19 07:06 |
```

使用 `freed-version` 告诉我这个特定的系统运行的是 FreeBSD 10.3-RELEASE-p13。我想我可能想回退到10.3-p12。但我不会回到 p10、或 p9，特别是尤其是 install 版本。删除这些启动环境将节省磁盘空间，并让我现有的启动环境更易阅读和理解。

使用 `beadm destroy` 和启动环境名称来移除不需要的启动环境。

```
#### beadm destroy 10.3-release
Are you sure you want to destroy '10.3-release'?
This action cannot be undone (y/[n]): y
Destroyed successfully
```

我 FreeBSD 10.3 的原始安装现在已经从这个系统中消失了。剩下的所有内容都以某种方式经过了修复。这可能会释放根池（root pool）上的一些空间——并不是所有启动环境使用的空间，快照和克隆在最后一个需要该块的快照被删除之前不会释放空间。但你会找回一些空间。

## 启动环境与 ZFS

启动环境利用了 ZFS 快照和克隆。但它们究竟是做什么的？看看我们最初安装在宿主机上的快照。

```
#### zfs list -t snapshot
| NAME | USED | AVAIL | REFER | MOUNTPOINT |
| zroot/ROOT/default@2016-02-16-08:35:22 | 25.9M | - | 479M | - |
```

这台主机有一个快照，以我创建的启动环境命名。默认启动环境是当前运行的那个，所以它不需要快照。现在看 `zroot/ROOT` 下的数据集。
