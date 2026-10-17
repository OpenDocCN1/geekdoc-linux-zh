
# 多路路径 (MULTIPATH)

## 名称 (NAME)

`multipath` - Device mapper target autoconfig

## 摘要 (SYNOPSIS)

```
multipath [-v verbosity] [-b bindings_file] [-d] [-h|-l|-ll|-f|-t|-F|-B|-c|-q-r|-r|-a|-A-]] [-p failover|multibus|group_by_serial|group_by_prio|group_by_node_name] [device]
```

## 描述 (DESCRIPTION)

`multipath` 用于出于故障转移或性能考虑检测指向设备的多个路径并对其进行合并。

## 选项 (OPTIONS)

`-v verbosity`，详细程度，打印所有路径和多路路径

`0` 无输出

`1` 仅打印创建或更新的多路路径名称，用于向其他工具 `kpartx` 输入

`2` + 输出信息：检测到的路径、合并的路径（即多路路径）和设备映射

`-h` 打印用法

`-d` 空运行运行，不创建或更新 devmaps

`-l` 从所有可用信息显示当前的多路路径拓扑（sysfs, 设备映射器 `-LL` 显示当前多路路径拓扑）

## 参见 (SEE ALSO)

`traceroute(8)`, `ping(8)` TCP/IP Illustrated (Stevens, ISBN 0201633469).

## 作者 (AUTHORS)

`multipath` 由 Christophe Varoqui <christophe.varoqui@opensvc.com> 和其他人开发。

# 守护进程 (MULTIPATHD)

## 名称 (NAME)

`multipathd` - 多路守护进程

## 摘要 (SYNOPSIS)

```
multipathd [options]
```

## 描述 (DESCRIPTION)

`multipathd` 进程负责检查故障路径。当发生这种情况时，它将重新配置所属的多路映射，以便该映射恢复最大的性能和冗余。

该守护进程在事件发生时执行外部 `multipath` 工具。反之，`multipath` 工具在完成 devmap 重配置后信号 `multipathd` 进程，以便其刷新故障路径列表。

## 选项 (OPTIONS)

`-d` 空运行运行，不创建或更新 devmaps，并将所有消息输出到 stdout 和 stderr。

`-v verbosity`，详细程度，在运行 `multipathd` 时打印额外信息。级别 `0` 表示仅打印错误。级别 `3` 或更高将打印调试信息。

`-k` `multipathd` 将进入交互模式。在此模式下，可以通过输入 `help` 查看可用命令。

## 命令 (COMMANDS)

可以查看以下命令：

- `show paths`
- `show format`
- `show daemon`
- `show group`
- `show status`
- `show stats`
- `show topology`
- `show map`
- `show wildcards`
- `show config`
- `show blacklist`
- `show devices`
- `add`
- `remove`
- `resize`
- `switch switchgroup`
- `reconfigure`
- `suspend`
- `resume`
- `reset`
- `reload`
- `fail`
- `reinstate`
- `disablequeueing`
- `restorequeueing`
- `forcequeueing`
- `map|multipath $map setprstatus`

```
map|multipath $map unsetprastatus
禁用 $map 上的持久保留管理
```

```
map|multipath $map getprastatus
获取 $map 当前的持久保留管理状态
```

```
quit|exit
结束交互会话。
```

```
shutdown
停止 multipathd。
```

### 另参

`multipath(8)` `kpartx(8)` `hotplug(8)`

### 作者

`multipathd` 由 Christophe Varoqui, <christophe.varoqui@opensvc.com> 等人开发。

# 名称IF

## 名称

`nameif` - 根据 MAC 地址重命名网络接口

## 概要

```
nameif [-c configfile] [-s] nameif [-c configfile] [-s] {interface macaddress}
```

## 注意事项

此程序已过时。请检查 `ip link` 作为替代方案。此功能也可以通过 udev 方法更好地提供。

## 描述

`nameif` 根据 mac 地址重命名网络接口。在未提供参数时，将读取 `/etc/mactab`。该文件的每行包含一个接口名称和一个以太网 MAC 地址。允许以 `#` 开头的注释。否则，将处理命令行上指定的接口。`nameif` 查找具有给定 MAC 地址的接口并将其重命名为指定的名称。

