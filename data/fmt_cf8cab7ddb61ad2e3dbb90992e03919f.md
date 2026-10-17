
# 增强你的 iptables 防火墙

你可以通过许多方式修改或扩展本章给出的 `iptables` 示例。`iptables` 极其灵活。

当你实际上创建自己的 `iptables` 防火墙时，应该参考 `iptables` 帮助页（输入 `iptables`）获取关于选项、匹配方法、输入地址的方法以及细节的详细描述。我还推荐 Oskar Andreansson 编写的优秀 `iptables` 教程（`www.linux-sxs.org/iptables/iptables-tutorial`）。

以下是使用 `iptables` 特性的几点提示：

- **减少规则** — 尝试通过减少规则数量来提高性能。使用子链（`subchains`）可以防止数据包使用不相关的规则。
- **处理分片** — 使用 `-f` 选项引用被分成分片的数据包的第二个及后续包。通常情况下，不丢弃没有第一个数据包分片的第二、第三分片是安全的，因为它们不会被重组。如果你使用 NAT，分片会在过滤之前重组，因此你不应该遇到未完成的分片通过的问题。
- **相反** — 要使一条规则变为其相反，使用感叹号 (`!`)。
- **所有接口** — 要匹配某种类型的所有接口，使用加号 (`+`)，例如 `eth+`。
- **阻塞连接** — 使用 `--syn` 选项阻塞 SYN 包（即请求连接的数据包）。此选项仅适用于 TCP 数据包。
- **限制** — 使用 `--limit` 选项限制产生日志消息的匹配范围。此选项允许匹配每秒仅产生有限次数（默认是每小时三次，突发五次）。使用此选项防止 Do 攻击。
- **表类型** — 默认表类型是 `filter`。其他类型的表是 `nat`（用于 IP 掩码）和 `mangle`（用于修改包）。要使用 `filter` `filter` 的表，必须添加 `-t table_type` 选项，其中 `table_type` 为 `nat` 或 `mangle`。

## 将 Red Hat Linux 配置为代理防火墙

我们已经看到 Red Hat Linux 可以作为过滤防火墙。添加 `socks5` 包后，Linux 可以被配置为代理防火墙。可以从 `ftp://ftp.redhat.com/pub/contrib/lib6/i386` 获取 `socks5` 的 RPM 版本。下载 `socks5` 包；然后像安装任何 RPM 包一样安装它。在当前目录下安装了 `socks5` 包后，输入：

```
# rpm -i socks5
```
...（注：此处后续文本存在大量重复和OCR错误，已根据指令要求清理并翻译核心逻辑部分）...

## 服务端口表示

可以使用 `/etc/services` 文件列出的服务名（如 `http` 或 `telnet`）来指定端口，或者使用相应的整数（如 `80` 或 `23`）。对于源主机（`source-host`）和源端口（`source-port`）条目，可以使用连字符 (`-`) 来匹配任何主机或端口。

# 封禁部分 (ban section)

`ban` 部分用于拒绝向特定主机和协议提供代理服务。`ban` 行以关键字开头，后跟跟源主机参数和源端口参数。

```bash
ban source-host source-port
```

# 表 14-7：有效的 ban 行

| 有效的 ban 行 | 描述 |
|---|---|
| `ban ratbert.glaci.com http` | 不允许主机 `ratbert` 访问该系统的 Web 服务器。 |
| `ban .glaci.com 1880` | `glaci.com` 域内的任何主机都被访问该系统的 1880 端口。 |
| `ban 199.170.177.22 tel` | 不允许 `199.170.177.22` 访问该系统的 `telnet` 服务。 |
| `ban 199.170.176. -` | `199.170.176.x` 子网上的任何主机都可以访问该系统的代理服务。 |
| `ban - -` | 不允许任何地方的主机访问该系统的任何代理服务。 |

# 验证部分 (authentication section)

身份验证行告诉 `socks5` 如何验证来自特定主机对于特定服务的连接。该行始终以 `auth` 关键字开头，后跟源主机、源端口以及要使用的身份验证类型。

```
auth source-host source-port auth-methods
```
有效的身份验证方法包括用户名/密码、kerberos、任意（`any`）或无（`none`）。使用单个字母（`u, k, -, 或 n`）表示每种认证类型。

- `u` — 用户名/密码
- `k` — Kerberos 5
- `-` — 任意认证方法
- `n` — 无认证

`auth-method` 参数可以是一个单一认证类型，也可以是多个逗号分隔的类型列表。如果您指定了多个类型，`socks5` 将按反序检查它们，因此列表中的最后一项是首选类型。

