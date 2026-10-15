
否则，为了安全投递，你需要一个 `root` 进程和一个 `setgid` 二进制文件。在这种情况下使用 `root` 实际上增加了安全性，因为它允许邮件服务器降低权限并作为目标用户解析转发（用户配置到邮件地址或程序）文件，这是执行最安全的方法。

因此，你可以选择使用由无权限 MTA 调用的 `setuid` 本地投递代理到我们提到的 `root` `setgid` 位来转移特权提升（或从 `root` 到其他用户的权限降低）。

`smrush` 可以对可接受的命令应用限制并避免常见的 shell 攻击。用法请参考 `smrman` 页面。可以通过指令作为功能启用它：

```
FEATURE(`smrush`,`/usr/bin/smrush`)
```

你还可以通过 `local_command_shell` 变量配置 `Postfix` 的本地投递使用受限 shell。

# 头部与信任关系

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 5 |
| 影响力 | 5 |
| 风险等级 | 5 |

我们提到过，头部永远不应该被信任，也不应被视为可靠的信息源。这产生了一个巨大的需求，即如何有效地过滤或拒绝未经授权的邮件，因为正如我们之前所说的，你应该只中继来自本地或信任源的邮件。

最近引入了两种用于验证外部邮件的协议：发送者策略框架 (`SPF`) 和域密钥 (`DomainKeys`)。这两个系统涉及邮件消息的不同部分，并且可以同时使用。

## 发送者策略框架 (SPF)

`SPF` 是一种简单的方法，将允许从特定域名发送消息的 IP 地址信息绑定到 DNS 文本记录中。这样，你的 DNS 服务器就可以告诉世界，来自你域名的邮件应仅来自某些特定地址；其他 MTA 在接收消息时可以查询你的 DNS 记录，并将该信息与显然来自你域名的入邮件头部进行交叉比对。

让我们来看一个 `SPF` 记录示例：

```
<Verbatim listing 18>
$ dig -t txt gmail.com
; <<>> DIG 9.3.2 <<>> -t txt gmail.com
; global options: printcmd
; Got answer:
; ->>HEADER-- opcode: QUERY, status: NOERROR, id: 21409
; flags: qr ra; QUERY: 1, ANSWER: 1, AUTHORITY: 4, ADDITIONAL: 4
;; QUESTION SECTION:
;; gmail.com.
                                     IN      TXT
;; ANSWER SECTION:
gmail.com.                               300    IN      TXT      "v=spf ip4:216.239.56.0/23
ip4:64.233.160.0/19 ip4:66.249.80.0/20 ip4:72.142.192.0/18 ?all"
</Verbatim listing>
```

查询 `gmail.com` 域名，你可以看到 Google 正在指示只有这些 IP 类（根据 Google 的规定）允许从 `@gmail.com` 发送消息。

在处理这项技术时，有几个重要的点需要考虑。首先，它仅用于正性结果（以及白名单），这意味着如果你发现一个 `SPF` 条目且消息匹配成功，那么对其进行验证并提高你的评分是安全的。

## 第 14 章：邮件服务

然而，缺失的 `SPF` 记录或负向查询都不应在你的过滤决策中占据过大权重，因为它不是一种标准的、因此也未被完全采用的技术。`SPF` 域名允许你明确说明你应该发布的信息具有多大的置信度。级别有 `PASS`（始终允许邮件通过）、`NEUTRAL`（不执行策略）、`SOFTFAIL`（留有解释空间）和 `FAIL`（拒绝）。

`SPF` 信封头部之一，如所示，它并不处理 `From` 头部或正文中的任何内容，这通常会欺骗大多数人。

`SPF` 在 DNS 方面非常容易发布。在应用层实现它要困难一些。有两个库（`libspf` 和 `libspf2`）以及十几个 Perl 应用程序，它们允许轻松地集成到 MTA 中，而且 `Spamassian` 显式支持 `SPF` 用以改进评分。至于过滤应用程序，一种安全的实现涉及添加一个包含验证结果的自定义头部。

