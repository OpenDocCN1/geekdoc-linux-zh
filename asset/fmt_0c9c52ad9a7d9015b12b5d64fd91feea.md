
大多数选项的默认值适用于一个对安全不是太偏执或对性能不关心的典型站点。特别是，默认值通过关闭中继、要求地址是完全限定的以及要求地址解析为 IP 地址，试图保护你免受垃圾邮件侵扰。如果你的邮件服务器非常忙并服务于大量的邮件列表，你可能需要微调某些性能值。

第 572 页的表 19.3 列出了你可能需要调整的选项（最多 175 个配置选项中的约 15%）以及它们的默认值。为了节省空间，选项名称没有显示 `conf` 前缀；例如，`FALLBACK_MX` 选项的实际名称为 `confFALLBACK_MX`。该表分为几个部分，标识变量地址的问题：通用、资源、性能、安全和垃圾邮件缓解以及杂项。某些选项显然属于多个类别，但我们只列出了一次。

![](img/4baff4a9c0bcfa44e45d38f4bdc1a0e2_608_0.png)

# 表 19.13 基本配置选项

| | 选项名称 | 描述及（默认值） |
| :--- | :--- | :--- |
| 通用 | `COPY_ERRORS_TO_DOUBLE_BOUNCE_ADDRESS` | 错误消息的抄送地址（无）捕获大量垃圾邮件；某些站点使用 `/dev/null`，但这可能会掩盖严重问题（postmaster） |
| 资源 | `FREE_BLOCKS`, `MAX_MESSAGE_SIZE`, `TO_lots_of_stuff`, `TO_IDENT` | 接收邮件所需的最小文件系统空间（100）单条邮件的最大字节数（无限）各种事务的超时时间（多种）用于检查发送者身份的 ident 查询的超时时间；如果为 0，则不进行 ident 检查（5） |
| | `MAX_DAEMON_CHILDREN`, `MCI_CACHE_SIZE`, `MCI_CACHE_TIMEOUT`, `HOST_STATUS_DIRECTORY`, `FALLBACK_MX` | 最大子进程数（无限制）缓存的打开输出 TCP 连接数（2）保留缓存连接的时间（5m）描述见第 614 页（无默认值）描述见第 613 页（无默认值） |
| 性能 | `FAST_SPL`, `QUEUE_LA`, `REFUSE_LA`, `DELAY_LA`, `MIN_QUEUE_AGE` | 在收件者排序并分发队列时抑制 MX 查找；见第 613 页（1 – true）邮件进入队列而非立即投递的平均负载（8 *CPUs）拒绝邮件的平均负载（12 *CPUs）减速投递的平均负载（0 = 否）任务在队列中停留的最少时间：忙碌机器处理队列缓冲区（0） |
| 安全/垃圾邮件 | `TRUSTED_USERS`, `PRIVACY_FLAGS`, `INPUT_MAIL_FILTERS`, `MAX_MIME_HEADER_LENGTH`, `CONNECTION_RATE_THROTTLE`, `MAX_RCPTS_PER_MESSAGE`, `DONT_BLAME_SENDMAIL` | 用于邮件列表软件所有者；允许伪造 From 行并重建别名数据库（root, daemon, ucp）SMTP 给出的限制（作者）入站邮件的过滤器列表（空）MIME头部的最大大小（无限制）*通过限制接受邮件连接的速率减缓 DOS 攻击（无限制）延迟；延迟额外的收件人并发送错误信息（info）覆盖 sendmail 的安全和文件检查；不要随意更改！（safe） |
| 杂项 | `AUTH_MECHANISMS`, `LDAP_DEFAULT_SPEC` | 用于 SASL 的 SMTP 机制（*）LDAP 数据库规范，包括运行的主机和服务器（未定义） |

a. 具体来说，可以同时运行的最大子进程数。当达到限制时，sendmail 将拒绝连接。此选项可以防止（或导致）拒绝服务（DOS）攻击。
b. 此选项可以防止用户缓冲区溢出。“256/128”是一个很好的值——意味着每个头部 256 字节，每个头部 128 字节。
c. 默认值为“EXTERNAL GSSAPI, KERBEROS, V4 DIGEST”；除非你想降低安全性，否则不要添加 LOGIN。

# 9.9 配置示例

