
注意上述 ① 处 `iptables` 的 `--algo` 命令行参数。`string` 扩展构建在 Linux 内核的搜索基础设施之上（位于内核源码中的 `linux/lib` 目录）。它支持多种算法，包括 Boyer-Moore 字符串搜索算法（上述的 `bm`）和 Knuth-Morris-Pratt 字符串搜索算法（`kmp`）。¹

— `-m state --ESTABLISHED` 命令行参数 ② 将字符串匹配操作限制在已建立的 TCP 连接包上，这意味着任何人无法让 `iptables` 对来自任意源地址的伪造包进行匹配——除非定向连接已建立。

我们将使用 Netcat 启动一个在本地监听 TCP 端口 5001 的 TCP 服务器，然后再次从 ext_scanner 系统作为客户端向服务器发送字符串 "tester"：

```bash
[iptablesfw]# nc -l -p 5001
[ext_scanner#] echo "tester" | nc 71.157.X.X 5001
```

现在检查系统日志，寻找字符串匹配规则了适当 syslog 消息证据：

```bash
[iptablesfw]# tail /var/log/messages | grep test
Jul 01 04:14:19 iptables for kernel: IN=eth0 OUT= MAC=00:13:b8:e3:b6:04 DST=00:30:48
```

此外，许多程序员并没有考虑到使用某些语言构造的影响，这些构造可能会以非直观的方式让应用程序暴露在攻击之下。最后，许多应用程序具有复杂的配置，缺乏经验的用户如果带有风险选项部署应用程序，可能会降低安全性。

应用层攻击分为三类：

## 针对编程漏洞的利用

应用程序开发是一项复杂的工程，不可避免地会出现编程错误。在某些情况下，这些漏洞会导致可以通过网络远程访问的严重漏洞。良好的示例包括由于使用不安全的 C 库函数导致的缓冲区溢出漏洞、以 Web 为中心的漏洞（例如将未清洗的查询传递到后端数据库的 Web 服务器，可能导致 SQL 注入），以及对用户内容进行后过滤的漏洞（可能导致跨站脚本攻击 XSS）。

## 针对信任关系的利用

某些攻击利用信任关系而非编程漏洞。从与应用程序交互来看，此类攻击看起来完全合法的，钓鱼攻击就是一个很好的例子；其目标不是 Web 服务器或邮件服务器，而是人。

## 资源耗尽

与网络或传输层一样，应用程序有时会在海量数据输入下遭受故障。此类攻击会让所有人都无法使用应用程序。

## 滥用应用层

网络化应用日益增长的复杂性使得利用应用程序漏洞变得更容易。虽然通用网络和传输协议的实现通常符合 RFC 定义的指南，但并没有标准可以可以控制特定应用程序如何处理用户输入，或者应用程序是否是用不具备自动边界检查或内存管理的语言（如 C）编写的。全新的攻击技术不断被发现并发布到安全社区——一个很好的例子是涉及跨域 Web Cookie 的跨站脚本攻击概念。

接下来的章节将说明一些应用层攻击。某些攻击可以通过 `iptables` 字符串匹配检测，每个示例都包含一个针对特定攻击的 `iptables` 规则。

## Snort 签名

理解应用层攻击的最佳方法之一是浏览 Snort 签名集。虽然最近的签名不再随源码发布，但 Bleeding Snort 项目会生成签名。将 `iptables` 规则与 Snort 签名关联是获得真实检测能力的关键。

为了在防火墙链中通过 80 端口建立的 TCP 连接看到 `/etc/shadow` 字符串时让 iptables 记录消息，请使用以下规则：

```bash
iptables -I FORWARD 1 -p tcp --dport 80 -m state --ESTABLISHED -m string --string "/etc/shadow" --algo bm -j LOG --log-prefix "ETC_SHADOW: "
```

我们将在第 9 章详细讨论 Snort 签名，但在这里我们介绍应用层检查。Web 服务器（以及它执行的任何 CGI 脚本）可能以没有读取 `/etc/shadow` 文件权限的用户身份运行，但攻击者在尝试请求文件之前知道这一点。考虑以下 Snort 签名：

```
alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-ATTACKS"; content:"etc/shadow"; flow:to_server,established; nocase; clasype:web-activity; sid:1372; rev:5);
```

