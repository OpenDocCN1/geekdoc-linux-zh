
# 各种网络应用程序

由 Systems 开发的 RPC 为客户端服务器应用程序提供了一种非常通用的机制。基于 RPC 构建的重要应用程序有 NFS（网络文件系统）和 NIS（网络信息系统），它们都将在后面的章节介绍。

| 服务 | 端口 | 说明 |
| :--- | :--- | :--- |
| `nlockmgr` | 100021 | |
| `x25,inr` | 100022 | |
| `statmon` | 100023 | |
| `status` | 100024 | |
| `yupdated` | 100028 | `ypupdate` |
| `keyserv` | 100029 | `keyserver` |
| `bootparam` | 100026 | |
| `sunlink_mapper` | 100033 | |
| `tfsd` | 100037 | |
| `sed` | 100038 | |
| `nsemntd` | 100039 | |
| `showfhd` | 100043 | `showfh` |
| `ioadmd` | 100055 | `rpc.ioadmd` |
| `NETLicense` | 100062 | |
| `unsisamd` | 100065 | |
| `debug_svc` | 100066 | `dbsrv` |
| `ypxfrd` | 100069 | `rpc.ypxfrd` |
| `bugtraqd` | 100071 | |
| `kerbd` | 100078 | |
| `event` | 100101 | `na.event` # SunNet Manager |
| `logger` | 100102 | `na.logger` # SunNet Manager |
| `sync` | 100104 | `na.sync` |
| `hostperf` | 100107 | `na.hostperf` |
| `activity` | 100109 | `na.activity` # SunNet Manager |
| `hostmem` | 100112 | `na.hostmem` |
| `sample` | 100113 | `na.sample` |
| `x25` | 100114 | `na.x25` |
| `ping` | 100115 | `na.ping` |
| `rpcnfs` | 100116 | `na.rpcnfs` |
| `hostif` | 100117 | `na.hostif` |
| `etherif` | 100118 | `na.etherif` |
| `iproutes` | 100120 | `na.iproutes` |
| `layers` | 100121 | `na.layers` |
| `snmp` | 100122 | `na.snmp` `snmp-cmc` `snmp-synysoptics` `snmp-unisys` `snmp-utk` |
| `traffic` | 100123 | `na.traffic` |
| `nfs_acl` | 100227 | |
| `sadmin` | 100232 | |
| `isd` | 100300 | `rpc.nisd` |
| `nispassword` | 100303 | `rpc.nispasswd` |
| `ufsd` | 100233 | `ufsd` |
| `pcnfsd` | 150001 | |
| `amd` | 300019 | `amq` |
| `bwnfsd` | 545580417 | |
| `ypxfrd` | 600100069 | `freebsd-ypxfrd` |

## 各种网络应用

在 `TCP/IP` 网络中，`RPC` 的作者面临着如何将数字映射到通用网络服务的问题。他们选择让每个服务器为每个程序和每个版本提供一个 `TCP` 和 `UDP` 端口。通常情况下，`RPC` 应用在发送数据时会使用 `UDP`，只有当要传输的数据能够放入单个 `UDP` 数据报中时，才会回退到 `TCP`。

当然，客户端程序有一种方法可以发现哪个程序号映射到哪个端口。使用配置文件来实现这一点将太不灵活；`RPC` 应用不使用预留端口，无法保证原本打算供我们的数据库应用程序使用的端口没有被其他进程占用。`RPC` 应用会选取它们能获取的任何端口，并将其注册到所谓的 `portmapper` 守护进程（端口映射器）中。后者充当运行在其本地机器上的所有 `RPC` 服务器的服务代理：想要联系具有特定程序号服务的客户端将首先查询服务器主机上的 `portmapper`，由其返回该服务可以访问的 `TCP` 和 `UDP` 端口。

这种方法的特别缺点是，它引入了单点故障，正如 `inetd` 守护进程对标准的 Berkeley 服务所做的那样。然而更糟的是当 `portmapper` 崩溃时，所有的 `RPC` 端口信息都会丢失；这通常意味着你必须手动重启所有 `RPC` 服务器或重启整个机器。

`portmapper` 称为 `rpc.portmap`，位于 `/usr/sbin`。

> 注意
> 对于 Red Hat 6，`portmapper` 位于 `/sbin/portmap`。

## 配置 r 命令

有许多可以在远程主机上执行命令的命令。这些包括 `login`、`rsh`、`rcp` 和 `rcmd`。它们都会在远程主机上启动一个 shell 并允许用户执行命令。当然，客户端需要在执行命令的主机上拥有账户。因此，所有这些命令都会执行授权程序。通常，客户端会将用户的登录名告诉服务器，服务器请求一个按通常方式有效的密码。

```
# /etc/rpc - 各种基于 RPC 的服务

#

portmapper  100000 portmap sunrpc

rstat       100001 rstat stat svc rup perfmer

rusersd     100002 rusers

nfs         100003 nfsprog

ypserv      100004 ypprog

mountd      100005 mount showmount

ypbind      100007

walld 100008 rwall shutdown

ypasswdd 100009 ypasswd

bootparam 100026

yupdated 100028 updatedate
```
