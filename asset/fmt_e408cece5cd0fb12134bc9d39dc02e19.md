
# 域名解析

在 TCP/IP 网络上通信的计算机使用唯一的 IP 地址来标识自己。然而，这种标识方案对于人类使用来说是不实际的，因为 IP 地址很难记忆。因此，网络上的每台计算机都通过一个人类理解的名称来标识，例如“Accounting1”或“Reception”。因为网络上的每台计算机被称为主机（host），所以分配给个体的名称就是其主机名。

对于需要在 Internet 上接入的计算机，很少使用简单的主机名。相反，根据称为域名系统空间（DNS）的分层命名方案，它们被赋予一个称为完全限定域名名称（FQDN）的主机名。域名空间的顶部是根域名（root domain），它实际上只是分支树形结构的一个理论起点。根域名之下是顶级域名（top-level domains），用于识别网络所在的组织类型。例如，`com` 域主要用于业务、商业或网络。每个顶级域名下面都存在二级域名，用于识别组织的名称，而简单的主机名则列在二级域名之下。图 12-6 显示了域名空间的部分内容。

> 为了简单起见，FQDN 通常被称为主机名。

因此，图 12-6 所示的主机计算机的 FQDN 为 `www.linux.org`。

主机名 `www`（万维网）经常用于托管 Web 页的服务器。

二级域名必须向 ISP 购买并注册，才能被 Internet 上的其他计算机识别。你可以使用 `whois` 命令获取域名空间内任何域名的注册信息。例如，要获取关于维护 `linux.org` 的组织的信息，你可以使用以下命令：

```bash
[server~1] # _

[root]@server1 ~]# whois linux.org
[querying.publicinterestregistry.net]
[whois.publicinterestregistry.net]
Domain ID: D2338975-LROR
Domain Name: LINUX.ORG
Created On: 10-May-1994 04:00:00
Last Updated: 19-Oct-2004 02:24:17
Expiration Date: 11-May-2013 04:00:00
Sponsoring Registrar: Network Solutions LLC (R63-LROR)
Status: CLIENT TRANSFER PROHIBITED
Registrant ID: 222756688-NSI
Registrant Name: Linux Online, Inc
Registrant Organization: Linux Online, Inc
Registrant Street1: 59 E. River, #2
Registrant Street2:
Registrant City: Ogdensburg
Registrant State/Province: NY
Registrant Postal Code: 13669
Registrant Country: US
Registrant Phone: +1.31533931202
Registrant Phone Ext.:
Registrant FAX:
Registrant FAX Ext.:
Registrant Email: mmclagan@INLOGIC.COM
Admin ID: 15412138-NSI
Admin Name: Michael McLagan
Admin Street1: 59 RIVER ST # 2
Admin Street2:
Admin Street3:
Admin City: OGDENBURG
Admin State/Province: NY
Admin Postal Code: 13669-1307
Admin Country: US
Admin Phone: +1.315939202
Admin Phone Ext:
Admin FAX: +1.231231234
Admin Ext:
Admin Email: mmclagan@INVLOGIC.COM
Tech ID: 15412138-NSI
Tech Name: Michael McLagan
Tech Street1: 59 RIVER ST # 2
Tech Street2:
Tech Street3:
Tech City: OGDENBURG
Tech State/Province: NY
Tech Portal Code: 13669-1307
Tech Country: US
Tech Phone: +1.315939202
Tech Phone Ext:
Tech FAX: +1.3159392134
Tech Ext:
Tech Email: mmclagan@INVLOGIC.COM
Name Server: NS.INVLOGIC.COM
Name Server: NS0.AIT.NET
DNSSEC: Unsigned
[root@server1 ~]#
```

**图 12-6** 域名空间

来源：Course Technology/Cengage Learning

© Cengage Learning. 版权所有。未经明确许可，不得分发。

你可以使用 `hostname` 命令查看 Linux 计算机的主机名，输出所示：

```bash
[root@server1 ~]# hostname
server1.class.com
[root@server1 ~]# hostname computer1.sampledomain.com
[root@server1 ~]# hostname computer1.sampledomain.com
[root@server1 ~]#
```

要在每次启动时配置上述的主机名，只需修改 `/etc/sysconfig/network` 文件中的 `HOSTNAME` 行，例如所示：

```bash
[root@server1 ~]# cat /etc/sysconfig/network
NETWORK=yes
HOSTNAME=server1.class.com
[root@server1 ~]#
```

在安装时规划合适的主机名是良好的，因为许多应用程序会记录此主机名。如果你在安装后更改了主机名，可能需要更改这些文件。

虽然在指定网络计算机时主机名更容易使用，但 TCP/IP 无法使用它们来标识计算机。因此，你必须将主机名映射到相应的 IP 地址，以便网络应用程序获取主机的正确 IP 地址。将主机名映射到 IP 地址的最简单方法是将条目放入 `/etc/hosts` 文件，如下所示：

```bash
[server1]# cat /etc/hosts
127.0.0.1 server1.class.com localhost.localdomain
0.0.0.2 ftp.sampledomain.com
192.168.0.1
[server1]#
```

上述输出中的条目通过主机名 `server1`、`server1.class.com`、`localhost` 和 `localhost.localdomain` 标识本地计算机 `127.0.0.1`。同样，你可以使用主机名 `ftp.sampledomain.com` 解析 IP 地址为 `0.0.0.2` 的计算机。此外，IP 地址为 `192.168.0.1` 的计算机可以使用名称。

> 你也可以通过网络配置工具中的 Hosts 标签页编辑 `/etc/hosts` 文件。

你可以使用网络信息服务（NIS）在多个计算机之间共享 `/etc/hosts` 配置。NIS 在第 13 章中讨论。

由于列出 Internet 上所有的主机非常繁琐，应用程序可以使用 DNS 服务器获取特定 FQDN 的 IP 地址。要配置系统将名称解析为 IP 地址，只需在 `/etc/resolv.conf` 文件中指定 DNS 服务器的 IP 地址。如果第一个 DNS 服务器不可用，系统将尝试连接第二个 DNS 服务器，然后是列出的第三个 DNS 服务器。示例所示：

```bash
[server1]# cat /etc/resolv.conf
nameserver 209.122.97.2
nameserver 192.168.0.144
nameserver 6.0.4.21
[server1]#
```
