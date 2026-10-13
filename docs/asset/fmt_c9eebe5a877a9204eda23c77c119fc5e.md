
仅将导出限制在需要访问的客户端。在 NFS 服务器上使用 `showmount -e` 命令审查服务器正在导出的内容。不要导出任何并非明确必需的内容。

不要使用 `no_root_squash` 选项，并审查现有安装以确保未使用该选项。更多信息请参阅第 4.3.7.4 节“不要使用 no_root_squash 选项”。

`secure` 选项是用于将导出限制在“保留”端口的服务器端导出选项。默认情况下，服务器仅允许来自“保留”端口（编号小于 1024 的端口）的客户端通信，因为传统上客户端仅允许“受信任”的代码（如内核中的 NFS 客户端）使用这些端口。然而，在许多网络中，任何人都不难在某个客户端上成为 root，因此服务器很少能安全地假设来自保留端口的通信具有特权。因此，对保留端口的限制价值有限；最好依赖 Kerberos、防火墙以及将导出限制到特定客户端。

大多数客户端在可能的情况下仍会使用保留端口。然而，保留端口是一种有限资源，因此客户端（尤其是拥有大量 NFS 挂载的客户端）可能会选择使用编号较高的端口。Linux 客户端可以使用“noregport”挂载选项来做到这一点。如果您希望允许在导出中使用此行为，可以使用“insecure”导出选项。

良好的做法是不允许用户登录到服务器。在审查上述 NFS 服务器设置时，应审查谁以及什么可以访问该服务器。

### 4.3.7.2.2. 审查 NFS 客户端

使用 `nosuid` 选项禁止使用 setuid 程序。`nosuid` 选项禁用 set-user-identifier 或 set-group-identifier 位。这可以防止远程用户通过运行 setuid 程序来获取更高权限。在客户端和服务器端都应使用此选项。

`noexec` 选项禁用客户端上的所有可执行文件。使用此选项可防止用户无意中执行放置在正在共享的文件系统中的文件。`nosuid` 和 `noexec` 选项是大多数（如果并非全部）文件系统的标准选项。

使用 `nodev` 选项防止客户端将“设备文件”作为硬件设备进行处理。

`resvport` 选项是客户端挂载选项，`secure` 是相应的服务器端导出选项（参见上述说明）。它将通信限制在“保留端口”。保留或“知名”端口是为特权用户和进程（如 root 用户）预留的。设置此选项会导致客户端使用保留源端口与服务器通信。

所有版本的 NFS 现在都支持使用 Kerberos 认证进行挂载。启用此功能的挂载选项为：`sec=krb5`。

NFSv4 支持使用 Kerberos 进行挂载，其中 `krb5i` 用于完整性，`krb5p` 用于隐私保护。这些在挂载时使用 `sec=krb5`，但需要在 NFS 服务器上配置。更多信息请参阅 exports 手册页（`man 5 exports`）。

NFS 手册页（`man 5 nfs`）有一个“SECURITY CONSIDERATIONS”（安全注意事项）章节，解释了 NFSv4 中的安全增强功能，并包含所有 NFS 特定的挂载选项。

#### 4.3.7.3. 警惕语法错误

NFS 服务器通过查阅 `/etc/exports` 文件来确定要导出哪些文件系统以及将这些目录导出到哪些主机。编辑此文件时，务必小心，不要添加多余的空格。

例如，`/etc/exports` 文件中的以下行将目录 `/tmp/nfs/` 以读/写权限共享到主机 `bob.example.com`。

```
/tmp/nfs/		bob.example.com(rw)
```

另一方面，`/etc/exports` 文件中的以下行将同一目录以只读权限共享到主机 `bob.example.com`，并由于主机名后的一个空格字符，将其以读/写权限共享给全世界。

```
/tmp/nfs/		bob.example.com (rw)
```

使用 `showmount` 命令检查任何已配置的 NFS 共享，以验证正在共享的内容，这是一种良好的做法：

```
showmount -e <hostname>
```

