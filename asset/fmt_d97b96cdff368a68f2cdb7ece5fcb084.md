
## 资源代理列表

### 通用

- `Postfix`
- `RabbitMQ`
- `Rsyslog`
- `Squid`
- `Squid`
- `Exports`
- `Ipc`
- `Systemd`
- `Pacemaker`
- `Corosync`
- `SBD`
- `Mail`
- `Delay`
- `ClusterMon`
- `Systemd`

### 锁定与保留 (LOCKING & RESERV)

- `Control`: 文件系统的分布式管理器
- `Clv`: `clv` 守护进程（集群逻辑卷管理器）
- `Lvmlock`: `lvmlock` 代理管理 `lvmlock` 守护进程
- `Multipath`: `mpath` 设备上的 SCSI 持久保留
- `Sg_persist`: SCSI3 的从资源

### 网络 (NETWORKING)

- `Route`: 网络路由
- `Iface-bridge`: Bridge 网络接口
- `Iface-vlan`: VLAN 网络接口
- `IPv`: 虚拟 IPv4 和 IPv6
- `Ipsec`: 用于 VIP 的 ipsec 隧道
- `IPscaddr`: 首源地址修改
- `IPv6`: IPv6 地址
- `Contracked`: `contracked` 实例
- `SendARP`: 为 IP 地址发送免费 ARP
- `VIParp`: 通过 RIP2 实现虚拟 IP 地址

### 虚拟化 (VIRTUALIZATION)

- `VirtualDomain`: 通过 `libvirt` 管理虚拟域（仅限虚拟机）

### 容器 (CONTAINERS)

- `Lcc`: 允许 `LXC` 被集群管理

`anything` | `generic` | 管理任何内容的通用代理
`Dummy` | 测试占位资源代理（RA 编写者模板）
`AudibleAlarm` | 间隔性听性蜂声
`Stateful` | 有状态的支持两种状态的示例代理
`WinPopup` | 向主机发送通知消息（弹出窗口）

## 服务

`asterisk` | `asterisk` PBX
`CTDB` | 集群化 samba（用于嵌套集群化底层）
`dnsupdate` | 通过动态 DNS 更新接管 IP
`nfs` | 实例
`galera` | `galera` 实例
`galera` | `galera` 仲裁器实例
`JBoss` | JBoss 应用服务
`jira` | JRA 服务器实例
`kamailio` | `kamailio` SIP 代理/注册表实例
`jboss` | `adb`
`MariaDB` | 主实例
`nacios` | `nagios`
`ovismon` | 复制资源以监控不同节点上的网络绑定
`ppagant` | `ppagant` 实例
`pound` | `pound` 反向代理负载均衡服务
`proftpd` | `proftpd` 实例
`Pure-FTPD` | `pure-ftpd` 实例
`redis` | `redis` 服务器（支持主从复制）
`syslog` | `syslog-syslog` 实例
`tomcat` | `tomcat` servlet 环境实例
`varnish` | `varnish` 实例

## 存储

`AoTarget` | 以太网传输 ATA

## 网络

`IPaddr` | 虚拟 IPv4 地址
`ocf:pacemaker:maker` | CIB 中记录主机可以连接的节点数量
`portblock` | 临时阻塞/解锁对 tcp/udp 端口的访问

## OPENSTACK

`openstack-cinder-volume` | 将 `cinder` 挂载到实例（os-info-<->)
`openstack-floating-ip` | 将浮动 IP 从一个实例移动到另一个

## 虚拟化

`Xen` | `xen` 非特权域

## 注册 (CIB)

`lxd-info` | 在 CIB 中包含运行中的 `lxd` 信息
`machine-info` | 在 CIB 中记录各种属性
`NodeUtilization` | 将 cpu / 主机内存 / 虚拟机等...写入 CIB
`openstack-info` | 在 CIB 中记录节点属性
`SysInfo` | 将值属性写入 CIB
`SystemHealth` | 使用 IPMI 监控系统健康状况
`attribute` | 启动时不是单向的，反之亦然

## 资源代理：宇宙社区

