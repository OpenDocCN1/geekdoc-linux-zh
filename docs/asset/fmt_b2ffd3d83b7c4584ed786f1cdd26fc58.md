
# POSTROUTING, 59–61
# PREROUTING, 59–61
# 重命名, 86
# 用户定义的, 54–55

计算机应急响应小组 (`CERT`), 352

- 配置文件, `AIDE`, 297–300
- 配置 `AIDE`, 297–301
- 邮件服务。另见初始化邮件服务（Email services, initializing）。
- 防火墙。另见初始化防火墙（Initializing firewalls）；安装防火墙（Installing firewalls）。
- 内部 LAN, 191–192
- 多局域网, 192–195
- `Snort` 程序, 288–289

# 校验和（Checksums）

- `AIDE` 检查, 310
- 定义, 352
- `TCP`（传输控制协议）, 15

# Chkrootkit 程序

- 下载, 251
- 假阴性（false negatives）, 252
- 假阳性（false positives）, 252
- 感染报告, 253
- 局限性, 253–254
- 运行计划计划, 255
- 运行, 253–256
- 安全使用, 254–255
- 连接状态，初始化防火墙, 107
- 连接跟踪表达式, 88–89
- 无连接协议与面向连接协议对比, 7
- `connectionstatepolicy` 文件, 170, 173
- 连接跟踪链, 151, 166
- `Contrack` 表达式, 88–89
- 瓶颈防火墙（Choke firewalls）, 181–182, 354
- `chroot` 程序/系统调用, 352
- `CIDR`（无类域网间路由）, 352
- 地址保护, 10
- 继续处理数据包, 87
- `continue` 语句, 87
- 措施。另见入侵防御（Intrusion prevention）。
- `create` 命令, 86
- 电路网关（Circuit gateway）。另见电路级代理（Proxies, circuit-level）。

# D

守护进程（Daemons）。另见特定守护进程。
- 定义, 353
- 默认拒绝一切（`deny-everything-by-default`）, 29–30
- 监听服务端口, 19
- 数据包过滤, 31–32
- `DARPA` 网络模型, 6
- 删除命令, `iptables`
- 链语法, 86
- 数据库, `AIDE`
- 规则语法, 87
- 初始化, 300
- 表格语法, 85
- 更新, 302–303

# 删除（Deleting）

- 数据链路层（Datalink layer）, 6, 353
- 链, 86
- 规则, 87
- 表, 85
- `Debian`, 初始化防火墙, 130
- 非军事化区（`DMZ`）, 180, 353
- `--debug` 选项, 85
- 多路用（Demultiplexing）, 6

# 调试（Debugging）

