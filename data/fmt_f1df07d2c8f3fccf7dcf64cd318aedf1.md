
d) 接下来继续？首先重置防火墙，并将入站包和通过防火墙的包的默认设置为“丢弃 (`drop`)”。如果由于原因脚本中没有某个包的规则，它将被丢弃。需要离开防火墙的包在此处设置为默认值“允许 (`allow`)”。

e) `/proc` 脚本允许在系统运行时简单地配置内核。脚本借此开启某些安全选项。对于许多人来说，只有将配置文件中的 `FW_SECURITY` 选项设置为 `"yes"` 才有帮助，因为影响可能是复杂的。

f) 设置为“路由 (`route`)”的将激活路由功能。

g) 然后——非常重要——允许通过 `"localhost"` 接口的所有流量。

h) 现在处理“IP 欺骗 (`IP Spoofing`)”和“防止绕过 (`Circumvention prevention`)”规则。这些规则确保拦截并拒绝伪装属于其他网段的外部和内部攻击。同时，也不会阻止对内部网络的直接访问尝试。

i) 重定向规则（`Redirecting rules`），可以将对内部网络或本地端口的访问切换到防火墙的特定端口。

j) 连接到内部（受信任）网络的用户可以在配置文件中指定防火墙是否应防御来自内部的攻击。如果不是如此，此处将允许所有从内部网络到防火墙的流量。此处的选项 `FW_PROTECT_FROM_INTERNAL` 有此作用。

然后生成 ICMP、TCP 和 UDP 的规则。

k) ICMP 规则分两个阶段创建。首先根据配置允许或禁止特定的 ICMP 包，例如对防火墙的 `"ping"` 来自最近连接路由器的“源拥塞通知 (`Source Quench`) 消息”（例如作为 `traceroute` 等通用程序的响应包）。第二阶段形成通用配置，禁止危险的 ICMP 包并允许重要的包。内部网络始终允许通过 `"ping"` 访问。

l) TCP 规则首先允许已配置的服务，然后是针对受信任网络的，最后是针对内部网络。随后配置端口 `13` 以引入超时机制，防止不必要的等待（例如发送电子邮件）。现在是一个关键的自动机制：将 `FW_AUTOPROTECT_GLOBAL_SERVICES` 设置 `"yes"` 的用户将过滤未监听特定接口（例如 `0.0.0.0` 或 `INADR_ANY`）的服务。因此，可以在情况下允许所有入站连接，但保护运行在端口 `4545` 上的数据库。最后生成规则，允许访问特权端口（`1024` 到 `65535`）；完全不允许；仅允许 `/etc/resolv.conf` 定义的 DNS；仅允许来自特定源端口的连接（如果需要保护则不建议这样做）；内部系统可以访问非特权端口——`AUTOPROTE` 会保护其服务。

m) UDP 类似，仅对端口 `13` 执行重置。

n) 随后是路由规则，定义哪些系统可以访问内部网络。由于上述原因不应使用！

o) 现在是配置伪装（`Masquerading`）规则。

p) 为敏感包配置额外的日志机制非常，例如尝试建立连接的禁用 TCP 包。如果设置了 `LOG_*ALL`，将记录每个包，这将产生大量条目，因此用于故障排除。

q) 此外为 SSH、FTP、WWW、Syslog 和 SNMP 添加一些优化规则，以使其在网络传输中更快或更安全。

脚本完成后，激活防火墙。如果发生错误，停止防火墙以防应用错误的规则。

### 5.3 防火墙上的服务

## SuSE Linux Live-CD

### 5.3 防火墙上的服务

检查内核版本以确定是否支持 `ipchains`。如果识别出 `2.0` 内核或在无法识别内核版本时无警告运行，脚本将终止。

### SuSE Linux Live-CD

## SuSE Linux Live-CD

### ICMP

