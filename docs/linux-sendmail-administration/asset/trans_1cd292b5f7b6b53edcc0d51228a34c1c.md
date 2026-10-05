

# 第 12 章 Sendmail 安全

使用源的公钥解密，证明了消息来自该源。此外，校验和是使用消息原始内容生成的，这意味着接收者可以通过重新运行校验和来检测受损坏的数据。这为源和内容都提供了身份验证。

安全密钥分发：公钥加密的一个弱点是，你必须信任公钥的源。一切——验证、加密和解密——都取决于公钥。从损坏的服务器获取的密钥会破坏一切的安全性。某些商业机构付费提供公钥服务器。大多数组织都使用这些服务。其他组织通过建立双边协议，在组织之间建立信任以便分发密钥。实际上，一个组织告诉合作伙伴信任特定的服务器作为其公钥的源。

Sendmail 安全协议没有定义分发公钥的机制。这些协议假设密钥已从信任的公钥服务器获取，或通过其他安全机制分发。

# Sendmail 身份验证

SMTP 的 AUTH 扩展用于验证 SMTP 客户端以及客户端传输的单个消息。该扩展不加密消息。相反，它提供了某种保证，确保消息源确实是其声称的对象。当系统无法通过其 IP 地址验证时（例如，客户端是移动系统，或客户端通过动态分配客户端 IP 地址的第三方连接服务器时），使用 AUTH 来验证客户端系统。AUTH 关键字有三种不同的使用方式。

AUTH 出现在 EHLO 命令响应的关键字列表中。以这种方式使用时，AUTH 通告服务器支持 SMTP AUTH 扩展，并通告服务器支持的身份验证方法。我们首次在第 1 章“互联网邮件协议”的列表 1.2 中看到这一点，当时服务器显示了以下信息消息：

250-AUTH DIGEST-MD5

此消息告诉客户端，服务器支持 AUTH SMTP 扩展，并使用 DIGEST-MD5 进行身份验证。消息摘要 5（MD5）是一种通用用于身份验证的加密系统。

服务器宣告的身份验证技术列表由 SASL 库（libsas1）支持的技术部分，以及管理员在 Sendmail 配置中使用 `AuthMechanisms` 选项请求的技术共同决定。`AuthMechanisms` 选项在 m4 宏配置文件中通过 `confAUTH_MECHANIS` 参数进行定义——例如：

```
define(`confAUTH_MECHANIS`, `DIGEST-MD5 CRAM-MD5')\dnl
```

此 `define` 命令告诉系统使用 DIGEST-MD5 或 CRAM-MD5（挑战/响应身份验证模式）进行客户端验证。服务器上的 SASL 库配置了其中一种或两种身份验证技术，这就是响应 EHLO 命令时将通告的内容。

客户端从通告的技术中选择一种身份验证技术，并使用 AUTH 命令启动身份验证过程。这是 AUTH 关键字的第二次用法。客户端只需发送 AUTH 命令，随后是从通告列表中选择的身份验证技术——例如：

```
AUTH CRAM-MD5
```

列表 12.6 显示了客户端与服务器之间身份验证交换的更完整示例。在列表 12.6 中，服务器通告 DIGEST-MD5 为唯一的身份验证技术。客户端决定使用它并响应必要的 AUTH 命令。服务器随后发送一个 BASE64 编码的挑战字符串。客户端加密挑战字符串及其身份验证数据，将加密后的响应转换为 BASE64 字符串，并发送回服务器。在列表 12.6 中，服务器接受了回复，身份验证会话开始运行。

# 列表 12.6 一个经过身份验证的 SMTP 会话

```
220 wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 18 Oct 2000
11:42:34 -0400
>>> ani.foobirds.org
250-wen.foobirds.org Hello ani@foobirds.org [172.16.12.1], pleased to
meet you
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

# Sendmail 安全协议

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

> 它是 AUTH 关键字的第三种用法。列表 12.6 显示了 MAIL From 头部之后出现的 AUTH 关键字。发送者地址。实际上，AUTH 验证的是服务器信任的客户端。对于 DIGEST-MD5 身份验证，客户端和服务器必须约定一个共享密码。使用 `saslpassword` 命令配置密码如下：

```
[root]# saslpassword craig
Password: thissecret!
Again (for verification): thissecret!
```

服务器通过 `saslpassword` 定义的密码必须与提供的密码匹配。在配置时定义。

# 配置身份验证客户端

AUTH 客户端与服务器通信的方式有两种：

- 客户端可以运行使用你的服务器的 MUA。某些 MUA（如 pine 和 Eudora）使用 AUTH 扩展。通过这种方法，客户端直接与服务器通信。
- 客户端可以运行 Sendmail 并作为 MTA。在客户端上运行 Sendmail 的优势是任何 MUA 都可以访问 AUTH 扩展。

`defaultAuthInfo` 选项指向在系统作为客户端时用于身份验证信息的文件。默认情况下，此选项未定义，系统在作为客户端时不会尝试使用 AUTH。在 m4 配置文件中使用 `confDEF_AUTH_INFO` 来定义 AUTH 数据文件——

```
define(`confDEF_AUTH_INFO`, `/etc/mail/default-auth-info`)
dnl
```

文件可以命名为任何名称，Sendmail 开发者建议使用 `/etc/mail/default-auth-info`。该文件必须位于只有 root 可写入的目录。文件本身必须由 root 所有且仅允许所有者读取。

文件（示例中为 `default-auth-info`）包含了用于验证 AUTH 客户端的四个信息。用 SASL 术语来说，这四个信息是：

**授权身份（Authorization identity）**：在远程系统上执行操作的身份。这是在远程系统中授予权限的用户名。例如，craig 是一个用户 ID，授予对 craig 拥有的文件的所有权。授权身份决定权限。

**身份验证身份（Authentication identity）**：通过挑战/响应协议进行验证的用户名。它不需要与授权身份相同。然而，一旦身份验证身份（authid）通过验证，它将被接受为授权身份的代理，并授予与授权身份相同的权限。例如，假设 craig 是授权身份，katy 是身份验证身份。身份验证后，katy 获得对 craig 拥有文件的所有权。对于上面的 DIGEST-MD5 示例，身份验证身份应匹配使用 `sas1password` 创建密码的用户名。

