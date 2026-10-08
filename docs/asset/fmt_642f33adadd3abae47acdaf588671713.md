
这告诉 `smb.conf` 文件按照以下特定配置进行设置：

- `[global]`

`workgroup = OPENENA`
此参数 "`workgroup`" 指定了当客户端查询时，工作组服务器将显示的工作组名称。在客户端和服务器机器上具有相同的工作组名称是重要的。之后，不要忘记在你连接到服务器的客户端部分也设置相同的工作组名称。

`server string = OpenName Samba Server`
此参数 "`server string`" 指定了你希望在打印机管理器的注释框中向用户显示的字符串，或者在 Windows 机器使用 "`net view`" 命令时向 IPC 连接显示的字符串。它可以是任何你希望显示给用户的字符串。

`encrypt passwords = True`
此参数 "`encrypt passwords`" 如果设置为 "`True`"，则指示 Samba 在与客户端协商时使用加密词而不是明文密码。当密码被加密时，嗅探程序（Sniffer program）将无法检测你的密码。出于安全考虑，此选项也必须设置为 "`True`"。这是一项安全功能。

`security = user`
此参数 "`security`" 如果设置为 "`user`"，则指定客户端首先使用有效的用户名和密码进行“登录”，否则连接将被拒绝。这意味着客户端的有效用户名密码必须在 Linux 服务器的 `/etc/passwd` 文件和 Samba 服务器的 `/etc/smbpasswd` 文件中存在，否则客户端的连接将失败。请参阅本章中的“安全 Samba”获取更多关于 `smb.conf` 文件中最重要的设置的信息。这是一项安全功能。

`smb password file = /etc/samba/smbpasswd`
此参数 "`smb password`" 指定了加密的 smbpasswd 文件的路径。"`smbpasswd`" 是 Linux 服务器 `/etc/passwd` 文件的副本，包含了连接到 Samba 服务器的客户端的有效用户名和密码。Samba 软件在请求连接时会读取此文件 (`smbpasswd`)。

`log file = /var/log/samba/log.%m`
此参数 "`log file`" 指定了 Samba 日志文件的位置和名称。通过扩展名 "`$m`"，它允许为你的 Samba 服务器上的每个不同用户或机器拥有独立的日志文件。

`socket options = IPT_LOWDELAY_NODELAY`
此参数 "`socket options`" 指定了你可以包含在 `smb.conf` 配置文件中的参数，用于调优和改进你的 Samba 服务器以获得最佳性能。默认情况下，我们会检查连接是否断开并将其关闭。`deadtime` 为 `0`（默认设置）可以提高 Samba 服务器传输文件的性能。这是一项性能功能。

`deadtime = 15`
此参数 "`deadtime`" 指定了在认为连接已断开并关闭之前等待客户端活动的分钟数。`deadtime` 为 `0`（默认设置）表示不执行自动断开。建议配合几分钟的超时使用此参数以获得更好的系统性能。这是一项性能功能。

`getwd cache = Yes`
此参数 "`getwd cache`" 如果设置为 "`Yes`"，则通过使用缓存算法减少 `getwd()` 消耗的时间。这是一项性能功能。

`lpq cache time = 45`
此参数 "`lpq cache time`" 指定了 `lpq` 信息在内存中缓存多长时间，以防止 `lpq` 命令被频繁调用。当你的系统上 `lpq` 命令非常慢时，建议使用较大的值。这是一项性能功能。

`domain master = Yes`
此参数 "`domain master`" 指定将 "`mbnd`"（即 NetBIOS 服务器守护进程）设置为其给定工作组的域主浏览器（domain master browser），并启用全网范围的浏览列表汇总。此选项通常只需要在一个 Samba 服务器上设置为 "`Yes`"，该设置适用于同一网络和工作组上的所有其他 Samba 服务器。

`local master = Yes`
此参数 "`local master`" 允许 "`nmbd`"（即 NetBIOS 标识守护进程）尝试成为子网上的本地主浏览器（local master browser）。与上述类似，此选项通常只需要在一个 Samba 服务器上设置为 "`yes`"，作为该子网的本地主，供网络上的所有其他 Samba 服务器使用。将此参数设置为 "`Yes`" 不能保证 Samba 会成为子网上的本地主浏览器，但可确保 Samba 参与本地主选举。请配合参数 "`domain master`" 和 "`preferred master`" 使用使用。

