
## 2. 确保 `assassin` 守护进程正在运行
如果没有，请按照以下方式启动（作为 root 用户）：

```
chkconfig spamassassin
```

## 3. 创建 `/etc/procmail` 文件
使用任何文本编辑器创建 `/etc/procmail` 文件（作为 root 用户）。此 procmail 文件将收到的所有邮件通过 `spamc`（它是上一步中开启的垃圾邮件客户端）：

```
:0fw
| /usr/bin/spamc
```

如果你喜欢，可以在 procmail 文件中进行更多操作以全局处理邮件。例如，你可以创建 procmail 规则来报告垃圾邮件并将其分类。同样，每个用户可以创建个人的 `.procmail` 文件。

## 4. 检查 `/etc/mail/spamassassin/local.cf` 文件
该文件包含了 SpamAssassin 全局使用的规则，除非被用户的个人 `$HOME/.spamassassin/user_prefs.cf` 文件覆盖。这里是 `local.cf` 文件的内容：

```
required_hits 5

report_header Subject [SPAM]
```

在 SpamAssassin 中，使用评分系统来判断特定消息是否为垃圾邮件。`required_hits` 行显示需要 5 分才能标记为垃圾邮件。对于公共邮件服务器，你应该将其调高（设置为 8 或 10）。将 `rewrite_header` 设置为 `[SPAM]` 允许 SpamAssassin 在垃圾邮件的主题行中添加 `[SPAM]` 文本供 `local.cf` 使用。（运行 `man Mail:SpamAssassin::Conf` 可查看其他设置。）

由于误报的发生，使用全局过滤会导致用户无法看到他们需要的邮件。为了解决这个问题，这种方法让用户决定如何处理标记为垃圾邮件的邮件。用户甚至可以调整他们对垃圾邮件判定的阈值。

接下来，你应该让邮件服务器的用户在他们的主目录下设置自己的偏好。用户在 `$HOME/.spamassassin/user_prefs.cf` 文件中的偏好有助于告诉 SpamAssassin 如何处理该用户的邮件。以下是用户可能希望在该文件中的行示例：

```
required_score 3
whitelist_from jsmith@example.com bjones@example.com
blacklist_from *.example.org
```

`required_score` 行（默认设置为 5，但此处设置为 3）设置了认为消息为垃圾邮件的分数。分数基于匹配或不匹配 `Assassin` 执行测试时所遵循的判定标准。（参见 http://spamassassin.apache.org/tests.html。）

你设置的 `whitelist_from` 和 `blacklist_from` 行针对个人、单个主机或整个域名，这些地址不应被视为垃圾邮件（`whitelist_from`）或应始终被视为垃圾邮件（`blacklist_from`）。若要通过修改 SpamAssassin 行为的其他方法，请使用以下命令：

```bash
man ::SpamAssassin::Conf
```