我们还没有真正完成所有的配置选项（将有一个垃圾邮件章节、一个安全章节和一个性能章节），但是时候看一些配置文件示例了。这个顺序可能有点像是马后驾车，或者说我们尝试过的某些安排看起来效果最好。我们尚未涵盖的核心配置是数据库，它主要用于过滤和控制垃圾邮件。从第 592 页开始，记录各个站点使用的配置文件，不可避免地会遇到一些旧时代留下的工艺，它们要么是错误的要么是不需要的。我们通过使用配置文件作为示例清理了这些不一致之处、拼写错误等，它们并没有按照它们在原始服务器上的样子显示。尽管如此，它们反映了真实世界的配置。

## 一个熟悉 sendmail 配置的学生

我们还没有真正完成所有的配置选项（一个垃圾邮件章节、一个安全章节和一个性能章节即将出现），但是时候看一些配置文件示例了。这个顺序可能有点像是马后驾车，或者说我们尝试过的某些安排看起来效果最好。我们尚未涵盖的核心配置是数据库，它主要用于过滤和控制垃圾邮件。从第 592 页开始，记录各个站点使用的配置文件，不可避免地会遇到一些旧时代留下的工艺，它们要么是错误的要么是不需要的。我们通过使用配置文件作为示例清理了这些不一致之处、拼写错误等，它们并没有按照它们在原始服务器上的样子显示。尽管如此，它们反映了真实世界的配置。

## 一个小型 sendmail 配置的公司

用于客户端机器的 `smi-client.mc` 非常简单。它使用主服务器 `smtp.sendmail.com`，这实际上是 `foon.sendmail.com` 的另一个名字。使用 MX 记录（或 CNAME）指向邮件服务器是一个好主意；当你想要移动主邮件服务器时很容易更改。

注意，这个日期是 1998 年 10 月。自此以后 sendmail 已经升级了多次，但配置文件不需要更改。

# Linux 管理手册

`MAIL_HUB` 和 `SMART_HOST` 行将入站和出站邮件重定向到主机 `smtp.sendmail.com`。DNS 中的 MX 记录应当配合，并将该主机的优先级高于单个客户端主机（MX 记录中的数字越小，优先级越高）。`.forward` 文件的路径被设置为 `null`，`aliases` 文件也被设置为 `null`；所有别名扩展均在主机上进行。在这里指定了 `nocanify` 特性以节省时间，因为 DNS 查询无论已经在主机上完成了。

`sendmail.com` 的主机可能是周围受攻击最频繁的 sendmail 安装实例之一。它必须防御各种复杂的狡猾主机攻击，并保护其背后的机器。以下是它的配置文件：

```
divert(-1)

# 使用 Sendmail Switch（sendmail.com 的商业产品）创建。

def('COMMERCIAL_CONFIG', 'INPUT_MAIL_FILTER', 'mime-filter', 'S=local:\n/var/run/mime-filter/mime.sock')

LDAP_DOMAIN(sendmail.com sendmail.net.org)

MASQUERADE_AS(sendmail.com)

MASQUERADE_DOMAIN(sendmail.com sendmail.net.org)

RELAY_DOMAIN('internal-hub.sendmail.com')

def('QUEUE_DIR', '/var/spool/mqueueq')

def('SMART_HOST', 'virus-scan-sendmail.com')

def('COMMERCIAL_CONFIG', 'define(confACERT', '/local/certs/certacert.pem)')

def('COMMERCIAL_CONFIG', 'define(confACERT_PATH', '/local/certs/trustedcerts'))

def('confCHECK_ALIASES', 'true')

def('COMMERCIAL_CONFIG', 'define(CLIENT_CERT', '/local/certs/cert.pem)')

def('COMMERCIAL_CONFIG', 'define(CLIENT_KEY', '/local/certs/key.pem)')

def('CONFIG_FEIGHT_BINDING', 'mimify')

def('confFLAP_DEFAULT_SEC', '-h ldap.sendmail.com ldap2.sendmail.com\n-b "sendmail.dc-com -p 1389'

def('confUSE_LA', '99')

def('conUX_USER', 'mailnull')

def('COMMERCIAL_CONFIG', 'define(SERVER_CERT', '/local/certs/cert.pem)')

def('COMMERCIAL_CONFIG', 'define(SERVER_KEY', '/local/certs/key.pem)')

def('confTO_ID', 'os')

def('confTO_QUEUEAV', '2d')
```
