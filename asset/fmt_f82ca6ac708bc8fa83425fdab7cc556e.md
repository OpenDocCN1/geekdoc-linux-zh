
虽然该文件的内容仍必须以明文形式存在，但你可以将`/etc/smbdonna`文件配置为仅 root 管理用户可读。也可以使用类似信息配置 automounter。但由于 automounter 是 RHCSA 技能，你需要参考第 6 章获取相关信息。

## 认证目标 15.03

### Samba 故障排除

Samba 很复杂。对于复杂的服务，简单的错误可能难以诊断。幸运的是，Samba 包含出色的故障排除工具。基本的`testparm`命令测试语法。日志文件可以提供更多信息。当然，除非对本地防火墙进行适当更改，否则 Samba 可能根本无法从远程系统访问。

### Samba 问题识别

Samba 是一个宽容的服务。它包含许多参数的同义词。有些参数拼写错误；例如，`writable`是`writeable`的同义词。但除这些参数外，`testparm`命令可以帮助识别问题。例如，图 15-7 说明了许多问题。未识别的参数会以“unknown parameter”消息突出显示。

有些参数不能一起使用。例如，以下`testparm`输出中的消息突出了两个不兼容的指令：

```
ERROR: both 'wins support = true' and 'wins server = <server list>' cannot be set in the smb.conf file. nmbd will abort with this setting.
```

有时，故障排除命令会出现在其他命令的输出中。例如，问题经常出现在各种命令的输出中。有时输出很直接，例如以下针对特定`mount.cifs`命令的输出，与错误的共享名称相关。它还表明在与 Microsoft 操作系统相关的网络上，共享名称的大小写不太重要。

```
Retrying with upper case share name
```

有时，消息可能看起来更直接，例如

```
mount error(13): Permission denied
```

但该消息可能指的是错误的密码，或未在 Samba 数据库中配置的用户。

有时问题可能看起来更烦人。例如，如果你挂载远程主目录但该目录中没有显示文件，这可能意味着 SELinux 的`samba_enable_home_dirs`布尔值尚未启用。如果你挂载的远程目录不是用户主目录，这可能意味着目录及其相关文件未正确标记为`samba_share_t`文件类型。

### 图 15-7
使用`testparm`检查 Samba 配置

```
[root@mini ~]# testparm /etc/samba/smb.conf

Load smb config files from /etc/samba/smb.conf

rlimit_max: rlimit_max (1024) below minimum Windows limit (16384)

Unknown parameter encountered: "security"

Ignoring unknown parameter "security"

Unknown parameter encountered: "passdb backend"

Ignoring unknown parameter "passdb backend"

Processing section "[homes]"

Processing section "[printers]"

Processing section "[public]"

Unknown parameter encountered: "write list"

Ignoring unknown parameter "write list"

Loaded services file OK.

ERROR: both 'wins support = true' and 'wins server = <server list>' cannot be set in the smb.conf file. smbd will abort with this setting.

Server role: ROLE_STANDALONE

Press enter to see a dump of your service definitions
```

### 本地日志文件检查

与 Samba 相关的问题可能出现在`/var/log/messages`文件中，也可能出现在`/var/log/samba`目录中的不同文件中。首先，`testparm`命令输出中显示的语法错误也可能出现在`/var/log/messages`文件中。当 Samba 服务启动时，配置文件中的错误是值得在标准系统日志文件中报告的问题。

此外，当尝试挂载共享 Samba 目录失败时，相关的消息也会出现在`/var/log/messages`文件中。有时消息很直接，例如`cifs_mount failed`，或`NT_STATUS_LOGON_FAILURE`。

大多数 Samba 日志文件位于`/var/log/samba`目录中。如图 15-8 所示，日志文件按连接到服务器的客户端的主机或 IP 地址分类。通常，消息越少表示成功。例如，连接到本地主机系统，这对于故障排除很有用，可能在`log.__ffff_127.0.0.1`日志文件中包含以下消息：

```
__ffff_127.0.0.1 (::ffff:127.0.0.1) connect to service michael

initially as user michael (uid=1000, gid=1000) (pid 23800)
```

其中的信息表明同时使用了 IPv4 和 IPv6 地址。已连接用户由 UID、GID 和 PID 数字标识。如果未经授权的用户连接，这些数字可以帮助识别有问题用户和/或受损账户，以及相关的进程 ID 号。

该目录中的大多数其他文件与各种服务命名相关；例如，`log.smbd`、`log.nmbd`和`log.winbindd`文件收集与每个日志文件中命名的守护进程相关的消息。

### 启用远程访问

除非允许其他系统访问，否则网络服务没什么用。与其他 RHEL 6 系统一样，每个服务器都有防火墙。默认情况下与 Samba 关联的端口是关闭的。通过防火墙配置工具，很容易为 Samba 服务器和 Samba 客户端设置访问。只需指定服务器或客户端为受信任服务即可。

如前几章所述，可以限制防火墙对某些 IP 地址的远程访问。`iptables`基于防火墙中的`-s`开关配置源地址。例如，以下规则将限制对 NetBIOS 名称服务的通信，仅限于 IP 地址`192.168.122.150`之外的任何系统：

```
-A INPUT -m state --state NEW -m udp -p udp -s !192.168.122.150 --dport 137 -j ACCEPT
```
