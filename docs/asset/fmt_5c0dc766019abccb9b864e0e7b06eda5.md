
# 第 22 章：网络文件系统 (NFS) 511

![](img/0878ea6dc96f881186251d3dfe31ad33_537_0.png)

**图 22-1.** NFS 服务器配置工具

在许多情况下，你只需要使用 `exportfs -r`。

## showmount 命令

在配置 NFS 时，使用 `showmount` 命令来检查一切是否运行正常非常有帮助。该命令用于显示 NFS 服务器的挂载信息。

通过使用 `showmount` 命令，你可以快速判断你是否已经正确配置了 `nfs`。

在你配置了 `/etc/exports` 文件并使用 `exportfs` 导出了所有文件系统后，可以运行 `showmount -e` 来查看本地 NFS 服务器上导出的文件系统列表。`-e` 选项告诉 `showmount` 显示 NFS 服务器的导出列表。例如：

```
[root@serverA ~]# showmount -e localhost

Export list for localhost:

/home *
```

## Linux 系统管理：入门指南

如果你直接运行不带选项的 `showmount` 命令，它将列出连接到服务器的客户端。例如，

```
[root@serverA ~#] showmount localhost

Hosts on localhost:

192.168.1.100
```

你也可以通过将服务器主机名作为最后一个参数在客户端上运行此命令。要从 NFS 客户端 `clientA` 显示 NFS 服务器 `serverA` 上导出的文件系统，你可以在登录到 `clientA` 时使用此命令：

```
[root@clientA ~#] showmount -e serverA

Export list for serverA:

/home *
```

## 排除服务器端 NFS 问题

在导出文件系统时，你可能会发现服务器似乎拒绝客户端的访问，即使客户端已列在 `/etc/exports` 文件中。通常情况下，这是因为服务器获取了连接到它的客户端 IP 地址，并将该地址解析为完全限定域名 `FQDN`，而 `/etc/hosts` 文件中的主机名是不完全的。例如，服务器认为主机名是 `clientA.example.com`，但 `/etc/exports` 文件中列出的仅是 `clientA`。

另一个常见问题是服务器对主机名/IP 映射的识别不正确。这可能是由于 `/etc/hosts` 文件或域名解析系统 `DNS` 表中的错误导致的。你需要验证该映射是否正确。

对于 `NFSv2` 和 `NFSv3`，如果其他所需的服务（如 `portmap` 服务）尚未运行，则 NFS 服务可能无法正确启动。

即使客户端端和服务器端似乎都已配置正确，你可能会发现服务器端的防火墙阻止了挂载过程的完成。在这种情况下，你会注意到 `mount` 命令似乎悬挂起，且没有任何明显的错误。

## 配置 NFS 客户端

在 Linux 下，NFS 客户端的配置非常简单，因为它们不需要加载任何新的或额外的软件。唯一的要求是编译内核以支持 NFS 文件系统。几乎所有的 Linux 发行版都默认启用了此功能。除了内核支持外，另一个重要因素是配合 `mount` 命令使用的选项。

## mount 命令

`mount` 命令在第 7 章中讨论过。使用 `mount` 命令时重要的参数是 NFS 服务器名称的指定、本地挂载点以及在 `mount` 命令行 `-o` 之后指定的选项。

以下是 `mount` 命令的示例：

```bash
root@clientA ~]# mount -o rw,bg,soft serverA:/home /mnt/home
```

在这里，`serverA` 是 NFS 服务器名称。`-o` 选项在表 22-2 中解释。

这些挂载选项也可以用于 `/etc/fstab` 文件。`/etc/fstab` 文件中的相同条目看起来如下：

```
serverA:/home /mnt/home rw,bg,soft 0 0
```
