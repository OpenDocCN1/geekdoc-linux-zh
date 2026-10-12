
NFS（网络文件系统）协议允许通过网络连接访问文件系统。它基于客户端-服务器架构，利用集中服务器与其他计算机共享文件。客户端可以将这些共享挂载到自己的文件系统中以便访问，因为它们位于本地存储上。虽然 Samba 和 AFP 是 Windows 和 OS X 上常见的分布式文件系统，但 NFS 现在是事实标准，也是任何 Linux 服务器系统的关键元素。在这个配方中，我们将向你展示如何方便地设置一个用于网络的 NFS 服务器。

### 准备工作

完成此配方，你需要一个运行良好的 CentOS 7 操作系统并具有 root 权限，以及一个你喜欢的控制台文本编辑器。你还需要一个启用了 SSL 加密且在网络中可访问的 Apache 服务器；请参考第 11 章“提供服务”，了解如何安装 HTTP 守护进程，特别是“使用 SSL 设置 HTTPS”配方。此外，具有一些 Apache 配置格式经验是有益的。

## 操作步骤

- 1. 为你的数据创建一个文件夹并创建一个 WebDAV 锁文件：

```
mdir -p /srv/webdav /etc/httpd/var/davlock
```

- 2. 由于 WebDAV 作为 Apache 模块通过 HTTPS 运行，我们需要为标准用户设置正确的权限：

```
chown apache:apache /srv/webdav /etc/httpd/var/davlock
chmod 770 /srv/webdav
```

- 3. 现在，创建并打开以下 WebDAV 配置文件：

```
vi /etc/httpd/conf.d/webdav.conf
```

- 4. 写入以下内容：

```
LockDB "/etc/httpd/var/davlock"
Alias /webdav /srv/webdav
<Location /webdav>
  DAV On
  Options None
  AuthType Basic
  AuthName webdav
  AuthFile /etc/httpd/conf/passwords
  Require valid-user
</Location>
```

- 5. 保存并关闭文件。现在，添加一个新的 WebDAV 用户（根据提示输入用户密码）：

`htpasswd -c /etc/httpd/conf/passwords john`

## 构建网络

- 6. 最后，重启 Apache 服务器：

`systemctl restart httpd`

- 7. 测试是否可以连接到 WebDAV 服务器，可以使用图形界面（如 Linux 文件管理器）从网络中的任何客户端浏览 WebDAV，或者使用命令行挂载驱动。

- 8. 在网络中的任何客户端机器上以 root 身份登录（在 CentOS 上，使用从仓库安装 davfs2 文件系统驱动，必须禁用锁的使用，因为当前版本不支持），输入名为 john 的用户密码，并在提示时确认自签名证书：

`yum install davfs`

`echo "use_locks 0" >> /etc/davfs/davfs2.conf`

`mkdir -t davfs https://<WebDAV IP>/webdav`

- 9. 现在，检查是否可以写入网络存储：

`touch /mnt/webdav/testfile.txt`

- 10. 如果你遇到了连接问题，请检查 WebDAV 服务器上 http 和 https 的防火墙设置，以及你的客户端。

### 工作原理

在这个配方中，我们向你展示了如何方便地设置 WebDAV 服务器进行文件共享。

那么，我们从这次经验中学习了什么？

我们通过创建两个目录开始旅程：一个存放 WebDAV 服务器的所有共享文件，另一个用于为 WebDAV 服务器创建锁数据库。后者是必要的，以便用户在他人修改文档时防止访问冲突。由于 WebDAV 作为原生 Apache 模块 (mod_dav) 在 CentOS 7 中已默认启用，我们只需要创建一个 Apache 主机配置，设置我们所有的 WebDAV 设置。首先，我们必须将 WebDAV 服务器链接到用于跟踪用户锁的文件。接下来，我们使用 `Location` 指令为我们的 WebDAV 共享文件夹定义了一个别名。在该区域内，我们指定该 URL 启用了 WebDAV 和 SSL 加密，并指定了基于用户的密码认证。用户账户密码将存储在用户数据库 `/etc/httpd/conf/passwords`。为了在该数据库中创建有效账户，我们随后使用了命令行 `htpasswd` 工具。最后，我们重启服务以应用更改。

