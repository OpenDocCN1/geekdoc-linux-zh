
`header_checks = regexp/etc/postfix/header_checks`

配合 `/etc/postfix/header_checks` 文件中包含以下内容的行：

```
^Subject: reject-me; REJECT You asked for it
```

将拒绝任何主题位以 "reject-me" 开头的消息。虽然支持正则表达式是一件好事，但在邮件处理的语文中，它也存在局限性。特别是，这并不是过滤垃圾邮件或病毒的有效方法。

## 使用 amavisd 进行内容过滤

工业级病毒过滤通常通过 `amavisd`（第 769 页）实现，这是一个 Perl 程序，用于连接邮件服务器软件与一个或多个杀病毒应用程序之间的接口。此类过滤器通过 Postfix 的 `content_filter` 参数进行配置，该参数指示 Postfix 将每条入站消息通过指定的服务一次。除了设置 `content_filter` 参数外，你还可以修改 `master.cf` 文件中的现有条目并添加新条目。

Postfix 和 `amavisd` 通过标准的 SMTP 和 LMTP 协议相互作用。Postfix 通过一个仅限本地机器访问的端口发送要由 `amavisd` 分析的邮件，`amavisd` 对其进行扫描，并通过一个禁用内容扫描的另一个端口通过 SMTP 发回 Postfix（以避免循环）。

对于来自互联网的入站邮件，`amavisd` 通常监听端口 `10024`，而 Postfix 的后门端口通常是 `10025`。如果我们还要处理出站邮件并希望将其与入站邮件区分，我们需要一个独立的 `amavisd` 端口用于——入站邮件可以通过与出站邮件相同的返回端口返回 Postfix。

下面列出的配置是一个“后置队列”（post queue），它在邮件接受进入 Postfix 队列后进行扫描。如果你想实现一种“扫描中”设置（即邮件在客户端的初始 SMTP 对话期间被扫描），请尝试 `amavisd-milter` 辅助工具，它允许将 Postfix 作为 milter 连接到 `amavisd`。

在 `amavisd` 侧，确保 `amavisd` 的配置包含类似下行的内容。（此配置为入站和出站消息使用了不同的端口。）

## 使用 amavisid 进行内容过滤

```
$inet_socket_port = [10024,10026];
$notify_method = 'smtp:[127.0.0.1]:10025';
$forward_method = 'smtp:[127.0.0.1]:10025';
$interface_policy[10026] = 'ORIGINATING';
$policy_bank['ORIGINATING'] = {
    originating => 1, # indicates client ours
```

你需要配置 Postfix 将邮件发送到 `amavisid`。

`amavisd-new` 分发包中的 `README.Postfix` 文件包含了最多 20 行 postfix 配置，你可以将其放入 `/etc/postfix/master.cf` 中，以使 `amavisid` 可访问并能够将邮件发回 Postfix。不要重复；这里只需从 README 复制并粘贴代码即可。

要让 Postfix 将邮件发送到 `amavisid` 进行扫描，请在 `main.cf` 中添加此行：

```
content_filter = amavisified:[127.0.0.1]:10024
```

为了区分入站和出站邮件，配置需要复杂一些。不仅是上述指令，你还需要如下修改 `smtpd_recipient_restrictions`（加粗部分所示）：

```
smtpd_recipient_restrictions =
n    reject_unknown_sender_domain
    reject_non_fqdn_recipient
    reject_non_fqdn_recipient
    check_sender_access regex:/etc/postfix/tag_as_originating.re
    permit_sasl_authenticated
    check_sender_access regex:/etc/postfix/tag_as_foreign.re
    check_client_access_hash:/etc/postfix/relaying_access
    reject_unauth_destination
    reject_unauth_pipelining
    reject_unknown_reverse_client_hostname
    reject_rbl_client zen.spamhaus.org
    permit
```

然后在 `tag_as_originating.re` 文件中放入以下行：

```
/ FILTER amavisified:[127.0.0.1]:10026
```

在 `tag_as_foreign.re` 中放入：

```
/ FILTER amavisified:[127.0.0.1]:10024
```

来自外部主机的邮件匹配 `tag_as_foreign.re` 限制，该限制指示 Postfix 通过将邮件发送到端口 `10024` 来过滤。所有邮件都匹配 `tag_as_originating.re` 限制，但对于外部主机，它会被替换为外部限制标记。

## 第 20 章 电子邮件

## 调试

当 Postfix 出现问题时，首先检查日志文件。你的问题答案可能就在那里；只是找到它们的问题。每个 Postfix 程序通常会为其处理的每条消息发布日志条目，出站邮件的示例可能如下：

```
Aug 18 22:41:33 postfix/pickup: uid=506 from=<dws@ee.ee>
```
