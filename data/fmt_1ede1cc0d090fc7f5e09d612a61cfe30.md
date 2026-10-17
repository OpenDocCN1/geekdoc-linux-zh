
Anhand einer Kommunikationsmatrix behalten Sie den Überblick, welche Dienste für welche Client zugänglich sind und angezeigt werden.

## 7.3 Dienstleistungen der SuSE Linux AG

SuSE Linux AG steht Ihnen gerne zur Verfügung für:

- Beratung: Kommunikationsanalyse

- Planung: Netzwerkplanung

- Installation: Integration

- Wartung: Online-Support

- Support: Fehlerbehebung

## 7.4 Updates

Beim Betrieb einer Firewall ist die permanente Pflege der Software extrem wichtig. Sobald eine Sicherheitslücke entdeckt wird, muss ein Update der Firewall stattfinden. Sicherheitsupdates für SuSE Linux werden zur Verfügung. Diese Pakete laden Sie z. B. mit dem Kommando:

```
root@adminhost:$ rpm -uh paket.rpm
```

Folgen Sie auch den Security-Mailinglisten:

- http://lists.suse.com/archive/suse-security

- http://www.suse.de/de/support/security/index.html

## 7.5 Maßnahmen im Falle eines Einbruchs

### 7.5.1 System-Einbruch und Ereignisanzeige

Ein „richtig“ konfiguriertes Linux/UNIX-System kann schon ziemlich sicher gelten. Gefahren, die mit einem komplexen System wie Linux zusammenhäng, werden besser erkannt als bei anderen Betriebssystemen, welche UNIX mehr als 30 Jahren eingesetzt und entwickelt wurden. UNIX ist die Grundlage des Internets. Nichtdestrotz werden Konfigurationsfehler und Sicherheitsücken immer wieder auf. Es wird immer Sicherheitsängel geben. Sicherheitsexperten und Cracker/Hacker stehen sich imwährend Kampf einen Schritt voraus. Was als sicher gilt, kann morgen wieder unsicher sein.

Anzeichen für einen Einbruch in Ihr System (engl. Intrusion Detection)

Als Zeichen für eine Kompromittierung Ihres Systems können Sie alles betrachten, was vom „normalen“ Verhalten Ihres Systems abweicht, z. B.:

- erhöhte Prozesslast

- außerhalb Netzwerkverkehr

- ungewöhnliche Prozesse oder

- Prozesse von Benutzern, die nicht existieren.

## Einen Angriff erkennen

Zunächst sollte man sich im Klaren darüber werden, welche Art von Aktionen als Angriff zu bewerten sind. Leider ist in der Zwischenzeit vollkommen normal, ein Rechner, der mit dem Internet verbunden ist, nach offenen, verbundenen Ports abgescannt zu. Ebenso ist es üblich, Ports anzugreifen, die irgendwann als verwundbar bekannt wurden (pop3/popper, rpc-mount, smtp/sendmail). Die meisten „Angriffe“ werden von „Script-Kiddies“ durchgeführt. Verwendet werden vorgefertigte „Exploits“, die auch auf vielfältigen Web-Seiten veröffentlicht werden (z.B. http://rootshell.com).

## 指南

如果您怀疑遭受了攻击，该怎么办？推荐以下文献：

[Steps for Recovering from a Unix Root Compromise](http://www.cert.org/tech/tips/root_compromise.html)

RFC 2196: 站点安全手册

这两份出版物描述了在成功入侵后应采取的措施。这些文档为公司、机构或教育机构提供了应对方案的正式方法。这种策划的流程需要大量的存储空间来分析系统的“快照”（Snapshots），以便让人员对安全问题负责，并在适当的情况下采取法律追究措施。

如果您怀疑已经遭受了成功的攻击，该怎么办：

- 保持冷静至关重要。被忽略的操作可能会破坏信息（例如由入侵者启动的进程）。

- 安全策略中应规定该做什么以及通知谁。但通信不应通过邮件进行，而应通过电话或传真进行。

- 物理上断开与防火墙的网络连接。关闭计算机不是一个好主意。重要的信息可能会丢失，例如入侵者刚刚启动的程序。

- 使用 `ps` 列出所有运行中的进程，并寻找在防火墙正常运行时未出现的进程。

- 为防火墙的运行创建一个进程表，作为比较的基础。

- 检查运行中的进程是否绑定了异常的 TCP 或 UDP 端口。

- 数据包过滤规则是否被更改过？

- 将所有配置文件与原始配置进行比较。这在“CD上的SuSE Linux”中非常简单。配置存储在管理主机上。但重要点是，不要重启防火墙计算机，否则对过滤规则的更改将会丢失！

- 此外，请备份所有日志文件（Logfiles）。日志文件可能是具有法律意义的证据。记录您采取的每一个步骤。如果将日志文件存储在本地硬盘上，您应该为了文档目的制作硬盘的 1:1 复制。

- 将您的数据备份到 CD 或其他介质（磁带驱动器、ZIP 驱动器）上。

## 7.5 入侵发生时的措施

- 分析日志文件：谁在何时、何地通过什么方式（IP地址、域名、可能甚至用户名）尝试访问哪些服务/端口？是否尝试了猜测密码（识别到同一个用户的多次登录失败尝试）？

- 确保您所有的计算机/服务器都使用统一、准确的时间源。计算机和防火墙日志尽可能保持一致非常重要。如果可能，请为所有服务器使用共同的时间源。只有这样才能对不同计算机上的事件进行精确归类。

- 违反了安全策略的哪些部分？这在内部攻击中尤为重要。

- 禁用您网络中执行攻击的用户账户。针对内部违规的相应处理程序应已有规定（安全策略或公司政策）。

## 7.52 外部攻击

向负责地址的系统管理员通知（通过域名的 Postmaster 或 Abuse 地址）报备。

这涉及到您应该提供哪些信息的日志文件。关于事件或攻击的报告应包含新信息，以便让对方能够查明问题。请记住，您的联系人可能是攻击您的人。以下是您可以提供的可能信息列表。请根据您的意愿选择提供的内容：

- 您的电子邮件地址，

- 电话号码，

- 您的 IP 地址、主机名、域名，

- 参与攻击的 IP 地址、主机名、域名，

- 攻击的日期和时间，最好带有相对于 GMT 的时区，

- 攻击的描述，

- 如何发现攻击的，

- 与攻击相关的日志文件摘录，

- 日志文件格式的描述，

- 描述攻击类型和严重性的安全公告（Advisories）及安全信息，

- 您对相关人员的要求，例如关闭账户、确认攻击、给出说明、提供信息、请求进一步观察。

在完成所有数据备份和记录措施后，重新启动您的防火墙。如果可能，请设置各个程序的日志级别（Loglevel）。攻击者很可能会再次尝试入侵您的系统。那将是您有机会抓获攻击者的时刻。

示例：
