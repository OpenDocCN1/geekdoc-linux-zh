
你使用 `CUPS` 管理工具管理打印机、类以及各种管理任务。`CUPS` 在第 26 章中描述。

`Samba` 和其他工具包含在许多 Linux 发行版中。其他提供基于 Web 管理的项目（可能包含包含包含你的发行版中）包括 `SquirrelMail`（一个 Web 界面）和 `Mailman`（邮件列表设施）。

由于许多管理界面以明文发送数据，因此它们最适合在本地系统上使用。但由于它们是基于 Web 的，你也可以从局域网或其他网络使用这些界面。然而，如果你计划将这些管理界面扩展到不可信的网络，你应该考虑对你的通信进行加密。

## Webmin 管理工具

`Webmin` 工具（`www.webmin.com`）提供了管理 Linux 和 UNIX 的功能。虽然 `Webmin` 并非所有 Linux 系统都自带的，但 `Webmin` 项目已将 `Webmin` 移植到了 70 多种操作系统。支持的 Linux 发行版包括 `SUSE`、`Red Hat (RHEL)`、`Debian`、`Ubuntu`、`Gentoo`、`Slack`、`Mandriva`、`Yellow Dog` 等（完整列表见 `webmin.com/support.html`）。

一旦从 `Webmin.com` 获取并安装 `Webmin`，你就可以从浏览器使用它。要启动 `Webmin` 界面，在浏览器中输入：

```
http://localhost:10000
```
