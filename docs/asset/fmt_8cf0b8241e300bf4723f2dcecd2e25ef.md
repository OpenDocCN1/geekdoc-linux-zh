
`/etc/rc.d/init.d/named start/stop/status/restart`

Debian 使用以下脚本：

`/etc/init.d/bind start/stop/restart/reload/force-reload`

BIND 还提供了一个名为 `ndc` 的工具来管理 `named` 守护进程。表 16-38 显示了 `ndc` 的选项。语法如下：

`ndc [-c channel] [-1 localsock] [-p pidfile] [-d] [-q] [-s] [-t] [command]`

### 表 16-38

#### `ndc` 选项

| 选项 | 功能 |
|---|---|
| `-c` | 指定用于与 DNS 服务器守护进程通信的通道。默认值是 `/var/run/ndc`。可以使用 `ipaddr/port` 指定地址和端口，例如 `127.0.0.1:54` |
| `-1 <localsock>` | 将源 `ndc` 连接绑定到特定接口 |
| `-p <pidfile>` | 指向 `pidfile` 文件的路径，用于旧版本的 BIND |
| `-d` | 启用调试输出 |
| `-q` | 静默模式 |
| `-s` | 不显示非致命错误 |
| `-t` | 启用协议和系统跟踪 |

### 关键点总结

大多数人运行 Linux 的原因是为他们的用户提供网络服务。本章涵盖了今天使用的主要网络服务。本章提供的信息对于考试来说绰绰有余，并且足以立即让服务启动并为你运行。

- 可以使用 `inetsd` 来启动许多不需要持续运行的服务。
- `inetsd` 通过 `/etc/inetsd.conf` 进行配置。
- `ineta.conf` 中的每一行都指定要运行的服务、以哪个用户身份运行、使用的协议以及其他选项。
- `ineta` 由 Red Hat 的 `/etc/rc.d/init.d/inet` 脚本和 Debian 的 `/etc/init.d/inetd` 脚本管理。
- `ftpaccess` 文件用于设置 FTP 服务器的限制、日志选项、信息设置以及其他选项。
- `ftphosts` 文件基于用户名和主机名来允许或拒绝访问 FTP 服务器。
- `ftpconversions` 文件告知 FTP 服务器如何处理压缩和归档操作。
- `/var/log/xferlog` 文件记录 FTP 服务器的传输。
- `ftpshtut` 命令优雅地关闭 FTP 服务器并警告用户。
- `ftpwho` 命令显示当前连接到 FTP 服务器的用户。
- `ftpcout` 工具显示连接到 FTP 服务器的用户数量，并按类别细分。
- `/etc/issue.net` 文件在 Telnet 用户登录系统之前向他们显示。
- MTA（消息传输代理）用于使用 SMTP 在服务器之间传输消息。
- MUA（邮件用户代理）是用户与邮件系统交互的应用程序。
- MDA（邮件投递代理）用于将消息从服务器投递到用户的信箱。
- `sendmail.cf` 是主要的 sendmail 配置文件，并且非常复杂。
- `sendmail.cw` 文件列出了该服务器接受邮件的主机。
- `/etc/aliases` 文件列出了邮件别名。
- 当创建新的邮件别名时，应该运行 `newaliases` 命令。
- 如果你想将所有邮件转发到另一个服务器进行投递，可能需要更改 `sendmail.cf` 中的 Smart Host 条目。
- m4 预处理器用于从宏文件创建新的 `sendmail.cf` 文件。
- 用户可以创建 `.forward` 文件以将邮件转发到另一个地址或文件。
- sendmail 由 Red Hat 的 `/etc/rc.d/init.d/sendmail` 脚本和 Debian 的 `/etc/init.d/sendmail` 脚本管理。
- 使用 `mailq` 工具列出邮件队列中的消息。
- Apache 可以配置为独立运行或从 `inetd` 运行。

#### 复习要点

