
`IP 地址` 是要连接的服务器地址。应以标准的 “a.b.c.d” 记法指定。

通常，客户端会尝试通过上文 `name resolve order` 参数中描述的 NetBIOS 名称解析机制来查找命名的 SMB/CIFS 服务器。使用此参数将强制客户端假设该服务器位于指定 IP 地址的机器上，并且将忽略正在连接的资源中 NetBIOS 名称部分。

此参数没有默认值。如果未提供，客户端将根据上述描述自动确定。

### `-p|--port port`

此数字是在连接到服务器时使用的 TCP 端口号。SMB/CIFS 服务器的标准（知名）TCP 端口号是 139，这是默认值。

### `-d|--debuglevel=level`

`level` 是 0 到 10 之间的整数。如果未指定此参数，默认值为 0。该值越高，日志文件中记录的关于服务器活动的详细信息就越多。在级别 0 时，仅记录关键错误和严重警告。级别 1 是日常运行的合理级别 - 它生成关于所执行操作的小量信息。

高于 1 的级别将产生大量日志数据，应仅在调查问题时使用。高于 3 的级别专为开发人员设计，会产生 HUGE 量的日志数据，其中大部分都极其晦涩。请注意，在此处指定此参数将覆盖 `s.conf` 文件中的 `log level` 参数。

### `-V|--version`

打印程序版本号。

### `-s|---configfile=<configuration file>`

指定文件包含服务器所需的配置详情。该文件中的信息包括服务器特定信息，例如使用什么 printcap 文件，以及服务器将提供的所有服务的描述。有关更多信息，请参阅 `s.conf`。默认配置文件名称在编译时确定。

### `-l|---log-basename=logdirectory`

日志/调试文件的基础目录名称。将追加扩展名 `.sclient`（例如 `log.sclient`, `log.smbd` 等…）。日志文件永远不会被客户端删除。

### `---option=<name>=<value>`

从命令行将 s 选项“`<name>`”设置为值“`<value>`”。这会覆盖编译时的默认值和从配置文件读取的选项。

### `-N|---no-pass`

如果指定了此参数，客户端将抑制向用户的常规密码提示。这在访问不需要密码的服务时很有用。除非在命令行上指定了密码或指定了此参数，否则客户端将请求密码。

如果在命令行上指定了密码并且也定义了此选项，则命令行上的密码将被静默忽略，并且不使用密码。

### `-k|---kerberos`

尝试使用 kerberos 进行身份验证。仅在 Active Directory 环境中有用。

### `-C|---use-ccache`

尝试使用由 winbind 缓存的凭据。

### `-A|---authentication-file=filename`

此选项允许你指定一个文件，从中读取连接中使用的用户名和密码。文件格式为

```
username = <value> password = <value> domain = <value>
```

确保文件权限限制非预期用户的访问。

### `-U|--user=username[%password]`

设置 SMB 用户名或用户名和密码。

如果未指定 `%password`，将提示用户输入。客户端首先检查 `USER` 环境变量，然后是 `LOGNAME` 变量，如果任者存在，则字符串将被大写。如果未找到这些环境变量，则使用用户名 `GUEST`。

第三种选项是使用包含用户名和密码明文的凭据文件。此选项主要提供给管理员不希望通过命令行或环境变量传递凭据的脚本使用。如果使用此方法，请确保文件权限限制非授权用户的访问。有关更多细节，请参阅 `-A`。

在脚本中包含密码时要谨慎。此外，在许多系统上，可以通过 `ps` 命令看到正在运行的进程的命令行。为了安全起见，始终让 rpcclient 提示输入密码并直接键入它。

### `-S|--signing on|off|required`

设置客户端签名状态。

### `-P|--machine-pass`

使用存储的机器账户密码。

### `-e|--encrypt`

此命令行参数要求远程服务器支持 UNIX 扩展或已选择 SMB3 协议。请求对连接进行加密。使用 GSSAPI 通过 SMB3 或 POSIX 扩展协商 SMB 加密。使用给定的凭据进行加密协商（如果给定域/用户名/密码三元组，则为 kerberos 或 NTLMv1/v2）。如果无法协商加密，则连接失败。

### `---pw-nt-hash`

提供的密码是 NT 哈希值。

### `-n|--netbiosname <primary NetBIOS name>`

此选项允许你覆盖 s 为自己使用的 NetBIOS 名称。这与在 `s.conf` 文件中设置 `netbios name` 参数相同。但是，命令行设置优先于 `s.conf` 中的设置。

### `-i|--scope <scope>`

这指定了 nlookup 在生成 NetBIOS 名称时用于通信的 NetBIOS 作用域。有关 NetBIOS 作用域的使用详情，请参见 `rfc1001.txt` 和 `rfc1002.txt`。NetBIOS 作用域很少使用，仅当你负责所有你与之通信的 NetBIOS 系统的系统管理员时才设置此参数。

### `-W|--workgroup=domain`

设置用户名的 SMB 域。这会覆盖 `s.conf` 中定义的默认域。如果指定的域与服务器的 NetBIOS 名称相同，则会导致客户端使用服务器的本地 SAM（而不是域 SAM）登录。

### `-O|--socket-options socket options`

在客户端套接字上设置的 TCP 套接字选项。有关有效选项列表，请参阅 `s.conf` 手册页中的 `socket options` 参数。

### `-?|--help`

打印命令行选项摘要。

### `---usage`

显示简要用法消息。

## 命令

### LSARPC

- `lsaquery`
  查询信息策略

- `lookupids`
  将 SID 列表解析为用户名。

- `lookupnames`
  将用户名列表解析为 SID。

- `enumtrust`
  枚举受信任域

- `enumprives`
  枚举特权

- `getdispname`
  获取特权名称

- `lsaenumtrisid`
  枚举 LSA 受信任域

- `lsaenumprivsaccount`
  枚举某个 SID 的特权

- `lsaenumaccsrights`
  枚举某个 SID 的权利

- `lsaenumaccswithsright`
  枚举拥有特定权利的用户账户

- `lsaaddaccsrights`
  为用户账户添加权利

- `lsaremoveaccsrights`
  移除用户账户的权利

- `lsalookupprivvalue`
  根据名称获取特权值

- `lsaquerysecobj`
  查询 LSA 安全对象

### LSARPC-DS

- `dsroledomainfo`
  获取主域信息

### DFS

- `dfsexist`
  查询 DFS 支持情况

- `dfsadd`
  添加 DFS 共享

- `dfsremove`
  移除 DFS 共享

- `dfsgetinfo`
  查询 DFS 共享信息

- `dfsenum`
  枚举 DFS 共享

### REG

- `shutdown`
  远程关机

- `abortshutdown`
  终止关机

### SRVSVC

- `srvinfo`
  服务器查询信息

- `netshareenum`
  枚举共享

- `netshareenumall`
  枚举所有共享

- `netsharegetinfo`
  获取共享信息

- `netsharesetinfo`
  设置共享信息

- `netsharesetdfsflags`
  设置 DFS 标志

- `netfileenum`
  枚举打开的文件

- `netremotetod`
  获取远程当前时间

- `netvalidate`
  验证共享名称

- `netfilegetsec`
  获取文件安全信息

- `netssddl`
  删除会话

- `netsessenum`
  枚举会话

- `netdiskenum`
  枚举磁盘

- `netconnenum`
  枚举连接

- `netshareadd`
  添加共享

- `netsharedel`
  删除共享

### SAMR

- `queryuser`
