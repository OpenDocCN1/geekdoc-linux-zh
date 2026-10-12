
```
define(`confAUTH_MECHANIS`, `DIGEST-MD5 CRAM-MD5')
\dnl
```

此`define`命令告诉系统使用`DIGEST-MD5`或`CRAM-MD5`（挑战/响应身份验证模式）进行客户端验证。服务器上的`SASL`库配置了其中一种或两种身份验证技术，这就是响应`EHLO`命令时将通告的内容。

客户端从通告的技术中选择一种身份验证技术，并使用`AUTH`命令启动身份验证过程。这是`AUTH`关键字的第二次用法。客户端只需发送`AUTH`命令，随后是从通告列表中选择的身份验证技术——例如：

```
AUTH CRAM-MD5
```

列表 12.6 显示了客户端与服务器之间身份验证交换的更完整示例。在列表 12.6 中，服务器通告`DIGEST-MD5`为唯一的身份验证技术。客户端决定使用它并响应必要的`AUTH`命令。服务器随后发送一个`BASE64`编码的挑战字符串。客户端加密挑战字符串及其身份验证数据，将加密后的响应转换为`BASE64`字符串，并发送回服务器。在列表 12.6 中，服务器接受了回复，身份验证会话开始运行。

### 列表 12.6 一个经过身份验证的 SMTP 会话

```
220 wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 18 Oct 2000 11:42:34 -0400
>>> ani.foobirds.org
250-wen.foobirds.org Hello ani@foobirds.org [172.16.12.1], pleased to meet you
250-ENHANCEDSTATUSCODES
250-EXPN
250-VERB
250-8BITIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250-AUTH DIGEST-MD5
250 HELP
>>> AUTH DIGEST-MD5
```

![](img/b8082498451dba2bf0cf2907c85c4c83_365_0.png)

```
334 INNEDETDeuxFREJoUndurnbmnhNWItOMJNGb29Klubm9zb2Z0LMvbT4=
>>> MJGetFdsZk1YW4ImebtVLMD1NDbHZkjfyHHVSWEMGMyYNNzg2Q==
255 Authentication successful.
>>> MAIL: <craig@ani.foobirds.org> AUTH-craig@ani.foobirds.org
250 <craig@ani.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 <craig@wren.obobirds.org>... Recipient ok
>>> DATA
354 Enter mail, with ". on a line by itself
>>>
250 NAA01047 Message accepted for delivery
>>> QUIT
221 wen.foobirds.org closing connection
```

*(注：原文此部分似乎存在乱码或格式错误，译文已根据上下文逻辑进行了平滑处理)*

> 它是`AUTH`关键字的第三种用法。列表 12.6 显示了`MAIL From`头部之后出现的`AUTH`关键字。发送者地址。实际上，`AUTH`验证的是服务器信任的客户端。对于`DIGEST-MD5`身份验证，客户端和服务器必须约定一个共享密码。使用`saslpassword`命令配置密码如下：

```
[root]# saslpassword craig
Password: thissecret!
Again (for verification): thissecret!
```

服务器通过`saslpassword`定义的密码必须与提供的密码匹配。在配置时定义。

### 配置身份验证客户端

`AUTH`客户端与服务器通信的方式有两种：

- 客户端可以运行使用你的服务器的`MUA`。某些`MUA`（如`pine`和`Eudora`）使用`AUTH`扩展。通过这种方法，客户端直接与服务器通信。
- 客户端可以运行`Sendmail`并作为`MTA`。在客户端上运行`Sendmail`的优势是任何`MUA`都可以访问`AUTH`扩展。

`defaultAuthInfo`选项指向在系统作为客户端时用于身份验证信息的文件。默认情况下，此选项未定义，系统在作为客户端时不会尝试使用`AUTH`。在`m4`配置文件中使用`confDEF_AUTH_INFO`来定义`AUTH`数据文件——

```
define(`confDEF_AUTH_INFO', `/etc/mail/default-auth-info`)
dnl
```

文件可以命名为任何名称，`Sendmail`开发者建议使用`/etc/mail/default-auth-info`。该文件必须位于只有`root`可写入的目录。文件本身必须由`root`所有且仅允许所有者读取。

文件（示例中为`default-auth-info`）包含了用于验证`AUTH`客户端的四个信息。用`SASL`术语来说，这四个信息是：

**授权身份（Authorization identity）**：在远程系统上执行操作的身份。这是在远程系统中授予权限的用户名。例如，`craig`是一个用户 ID，授予对`craig`拥有的文件的所有权。授权身份决定权限。

**身份验证身份（Authentication identity）**：通过挑战/响应协议进行验证的用户名。它不需要与授权身份相同。然而，一旦身份验证身份（`authid`）通过验证，它将被接受为授权身份的代理，并授予与授权身份相同的权限。例如，假设`craig`是授权身份，`katy`是身份验证身份。身份验证后，`katy`获得对`craig`拥有文件的所有权。对于上面的`DIGEST-MD5`示例，身份验证身份应匹配使用`saslpassword`创建密码的用户名。

前两行是授权身份（authorization identity）和身份验证身份（authentication identity）。它们具有相同的值——在此例中为`craig`。`Sendmail`期望这两个值是相同的。如果它们不相等，`Sendmail`将不会为客户端转发邮件。（当然，你可以通过编写重写规则来更改此行为；但默认配置期望这些值相匹配。）第三行是用于加密客户端对服务器响应的密钥。最后一行是客户端的主机名，它是`Sendmail`使用的默认区域（`realm`）值。

### Sendmail 安全协议

上文指出，`Sendmail`服务器会检查客户端提供的数值，以决定是否应该中继客户端的邮件。第 11 章中中继配置的示例都依赖于 IP 地址或域名。然而，当今网络中的移动性和动态地址分配意味着，客户端并不总是拥有可以解析回固定地址的固定地址或名称。`Sendmail`使用`AUTH`扩展对客户端进行身份验证的唯一原因是，决定是否在不考虑客户端域名或地址的情况下中继该客户端的邮件。

### 身份验证在中继中的作用

列表 12.6 中的服务器仅为客户端提供一种身份验证。如果客户端无法执行`DIGEST-MD5`身份验证，客户端可以在不启动身份验证的情况下发送邮件。所有服务器都接受未经验证的邮件——但它们可能不会中继。

如果客户端通过受信任的身份验证方法通过验证，则允许其转发邮件。要更改该行为，你需要创建自己的重写规则。自定义重写规则定义在`Local_check_ruleset`中。`TRUST_AUTH_MECH`可以列出信任的身份验证方法。例如，要信任`DIGEST-MD5`，请在`m4`宏配置中放置：

```
TRUST_AUTH_MECH(`DIGEST-MD5') )
```

即使通过受信任机制验证的客户端也不允许为所有人转发邮件。要更改该行为，你需要创建自己的重写规则。在`Local_check_ruleset`或`Local_trust_auth`规则集中定义的自定义重写规则用于验证客户端是否已身份验证，以及使用了什么身份验证方法完成任务。`Local_trust_auth`规则集用于修改`fact`：`Sendmail`仅在`MAIL From:`请求头中的标识用户与通过挑战/响应验证的用户相同时，才在该头中发送`AUTH`关键字。三个变量包含了可用于这些规则集的信息：

- `auth_type`: 此变量包含用于身份验证客户端的身份验证技术名称——例如，`DIGEST-MD5`。
- `auth_user`: 此变量包含通过客户端和服务器原始挑战/响应交换进行身份验证的名称。
- `auth_author`: 此变量初始包含来自授权身份的值。如果在`MAIL From:`请求头通过`AUTH`关键字定义了值，则该值将成为`auth_author`变量的值。

![](img/b8082498451dba2bf0cf2907c85c4c83_369_0.png)
