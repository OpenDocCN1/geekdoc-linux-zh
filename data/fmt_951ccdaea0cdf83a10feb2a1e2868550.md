
此配置意味着名称服务查找首先在 `/etc/hosts` 中查找，然后通过 `bind`（名称服务器）执行名称查找。更改此行使其内容为：

```
hosts.nis.bind
```

此条目会导致主机名查找在查找 `/etc/hosts` 之后、在使用解析器库之前查询 `NIS`。

最后，查看 `/etc/nsswitch.conf`。默认情况下，Red Hat Enterprise Linux 配置为在请求认证和相关信息时执行 `NIS`（而非 `NIS+`）查找。在其他条目中，你应该能看到类似下面的行：

```
passwd files nis
shadow files nis
group  files nis
hosts  files nis
```

以井号符号 (`#`) 开头的条目是被注释的，可以忽略。如果你没有看到这些条目，请添加它们。

# 配置客户端启动文件

作为配置 `NIS` 服务器，你必须修改系统配置文件并确保守护进程在系统启动和停止时启动和停止。除了在 `/etc/sysconfig/network` 中设置 `NIS` 域名以及在 `/etc/yp.conf` 中设置服务器信息外，你必须使用服务配置工具（Service Configuration）确保客户端守护进程 `ybind` 在启动时启动。要做到这一点，请按照配置 `NIS` 服务器节中的说明启动 `serviceconf`，滚动到服务列表的底部，并在 `ybind` 服务旁边打一个勾（见图 12-9）。

选择 `File -> Save` 保存你的更改，然后选择 `File -> Exit` 关闭服务配置工具。最后，重启客户端系统并观察启动消息，以确保 `ybind` 实际启动。重启客户端系统后，`NIS` 客户端服务已处于运行。

![](img/8c5ce181a0f26bec693ad7f04bbfb6fe_373_0.png)

图 12-9：启动时启用 `NIS` 客户端

# NIS 客户端文件和命令

表 12-2 列出了关键的 `NIS` 客户端配置文件和命令，并简要描述了它们的用途。

## 表 12-2 NIS 客户端配置文件和命令

| 文件/命令 | 说明 |
| --- | --- |
| `ywhich` | 显示主 `NIS` 服务器的名称 |
| `ypcat` | 输出 `NIS` 数据库中的条目 |
| `yppasswd` | 修改 `NIS` 服务器上的用户密码和信息 |
| `yppoll` | 显示 `NIS` map 的服务器和版本号 |
| `ypmatch` | 输出 `NIS` map 中一个或多个条目的值 |
| `/etc/yp.conf` | 配置 `NIS` 客户端绑定 |
| `/etc/nsswitch.conf` | 配置系统名称数据库查找 |
| `/etc/host.conf` | 配置主机名解析 |

> 不带参数调用 `ypwhich` 会显示默认 `NIS` 服务器的名称。如果带有 `-d nisdomain` 选项调用，它将查询主 `NIS` 服务器以名为 `nisdomain` 的 `NIS` 域。你也可以指定 `ywhich hostname` 来查询名为 `hostname` 的机器上的 `NIS` 服务器（如果有）。`-x` 选项导致 `ywhich` 显示可用 `map` 的列表。

`ypcat` 命令允许你查看 `NIS` map 的内容。与 `ypwh` 命令一样，`ypcat` 显示来自默认服务器的 `map`，除非你使用 `-d nisdomain` 请求特定的 `NIS` 服务器。同样，要查看特定机器的 `map`，请使用 `-h hostname`，将 `hostname` 替换为你感兴趣的主机。假设例如，你想知道 `NIS` 服务器所知的主机列表。首先，使用 `ypwh -x` 命令查看 `luther` 上可用的别名列表。

`ypcat` 命令允许你查看 `NIS` map 的内容。与 `ypwh` 命令一样，除非你使用 `-d nisdomain` 请求特定的 `NIS` 服务器，否则 `ypcat` 显示来自默认服务器的 `map`。同样，要查看特定机器的 `map`，使用 `-h hostname`，将 `hostname` 替换为你感兴趣的主机。假设例如，你想知道 `NIS` 服务器所知的主机列表。首先，使用 `ypwh -x` 命令查看 `luther` 上可用的别名列表。

