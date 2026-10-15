
# 第 20 章 电子邮件

## 客户端配置

如果你遵循第 753 页的邮件系统设计，`sendmail` 应该以 MSA 运行（不带 `-bd` 标志），如果客户端机器可以被教使用端口 587 提交。否则，以守护进程模式（`-bd`）运行 `sendmail`，但将 `DAEMON_OPTIONS` 配置为仅监听回环接口连接。

## `sendmail` 中的垃圾邮件相关功能

SUSE 在 `/etc/mail/linux.nullclient.mc` 提供了一个空客户端 `.mc` 文件。填入你的邮件服务器名称，构建 `sendmail.cf` 文件，然后就完成了。

## 配置选项

你使用 `m4` 的 `define` 命令设置配置选项。所有作为 `m4` 变量访问的选项列表（以及它们的默认值）都在 `cf/README` 文件中。默认值对于一个对安全不敏感且对性能不在关心的典型设置是足够的。默认通过关闭中继、要求地址全限定以及要求发送域名解析为 IP 地址来保护你免受垃圾邮件的影响。如果你的邮件服务器繁忙并处理大量的邮件列表，你可能需要调整某些性能值。

下一页的表格 20.11 列出了可能需要调整的选项（175 多个配置选项中的 10%）。它们的默认值显示在括号中。为了不带 `conf` 前缀，名称使用了空格；例如，`FALLBACK_MX` 选项实际的名为 `confFALLBACK_MX`。我们将表格分为识别变量地址问题的子部分：资源管理、性能、安全和垃圾邮件缓解以及杂项选项。某些选项属于多个类别，但我们只列出了一次。

## 20.11 基础 `sendmail` 配置选项

| 分类 | 选项名称 | 说明（默认值）ᵃ |
| --- | --- | --- |
| 资源 | `MAX_DAEMON_CHILDREN` | 子进程的最大数量（不限制） |
| 资源 | `MAX_MESSAGE_SIZE` | 单条消息的最大字节数（无限） |
| 资源 | `MAX_FREE_BLOCKS` | 接收邮件所需的最小文件系统空间（100） |
| 资源 | `TO_lots_of_stuff` | 各种事务的超时时间（变量） |
| 性能 | `DELAY_LA` | 减慢交付的负载平均值（0 = 不限制） |
| 性能 | `FALLBACK_MX` | 描述请见第 803 页（无默认值） |
| 性能 | `FAST_SPLIT` | 在对接收者排序并分发到队列时抑制 `MX` 查询（1 = `true`） |
| 性能 | `HOST_STATUS_DIRECTORY` | 描述请见第 803 页（无默认值） |
| 性能 | `MCI_CACHE_SIZE` | 缓存的打开 TCP 连接数（2） |
| 性能 | `MCI_CACHE_TIMEOUT` | 保持缓存连接的时间 |
| 性能 | `MIN_QUEUE_AGE` | 邮件留在队列中的最小时间；使繁忙的机器处理队列缓冲区（0） |
| 性能 | `QUEUE_LA` | 邮件应进入队列而非立即交付的负载平均值（8 * `IPCUs`） |
| 性能 | `REFUSE_LA` | 拒绝邮件的负载平均值（12 * `IPCUs`） |
| 安全与反垃圾邮件 | `AUTH_MECHANISMS` | 用于 Cyrus SASLB 的 SMTP 认证机制 |
| 安全与反垃圾邮件 | `CONNECTION_RATE_THROTTLE` | 通过限制接受邮件连接的速率来缓 DDoS 攻击（不限制） |
| 安全与反垃圾邮件 | `_SENDMAIL` | 覆盖 `sendmail` 的安全和文件检查；通常不要更改！（`safe`） |
| 安全与反垃圾邮件 | `MAX_MIME_HEADER_LENGTH` | 设置 MIME 头部的大小（不限制） |
| 安全与反垃圾邮件 | `MAX_RCPTS_PER_MESSAGE` | 减慢垃圾邮件交付；推迟额外的接收者并发送临时错误消息（`info`） |
| 安全与反垃圾邮件 | `PRIVACY_FLAGS` | 限制通过 SMTP 传出的信息（`authwarnings`） |
| 其他 | `DOUBLE_BOUNCE_ADDRESS` | 拦截大量垃圾邮件；某些使用 `use/null`，但这可能导致严重问题（`postmaster`） |
| 其他 | `LDAP_DEFAULT_SPEC` | LDAP 数据库的映射规范，包括运行的主机和端口（未定义） |

