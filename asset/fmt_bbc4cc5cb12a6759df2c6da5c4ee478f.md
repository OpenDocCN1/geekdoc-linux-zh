
`-m` 标志告诉 `ypinit` 它正在配置一个主服务器；它会提示你输入一个从用服务器列表。一旦主服务器启动运行，你就应该通过运行带有 `-s`（从用）标志的 `ypinit` 来提升每个从服务器的状态：

```bash
# cd /var/yp
# ypinit -s master  * 参数是主机的主机名。
# ypserv
```

`ypinit` 会创建主数据的本地副本；只要域数据文件存在，就足以服务器知道它应该提供该域的服务。

在每个从服务器上，你应该设置条目从主服务器拉取映射（maps）的最新副本。命令 `ypmap`（其中 `map` 是如 `passwd.byuid` 类的名称）从主服务器传输指定的映射。你必须为每个映射运行该命令。映射的变化速率可能不同，如果网络带宽非常珍贵，你可能比其他映射更频繁地传输它们。在某些情况下，每天传输一两次所有映射（可能在深夜）就足够了。以下脚本传输每一个映射：

```bash
#!/bin/sh
mydomain=`domainname`
cd /var/yp/$mydomain # NIS 目录
for map in $(ls /bin); do
  /usr/lib/yp/ypxr $map
done
```

`/usr/lib/yp` 中还有预制的脚本用于以各种频率传输 NIS 映射（`ypxr_1day`、`ypxr_2day` 和 `ypxr_1perhour`）。

如果用户想用 `passwd` 更改密码，你必须在主 NIS 服务器上运行 `yppasswd` 守护进程。该服务器的 Linux 版本已知经常崩溃，因此务必验证 `yppasswd` 守护进程是否正常工作。

## 配置 NIS 客户端

设置服务器后，你必须通知每台客户端机器它是新域的成员。域的服务器通常也是客户端。

`domainname` 命令设置机器的 NIS 域。它通常在启动时从其中一个启动脚本执行。配置此项所需的精确轮廓因发行版而异；文中提供了特定发行版的细节。

每个客户端必须至少有一个最小版本的 `passwd`、`group` 和 `hosts` 文件。当 NIS 服务器可用时，需要 `passwd` 和 `group` 来允许 `root` 登录。它们应该包含标准系统账户和组：`root`、`bin`、

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_540_0.png)

《Linux 管理手册》

`daemon` 等。`hosts` 文件（或 DNS）必须存在，以回答 NIS 运行时发生的启动查询。

在 Red Hat 下，你通过在 `/etc/sysconfig/network` 中设置变量 `NISDOMAIN` 来设置 NIS 域名。`ybind`、`pserv` 和 `ypassswdd` 通过 `chkconfig` 启用或禁用；例如：

```bash
# chkconfig ybind
```

在 SUSE 下，通过编辑 `rc.config` 开启 `ybind`。将 `Y_DOMAINNAME` 设置为你的域名，并将 `START_YPBIND` 设置为 'yes'。你也可以（可选）使用 `NIS_SERVER` 变量列出服务器列表。运行 NIS 服务器 (`pserv`) 需要将 `START_YPSERVER` 设置为 'yes'；其他服务器参数在文件中设置：

```text
/etc/rc.config/dpserv.rc.config
```

Debian 将 NIS 域名存储在 `/etc/defaultdomain`。其余配置信息来自 `/etc/ypbind.config`。Debian 自动存储 `ypbind`。你可以通过更改 `/etc/init.d/nis` 文件中的行 `NISSERVER=false` 来启用它。

## 18.4 NIS+: NIS 的延续

NIS+，又被称为“加强版的 NIS”，旨在纠正 NIS 的缺陷并引入自身的特性。它处理大型机器网络。它内置安全功能。它允许从网络任何地方管理多个域：它高效地传输更新。它是一个分布式数据库；它同步，在单带内。

Sun 在 90 年代初发布了 NIS+。尽管两者有相似之处，NIS 和 NIS+ 之间并没有太大关系。NIS+ 比 NIS 复杂得多，并且没有获得同等的支持。Sun 已宣布停止支持 NIS+，我们预计它将逐渐消失。

尽管 Linux 可以作为 NIS 客户端，但没有 NIS 服务器，也没有人实现它。作为 Linux 管理员，除非你将系统集成到已经标准化 NIS+ 的环境中，否则你不需要处理 NIS+。在理论上，它是完美的；在实践中，它相当笨拙，脱离了现实。从客户端的角度来看，NIS+ 与 NIS 大多相同。大多数数据通过相同的库程序访问，而域、权限和搜索路径最终归于平直文件。它没有很好地集成到发行版中。Red Hat 包含了 NIS+ 所需的基础软件，但没有文档。你将不得不编写脚本来启动守护进程。NIS HOWTO 中包含一些说明（参见 www.linuxdoc.org）；它们太长了，无法在书中复制。

在 SuSE 下使用 NIS+ 的指南可以在此处找到：

```
http://www.suse.de/~kuk/nisplus/SuSE.html
```

Debian 的 NIS+ 软件包可以从此处获取：

```
http://www.debian.org
```
