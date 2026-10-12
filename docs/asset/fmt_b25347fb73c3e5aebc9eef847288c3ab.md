
# 第 17 章 将 SAMBA 4 作为与 AD 兼容的域控制器

为 `NOVEMBER.linuxaholics.com` 添加 DNS CNAME 记录 `604a4e5c-a897-45c9-b3ba-026b4d9c9b31._msdcs.linuxaholics.com`

所有其他 DNS 记录（如 `_ldap` SRV 记录）将在首次启动时通过 `samba_dnsupdate` 创建

在 `DC=DomainDnsZones,linuxaholics,DC=com` 分区中同步新的 DNS 记录 `[DC=DomainDnsZones,DC=linuxaholics,DC=com]` 对象 `[2/2]` 链接值 `[0/0]`

在 `DC=ForestDnsZones,linuxaholics,DC=com` 分区中同步新的 DNS 记录 `[DC=ForestDnsZones,DC=linuxaholics,DC=com]` 对象 `[2/2]` 链接值 `[0/0]`

向所有已同步的分区发送 `DsReplicaUpdateRefs`
设置 `isSynchronized` 和 `dsServiceName`
正在设置 secrets数据库

作为域控制器加入域 `LINUXAHOLICS` (SID `S-1-5-21-2526023654-1533215790-5003170`)

如果我们在 Windows 工作站上打开 Active Directory 用户和计算机控制台，并检查域控制器 OU 的内容，我们将看到两个 DC（图 17-17）。

## Active Directory 站点

我们正在操作的 Active Directory 域现在有两个 DC，它们都位于同一个本地子网中。但情况并非总是如此；我们可能在纽约有一个办公室，在洛杉矶也有一个办公室。在这种情况下，我们预计两个局域网的本地连接是快速且可靠的，但两个办公室之间的连接可能会明显慢得多。

对于这种场景，建议使用不同的 Active Directory 站点。在刚才提到的示例中，我们需要两个不同的站点，一个用于纽约，一个用于洛杉矶。同一站点内 DC 之间的通信将定期进行，不需要管理员配置任何内容，但...

图 17-17. 域控制器 OU

![](img/dfa44432604022575079471b648e25ca_471_0.png)

最后，如果我们想降级一个 DC，可以使用 `samba-tool domain demote` 命令。

两个站点之间的通信将由管理员根据任何情况的具体需求进行设置。

我们可以使用 `samba-tool sites create` 命令创建一个新站点。

```bash
root@mike ~# /usr/local/samba/bin/samba-tool sites create NYC

Site NYC created !
```

不过，使用 Active Directory 站点和服务控制台（Active Directory Sites and Services console）可能会更简单，该控制台包含了我们之前安装的 RSAT 工具。启动后，它将显示我们刚刚创建的 NYC 站点以及在未创建站点时默认使用的 `Default-First-Site-Name`（图 17-18）。

![](img/dfa44432604022575079471b648e25ca_472_0.png)

图 17-18. Active Directory 站点和服务控制台

在选择站点 `Sites` 时，我们可以右键点击新建站点 `New Site` 以打开新窗口（图 17-19）。

![](img/dfa44432604022575079471b648e25ca_473_0.png)

图 17-19. 创建新站点

创建新站点时，我们必须选择一个链接 `link`。正如我们之前提到的，站点之间的通信必须由管理员配置。这是通过站点链接对象 `site link objects` 实现的，外观类似于图 17-20 中的一个。

![](img/dfa44432604022575079471b648e25ca_474_0.png)

图 17-20. 站点链接

我们可以为连接分配一个成本 `cost`，并根据我们的需要增加或减少同步的频率。

在创建站点并将其与链接关联后，我们看到一条警告消息，告知我们使新站点完全运行所需的后续步骤（图 17-21）。

![](img/dfa44432604022575079471b648e25ca_475_0.png)

图 17-21. 站点已创建

该站点链接到 `Default-First-Site-Name` 站点，是因为我们在 Active Directory 站点和服务控制台中创建它时，将其与相应的链接对象关联起来了。在图 17-20 中可以看到这一点。然而，用 `samba-tool` 创建的 NYC 站点没有关联任何站点链接，因此我们需要在 Active Directory 站点和服务控制台中手动对其进行关联。

我们需要处理的下一个任务是为 LA 站点添加子网（NYC 站点也是如此）。我们可以使用 `samba-tool` 来完成。

```bash
root@mike ~# /usr/local/samba/bin/samba-tool sites subnet create 192.168.2.0/24

Subnet 192.168.2.0/24 created !
```

## 在 Samba 中管理 FSMOs

在 Samba 中，通过 `samba-tool fsmo` 命令来管理 FSMO。我们可以通过以下命令获取域内分配的 FSM 列表：
