

# 3.8 玩转 Samba

## 3.8.13 身份验证方法（推断标题）

第三种方法是在 NT 域控制器上存储用户密码。这允许 Samba 服务器作为域中的一个常规文件服务器运行，并允许客户端登录到该域。这并不意味着 /etc/passwd 不再被使用，只是说用户账户（passwd 等）信息现在存储在了域控制器中，而不是存储在 smbpasswd 数据文件中。

```
[global]
security = domain
```

或者

```
[global]
security = server
```

使用 winbind 守护程序和 LDAP 将 Samba 服务器集成到你的环境中还有另外两种方式。我将在后面讨论这些内容。这些方法涉及替换 /etc/passwd 和 smbpasswd 文件，并对 nss switch 进行一些“取巧”的操作。

### 3.8.13.1 用户账户

每个连接到 Samba 服务器的用户都必须拥有一个用户账户。永远不要忘记，Samba 底层是一个 UNIX 系统，Linux 的访问规则为 Samba 提供了基础。提供用户账户有很多方式，包括 /etc/passwd、NIS、winbind 和 LDAP。

#### 3.8.13.1.1 本地身份验证

这是所有身份验证方法中最简单的一种。在我使用过的热门发行版中，都有一个默认的 Samba 配置文件，该配置使用 /etc/passwd 和 /etc/group 来跟踪用户账户。Windows 加密密码存储在 smbpasswd 文件中。在 Red Hat 中，这是 /etc/samba/smbpasswd。

每个需要访问 Samba 服务器的用户都需要在 /etc/passwd 中拥有一个账户，可以使用 `useradd [options] username` 添加。要创建必要的 smbpasswd 条目，需要运行以下命令：

```
smbpasswd -a username
```

一个例子如下：

```
useradd -g users -d /dev/null -s /dev/null -n -u 500 bob
smbpasswd -a bob
```

这是你可以创建的最安全的用户账户（我认为）。没有主目录，也没有默认 shell。该用户只能访问 SysAdmin 允许其访问的 Samba 共享。

如果你希望为用户设置主目录，请将 -d 参数更改为 /home/bob，并确保主目录的权限为 700。

在此配置中，你希望 nsswitch.conf 文件如下所示：

```
passwd: files
shadow: files
group: files
```

这样，用户账户就只能在本地机器上存储在一个地方。

如果你只有一台 Samba 服务器，那么设置用户账户的最安全方式就是这种方式。如果你有多个 Samba 服务器，或者需要将用户账户与其他机器同步，你可以使用这种方法，但作为系统管理员，你需要手动负责保持文件同步。在这里，你可以使用 rsync 等工具来保持多个 Samba 服务器账户的同步，但这可能会带来问题，并且在更新传播之前总会存在延迟，此外还有竞争条件问题。下文描述的方法将有助于缓解这一问题，并更容易地在多台机器之间共享一组通用的用户账户。

### 3.8.13.2 NIS 和 NIS+

NIS 和 NIS+ 是 UNIX 中跨多台机器同步账户的标准。NIS 使用一台指定的主服务器，网络上的其他主机从中拉取用户账户数据。它非常有效，但由于使用了不安全的协议（因为 RPC 运行在 UDP 上），所以存在安全问题。有一个网站展示了如何安全地运行 NIS+，以及如何让 NIS 安全运行。你可以在 www.linux-nis.org 找到它。

使用 NIS 时，你仍然需要一个 smbpasswd 文件。作为系统管理员，如果 NIS 映射文件中有很多用户，这可能是一项繁重的工作。如果你既是 NIS 管理员又是 Samba 管理员，请确保在添加和删除 NIS 映射文件中的用户时，也对 smbpasswd 文件做出相应的更改。如果你有多台机器，那么处理这些 smbpasswd 文件的工作量会很大。你可能希望使用 perl 脚本来查找 NIS 数据库和 smbpasswd 文件之间的差异，并自动处理它们。

由于 NIS 存在安全弱点，你需要使用 IP Chains 或 IP Tables 来定义网络中哪些计算机可以访问本地 portmap 守护程序。然而，由于 portmap (RPC) 使用 UDP，且容易被欺骗，这将只提供部分安全性。请仔细检查并双重检查，确保 portmap 守护程序被防火墙阻止，以防止该历史上存在漏洞的服务被利用。Portmap 运行在 TCP 和 UDP 端口 111 上。

### 3.8.13.3 winbind

winbind 守护程序是 2.2 系列中的新增强功能，并在 2.2.3 版本中成为标准分发的一部分。它允许 Windows 域控制器充当 /etc/passwd 和 /etc/group 文件的作用。

需要在 smb.conf 文件中放置一些指令才能启用此行为。此外，在启动 Samba 之前，你需要先启动 winbind 守护程序。

```
[global]
minidbind uid = 1000-24999
minidbind gid = 25000-29999
security = domain
password server = Primary Domain Controller, Backup Domain Controller(s)
```

