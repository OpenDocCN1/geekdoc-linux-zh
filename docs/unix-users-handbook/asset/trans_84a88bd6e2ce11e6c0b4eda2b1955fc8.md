

# 返回值

等同于：

```bash
login remotehost
```

如果在与远程主机的连接完成之前发生错误，`rlogin` 会向标准错误输出发送错误信息并返回非零值。否则，它返回零。

# 诊断

诊断信息可能来自本地主机和远程主机。在连接完全建立之前发生在本地主机的诊断信息会被写入标准错误输出。一旦连接建立，来自远程主机的任何错误信息都会像其他数据一样写入标准输出。

- `login/tcp: Unknown service`
  `rlogin` 无法在 `/etc/services` 数据库文件中找到列出的 `login` 服务。

- `There is no entry for you (user ID username) in /etc/passwd`
  `rlogin` 无法在密码文件中找到你的用户 ID。下一步：请联系你的系统管理员。

- `system call: ...`
  当 `rlogin` 尝试执行指定的系统调用时发生了错误。请参阅相应的手册条目以获取有关该错误的信息。

- `rcmd: connect <hostname>: Connection refused.`
  显示此通用错误消息的一个原因可能是远程系统的 `/etc/inetd.conf` 中缺少 `login` 的条目。该条目可能被删除或注释掉，以防止非安全访问。

Kerberos 特定错误列于 `sis(5)` 中。

# 示例

以远程主机 `remote` 上的相同用户登录：

```bash
login remote
```

