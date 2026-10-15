
Child process of mailrop_pipe transport returned 75 (could mean temporary error) from command: `/usr/bin/maildrop`

此错误表示 Exim 尝试将消息传递给 Maildrop，但 Maildrop 返回了错误代码。最可能的原因是缺少 Maildrop 目录，或者 Maildrop 目录属于某个用户。下一节将介绍如何检测并修复这些问题。

## 连接 Courier 时的登录失败

除了真实的密码错误（可以通过在邮件客户端输入正确的密码来解决），其他某些情况也会导致登录失败。其中某些情况还可能导致暂时的投递问题。正常的登录失败会产生如下日志条目：

```
courierpop3login: LOGIN FAILED. ip=::ffff:1.2.3.4
```

在这种情况下，来自 IP `1.2.3.4` 的用户输入的错误的用户名或密码。

可能发生的其他几个错误将记录在邮件日志中，这意味着你可能需要通过手动连接到 POP3 服务（从邮件服务器或从远程机器）并发送有效的用户名和密码来测试它们。此示例显示了如何在邮件服务器的 shell 提示符上连接 POP3 服务：

```
$ telnet localhost 110

Trying 127.0.0.1...

Connected to localhost.localdomain.

Escape character is '^]'.

+OK Hello here.

USER username

+OK Password required.

PASS password
```

你从服务器收到的响应应类似于以下内容之一：

- `+OK logged in`——此响应是正常的，意味着没有问题。
- `No such file or directory`——这表明服务未运行。
- `Permission denied`——这表明该目录属于另一个用户。
- `Login failed`——这表明用户名或密码错误。
- `Connection refused`——这表明服务未在该端口上监听。

# 第四部分：设置 Linux 服务器

如果你以前没有配置过 crontab 文件，设置它的方法就像输入以下三条命令一样简单：

```
$ cat > mycron

@reboot /usr/bin/fetchmail --daemon 300

<Ctrl+D>

$ crontab mycron
```

## 配置基于 Web 的邮件

如果你正在运行 IMAP 服务器，可以通过安装 SquirrelMail (`http://squirrelmail.org/`) 来提供基于 Web 的访问，该软件也包含在 `squirrelmail` 软件包中。首先将你的系统配置为 LAMP 服务器（参阅第 13 章），然后安装并配置相应的软件包。

## 使用 SSL/TLS 保护通信

由于邮件客户端与服务器之间的通信包含密码等敏感信息，通常建议启用 SSL/TLS 加密。以下是在 Exim 和 Courier 中启用 SSL/TLS 的方法：

- 安装支持 SSL/TLS 的 Courier 守护进程：

```
$ sudo apt-get install courier-imap-ssl courier-pop-ssl
```

- 第三方 CA 证书由 `ca-certificates` 软件包提供。配置中将引用它，因此也需要安装它：

```
$ sudo apt-get install ca-certificates
```

Defconf 会询问你是否要默认信任 CA 证书。在大多数情况下，你应该选择 Yes。

- 如果你使用的是来自尚未被识别的 CA 的证书（如果你运行自己的 CA，通常如此），请将 CA 公钥证书放置在 `/etc/ssl/certs/` 中的对应文件中并更新证书数据库：

```
$ sudo update-ca-certificates
```

- 按照第 13 章所述生成私钥和证书签名请求（CSR）。这些文件的最佳位置是 `/etc/ssl/private/`。以下是一个示例：

```
$ sudo su -

@# cd /etc/exim4
```

# 第 14 章：运行邮件服务器

```
# openssl genrsa -out mail.key 1024

# chmod 640 mail.key

# openssl req -new -key mail.key -out mail.csr

# chown root:Debian-exim mail.key
```

5. 获取你的 CSR（证书签名请求）签名并将证书放置在 `/etc/mail/private/mail.crt`。或者，要制作自签名证书，可以执行以下操作：

```
# cd /etc/exim4

# openssl req -new -x509 -nodes -sha \
-days 365 -key mail.key -out mail.crt

# chmod 640 mail.crt

# chown root:Debian-exim mail.crt
```

## 注意事项

如果你的证书没有它们识别的 CA 签名，某些远程服务器将拒绝向你的服务器发送消息。此外，确保证书上的通用名称 (`cn`) 属性与 DNS 中的服务器名称匹配。

- 6. 将你的密钥和证书合并成一个文件供 Courier 使用：

```
# cd /etc/courier

# cat /etc/exim4/mail.key /etc/exim4/mail.crt > mail.pem

# chmod 600 mail.pem
```

- 7. 通过编辑 `/etc-courier/imapd-ssl` 和 `/etc/courier/pop3d-ssl`，并将 `TLS_CERTFILE` 和 `TLS_TRUSTCERTS` 的值替换为以下内容，从而在 Courier IMAP 和 POP 守护进程中启用 SSL/TLS：

```
TLS_CERTFILE=/etc/courier/mail.pem

TLS_TRUSTCERTS=/etc/ssl/certs/ca-certificates.pem
```

- 8. 告诉 Exim 在哪里找到密钥和证书并启用 TLS。创建一个名为 `/etc/exim4/conf.d/main/12_exim4-config_local_tls_options` 的文件包含包含内容：

```
MAIN_TLS_CERTIFICATE = CONFDIR/mail.crt

MAIN_TLS_PRIVATEKEY = CONFDIR/mail.key

MAIN_TLS_ENABLE = 1
```

- 9. 重启 Exim：

```
# sudo invoke-rc.d exim restart
```