这两个指令控制分配给域控制器上账户的 UID 和 GID。如果你试图将 NIS(+) 与 winbind 一起使用，请非常确保你为 winbind 指定的范围不会与 NIS 树中分配的 UID 和 GID 发生冲突。如果发生冲突，你将得到奇怪的结果并破坏你的安全模型。

如果你计划在使用 winbind 的同时在 Linux 机器上允许主目录，你需要在用户登录之前负责创建它们。全局部分中的 template homedir 指令提供了一种自动确定用户主目录位置的方法。此外，如果你计划使用 winbind，默认的登录 shell 是 /bin/false。如果你的 Windows 用户有任何理由通过 Telnet 或 SSH（SSH 更受青睐）登录到 Linux 机器，你需要更改 logon script 参数。

要启用 winbind 的使用，你需要修改 /etc/nsswitch.conf 文件，使其类似于以下内容：

```
passwd: files winbind
group: files winbind
```

在这个顺序下，本地用户将优先于域控制器上同名的用户。如果你希望域账户优先于本地账户，只需反转 files 和 winbind 的顺序即可。

关于在多台 Samba 服务器上运行 winbind 守护程序的另一个考虑因素是，如果你以完全相同的方式配置它们，域账户的 Linux UID 和 GID 几乎可以保证不匹配。示例：我们有两台 Samba 服务器，SAMBA1 和 SAMBA2。两台都运行 winbind 守护程序并针对 NTPDC 进行身份验证。Larry 在域控制器上有一个账户。在 SAMBA1 上，他的 Linux UID = 1000，而在 SAMBA2 上，他的 Linux UID = 1547。我还没有想出任何自动修复这个问题的方法。如果你试图将 winbind 与其他协议一起使用，特别是 NFS，这将是一个真正的问题，因为 NFS 要求不同 Linux 计算机之间的 UID 和 GID 同步以确保良好的文件质量。

使用 winbind 建立用户账户时的另一个问题也值得在此指出。进入 Windows 计算机比进入受保护的 Linux 计算机容易得多。在使用 Windows 机器为 Linux 机器提供用户账户时请考虑这一点。如果使用 winbind，我的建议是不为任何由域控制器提供的账户设置默认 shell。

Windows 域账户名称与其 UID 之间的关联存储在 /var/lock/samba（或你指定的其他位置）目录中。同样，Windows 域组、其 Linux GID 及其成员列表之间的关联也由数据库文件控制和缓存。缓存对于应对潜在的网络故障和微软传奇般的可靠性是必要的。

### 3.8.13.4 LDAP

LDAP 是另一种集中存储用户数据的方式。有几种可用的 LDAP 服务器，其中一种是 OpenLDAP (www.openldap.org)。Samba 可以使用 LDAP 服务器来存储通常存储在 smbpasswd 文件中的用户账户信息。当与来自 padl.com 的一些软件以及 nsswitch 文件的更改结合使用时，Linux 机器可以在整个企业中共享 UNIX UID 和 Windows SID。这通过扩展标准的 Posix LDAP 模式以包含 Windows 加密密码和 SID 来实现。

使用 LDAP 时，你希望使用以下选项：

```
[global]
security = user
ldap admin dn = ldapadmin # 或者你选择的任何值
ldap server = ldap.yourdomain # 或者 localhost 或 ...
password server = # 没有密码服务器
```

截至 2.2.3 版本，LDAP 接口被认为稳定且可安全使用。使用 LDAP 服务器的一个巨大优点是，使用 unbound 时，Linux UID 在机器之间将保持一致，使得可以在相同的群服务器上同时使用 Samba 和 NFS，并在所有服务器上执行统一的安全模型。当你超越当前的 Samba 服务器时，你可以简单地添加另一台并重新使用所有用户账户、UID 和 Windows 信息（SID、密码等）。

## 3.8.13.5 登录服务

Samba 具有存储用户配置文件和登录脚本的能力。这些是 DOS 格式的脚本和信息，如果允许不受信任的用户访问，可能会遭到破坏。想象一下，一个恶意用户向登录脚本中添加一条命令，以连接他的本地机器并安装恶意程序。请保持这些安全，并仅允许需要修改它们的人访问。至少将它们设置为除 root 外的其他用户只读。

# 3.8.14 Samba 管理安全

Swat 是一个很好的工具，但我从未找到使用它的理由。一旦 Samba 服务器设置好，它通常不需要系统管理员的持续关注。因此，没有必要让超级服务器在特定端口（通常是 901）上监听，以便系统管理员或黑客尝试入侵。

如果你决定使用 swat，请限制其实例的启动方式及其可访问的来源。并且，如果有人试图访问它，请通过记录日志来跟踪访问者的身份。一个典型的受保护的 xinetd 文件看起来像这样：

```
service swat {
port = 901
socket_type = stream
wait = no
only_from = 192.168.1.100
}
```

