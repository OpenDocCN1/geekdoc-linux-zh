
无论你是否需要，集群软件都会创建一个默认的集群别名（cluster alias）。客户端节点可以使用默认集群别名来访问集群内的可用服务。听起来很棒，不是吗？如果真的这么棒，我们为什么还需要创建额外的集群别名呢？

如果你的配置包含某些资源涉及集群成员子集的应用程序，那么设置一个由选定的集群成员“加入”的别名是有意义的。或者，如果你的客户端期望将集群作为 NFS 服务器，但并非所有集群成员访问 NFS 服务器的性能都相同，设置另一个别名可能是最好的。此别名可以包含选定的成员，或者包含所有成员但具有不同的选择权重（`selwx`）值，以帮助负载均衡或决定哪些成员用于大部分 NFS 活动。请注意，新别名中的成员是为了以防首选成员宕机时可以使用用。慢速访问总比无法访问要好。

额外的别名由 `clumagr` 创建和管理。请注意`/etc/clua_alias.config` 文件的内容将是一系列（至少一个）`clumagr` 命令。创建默认别名的条目在下一节显示。以下示例为发布集群成员创建了一个名为“join”的别名，并在时对别名进行路由。此命令必须在其他集群成员上执行，以便它们也能识别该别名。如节 16.5.1.4 所示，`clumagr -s all` 命令提供了集群别名的统计和状态报告。

## 16.5.1.6 使别名持久化

要使别名持久化的任何更改，都必须在 `/etc/clu_alias.config` 文件中添加条目。该文件是一个 CDSL（集群定义列表），允许每个成员管理自己的别名组。该文件的内容将是 `clumagr` 命令。以下示例显示了一个定义了默认集群别名的 `/etc/clu_alias.config` 文件。

```
# cat /etc/clu_alias.config
/usr/bin/clumagr -a sel=3,selp=1,join,alias=DEFAULTALIAS
```

该文件在启动时从 `/sbin/init.d/clu_alias` 脚本以脚本的形式执行。以下是 `/sbin/init.d/clu_alias` 脚本的片段。

`test -s -s` 语法用于检查文件是否存在且大小非零：

```
if test -s "/etc/clu_alias.config"
then
  /etc/clu_alias.config
fi
```

更多信息，请参阅 `clu_alias.config(4)` 参考页面。

## 16.5.1.7 消除别名

如果集群成员需要更改其相对于之前“加入”的别名的职责，该成员可以“离开”该别名。这将消除该成员通过别名提供客户端请求服务的职责，但不会消除别名路由职责。以下示例显示了集群成员离开别名。

```
[molari]
# cluamgr -s clua_den | grep -E "^Status|^[Mm]ember|^$\$ | uniq
Status of Cluster Alias: clua_den
Member Attributes:
memberid: 1, selw=1, selp=1, rpi=1 flags=11<JOINED, ENABLE>
memberid: 2, selw=1, selp=1, rpi=1 flags=11<JOINED, ENABLE>
```

接下来的命令显示集群成员 molari 请求“离开”集群别名 `clua_den`。

```
[molari]
# cluamgr -a alias=clua_den,leave
```

```
[molari]
# cluamgr -s clua_den | grep -E "^Status|^[Mm]ember|^$\$ | uniq
Status of Cluster Alias: clua_den
Member Attributes:
memberid: 1, selw=1, selp=1, rpi=1 flags=11<JOINED, ENABLE>
memberid: 2, selw=1, selp=1, rpi=1 flags=10<ENABLED>
```

以下 `rsh` 命令显示 sheridan “离开”了 `clua_den` 集群别名。

```
# rsh sheridan /usr/sbin/cluamgr -a alias=clua_den,leave
```

注意别名仍然存在，且两个成员都是别名的潜在路由者。为了停止路由，必须执行 `clumagr -r stop` 命令（这会停止所有集群别名的路由），或者必须将 `rpi` 属性设置为 0（这会停止单个别名的路由）。

```
# cluamgr -s clua_den | grep -E "^Status|^[Mm]ember|^$\$ | uniq
Status of Cluster Alias: clua_den
Member Attributes:
memberid: 1, selw=1, selp=1, rpi=1 flags=10<ENABLED>
memberid: 2, selw=1, selp=1, rpi=1 flags=10<ENABLED>
```

根据我们的测试，将特定别名在所有成员上的 `rpri` 值设置为 0（然后使用“`cluamgr -r start`”命令重启路由活动）将导致集群没有指定的全局代理 ARP 主节点。这与 `clu_alias.config` 的以下片段相反。

值 0 是一个特殊情况。如果 `rpri=0`，系统将不会进行路由。

## 16.5.1.8 别名的动态路由

根据我们的测试，将特定别名在所有成员上的 `rpri` 值设置为 0（然后使用“`cluamgr -r start`”命令重启路由活动）将导致集群没有指定的全局代理 ARP 主节点。这与 `clu_alias.config` 的以下片段相反。

值 0 是一个特殊情况。如果 `rpri=0`，系统将不会进行路由。

## 16.5.1.9 动态路由守护进程

根据我们的测试，将特定别名在所有成员上的 `rpri` 值设置为 0（然后使用“`cluamgr -r start`”命令重启路由活动）将导致集群没有指定的全局代理 ARP 主节点。这与 `clu_alias.config` 的以下片段相反。

## 16.5.1.10 `gated.conf` 文件

当在成员上启动集群路由（或使用“`clamagr -r start`”重启）时，`gated` 进程将使用集群版本的 `gated.conf` (`/etc/gated.conf`) 启动，该文件包含描述通往集群别名主机路由的 RIP 信息。在集群成员上传递给 `gated` 的命令行。

```
# ps -A | grep gated | grep -v grep
105031 ?? S 0:00.13 /usr/sbin/gated -f /etc/gated.conf2
```
