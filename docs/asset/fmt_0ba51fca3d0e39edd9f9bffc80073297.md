
15. 为了确保交换分区在启动时作为交换分区添加，应该在文件中创建条目？

A. `/etc/swaptab`

B. `/etc/sharestab`

C. `/etc/vfstab`

D. `/etc/dhcptab`

## 答案

1. 系统的是 `/proc`

2. `PR_ISSYS` 是系统进程标志。

3. `PR_VFORKP` 是 vfork 子父标志。

4. `PR_FORK` 是继承分区标志。

5. `PR_RLC` 是运行到最后关闭的标志。

6. `PR_KLC` 是杀死（最后关闭）的标志。

7. `PR_ASYNC` 是异步停止标志。

8. `PR_MSACCT` 是微状态计数标志。

9. `FORK` 是 fork 之后的微状态继承标志。

10. `-a` 命令用于添加交换空间。

11. `-s` 命令用于总结交换使用情况。

12. `-l` 命令用于列出交换使用情况。

13. `-d` 命令用于删除交换空间。

14. 文件和分区都可以用于交换。

15. 应该在 `/etc/vfstab` 中创建条目。

# 第 23 章：网络文件系统 (NFS)

439

| NFS 服务器 | NFS 客户端 |

![](img/0ce985fd07a5af27ed793d64cf4b977d_466_0.png)

图 23-2 NFS 服务器 carolina 使用其自身的挂载点，将其邮件目录共享给 NFS 客户端 georgia、fairfax 和 virginia。

RPC 的目的是抽象化在跨网络访问过程时所需的连接细节和方法——也就是说，客户端和服务器程序不需要实现单独的网络代码，因为系统提供了一个简单的 API，通过一个名为 portmapper（或 rbind）的服务来查找服务。为了让 NFS 正常运行，portmapper 至少应该运行在服务器上。

> 提示：portmapper 同时在 UDP 和 TCP 均已注册，因为可能会分别使用 NFS 2 或 NFS 3 生成或接收请求。

## 配置 NFS 服务器

如果你在安装过程中安装了 NFS 服务器，系统会在 `/etc/init.d` 中创建一个名为 `nfs.server` 的启动脚本。因此，可以通过输入以下命令手动启动 NFS 服务器：

```
/etc/init.d/nfs.server start
```

此命令将启动两个守护进程：NFS 服务器（`/usr/lib/nfs/nfsd`）和挂载守护进程（`/usr/lib/nfs/mountd`）。nfs 负责回答来自客户端对服务器共享卷的访问请求，而 mount 负责提供有关挂载文件系统的信息。

要检查 NFS 是否正确启动，可以使用以下命令检查 nfs 和 mount 的进程列表：

```bash
# ps -eaf | grep nfs
root 19961 1 0 0 Aug 31 ? 0:09 /usr/lib/nfs/nfsd -a 16
# ps -eaf | grep mount
root 370 1 0 May 16 ? 2:49 /usr/lib/nfs/mountd
```

或者，为了节省空间：

```bash
# ps -aef | grep 'mounted|nfsd'
```

# Sun 认证 Solaris 9.0 系统和网络管理员合一考试指南

在这种情况下，`nfsd` 和 `mountd` 都在正常运行。要停止 NFS 服务器，可以使用以下命令：

```bash
# /etc/init.d/nfs.server stop
```

NFS 服务器启动脚本还启动了一些可选服务，包括支持无盘启动的守护进程（反向地址解析协议守护进程 `/usr/sbin/bin.arpd` 和启动参数服务器 `/usr/sbin/rpc.bootparam`）。此外，还可以启动一个用于 x86 启动的独立守护进程（`/usr/sbin/rpld`），它使用网络启动 RPL（远程程序加载）。

![](img/0ce985fd07a5af27ed793d64cf4b977d_467_0.png)

> 提示：只有当你希望为本地客户端提供无盘启动时，才需要配置这些服务；否则可以安全地从 `/etc/init.d.nfs.server` 脚本中注释掉。

## 共享文件系统

要实际共享文件系统和目录，可以使用 `share` 命令。例如，如果你想从 georgia 共享 `/var/mail` 目录，可以使用以下命令：

```bash
# share -F nfs -o rw=georgia /var/mail
```

在这个示例中，“Nfs”代表“NFS 类型的文件系统”。当然，我们还想共享 VIRGINIA 和 fairfax，所以我们可能会使用这条命令：

```bash
# share -F nfs -o rw=georgia,virginia,fairfax /var/mail
```

将 `/var/mail` 卷共享给这些客户端，是因为这些系统上的用户需要读写他们的电子邮件。然而，如果我们需要共享 CD-ROM 卷，显然需要以只读方式共享：

```bash
# share -F nfs -o ro /cdrom
```

通常情况下，要共享的卷在 `/etc/dfs/dfstab` 文件中标识。NFS 的创新功能之一是，共享卷到其他系统的系统可以从自己的客户端远程挂载共享卷。例如，carolina 可以将 `/cdrom` 卷共享给 georgia、fairfax 和 virginia，virginia 可以使用以下命令将包含家目录的 `/staff` 目录共享给 carolina、georgia 和 fairfax：

```bash
# share -F nfs -o rw=georgia,virginia,fairfax /staff
```

文件系统可以使用 `unshare` 命令取消共享。例如，如果我们要在 carolina 上更改一个通过 NFS 共享给客户端的 CD-ROM，那么先将其卸载可能是更明智的：

```bash
# unshare -F nfs /cdrom
```

# 第 23 章：网络文件系统 (NFS)

441

要取消当前从 NFS 服务器上共享的所有卷，可以使用以下命令：

```bash
# unshareall
```

`dfmounts` 命令显示通过网络文件系统共享且当前由特定客户端挂载的本地资源：

```bash
# dfmounts
RESOURCE                PATHNAME               CLIENTS
carolina /cdrom         virginia,Georgia
carolina /var/mail      fairfax
```

然而，`dfmounts` 不提供关于共享了哪些文件系统的信息。要查看此，请使用 `dfshares` 命令。例如，查看服务器共享的卷：

```bash
# dfshares
RESOURCE                PATHNAME               CLIENTS
carolina /cdrom         virginia,Georgia
carolina /var/mail      fairfax
carolina /staff         virginia
```

要查看特定客户端上挂载了哪些卷，请使用 `dfmounts` 命令：

```bash
# dfmounts
RESOURCE                PATHNAME               CLIENTS
carolina /cdrom         virginia,Georgia
carolina /var/mail      fairfax
carolina /staff         virginia
```

表 23-1 NFS 服务器选项

| 参数 | 说明 |

| :--- | :--- |

| anon | 设置用户名。 |

| log | 启动日志。 |

| nosuid | 防止 setuid。 |

| nosub | 防止子目录。 |

| ro | 禁止写入。 |

| root | 允许 root 用户。 |

| sec | 指定认证级别（sys, krb4）。 |

| rw | 允许读写。 |

表 23-2 NFS 客户端选项

## 第 23 章：网络文件系统 (NFS)

| | | | | |

|---|---|---|---|---|

| 100007 | 1 | udp | 32774 | ypbind |

| 100007 | 3 | tcp | 32771 | ypbind |

| 100007 | 2 | tcp | 32771 | ypbind |

| 100007 | 1 | tcp | 32771 | ypbind |

| 100011 | 1 | udp | 32785 | rquotad |

| 100024 | 1 | udp | 32789 | status |

| 100021 | 1 | tcp | 32775 | status |
