
文件准备好导出后，是时候启动共享文件的程序和守护进程了：`exports(8)`、`rpc.quotat(8)`、`rpc.mountd(8)` 和 `rpc.nfsd(8)`。简单的方法是运行 `/etc/init.d/nfs start`。该命令在启动时会使用 `-r` 选项同步 `/var/lib/nfs/stab` 与 `/etc/exports` 文件内容。对于典型的 NFS 服务器，`exportfs` 会在启动时同步 `/var/lib/nfs/stab`。然而，有时你可能想手动运行 `exports(8)` 来检查哪些文件系统已导出；这是当你对 `/etc/exports` 做了更改，或者你只是为了临时共享文件系统而不进行永久更改时。注意你不应该手动编辑 `/var/lib/nfs/stab`；使用 `exports(8)`。

`rpc.quotat(8)` 为用户配额提供接口。`rpc.mountd(8)` 实现挂载协议。`rpc.nfsd(8)` 是 NFS 服务器守护进程。

## 文件共享

你可能会遇到这样的情况：你需要共享一个尚未共享的文件系统，并且编辑 `/etc/exports` 文件并运行 `exports(8)` 使用 `-a` 或 `-r` 选项之一，但你需要选择使用哪一个。记住，带有 `-r` 选项的 `exportfs(8)` 会用 `/etc/exports` 的内容更新 `/varfs/stab`，因此如果你使用此选项运行 `exports(8)`，你的任何临时导出都将从系统中消失。如果你没有共享任何文件系统，请使用 `-r`；另一方面，如果你已经共享了文件系统，请使用 `-a`，它会维护当前的文件系统并添加 `/etc/exports` 中列出的。下面的示例应该说明这种区别。

`etc/exports`:

| 要共享的文件系统 | 允许的客户端主机（可选主机列表） |
| :--- | :--- |
| `/usr/local` | `*.angrysungoy.com(async,ro,root_squash)` |
| `/var/mail` | `@dept_hosts(rw,sync)` |
| `/var/spool/news` | `192.168.0.19/24` |
| `/opt` | `ws1.angrysungoy.com(rw)` |

`exportfs -v`（详细模式）命令的输出，显示当前共享的内容：

```
/opt	ws1.angrysungoy.com(rw,async,wdelay,root_squash)
/var/spool/news	192.168.192.0/19(ro,async,wdelay,root_squash,all_squash)
```

### 关键子系统

第二部分

```
/usr/local *.angrysumuy.com(ro,async,wdelay,root_squash)
/var/spool/mail
@dept_hosts(rw,wdelay,root_squash)
```

从命令行临时导出一个文件：

```
exportfs -o ro ws1.angrysumuy.com:/mnt/cdrom
```

执行 `exports -v` 命令后的新输出：

```
/mnt/cdrom ws1.angrysumuy.com(ro,async,wdelay,root_squash)
/opt ws1.angrysumuy.com(rw,async,wdelay,root_squash)
/var/spool/news 192.168.192.0/19(ro,async,wdelay,root_squash,all_squash)
/usr/local *.angrysumuy.com(ro,async,wdelay,root_squash)
/var/spool/mail @dept_hosts(rw,wdelay,root_squash)
```

向 `/etc/exports` 添加新行以永久共享文件系统：

```
# Filesystem to share Allowed client hosts(list of options)
/usr/local *.angrysumuy.com(ro,async,root_squash)
/var/mail @dept_hosts(rw,sync)
/var/spool/news 192.168.192.0/19(all_squash) ws1.angrysumuy.com(rw,sync)
/opt ws1.angrysumuy.com(rw,async,wdelay,root_squash)
/home *.angrysumuy.com(rw)
```

运行 `exports -a` 共享新文件系统后，`exports -v` 的输出：

```
/mnt/cdrom ws1.angrysumuy.com(ro,async,wdelay,root_squash)
/home ws1.angrysumuy.com(rw,async,wdelay,root_squash)
/opt ws1.angrysumuy.com(rw,async,wdelay,root_squash)
/var/spool/news 192.168.192.0/19(ro,async,wdelay,root_squash,all_squash)
/usr/local *.angrysumuy.com(ro,async,wdelay,root_squash)
/var/spool/mail @dept_hosts(rw,wdelay,root_squash)
```

运行 `exportfs -r` 共享新文件系统后，`exports -v` 的输出：

```
/home ws1.angrysumuy.com(ro,async,wdelay,root_squash)
/opt ws1.angrysumuy.com(rw,async,wdelay,root_squash)
/var/spool/news 192.168.192.0/19(ro,async,wdelay,root_squash,all_squash)
/usr/local *.angrysumuy.com(ro,async,wdelay,root_squash)
/var/spool/mail @dept_hosts(rw,wdelay,root_squash)
```

你会注意到，在带有 `-r` 选项运行 `exports(8)` 后，`/mnt/cdrom` 不再被共享。这里的教训是共享文件系统时要小心，以免无谓地撤销已经完成的操作。

# 将 Solaris 8 系统配置为 NFS 服务器

我们将通过展示如何初始化服务器设置来开始讨论 Solaris NFS 服务器，然后跟后续介绍如何进行动态更改。

要设置 Solaris 8 NFS 服务器，你必须首先在 `/etc/dfs/dfstab` 中列出你想要共享的文件。然而，这不仅仅是待共享文件系统的列表；它实际上是一系列在 NFS 系统启动时运行的 `share (1M)` 命令列表。`share (1M)` 命令的作用正如其名：它让本地文件系统可以被远程客户端机器访问。现在来看示例的 `/etc/dfs/dfstab`，然后我们将为你提供有关 `share (1M)` 命令的背景知识。

```
# 一个示例 /etc/dfs/dfstab 文件
# Format: share [-f type] [-o options] [-d <type>] <pathname>
share -nfs -o rw,"Home directories" /export/home
share -nfs -o ro /cdrom
share -nfs -d "Mail files" /var/spool
```

`share (1M)` 命令只有几个参数，且它们都是可选参数（如果不带任何选项运行，`share (1M)` 命令仅报告当前主机已共享了哪些文件系统）。`-F` 参数指定指定的文件系统类型，可能是 `cachefs` 或 `autofs` 等。`/etc/dfs/fstypes` 列出了可用于共享的文件系统类型。请注意，服务器上的实际文件系统类型不是 `nfs`；`nfs` 指定的是所有访问它的客户端将看到的文件系统类型。`-d` 参数是对所共享文件系统的文本描述；你可以将其视为注释，当在不带任何参数运行 `share (1M)` 命令时，它会在输出中提供一些详细信息。

`-o` 参数用于指定共享文件系统的选项。选项既包括 `share (1M)` 命令的通用选项，也包括共享 nfs 类型的特定选项。事实上，当你为 `-F` 参数指定值为 `nfs` 时，你运行的是 `sharenfs(1M)` 命令，而不仅仅是 `share (1M)`。所有选项都在 `sharenfs(1M)` 命令的手册页中列出，我们将讨论其中一些有趣的选项。
