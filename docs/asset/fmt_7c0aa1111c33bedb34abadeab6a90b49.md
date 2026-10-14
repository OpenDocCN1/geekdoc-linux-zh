
| 8 | parse | | |

| 9 | mx4200 | GPS | Magnavax MX4200 GPS 接收器 |

| 10 | as2201 | GPS | Austron 2201A GPS 接收器 |

| 11 | arbiter | GPS | Arbiter 1088A/B GPS 接收器 |

| 12 | tpro | IRIG | KSI/Odetis TPRO/S IRIG 接口 |

| 13 | leich | ATOM | Lech CDS 530 主时钟控制器 |

| 15 | * | * | TrueTime GPS/TM-TMD 接收器 |

| 17 | datum | DATM | 精密时间系统服务 |

| 18 | acts | ACTS | NIST 自动计算机时间服务 |

| 19 | heath | WWV | Heath WWW/WWVH 接收器 |

| 20 | nmea | GPS | 通用 NMEA GPS 接收器 |

| 22 | atom | PPS | PPS 时钟律维持 |

| 23 | Ptb | TPTB | PTB 自动计算机时间服务 |

| 24 | Usno | USNO | USNO 调制解调时间服务 |

| 25 | * | * | TrueTime 通用接收器 |

| 26 | Hpgps | GPS | Hewlett Packard 58503A GPS 接收器 |

| 27 | Arc | MSFA | Arcron MSF 接收器 |

**表 39-1 可用的 XType**

# Sun 认证 Solaris 9.0 系统与网络管理员全合一考试指南

## 731

恰当地地。此外，服务器能够从来自多个不同的权威源提供数据。

通过选择最准确的服务器，可以提高客户端时间的准确性。坦率地说，已有可用的测量数据来确定哪些时钟提供最准确的数据。当客户端向服务器发出请求时，响应中会返回可靠性和准确性数据。

在更复杂的网络中，时间服务器必须具有高可用性，此时创建一个可以进行动态重新配置的 NTP 服务器分层系统可能更为合适。只有在硬件或软件故障影响单个生产系统的可靠性时，这种做法才是必要的。在这种情况下，多个服务器可以互充作为彼此的对等节点。在这种设置中，主时间服务器从参考源（如外部时钟）获取时间，并将其传输到其他次级服务器。或者，可能有多个主时间服务器，次级服务器必须确定哪一个最准确。客户端直接访问次级源。

当然，这形成了一个精度分层，其中主 (1) 最准确，次级服务器 (2) 次之，而客户端 (3) 最准确。至少在第 2 级应该达到毫秒级精度。然而，在较低级别可以检测到错误并进行修正，以提高时间估计的整体精度。

时间戳位于 NTP 数据模型的核心。它由一个 64 位无符号浮点数表示，是自 1990 年 1 月 1 日 00:00 以来经过的秒数。前 32 位表示该数字的整数部分，后 32 位表示该数字的小数部分。

一个非闰年的秒数为 31536000。鉴于 NTP 格式中仅有 64 位用于存储时间数据，最大值将在 2036 年达到。考虑到现在有许多使用时间戳的遗留应用程序，在大约 30 年后需要大量的规划，以开发一种与现有格式向后兼容的高容量时间戳格式。

NTP 服务器配置文件位于 `/etc/inet/ntp.server`。该文件为配置利用外部时钟设备、提供本地时钟同步并在跨网络运行的 NTP 服务器提供了一个适当的模板。这里有一个示例文件：

```
server 127.127.Xtype. prefer
fudge 127.127.Xtype stratum 0
broadcast 224.0.0.1 ttl 4
enable auth monitor
drift /var/ntp/ntp.drift
stats /var/ntp/stats/
filegen peers file peers type day enable
filegen loopstats file loopstats type day enable
filegen clockstats file clockstats type day enable
keys /etc/inet/ntp.keys
trustedkey 0
```

# 第 39 章：网络时间协议

```
requestkey 0
controlkey 0
```

`server` 条指示该系统首选的主服务器。`broadcast` 条引导服务器向客户端广播消息。漂移文件（`driftfile`）与本地时钟的准确性及其频率偏移有关。