将转义字符设置为 `\`，使用七位数据连接，并尝试以用户 `guest` 身份登录到主机 `remote`：

```bash
login remhost -e! -7 -l guest
```

假设你的系统管理员已在 `/usr/hosts` 中设置了链接，以下命令等同于上述命令：

```bash
remhost -e! -7 -l guest
```

# 警告

出于安全目的，`/etc/hosts.equiv` 和 `.rhosts` 文件应当存在，即使它们是空的。这些文件应当仅允许所有者读取和写入。更多信息请参阅 `hosts.equiv(4)`。

另外请注意，所有信息，包括密码，都是在两个主机之间以未加密的方式传输的。在 Kerberos V5 网络认证环境中，密码不会通过网络传输，因此它受到保护。

无论用户是否在本地系统上设置了 `stty brkint`，`rlogin` 都无法将 Break 键作为中断信号传输到远程系统。应使用通过命令 `stty intr c` 分配给 `SIGINT` 的键（请参阅 `stty(1)`）。

**作者**

`rlogin` 由加利福尼亚大学伯克利分校开发。

**文件**

- `$HOME/.rhosts`: 用户私有等价列表
- `/etc/hosts.equiv`: 等价主机列表
- `/usr/hosts/*`: 命令的 rhost 版本

**参见**

`csh(1)`, `ksh(1)`, `login(1)`, `remsh(1)`, `sh(1)`, `sh-bourne(1)`, `sh-posix(1)`, `stty(1)`, `telnet(1)`, `rlogind(1M)`, `hosts(4)`, `hosts.equiv(4)`, `inetd.conf(4)`, `services(4)`, `termio(7)`, `tty(7)`, `sis(5)`。

# route

`route - 操纵网络路由表。`

![](img/75f39fc91296b889c0653851accdfd46_586_0.png)

**名称**

`route - 手动操纵路由表`

**概要**

```bash
/usr/sbin/route [-f] [-n] [-p pmu] add [net|host] destination [netmask mask] gateway [count]
/usr/sbin/route [-f] [-n] delete [net|host] destination [netmask mask] gateway [count]
/usr/sbin/route -f [-n]
```

**描述**

`route` 命令手动操纵网络路由表。你必须具有适当的权限。

**子命令**

支持以下子命令。

- **add**
  将指定的主机或网络路由添加到网络路由表中。如果该路由已存在，则打印一条消息，且不做任何更改。

- **delete**
  从网络路由表中删除指定的主机或网络路由。

**选项和参数**

`route` 识别以下选项和参数。

- **-f**
  删除所有指定网关为远程主机的路由表条目。如果与某个子命令一起使用，则在该子命令处理之前删除这些条目。

- **-n**
  以 Internet 点分表示法打印所有主机和网络地址，默认网络地址除外，后者打印为 `default`。

- **-p pmu**
  为静态主机路由指定路径最大传输单元 (MTU) 值。允许的最小值为 68 字节；最大值为此路由出站接口的 MTU。此选项仅适用于添加主机路由。在所有其他情况下，此选项将被忽略，对系统没有影响。
  
  还可以通过将 `pmu` 指定为零来禁用主机路由的路径 MTU 发现。

- **net** 或 **host**
  目标地址的类型。如果省略此参数，则通过解释与 `destination` 关联的 Internet 地址来区分到特定主机的路由和到网络的路由。如果目标的本地地址部分为 `INADDR_ANY(0)`，则假定该路由指向网络；否则，将其视为指向主机的路由。

- **destination**
  数据包将被路由到的目标主机系统。`destination` 可以是以下之一：
  - 主机名（官方名称或别名，请参阅 `gethostbyname(3N)`）。
  - 网络名称（官方名称或别名，请参阅 `getnetbyname(3N)`）。
  - 点分表示法的 Internet 地址（请参阅 `inet(3N)`）。
  - 关键字 `default`，表示通配符网关路由（请参阅 `routing(7)`）。

- **netmask** **mask**
  将与 `destination` 进行按位与运算以得出数据包将被路由到的网络地址的掩码。`mask` 可以指定为以 `0x` 开头的单个十六进制数、点分表示法的 Internet 地址，或者列在网络表中的伪网络名称（请参阅 `networks(4)`）。掩码的长度（即从 32 位字段的最左侧位开始计算的连续 1 的数量）可以短于目标地址的默认网络掩码（请参阅 `routing(7)`）。如果未给出 `netmask` 选项，则路由的 `mask` 将根据与本地接口关联的网络掩码推导出来（请参阅 `ifconfig(1)`）。`mask` 将默认为具有相同网络地址的本地接口中最长的网络掩码。如果没有任何本地接口具有相同的网络地址，则 `mask` 将默认为 `destination` 的默认网络掩码。

- **gateway**
  到达目标所经过的网关。`gateway` 可以是以下之一：
  - 主机名（官方名称或别名，请参阅 `gethostbyname(3N)`）。
  - 点分表示法的 Internet 地址（请参阅 `inet(3N)`）。

- **count**
  一个整数，指示网关是远程主机还是本地主机。如果路由通过远程网关指向目标，则 `count` 应为大于 0 的数字。如果路由指向目标且网关是本地主机，则 `count` 应为 0。`count` 的默认值为零。如果 `count` 为负数，结果未定义。

- **操作**
    为目标或网关指定的所有符号名称首先使用 `gethostbyname()` 作为主机名查找；如果找不到主机名，则使用 `getnetbyname()` 将目标作为网络名称进行搜索。`destination` 和 `gateway` 可以是点分表示法（请参阅 `inet(3N)`）。
  
  如果未指定 `-o` 选项，则根据 `gethostbyaddr()` 和 `getnetbyaddr()` 分别返回的名称，以符号形式显示所有主机和网络地址，默认网络地址（打印为 `default`）和名称未知的地址除外。名称未知的地址以 Internet 点分表示法打印（请参阅 `inet(3N)`）。
  
  如果指定了 `-o` 选项，则除默认网络地址（打印为 `default`）外，所有主机和网络地址均以 Internet 点分表示法打印。
  
  如果指定了 `-f` 选项，`route` 将删除所有指定网关为远程主机的路由表条目。如果与上述子命令之一一起使用，则在该子命令处理之前删除这些条目。
  
  路径 MTU 发现是一种技术，用于发现可以在 Internet 路径上发送而不在中间路由器中引起数据报片段的最大 IP 数据报大小。本质上，利用此技术的源主机最初发送的数据报大小可达出站接口的尺寸。IP 数据报头中的不分片 (DF) 位被设置。当支持路径 MTU 发现的中间路由器收到一个过大而无法作为单件转发到下一跳路由器且 DF 位已设置的数据报时，路由器将丢弃该数据报并发送一个 ICMP 目标不可达消息，代码含义为“需要分片且 DF 已设置”。ICMP 消息还将包含下一跳路由器的 MTU。当源主机收到 ICMP 消息时，它将此路由的路径 MTU 减少为 ICMP 消息中的 MTU。通过此技术，源主机中此路径的主机路由将包含正确的 MTU。
  
  默认情况下，路径 MTU 发现对 TCP 套接字启用，对 UDP 套接字禁用。
  
  如果为主机路由指定了 `-p pmtu` 选项，则 `pmtu` 值被视为该主机路由的永久值。即使路径 MTU 发现过程后来发现此路由的较小 `pmtu`，主机路由中的 `pmtu` 字段也不会更新。一条带有新 `pmtu` 值的警告消息将被记录。
  
  `-p pmtu` 选项仅在你对网络环境足够了解并能为主机路由输入适当的 `pmtu` 时才有用。IP 将在将数据报发送到远程之前，将数据报分段为本地主机路由中指定的 `pmtu`。如果路由命令中指定的 `pmtu` 正确，它将避免路径中路由器的分段。
  
  可以使用 `ping` 来查找到远程主机路由的 `pmtu` 信息。路由表中的 `pmtu` 信息可以使用 `netstat -r` 命令显示（请参阅 `netstat(1)`）。

# 输出

- `add destination: gateway gateway`
  指定的路由正在被添加到表中。

- `delete destination: gateway gateway`
  指定的路由正在从表中删除。

# 标志