此列表中的代理仅由上游社区支持。针对这些代理提交的所有 bug 如果合理，将转发到上游（受影响版本接近上游）。

| 资源代理 | 资源代理描述 |

### 服务

`SphinxSearchDaemon` | `sphinx` 搜索守护进程
`Xinetd` | 启动/停止 经由 `xinetd` 管理的服务
`zab-bixserver` | `zabbix` 服务实例

### 存储

`o2cb` | oracle 集群文件系统用户守护进程（oracle）
`sfex` | 使用 SF-EX 访问共享存储

### 虚拟化

`aliyum-vpc-move-ip` 在 `aliyum ecs` (阿里云) 的 vpc 内移动 ip
`awseip` | 管理弹性 IP 地址 (aws)
`awsvip` | 管理 aws 次级 ip 地址 (aws)
`aws-vpc-move-ip` 在 `ec2` (aws) 的 vpc 内移动 ip
`aws-vpc-route53` | 更新 `ec2` 的 vpc 记录 (aws)
`azure-monitor` | 虚拟机 的计划事件监控 (azure)
`azure-lb` | 回答负载均衡器健康探针请求 (azure)
`gcp-vpc-move-ip` | GCP VPC 中的浮动地址 (google)
`ManageVE` | 开放虚拟环境 (virtuoso)
`minio` | `mini` 服务器实例
`podman` | 创建/启动 `podman` 容器
`rkt` | 根据提供的镜像创建/启动容器

### 容器

`docker` | `docker` 容器资源代理

## 资源代理：不支持的

此列表中的代理在 Ubuntu 中不被支持，并可能在未来的 Ubuntu HA 版本中移除。

| 资源代理 | 资源代理描述 |

|---|---|

不支持的

`db2` | 管理 IBM DB2 数据库 (IBM)
`eDir88` | Novell eDirectory 服务器实例 (nov)
`ICP` | ICP 顶点集群主机驱动程序 (intel)
`ids` | IBM informix 动态服务器 (IDS) (IBM)
`SAP-Database` | (任何类型）SAP 数据库实例 (SAP)
`Instance` | SAP 应用服务器实例 (SAP)
`ServeAID` | 启用的共享 RAID 合并组 (IBM)
`ManageRAID` | `raid-设备 (/etc/code)/IBM-HB-AGE (mare)`
`oraism` | `oracle` 资源代理使用 os 作为磁盘组 (oracle)
`oracle` | `oracle` 实例 (oracle)
`oracle` | `oracle` TNS 监听器 (oracle)
`sybaseASE` | `sybase ASE` 故障转移实例 (Sybase)
`ivdo-vol` | https://bugs.launchpad.net/+ubuntu/+bug/169825
`WAS` | `webphere` 应用服务器实例 (IBM)

## 资源代理：已弃用

此列表中的代理在 Ubuntu 或上游均不被支持（由于被其他代理所取代），并可能在未来的 Ubuntu HA 版本中移除。

| 资源代理 | 资源代理描述 |

|---|---|

已弃用

`Evms` | 集群虚拟机管理 (evms 不维护)
`EvmsCSC` | 集群虚拟机管理 (evms 不维护)
`LinuxSCSI` | 通过内核 scsi 热插拔启用 scsi 设备
`scsi2reservation` | SCSI2 预留代理（依赖 `scsi_reserve`）
`ocf|heartbeat:ping` | 监控与特定主机的连接性
`ocf|pacemaker:ping` | 已被 `pacemaker:ping` 替换（此已失效）
`vmware` | 控制 `vmare` 服务器 2.0 虚拟机 (2009)

## Ubuntu HA - Pacemaker 代理支持

在 Ubuntu 开发者之间的讨论后，决定 Ubuntu 项目应专注于将所有现有 Pacemaker 代理划分为不同的类别：

- 围栏代理 (Fence Agents): 宇宙
- 围栏代理：宇宙-社区
- 围栏代理：不支持
- 围栏代理：弃用

注意：有一个计划将围栏代理拆分为不同的包。

| 围栏代理 | 围栏代理描述 | 额外描述 |

|---|---|---|

宇宙
