
- `append_dot_mydomain`：决定 Postfix 是否应向发送到 user@host 的邮件附加域名名。现在，这通常由 MUA 处理，因此它是禁用的。
- `delay_warning_time`：取消此参数的注释将指定如果发送的邮件尚未投递，一段时间后通知用户。毕竟，远程站点可能在使用 Microsoft Exchange，并且可能处于离机状态。
- `smtpd_tls_cert_file`：识别此系统上文件的完整路径，该文件持有机器在使用 TLS（传输层安全）发送消息时使用的证书。
- `smtpd_tls_key_file`：识别此系统上文件的完整路径，该文件持有在使用 TLS（传输层安全）发送消息时为 Postfix SMTP 客户端提供的 RSA 私钥。
- `smtpd_use_tls`：决定当远程 SMTP 服务器宣布 STARTTLS 支持时，此 Postfix 服务器是否应使用 TLS。如果远程服务器未宣布 STARTTLS 支持，消息将以明文发送。
- `smtpd_tls_session_cache_database`：识别 `tlsmgr` 守护进程使用的 SMTP 服务器 TLS 会话缓存的组织和位置。
- `smtp_tls_session_cache_database`：识别 `tlsmgr` 守护进程使用的 SMTP 客户端 TLS 会话缓存的组织和位置。
- `myhostname`：识别此系统的实际 Internet 主机。默认情况下，此值是 `hostname()` 返回的值。
- `alias_maps`：识别用于本地邮件投递的别名的组织和完整路径。
- `alias_database`：识别用于本地邮件投递的别名的组织和完整路径，并进行更新。
- `myorigin`：Debian 及其衍生发行版（如 Ubuntu）的一个选项，允许你使用 `/etc/mailname` 文件的第一行作为邮件传输器的名称。这实际上位于默认文件的后部分。
- `smtpd_banner`：设置建立 SMTP 连接时显示的横幅的值。在这种情况下，该横幅是由配置文件中设置的变量的值构造的。
- `biff`：决定当 Postfix 处理入邮件队列时，是否应对每个有新邮件的用户使用本地邮件通知服务（`biff`）。在这种情况下，它是禁用的，因为 `biff` 通知可能会导致性能损耗，并且仅在存放邮件文件的机器上相关。使用本地邮件文件的用户可以自己开启此功能。

## 识别主机和域名

`main.cf` 配置文件是大多数用户需要修改的唯一 Postfix 配置文件。在 Ubuntu 系统上安装后，系统的 `main.cf` 配置文件所示（我删除了了一些无关的注释和空白符）：
