
# Be sure to keep the ":" after "su" to avoid matching "sudo".

```
watchfor = /su:/

echo=bold

exec="call_pager.pl 5551234 888"

pipe=" /usr/bin/lpr"

watchfor = /,*/

echo
```

...的一些 SunOS 相关内容）。当你不在终端前时，如需实时通知，可以使用 `exec` 和 `pipe` 关键字。`swatch-2.2` 附带了一些可在配置文件中使用的实用工具（如 `badloginfinger.pl` 和 `call_pager.pl`），但 `3.0` 版本似乎不再包含这些工具。如果你需要，可以从旧版本 `2.2` 中提取它们，或者替换为你可能已经拥有的类似实用工具。我们的示例展示了对 `badloginfinger.pl` 的调用，该工具可以安全地查询发出非法登录请求的站点。我们还通过 `call_pager.pl` 实用工具将非法登录尝试的通知发送到我们的寻呼机，并使用 `pipe` 关键字将 `su` 的输出回声到打印机。

由于 `swatch` 仅报告你指示它报告的内容，你可能需要考虑在文件末尾保留全模式报告（`/.*/`），并随着操作的进行仔细添加需要忽略的模式。为了本说明的目的，我们的配置文件将保存在 `/usr/local/etc/swatch/swatchrc.messages` 中。你需要为你希望使用 `swatch` 监控的每个日志文件创建配置文件。

如果我们的消息文件每天都被轮转，我们可以告诉 `swatch` 在轮转发生后立即重启自身。用于持续监控此文件并在每天早上重启的命令可能如下所示：

```
swatch -t /var/log/messages -c /usr/local/etc/swatch/swatchrc.messages -r 04:01
```

你也可以通过 `logrotate` 调用重启。示例 `17-11` 提供了一个示例条目，可以放置在 `/etc/logrotate.d` 中用于 `/var/log/messages`。

### 示例 17-11 通过 logrotate 重启监控 /var/log/messages 的 swatch

```
/var/log/messages {

    prerotate

        /usr/bin/chattr -a /var/log/messages

    endscript

    postrotate

        /usr/bin/killall -HUP syslogd

        /usr/bin/chattr +a /var/log/messages

        /usr/local/etc/swatch -t /var/log/messages -c /usr/local/etc/swatch/swatchrc.messages -r +0

    endscript

}
```

使用示例 `17-10` 中所示的命令和配置文件，我们可能会在监控窗口中看到类似示例 `17-12` 的输出（因长度原因折行）。

如果在 `swatch` 运行期间更新配置文件，请向 `swatch` 进程发送 `ALRM` 或 `HUP` 信号。它将重新读取其配置文件并重启。当你向 `swatch` 发送 `QUIT`、`TERM` 或 `INT` 信号时，它将正常终止。

`swatch` 在确保你收到通知方面表现相当出色。通过微调配置文件，它应该能很好地为你工作，但也请使用额外的工具。

### 示例 17-12 基于示例 17-10 由 swatch 生成的输出样本

```
Mar 2 17:54:15 topcast login[14435]: FAILED LOGIN 1 FROM roadrunner FOR guest,  

Authentication failure

Mar 2 17:54:23 topcast login[14435]: FAILED LOGIN 2 FROM roadrunner FOR guest,  

Authentication failure

Mar 2 17:54:28 topcast login[14435]: TOO MANY LOGIN TRIES (3) FROM roadrunner FOR  

guest, Have exhausted maximum number of retries for service.

Mar 2 17:54:28 topcast PAM_pwdb[14435]: 3 authentication failures; (uid=0)  

->guest for login service

Mar 2 18:00:10 topcast login[14478]: FAILED LOGIN 1 FROM roadrunner FOR guest,  

Authentication failure

Mar 2 18:00:16 topcast login[14478]: FAILED LOGIN 2 FROM roadrunner FOR joe,  

Authentication failure

Mar 2 18:00:20 topcast login[14478]: FAILED LOGIN 2 FROM roadrunner FOR mary,  

Authentication failure

Mar 2 18:50:38 net-print.mydomain.com printer: paper out

Mar 2 18:50:38 net-print.mydomain.com printer: error cleared

Mar 2 18:50:38 net-print.mydomain.com printer: cover/door open

Mar 2 18:50:38 net-print.mydomain.com printer: error cleared

4 in 0:28:06 net-print.mydomain.com printer: paper out

4 in 0:28:06 net-print.mydomain.com printer: error cleared

4 in 0:28:06 net-print.mydomain.com printer: cover/door open

4 in 0:28:06 net-print.mydomain.com printer: error cleared
```

## logcheck

`logcheck` 是一个实用工具，旨在定期检查日志文件中的新内容，寻找“异常”项目，同时忽略你不关心的项目。然后，它将感兴趣的事件（如果有）以清晰的摘要形式通过邮件发送给你。`logcheck` 的理念是报告已知的不良事件（通过在配置文件中匹配关键字），并报告所有其他未被指示忽略的内容。虽然 `swatch` 可以以实时方式使用，但你也可以使用 `logcheck` 接收关于那些可能时效性不那么强但同样重要的其他日志条目的通知。

`logcheck` 附带了一个辅助实用工具，它足够智能，可以通过检查 `inode` 号和文件大小来知道你的日志文件何时被轮转。它还跟踪日志文件中已处理的部分，因此你只会收到新事件的报告（如果没有事件则无报告）。`logcheck` 不应遗漏任何重要事件，因为它的默认行为是报告你告诉它要报告的所有内容，以及你没有明确告诉它要忽略的所有内容。

`logcheck` 是 `Trusted Information Systems, Inc.` 随 `Gauntlet` 防火墙分发的 `frequentcheck.sh` 脚本的一个免费克隆。`Craig H. Rowland` 是 `logcheck` 的作者，他获得了 `TIS` 的许可以发布此克隆版本。更多信息请参阅随 `logcheck` 分发的 `LICENSE` 文件。

## 获取 logcheck

你可以从其主页或 `COAST` 获取 `logcheck`：

- `http://www.psonic.com/abacus/logcheck/`
- `ftp://coast.cs.purdue.edu/pub/tools/unix/logcheck/`

截至本文写作时，`logcheck` 的最新版本为 `1.1`。要获取 `logcheck` 的最新版本、作者的 `PGP` 密钥以及 `logcheck` 的签名文件：

```
logcheck-1.1.tar.gz

logcheck-1.1.tar.gz.asc

signature-file.asc
```

将作者的 `PGP` 签名添加到你的密钥环，并验证包的签名是否正确，如下所示：

```bash
# gpg signature-file.asc

# gpg logcheck-1.1.tar.gz.asc
```
