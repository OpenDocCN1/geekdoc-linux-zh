
# 第 22 章：网络文件系统 (NFS)

```
[root@serverA ~]# service rpcbind start
```

> 在 openSUSE 系统上，上述命令的等效命令是 `rpcbind status` 和 `rpcbind start`。在其他没有 `service` 命令的发行版上，你可以尝试在 `/etc/init.d/` 目录下查找可能名为 `portmap` 的文件。然后你可以手动执行该文件并带有 `status` 或 `start` 选项来控制 `portmap` 服务，例如通过输入

`/etc/init.d/portmap status`

## 4. 接下来，启动 NFS 服务，它将启动所需的所有辅助服务。

```
[root@serverA ~]# service nfs-server start
```

从其输出中，`nfs status` 脚本将告诉你是已启动还是启动失败。或者，你可以在 Fedora 等启用 `systemd` 的 Linux 发行版上通过输入 `systemctl` 命令来启动 nfs 服务器：

```
[root@fedora-server ~]# systemctl start nfs-server.service
```

## 5. 要检查你的导出配置是否正确，请运行 `showmount` 命令：

```
[root@serverA ~]# mount -e localhost
```

## 6. 如果你没有看到放入 `/etc/exports` 的文件系统，请检查 `/var/log/messages` 查看任何 `nfsd` 或 `mountd` 忽略的输出。如果你需要对 `/etc/exports` 进行更改，完成后运行 `nfs reload` 或 `exports -r`，最后运行 `showmount -e` 以确保更改生效。

## 7. 现在你已经配置好了服务器，是时候设置客户端了。首先，检查客户端和服务器之间的 rpc 机制是否正常工作。你将使用 `showmount` 命令来验证客户端是否可以看到共享内容。如果客户端看不到共享内容，你可能存在网络问题或服务器端存在问题。在 `clientA` 上，执行以下命令：

```
[root@clientA]# showmount -e serverA
Export list for serverA:
/usr/local (everyone)
```

> 提示 如果 `showmount` 命令返回类似于 `/clint_create: Port mapper failure - Unable to receive: errno 113 (No route to host)` 或 `/clint_create: Port mapper failure - RPC: Unable to receive` 的错误，你应该确保运行在 NFS 服务器上或 NFS 服务器与客户端之间的防火墙没有阻止通信。

## 8. 一旦你验证了可以从客户端查看共享内容，就可以查看你是否可以成功挂载文件系统了。首先创建本地的 `/mnt/usr/local/` 挂载点，然后使用 `mount` 命令创建：

```
[root@clientA]# mkdir -p /mnt/usr/local
[root@clientA]# mount -o rw,bg,intr,soft serverA:/usr/local /mnt/usr/local
```

## 9. 你可以使用 `mount` 命令查看挂载在 `clientA` 上的 NFS 类型文件系统。你输入此：

```
[root@clientA]# mount -t nfs
```

或者对于 NFSv4 挂载，你运行此命令：

```
[root@clientA]# mount -t nfs4
```

## 10. 如果这些命令执行成功，你可以将 `mount` 命令及其选项添加到 `/etc/fstab` 文件中，这样它们在重新启动时会自动挂载远程文件。

```
serverA:/usr/local /mnt/usr/local nfs rw,bg,intr,soft 0 0
```
