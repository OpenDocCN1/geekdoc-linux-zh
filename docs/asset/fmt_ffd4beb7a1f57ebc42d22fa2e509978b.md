
关于此页面的意见和建议应发送至 gmounrai@videotron.ca

使用用户级安全时，客户端必须先使用有效的用户名和密码“登录”，否则连接将被拒绝。这意味着在 Samba 服务器的 `/etc/passwd` 中必须存在客户端有效的用户名和密码，否则客户端的连接将失败。

`smb passwd = /etc/smbpasswd`

此 "`smb passwd`" 设置了加密的 `smbpasswd` 文件的路径，该文件是 `/etc/passwd` 文件的副本，包含了允许连接到 Samba 服务器的客户端的有效用户名和密码。Samba 软件在请求连接时读取此文件。

`log file = /var/log/samba/%m`

此 "`log file`" 使用扩展名 "`%m`"，允许你为登录到服务器的每个用户或每种机器分离日志文件。

`socket options = IPTOS_LOWDELAY_TCP_NODELAY`

此 "`socket options`" 为局域网优化连接，并提高 Samba 服务器传输文件的性能。

`domain master = Yes`

此 "`domain master`" 将 Samba 守护进程识别为 `(nbmd)` 其工作组的网域主浏览器。此选项通常必须在同一网络和工作组的所有其他 Samba 服务器中，仅在该工作组的一个 Samba 服务器上设置为 "`Yes`"。

`local master = Yes`

此 "`local master`" 允许 Samba 守护进程 `(nbmd)` 成为子网上的本地主浏览器。通常，此选项必须在你的网络中所有其他 Samba 服务器中，仅在作为子网本地主器的一台 Samba 服务器上设置为 "`Yes`"。

`preferred master = Yes`

此 "`preferred master`" 控制 Samba 守护进程 `(nbmd)` 是否为其工作组的首选主浏览器。再次，必须在你网络中的所有其他服务器上设置为 "`Yes`"。

`os level = 65`

此 "`os level`" 决定了 Samba 守护进程 `(nbmd)` 是否有机会成为本地广播区域内 WORKGROUP 的本地主浏览器。如果你的网络上有任何 NT 服务器，数字 65 将获胜；若要让你的 Linux Samba 服务器成为本地广播区域内工作组主浏览器的胜 NT 服务器，则必须将 "`os level`" 设置为 65。此外，此选项必须在一个 Linux 服务器上设置，并对网络上可能存在的所有 Linux Samba 服务器禁用。

`dns proxy = No`

此 "`dns proxy`" 如果设置为 "`Yes`"，则指定 Samba 守护进程在作为 WINS 服务器运行并发现 Net BIOS 名称未注册时，应将 Net BIOS 名称逐字逐字地视作 DNS 查询客户端。然后代表该客户端向 DNS 服务器进行名称查找。由于我们没有配置 Samba 服务器充作为 WINS 服务器，因此我们不需要将其设置为 Yes。

`name resolve order = imhosts host`

此 "`name resolve order`" 决定了命名服务以及将主机名解析为 IP 地址的顺序。

`bind interfaces = True`

关于此页面的意见和建议应发送至 gmnourai@videotron.ca

此选项 '`bind interfaces only`' 如果设置为 True，允许限制机器上哪些接口提供 SMB 服务。这是一项安全功能。配置 "`interfaces = eth0 192.168.1.1`" 完善了此选项。

`interfaces = eth0 192.168.1.1`

此选项 '`interfaces`' 允许你覆盖 Samba 用于浏览、名称注册和 NBT 流量的默认网络接口。默认情况下，Samba 会查询内核获取所有活动接口列表，以及除 127.0.0.1 外任何具有广播能力的接口。通过此选项，Samba 将仅在 IP 地址 192.168.1.1 的 "`eth0`" 接口上监听。这是一项安全功能，并配合上述配置（`bind interfaces only = True`）。

`hosts deny = All`

列在 '`hosts deny`' 中的主机除非服务有自己的列表，否则不允许访问服务。我们默认拒绝对主机的访问，并在下方的 hosts (`hosts allow =`) 选项中允许访问。

`hosts allow = 192.168.1.4 127.0.0.1`

此选项 '`allow`' 是允许访问服务的逗号、空格或分隔主机集合。我们允许主机 192.168.1.4 和本地主机 127.0.0.1 访问 Samba 服务器。注意，必须设置 localhost，否则你将收到错误消息。

`debug level = 1`

此选项 '`debug level`' 允许在 "`smb.conf`" 文件中指定调试级别（日志级别）。如果你将调试级别设置为高于2，可能会导致性能大幅下降。这是因为服务器在每次操作后都会向日志文件写入大量内容，这非常消耗资源。

`create mask = 0640`

此选项 '`create mask`' 根据从 DOS 到 UNIX 权限的映射设置权限。将此选项设置为 0640，从 Windows 系统复制或创建到 Unix 系统的所有文件默认权限均为 0640。

`directory mask = 0750`

此选项 '`directory mask`' 设置在创建目录时从 DOS 转换为 UNIX 模式时使用的八进制模式。将此选项设置为 0750，从 Windows 系统复制或创建到 Unix 系统的所有目录默认权限均为 0750。

`level2 oplocks = True`

此选项 '`level2 oplocks`' 提高了对许多文件频繁访问的性能。

`wide links = no`

此选项 '`wide links`' 控制是否跟踪目录树内的链接。

`read raw = no`

此选项 '`read raw`' 控制服务器是否支持原始读取。

### [tmp]

关于此页面的意见和建议应发送至 gmnourai@videotron.ca

`comment = Temporary Space`

此选项 '`comment`' 类似于客户端查询时看到的文本字段。

`path = /tmp`

此选项 '`path`' 指定用户访问的目录。

`read only = No`

此选项 '`read only`' 指定用户是否为只读。

`valid users = admin`

此选项 '`valid users`' 是允许登录此服务的用户列表。

`invalid users = root daemon sys kmem`

此选项 '`invalid users`' 是不允许登录此服务的用户列表，这实际上是一种“偏执性”的检查，以绝对确保不当设置不会违反安全。

关于此页面的意见和建议，请邮件至 gmourani@videotron.ca

```bash
[-f /etc/smb.conf] || exit 0
```

`RETVAL=0`

# 查看我们是如何被调用的。

case "$1" in

start)

  echo -n "Starting SMB services:"

  daemon smbd -D

  RETVAL=$?

  echo

  echo -n "Starting NMB services:"

  daemon nmbd -D

  RETVAL=$2

  echo

  [ $RETVAL -eq 0 -a $RETVAL -eq 0 ] && touch /var/lock/subsystem/smb || \

  RETVAL=1

stop)

  echo -n "Shutting down SMB services:"

  killproc smbd

  RETVAL=$?

  echo

  echo -n "Shutting down NMB services:"

  killproc nmbd

  RETVAL=$2

  [ $RETVAL -eq 0 -a $RETVAL -eq 0 ] && rm -f /var/lock/subsystem/smb

  echo

  ;;

restart)

  $0 stop

  $0 start

  RETVAL=$?

  ;;

reload)

  echo -n "Reloading smb.conf file:"

  killproc -HUP smbd

  RETVAL=$?

  echo

  ;;

status)

  status smbd

  status nmbd

  RETVAL=$?

  ;;

)

  echo "Usage: $0 [start|restart|status]"

  exit 1

esac

exit $RETVAL
