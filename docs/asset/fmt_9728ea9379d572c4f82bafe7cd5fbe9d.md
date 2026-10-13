
dnl

dnl client.mc:

dnl starlight.com 的客户端宏配置文件

dn

`include`('/usr/lib/mail/m4/cf.m4')

`ostYPE`('solaris2)

`FEATURE`('nullclient', 'mailhost.starlight.com')

```
注意，这里只激活了一个功能：`nullclient`。此功能告诉所有客户端将本地生成的所有邮件发送到 `mailhost.starlight.com`，而不进行任何标头重写。
```

## 具有互联网连接的单一 DNS Domain

接下来，使用以下命令从 `/usr/lib/mail/client.mc` 文件创建客户端 sendmail 配置文件：

```
# m4 /usr/lib/mail/client.mc > /usr/lib/mail/client.cf
```

最后，将生成的 `client.cf` 配置文件拷贝到所有客户端工作站的 `/etc/mail/sendmail.cf` 上。

### 邮件中心/网关配置

以下示例展示了充当邮件中心和网关的系统的 `/usr/lib/mail/hub-gateway.mc` 宏配置文件。

```
dnl

dnl hub-gateway.mc

dnl starlight.com 的邮件中心/网关宏配置文件

dnl

include(`/usr/lib/mail/m4/cf.m4`)

dnl

OSTYPE(`solaris2`)

dnl

dnl 现在让一切看起来都像是来自 username@starlight.com

dnl

MASQUERADE_AS(`starlight.com`)

dnl

dnl 将伪装后的标头接收者设为

dnl

FEATURE(allmasqueraded)

dnl

dnl 以及信封

dnl

FEATURE(masquerade_envelope)

dnl

dnl 激活基于 DNS 的黑洞，以丢弃来自已知垃圾邮件站点的邮件

dnl 激活实时黑洞，以丢弃来自已知垃圾邮件站点的邮件

dnl 升级到 sendmail 8.10 时将将其更改为 dnabl 功能

dnl

FEATURE(`rb8`)

dnl

dnl 开启 mailerter 功能，我们可以中继到某些域

dnl 通过使用我们在 /etc/mail/mailter 中定义的网关。（在 8.10 中，

dnl 这将邮件移动到 /etc/mail/mailter，所以我们现在手动

dnl 将放在那里）

dnl

FEATURE(`cw_file.dnl`)

dnl

FEATURE(`mailter`, hash -o /etc/mail/domaintable`)

     hash -o /etc/mail/domaintable`)

dnl

FEATURE(`virtuesmailter`)

dnl

FEATURE(`access_db`, hash -o /etc/mail/access`)

dnl

dnl 允许中继 starlight.com 域中的主机，但也

dnl 允许我们指定我们将中继的更多域

dnl

FEATURE(`relay_entire_domain`)

d

RELAY_DOMAIN_FILE(`-o /etc/mail/relay-domains`)

dnl

```

# 邮件服务规划

当你完成创建 `hub-gateway.mc` 文件后，使用以下命令来生成 sendmail 配置文件：

```
# m4 /usr/lib/mail/hub-gateway.mc > /usr/lib/mail/hub-gateway.cf
```

然后，将生成的 `hub-gateway.cf` 文件复制到 `mailhost.starlight.com` 的 `/etc/sendmail.cf` 上。

# 自定义外部数据库

在启动 `sendmail mailhost.starlight.com` 之前，你必须至少配置一个外部数据库。这些数据库及其内容列在下方。

- `/etc/mail/mailertable`
由于该系统是邮件中枢，请使用此文件确保所有发送至 `username@starlight.com` 的入站邮件都递送到此系统。该文件还处理了邮件可能发送至 `username@hostname.com` 的罕见情况。

```
# 在此系统上本地处理所有以 starlight.com 结尾的内容。

# 此外，本地处理任何地址为

# username@hostname.starlight.com 的邮件，以防使用此类格式。

starlight.com      local:
starlight.com      local: 
```

使用 `makemap` 命令将此文件处理为哈希映射，如下所示。

```
# makemap hash /etc/mail/mailertable > /etc/mail/mailertable
```

- `/etc/mail/relay-domains`
使用此文件确保来自你域名内部的邮件被此网关接受并递送到任何地方。`relay-domains` 文件必须包含你的域名。

```
# 列出我们实际上中继邮件的域名。

# 如果此处未列出域名，则拒绝中继来自该域的邮件。

starlight.com
```

由于 `sendmail` 将 `relay-domains` 视为纯文本文件，你不需要采取其他操作来处理。

# 带有 Internet 连接的单 DNS 域名与独立网关 83

- `/etc/mail/sendmail.cw`
使用此文件列出该主机已知的所有名称，以便 `sendmail` 识别发送到这些任何一个主机名的邮件确实是发送给此系统的。此外，在此处列出域名，因为大多数邮件是发送至 `username@starlight.com`，而你希望 `sendmail` 识别出 `starlight.com` 是指代此主机的另一种方式。

```
# 列出邮件中枢已知的所有名称，

# 以免 sendmail 混淆认为它不应该

# 将邮件递送到此系统的正确队列中。请注意

# 邮件列表本身位于列表末尾，因为

# 大多数邮件的地址为 username@starlight.com

mailhost.starlight.com
```

由于 `sendmail` 将 `sendmail.cw` 视为纯文本文件，你不需要采取其他操作来处理它。现在你已经自定义了所有这些文件，请重启 `sendmail`，使其读取这些文件并使用它们的设置为入站和出站邮件做出决策。

# DNS 配置

为了确保从任何 站点发送的所有邮件都直接到达作为 `starlight.com` 邮件网关和中枢的系统，请在 `starlight.com` DNS 服务器表中放入示例所示的条目。

```
starlight.com   IN MX 10 mailhost
mailhost        IN A  205.172.3.45
```
