
## 问题 4

- A. `/etc/default/path`
- B. `/etc/inet/path`
- C. `/default`
- D. `init`

## 问题 5

+ 无磁盘客户端启动时，它能向服务器提供的唯一信息是什么？

- A. 主机名
- B. IP 地址
- C. 以太网地址
- D. 系统

## 问题 6

+ 哪个文件指定规范名称？

- A. `/etc/inet/hosts`
- B. `/etc/networks`
- C. `hostname`
- D. `system`

## 问题 7

+ 连接远程主机时，收到消息：目标不可达。哪个协议引发了此错误？

- A. IP
- B. ARP
- C. TCP
- D. ICMP

## 问题 8

+ 要确定系统是否使用 DNS 进行解析，你需要查看哪个文件？

- A. `/etc/inet/hosts`
- B. `/resolv.conf`
- C. `/etc/nsswitch.conf`
- D. `named.conf`

## 问题 9

+ 哪种 IEEE 标准用于以太网？

- A. `802.3`
- B. `802.4`
- C. `802.5`
- D. `802.2`

## 问题 10

+ 以下哪些是 UDP 的特征？选择 2。

- A. UDP 开销低。
- B. UDP 开销大。
- C. UDP 是无连接、无状态且不可靠的协议。
- D. UDP 是面向连接、有状态且可靠的协议。
- E. UDP 需要接收方的确认消息。

## 问题 11

+ 哪个命令允许连续查看路由表的变化？

- A. `route monitor`
- B. `route flush`
- C. `netstat -r`
- D. `netstat -i`

## 问题 12

| B 类网络的默认子网掩码是什么？ |

| A. `255.0.0.0` |
| B. `255.255.0.0` |
| C. `255.255.255.0` |
| D. `255.255.255.240` |

## 问题 13

+ 配置 DHCP 服务器时，你决定数据存储选项将是 SUNnisplus。对于此选项，位置将是以下哪项？

- A. 绝对路径
- B. 相对路径
- C. 根目录 (`/`)
- D. NIS+ 表名

## 问题 14

+ 点点协议（PPP）运行在 TCP/IP 模型的哪一层？

- A. 应用层
- B. 网络层
- C. 网络接口层
- D. 传输层

## 问题 15

+ `pntadm` 工具用于管理 DHCP 网络表。使用 `pntadm` 可以实现哪些操作？选择 2。

- A. 添加 DHCP 管理下的网络。
- B. 删除 DHCP 管理下的网络。
- C. 为 DHCP 管理下的网络创建别名。
- D. 修改 DHCP 数据存储类型。

## 问题 16

- 以下哪些项是许多网络应用需要时间同步才能正常工作的原因？选择 2 项。

- A. 许多加密算法使用时间作为加密密钥的一部分。
- B. DHCP 客户端在请求租约时必须与 DHCP 服务器进行时间同步。
- C. 以太网 II 帧使用了时间戳，要求发送者进行时间同步。
- D. 文件和目录在创建或修改时，由应用程序打上时间戳。

## 问题 17

- 应该使用哪两个工具来管理 `dhcptab` 表？选择 2 项。

- A. `dhcppmgr`
- B. `pntadm`
- C. `dhcpconfig`
- D. `dhtadm`

## 问题 18

- 你有一个系统，包含主网络接口 `hme0` 和一个配置了 IP 地址 `192.168.7.4` 的逻辑网络接口。你不知道该 IP 地址被分配给了哪个逻辑接口，但该逻辑接口已不再需要。使用哪个命令可以成功移除此逻辑接口？

- A. `ifconfig hme0 down`
- B. `ifconfig hme0 removeif 192.168.7.4`
- C. `ifconfig hme0 192.168.7.4 down`
- D. `ifconfig 192.168.7.4 hme0 removeif`

## 问题 19

当你运行 `netstat -i` 命令时，你注意到主接口上发生了大量的输出错误。以下哪两种情况可能是导致此问题的原因？

- A. 同一网络上存在重复 IP 地址。
- B. 多个主机正尝试同时发送数据。
- C. 系统具有一个故障的网络适配器。
- D. 网络上的某个远程主机有硬件问题。