- “拒绝服务（Denial of Service）”, 40
- 启用, 85
- 拒绝服务（`DoS`）攻击。另见 `DoS` 防火墙脚本，（denial of service）攻击。
- 默认拒绝一切策略。另见调试（Debugging），防火墙规则（firewall rules）。
- 防火墙开发技巧, 211–212
- `fuser` 命令, 226–227
```
iptables -L INPUT
```
214–215
- 调试, 211–212
```
iptables -n INPUT
```
215–216
- 定义, 353
- `iptables` 表列表, 213–214
```
iptables -v INPUT
```
216
- 缺点, 114
- 列出防火墙规则, 213–217
- 拒绝数据包与丢弃（Denying packets vs. rejecting）, 202
- 日志消息优先级, 218
- 目标地址, `NAT`, 202
- 日志消息解释, 220–223
- 目标 `NAT`（`DNAT`）, 205–206
- 网络安全审计, 227
- 目标地址检查（destination-address-check）, 151, 168
- `nftables` 列表, 216–217
- `Nmap` 工具, 227
- 检查开放端口, 223–227
- 输出报告规范, 226
- 检查端口绑定进程, 226–227
- `syslog` 配置, 217–222
- 系统日志, 217–223
- 详细程度, 216
- 默认策略。另见默认允许一切（everything-by-default policy）；默认拒绝一切（Deny-everything-by-default）。
- 默认允许一切（`accept-everything-by-default`）, 29–30
- `DHCP`（动态主机配置协议）, 353
- `DHCP`（动态主机配置协议）
- `DHCPACK` 消息, 135
- `DHPDECLINE` 消息, 135
- `DHCPDISCOVER` 消息, 135
- `DHCPINFORM` 消息, 135
- `DHCPNAK` 消息, 135
- `DHCPOFFER` 消息, 135
- `DHCPRELEASE` 消息, 135
- `DHCPREREQUEST` 消息, 135
- 定向广播, 12, 110
- 方向限定符, `TCPDump`, 270–271
- 目录，包括搜索路径, 85
- 禁止入站数据包, 108–109
- `DMZ`（非军事化区）, 180, 353
- `DNAT`（目标 `NAT`）, 205–206, 209–210
- `DNAT` 目标扩展, 56, 58, 80–81
- `DNS`（域名服务）
- 定义, 18, 353
- `DNS` 查找，作为客户端, 120–121
- `DNS` 查找，转发服务, 117
- `DNS` 查找，端口使用, 121–122
- `DNS` 协议, 109
- `DNS` 流量识别, 157
- `dns-policy` 文件, 170
- `DoS`（拒绝服务）攻击。另见禁止入站数据包。
- 应对措施, 34
- 缓冲区溢出, 45
- 启用 `SYN` Cookie, 41
- 分段, 44
- 文件系统溢出, 45
- 定义, 352
- 禁用, 32
- 死亡（Death）攻击, 42–43
- 源地址过滤, 38
- 点点表示法, 8
- 默认策略, 106
- 丢弃规则, 88
- 丢弃语句, 87
- 丢弃数据包, 102
- 双宿主机计算机, 353
- 动态分配地址, 39
- `ECE` 标志位, 16
- 邮件泛滥（Email Bombing and Spamming）, 46
- 邮件服务，`DoS`（拒绝服务）攻击, 125
- 邮件服务，初始化, 123
- 接收邮件, 127
- 向外部服务器发送邮件, 124
- 通过 `SMTP` 发送邮件, 125
- 端到端透明性, 4
- `ESP` 封装负载, 231–232
- `ESTABLISHED` 状态, 7
- `ESTABLISHED` 数据包, 74
- 以太网卡, 18
- 以太网帧, 354
- 以太头部, 91
- 防火墙规则, 17
- 扩展, 55
- 扩展匹配, 56
- 扩展语法, 87
- 扩展目标, 57
- 扩展 `iptables` 表, 88
- 扩展 `nftables` 链, 86
- 扩展 `nftables` 列表, 216
- 扩展 `nftables` 语法, 85
- 扩展 `nftables` 规则, 211
- 扩展 `nftables` 策略, 217
- 扩展 `nftables` 链, 151
- 扩展 `nftables` 过滤, 157
- 扩展 `nftables` 链, 152
- 扩展 `nftables` 过滤器, 164
- 扩展 `nftables` 规则, 168
- 扩展 `nftables` 策略, 170
- 扩展 `nftables` 链, 152
- 扩展 `nftables` 过滤器, 164
- 扩展 `nftables` 规则, 168
- 扩展 `nftables` 策略, 170
- 扩展 `nftables` 链, 151
- 扩展 `nftables` 策略, 172
- 扩展 `nftables` 语法, 85
- 默认允许一切（`accept-everything-by-default`）, 29–30
- 默认拒绝一切（`deny-everything-by-default`）, 29–30
- `DHCP`（动态主机配置协议）, 353
- `DHCP`（动态主机配置协议）
- `DHCPACK` 消息, 135
- `DHPDECLINE` 消息, 135
- `DHCPDISCOVER` 消息, 135
- `DHCPINFORM` 消息, 135
- `DHCPNAK` 消息, 135
- `DHCPOFFER` 消息, 135
- `DHCPRELEASE` 消息, 135
- `DHCPREREQUEST` 消息, 135
