
# 第 10 章：邮件服务

总结来说，对于每个虚拟邮件域名，创建一个 `.ltr` 文件将虚拟电子邮件地址映射到真实地址，并创建另一个文件将真实地址映射到邮件地址。一旦制作了这些文件，你就将它们合并以创建 `/etc/mail/virtusertable`（针对 `*.ltr`）和 `/etc/mail/genericstable`（针对 `*.rtf`）。然后，如上所示运行 `makemap` 来创建这些文件的数据库版本。只要你在 `/etc/mail/sendmail.cc` 和 `/etc/mail/relay-domains.files` 中列出了每个虚拟域名，过程就完成了。

## 测试你的 `sendmail` 配置

由于有很多配置文件需要安排，很有可能某些地方不会按照你预期的方式工作。因此，我们建议执行以下操作：

- 在进行任何更改之前，始终备份你的配置。

- 每当你对 `sendmail` 配置进行更改时，在继续后续操作之前对其进行测试。

### 测试 `sendmail` 地址重写规则

你可以测试 `sendmail` 规则的行为。要执行此类测试，请按如下方式运行 `sendmail`：

```bash
sendmail -bt
```

这将以地址模式运行 `sendmail`，并为你提供一个提示符与其进行交互。在提示符处，你可以输入如下测试命令：

```
<rewrite rule #s> <test address>
```

例如，要查看 `sendmail` 的重写规则 0 将对 `paul@paunchy.net` 执行什么操作，请运行

`0 paul@paunchy.net`

我的 `sendmail` 系统上的输出所示：

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 0 paul@paunchy.net
rewrite: ruleset 0 input: paul @paunchy . net
rewrite: ruleset 199 input: paul @paunchy . net
rewrite: ruleset 199 returns: paul @paunchy . net
rewrite: ruleset 0 input: paul @paunchy . net
rewrite: ruleset 98 returns: paul @paunchy . net
rewrite: ruleset 198 input: paul @paunchy . net
rewrite: ruleset 198 returns: ## local $: paul @ paunchy . net
rewrite: ruleset 0 input: paul @paunchy . net
```

如前面的示例所示，创建多个虚拟用户映射文件可以帮助你轻松地跟踪各个域名。每当你想要更改特定域名的映射时，只需修改该域名的 `ftr` 文件，并使用这里讨论的技术创建最终的 `/etc/mail/virtertable` 文件即可。
