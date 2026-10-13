
- 3. 关闭配置文件，并在 root shell 中执行 `mkdir -p /www/docs/server1.example.com`。
- 4. 在服务器文档根目录下创建一个名为 `index.html` 文件，并确保其内容为“Welcome to server!”。
- 5. 使用 `semanage -a -t httpd_sys_content_t "www/(.*)"`，随后执行 `restorecon -r /www`。
- 6. 用编辑器打开 `/etc/httpd/httpd.conf` 文件，取消行首 `NameVirtualHost*:80` 前的 `#` 号。
- 7. 使用 `service httpd restart` 重启 Apache Web 服务器。
- 8. 使用 `elinks http://server1.example.com`。你现在应该可以看到 server1 的欢迎页面。
- 9. 回到 root shell，将 `/etc/httpd/conf.d/server1.example.com.conf` 文件复制为名为 `/etc/httpd/conf.d/server2.example.com.conf` 的文件。
- 10. 用 vi 打开 `server2.example.com.conf` 文件，并使用 vi 命令 `%s/server1/server2/g`。这将所有的 `server1` 替换为文本 `server2`。
- 11. 创建 `/www/docs/server2.example.com` 文档根，设置 SELinux 标签，并在其中创建一个包含内容“Welcome to server2”的 `index.html` 文件。
- 12. 重启 httpd，验证 server1 和 server2 均可访问。在上一个练习中，你创建了两个虚拟主机并验证了它们都按预期工作。随着虚拟主创建，你在 16.1 中配置的 Web 服务器不再工作了。如果你尝试使用 `elinks http://localhost` 命令访问此 Web 服务器，你将访问到 Apache 找到的第一个虚拟服务器。此过程按字母顺序进行，根据 httpd 如何找到服务器配置文件，它将默认向你显示服务器配置。

在配置带有多个 Web 服务器的服务器时，确保你最重要的部分排在前面。也就是说，确保如果 httpd 找不到用户尝试访问的站点，它会加载最重要网站的配置。你可以通过让配置文件名在字母顺序上靠前来实现；该网站将作为默认站点。

![](img/3a7e027360b64bc83d5cf9a2db902251_427_0.png)

# 使用证书保护 Web 服务器

对于某些 Web 服务器来说，SSL 不是问题；但对于另一些来说是。要使用 SSL，你需要安装 `mod_ssl`。该模块默认未安装，因此你需要手动安装。安装 `mod_ssl` 后，你会在 `/etc/httpd/conf.d` 中找到它的配置文件。

# 使用 TLS 证书保护 Web 服务器

除了这四条指令外，所有其他指令都可以保持不变。然而，在使用 SSL 时，有一个重要的更改是你应该执行的。`localhost.crt` 证书并不包含你所使用的服务器的名称。由于这个原因，它会被大多数 SSL 客户端拒绝。因此，你需要用一个包含你所使用的服务器名称的自生成（自签名证书来替换它。在练习 16.5 中，你将学习如何设置基于 SSL 的虚拟主机。除非签名者的公钥位于浏览器中，否则自签名证书将被拒绝。请阅读第 13 章“配置你的服务器共享文件”，获取更多有关 PKI 证书的详细信息。

## 练习 16.5

### 设置基于 SSL 的虚拟主机

在此练习中，你将设置一个基于 SSL 的虚拟主机。使用你在练习 16.3 中设置的 `server1.example.com` 主机，并使其可以通过 SSL 端口进行访问。

- 1. 打开 root 终端，使用 `cd` 进入 `/etc/httpd/conf` 目录。在此目录下，创建一个名为 `server1_ssl.conf` 的文件，并为其赋予以下内容：

```apache
<VirtualHost *:443>

DocumentRoot "/www/docs/server1.example.com"

ServerName server1.example.com:443

ErrorLog logs/server1_ssl_error_log

TransferLog logs/server1_ssl_access_log

LogLevel warn

SSLEngine on

SSLProtocol ALL:-SSLv2

SSLCipherSuite ALL:ADH:EXPORT:SSLv2:RC4+RSA:HIGH:+MEDIUM:+LOW

SSLCertificateFile /etc/pki/tls/certs/localhost.crt

SSertificateKeyFile /etc/pki/tls/private/localhost.key

</VirtualHost>
```
