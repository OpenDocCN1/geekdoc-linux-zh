
> 提示：使用发行版包管理系统（`Yum` 或 `APT`）安装的 `UW-IMAP` 包二进制版本支持 SSL。

不要忘记将新编译的二进制文件复制到 `/usr/local/sbin` 目录并相应设置它们的权限。
通过创建 SSL 证书，你可以使用 `OpenSSL` 轻松地创建一个自签名证书。只需运行

```
[root@serverA imap-2007b]# openssl req -new -x509 -nodes -out imapd.pem \
-keyout imapd.pem -days 3650
```

这将创建一个有效期为十年的证书。将其放在你的 OpenSSL 证书目录中。在 RHEL、Fedora 和 Centos 上，该目录是 `/etc/pki/tls`。

> 注意：如果你使用这种方法创建证书，用户将收到证书未妥善签名的警告。如果你不想这样，将需要从像 VeriSign 这样的证书机构 (CA) 购买证书。然而，取决于你的用户需求，如果你只需要一个用于传输密码的加密隧道，那么自签名证书就可以用。

## 使用 SSL 测试 IMAP 连接性

一旦你迁移到基于 SSL 的邮件服务器，你可能会发现使用 `Telnet` 检查邮件服务器的技巧不再奏效了。因为 `Telnet` 假设线路上没有加密。
解决这个小障碍非常简单；只需使用 `OpenSSL` 作为客户端而非 `Telnet`，例如：

```
[root@serverA ~]# openssl s_client -connect 127.0.0.1:993
```
