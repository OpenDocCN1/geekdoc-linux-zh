

## 复习要点

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

## 学习指南

以下问题和练习将帮助你回顾本章涵盖的信息。请花时间仔细完成本章的这一部分，仔细审查你可能有疑问的题目。正确回答问题不如理解答案重要，因此请复习你可能仍不确定的材料。熟悉此处提出的问题及答案将有助于你更好地为认证考试题目做准备。

### 评估问题

1. 当服务使用 TCP 时，`inetd.conf` 中使用哪种套接字类型？
   - A. dgram
   - B. stream
   - C. raw
   - D. rdm

2. `inetd` 每 30 秒读取一次 `inetd.conf` 文件以查找配置更改。
   - A. 正确
   - B. 错误

3. 用于匿名 FTP 的账户应该使用哪个 shell？
   - A. `/bin/bash`
   - B. `/bin/csh`
   - C. `/bin/false`
   - D. `/bin/ksh`

4. `ftpaccess` 中的哪个条目限制失败的密码尝试次数？
   - A. loginfails
   - B. loginlimit
   - C. badpw
   - D. pwattempts

5. 哪个工具用于查看谁登录到你的 FTP 服务器？
   - A. `ftpstats`
   - B. `whoftp`
   - C. `ftpd -w`
   - D. `ftpwho`

6. 为用户创建新的邮件别名需要做什么？（选择所有适用项。）
   - A. 将别名添加到 `/etc/aliases`。
   - B. 将别名添加到 `/etc/mailboxes`。
   - C. 运行 `newaliases` 命令。
   - D. 运行 `addalias` 命令。

7. ______ 命令用于列出当前邮件队列中的消息。

8. 为了使 Web 服务器表现最佳，应通过 `inetd` 运行它。
   - A. 正确
   - B. 错误

9. 要通过 `inetd` 运行 `httpd` 需要做什么？（选择所有适用项。）
   - A. 更改 `httpd.conf` 中指定的端口号。
   - B. 更改 `httpd.conf` 中的 `ServerType` 指令。
   - C. 在 `inetd.conf` 中为 `httpd` 添加条目。
   - D. 运行 `inetd -d /usr/sbin/httpd`。

10. 默认情况下，Apache 使用 `/etc/passwd` 文件进行用户身份验证。
    - A. 正确
    - B. 错误

11. `/etc/exports` 中的哪个条目或条目的组合将仅向 192.168.10.0/24 网络（由域 `mydomain.org` 组成）上的用户共享 `/home` 目录？
    - A. `/home 192.168.10.0 - 254(rw)`
    - B. `/home 192.168.10.0/24(ro)`
    - C. `/home *.mydomain.org(rw)`
    - D. `/home ANY.mydomain.org(rw)`

12. 编辑 `/etc/exports` 文件后，应运行 ______ 命令（无参数）。

13. `smb.conf` 中的哪个条目设置 Samba 的 Windows NT 域？
    - A. workgroup
    - B. domain
    - C. nt_domain
    - D. MS_DOMAIN

14. 哪个命令显示使用 `smbclient` 的 Windows 共享上的所有文件？
    - A. dir
    - B. list
    - C. cp
    - D. ls

15. BIND v4 使用 ______ 配置文件。
    - A. named.boot
    - B. named.conf
    - C. named.cf
    - D. conf.named

16. 哪个 DNS 资源记录用于将 IP 地址反向映射到名称？
    - A. A
    - B. MX
    - C. SRV
    - D. PTR

17. 哪个 DNS 资源记录显示提供服务的宿主机？
    - A. SRV
    - B. LOC
    - C. A
    - D. CNAME

18. 在 `nsswitch.conf` 文件中 hosts 条目前应该放置哪个字段，以使系统首先检查 `/etc/hosts`？
    - A. files
    - B. NIS
    - C. dns
    - D. yp

19. 哪个邮件服务器具有最高优先级？
    - A. IN MX 10 mail
    - B. IN MX 20 mail
    - C. IN MX 100 mail
    - D. IN MX 0 mail

20. 哪个文件显示给通过 Telnet 登录系统的用户之前？
    - A. /etc/issue
    - B. /etc/login.net
    - C. /etc/motd.net
    - D. /etc/issue.net

### 场景

1. 你是一家中型公司的网络管理员。为了帮助维护网络中的 Linux 工作站，你想共享一个常见的文件基础。实现这一目标的最佳方法是什么？
2. 在进行常规网络监控时，你注意到 WAN 上的大量流量来自 DNS 查询。你可以做些什么来帮助减少流量并提高用户性能？
3. 你的公司有多位经常出差的销售人员。他们需要在外出旅行时从远程位置访问多个文档和文件。你可以如何设置服务让他们获取这些文件？

### 实验室练习

#### 实验 16-1 本地 DNS 服务器
除非你注册了自己的域名，否则你只能设置本地 DNS 服务器。此服务器托管的区域无法从外部访问。

