
`-a`选项是归档模式，包含了许多其他选项，如`-r`（递归）包含所有子目录、`-t`保留文件日期、`-l`创建符号链接以及`-p`保留权限。此外，`--delete`选项用于删除发送端不存在的文件。

## 安全 FTP 服务器

安全 FTP 服务器 (`vsftpd`) 小巧、快速、易用且安全。它的设计旨在避免像 ProFTPD 这样大型应用程序的开销，同时保持极高的安全性。安全 FTP 服务器本质上旨在提供最大的安全性，充分利用 Unix 和 Linux 操作系统的特性。服务器被分为特权和非特权进程。非特权进程接收所有 FTP 请求，解释它们并通过 socket 发送到特权进程，由后者对请求进行安全过滤。特权进程不以 root 权限运行，仅使用执行任务必需的权限。此外，安全 FTP 服务器使用自己的目录命令（如 `ls`），而不是系统的版本。

## 运行 vsftpd

安全 FTP 服务器的守护进程名为 `vsftpd`。它被设计为独立服务器运行，可以通过 `/etc/rc.init.d/vsftpd` 脚本启动和停止。要启动、停止和重启 vsftpd，可以使用 `service` 命令。

```bash
service vsftpd start
```

要让服务器自动启动，你可以使用 `chkconfig` 命令开启，并使用 `off` 参数禁用服务器。如果你启用了其他 FTP 服务器（如 ProFTPD），请先禁用它。

```bash
chkconfig vsftpd on
```

你也可以使用 `system-config-services` 来启动和停止 vsftpd，或让其自动启动。或者，你可以实现 vsftpd 由 `inetd` 运行，仅在用户提出请求时启动服务器。`xinetd` 用于服务器的情况在第 3 章中有详细描述。

# 第 4 部分：网络服务

最初，服务器处于关闭状态。你可以使用 `chkconfig` 命令并配合 `on` 参数来开启 xinetd，如下所示。使用 `off` 参数禁用服务器。

`chkconfig vsftpd on`

使用服务命令（或 `system-config-services`）重启 xinetd 以重启 ftpd 服务，当你对配置更改时应当执行此操作。

```
service xinetd restart
```

# 防火墙访问

要允许防火墙访问 FTP 端口（通常为端口 21），你应该使用防火墙配置工具 `system-config-firewall` 访问。

如果你直接管理 IPTables 防火墙，可以通过添加以下 IPTables 规则直接管理访问。这将允许来自端口 21 的 TCP/IP 协议数据包。

`iptables -A INPUT -p tcp -j ACCEPT`

# 使用 system-config-vsftpd 管理 vsftpd

Fedora 提供了一个名为 `system-config-vsftpd` 的系统管理工具包，通过它可以轻松地配置 vsftpd 服务器。首先安装 `system-config-vsftpd` 软件包。然后通过选择 Selection | Administration | Server Settings | FTP Administration 来启动 `system-config-vsftpd`。配置设置保存到 `/etc/vsftpd/vsftpd.conf` 文件中。

`system-config-vsftpd` 工具将显示常规、服务器控制、访问控制、用户、目录选项、日志、网络选项和传输日志面板（见图 21-1）。从列表中选择你需要的项。常规（General）面板设置基本的服务器功能，例如以独立模式运行、使用的协议以及是否可以下载或上传文件。

服务器控制（Server Control）面板允许你启动和停止服务器，并检查服务器日志。

访问控制（Access Control）面板允许拒绝 `/etc/vsftpd_users.list` 中的用户访问。如果你需要，可以指定另一个文件。你还可以禁止某些电子邮件，并指定登录横幅。

用户（Users）有两个选项卡，一个用于系统用户，另一个用于匿名用户（见图 21-2）。你可以使用匿名用户设置来设置匿名登录的控制，例如允许上传、创建新目录或不需要密码。你还可以指定不同的用户、站点目录或上传文件的所有者，以为你的站点提供更高的安全性。

在目录选项（Directory Options）面板上，你可以控制对文件的访问，隐藏如点文件（配置文件）或任何你想要对匿名用户隐藏的其他类型的文件。

