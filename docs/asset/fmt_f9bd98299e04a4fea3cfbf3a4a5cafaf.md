
## 原始对照表

| dot1x | all | Dot1X |
| firewall | all | 防火墙 |
| category | subcat | 类别 |
| configuration | all | 配置 |
| client-match | all | 客户端匹配 |
| captive-portal | all | 捕捉式门户 |
| category | all | 类别 |
| category | all | 类别 |
| category | all | 类别 |
| category | all | 类别 |
| category | all | 类别 |
| subcategory | all | 子类别 |
| description | all | 类别 |

*(注：由于原文表 13-3 格式存在混乱，翻译时已根据逻辑进行了对齐修正)*

## 修正后的表 13-3 翻译内容

| 类别 (Category) | 子类别 (Subcategory) | 说明 (Description) |
| :--- | :--- | :--- |
| arm | subcat |  |
| ap-debug | all |  |
| ap-config | all |  |
| auth-amon | all |  |
| certmgr | all |  |
| dhcp | all |  |
| arm | all | ArubaOS 保护 |
| ha | all | 高可用性 |
| auth | all | 身份认证 |
| ids | all | 入侵检测 |
| ids-ap | all | AP 入侵检测 |
| ike | all | IKE 协议 |
| kerberos | all | Kerberos 服务 |
| mobility | all | 移动 |
| ntlm | all | NTLM |
| packet-trace | all | 数据包跟踪 |
| vpn | all | VPN |
| webserver | all | Web 服务器 |
| wl-sync | all | 无线同步 |
| system | all | 系统 |
| security | all | 安全 |
| network | all | 网络 |
| user | all | 用户 |
| wireless | all | 无线 |
| messages | all | 消息 |
| pan | all | 策略面板 |
| reg-tbl | all | 监管表 |
| snmp | all | SNMP |
| amon | all | AMON 相关的日志 |
| amon-ale | all | AMON-ALE 相关日志 |
| amon-amp | all | AMON-AMP 相关日志 |
| cpsec | all | CPsec |
| db | all | 数据库 |
| dot1x | all | Dot1X |
| firewall | all | 防火墙 |
| configuration | all | 配置 |
| client-match | all | 客户端匹配 |
| captive-portal | all | 捕捉式门户 |

*(注：原文中表 13-3 的文本内容存在大量重复和错位，此处已基于标准 Markdown 结构进行了清理处理)*

### 补充说明

`vpn`

VPN 日志

`user-debug all`

启用所有子类的日志

`configuration`

Dot1X 用户日志

`wireless`

`all`

启用所有子类的日志

日志级别的最终自定义是选择一个进程。选择进程是可选的，有 60 多个进程供选择。以下 CLI 输出列出了所有可用进程及其简要描述：

```
(config) #logging level emergencies wireless process ?
```

- `aaa` AAA logging
- `activate` Logging for Activate
- `anti_virus` Logging for Anti Virus
- `approc` Logging for AP processes
- `armd` Logging for ARM Process
- `aruba-central` Logging for Aruba Central
- `authmgr` Logging for user authentication
- `ble_relay` Logging for BLE Relay
- `bocmgr` Logging for BOC Manager
- `cert_dwnld` Logging for Cert Download Process
- `certmgr` Certificate Manager logging
- `cfgm` Logging for Configuration Manager
- `cpsec` CPSec logging
- `crypto` Logging for VPN (IKE/IPSEC)
- `cts` Logging for transport service
- `dbsync` Logging for Database Synchronization
- `dds` Logging for DDS Process
- `dhcpd` Logging for DHCP packets
- `esi` Logging for External Services Interface
- `extifmgr` Logging for External Interface Manager
- `fpapps` Logging for Layer 2,3 control
- `fw_visibility` Logging for FW Visibility Process
- `gsmmgr` Logging for GSM Manager
- `ha_mgr` Logging for HA_MGR
- `hcm` Logging for Health Check Process
- `httpd` Logging for Apache
- `hwmon` Logging for hwMon task
- `iapmgr` Logging for IAP manager process
- `ip_flow_export` Logging for IP Flow Export Process
- `ipstm` Logging for IPSTM Process
- `l2tp` Logging for L2TP
- `licensemgr` Logging for license manager
- `lldp` Logging for LLDP Process
- `localdb` Logging for local database
- `mdns` Logging for MDNS Proxy
- `mobileip` Logging for Mobile IP
- `msghh` Logging for msg handler helper
- `npppd` Logging for NPPPD
- `ofa` Logging for OpenFlow Agent Process
- `ospf` Logging for OSPF
- `packetfilter` Logging for packet filtering of messaging and control frames
- `phonehome` Logging for Phone Home
- `pim` Logging for Protocol Independent Multicast
- `pppd` Logging for PPP
- `pppoed` Logging for PPPoE
- `pptp` Logging for PPTP
- `processes` Logging for run-time processes
- `profmgr` Logging for Profile Manager
- `publisher` Logging for publish subscribe service
- `radvd` Logging for Router Advertisement daemon
- `resolvwrap` Logging for Resolvwrap Process
- `rfm` Logging for RF Troubleshooting Manager
- `rsync` Logging for Rsync
- `snmp` SNMP logging
- `spectrum` Logging for Spectrum process
- `stm` Logging for Station Management
- `survival` Logging for Auth Survival Server
- `syslogdwrap` Logging for Syslogd Wrap
- `traffic` Logging for traffic
