

# 第四部分 ♦ 在 SUSE Linux 中实现网络服务

首先，我们来看客户端：我们将假设有一个可用的 NFS 服务器，并查看如何挂载 NFS 服务器提供的共享目录。在此阶段，你只需要知道 NFS 服务器能够以这种方式提供其上的一个或多个目录，使得网络上的其他机器可以挂载这些目录。例如，如果你知道服务器上通过 NFS 提供的目录是 `/share` 是可用的，你可以通过如下命令在客户端机器上挂载该共享：

```
root@client:~ # mount bable:/share /mnt
```

你应该能够切换到目录 `/mnt`，并看到在 `bable` 服务器的 `/share` 目录中存在的文件。

如果此命令挂起，可能是客户端上的 `portmap` 可能没有运行：请通过 `portmap status` 检查此项。如有必要，执行 `portmap start` 或 `portmap restart` 命令。当然，问题所在可能在服务器端，在这种情况下，你更有可能看到类似下面的错误：

```
mount: RPC: Remote system error - Connection refused
```

# 在启动时挂载 NFS 文件系统

你可能想在启动时挂载特定的 NFS 文件系统。你可能还想允许客户端非 root 用户自行挂载 NFS 共享。在这两种情况下，你都需要在 `/etc/fstab` 文件中包含适当的条目。正如此文件控制本地文件系统的挂载方式一样，你也可以控制 NFS 共享的挂载。

在此示例中，客户端 `/etc/fstab` 中的条目为：

```
bable:/test /testmount nfs user,mount,ro 0 0
```

客户端上的任何用户都可以通过执行 `mount /testmount` 命令，以只读方式挂载来自 `bable` 的指定目录到挂挂点。

要强制自动挂载目录，你可以使用以下命令：

```
bable:/test /testmount nfs rw 0 0
```

`/etc/fstab` 中的这一行确保了只要系统启动，NFS 共享就会以读写模式挂载，前提是客户端上的 `nfs` 服务被设置为在运行级别（runlevel）3 启动。关于使用 `/etc/fstab` 设置文件系统挂载选项的更多信息，请参阅第 3 章。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_628_0.png)

# 第 22 章 ◆ 使用 NFS 和 NIS 585

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_629_0.png)

要查看挂载了哪些文件系统（包括 NFS 挂载），只需输入 `mount` 即可。

# 使用 mount 选项

对 NFS 行为的大部分控制基于服务器；然而，`mount` 命令的某些选项会产生差异。

你可能想强制进行只读挂载（即使服务器提供了读写共享）。在命令行中，输入：

```
root@client: ~ mount bible:share /mnt -o ro
```

换句话说，挂载来自服务器 `bible` 的 `/share` 目录（通过挂载点 `/mnt` 可用），并在 `mount` 命令带有选项 `-o ro`，这意味着只读。

你还可以指定硬挂载（hard mount）或软挂载（soft mount）：

- 硬挂载（hard mount）——确保在 NFS 服务器变得不可用的情况下，访问挂载点的程序会挂起，但一旦服务器恢复，将能够恢复。
- 软挂载（soft mount）——客户端将向请求程序报告错误；并非所有程序都能正确处理这种情况，并且存在数据损坏的可能性。

要指定硬挂载，在 `mount` 命令的选项中（`-o` 之后）添加关键字 `hard`。例如：

```
root@client: ~ mount bible:share /mnt -o ro
```

事实上，`hard` 是默认值，因此你不需要显式指定它。NFS HOWTO 建议除非有其他理由，否则使用 `hard` 选项。`intr` 选项确保如果服务器不再响应，访问挂点的程序可以被 `kill` 信号中断。

你还可以尝试强制通过 TCP 传输而非 UDP 传输连接，在 `mount` 命令的选项列表中使用 `tcp`。UDP 是默认值，且 NFS over UDP 是无状态的；这意味着服务器可以重启而不破坏连接。然而，如果网络发生丢包，其效率较低，因为如果使用 TCP，每个数据包都会被确认并在未到达时重发。使用 UDP 时，只有整个请求完成后才会确认。

# 586 第四部分 ♦ 在 SUSE 中实现网络服务

`mount` 命令的其他选项是 `resize` 和 `wsize`，分别设置读取和写入块的大小。如果将这些设置为 `8192` 而非默认的 `1024`，预计性能将提高。`mount` 命令如下：

```
root@client:~ # mount bible:/share/mnt -o resize=8192 wsize=8192
```

在某些情况下，通过不同的值可以获得更好的性能，但如果这些参数与默认值太远，就会出现问题。

