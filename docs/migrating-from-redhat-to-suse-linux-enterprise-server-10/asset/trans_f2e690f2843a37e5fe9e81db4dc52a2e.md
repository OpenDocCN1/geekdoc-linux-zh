
要运行的命令的路径名是相对于通过 /etc/postfix/main.cf 文件中的变量 daemon_directory 定义的目录（这通常是目录 /usr/lib/postfix/）。

如果提供了 **-v** 参数，将提高给定命令的调试级别。

指定 **-D** 参数允许通过使用在 /etc/postfix/main.cf 文件中由变量 debugger_command 指定的调试命令来进行调试。

## 配置全局设置

除查找表中处理规则的配置外，所有其他配置定义都在以下文件中设置：

/etc/postfix/main.cf

在 SUSE Linux Enterprise Server 10 中，可以使用以下文件中的变量来修改该文件中最常见的参数：
- /etc/sysconfig/mail
- /etc/sysconfig/postfix

Postfix 是最后需要运行 **SuSEconfig** 才能从 /etc/sysconfig/ 目录下的文件生成实际配置文件的少数服务之一。

/etc/sysconfig/mail 文件用于一般配置，这些配置不仅针对 Postfix，也适用于 Sendmail。 为了使 MTA 正确运行，您必须在 /etc/sysconfig/mail 文件中执行以下操作：
1. 必须在 FROM_HEADER 变量中输入完全限定域名 (FQDN)。
   如果未设置此变量，将使用主机名 (FQDN)。
2. 应将 SMTPD_LISTEN_REMOTE 变量设置为 yes，Postfix 将监听端口 25 以接收传入的邮件。
   否则，将仅接受来自本地主机的电子邮件。

通过 /sbin/SuSEconfig 脚本，这两个设置以及 /etc/sysconfig/postfix 文件中的条目将转换为 /etc/postfix/main.cf 文件中的相应参数。

如果不想让 SuSEconfig 生成此配置文件，请将 /etc/sysconfig/mail 文件中的变量 MAIL_CREATE_CONFIG 设置为 no。

要配置 Postfix，您需要知道如何执行以下操作：
- 使用 /etc/sysconfig/postfix 配置 Postfix
- 使用 /etc/postfix/main.cf 配置 Postfix

### 使用 /etc/sysconfig/postfix 配置 Postfix

对 /etc/sysconfig/postfix 文件的修改仅在 /etc/postfix/main.cf 文件中采纳，在某些情况下也在 /etc/postfix/master.cf 文件中采纳，前提是执行了 /sbin/SuSEconfig 或 Postfix 的 SuSEconfig 模块：
- /sbin/conf.d/SuSEconfig.postfix
- 或 /sbin/SuSEconfig --module postfix

配置文件中简要注释了变量的含义。

以下提供了更详细的说明。