> 考试提示 你应该能够解释 NTP 服务器配置文件。

在两种情况下都出现了 "`XType`"，必须插入一个时钟设备的合法值。设备代码可以是表 39-1 所示的设备之一。

| XType | 设备 | RefID | 描述 |
| --- | --- | --- | --- |
| I | local | LCL | 未约束的本地时钟 |
| 2 | trak | GPS | TRAK 8820 GPS 接收器 |
| 3 | pst | WWW | PSTI/Traconex WWW/WWVH 接收器 |
| 4 | wwwv | WWVB | Spectram WWVB 接收器 |
| 5 | true | | TrueTime GPS/GOES 接收器 |
| 6 | irig | IRIG | IRIG 音频解码器 |
| 7 | chu | CHU | 通用参考时钟驱动程序 |
| 8 | parse | | |
| 9 | mx4200 | GPS | Magnavax MX4200 GPS 接收器 |
| 10 | as2201 | GPS | Austron 2201A GPS 接收器 |
| 11 | arbiter | GPS | Arbiter 1088A/B GPS 接收器 |
| 12 | tpro | IRIG | KSI/Odetis TPRO/S IRIG 接口 |
| 13 | leich | ATOM | Lech CDS 530 主时钟控制器 |
| 15 | * | * | TrueTime GPS/TM-TMD 接收器 |
| 17 | datum | DATM | 精密时间系统服务 |
| 18 | acts | ACTS | NIST 自动计算机时间服务 |
| 19 | heath | WWV | Heath WWW/WWVH 接收器 |
| 20 | nmea | GPS | 通用 NMEA GPS 接收器 |
| 22 | atom | PPS | PPS 时钟律维持 |
| 23 | Ptb | TPTB | PTB 自动计算机时间服务 |
| 24 | Usno | USNO | USNO 调制解调时间服务 |
| 25 | * | * | TrueTime 通用接收器 |
| 26 | Hpgps | GPS | Hewlett Packard 58503A GPS 接收器 |
| 27 | Arc | MSFA | Arcron MSF 接收器 |

## NTP Client

NTP 客户端以特定格式发送和接收 NTP 数据。默认情况下，它监听以下组播：

```
multicast 224.0.0.1
```

以下消息中包含主要字段：

+ *Root Dispersion* 来自主源的误差估计。
* *Reference Clock Identifier* 允许主源被识别。
* *Reference Timestamp* 本地时钟上次更新的时间。
* *Originate Timestamp* 客户端发送消息的时间。
* *Receive Timestamp* 接收消息的时间。
* *Transmit Timestamp* 服务器发送消息的时间。
* *Authenticator* 指定了所使用的身份验证方法。

### 总结

在本章中，我们审查了核心 NTP 协议和配置信息，以及如何配置 NTP 客户端和服务器。鉴于 NTP 是确保数据完整性的中心服务器，我们还审查了运行 NTP 服务的安全影响，以及如何通过适当的访问控制和身份验证机制对其进行保护。

### 问题

- 1. 为什么生产系统需要定期同步其时钟？
  - A. 为了确保企业应用中的数据一致性
  - B. 确保向用户正确打印时间
  - C. 确保机器可以独立估算时间
  - D. 确保每个系统都需要一个外部硬件钟
- 2. NTP 的目的是什么？
  - A. 让每个系统都拥有自己的外部硬件钟
  - B. 允许网络上的所有系统通过多播同步时间
  - C. 防止网络客户端访问主时间服务器
  - D. 在路由器级别过滤时间戳并防止其离散
- 3. 哪种方法允许网络上的某台服务器被授权负责该网络上所有系统的时钟工作？
  - A. 点对点 (Peer-to-peer)
  - B. 星型拓扑 (Star topology)
  - C. 网络拓扑 (Net topology)
  - D. 主从模式 (Master-slave)
- 4. NTP v3 的主要新功能是什么？
  - A. 它支持一种服务器与一组对等服务器通信的方法，以平均偏移并实现对当前时间更准确的估计。
  - B. 它支持原生的公钥加密。