`preferred master = Yes`
此参数 "`preferred master`" 指定并控制 "`nmbd`" 是否为你所在组的首选主（preferred master）。一旦，必须在一台服务器上将其设置为 "`yes`"。

`os level = 65`
此参数 "`os level`" 指定了在 Samba 服务器中 `nmbd` 成为本地主浏览器的优先级。在 Samba 服务器上将此参数设置为 `65`，可以允许该 Samba 服务器 成为 域主。

`dns proxy = Yes`
此参数 "`dns proxy`" 如果设置为 "`Yes`"，则允许 `nmbd` 作为 DNS 代理来处理查询请求。

`name resolve = yes`
此参数 "`name resolve`" 指定了 Samba 是否使用 `gethostbyname()` 来解析主机名。

`bind only = True`
此参数 "`bind only`" 如果设置为 "`True`"，则限制 Samba 仅在指定的接口上运行。

`interfaces = eth0 192.168.1.1/24 127.0.0.1`
此参数 "`interfaces`" 指定了 Samba 监听的接口和 IP 地址。

`read only = Yes`
此参数 "`read only`" 指定了该共享是否为 `只读`。

# Samba 4
## 第6 章

### `read raw = No`
此参数 "`read raw`" 控制服务器在向客户端传输数据时是否支持 read raw 请求。请注意，“read raw" 操作不使用内存映射（memory mapping）。因此，如果你像我们一样通过 "`read raw = No`" 禁用 "`read raw`"，你可能会发现内存映射更有效。这是一项性能特性。

`write cache size = 262144`
此参数 "`write cache size`" 允许 Samba 在磁盘子系统成为瓶颈的系统中提高性能。该选项的值以字节为单位，`262,144` 的大小代表每个文件 `256k` 的缓存大小。你可以根据希望与服务器共享的文件大小来合理地设置此参数。大多数共享文件的大小在 `52K` 之间，你可以将参数设置为 "`524288`"。这是一项性能特性。

`comment = 临时文件空间`
此参数 "`comment`" 允许你指定一个注释，当客户端通过网络邻域或 "`net view`" 查询服务器以列出可用共享时，该注释将显示在共享名称旁边。

`path = /tmp`
此参数 "`path`" 指定了服务用户将被访问的目录。在我们的示例中，这是 Linux 服务器的 `/tmp` 目录。

`read only = No`
此参数 "`read only`" 指定是否允许用户只读文件。在我们的示例中，由于这是 Linux 服务器上 "`tmp`" 目录的配置，用户可以的操作不仅仅是读取文件。

`valid users = smbadmin`
此参数 "`valid users`" 指定了允许登录此服务的用户列表。在我们的示例中，仅允许用户 "`smbadmin`" 访问服务。

`invalid users = root bin daemon nobody sys tty disk mem`
此参数 "`invalid users`" 指定了不允许登录服务的用户列表。这实际上上是一个“偏执性”检查，以确保不当设置不会破坏您的安全。建议包含所有在服务器上运行守护程序的默认用户。这是一项安全特性。

# `/etc/samba/lmhosts`: Samba Net BIOS 映射文件

`/etc/lmhosts` 文件是 Samba Net BIOS 名到 IP 地址的映射文件。它与 `/etc/hosts` 格式非常相似，不同之处主机部分必须对应 Net BIOS 命名格式。**加粗文本**是脚本初始化文件中必须根据你的需要自定义和调整的部分。

- 创建 `lmhosts` 文件（`touch /etc/samba/lmhosts`）并添加以下行：

```
# 示例 Samba lmhosts 文件。

127.0.0.1localhost

192.168.1.30    station1

192.168.1.31    station2
```

在我们的示例中，该文件包含了三个 IP 到 Net BIOS 名的映射。`localhost` (`127.0.0.1`) 是必须的，名为 `station1`(`192.168.1.30`) 的客户端机器，以及另一个名为 `station2`(`192.168.1.31`) 的客户端机器。不要忘记在该文件中列出你的其他客户端名称。