## 缓冲区溢出利用

*缓冲区溢出* 是一种利用应用程序源代码中编程错误的攻击，其中缓冲区的大小不足以容纳拷贝到其中的数据；当相邻的内存位置被重写时，使用“溢出”一词。对于基于栈的缓冲区，成功的利用会重写返回地址（位于栈上），使其指向攻击者提供的代码。这反过来允许攻击者控制进程的执行。

另一类缓冲区溢出攻击通常在 C 或 C++ 应用程序中通过不当使用某些未自动实现边界检查的库函数引入。此类函数的示例包括 `strcpy()`、`sprintf()`、`gets()` 和 `scanf()`。

> Snort 社区将它的签名称为规则（rules），但入侵检测系统也采用签名（signature）一词作为向入侵检测系统描述攻击的机制。在书中，这两个术语互用——签名并不限于单一模式，因此将通过 `malloc()` 和 `calloc()` 等函数分配的内存区域描述为攻击是有效的。注意你可以在 Aleph One 广泛引用的论文中找到如何编写缓冲区溢出攻击（参见 http://insecure.org/st/.html）。Jon Erickson 的《Hacking: The Art of Exploitation》（Starch Press, 2007）是缓冲区溢出技术信息的另一个优秀来源。

在网络攻击的背景下，没有通用的方法来检测缓冲区溢出攻击。然而，对于通过加密通道传输数据的应用程序，用 50 个加密字符 A 填充缓冲区是非常可疑的。（加密协议通常不会反复使用同一个字符。）

如果存在此类攻击并在地下社区共享，那么可能添加 `iptables` 来查找此类行为是值得的。例如，以下规则将用于 SSL 通信。注意 A 字符的字符串：

```bash
iptables -I FORWARD 1 -p tcp --dport 443 -m state --ESTABLISHED -m string --string "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA" -j LOG --log-prefix "SSL OVERFLOW "
```

由于利用代码可以将字符 A 更改任何其他字符，上述规则通常可以通过对代码进行简单的修改来绕过。然而，利用代码有时会被未经修改使用，因此上述策略在某些情况下是有效的。

虽然签名集包含许多针对溢出攻击的签名，但这些签名通常不需要特定的字节即可检测攻击。作为参数创建应用程序命令的数据大小指示了溢出攻击。例如，以下是针对 FTP 服务器中选定命令溢出的签名。它需要至少 100 字节的数据才能检测到 FTP 服务器中的所示命令。

```
alert tcp $EVE_NET any -> $HOME_NET (msg:"FTP SITE CHOWN overflow attempt";
flow:to_server,established;content:"SITE";content="CHOWN";distance:0; nocase;
disatata=100,relative;pcre="/SITE$CHOWN%n{100,}"; reference=bugtrack,2120;
cve:2001-0065;clasype=attempted-admin; sid:1562; rev:11;)
```

```bash
[iptablesfw] iptables -I FORWARD 1 -p tcp --dport 21 -m state --state ESTABLISHED -m string --string "site" --algo bm -m string --string "chown" --algo bm -m length --length -j LOG --log-prefix "CHOWN OVERFLOW "
```

## SQL 注入攻击

SQL 注入攻击利用了应用程序中的一种状态，即在将输入包含在数据库查询之前，未对输入进行正确的验证或过滤。聪明的攻击者可以使用 SQL 语言的嵌套来构建一个新查询，并可能从数据库中修改或提取信息。SQL 注入攻击的常见目标是通过 Web 服务器执行并与后端数据库建立交互的 CGI 程序。

例如，假设一个 CGI 程序通过 CGI 脚本从 Web 客户端获取用户名和密码，对数据库中的数据进行用户名和密码检查。如果用户名和密码没有经过妥当过滤，那么用于执行验证的查询可能会受到注入攻击。这种攻击可以更改查询，使其不仅检查相等性，还能通过新查询来修改数据。攻击者可以利用这种方法为任意用户设置密码；甚至可能是管理员级别的密码。

很难检测到通用的 SQL 注入，但某些 Snort 规则对于特定攻击非常有效。例如，这里的一个 Bleeding 签名可以检测攻击者尝试通过在 ① 处提供单引号并在 ② 处提供两个字符（每个字符后跟着 NULL 字节）来截断 SQL 查询。注释掉 SQL 查询的剩余部分，这可以用于移除通过其他字段的额外连接对查询可能设置的限制。

