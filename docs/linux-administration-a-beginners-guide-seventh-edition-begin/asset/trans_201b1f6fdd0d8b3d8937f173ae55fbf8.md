

## 620 Linux 系统管理：入门指南

如果服务没有运行，请启动它。如果它已停止或禁用，可以使用此命令启动：

```
[root@serverA ~#] systemctl start rpcbind
```

> 提示：在 openUSE 系统上，上述命令的等命令是 rpcbind status 和 rpcbind start。

在其他没有 `systemctl`、`start`、`stop` 或 `status` 命令的发行版中，你可以尝试在 `/etc/init.d/` 目录下查找名为 `rpcbind` 的文件。然后你可以手动执行该文件并使用状态或选项来控制 rpcbind 服务，例如输入 `#etc/init.d/rpcbind status`。

- 4. NFS 服务，它将启动所需的所有其他辅助服务。在 Fedora 等启用 systemd 的 Linux 发行版上，通过输入以下命令使用 systemctl 命令启动服务：

```
[root@serverA ~#] systemctl start nfs-server
```

- 5. 使用 `exportfs` 命令运行重新导出 `/etc/exports` 中的目录：

```
[root@serverA ~#] exportfs -r
```

- 6. 要检查你的导出是否配置正确，运行 `showmount` 命令：

```
[root@serverA ~#] showmount -e localhost
```

- 7. 如果你没有看到放入 `/etc/exports` 的文件，请检查 `/var/log/messages` 查看 `nfsd` 或 `mount` 可能记录的任何输出。对于启用了 journal 的系统，你也可以使用 `journalctl -f xe` 来实时监控命令。

如果你需要对 `/etc/exports` 进行更改，在完成更改后不要忘记加载或重启 nfsd 服务，并运行 `exportfs -r`。最后，运行 `showmount -e` 以确保更改生效。

- 8. 现在你已经配置好了服务器，是时候设置客户端了。检查客户端和服务器之间的 RPC 机制是否工作正常。你将再次使用 `showmount` 命令验证客户端是否可以看到共享。如果客户端看不到共享，你可能存在网络问题或到服务器的权限问题。从 clientA 发出以下命令：

```
[root@clientA ~#] showmount -e serverA
Export list for serverA:
/usr/local (everyone)
```

## 第23 章 网络文件系统 (NFS) 621

**提示** 如果 `showmount` 命令返回类似 'clnt_create: RPC: Port mapper failure - Unable to receive: errno 113 (No route to host)' 或 'clnt_create: RPC: Port mapper failure - RPC: Unable to receive,' 的错误，你应该确保 NFS 服务器上运行或 NFS 服务器与客户端之间的防火墙没有阻塞通信。

9. 一旦你确认可以从客户端查看共享，就是时候看看是否可以成功挂载文件系统了。首先创建 `/mnt/usr/local/`，然后按照如下方式使用 `mount` 命令：

```
[root@clientA ~]# mkdir -p /mnt/usr/local
[root@clientA ~]# mount -o rw,bg,int,soft serverA:/usr/local /mnt/usr/local
```

10. 你可以使用 `mount` 命令仅查看在 clientA 上挂载的 NFS  own文件系统。输入以下内容：

```
[root@clientA ~]# mount -t nfs
```

或者对于 NFS4 挂载，你应该运行：

```
[root@clientA ~]# mount -t nfs4
```

11. 如果这些命令成功，你可以将带有选项的挂载条目添加到 `/etc/fstab` 文件中，以便它们在重启时远程挂载文件系统：
serverA:/usr/local /mnt/usr/local nfs rw,bg,int,soft 0 0

## NFS 的常见用途

以下想法当然只是一些想法。你可能有自己的理由来通过 NFS 共享文件系统。

- **存放流行程序** 如果你习惯 Windows，你可能处理过某些拒绝安装在网络共享上的应用程序。由于这样或那种原因，这些程序希望每个系统都拥有自己的软件副本——这是一种令人困扰，特别是当有大量机器需要该软件时。Linux（通常指 UNIX）很少有这种情况。

- **存放用户主目录** NFS 的另一个用途是存放用户主目录。

- **共享数据** NFS 的一个常见用途是在多个客户端之间共享数据。

## 总结

在本章中，我们讨论了设置 NFS 的过程。这里是一些需要记住的点：

- NFS 已经存在很长时间了，并且经历了多次版本修订。
- NFS2 和 NFS3 中的关键进程是 `statd`、`quotad`、`mount` 和 `nfsd`。
- NFS4* 是最新版本，具有许多以前没有的功能。