# `/etc/sysconfig/samba`: Samba 系统配置文件

`/etc/sysconfig/samba` 文件用于指定 Samba 系统配置信息，例如启动时是否需要传递给 `smbd` 和 `nmbd` 守护进程的额外选项。

- 创建 `samba` 文件（`touch /etc/sysconfig/samba`）并添加以下行：

```
# 在服务器上作为守护进程启动 Samba。

SMDBOPTIONS="-D"

# 在服务器上作为守护进程启动 Samba。

NMDBOPTIONS="-D -H /etc/samba/lmhosts"

# 在服务器上作为守护进程启动 WINBIND。

WINBINDOPTIONS="*"
```

带有 "`-D`" 选项的 "`SMDBOPTIONS`" 和 "`NMDBOPTIONS`" 参数指示 samba 在系统中作为守护进程运行。默认情况下必须在该文件中指定这些值，否则服务器将**不会**作为守护进程运行。以守护进程运行服务器是运行 Samba 的推荐方式。

# `/etc/pam.d/samba`: Samba PAM 支持配置文件

为了提高 Samba 的安全性，我们将使用 PAM 密码认证支持。要做到此，你必须创建 `/etc/pam.d/samba` 文件并按顺序添加以下参数：

- 创建 `pam` 文件（`touch /etc/pam.d/samba`）并添加以下行：

```
auth       required      /lib/security/pam_stack.so service=system-auth

auth       required      /lib/security/pam_nologin.so

account    required      /lib/security/pam_stack.so service=system-auth

account    required      /lib/security/pam_access.so

account    required      /lib/security/pam_time.so

password   required      /lib/security/pam_stack.so service=system-auth

session     required      /lib/security/pam_stack.so service=system-auth

session     required      /lib/security/pam_limits.so

session     optional      /lib/security/pam_console.so
```

# `/etc/logrotate.samba`: Samba 日志轮配置文件

此文件允许 Samba 服务器在指定时间自动轮转日志文件。在这里我们将配置 `/etc/logrotate.d/samba` 文件来自动轮转每个日志文件。

- 创建 `samba` 文件（`touch /etc/logrotate.d/samba`）并添加以下行：

```
/var/log/samba/*.log {

  notempty

  missing

  sharedscripts

  copyuncate

  postrotate

  /usr/kill -H `cat /var/run/smbd.pid /var/run/nmbd.pid` 2>/dev/null || true

  endscript

}
```

`/etc/init.d/smbd`: Samba 初始化文件

`smbd` 脚本负责在你的 Linux 系统上自动启动和停止 Samba。将 `smbd` 和 `nmbd` 作为独立守护进程加载将消除加载时间并减少交换。请注意，以下脚本适用于使用 System V 的 Linux 操作系统。如果你的 Linux 系统使用 BSD 等方法，你必须调整脚本以使其工作。

步骤1 创建 `smbd` 脚本（`touch /etc/init.d/smbd`）并添加以下行：

```bash
#!/bin/bash

# 此脚本负责启动和停止 Samba。

# chconfig: 3

# description: 启动和停止 smbd 和 nmbd 守护进程

# 用于提供 SMB 服务。

# config: /etc/samba/smbd.conf

# pidfile: /var/run/smbd.pid

# pidfile: /var/run/nmbd.pid

# 载入库。
. /etc/init.d/functions

# 载入网络配置。
. /sysconfig/network

# 如果有额外选项。
if [ -f /sysconfig/samba ]; then
  . /sysconfig/samba
fi

# 检查网络是否就绪。
[ $NETWORK = "no" ] && exit 0

# 避免使用 root TMPDIR
unset TMPDIR

# Samba Samba可用。
[ -f /usr/sbin/smbd ] || exit 0
[ -f /usr/sbin/nmbd ] || exit 0

# Samba 二进制文件的路径。
smbd=/usr/sbin/smbd
nmbd=/usr/sbin/nmbd

RETVAL=0
prog="Samba"
start() {
    KIND="Smbd"
```