![](img/e4e45c9f32e76fb35fabbd21a96f1e_630.png)建议增加这些值，因为 Linux 内核对于大于页大小（x86 架构为 4096）的值执行预读。大于 `8192` 的值将提高 NFS 性能。该值需要 `1024` 的倍数，且不应大于 `16384`。

# rcnf start 和 rcnf stop

在 SUSE 系统上，NFS 客户端的操作被视为一种服务，并在 `/etc/init.d` 中有其启动脚本。`nfs start` 和 `nfs stop` 命令以 root 身份运行启动和停止 NFS 客户端。如果可能）任何 NFS 共享都包含在 `/etc/fstab` 中。如果挂载点不存在，卸载将失败。如果 `nfs` 服务未设置为在运行级别 3 和 5 启动，由于某些原因服务器无法访问，将需要长时间才能退出；通过在 `/etc/fstab` 中添加 `bg`（后台）选项可以避免这种情况。示例如下：

```
bable:/test /testmount nfs user,mount,ro 0 0
```

客户端上的任何用户都可以通过执行 `mount /testmount` 命令，以只读方式挂载来自 `bable` 的指定目录到指定挂点。

要强制自动挂载目录，你可以使用以下命令：

```
bable:/test /testmount nfs rw 0 0
```

`/etc/fstab` 中的这一行确保了只要系统启动，NFS 共享就会以读写模式挂载，前提是客户端上的 `nfs` 服务被设置为在运行级别 3 启动。关于使用 `/etc/fstab` 设置文件系统挂载选项的更多信息，请参阅第 3 章。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_628.png)

# 第 22 章 ◆ 使用 NFS 和 NIS 585

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_629_0.png)

要查看挂载了哪些文件系统（包括 NFS 挂载），只需输入 `mount` 即可。

# 使用 mount 选项

对 NFS 行为的大部分控制基于服务器；然而，`mount` 命令的某些选项会产生差异。

你可能想强制进行只读挂载（即使服务器提供了读写共享）。在命令行中，输入：

```
root@client: ~ mount bible:share /mnt -o ro
```

换句话说，挂载来自服务器 `bible` 的 `/share` 目录（通过挂载点 `/mnt` 可用），并在 `mount` 命令带有选项 `-o ro`，这意味着只读。

你还可以指定硬挂载（hard mount）或软挂载（soft mount）：

- 硬挂载（hard mount）——确保在 NFS 服务器变得不可用的情况下，访问挂载点的程序会挂起，但一旦服务器恢复，将能够恢复。
- 软挂载（soft mount）——客户端将向请求程序报告错误；并非所有程序都能正确处理这种情况，并且存在数据损坏的可能性。

要指定硬挂载，在 `mount` 命令的选项中（`-o` 之后）添加关键字 `hard`。例如：

```
root@client: ~ mount bible:share /mnt -o ro
```

事实上，`hard` 是默认值，因此你不需要显式指定它。NFS HOWTO 建议除非有其他理由，否则使用 `hard` 选项。`intr` 选项确保如果服务器不再响应，访问挂点的程序可以被 `kill` 信号中断。

你还可以尝试强制通过 TCP 传输而非 UDP 传输连接，在 `mount` 命令的选项列表中使用 `tcp`。UDP 是默认值，且 NFS over UDP 是无状态的；这意味着服务器可以重启而不破坏连接。然而，如果网络发生丢包，其效率较低，因为如果使用 TCP，每个数据包都会被确认并在未到达时重发。使用 UDP 时，只有整个请求完成后才会确认。

# 586 第四部分 ♦ 在 SUSE 中实现网络服务

`mount` 命令的其他选项是 `resize` 和 `wsize`，分别设置读取和写入块的大小。如果将这些设置为 `8192` 而非默认的 `1024`，预计性能将提高。`mount` 命令如下：

```
root@client:~ # mount bible:/share/mnt -o resize=8192 wsize=8192
```

在某些情况下，通过不同的值可以获得更好的性能，但如果这些参数与默认值太远，就会出现问题。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1_630.png)建议增加这些值，因为 Linux 内核对于大于页大小（x86 架构为 4096）的值执行预读。大于 `8192` 的值将提高 NFS 性能。该值需要 `1024` 的倍数，且不应大于 `16384`。

# rcnf start 和 rcnf stop