当给出 `-s` 参数时，所有错误信息将发送到 syslog。

当给出 `-c` 参数并指定文件名时，将读取该文件而不是 `/etc/mactab`。

## 备注

`nameif` 应该在接口启动之前运行，否则将失败。

## 文件

`/etc/mactab`

## 另参

`ip(8)`, `udev(7)`

## 缺陷

目前仅对以太网起作用。

# ndptool

## 名称

`ndptool` – 邻居发现协议工具

## 概要

```
ndptool -h
ndptool [OPTIONS] COMMAND
```

## 描述

`ndptool` 是一个为邻居发现协议消息提供封装的工具。

## 选项

`-h`, `--help`

向控制台打印帮助文本并退出。

`-v`, `--verbose`

增加输出的详细程度。

`-t type`, `--msg-type type`

指定消息类型。支持以下类型：

- `rs` - 路由器请求 (Router Solicitation)。
- `ra` - 路由器公告 (Router Advertisement)。
- `ns` - 邻居请求 (Neighbor Solicitation)。
- `na` - 邻居公告 (Neighbor Advertisement)。

`-i ifname`, `--idname ifname`

指定接口名称。

## 命令

`monitor`

监控传入的 NDP 消息并将其打印。

`send`

发送指定类型的 NDP 消息。

## 作者

Jiri Pirko 是 libndp 的作者和当前维护者。

# 网络

## 名称

`net` - 管理 Samba 和远程 CIFS 服务器的工具。

## 概要

```
net {<ads|rap|rpc>} [-h|help] [-w|workgroup workgroup] [-W|—myworkgroup myworkgroup] [-U|user user] [-I|ipaddress ip-address] [-p|—port port] [-n myname] [-s confile] [-S|—server] [-l|long] [-v|verbose] [-f|—force] [-P|—machine-pass] [-d debuglevel] [-V|—request-timeout seconds] [-t|—timeout seconds] [-i|stdin] [--allocreport]
```

## 描述

该工具是 `samba(7)` 软件包组的一部分。

Samba `net` 工具的作用方式与 Windows 和 DOS 中的 net 工具完全相同。第一个参数应用于指定执行特定命令时使用的协议。ADS 用于 ActiveDirectory，RAP 用于旧版 (Win9x/NT3) 客户端，RPC 可用于 NT4 和 Windows 2000。如果省略此参数，net 将尝试自动确定它。并不是所有命令在所有协议上都可用。

## 选项

`-?|help`

打印命令行选项的摘要。

`-k|kerberos`

尝试使用 kerberos 进行身份验证。仅在 Active Directory 环境下有用。

`-w|workgroup target-workgroup`

设置工作组或域。你必须指定此选项或服务器的 IP 地址或名称。

`-W|myworkgroup workgroup`

设置客户端工作组或域。

`-U|user user`

要使用的用户名。

`-I|ipaddress ip-address`

要使用的目标服务器 IP 地址。你必须指定此选项或工作组或目标服务器。

`-p|port port`

连接到目标服务器的端口（通常为 139 或 445）。默认首先为 445，然后是 139。

`-n|netbiosname NetBIOS 名称`

此选项允许覆盖 Samba 自身使用的 NetBIOS 名称。这与在 smb.conf 中设置 netbios name 相同。然而，命令行设置将优先于 smb.conf 中的设置。

`-s|configfile=<configuration file`

指定的文件包含服务器所需的配置细节。文件中的信息包括服务器特定的有信息，例如使用哪个 printcap，以及所有将提供的服务的描述。默认配置名称在编译时确定。

`-S|server`

目标服务器的名称。你应该指定此选项或工作组或目标 IP 地址。

`-l|long`

在列出数据时，为每个项目提供更多信息。

`-v|verbose`

在列出数据时，为每个项目提供详细信息。

`-f|force`

强制执行 net 命令。

`-P|machine-pass`

使用本地服务器的机器账户对外部服务器进行查询。

