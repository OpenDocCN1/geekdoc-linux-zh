

## reject_unknown_client

如果客户端 IP 在 DNS 中没有 PTR 记录，则请求将被拒绝。这意味着 IP 地址无法解析为主机名的客户端无法向此主机发送邮件。

## check_client_access maptype:mapname

此选项需要包含一个已配置的映射，如前所述。这将根据映射的内容进行限制，仅允许映射允许的客户端。映射可能包含网络、父域或客户端地址，Postfix 将剥离不必要的信息以将客户端匹配到所需的具体级别。

## check_sender_access maptype:mapname

这将根据映射的内容进行限制，仅允许映射允许的发件人。映射可能包含网络、父域或 localpart@。

## reject_maps_rbl

RBL 是中继域黑洞列表。通过对接收域黑洞列表传输的域名服务器进行反向域名查找测试，服务器可以知道邮件是否通过已知的开放邮件中继发送。有许多免费和付费服务提供黑洞数据。最大且历史最悠久的是 MAPS 运营的服务 [http://www.mail-abuse.org/]，而另外两个类似服务由开放中继数据库 [http://ordb.org/] 和分布式发件人抵制列表 [http://dsbl.org/] 运营。所有这些都基于允许管理员选择拒绝从开放邮件中继发送的邮件的原则。如果列出此选项，客户端将被检查与可用的 RBL 域，如果有任何匹配，邮件将被拒绝。

> 注意 如果在网络上使用任何免费的 RBL 服务，请考虑向项目维护者捐赠金钱、时间和资源。项目通常由志愿者劳动运行，使用维护者支付的网络资源。

## reject_invalid_hostname

如果客户端主机名无效，由于语法错误，请求将被拒绝。

## permit_naked_ip_address

如果客户端 HELO 或 EHLO 命令包含裸 IP 地址，而没有邮件 RFC 要求的 [] 括号括起来，消息将被拒绝。请注意，一些流行的邮件客户端发送的 HELO 问候语就是这样损坏的。

## reject_unknown_hostname

如果客户端 HELO 命令中的主机名在 DNS 中没有 A 或 MX 记录，则拒绝请求。

## reject_non_fqdn_hostname

如果客户端主机名不是 RFC 要求的完全限定域名形式，则消息将被拒绝。

```
check_helo_access maptype:mapname
```

服务器将在命名的访问数据库映射中搜索 HELO 主机名或父域。如果数据库搜索结果为 REJECT 或 4xx 文本或 5xx 文本错误代码，消息将被拒绝，而响应为 OK 或 RELAY 或全数字响应将允许消息。

```
permit
```

这只是允许任何内容。通常这将位于一组限制的末尾，以便允许未明确禁止的任何内容。

```
reject
```

拒绝一切。这可以在一组限制的末尾使用，以禁止未明确允许的任何内容。

```
warn_if_reject
```

这是一个特殊选项，它改变了以下限制的含义，使得本应被拒绝的消息将被记录但仍被接受。这可用于在生产邮件服务器上测试新规则，而不会因规则问题而拒绝邮件的风险。

```
reject_unauth_pipelining
```

如果客户端在未先确认服务器支持 SMTP 命令流水线的情况下提前发送命令，则消息将被拒绝。这将防止某些编写不佳的批量邮件软件错误使用流水线来加快大规模投递。

## Restrictions on client hostnames/addresses

此限制适用于客户端主机名和/或地址。默认情况下，Postfix 将允许任何主机的连接，但您可以使用以下方式添加额外限制：reject_unknown_client、permit_mynetworks、check_client_access maptype:mapname、reject_maps_rbl、maps_rbl_reject_code、permit、reject、warn_if_reject、reject_unauth_pipelining。

## Restrictions on sends in HELO commands

此选项指定客户端在 HELO 和 EHLO 命令中可以发送的额外信息限制。此选项对应于 smtpd_helo_restrictions 指令。默认情况下 Postfix 接受任何内容，并且可以添加以下限制：reject_invalid_hostname、permit_naked_ip_address、reject_unknown_hostname、reject_non_fqdn_hostname、check_helo_access maptype:mapname、reject_maps_rbl、reject_unknown_client、check_client_access maptype:mapname、permit、reject、warn_if_reject、reject_unauth_pipelining。

## Restrictions on sender addresses

此选项限制邮件中 MAIL FROM 命令中可以包含的内容。它可用于防止特定电子邮件地址发送邮件，拒绝没有可解析主机名的客户端，等等。此选项对应于 smtpd_sender_restrictions 指令，可能包含以下任何内容

```
restrictions: permit_mynetworks:, reject_unknown_client, reject_maps_rbl,
reject_invalid_hostname, reject_unknown_hostname, reject_unknown_sender_domain,
check_sender_access maptype:mapname, check_client_access maptype:mapname,
check_helo_access maptype:mapname, reject_non_fqdn_hostname, reject_non_fqdn_sender,
reject, permit.
```

## Restrictions on recipient addresses

此参数对发送消息的 RCPT TO 命令中可以包含的收件人进行限制。它可用于规定邮件可以发送到何处。此选项对应于 smtpd_recipient_restrictions，可能包含以下任何限制：permit_mynetworks、reject_unknown_client、reject_maps_rbl、reject_invalid_hostname、reject_unknown_hostname、reject_unknown_sender_domain、check_relay_domains、permit_auth_destination、reject_unauth_pipelining、permit_mx_backup、reject_unknown_recipient、check_recipient_access、check_client_access、check_helo_access、check_sender_access、reject_non_fqdn_hostname、reject_non_fqdn_sender、reject_non_fqdn_recipient、reject、permit。

## DNS domains for blacklist lookups

此选项配置可选的黑名单 DNS 服务器，这些服务器将用于所有访问限制中指定的所有 RBL 检查。它可能包含任意数量的服务器，以空白分隔的列表。这些服务可用于帮助防止垃圾邮件，如本节前面所述，使用 Restrict ETRN 命令参数。此选项配置 maps_rbl_domains 指令，默认为空。

## Restrict mail relaying

此选项指定 Postfix 将为其中继邮件的主机、网络、域等。此选项对应于 relay_domains 指令，默认为 $mydestination。

## SMTP server response on access map violation, SMTP server response on RBL domains violation, SMTP server response on forbidden relaying, SMTP server response on unknown client reject, SMTP server response on invalid hostname reject, SMTP server response on unknown domain reject, SMTP server response on unknown hostname reject

这些选项配置当应用任何指定限制时将发送给客户端的错误结果代码。这些错误具有合理的默认值，通常不需要更改。如果您希望了解有关 SMTP 错误代码的更多信息或有更改这些值的理由，请参阅 RFC 822。

## SMTP Client Options

SMTP 客户端选项配置 Postfix 在作为客户端处理其他邮件服务器时，例如代表用户发送邮件时的行为。配置的这一部分主要规定服务器将如何响应某些错误条件。

## Action when listed as best MX server

如 BIND 章节所述，邮件服务器执行名称服务器查询以查找目标域的 MX 或邮件服务器记录。如果该记录指示本地服务器是邮件应发送到的服务器，它可以以几种方式响应。默认情况下，邮件将以指示邮件循环的错误退回。如果选择该字段并输入 local，则邮件将被定向到本地投递代理，而不是退回邮件。此选项对应于 best_mx_transport 指令。

## Hosts/domains to hand off mail to on invalid destination

默认情况下，无法投递的邮件因为目标无效而会以适当的错误消息退回。但是，可以配置 postfix 将电子邮件移交给另一台服务器。此选项对应于 fallback_relay 指令。

## Ignore MX lookup error

如果名称服务器查询未能提供 MX 记录，服务器默认会延迟邮件并稍后重试。如果改为选择 Yes，将执行 A 记录查询，并尝试将邮件投递到 resulting 地址。此选项对应于 ignore_mx_lookup_error 指令。

## Skip 4xx greeting

如果远程服务器以 4XX 状态代码响应连接，Postfix 默认会选择 MX 记录指定的下一个可用邮件交换器。如果设置为 No，邮件投递将在第一次投递尝试后被延迟，并在稍后再次尝试。此选项对应于 smtp_skip_4xx_greeting 指令。

## Skip wait for the QUIT command

此选项配置 Postfix 是否等待接收邮件服务器响应 QUIT 命令。此选项对应于 smtp_skip_quit_response 指令，默认为 no。