[/content]
</think>

[content]
## 复习要点

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

## 学习指南

以下问题和练习将帮助你回顾本章涵盖的信息。请花时间仔细完成本章的这一部分，仔细审查你可能有疑问的题目。正确回答问题不如理解答案重要，因此请复习你可能仍不确定的材料。熟悉此处提出的问题及答案将有助于你更好地为认证考试题目做准备。

### 评估问题

1. 当服务使用 TCP 时，`inetd.conf` 中使用哪种套接字类型？
   - A. dgram
   - B. stream
   - C. raw
   - D. rdm

2. `inetd` 每 30 秒读取一次 `inetd.conf` 文件以查找配置更改。
   - A. 正确
   - B. 错误

3. 用于匿名 FTP 的账户应该使用哪个 shell？
   - A. `/bin/bash`
   - B. `/bin/csh`
   - C. `/bin/false`
   - D. `/bin/ksh`

4. `ftpaccess` 中的哪个条目限制失败的密码尝试次数？
   - A. loginfails
   - B. loginlimit
   - C. badpw
   - D. pwattempts

5. 哪个工具用于查看谁登录到你的 FTP 服务器？
   - A. `ftpstats`
   - B. `whoftp`
   - C. `ftpd -w`
   - D. `ftpwho`

6. 为用户创建新的邮件别名需要做什么？（选择所有适用项。）
   - A. 将别名添加到 `/etc/aliases`。
   - B. 将别名添加到 `/etc/mailboxes`。
   - C. 运行 `newaliases` 命令。
   - D. 运行 `addalias` 命令。

7. ______ 命令用于列出当前邮件队列中的消息。

8. 为了使 Web 服务器表现最佳，应通过 `inetd` 运行它。
   - A. 正确
   - B. 错误

9. 要通过 `inetd` 运行 `httpd` 需要做什么？（选择所有适用项。）
   - A. 更改 `httpd.conf` 中指定的端口号。
   - B. 更改 `httpd.conf` 中的 `ServerType` 指令。
   - C. 在 `inetd.conf` 中为 `httpd` 添加条目。
   - D. 运行 `inetd -d /usr/sbin/httpd`。

10. 默认情况下，Apache 使用 `/etc/passwd` 文件进行用户身份验证。
    - A. 正确
    - B. 错误

11. `/etc/exports` 中的哪个条目或条目的组合将仅向 192.168.10.0/24 网络（由域 `mydomain.org` 组成）上的用户共享 `/home` 目录？
    - A. `/home 192.168.10.0 - 254(rw)`
    - B. `/home 192.168.10.0/24(ro)`
    - C. `/home *.mydomain.org(rw)`
    - D. `/home ANY.mydomain.org(rw)`

12. 编辑 `/etc/exports` 文件后，应运行 ______ 命令（无参数）。

13. `smb.conf` 中的哪个条目设置 Samba 的 Windows NT 域？
    - A. workgroup
    - B. domain
    - C. nt_domain
    - D. MS_DOMAIN

14. 哪个命令显示使用 `smbclient` 的 Windows 共享上的所有文件？
    - A. dir
    - B. list
    - C. cp
    - D. ls

15. BIND v4 使用 ______ 配置文件。
    - A. named.boot
    - B. named.conf
    - C. named.cf
    - D. conf.named

16. 哪个 DNS 资源记录用于将 IP 地址反向映射到名称？
    - A. A
    - B. MX
    - C. SRV
    - D. PTR

17. 哪个 DNS 资源记录显示提供服务的宿主机？
    - A. SRV
    - B. LOC
    - C. A
    - D. CNAME

18. 在 `nsswitch.conf` 文件中 hosts 条目前应该放置哪个字段，以使系统首先检查 `/etc/hosts`？
    - A. files
    - B. NIS
    - C. dns
    - D. yp

19. 哪个邮件服务器具有最高优先级？
    - A. IN MX 10 mail
    - B. IN MX 20 mail
    - C. IN MX 100 mail
    - D. IN MX 0 mail

20. 哪个文件显示给通过 Telnet 登录系统的用户之前？
    - A. /etc/issue
    - B. /etc/login.net
    - C. /etc/motd.net
    - D. /etc/issue.net

### 场景

1. 你是一家中型公司的网络管理员。为了帮助维护网络中的 Linux 工作站，你想共享一个常见的文件基础。实现这一目标的最佳方法是什么？
2. 在进行常规网络监控时，你注意到 WAN 上的大量流量来自 DNS 查询。你可以做些什么来帮助减少流量并提高用户性能？
3. 你的公司有多位经常出差的销售人员。他们需要在外出旅行时从远程位置访问多个文档和文件。你可以如何设置服务让他们获取这些文件？

### 实验室练习

#### 实验 16-1 本地 DNS 服务器
除非你注册了自己的域名，否则你只能设置本地 DNS 服务器。此服务器托管的区域无法从外部访问。
