
[TAB] 切换区域 [q] 退出 [UP] 向上 [DOWN] 向下 [/] 搜索 [x] 下一个

**图 8-1.** Samba-regedit

最后，我们甚至可以从 Windows 机器执行微软 regedit 并连接到远程注册表（图 8-2）。我们需要提供 Samba 用户的凭据，并且根据用户授予的权限，我们将看到某些注册表值或看不到。

![](img/dfa44432604022575079471b648e25ca_221_0.png)

**图 8-2. Regedit**

在案例中，我们将使用 `net` 子命令来管理注册表项。假设我们要添加一个新的共享。首先在服务器上创建该共享。

```bash
[root@hotel ~]## mkdir /reg_share
```

我们将更改 SELinux 上下文。

```bash
[root@hotel ~]## chcon -t samba_share_t /reg_share/
```

我们还必须确保系统重启时该文件夹具有正确的上下文。

```bash
[root@hotel ~]## semanage fcontext -a -t samba_share_t "/reg_share/(.*)\\"
```

我们在共享内部创建一个示例文件。

```bash
[root@hotel ~]## echo "123" > /reg_share/file_shared_through_registry.txt
```

我们使用 `net conf` 将共享定义添加到 Samba 注册表中。

```bash
[root@hotel ~]# net conf addshare regshare /reg_share/ writable=N guest_ok=y "Registry based share"
```

我们传递了共享名称（`/reg_share/`）以及两个参数：不可写和公共。

我们可以通过 `net registry enumerate` 共享定义是否已正确添加到 Samba 注册表中。

```bash
[root@hotel]# net registry enumerate HKLM\Software\Samba\smbconf'

Keyname = regshare

Modtime = Tue, 01 Jan 1970 01:00:00 CET

[root@hotel]# net registry enumerate HKLM\Software\Samba\smbconf\regshare

Valename = path

Type = REG_SZ

Value = "/reg_share/"

nValename = comment

Type = REG_SZ

Value = "Registry based share"

nValename = guest ok

Type = REG_SZ

Value = "yes"

nValename = read only

Type = REG_SZ

Value = "yes"
```

我们看到命令添加了多个 `REG_SZ` 类型的值。这是一种由空字符终止的字符串。还有许多其他类型，例如 `REG_MULTSZ`，它是一个由空字符终止的字符串序列。除了这两种常用类型外，可以在微软官方文档中研究许多其他类型。

我们也可以通过 `net registry enumerate` 检查 Samba 注册表中的共享定义。

## 第 8 章：SAMBA 概念与架构、SAMBA 配置以及国际化

配置文件分为两个主要部分：全局（global）和共享（shares）。

全局部分定义了适用于整个服务器的参数。通常，我们可以在全局部分看到参数的描述。共享部分则在其中定义了共享资源，如主目录、打印机或文件夹。

要检查共享定义是否已正确添加到 Samba 注册表中，我们使用：

```bash
[root@hotel]# net registry enumerate HKLM\Software\Samba\smbconf'

Keyname = regshare

... 

    path = /reg_share/

    comment = "Registry based share"

    guest_ok = yes

    read_only = yes
```

# 第 8 章 SAMBA 概念与架构、SAMBA 配置以及国际化

按回车键查看服务定义转储

```
### Global parameters

[global]

abort shutdown script =

add group script =

add machine script =

addport command =

addprinter command =

add share command =

add user script =

add user to group script =

afs token lifetime = 604800

afs username map =

aio max threads = 100

```

由于命令输出内容非常长，如果我们只是想检查某个参数的值，可能需要使用 `grep`。

```
[root@hotel ~]# testpar -v | grep "preferred master"

Load smb config files from /etc/samba/smb.conf

rlimit_max: increasing rlimit_max (1024) to minimum Windows limit (16384)

Processing section "[homes"

Processing section "[printers]"

Processing section "[print$]"

Processing section "[Docs]"

Loaded services file OK.

Server role: ROLE_STANDALONE
```

按回车键查看服务定义转储

```
preferred master = Auto
```

# 第 8 章 SAMBA 概念与架构、SAMBA 配置以及国际化

我们将更改之前看到的参数值。

```
workgroup = MY_SAMBA_GROUP

server string = My Samba Server %v

netbios name = HOTEL
```

重启 SMB 服务后，如果再次执行 `testparam`，我们将看到输出发生了变化。

```
[root@hotel ~]# testparam

Load smb config files from /etc/samba/smb.conf

rlimit max: increasing rlimit_max (1024) to minimum Windows limit (16384)

Processing section "[printers"

Processing section "[Docs]"

Loaded services file OK.

Server role: ROLE_STANDALONE

Press enter to see a dump of your service definitions
```

```
[global]

workgroup = MY_SAMBA_GROUP

netbios name = HOTEL

server string = My Samba Server %v

log file = /var/log/samba/log.log

max log size = 50

idmap config * : backend = tdb

cups options = raw
```

另一个有趣的参数是 "log file"：

```
# log files split per-machine:

log file = /var/log/samba/log.log

# maximum size of 50KB per log file, then rotate:

max log size = 50
```