省略认证部分将导致所有允许的连接允许任何认证方法。如果您主要将 `socks` 用于出站代理服务（从您的网络到互联网），并根据地址和端口允许或拒绝连接，那么这样做是合适的。这是配置代理服务器最常见的方法。

## interfaces 部分

`interfaces` 部分仅在当您的 Linux 系统是双宿的（`dual-homed`）时才使用，这意味着它拥有多个网络接口。当您的 Linux 系统同时作为过滤防火墙（而不只是代理）或路由器时，通常会是这种情况。

`interface` 部分允许您为不同接口上的连接处理方式指定不同的规则。

## variables and flags 部分

`variables and flags` 部分用于调整 `socks5` 生成的日志级别和调试信息。该部分的条目始终以 `set` 关键字开头，随后是变量名及其要设置的值，如下所示：

```
set variable value
```

通常情况下，默认设置已经足够。阅读 `socks5` 在线帮助页的 Environment 部分（使用 `man socks5` 命令）可以了解更多关于设置变量和标志的信息。

## proxies 部分

使用 `proxies` 部分告诉 `socks` 如何以及在何时将连接转发到另一个代理服务器。这在普通的互联网使用中并不常见，但在您的内网中，可能会遇到这种有用的情况。

## access-control 部分

这可能是 `socks5.conf` 文件中最常用的部分。`access-control` 部分用于根据源机器或目的机器的主机地址或端口号来允许或拒绝代理连接。`access-control` 行始终以 `permit` 或 `deny` 关键字开头。关键字之后有六个必填参数和一个可选的第七个参数。

| `permit auth cmd src-host dest-host src-port dest-port [user-list]` |
| `deny auth cmd src-host dest-host src-port dest-port [user-list]` |

当客户端连接到代理服务器时，`socks5` 会扫描访问控制行列表，直到找到接入连接。如果某一行中的任何一个参数与连接不匹配，则该行不被视为匹配，`socks5` 将继续处理下一行。如果没有找到匹配的行，`socks5` 将拒绝该连接。如果找到匹配项，`socks5` 将查找该行的关键字，并根据情况允许或拒绝连接。

`auth` 参数用于描述连接允许的身份验证方法。请参阅身份验证部分的讨论以获取不同认证方案的详细信息。

`cmd` 参数用于告诉 `socks5` 在特定连接上可以执行什么种的操作。允许的值为：

- `c` — Connect (连接)
- `b` — Bind (绑定)
- `u` — UDP
- `p` — Ping
- `t` — Traceroute (路由追踪)
- `-` — All Commands (所有命令)

`src-host` 参数匹配连接的主机名或 IP 地址，而 `dest-host` 参数匹配其尝试连接的机器的主机名或地址。同样，`src-port` 匹配客户端连接的服务端口号，`dest-port` 匹配代理服务器将连接重定向到的端口号。

`user-list` 是一个可选参数，可以将连接限制为仅指定的用户。它是一个没有空格的逗号分隔用户名列表。

如您所见，其他部分的许多功能在 `access` 部分也可用。一个仅包含 `permit` 和 `deny` 访问行的 `socks5.conf` 文件并不罕见。以下是一个 `socks5.conf` 文件的示例。每个 `permit` 或 `deny` 之前都有一个解释其职的注释。

```
# 示例 socks5.conf 文件

# 允许 199.170.177.x 子网中的主机通过

# 代理端口 1880 访问网页 (http协议)

permit - - 199.170.177. - 1880 http
```

```
# 允许 glaci.com 域名内的任何主机

# 连接代理 telnet 服务。需要

# 用户名/密码认证才能访问。

permit u c .glaci.com - ptelnet telnet

# 拒绝所有其他连接

deny -
```

您可以在主 `socks` 目录下的 `examples` 目录中找到额外的 `socks5.conf` 示例。`socks5.conf` 的 `man` 页也包含有用信息。

## socks5 服务

通过安装 `socks5` RPM，您的 Red Hat Linux 系统将自动配置为启动 `socks5` 服务。当系统启动时，`/etc/init.d/socks5` 脚本将从相应的运行级别目录运行（针对系统状态 3、4 和 5）。如果您想立即启动该服务，请以 root 用户身份输入以下命令：

```
# /etc/init.d/socks5 start
```

这会导致 `socks5` 守护进程在您的计算机上运行，通过通过代理服务来处理入站请求。

## 使用 Tiger 进行安全审计

