
此行导致 `access_db` 使用 `sendmail` 分发中 `cf/sendmail.schema` 定义的 LDAP 架构。你可以通过 `FEATURE` 的额外参数来定义自己的数据库架构；详情请参见 `cf/README` 文件。

## mailtable 功能

`mailtable` 通过特定的邮件代理（mailer）将邮件重定向到特定主机或域名的备目的地。它在邮件离开站点时应用。`mailtable` 功能只查看地址的主机端口，而不查看用户部分。报头地址不会被重写，因此邮件继续发送给同一个用户，但通过不同的邮件代理发送到不同的主机。`mailtable` 最初设计用于处理 UUCP、DECnet 和 BITNET 等其他邮件系统，但今天它用于将邮件从网关机重定向到内部服务器，或重定向到没有直接访问 Internet 的远程站点服务器。

要使用 `mailtable`，请在你的 `.mc` 文件中包含以下行：

```
FEATURE('mailtable')
```

`mailtable` 中的条目格式为：

```
old_domain mailer:destination
```

左侧键前面的点号是一个通配符，意味着该域内的任何主机。只允许主机和域名作为 `mailtable` 键；不允许使用用户。右侧的目标值可以是域、`user@domain` 子句，甚至为空，在这种情况下，信封（envelope）不会发生变化。`mailtable` 的值必须是 `MAILER` 子句中定义的名称的字符串（MS）；参见第 573 页。

例如，假设你使用 Exchange 作为主要的内部邮件服务器，但不想让它直接面对 Internet。你可以在 Internet 上放置一台 Linux 机器作为邮件网关，并在病毒扫描或你喜欢的任何预处理后将所有邮件转发到 Exchange 服务器。以下是实现此操作的 `mailtable` 条目，假设 Exchange 服务器具有所示的内部 IP 地址：

```
my-domain esmtp:[192.168.1.245]
```

然而，这是中继（relaying）的形式（我们在第 589 页见过），需要进行控制。为了完成此示例，你需要在访问数据库中放入行：

`To:my-domain RELAY`

以允许发送到 `my-domain` 任何用户的邮件进行中继。

## 18.9 更高级的 sendmail 配置原语

### genericstable 功能

`genericstable` 功能（"generics table", "generic stable"）类似于出站邮件的别名。例如，它可以在出站邮件中将 `trent@astrust.com` 映射到 `trent.hein@astrust.com`。被重写的是报头，邮件投递不受影响，只有回复影响。

有几种机制可以映射主机，`genericstable` 是唯一一个同时包含用户名和主机名作为映射键一部分的机制。在本节后面讨论的 `masquerade_envelope` 和 `allmasquerade` 功能也可以适用于 `genericstable` 中的地址。

要使用 `genericstable`，请确保你的域在 `generics` 类中。要将域放入 `generics` 类，你可以在 `GENERICS_DOMAIN` 宏中列出它，或者将其放入 `GENERIC_DOMAIN_FILE` 宏指定的文件中。

例如，使用数据库默认的 `genericstable`，在你的 `mc` 配置文件中添加：

```
GENERICS_DOMAIN_FILE(/etc/mail/local-host-names)
FEATURE('genericstable')
```

在此示例中，任何接收邮件的主机都被包含在内。启用 `genericstable` 功能会略微减慢 `sendmail`；每个发送者地址都必须查找。

### virtuosirable 功能

虚拟用户支持入站邮件的域别名。此功能允许在一台机器上托管多个虚拟域，这在 Web 托管站点很常见。

表的键包含电子邮件地址（`user@host.domain`）或域规范（`@domain`）。值字段是本地电子邮件地址或电子邮件地址。如果键是域，值可以将用户字段解析为变量 `%1` 并传递，或者路由到不同的用户。如果规范使用 `form+details` 格式，则变量 `%2` 包含细节，`%3` 包含 `+details`；你可以根据需要使用。

让我们来看一些示例（我们添加了注释）：

```
info@conf # 路由到本地用户
info@bar.com bar-info # 另一个本地用户
joe@bar.com error:No such user # 返回错误
@baz_org jane@elsewhere.com # 所有邮件发送到
@zokni.org %1@elsewhere.com # 路由到同一个用户，不同域
```

数据映射左侧的所有主机都必须列在 `cw` 文件 `/etc/mail/local-host-names`（或 `VirtHost` 类）中；否则 `sendmail` 将尝试在 Internet 上查找该主机并投递邮件。如果 DNS 将 `sendmail` 指回你的服务器，你会在退信邮件（bounces）中收到“local configuration error”。遗憾的是，`sendmail` 无法判断此实例的错误信息实际上应该是“virtuosirable key not in cw file”。

这里实际上涉及几个部分：

- 存在 DNS MX 记录，以便邮件首先路由到正确的主机；然后
- 必须存在 `cw` 条目或指定 `VIRTUSER_DOMAIN`（或等同于 `VIRTUSER_DOMAIN_FILE`）

`mailtable` 的值是 `MAILER` 子句中定义的名称；参见第 573 页。例如，假设你使用 Exchange 作为主要的内部邮件服务器，但不想让它直接面对 Internet。你可以在 Internet 上放置一台 Linux 机器作为邮件网关，并在病毒扫描或你喜欢的任何预处理后将所有邮件转发到 Exchange 服务器。以下是实现此操作的 `mailtable` 条目，假设 Exchange 服务器具有所示的内部 IP 地址：

```
my-domain esmtp:[192.168.1.245]
```