- `srm.conf` 文件可用于控制 Apache 的文件类型和文档规范。
- `access.conf` 文件可用于控制 Apache 的访问配置。
- `httpd.conf` 是主要的 Apache 配置文件，已取代前两个文件。
- Apache 使用配置文件中的指令命令进行配置。
- `.htaccess` 文件可用于覆盖主 Apache 配置文件中的设置。
- `htpasswd` 工具用于创建 Apache 的用户和组密码文件。
- 虚拟主机可以使用单个 IP 地址或多个 IP 地址。
- 要使用基于名称的虚拟主机，客户端的 Web 浏览器需要支持 HTTP/1.1。
- NFS 用于向其他网络用户共享目录。
- NFS 导出通过 `/etc/exports` 文件进行配置。
- `exportsfs` 工具用于更新导出的目录并手动添加新目录。
- 远程 NFS 目录使用命令 `mount host:/directory /mount_point` 挂载。
- NFS 服务器使用 Red Hat 脚本 `/etc/rc.d/init.d/nfs` 和 Debian 脚本 `/etc/init.d/nfs-kernel-server` 进行管理。
- `nfsstat` 工具用于显示 NFS 服务器的统计信息。
- Samba 用于与 Windows 客户端共享文件和打印机。
- Samba 通过 `smb.conf` 文件进行配置。
- Samba 使用 Red Hat 脚本 `/etc/rc.d/init.d/smb` 和 Debian 脚本 `/etc/init.d/samba` 进行管理。
- `testparm` 工具用于检查 `smb.conf` 的语法错误。
- `smbstatus` 工具用于显示当前连接到 Samba 服务器的用户。
- `smbclient` 工具用于连接 Samba 服务器或 Windows 共享。
- DNS 用于将名称映射到 IP 地址，反之亦然。
- 根名称服务器负责将查询服务器引导至 TLD 服务器。
- DNS 命名空间是一种分层树结构，根名称服务器位于“顶部”，独立管理的域位于“底部”。
- BIND 是提供 DNS 实现的软件套件。
- BIND v8 使用 `named.conf` 文件进行服务器配置。
- 区域文件包含 DNS 资源记录，其中持有映射信息。
- 如果 BIND 服务器拥有该域或子域的主区域信息副本，则为主服务器。
- 如果 BIND 服务器从主服务器获取区域信息，则为从服务器。
- BIND 前向服务器将所有查询转发给其他 DNS 服务器。
- BIND 桩服务器仅从主服务器获取 NS 记录。
- 当区域信息被复制到另一台服务器时，这被称为区域传输。
- 仅缓存的名称服务器对某个域没有权威，它只查询其他服务器的信息并将这些信息缓存起来以备后续使用，从而提高性能。
- BIND v4 使用 `named.boot` 配置文件。
- `/etc/hosts` 文件存储静态映射信息。
- `/etc/nsswitch.conf` 文件控制系统如何解析名称。
- `/etc/resolv.conf` 文件列出搜索域和要查询的 DNS 服务器。
- `nslookup` 工具提供交互和非交互界面以执行 DNS 查询。
- `dig` 工具具有与 `nslookup` 类似的功能，但可以提供更多信息。
- `host` 是一个小巧的工具，可以执行查询，但通常提供的信息少于 `dig`。
- `ndc` 工具用于管理 BIND `named` 守护进程。
- BIND 守护进程使用 Red Hat 脚本 `/etc/rc.d/init.d/named` 和 Debian 脚本 `/etc/init.d/bind` 进行管理。

#### 学习指南

以下问题和练习将帮助你回顾本章涵盖的信息。请花时间仔细完成本章的这一部分，仔细审查你可能有疑问的题目。正确回答问题不如理解答案重要，因此请复习你可能仍不确定的材料。熟悉此处提出的问题及答案将有助于你更好地为认证考试题目做准备。

##### 评估问题

1. 当服务使用 TCP 时，`inetd.conf` 中使用哪种套接字类型？
   - A. `dgram`
   - B. `stream`
   - C. `raw`
   - D. `rdm`

2. `inetd` 每 30 秒读取一次 `inetd.conf` 文件以查找配置更改。
   - A. 正确
   - B. 错误

3. 用于匿名 FTP 的账户应该使用哪个 shell？
   - A. `/bin/bash`
   - B. `/bin/csh`
   - C. `/bin/false`
   - D. `/bin/ksh`

4. `ftpaccess` 中的哪个条目限制失败的密码尝试次数？
   - A. `loginfails`
   - B. `loginlimit`