注意 `SPF` 转发，当任何转发转发时并不意味着你的转发邮件对于 `SPF` 感知的 MTA 看起来是无效的（如果该域名发布了记录）。这是一个在实现这项技术时应该考虑的严重问题。一个提出的但更好的不完全解决方案是发送者重写方案 (`SRS`) 它它在转发时会重写 `Return-Path`。

未来看到一个完整的 `SPF` 实现将要求在任何转发机制中完全采用 `SRS`，这是不太可能的。这也是只对正性结果和白名单化信任该机制的另一个原因。

`SPF` 并不是一种广泛实现的技术，但大型提供商（特别是 AOL 和 Google 的 Gmail）正在使用它来增加反垃圾邮件评分的准确性。

## 域密钥 (DomainKeys)

`DomainKeys` 是用于验证邮件发送者和消息完整性的机制。它的工作原理是在发送消息时使用其域名公钥对消息头部进行加密签名。密钥发布在 DNS 记录中，因此接收方 MTA 执行端验证时可以获取它以供稍后检查。

这里是 `DomainKey` 记录：19>

```
<Verbatim listing 19>
# -t txt beta.domainkey.gmail.com
; <<>> DIG 9.3.0 <<-> -t txt beta._domainkey.gmail.com
; global options: printcmd
; Got answer:
; ->|HEADER<< opcode: QUERY, status: NOERRER, id: 23202
; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 4, ADDITIONAL: 4
; QUESTION SECTION:
;beta._domainkey.gmail.com. IN TXT
; ANSWER SECTION:
beta.domainkey.gmail.com. 300 IN TXT "t=y\; k=rsa";
```

*

## 攻防 Linux：安全秘密与解决方案

```
p-MIGMA0GGSQIb3DBEQUAA4GNADCB1QBqGC9C3nOf+G/3mg5r
t4p6nMkVVlD0lc2x6BwX2kNXJ1KM10f8MTX6pB6JN7UR1BEdubagqtzm2r
WK4LIJmhoQwcqZiGlbKp/24XZEWWMFC1LYY0UitK7j
```

`SPF` 转发时，当任何转发转发并不意味着你的转发邮件对于 `SPF` 感知的 MTA 看起来是无效的（如果该域名发布了记录）。这是一个在实现这项技术时应该考虑的严重问题。

未来看到一个完整的 `SPF` 实现将要求在任何转发机制中完全采用 `SRS`，这是不太可能的。这也是只对正性结果和白名单化信任该机制的另一个原因。

`SPF` 并不是一种广泛实现的技术，但大型提供商（特别是 AOL 和 Google 的 Gmail）正在使用它来增加反垃圾邮件评分的准确性。

`DomainKeys` 是用于验证邮件发送者和消息完整性的机制。它的工作原理是在发送消息时使用其域名公钥对消息头部进行加密签名。密钥发布在 DNS 记录中，因此接收方 MTA 执行端验证时可以获取它以供稍后检查。

除了 DNS 记录发布，`DomainKeys` 可以作为针对你 MTA 的特定应用程序实现。

`DomainKeys` 最主要用于 Yahoo!（该协议最初的开发者）和 Google 的 Gmail。

如果头部被重新排列或消息正文被更改，签名验证将失败，邮件列表软件（通常在消息末尾添加页脚）以及反垃圾邮件/病毒软件添加自定义头部也会导致问题。消息转换和换行也会导致问题。

建议的解决方案是邮件列表软件在发送时应识别消息，而反垃圾邮件/病毒软件在执行 `DomainKeys` 验证后解析消息。此外，发送者可以在 DNS 记录中指定哪些头部将进行计算。

与 `SPF` 类似，这些使得 `DomainKeys` 一个仅用于正性结果和白名单的机制。此外，由于计算加密校验和，处理每条消息时 CPU 负载会增加。

这里是 `DomainKey` 记录：19>