到此时，您已经观察到维护 Linux 盒箱的安全可能是一个耗时的过程。幸运的是，有一些工具可以自动化更多的例行任务。`Tiger` 就是其中一个工具。它执行安全审计，扫描计算机的错误配置或其他潜在问题。`Tiger` 还会执行以下检查：

- `cron` 条目
- 邮件别名
- `inetd` 条目
- `PATH` 变量
- `rohosts`
- `.netrc`

当运行 `Tiger` 时，它会将发现的所有弱点记录在文件中。然后您可以查看该文件并纠正任何安全问题。甚至可以配置 `Tiger` 定期运行并将结果通过电子邮件发送给您。随着新软件包的安装和用户的增加，即使是最安全的系统也会变得不稳定。`Tiger` 是由德克萨斯州大学创建的安全工具。可以在 `www.tamu.edu/network/public.html` 了解有关 TAMU 安全的信息。可以使用 `tar` 命令下载 `tiger-2.2.4` 包（如果有更高版本）：

```
# tar xzvf tiger-2.2.4
```

这将创建一个 `tiger-2.2.4` 目录并将 Tiger 文件提取到其中。使用 `cd` 命令进入 `tiger-2.2.4` 目录。现在通过输入 `make install` 命令将 Tiger 安装到相应的系统目录。

```
# cd tiger-2.2.4
# make install
```

这将创建 `/usr/local/tiger` 目录并将脚本和配置文件复制其中。接下来，您需要为 Tiger 审计系统创建临时目录。使用 `mkdir` 命令在 `/var/spool/` 目录下创建几个子目录：

```
# mkdir /var/spool/tiger
# mkdir /var/spool/tiger/work
# mkdir /var/spool/tiger/logs
```

接下来，您应该自定义位于 `/usr/local/tiger` 目录下的 `tigerrc` 文件。进入该目录并使用 `vi` 等编辑器加载 `tigerrc` 文件，如下：

```
# cd /usr/local/tiger
# vi tigerrc
```

然后您应该看到一个类似于下面的文件：

```
# Tiger 的 'rc' 文件。此文件经过了预处理，因此

# *只能*包含变量赋值和注释。

#

#-

#---------------------------------------

#

# 选择要执行的检查。对于不想执行的检查，

# 指定 'N'（大写）。

#

Tiger_Check_PASSWD=Y    # 快速

Tiger_Check_GROUP=Y     # 快速

Tiger_Check_ACCOUNTS=Y   # 随用户数量变化

Tiger_Check_RHOSTS=Y     # 随用户数量变化

Tiger_Check_NETRC=Y      # 随用户数量变化
```

## 第 14 章：计算机安全问题 535

```
Tiger Check_ALIASES=Y      # 快速

Tiger Check_CRON=Y         # 快速

Tiger Check_ANFTP=Y       # 快速

Tiger Check_EXPORTS=Y      # 快速

Tiger Check_INED=Y         # 可以更快，但也不错

Tiger Check_KNOWN=Y       # 快速

Tiger Check_PERMS=Y       # 可以更快，但也不错

Tiger Check_SIGNATURES=Y # 需要几分钟
```

一如既常的注释，`#` 所有行都以 `Tiger Check` 参数开头，该参数被设置为 `yes` 或 `no`（用大写的 `U` 或 `N` 表示）。每个参数后面都是一个注释，描述了运行该检查大约需要的时间。如要关闭特定测试，只需将 `Y` 更改为 `N`。在进行更改时保存并退出文件。

要运行 `tiger` 审计脚本，请在命令行提示符输入 `./tiger`：

```
./tiger
```

脚本在运行时会打印状态消息。最后一行将告诉您报告安全问题的文件名。

安全报告位于：
`/var/spool/logs/security.ratbert.glaci.com.01023-17:39:`

如所述，此文件位于 `/var/spool/tiger/logs` 目录。使用 `cd` 命令切换到该目录，然后使用 `more` 命令或编辑器查看内容。以下是典型的 `tiger` 安全报告的一部分：

```
# 正在执行 NFS 导出检查...

--FAIL--[ins006f] Directory /home 对所有人开放 R/W 权限。

--FAIL--[ins006f] Directory /var 对所有人开放 R/W 权限。

# 正在检查系统文件权限...

--WARN--[perm006w] /root/.bashrc 不应该有组读。

--WARN--[perm006w] /root/.bashrc 不应该有世界读。

--WARN--[perm006w] /root/.bashrc 不应该有组读。

--WARN--[perm006w] /root/.bashrc 不应该有世界读。

--FAIL--[perm007f] /etc/aliases 不应该有组读。

--FAIL--[perm007f] /etc/aliases 不应该有世界读。
```