#### 4.3.7.4. 不要使用 no_root_squash 选项

默认情况下，NFS 共享会将 root 用户转换为 `nfsnobody` 用户，这是一个无特权用户帐户。这会将所有由 root 创建的所有者的文件所有者更改为 `nfsnobody`，从而防止上传设置了 setuid 位的程序。

如果使用 `no_root_squash`，远程 root 用户将能够修改共享文件系统上的任何文件，并留下被特洛伊木马感染的应用程序供其他用户无意中执行。

#### 4.3.7.5. NFS 防火墙配置

NFSv4 是 Red Hat Enterprise Linux 7 的默认 NFS 版本，它仅需要打开 TCP 端口 2049。如果使用 NFSv3，则需要下面解释的另外四个端口。

### 为 NFSv3 配置端口

NFS 使用的端口由 `rpcbind` 服务动态分配，这在创建防火墙规则时可能会引起问题。为了简化此过程，请使用 `/etc/sysconfig/nfs` 文件指定要使用的端口：

- `MOUNTD_PORT` – `mountd` (`rpc.mountd`) 的 TCP 和 UDP 端口

- `STATD_PORT` – `status` (`rpc.statd`) 的 TCP 和 UDP 端口

在 Red Hat Enterprise Linux 7 中，请在 `/etc/modprobe.d/lockd.conf` 文件中设置 NFS 锁管理器 (`nlockmgr`) 的 TCP 和 UDP 端口：

- `nlm_tcpport` – `nlockmgr` (`rpc.lockd`) 的 TCP 端口

- `nlm_udpport` – `nlockmgr` (`rpc.lockd`) 的 UDP 端口

指定的端口号不得被任何其他服务使用。请配置防火墙以允许指定的端口号，以及 TCP 和 UDP 端口 2049 (`NFS`)。有关其他可自定义的 NFS 锁管理器参数的说明，请参阅 `/etc/modprobe.d/lockd.conf`。

在 NFS 服务器上运行 `rpcinfo -p` 命令，以查看正在使用的端口和 RPC 程序。

#### 4.3.7.6. 使用 Red Hat Identity Management 保护 NFS

在使用 Red Hat Identity Management 的环境中，支持 Kerberos 的 NFS 设置可以大大简化。Red Hat Identity Management 包含在 Red Hat Enterprise Linux 中。

请参阅 [Red Hat Enterprise Linux 7 Linux 域身份、身份验证和策略指南](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/linux_domain_identity_authentication_and_policy_guide/index)，特别是 [设置支持 Kerberos 的 NFS 服务器](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/linux_domain_identity_authentication_and_policy_guide/setting-up-a-kerberos-aware-nfs-server)，以了解在使用 Red Hat Identity Management 时如何使用 Kerberos 保护 NFS。

### 4.3.8. 保护 HTTP 服务器

#### 4.3.8.1. 保护 Apache HTTP 服务器

Apache HTTP 服务器是 Red Hat Enterprise Linux 7 中最稳定和安全的服务之一。有大量可用的选项和技术来保护 Apache HTTP 服务器——数量之多，无法在此深入探讨。以下部分简要介绍了运行 Apache HTTP 服务器时的良好实践。

在将任何脚本投入生产之前，始终验证运行在系统上的脚本是否按预期工作。此外，确保只有 root 用户对包含脚本或 CGI 的任何目录具有写入权限。为此，请以下 root 用户身份输入以下命令：

```
chown root <directory_name>
```

#### 4.3.8.1. 保护 Apache HTTP 服务器

系统管理员在使用以下配置选项（配置于 `/etc/httpd/conf/httpd.conf`）时应保持谨慎：

### FollowSymlinks

此指令默认是启用的，因此在为 Web 服务器文档根目录创建符号链接时务必谨慎。例如，提供指向 `/.` 的符号链接是一个坏主意。

```bash
chmod 755 <directory_name>
```

### Indexes

此指令默认是启用的，但这可能不是理想的设置。要防止访问者浏览服务器上的文件，请移除此指令。

### UserDir