ICMP 规则分两个阶段创建。首先根据配置允许或禁止特定的 ICMP 包，例如对防火墙的 `"ping"` 来自最近连接路由器的“源拥塞通知消息”（例如作为 `traceroute` 等通用程序的响应包）。第二阶段形成通用配置，禁止危险的 ICMP 包并允许重要的包。内部网络始终允许通过 `"ping"` 访问。

### TCP

TCP 规则首先允许已配置的服务，然后是针对受信任网络的，最后是针对内部网络。随后配置端口 `13` 以引入超时机制，防止不必要的等待（例如发送电子邮件）。现在是一个关键的自动机制：将 `FW_AUTOPROTECT_GLOBAL_SERVICES` 设置 `"yes"` 的用户将过滤未监听特定接口（例如 `0.0.0.0` 或 `INADR_ANY`）。因此，可以在情况下允许所有入站连接，但保护运行在端口 `4545` 上的数据库。最后生成规则，允许访问特权端口（`1024` 到 `65535`）；完全不允许；仅允许 `/etc/resolv.conf` 定义的 DNS；仅允许来自特定源端口的连接（如果需要保护则不建议这样做）；内部系统可以访问非特权端口——`AUTOPROTE` 会保护其服务。

### UDP

UDP 类似，仅在此对端口 `13` 执行重置。

随后是路由规则，定义哪些系统可以访问内部网络。由于上述原因不应使用！

现在是配置伪装（`Masquerading`）规则。

为敏感包配置额外的日志机制非常重要，例如尝试建立连接的禁用 TCP 包。如果设置了 `LOG_*ALL`，将记录每个包，这将产生大量条目，因此用于故障排除。

此外为 SSH、FTP、WWW、Syslog 和 SNMP 添加一些优化规则，以使其在网络传输中更快或更安全。

脚本完成后，激活防火墙。如果发生错误，停止防火墙以防应用错误的规则。

> 注意

仅通过配置这些设置和使用 SuSE 防火墙脚本并不能让您的系统从生变得安全。没有任何方法是只需简单安装就能防止所有安全漏洞的。

* 不要信任任何你未创建的软件。
* 定期检查服务器的完整性。
* 如果您想使用（这是不推荐的）防火墙/堡垒服务器，应该检查是否使用了代理服务器，例如用于 WWW 的 `Squid`、用于邮件的 `smtp` 等。在此情况下也请考虑 `chroot` 并让进程以 `root` 身份运行。

# SuSE Linux Live-CD für Firewall

Für ein „sicheres“ System sollten Sie außerdem folgendes beachten: Sichern Sie alle Dienste, die über nicht vertrauenswürdige Netzze (z. B. Internet) angeboten werden, durch die Verwendung von Software, die im Hinblick auf Sicherheit entwickelt wurde (z. B. `posix` und `ssh`). Setzen keine Software aus nicht vertrauwürdigen Quellen ein. Darüber hinaus sollten Sie regelmäßig die Sicherheit Ihres Servers überprüfen.

# Konfiguration des SuSE Firewall-Scripts

Um das Firewall-Script starten zu können, muss unbedingt die Variable `START_FW` in der Datei `/etc/rc.config` auf „yes“ gesetzt sein. Die Verwendung des SuSE Firewall Admin-hosts erfolgt automatisch.

Wenn es sich bei Ihrem Computer um eine Firewall handelt, die wie ein Proxy funktioniert (also Routing zwischen den Netzwerken), oder wenn Sie sich außen befinden und gleichzeitig mit dem Internet und intern verbunden sind, müssen Sie die Punkte 2), 3), 9) und evtl. 7), 10), 11), 12), 14) und 18 konfigurieren.

Wenn der Computer als Firewall dient und die Funktionalität von Routing bzw. Masquerading zur Verfügung stellen soll, müssen Sie die Punkte 2), 5, 6), 9) und evtl. 7), 10), 11), 12), 15) bearbeiten.

Wenn Sie genau wissen, was Sie tun, können Sie die Punkte 16), 17), 18) und die Experten-Optionen (20 bis 21) und 22 konfigurieren. SuSE empfiehlt, davon Abstand zu nehmen.
