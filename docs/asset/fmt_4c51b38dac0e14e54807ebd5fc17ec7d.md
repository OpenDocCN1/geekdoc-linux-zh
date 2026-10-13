
(2) DSA（仅签名）

(5) RSA（仅签名）

2. 按回车选择默认选项，因为这足够用了。GPG 会提示你输入密钥长度（位数）。

3. 按回车接受 1024 位的默认值。GPG 询问你密钥何时过期。默认是永不过期。

4. 如果默认值就是你想要的（为什么不这样呢？），按回车。

5. 当 GPG 询问你是否真的想要密钥永不过期时，按 Y 确认。GPG 提示你输入姓名、电子邮件地址，最后是注释，以便该密钥对与你的姓名关联。

6. 输入每项被请求的信息并按回车。

7. 当 GPG 给你机会更改信息或按原样确认（通过输入 `o` 然后按回车）时，GPG 会提示你输入一个保护私钥的短语。输入一个包含大小写字母、数字和标点符号的长短语——越长越好——然后按回车。仔细选择一个你容易记住的短语。GPG 会生成密钥。它可能会要求你在电脑上执行一些操作，以便随机生成器能为密钥生成足够的数字。

## 交换密钥

要与他人通信，你必须给他们你的公钥。你也必须从可能给你发送消息的人那里获取公钥（或者有人签署了文件而你想验证签名）。GPG 将公钥保存在你的密钥环中。要列出密钥环中的密钥，请输入

```
gpg --list-keys
```

要发送你的公钥或将其放在网站上，你必须将密钥导出到文件。最好的方法是将密钥导出到文件。使用以下命令将公钥导出为 ASCII 格式的文件：

```
gpg --armor --export youremail@example.com > yourkey.asc
```

# 使用 GnuPG 加密和签名文件

## 签名文件

如果你向某人发送文件并希望向接收者确认文件没有被篡改，且确实是由你发送的，你可能会发现签名很有用。GPG 让文件签名变得非常简单。当你使用以下命令对名为 `message` 的文件进行压缩和签名时：

```
gpg -o message.sig -s message
```

要验证签名，

```
gpg --verify message.sig
```

要获取原始文档，只需输入

```
gpg -o message --decrypt message.sig
```

有时候，你并不关心保持消息的机密，只想对其进行签名以证明该消息是由你发出的。在这种情况下，你可以使用以下命令生成并附加一个明文签名：

```
gpg -o message.asc --clearsign message
```

这基本上是向文本消息附加了一个明文签名。以下是一个典型的明文签名块：

> -----BEGIN GPG SIGNATURE-----
> 
> Version: GPG v1.2.4 (GNU/Linux)
> 
> idDB0BFAfdDHOH/bud6KS5MRRAO5VAJSGS1waZ36P0JWKZZVSDVCMjphZFACEIYFBYSZMEEDawAtHeq6IM=-yu0=
> 
> -----END GPG SIGNATURE-----

当消息附加了明文签名后，你可以使用以下命令通过 GPG 验证签名：

```
gpg --verify message.asc
```

输出的最后一行显示签名良好。

## 加密和解密文档

要对发给接收者的消息加密，你可以使用 GPG 的 `--encrypt`（或 `-e`）命令。如果你有我的 GPG 公钥，你可以像这样为我加密消息：

```
gpg -o message.gpg -e naba@comcast.net message
```

该消息使用我的公钥加密（无任何签名）。

当我收到 `message.pgp` 文件时，我必须使用我的私钥对其进行解密。我使用的命令是：

```
gpg -o message --decrypt message.pgp
```

GPG 会提示我输入密码以解锁私钥，然后解密消息并将输出保存到 `message` 文件中。

如果你只是想加密一个文件且没有其他人解密该文件，可以使用 GPG 进行对称加密。在这种情况下，你提供一个密码并使用以下 GPG 命令加密文件：

```
gpg -o secret.pgp -c somefile
```

GPG 会提示你输入密码并要求你重复输入密码（以确保你没有输入任何错误）。然后，GPG 将使用从密码生成的密钥加密文件。

要解密用对称密钥加密的文件，请输入

```
gpg -o myfile --decrypt secret.pgp
```

GPG 会提示你输入密码。如果你输入正确的密码，GPG 将解密文件并将输出（在本例中）保存到 `myfile` 文件中。

## 监控系统安全

即使你加固了系统，也必须定期检查日志文件，以寻找入侵的迹象。你可能想要安装 Tripwire 软件来监控关键系统文件和目录的完整性。Fedora Core 不带 Tripwire 软件包。要使用 Tripwire，你需要从 www.tripwire.org/downloads/index.php 下载。你需要下载源码 tarball（源文件的压缩归包），然后编译 Tripwire。（第 VI 卷第 4 章提供了更多关于如何从源文件构建软件包的信息）。在构建并安装 Tripwire 后，你可以配置它监控你系统中指定系统文件和目录的任何更改。

定期检查日志文件。许多 Fedora Core 应用（包括某些服务器）使用 syslogd 的日志功能写入日志信息。

### 日志文件位置

在 Fedora Core 系统中，由 syslog 写入的日志文件位于 `/var/log` 目录。确保只有 root 用户可以读写这些文件。

syslog 配置文件为 `/etc/syslog.conf`。syslog 的默认配置会生成必要的日志文件；但如果你想检查并理解配置文件，请输入 `man syslog` 获取更多信息。

定期监控日志文件：

- `/var/log/messages` 包含各种日志消息，从用户登录到 TCP wrapper 提供的消息。
- `/var/log/secure` 包含服务的报告，例如 `in.telnet` 和 `in.ftpd`，通过 TCP wrapper 启动的 `xinetd`。
- `/var/log/maillog` 包含 sendmail 的报告。
- `/var/log/xferlog` 包含所有 FTP 文件传输的日志。

Fedora Core 自带图形化日志文件查看器。要使用此工具，请从 GNOME 面板选择 `Main Menu=Tools>System Logs`。图 2-3 显示了系统日志。

图 2-3：使用 System Logs 工具查看日志文件。

![](img/d9230b719dc0efd80851f36d8c6f571_581.png)

System Logs 工具可以很方便的使用。你可能查看日志以寻找入侵的迹象。Fedora Core 的各种日志消息从用户登录到 TCP wrapper 提供的消息。