图 21-1：system-config-vsftpd 常规面板

图 21-2：system-config-vsftpd 用户面板

在日志（Logging）面板上，你可以选择日志选项并指定日志目录，默认认为 `/var/log/vsftpd.log`。

在网络选项（Network Options）面板上，你可以控制网络连接，设置连接数限制、失败连接的超时时间以及主动（Active）和被动（Passive）连接的控制（见图 21-3）。

图 21-3：system-config-vsftpd 网络选项面板

在传输日志（Transfer log）面板上，你可以显示传输日志以查看详情。

# 配置 vsftpd

vsftpd 配置使用一个配置文件 `/etc/vsftpd/vsftpd.conf`。配置选项简单且保持最少（见表 21-2）。`vsftpd.conf` 文件包含一组指令，每个选项都分配了一个值（`=` 两边没有空格）。选项可以是分配了 `YES` 或 `NO` 值的开关、带有数值的特征或分配了字符串的选项。`vsftpd.conf` 文件位于 `/etc` 或 `/etc/vsftpd` 目录下。该文件列了一些常用选项并对每个选项进行了详细说明。未使用的选项用前面的 `#` 字符注释。选项名称非常易懂。例如，`anon_upload_enable` 允许匿名用户上传文件，而 `anon_mkdir_write_enable` 让匿名用户创建目录。`vsftpd.conf` 的 Man 页列出了所有选项并为每个选项提供了详细说明。

## 启用独立访问

要将 vsftpd 作为独立服务器运行，你需要将 `listen` 选项设置为 `YES`。这指示 vsftpd 持续监听其分配端口的请求。你可以通过 `listen_port` 选项指定它监听的端口。

`listen=YES`

## 启用登录访问

在以下摘自 `vsftpd.conf` 文件的示例中通过为 `anonymous_enable` 选项分配 `YES` 值来启用匿名 FTP。`local_enable` 选项允许系统上的本地用户使用 FTP 服务器。

```
# Allow anonymous FTP?
anonymous_enable=YES
#
# 取消注释以允许本地用户登录。
local_enable=YES
```

如果你想让匿名用户在不提供密码登录，可以设置 `no_anon_password=YES`。

## 本地用户权限

各种权限控制本地用户如何访问服务器上的文件。如果你想允许本地用户创建、重命名和删除文件……

## 第 21 章：FTP 服务器

所有上传的文件都归匿名 FTP 用户所有。你可以让文件归另一个用户所有，从而提供更大的安全性。事实上，拥有上传文件的实际用户对匿名用户来说是隐藏的。要启用此选项，你使用 `chown_uploads` 并通过 `chown_username` 指定新用户。千万不要将该用户设置为像 root 这样的管理员用户。

```
chown_uploads=YES
chown_username=myftpfiles
```

上传目录本身应该赋予其他用户写权限。

- `chmod 777 /var/ftp/upload`

你可以通过 `anon_mask` 选项控制用户对文件的访问类型，为上传的文件设置默认的读/写权限。默认值为 077，它仅赋予所有者读/写权限（600）。要允许所有用户具有读取权限，你需要将 `umask` 设置为 022，其中 2 关闭写权限但设置读取权限（644）。值 000 则允许所有用户读取和写权限。

## 连接时间限制

为了更有效地控制服务器上的工作负载，你可以对空闲用户和失败的传输设置时间限制。`idle_session_timeout` 和 `data_connection_timeouts` 会在指定时间后断开空闲用户并断开失败连接。默认值所示：

```
idle_session_timeout=600
data_connection_timeout=120
```

## 消息

`dismissage_enable` 选项允许在用户访问该目录时显示目录下的 `.message` 文件中的消息。`ftpd_banner` 选项允许你设置自己的 FTP 登录消息。默认值所示：

```
ftpd_banner=Welcome to blah FTP service.
```

## 日志

一组 `xferlog` 选项控制日志。你可以启用日志，并指定文件的格式和位置。

```
xferlog_enable=YES
```
