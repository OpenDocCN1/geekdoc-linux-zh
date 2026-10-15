
```
--with-autoupid-pop --without-gdbm \
--enable-keep-temp-drop \
--enable-standalone
```

现在，运行 `make` 和 `install` 来构建一个以独立模式运行的 Qpopper 版本。它仍然会被安装在 `/usr/local/libexec`。不要从此位置移动它，因为这将导致以后卸载变得困难。

你需要在系统启动期间启动独立 Qpopper 进程；可以通过在 `/usr/local/etc/rc.d` 中创建一个启动脚本（例如 `qpopper.sh`）来实现，正如你在第 14 节“系统配置与启动脚本”中看到过的。如果你需要，请确保 `qpopper` 没有在 `inetd` 中启用。

# 启用服务器模式

如果你的系统只有通过 POP3 访问邮件信箱的用户——即没有用户可以访问或运行基于 shell 的服务端邮件程序——可能会选择为 Qpopper 启用服务器模式。

服务器模式允许 Qpopper 以更精简的方式运行。与其将邮件邮件池文件复制到临时副本、锁定它、跟踪会话期间到达的邮件以及将锁定的邮件池管理回原始位置，服务器可以直接从邮件信箱文件工作。然而，请注意，服务器模式可能是危险的，特别是如果有用户通过其他方法（如基于 shell 的邮件客户端或使用 IMAP 的邮件程序）访问他们的邮件池文件。因此，只有当你的系统专门通过 POP3 为用户提供邮件，并且负载足够大让你认为这种性能提升措施是必要的时，才应该使用服务器模式。

你有多种方法启用服务器模式。最简单是在调用行中使用 `-S` 切换，但在 `inetd.conf` 中或如果你使用独立模式则在命令行中使用：

```
pop3 stream tcp root /usr/local/libexec/qpopper qpopper -S $
```
这将使 Qpopper 对所有用户始终处于服务器模式。不过，你也可以根据需要按用户或组组进行。要让 Qpopper 使用配置文件，请在 `/usr/local/etc/qpopper` 中创建一个（命名为 `qpopper.conf`），然后在 `inetd.conf` 的命令行中使用 `-f` 选项指定它：

```
pop3 stream tcp root /usr/local/libexec/qpopper qpopper -f /usr/local/etc/qpopper/qpopper.conf
```
现在，在 `qpopper.conf` 中，使用 `group-server-mode` 关键字指定包含或排除在服务器模式下的组。以下示例开启了 `group1` 成员的服务器模式并关闭了 `group2` 成员的：

```
set group-server-mode=group1
set group-mode=group2
set-server-mode=group3
```
你也可以按用户单独使用这种技术。你可能为不同的用户配置不同的 Qpopper——如果系统中的不同用户想使用该模式而另一些用户不想。要这样做，你需要在调用行中添加 `-u` 切换（以启用用户配置文件）。然后，每个想要该模式的用户都应该在他们的目录下有一个名为 `.qpopper.options` 的文件，其中包含 `set server-mode` 这一行。或者，如果你不想让每个用户都能修改他们的 `.qpopper.options` 文件，请使用 `-U` 切换代替 `-u`，并在 `/var/mail` 中放置相应的文件 `.user.user.options`（其中 `user` 是涉及的用户名）。这允许你以个人身份运行。如果你这样做这样做，请不要使用全局服务器模式切换！

# 启用 SSL 加密

安全套层（SSL） 是 FreeBSD 中包含的一组库，它用于加密特定服务的流量，这样如果携带该服务流量的数据包被监听者截获，没有适当的加密密钥将无法被解密。SSL 最常用于网络流量，但其在 POP3 等服务上的使用也有益处。

默认情况下，Qpopper 在构建时将带有隐式的 TLS/SSL 支持。然而，为了利用这一点，你需要使用 FreeBSD 内置的 OpenSSL 库创建并安装安全证书。首先，为你的证书创建一个目录：

```bash
# mkdir -p -m665 /etc/mail/certs
# chown root:mail /etc/mail/certs
```
默认，Qpopper 将将带有隐式的 TLS/SSL 支持。然而，创建一个创建一个证书。接下来，使用 `openssl` 命令生成证书请求。这将要求输入有关你组织的准确信息（在此所示的交互式中生成证书请求）。之后，确保私钥文件的权限允许 root 查看：

```bash
# openssl req -new -nodes -out req.pem -keyout /etc/mail/certs/cert.pem
# chmod 600 /etc/mail/certs/cert.pem
```
完成后，你需要向证书颁发机构（CA）（如 Verisign）提交证书请求。然后你将获得一个签名证书。将其合并到 `cert.pem` 的末尾：

```bash
# cat signed_req.pem >> /etc/mail/certs/cert.pem
```
或者，直接用 `signed_req.pem` 替换旧的 `cert.pem`。现在，为 `/usr/local/etc/qpopper/qpopper.conf` 添加 TLS/SSL 支持，重启服务器（如果它是独立模式运行），SSL 加密就属于你了。任何支持 SSL 的客户端现在都可以协商安全连接。以下行应添加到 `qpopper.conf` 文件中：

```
set tls-support = yes
set tls-cert-file = /etc/mail/certs/cert.pem
```
有时向第三方机构证书是不可行的。如果你愿意，可以模拟证书颁发机构创建一个自签名证书，以便系统工作。然而，启用 SSL 的客户端不会信任此证书，并要求用户手动批准后才能继续。

首先，创建 CA 的私钥（记住你输入的密码），然后创建 CA 证书：

```bash
# openssl genrsa -des3 -out ca.key 1024
#...
# openssl req -new -x509 -days 365 -key ca.key -out ca.crt
```
现在，你可以签名请求的证书（`req.pem`）：

```bash
# openssl x509 -req -CA ca.crt -CAkey ca.key -days 365 -in req.pem -out signed_req.pem -CAcreateserial
```