在 SUSE 系统上，NFS 客户端的操作被视为一种服务，并在 `/etc/init.d` 中有其启动脚本。`nfs start` 和 `nfs stop` 命令以 root 身份运行启动和停止 NFS 客户端（如果可能）任何 NFS 共享都包含在 `/etc/fstab` 中。如果挂载点不存在，卸载将失败。如果 `nfs` 服务未设置为在运行级别 3 和 5 启动，由于某些原因服务器无法访问，将需要长时间才能退出；通过在 `/etc/fstab` 中添加 `bg`（后台）选项可以避免这种情况。示例如下：

```
bable:/test /testmount nfs user,mount,ro 0 0
```

客户端上的任何用户都可以通过执行 `mount /testmount` 命令，以只读方式挂载来自 `bable` 的指定目录到指定挂点。

要强制自动挂载目录，你可以使用以下命令：

```
bable:/test /testmount nfs rw 0 0
```

`/etc/fstab` 中的这一行确保了只要系统启动，NFS 共享就会以读写模式挂载，前提是客户端上的 `nfs` 服务被设置为在运行级别 3 启动。关于使用 `/etc/fstab` 设置文件系统挂载选项的更多信息，请参阅第 3 章。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_628.png)

# 第 22 章 ◆ 使用 NFS 和 NIS 585

![](img/e4e45c9f32e76fb35fabbd21a96f1a1_629_0.png)

要查看挂载了哪些文件系统（包括 NFS 挂载），只需输入 `mount` 即可。

# 使用 mount 选项

对 NFS 行为的大部分控制基于服务器；然而，`mount` 命令的某些选项会产生差异。

你可能想强制进行只读挂载（即使服务器提供了读写共享）。在命令行中，输入：

```
root@client: ~ mount bible:share /mnt -o ro
```

换句话说，挂载来自服务器 `bible` 的 `/share` 目录（通过挂载点 `/mnt` 可用），并在 `mount` 命令带有选项 `-o ro`，这意味着只读。

你还可以指定硬挂载（hard mount）或软挂载（soft mount）：

- 硬挂载（hard mount）——确保在 NFS 服务器变得不可用的情况下，访问挂载点的程序会挂起，但一旦服务器恢复，将能够恢复。
- 软挂载（soft mount）——客户端将向请求程序报告错误；并非所有程序都能正确处理这种情况，并且存在数据损坏的可能性。

要指定硬挂载，在 `mount` 命令的选项中（`-o` 之后）添加关键字 `hard`。例如：

```
root@client: ~ mount bible:share /mnt -o ro
```

事实上，`hard` 是默认值，因此你不需要显式指定它。NFS HOWTO 建议除非有其他理由，否则使用 `hard` 选项。`intr` 选项确保如果服务器不再响应，访问挂点的程序可以被 `kill` 信号中断。

你还可以尝试强制通过 TCP 传输而非 UDP 传输连接，在 `mount` 命令的选项列表中使用 `tcp`。UDP 是默认值，且 NFS over UDP 是无状态的；这意味着服务器可以重启而不破坏连接。然而，如果网络发生丢包，其效率较低，因为如果使用 TCP，每个数据包都会被确认并在未到达时重发。使用 UDP 时，只有整个请求完成后才会确认。

# 586 第四部分 ♦ 在 SUSE 中实现网络服务

`mount` 命令的其他选项是 `resize` 和 `wsize`，分别设置读取和写入块的大小。如果将这些设置为 `8192` 而非默认的 `1024`，预计性能将提高。`mount` 命令如下：

```
root@client:~ # mount bible:/share/mnt -o resize=8192 wsize=8192
```

在某些情况下，通过不同的值可以获得更好的性能，但如果这些参数与默认值太远，就会出现问题。

![](img/e4e45c9f32e76fb35fabbd21a96f1a1_630.png)建议增加这些值，因为 Linux 内核对于大于页大小（x86 架构为 4096）的值执行预读。大于 `8192` 的值将提高 NFS 性能。该值需要 `1024` 的倍数，且不应大于 `16384`。

# rcnf start 和 rcnf stop

在 SUSE 系统上，NFS 客户端的操作被视为一种服务，并在 `/etc/init.d` 中有其启动脚本。`nfs start` 和 `nfs stop` 命令以 root 身份运行启动和停止 NFS 客户端（如果可能）任何 NFS 共享都包含在 `/etc/fstab` 中。如果挂载点不存在，卸载将失败。如果 `nfs` 服务未设置为在运行级别 3 和 5 启动，由于某些原因服务器无法访问，将需要长时间才能退出；通过在 `/etc/fstab` 中添加 `bg`（后台）选项可以避免这种情况。示例如下：

```
bable:/test /testmount nfs user,mount,ro 0 0
```