`-request-timeout seconds`

让客户端请求在秒后超时，默认为 10 秒。

`-t|timeout seconds`

设置客户端操作的超时时间（秒）。

`-use-cache`

尝试使用 winbind 缓存的凭据。

`-i|stdin`

从标准输入获取 net 命令的输入。

`-allocreport`

在处理 net 命令时生成 talloc 报告。

`-T|test`

仅测试命令序列，空运行。

`-F|flags`

将整数标志传递给 net 子命令。

`-C|comment`

将注释字符串传递给 net 子命令。

`-n|myname MYNAME`

使用 MYNAME 作为 net 子命令的请求者名称。

`-c|container`

为 net 操作特定的 AD 容器。

`-M|maxusers MAXUSERS`

在 net rpc share 操作中填充 maxusers 字段。

`-r|reboot`

在命令成功执行后重启远程机器（例如在远程加入操作中）。

`-force-full-repl`

在调用 `net rpc keytab` 时，此选项强制重新创建生成的 keytab 文件。

`-single-obj-repl`

在调用 `net rpc keytab` 时，此选项允许仅同步对象到生成的 keytab 文件。

`-clean-old-entries`

在调用 `net rpc keytab` 时，此选项清理生成的 keytab 文件中的旧条目。

`-db`

为 `net idmap` 命令定义 dbfile。

`-lock`

激活 dbfile 的锁定。

`-a|auto`

在 `net idmap check` 中激活非交互模式。

`-repair`

在 `net idmap check` 中激活修复模式。

`-acls`

在 `net rpc migrate` 中包含 ACL。

`-atts`

在 `net rpc migrate` 中包含属性。

`-timestamps`

在 `net rpc migrate` 中包含时间戳。

`-X|exclude DIRECT`

在使用 `net rpc migrate` 时排除目录。

`-destinationSERVERNAME`

定义迁移的目标服务器名称（默认 localhost）。

`-L|local`

将映射类型设置为本地（用于 `net groupmap set`）。

`-D|domain`

将映射类型设置为域（用于 `net groupmap set`）。

`-N|ntname NTNAME`

设置映射的 ntame（用于 `net groupmap set`）。

设置映射的 rid（用于 `net groupmap set`）。

`reg-version REG_VERSION`

假设数据库版本 {1,2,3}（用于 `net registry check`）。

`output FILENAME`

输出数据库文件（用于 `net registry check`）。

`wipe`

从头创建一个新数据库（用于 `net registry check`）。

`precheck_DB_FILENAME`

定义用于数据库预检查的文件（用于 `net registry import`）。

`encrypt`

此命令行需要远程服务器支持 UNIX 扩展或选择了 SMB3 协议。请求加密连接。使用 SMB3 或通过 GSSAPI 使用 POSIX 扩展协商加密。使用给定的凭据进行加密协商（如果是 de域/用户名/密码三元组则使用 kerberos）。如果无法协商加密则连接失败。

`debuglevel=level`

level 为 0 到 10 的整数。如果没有指定此参数，默认值为 1。

此值越高，日志文件中记录的服务器活动详细信息就越多。在级别 0，仅记录关键错误和严重警告。级别 1 是日常运行的合理水平——它产生有关执行操作的少量信息。1以上的级别将产生大量的日志数据，应仅在调查问题时使用。3以上的级别专为开发者设计，并产生巨大的日志数据，其中大部分极其晦涩。注意，在此指定此参数将覆盖 smb.conf 文件中的 log level[] 参数。

`--version`

打印程序版本号。

更多信息请参阅 smb.conf。默认配置文件名是在编译时确定的。

`-l|log-basename=logdirectory`

日志/调试文件的基础目录名称。将附加后缀 `.progname`（例如 log.smbclient, log.smbd, 等...）。客户端永远不会删除日志文件。

`--option=<name>=<value>`

从命令行中将 smb.conf(5) 选项 "<name>" 设置为值 "<value>"。这将覆盖编译的默认值和从配置文件读取的选项。

## 命令 (COMMANDS)

# CHANGESECRETP
