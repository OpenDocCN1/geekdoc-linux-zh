
在 `security = server` 模式下，这是 SMB/CIFS 协议的一个限制，无法在 Samba 中修复。

-   如果你正在使用 Windows NT 服务器作为你的密码服务器，那么你必须确保你的用户能够从 Samba 服务器登录，因为在 `security = server` 模式下，网络登录看起来像是从那里发出的，而不是从用户的工作站发出的。

## directory
此参数是 *path* 的同义词。

## path (S)
默认值：*无默认值*

示例：*path* = /home/fred

此参数指定了一个目录，服务的用户将被授予对该目录的访问权限。对于可打印服务而言，这是打印数据在提交给主机进行打印之前暂存的位置。

对于提供来宾访问权限的可打印服务，服务应为只读，并且路径应是全球可写且设置了粘滞位（sticky bit）的。当然，这并非强制要求，但如果你不这样做，可能无法获得预期的结果。

路径中出现的任何 %u 都将被替换为客户端在此连接上使用的 UNIX 用户名。出现的任何 %m 都将被替换为连接来源机器的 NetBIOS 名称。这些替换对于为用户设置伪主目录非常有用。

请注意，如果指定了 *root dir*，则此路径将基于 *root dir*。

## pid directory (G)
默认值：*pid directory* = ${prefix}/var/lock
pid directory = /var/run/

示例：*pid directory* = /var/run/

此选项指定了 pid 文件将放置的目录。

## posix locking (S)
默认值：*posix locking* = *yes*

smbd(8) 守护程序维护一个由 SMB 客户端获取的文件锁数据库。默认行为是将此内部数据库映射到 POSIX 锁。这意味着由 SMB 客户端获取的文件锁与通过非 SMB 方法（例如 NFS 或本地文件访问）访问文件的 POSIX 兼容应用程序看到的锁是一致的。你绝不需要禁用此参数。

## postexec (S)
默认值：*无默认值*

示例：*postexec* = echo "%u disconnected from %S from %m (%I)" >> /tmp/log

此选项指定了一个命令，每当服务断开连接时都会运行。它接受通常的替换。在某些系统上，该命令可能以 root 身份运行。

一个有趣的例子可能是卸载服务器资源：

**postexec = /etc/umount /cdrom**

## prexec close (S)
默认值：*prexec close = no*

此布尔选项控制如果 *prexec* 返回非零代码，是否应关闭正在连接的服务。

## exec
此参数是 *prexec* 的同义词。

## preexec (S)
默认值：*无默认值*

示例：*prexec = echo "%u connected to %S from %m (%I)" >> /tmp/log*

此选项指定了一个命令，每当连接到服务时都会运行。它接受通常的替换。

一个有趣的例子是每次用户登录时向他们发送一条欢迎消息。也许是一条“每日问候”消息？这里是一个示例：

**preexec = csh -c 'echo "\\`Welcome to %S!"` | /usr/local/samba/bin/smbclient -M %m -I %I' &**

当然，过一会儿这可能会变得烦人 :-)

参见 *prexec close* 和 *postexec*。

## prefered master
此参数是 *preferred master* 的同义词。

## preferred master (G)
默认值：*preferred master = auto*

此布尔参数控制 *nmbd(8)* 是否是其工作组的首选主浏览器。

如果设置为 **yes**，启动时 **nmbd** 将强制进行一次选举，并且它在赢得选举方面具有轻微优势。建议此参数与 *domain master* = yes 一起使用，以便 **nmbd** 能够保证成为域主控服务器。

请谨慎使用此选项，因为如果有多个主机（无论是 Samba 服务器，还是 Windows 95 或 NT）在同一子网中是首选主浏览器，它们将定期且持续地尝试成为本地主浏览器。这将导致不必要的广播流量和浏览功能下降。

## preload modules (G)
默认值：*无默认值*

示例：*preload modules = /usr/lib/samba/passdb/mysql.so*

这是应在客户端连接之前加载到 smbd 中的模块路径列表。这在某种程度上提高了 smbd 响应新连接的速度。

## auto services
此参数是 *preload* 的同义词。

## preload (G)
默认值：*无默认值*

示例：`preload = fred lp colorlp`

这是你希望自动添加到浏览列表中的服务列表。这对于主目录和打印机服务最为有用，否则这些服务将不可见。

请注意，如果你只是想加载 printcap 文件中的所有打印机，使用 *load printers* 选项更简单。

## preserve case (S)
默认值：*preserve case = yes*

这控制新创建的文件名是否保留客户端传递的大小写，或者是否强制为 *default case*。

有关更详细的讨论，请参阅 §22:0:NAME MANGLINGS22: 章节。

## print ok
此参数是 *printable* 的同义词。

## printable (S)
默认值：*printable = no*

如果此参数为 *yes*，则客户端可以打开、写入并向指定给该服务的目录提交 spool 文件。

请注意，可打印服务将**始终**允许通过打印数据 spooling 写入服务路径（在用户权限允许的情况下）。*read only* 参数仅控制非打印访问对资源的限制。

## printcap cache time (G)
默认值：*printcap cache time = 600*

示例：`printcap cache time = 600`

此选项指定了再次向打印子系统查询已知打印机之前的秒数。如果值大于 *60*，初始等待时间将设置为 *60* 秒，以便更早地对打印子系统进行首次重新扫描。

将此参数设置为 *0*（*默认值*）将在初始启动后禁用对新添加或移除打印机的重新扫描。

## printcap
此参数是 *printcap name* 的同义词。

## printcap name (S)
默认值：*printcap name = /etc/printcap:$LC_MESSAGES*

示例：*printcap name* = */etc/myprintcap*

此参数可用于覆盖服务器使用的编译时默认 printcap 名称（通常为 */etc/printcap*）。有关为什么要这样做的讨论，请参见上面“[printers] 部分”的讨论。

要使用 CUPS 打印接口，请设置 *printcap name* = *cups*。应在 *[global]* 部分补充设置 *printing* = *cups*。*printcap name* = *cups* 将使用 CUPS 创建的“虚拟” printcap，如你的 CUPS 配置文件中指定那样。

在使用 *lptest* 列出可用打印机的 System V 系统上，你可以使用 *printcap name* = *lptest* 来自动获取可用打印机列表。这是 Samba 在配置时定义了 *SYSV* 的系统的默认设置（这包括大多数基于 System V 的系统）。如果在这些系统上 *printcap name* 设置为 *lptest*，则 Samba 将启动 *lptest -v* 并尝试解析输出以获取打印机列表。

一个最小的 printcap 文件看起来像这样：

```
print1|My Printer 1
print2|My Printer 2
print3|My Printer 3
print4|My Printer 4
print5|My Printer 5
```

其中‘|’分隔打印机的别名。第二个别名中包含空格这一点暗示 Samba 它是注释。

> **注意**
>
> 在 AIX 上，默认 printcap 名称是 */etc/qconfig*。如果 printcap 文件名中出现 *qconfig* 字符串，Samba 将假设该文件是 AIX *qconfig* 格式。

## print command (S)
默认值：*无默认值*

示例：*print command* = */usr/local/samba/bin/myprintscript %p %s*

在打印作业完成 spooling 到服务后，将通过 *system*() 调用使用此命令来处理 spool 文件。通常，指定的命令将提交 spool 文件到主机的打印子系统，但这并不是必须的。服务器不会删除 spool 文件，因此无论你指定什么命令，都应在处理完成后删除 spool 文件，否则你需要手动删除旧的 spool 文件。