a. 具体而言，可以同时运行的子进程的最大数量。当达到限制时，`sendmail` 将拒绝连接。此选项可以防止（或）拒绝服务攻击。
b. 默认值为 `EXTERNAL GSAPI KERBEROS_V4 DIGEST-MD5 CRM-MD5`；不要添加 `LOGIN`，因为密码是以明文传输的。这在内部可能是可以的，但除非 Internet 连接也通过 SSL 了安全，否则不行。
c. 此选项可以防止用户代理缓冲区。“256/128” 是一个很好的值——它意味着每个头部 256 字节，每个参数到头部的 128 字节。

将这些技术与灰名单列表（greylisting，第 764 页）、使用 `amavisird-new` 进行内容扫描（第 769 页）以及用于电子邮件验证的新 DNS 记录（第 767 页）结合使用，你可能在对抗垃圾邮件者时有一机会。

## 中继控制 (Relay control)

`sendmail` 接收入站邮件，查看信封地址，决定邮件应该去向何处，然后将其传递给适当的目标。该目标可以是本地的，也可以是交付链中后续的传输代理。当入站消息没有本地接收者时，处理它的传输代理就充当了中继的角色。

只有在访问数据库中标记为 `RELAY`（见第 785 页）且列在 `/etc/mail/relay-domains` 中的主机才被允许提交邮件进行中继。某些类型的中继是有用且合法的。你该如何判断哪些邮件应该被中继，哪些应该被拒绝呢？中继实际上只在三种情况下是必要的：

- 当传输代理作为无法通过其他方式访问的主机的网关时；例如：
- 当传输代理是那些不太智能的主机的出站邮件服务器时。在这种情况下，发送者的主机名或 IP 地址将是本地的（或至少是枚举的）
- 当你同意成为另一个站点的备份 MX 目标时。

任何其他看起来需要中继的情况可能都是设计不当的指示（支持移动用户除外）。你可以通过指定一个中央服务器接收邮件，并使用 POP 或 IMAP 进行客户端访问，来模糊中继首次首次（上述）。第二种情况应该是允许的，但仅限自己的主机。你可以检查 IP 地址或主机名。在第三种情况下，你可以在访问数据库中列出其他站点，并仅对该站点的 IP 地址段允许中继。

尽管 `sendmail` 默认关闭中继，但已添加了一些功能来重新开启中继，以限制且受控的方式。为了完整起见，下面列出了这些功能，但我们的建议是不要过度开启。`access_db` 功能是允许中继最安全的方法。

- `FEATURE('relay_entire_domain')` – 允许对你的域名进行中继
- `RELAY_DOMAIN(domain, ...)` – 增加更多需要中继的域名
- `RELAY_DOMAIN_FILE(filename)` – 同上；从文件获取域名列表
- `FEATURE('relay_hosts_only')` – 影响 `RELAY_DOMAIN`, `accessdb`

如果你如果你使用 `SMART_HOST` 或 `MAIL_HUB` 标记通过特定的邮件服务器路由邮件，则需要进行异常处理。该服务器必须配置为中继来自本地主机的邮件。使用以下进行配置：

```
FEATURE('relay_entire_domain')
```

![](img/579efec8c8)

## 用户或站点黑名单 (User or site blacklisting)

如果你有拦截的用户或站点，使用 `FEATURE('blacklist')`，它支持访问文件中的以下类型：

```
To:nobody ERROR:550 禁止此用户

To:host. ERROR:550 此主机不接受邮件

To:user@mydomain ERROR:550 禁止此用户
```

这些行限制了对任何 的邮件。

## 节、速率与连接限制 (Throttles, rates, and connection limits)

| 原语 |  |
| --- | --- |
| `BAD_RCPT_THROTTLE` | 减慢入站连接 |
| `MAX_RCPTS_PER_MESSAGE` | 如果消息过多，则延迟交付 |
| `conncontrol` | 限制并发连接数 |
| `greet_pause` | 延迟响应响应，要求严格遵守 |

当登录计数达到限制时，使用

```
define(confBAD_RCPT_THROTTLE, `3`)
```

设置 `MAX_RCPTS_PER_MESSAGE` 选项会导致发送者等待。`ratecontrol` 和 `conncontrol` 功能允许按主机或网络限制入站连接的速率以及并发连接数。两者都使用 `/etc/mail/access` 文件来指定它们遵守的限制，第一个在键字段中使用 `ClientRate:`，第二个使用 `Conn:`。要启用这些控制，在 `.mc` 文件中插入此类行：

```
FEATURE('rate', 'nodelay', terminate)

FEATURE('conncontrol', 'nodelay', terminate)'
```

然后在 `/etc/mail/access` 中添加要受控制的主机或网络列表及其限制阈值。例如，这些行