- **POSTFIX_RELAYHOST。** 如果本地电子邮件服务器应使用中继主机来投递无法本地投递的电子邮件，则此处必须给出中继主机本身或中继主机的域名。如果提供了域名，Postfix 通过 MX 查找确定该域名的中继主机。如果 Postfix 应在不执行 MX 查找的情况下将所有无法本地投递的电子邮件转发到中继主机，则必须在方括号中给出中继主机的名称（例如， **[mailrelay.digitalairlines.com]**）。也可以以这种形式给出 IP 地址。可选地，可以使用端口号扩展域或主机（例如，**digitalairlines.com:1025**）。如果您留此条目为空，Postfix 将所有无法本地投递的邮件投递到邮件交换器。文件 `/etc/postfix/transport` 中的任何条目优先于中继主机。如果为该变量赋值，运行 **SuSEconfig** 将修改文件 `/etc/postfix/main.cf` 中的变量 `relayhost`。
- **POSTFIX_MASQUERADE_DOMAIN。** 如果配置了此变量的自有 DNS 域（例如，digitalairlines.com），则包含主机前缀的所有电子邮件地址将通过该主机前缀缩短。例如，geeko@da2.digitalairlines.com 变成 geeko@digitalairlines.com。如果为该变量赋值，运行 **SuSEconfig** 将修改文件 `/etc/postfix/main.cf` 中的变量 `masquerade_domains`。此外，将设置变量 `masquerade_exceptions` = root。
- **POSTFIX_LOCALDOMAINS。** 包含一个逗号分隔的域名列表，Postfix 应接受这些域名的电子邮件。运行 **SuSEconfig** 时，这些值将写入文件 `/etc/postfix/main.cf` 中的变量 `mydestination`。如果 **POSTFIX_LOCALDOMAINS** 为空，**SUSEconfig** 会将变量设置为 $my*hostname*, localhost.$my*domain*。
- **POSTFIX_NULLCLIENT。** 无客户端是一个只能通过网络发送邮件、不通过网络接收邮件且不在本地投递任何邮件的主机。如果您输入 **yes**，运行 **SuSEconfig** 后，/etc/postfix/main.cf 文件中的变量 mydestination 将保持为空。默认条目为 **no**。
- **POSTFIX_DIALUP。** 如果将此值设置为 **yes**，无法本地投递的电子邮件不会在运行 sendmail -q 命令之前发送到其目标。该设置对拨号系统有用；否则，如果系统不在线，发送邮件时会出现错误消息，或者如果使用拨号即连，每个电子邮件消息都会建立连接。值为 **no** 会导致立即尝试投递任何等待投递的电子邮件。如果为该变量赋值 **yes**，运行 **SuSEconfig** 将在 /etc/postfix/main.cf 文件中添加行 defer_transports = smtp。
- **POSTFIX_NODNS:** 如果将此变量设置为 **yes**，Postfix 在处理电子邮件时将不会为发件人和收件人域执行任何 DNS 查找。如果为该变量赋值 **yes**，运行 **SuSEconfig** 将激活 /etc/postfix/main.cf 文件中的变量 disable_dns_lookups = yes。
- **POSTFIX_CHROOT。** 如果将此变量设置为 **yes**，服务将在可能的情况下在 chroot 环境中运行。您可以在 /var/spool/postfix 中找到 chroot 环境。如果将变量设置为 **no**（默认），所有 Postfix 进程将在正常环境中运行。
- **POSTFIX_UPDATE_CHROOT_JAIL。** 如果 SuSEconfig 需要设置 chroot 环境，此值应设置为 yes。默认情况下，该变量设置为 no。
- **POSTFIX_LAPTOP。** 某些 Postfix 服务频繁访问 FIFO，从而阻止硬盘停止旋转。然而，如果希望在笔记本电脑上出于省电目的这样做，可以将该变量设置为 yes。
- **POSTFIX_UPDATE_MAPS。** 如果 SuSEconfig 需要从相应的查找表创建数据库文件，则应将该变量设置为 yes（默认）。
- **POSTFIX_MAP_LIST。** 如果 POSTFIX_UPDATE_MAPS 设置为 yes，您可以在此选择 Postfix 应支持的列表。
- **POSTFIX_RBL_HOSTS。** 您可以在此指定一个逗号分隔的主机名列表，RBL（实时黑洞列表）可以从这些主机获取。不接受来自这些列表的客户端的邮件。仅当 POSTFIX_BASIC_SPAM_PREVENTION 未设置为 off 时，此条目才有意义。
- **POSTFIX_BASIC_SPAM_PREVENTION。** 此处，指定如何配置针对 UCE（未经请求的商业电子邮件）的严格过滤规则。可能的级别为 off、medium 和 hard。更多详细信息请参见 http://www.postfix.org/uce.html。
- **POSTFIX_MDA。** 此处，指定 Postfix 应配合使用的 MDA。条目如下：
  - procmail. 使用 Procmail 在本地投递邮件。
  - cyrus. 使用 lmtp 投递到 cyrus-imapd。
  - local. 使用 Postfix 本地 MDA。
- **POSTFIX_SMTP_AUTH_\*.** 这些变量控制 Postfix 在身份验证方面的行为：如果 Postfix 接受邮件以及如果 Postfix 将邮件投递到其他邮件服务器。
- **POSTFIX_SMTP_TLS_SERVER,** **POSTFIX_SMTP_TLS_CLIENT.** 如果将这些变量设置为 **yes,** 在配置了以下变量的情况下，Postfix 可以在发送和接收邮件时加密与另一方的通信。
- **POSTFIX_SSL_\*,** **POSTFIX_TLS \*.** 这些变量控制加密所需的证书和密钥管理的各个方面。本课程不涵盖加密连接；此手册不提供关于各个变量的任何详细信息。
- **POSTFIX_ADD_\*:** 这些变量可用于设置 Postfix 变量。必须将该变量转换为大写字母并附加到 **POSTFIX_ADD_。** 例如，要将 Postfix 变量 *message_size_limit* 设置为 100000，请在 */etc/sysconfig/postfix* 中输入 `POSTFIX_ADD_MESSAGE_SIZE_LIMIT=100000`。随后，SuSEconfig 将在 */etc/postfix/main.cf* 中生成相应的条目 *message_size_limit*=100000。可以使用 *postconf* 列出所有可用的 Postfix 变量。
- **POSTFIX_REGISTER_SLP.** 如果设置为 **yes,** Postfix 将自动向 SLP 注册。

除了这种方法之外，还可以直接在具有非常详细注释的文件 */etc/postfix/main.cf* 中进行更多设置。在手动修改文件 */etc/postfix/main.cf* 之后，修改 */etc/sysconfig/postfix* 并随后运行 */sbin/SuSEconfig* 将不会影响文件 */etc/postfix/main.cf*。

