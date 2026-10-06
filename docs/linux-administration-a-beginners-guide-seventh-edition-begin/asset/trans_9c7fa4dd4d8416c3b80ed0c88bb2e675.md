

# 第 23 章 网络文件系统 (NFS) 611

以下是 /etc/exports 文件中每个条目/行的格式：

```
/directory/to/export client|ip_network(permissions) client|ip_network(permissions)
```

此处对不同字段进行了了说明：

- directory/to/export 这是您想要与其他用户共享的目录——例如 .home。

- client 指的是 NFS 客户端的主机名（们）。

- ip_network 允许通过 IP 地址（例如 172.16.1.1）或带有子网掩码组合的网络地址（例如 172.16.0/16）来匹配主机。此字段还支持如 `*` 和 `?` 等通配符。

- permissions 这些是对应每个客户端的权限。表 23-1 描述了每个客户端的有效权限。

| 权限选项 | 含义 |
| --- | --- |
| secure | 客户端请求挂载的端口号必须小于 1024。此权限默认开启。若要关闭它，请指定 insecure 代替。 |
| ro | 允许对分区进行只读访问。当显式指定任何内容时，这是默认权限。 |
| rw | 允许标准的读/写访问。 |
| noaccess | 客户端将被访问 /dir/to/mount 下的所有目录。这允许您将目录 /dir 导出给客户端，然后指定 /dir/to 为不可访问，而不会剥夺对 /dir/from 等内容的访问。 |
| root_squash | 此权限防止 root 用户在远程 NFS 挂载卷上使用超级用户 (root) 权限。squash 字面意思是“压缩” root 用户的权力。 |
| no_root_squash | 允许客户端主机上的 root 用户以超级用户通常拥有的权利和权限访问 NFS 挂载目录。 |
| all_squash | 将所有用户 ID (UID) 和组 ID (GID) 映射到匿名用户。相反的选项是 no_all_squash，它是默认设置。 |

表 23-1 NFS 权限

```
[root@server ~]# exports -a
```

# 第 23 章 网络文件系统 (NFS) 613

要向 clientA 导出 /usr/local 目录并赋予读/写和 no_root_squash 权限，输入：

```
[root@server ~]# exports -o rw,no_root_squash clientA:/usr/local
```

在大多数情况下，您将只想使用带有 -r 选项的 exports（意味着重新导出所有目录并完成其他后台管理任务）。

# showmount 命令

在配置 NFS 时，你会发现使用 showmount 命令来检查一切是否运行正常非常有帮助。该命令用于显示 NFS 服务器的挂载信息。

通过使用 showmount 命令，您可以快速判断出自己是否已正确配置了 nfsd。

在配置了 /etc/exports 并使用 exports -e 导出了所有文件系统后，使用 `showmount` 来查看本地 NFS 服务器上导出的文件系统列表。-e 选项告诉 showmount 显示 NFS 服务器的导出列表。这里是一个示例：

```
[root@server ~]# showmount -e localhost
localhost 的导出列表:
home *
```

如果您在不带任何选项的情况下运行 showmount 命令，它将列出连接到服务器的客户端：

```
[root@server ~]# showmount localhost
localhost 上的主机:
* 192.168.1.100
```

您也可以通过将服务器主机名作为最后一个参数在客户端上运行此命令。要从客户端 (clientA) 导出远程 NFSv3 服务器 (serverA) 的文件系统，您可以在登录 clientA 时使用此命令：

```
[root@clientA ~]# showmount -e serverA
serverA 的导出列表:
home *
```

# 服务器侧 NFS 问题

在导出文件系统时，可能会发现服务器似乎拒绝访问，尽管在 /etc/exports 中已配置。通常，这是由于挂载点的完全限定域名 (FQDN) 导致服务器认为是 clientA。

# 614 Linux 管理：初学者指南

另一个常见问题是 /etc/hosts 文件中的主机名匹配。对于 NFS2 和 NFS3，如果服务器服务没有启动，挂载可能会失败。

即使服务器端已经设置好，由于防火墙的原因，挂载命令可能会挂起。在某些情况下，您可以使用 `firewall-cmd` 命令来永久性地打开 NFS 服务端口，例如：

```
root@fedora-server ~]# firewall-cmd --add-service=nfs --permanent
root@fedora-server ~]# firewall-cmd --reload
```

# 配置 NFS 客户端

NFS 客户端配置非常简单，因为它们不需要额外的软件。

# mount 命令

mount 命令在第 7 章讨论过。使用 mount 命令的重要参数是服务器名称或 IP 地址、本地挂载点以及 -o 指定的选项。

```
root@clientA ~]# mount -o rw,bg,soft serverA:/home
```

这些挂载选项也可以用于 /etc/fstab。fstab 中的条目如下：

```
serverA:/home /mnt/home nfs rw,bg,soft 0 0
```

# 第 23 章 网络文件系统 (NFS) 615

| 命令选项 | 描述 |
| --- | --- |
| bg | 后台挂载。如果初始挂载失败（例如服务器宕机），挂载进程将进入后台继续尝试直到成功。这对于启动时挂载的文件系统很有用。 |
| intr | 可中断挂载。如果挂分区上有待处理的 I/O，此选项允许进程被中断并丢弃 I/O 调用。更多信息请参阅本章后面的“intr 选项的重要性”。 |
| hard | 隐默认选项。如果 NFS 文件操作发生严重超时，控制台将报告“服务器未响应”，且客户端将无限重试。 |
| soft | 为此分区启用软挂载，允许客户端在重试次数（通过 retrans=r 选项指定）后超时连接。更多信息请参阅本章后面的“软挂载与硬挂载”。 |
| retrans=n | 该值指定软挂载系统的最大连接重试次数。 |
| rsize=n | 该值为从 NFS 服务器读取文件时使用的字节数。默认值取决于内核，但在 NFSv4 中为 4096 字节。通过请求更大的值可以大幅提高吞吐量（例如 rsize=32768）。 |
| wsize=n | 该值是向 NFS 服务器写入文件时使用的字节数。默认值取决于内核，但在 NFSv4 中为 4096 字节。通过请求更大的值可以大幅提高吞吐量（例如 wsize=32768）。该值将与服务器进行协商。 |

