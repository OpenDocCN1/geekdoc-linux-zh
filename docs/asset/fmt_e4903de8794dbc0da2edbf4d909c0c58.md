
## 文件权限与日志配置

- 不要为任何配置文件、目录或 `sendmail` 需要读取的任何其他文件启用组写权限。

在任何情况下，都不应为任何配置文件启用组写访问权限。虽然 `sendmail` 允许你使用 `DontBlameSendmail` 选项禁用与文件权限/所有权相关的安全功能，但我强烈建议修复权限/所有权问题，然后在 `sendmail` 中禁用这些检查。如果你想保留现有的安全检查，请确保存放 `.forward` 文件的主目录对任何组都是可写的。`.forward` 文件本身应该设置为 `644` (`rw-r--r--`) 权限。

你还应该确保 `sendmail` 读取的文件路径中的任何目录都禁用了组写访问。如果你使用 `DontBlameSendmail` 选项引入安全漏洞，请参考 `sendmail` 随附的文档了解如何使用此功能。

一旦你确保文件/目录级权限已正确设置，且 `sendmail` 没有输出任何关于文件和目录权限/所有权的警告或错误信息，你应该确保日志已正确启用。默认情况下，`sendmail` 会通过 `syslog` 写入日志，因此你应该在你的 `/etc/syslog.conf` 中遵循以下行：

```
mail.*                /var/log/maillog
```

你可以根据喜好更改文件名；通常此文件命名为 `log`。同时确保你有如下条目：

```
mail.* {
    /usr/bin/mailx
}
```

## 确保反垃圾邮件

在这个垃圾邮件时代，你的 `sendmail` 服务器可能受到攻击。你应该采取其他安全措施来保护 `sendmail`。检查邮件服务器是否易受到攻击的最简单方法是访问 `http://maps.vix.com/tsi/ar.html`，这是由 MAPS 安全倡议提供的。你可以在主机框中输入邮件服务器的主机名并点击 GO 按钮以确定你的邮件服务器是否易受到攻击。图 11-2 显示了 `nitec.com`。

![](img/cbfef9f620ba4100baa62876f02b1_347_0.png)

图 11-2：测试 `nitec.com` 的漏洞

## 处理第三方中继漏洞

直到最近，`sendmail` 默认允许任何人中继。换句话说，与你无关的人可以使用你的邮件服务器向其他人发送邮件。在这种情况下，发送者和接收者对你都是未知的。以前这是允许的，因为提供了调试功能。然而，垃圾邮件发送者（即垃圾邮件邮件）现在互联网上泛滥，他们寻找中继站来执行大型任务。这滥用了你的系统，并让你面临法律问题。许多美国州正在通过反对未经许可邮件的法律，相关方可能对损害负责。如果你的邮件服务器卷入与未经许可邮件相关的法律案件，处理并证明清白可能需要额外的法律和资金资源。此外，如果你的服务器卷入此类邮件，许多接收者将简单地认为你参与了此事，并可能发送数百封愤怒邮件并将你举报到垃圾邮件黑名单。这可能会损害你或你组织的声誉，并干扰你的邮件连接操作，因为许多邮件服务器在同意与你的域名交换邮件之前会检查垃圾邮件黑名单。

`PrivacyOptions` 的值如下表所示：

| Option | 说明 |
| :--- | :--- |
| public | 开放。 |
| needhe | 必须使用 HELO。 |
| needexpn | 必须使用 HELO 或 EHLO。 |
| needvrfy | 必须使用 VRFY。 |
| notrn | 不允许 ETRN。 |
| noverb |不允许 VERB。 |
| noreceipt | 不返回成功。 |
| restrictmail | 限制使用 mail。当设置此选项时，仅允许超级用户和队列所有者使用。 |
| restrictrun | 限制 q。当设置此选项时，仅允许超级用户和队列所有者使用。 |
| goaway | 不允许 SMTP 查询。 |
| authwarnings | 在邮件中插入 X-Authentication-Warning 头部。 |

# 第 11 章：邮件服务