`passwd` 命令允许用户更改他们的密码。对于普通的 `passwd` 命令有什么问题吗？简单来说，`passwd` 命令仅影响客户端机器。事实上，如果你对通过 `NIS` 认证的用户使用 `passwd` 命令，密码更改将在整个网络中生效。

# 测试 NIS 配置

如果前面的配置步骤正常，你可以使用几个简单的命令来验证你的 `NIS` 配置。例如，在如本文所述的 `NIS` 客户端上执行以下命令，应该打印 `NIS` 服务器的信息：

```
# ypcat
nfs::65534:65534:Anonymous User:/var/lib/nfs:/sbin/nologin
bubba:$1F21EOTOW$32MNfbobZbGooS89mks/:500:500:Bubba:/home/bubba//bash
maryse:$1Tn06c*YLFSEARimThu/:501:501:Mary Sue
```

注意只显示由 `NIS` map 维护的密码。本地登录，仅存在客户端系统上的账户并不显示。这种分离是有意的——想象一下如果客户端机器上的 `root` 账户由你无法控制的 `NIS` 服务器控制会造成怎样的混乱！

你可以使用 `ymatch` 命令打印特定的信息。例如，为了打印任意密码条目，你可以使用格式为 `ymatch username passwd` 的 `ymatch` 命令，其中 `username` 是你感兴趣的用户。因此，要打印 `bubba` 的密码条目，使用：

```
# ymatch bubba passwd
bubba:$1F21EOTOW$32MNfbobZbGooS89mks/:500:500:Bubba:/home/bubba//bash
```

要显示 `maryse` 的组文件条目，同样，正确的命令是：

```
# ymatch maryse group
maryse::501:
```

要显示 `NIS` 服务器共享的 `map` 列表，使用 `ypcat -x` 命令，如下例：

```
# ypcat -x
Use "ethers*" for map "ethers.byname"
Use "aliases*" for map "mail.aliases"
Use "services*" for map "services.byname"
Use "protocols*" for map "protocols.bynumber"
Use "hosts*" for map "hosts.byname"
Use "networks*" for map "networks.byaddr"
Use "group*" for map "group.byname"
Use "passwd*" for map "passwd.byname"
```

# 关于 NIS+

网络信息服务增强（`NIS+`）是 `NIS` 的替代方案，它提供了更高的安全性、更具扩展性的命名模型，以及对大型（好吧，巨大的）`NIS` 安装的良好支持。安全性改进包括数据加密和安全 `RPC`。原始的 `NIS` 规范（通常称为传统 `NIS` 以区别于 `NIS+`）以明文形式在网络上传输信息，这使其成为数据包嗅探器和坏子的容易攻击目标。数据加密增加了窥探者的难度。`NIS+` 的命名模型有很大不同。新结构非常类似于 `LDAP`，围绕对象节点树组织，而不是一组平面的文本文件。遗憾的是，`NIS+` 的开发已经停止。因此，用于 Linux 的 `NIS+` 过于不成熟，尚无法用于生产环境。

# 配置示例 NIS 客户端

本小节说明了如何配置 `NIS` 客户端使用本章之前配置的 `NIS` 服务器提供的 `NIS`。与之前一样，`NIS` 域名为 `kurtwerks`，运行在服务器 `marta.kurtwerks.com` 上，`IP` 地址为 `192.168.0.1`。

1. 设置 `NIS` 域名：
   ```bash
   # nisdomainname kurtwerks
   # nisdomainname kurtwerks
   ```
2. 编辑 `/etc/yp.conf` 以指定默认 `NIS` 服务器。完成后的配置文件如下（不含注释）：
   ```text
   ypserver 192.168.0.4
   ```
3. 确保 `portmapper` 正在运行：
   ```bash
   # rpcinfo -p 192.168.0.4
   program vers proto port
   100000 2 tcp 111 portmapper
   100000 2 udp 111 portmapper
   ```
4. 启动主守护进程 `ypbind`：
   ```bash
   # /etc/rc.d/init.d/ypbind start
   Binding to the NIS domain: [ OK ]
   Listening for an NIS domain server.
   ```