## 问题 20

- `ifconfig` 命令的哪些选项用于为多路径环境下使用的网络接口设置测试地址？选择 2 项。

- A. `deprecated`
- B. `-failover`
- C. `failover`
- D. `-deprecated`
- E. `unplumb`

## 问题 21

- 关于 DNS 权限区域（zones of authority），以下哪些项是正确的？选择 2 项。

- A. 区域可以跨一个或多个域名。
- B. 区域被限于单个域名。
- C. 区域包含域名以及与该域名相关的数据。
- D. 区域包含域名，但不包含域名内的相关数据。

## 问题 22

- 哪种地址类型存在于 IPv4 中但在 IPv6 中不再使用？

- A. 任播 (Anycast)
- B. 多播 (Multicast)
- C. 单播 (Unicast)
- D. 广播 (Broadcast)

## 问题 23

- NTP 服务器属于一个称为分层（strata）的层级结构。有多少层？

- A. 5
- B. 10
- C. 15
- D. 20

## 问题 24

- 你的 ultra10 系统（主机名 alpha）有一个主网络接口 `hme0` 和一个逻辑接口 `hme0:1`。你想添加一个 IP 地址为 `192.168.9.9` 的进一步逻辑接口。以下哪些选项可以正确实现此操作？选择 2 项。

- A. `ifconfig hme0 plumb 192.168.9.9 up`
- B. `ifconfig hme0:2 plumb 192.168.9.9 up`
- C. `ifconfig hme0 addif 192.168.9.9 up`
- D. `ifconfig hme0 -add 192.168.9.9 up`
- E. `ifconfig hme0 addif 192.168.9.9 up`

## 问题 25

- `in.ndpd` 进程在启动时读取哪个配置文件？

- A. `/etc/inet/ndpd.conf`
- B. `/etc/ndpd.conf`
- C. `/etc/inet/ipnodes`
- D. `/etc/ipnodes`

## 问题 26

- `com`, `gov`, `edu` 和 `org` 等 DNS 域名属于哪种类型的域名？

- A. 根域名 (Root domain)
- B. 顶级域名 (Top-level domain)
- C. 二级域名 (Second-level domain)
- D. 完全限定域名 (Fully-qualified domain name)

## 问题 27

- TCP 使用哪种连接提供双方向的并发数据传输？

- A. 全双工 (Full-duplex)
- B. 单工 (Simplex)
- C. 半双工 (Half-duplex)
- D. 双双工 (Double duplex)

## 问题 28

`netstat -i` 命令的输出可计算网络接口上的冲突率。你的输出报告有352 次冲突和 16000 个输出包。冲突率百分比是多少？

- A. `4.4%`
- B. `2.2%`
- C. `1.1%`
- D. `8.8%`

## 问题 29

- 你想删除路由表中的所有条目。哪个命令（及其选项）可以实现这一点？

- A. `route delete default`
- B. `route flush`
- C. `init 2`
- D. `route monitor`

## 问题 30

文件 `/etc/default/mpathd` 设置了一些供 `in.mpath` 守护进程初始变量。其中一个变量定义了在将接口标记为失败之前等待多长时间。是哪个变量定义的？

- A. `FAILURE_TIMEOUT`
- B. `FAILURE_DELAY`
- C. `FAILURE_DETECT`

## 问题 31

TCP/IP 模型中的哪层描述了硬件问题？

- A. 网络层
- B. 网络层
- C. 传输层
- D. 应用层

## 问题 32

`arp` 命令的哪个选项用于删除缓存中的条目？

- A. `-s`
- B. `-d`
- C. `-a`
- D. `-f`

## 问题 33

- `255.255.255.0` 有多少位表示网络？

- A. `8`
- B. `16`
- C. `18`
- D. `24`

## 问题 34

- 使用多路径时，为什么需要创建一个地址？

- A. 为了在发生故障时。
- B. 为了监控接口状态。
- C. 为了启用多路径。
- D. 为了负载均衡。

## 问题 35

- 冲突在哪个模型的哪层发生？

- A. 网络层
