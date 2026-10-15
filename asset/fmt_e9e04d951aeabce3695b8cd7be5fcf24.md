
# Fedora 或 Red Hat Linux 的其他邮件服务器

sendmail 的开源版本并不是 Fedora 和 Red Hat Enterprise Linux 系统唯一的可用邮件服务器，但它绝对是最常用的。以下列表描述了其他服务器，并提供了进一步信息的 URL：

- `Postfix` — 与 sendmail 类似，`Postfix` MTA 也包含在 Fedora 中。该邮件服务器由 Wiese Venena（以 top_wrappers 出名）设计，以安全为考虑因素，并在限制的 root 环境中以特权用户身份执行大多数功能。该服务器包含十多个小程序（执行不同的任务）和几个单用途队列。你可以在 `www.postfix.org` 找到更多信息和源代码。
- `Exim` — `Exim` MTA 是一个运行在 Linux 和其他 Unix 系统上的免费邮件服务器（遵循 GPL）。`Exim` 包含在 Fedora 发行版中。此 MTA 包含配置和路由邮件的功能。可以通过 `Exim` 主页 (`www.exim.org`) 了解更多信息。
- `Qmail` — 该邮件服务器也以安全为首要考虑因素（由 Daniel J. Bernstein 编写），提供安全可靠的消息传输、信箱配额、虚拟域名和反垃圾邮件功能。可以在 `www.gmail.com/top.html` 获取更多信息。
- `Smail` — `Smail` 提供了与 sendmail 许多相同的功能，但配置稍简单，且所需的内存较少。`Smail` 最适用于中小型邮件服务器。Snail 项目页面位于 `www.weird.com/~woods/projects/snail.html`。源代码可以从 `ftp://ftp.planix.com/pub/Snail/` 下载。

# 启动 sendmail

一旦安装完成，sendmail 服务默认开启。要立即启动 sendmail，你可以重启机器或运行 `service sendmail start` 来启动服务器。启动和停止 sendmail 的过程与其他任何其他服务器类似。

默认情况下，sendmail 接收到的传入消息会被处理并存储在 `/var/spool/mail` 目录。该目录中的每个文件代表本地机器上的一个用户名。当第一封电子邮件发送给用户时（或者如果该文件缺失），该文件将自动创建。拥有登录账户的用户使用此目录并将其用户账户名作为他们的入站信箱（例如，`/var/spool/mail/johng`）。

发出的消息将进入 `/var/spool/mqueue` 目录等待发送。该目录中的文件名遵循命名方案。前两个字符表示存储在文件中什么类型的数据（见表 19-1）。后续字符根据处理该消息的 sendmail 进程的 PID 形成唯一标识符。

## 表 19-1：`/var/spool/mqueue` 中的文件前缀

| 文件名前缀 | 存储的数据类型 |
| :--- | :--- |
| df | 构成电子邮件正文的数据。 |
| qf | 包含消息头和其他管理详细信息的控制文件。 |
| tf | qf 文件的临时副本，在发生交付错误时创建。 |
| xf | 尝试发送消息时生成的任何错误信息。 |

# 其他程序

发行版包含几个可执行程序。它们在表 19-2 中描述。

## 表 19-2：其他相关的 sendmail 程序

| 程序 | 描述 |
| :--- | :--- |
| mailq | 显示邮件队列中等待处理的消息摘要（该命令等同于 `sendmail -bp`）。 |
| mailstats | 显示消息数量和计数统计。 |
| makemap | 将文件 (`/etc/mail/virtertable`) 转换为哈希伯克利数据库 (`/etc/mail/virtertable.db`)）。此命令在每次 sendmail 脚本启动时运行。 |
| newaliases | 将纯文本 `/etc/aliases` 转换为哈希伯克利数据库文件 `/etc/aliases.db`（该命令等同于 `sendmail -bi`）。 |
| 程序 | 描述 |
| :--- | :--- |
| pialiases | 打印 `/etc/aliases` 中定义的所有别名。 |
| procmail | 不包含在 sendmail 软件包中，但用作 sendmail 的 MDA。（它包含在 Fedora 和 RHEL 的 procmail 软件包中。） |
| purgestat | 清除存储主机状态信息的目录。该命令等同于 `sendmail -b`，默认是禁用的。 |
| rmail | 通过 UUCP (Unix 到 Unix) 处理入站邮件。 |
| smrsh | 实现一个用于从 sendmail 运行程序的受限外壳。 |

# sendmail 执行的日志

sendmail 执行的日志量可以在 `sendmail.mc` 文件中配置，但默认级别为信息性通知和错误消息提供了良好的覆盖。默认情况下，syslog 配置文件 (`/etc/syslog.conf`) 告诉 syslog 将 sendmail 的信息存储在 `/var/log/maillog` 中。每当 sendmail 启动时，类似的信息会被写入 `/var/log/maillog`：

```
May 12 10:00:00 host sendmail[1234]: config file /etc/mail/sendmail.mc read

May 12 10:00:00 host sendmail[1234]: access file /etc/mail/access read

May 12 10:00:00 host sendmail[1234]: database file /etc/mail/aliases.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/virtual_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/access_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/card_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/recipient_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/policy_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/transport_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/info_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/generic_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/expire_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/local_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/address_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/header_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/body_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/aliases_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/virtual_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/policy_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/transport_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/info_map.db read

May 12 10:00:00 host sendmail[1234]: map file /etc/mail/generic_map.db read
```