## 创建导出共享

现在我们的 NFS 服务器已经配置完成并运行，是时候为我们的客户端创建一些文件共享了：

- 1. 首先，为我们的共享创建一个文件夹并更改其权限：

`mkdir /srv/nfs-data`

- 2. 创建一个具有特定 GID 的新组并与导出关联，然后更改权限：

`groupadd -g 50000 nfs-share;chown:nfs-share /srv -R;chmod 777 serv -R`

- 3. 打开以下文件：

`vi /etc/exports`

- 4. 现在，输入以下文本，但打字时请务必集中：

`/srv/nfs-data *(ro) 192.168.1.11 (rw) 192.168.1.12 (rw) /home`

`*.example.com (rw)`

- 5. 接下来，我们需要为服务器开放端口以获得正确的 NFS 访问：

`for s in nfs mountd rbind; do firewall-cmd --permanent --add-service $s; done; firewall-cmd --reload`

### 工作原理

在 CentOS 7 上，你可以安装版本 4 的 NFS，它比之前的版本有所增强，例如提供了更灵活的验证选项，并与旧版本的 NFS 版本向后兼容。在这里，我们展示了安装和配置 NFS 服务器以及为我们的客户端创建一些共享导出（exports）有多简单。

那么，我们从这次经历中学习到了什么呢？

我们通过安装 `nfs-utils` 包实现了这一点，因为 CentOS 7 默认没有提供 NFS 服务器功能。接下来，我们使用 `/etc/hosts` 文件配置了服务器的域名，因为我们没有为自己的名称配置 DNS。如果你已经设置了 DNS 服务器，你应该遵循与我们类似的域名命名方案，因为这对 NFS 的工作非常重要，因为所有客户端和服务器都应该在同一个域内。在示例中，我们指定它们是 `example.com` 的子域：`myClient1.example.com,myClient2.example.com,myServer.example.com`。这是一种数据安全的方法，因为 NFS 只在名称匹配时才允许客户端共享服务器（在我们的示例中，服务器和客户端都是 `example.com` 域的一部分）。接下来，我们在 `mapd` 文件中使用了此基础域，该文件控制用户和 GID 到 NFS 的映射。之后，我们在 `firewalld` 实例中启用了 `nfs-mount` 和 `rpcbind` 防火墙服务，这些对于我们客户端和服务器之间的完整支持和通信都是必要的。为了辅助基础配置，我们启动了 `rpcbind` 和 NFS 服务器并启用了它们。

在成功建立 NFS 服务器后，我们向它添加了一些导出，以允许客户端访问服务器上的某些共享文件夹。因此，我们在文件系统中创建了一个特殊目录，存放我们所有的共享文件夹。我们将此共享文件夹 `/srv/nfs-data` 与一个新组 `nfs-share` 关联，并赋予了它读/写权限。出于实际考虑，我们在组级别上控制导出目录的 Linux 文件权限。组名称并不重要，但其组标识符（GID）必须设置成静态值（例如 50000）。对于想要写权限的用户，此 GID 必须在服务器和每个客户端上保持一致，以便在网络上通过用户（UID）或 GID 在服务器和客户端之间进行 NFS 传输。共享映射发生在 `/etc/exports` 文件中，它包含了所有关于你的共享文件夹及其访问安全性的重要信息。该文件中的每一行等同于系统中的一个共享文件夹，以及一个允许访问它们的所有主机的白名单，以及它们括号中的访问选项。如你所示，使用 IP 地址或主机名来定义目标客户端有多种可能性。对于主机名，我们可以使用通配符如 `*` 并在后跟 `?` 以保持文件更紧凑并允许同时处理多个机器，你也可以为每个主机名定义导出选项。解释所有选项超出了本书的范围；如果你需要更多信息，请查阅 exports 手册，可以通过 `man exports` 找到。