```snort
alert tcp $EXTERNAL_NET any -> $SQL_SERVERS 1433 (msg:"BLEEDING-EDGE EXPLOIT MS-SQL SQL injection string plus line comment"; flow:to_server,content:"|00|"; content:"|00||00|"; reference:url,www.nextgens.com/papers/more_advanced_sql_injection.pdf; reference:url,securitymap.net/sm/docs/mysql-checklist.html; clasype:attempteduser; sid:200048;rev:5);
```

此 Snort 规则可以干净地转换为 iptables，包括使用 `-hex-string` 命令行处理 NULL 字符：

```bash
[iptablesfw] iptables -I FORWARD 1 -p tcp --dport 1433 -m state --state ESTABLISHED -m string --string "|00|" --algo bm -m string --hex-string "|00||00|" --algo bm -j LOG --log-prefix "SQL INJECTION COMMENT"
```

SQL 签名及其 iptables 等效规则中的一个棘手问题是Snort 或 iptables 都不遵守两个内容字符串的顺序。如果数据包是已建立 TCP 连接的一部分，且包含两个反序的字符串（使用 Snort 的十六进制表示表示 NULL），例如 `|00||00| foo bar |'00|'` 而不是 `|00| foo bar - |00|-|00|`，那么 Snort 签名和 iptables 规则就会触发。对于某些签名，如果合法数据有可能模拟反序的恶意数据，这可能会增加误报率。

**注意** Snort 规则中的 Web 参考：http://www.nextgens.com/papers/more_advanced_sql_injection.pdf（注：已从 nextgenss 纠正为 nextgens）包含了关于 SQL 注入攻击的极佳信息。

## 大灰脑黑客

如今互联网上一些最严重的攻击是那些通过用户使用的应用程序直接针对个人的攻击。这些攻击通过利用人们信任某些信息的倾向，绕过了最优秀的加密算法和身份验证方案。例如，如果攻击者让某人信任某些恶意软件的来源，或者是假的密码或加密密钥，攻击者就可以绕过最复杂的安全机制。有时，利用人性比在加固的系统、应用程序或加密方案中寻找漏洞要得多。

## 钓鱼

钓鱼是一种攻击手段，其中用户被欺骗向非意愿来源提供在线账户（如银行账户）的身份验证凭据。通常通过向用户发送一封看起来官方的电子邮件，要求他们访问在线账户并出于安全考虑执行某些“紧急”任务，例如更改密码。（如果不是因为成功的钓鱼攻击对用户造成的破坏性影响，这里的讽刺会很幽默了。）邮件提供了一个看似合法的网页链接，但经过精心设计，将用户引导到由攻击者控制的模仿正版网站的网站。一旦钓鱼用户访问网站并输入凭据，攻击者就会窃取他们的凭据。

例如，这是我收到的一封来自伪造邮件支持 `support@citibank.com` 的钓鱼邮件部分，主题为“Citibank Online Message”：

在登录 Citibank Online 时，您或其他人已尝试多次登录并达到了您的每日限制。作为额外的安全措施，这不会影响您对在线银行或 ATM 银行的访问。在尝试登录之前，请验证您的信息 <a href="http://196.41.X.Y/s/" onmouseover="window.status='status">http://www.citibank.com/us/cards/index.jsp;return true";</a>。在验证您的信息后二十小时内，您将可以尝试登录 Citibank Online。（此时不需要更改密码。）

看似无害的文字、友善帮助的态度（“多次登录尝试”和“您不需要更改密码……”）以及网页链接都是精心设计的。链接包含一些嵌入的 JavaScript，指示网络浏览器如果用户使用该链接，则显示 Citibank 网站的合法链接。

幸运的是，在 Web 会话中，可以使用以下规则检测攻击检测这封特定的钓鱼邮件：

```bash
iptables -I FORWARD 1 -n tcp --dport 25 -m state --state ESTABLISHED -m string --string "http://196.41.X.Y/s/" -algo bm -m string --hex-string "|window.status=27|https://www.citibank.com" -j LOG --log-prefix "CITIBANK PISH"
```