![](img/cbfef09f620ba4100baa62876f6f02b1_348_0.png)

图 11-3：第三方中继测试的输出

如你所见，`mail.nitec.com` 不允许第三方中继。请注意，如果你想允许一个或多个域名使用你的 `sendmail` 服务器进行中继，请将它们添加到 `/etc/mail/relay-domains` 文件中。此外，如果你想阻止垃圾邮件发送者发送垃圾邮件，请使用 `/etc/mail/access` 文件显式地拒绝它们访问你的邮件服务器。

## 将垃圾邮件发送者送入“黑洞”

邮件滥用防护系统（Mail Abuse Prevention System）所提供的实时黑洞列表（RBL）可用于自动阻止已知的垃圾邮件发送者使用你的 `sendmail` 服务器。RBL 的网站地址为：`http://maps.vix.com/`。

你可以将 RBL 视为一个已知垃圾邮件发送者的数据库。通过查询该数据库，你可以发现谁是垃圾邮件发送者，并拒绝来自相关域名的邮件请求。

为了理解 RBL 是如何工作的，请考虑一个示例。假设你想知道 IP 地址为 `127.0.0.2` 的某个域名是否列在 RBL 中。运行：

```
nslookup -q=a 2.0.0.127.rbl.maps.vix.com
```

这会将前述主机（`2.0.0.127.rbl.maps.vix.com`）的 IP 地址显示为 `127.0.0.2`。在这里，你获取了 IP 地址 `127.0.0.2`，通过反转 IP 字节并在末尾添加 `rbl.maps.vix.com` 将其转换为一个特殊的主机名，生成了 `2.0.0.127.rbl.maps.vix.com`。然后你查询了该主机的 A（地址）记录，它返回了你已经知道的 IP 地址（`127.0.0.2`）。换句话说，如果你知道一个可能的垃圾邮件发送者的 IP 地址，只需执行上述测试，看看是否返回了 IP 地址即可。如果你从查询中得到了相同的 IP 地址，则意味着该 IP 已列在 RBL 中。你可以执行另一次查询来获取文本记录（txt），如下：

```
nslookup -q-txt 2.0.0.127.rbl.maps.vix.com
```

这将显示：

```
2.0.0.127.rbl.maps.vix.com    text = "Blackholed - see <URL:http://maps.vix.com/cgi-bin/lookup?127.0.0.2>"
```

如果你用于创建特殊主机名的 IP 地址未列在 RBL 中，则你将无法从 A（地址）记录或 TXT（文本）记录中获得任何响应，并可以假设该 IP 未被列在列表中。由于 RBL 为了测试目的提供了 `127.0.0.2` IP 地址，它被列在 RBL 中，因此你才在名称服务器查询中得到了上述响应。

因此，MAP RBL 是一种基于 DNS 的垃圾邮件检查和拦截系统，可以通过查询它来确定某个 IP 地址是否被作为垃圾邮件发送者进行拦截。你可以通过两种方式使用 RBL：你可以与 MAPS RBL 签署协议，将整个数据库传输到本地主机，并为自己创建一个本地 RBL。或者，你可以根据情况查询主 RBL 数据库。最新版本的 `sendmail` (`8.9.r`) 附带 `sendmail`。适用于最新版本的 Red Hat Linux RPM 允许在 `/etc/sendmail.cf` 中启用 RBL，因此你不需要进行任何操作来配置它。以下是如何在你的 `sendmail` 中测试 RBL 配置。运行：

```
sendmail -bt
```

在地址测试提示符处输入：

```
.O(client_addr)127.0.0.1
Basic_check_relay <>
```

输出如下：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
  > .client_addr>127.0.0.1
  > Basic_check_relay <>
    rewrite: ruleset 190    input: <>
    rewrite: ruleset 190 returns: OKSOFAR
```

这告诉你地址 `127.0.0.1`（环回地址）未在 RBL 中被拦截，因为重写结果为 `OKSOFAR`。现在使用 `127.0.0.2` 重复上述测试（这是 RBL 提供的 IP，在 RBL 中被拦截）。你应该会看到类似如下的输出：
