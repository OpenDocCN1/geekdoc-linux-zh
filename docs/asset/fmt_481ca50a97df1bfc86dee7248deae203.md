
当 Apache 配置工具保存其设置时，它将覆盖 Apache 配置文件 `/etc/httpd/conf/httpd.conf`。建议首先对 `httpd.conf` 文件进行备份副本，以防您想恢复由发行版为 Apache 创建的原先设置。如果您已手动编辑过此文件，系统将显示警告，并且 Apache 配置工具将在 `/etc/httpd/conf/httpd.conf.bak` 创建备份副本。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_536_0.png)

## ABC Amber CHM 转换器 试用版

请注册以移除此横幅。

http://www.processestext.com/abcchm.html

### Web 服务器安全：SSL

Web 服务器安全涉及两项不同的任务：保护您的 Web 服务器免受未授权访问，以及为在 Web 浏览器客户端与您的 Web 服务器之间进行的事务提供安全保障。为保护服务器免受未授权访问，您需使用代理服务器，如 `Squid`。`Squid` 是一个 GNU 代理服务器，常用于 Linux 系统中的 Apache。 （有关 `Squid` 服务器的详细说明，请参见第 23 章。）Apache 本身具有几个提供安全功能的模块。这些模块包括用于强制控制的 `mod_access`；提供身份验证支持的 `mod_auth`、`mod_auth_db`、`mod_auth_digest` 和 `mod_auth_dbm`；以及用于匿名 FTP 类似登录的 `mod_auth_anon`（参见前面关于访问控制和身份验证的章节）。

为了安全传输，您需要执行三项任务。您必须验证身份、检查数据的完整性，并确保传输的隐私。要验证参与传输的主机身份，您需要执行身份验证程序。要检查数据的完整性，您需要添加包含数据摘要值的数字签名。摘要值是独特代表数据的值。最后，为确保传输的隐私，您需要对其进行加密。浏览器与服务器之间的事务随后可以被加密，只有浏览器和您的服务器能够解密传输。在 Linux Apache Web 服务器上实现安全传输最常用的协议是安全套接字层（SSL）协议，该协议最初由 Netscape 开发用于 Web 上的安全事务。

与第 18 章中描述的 Secure Shell (`SSH`) 和第 16 章中讨论的 `GPG` 类似，SSL 使用公钥和私钥加密的形式进行身份验证。数据使用公钥加密，但只能使用私钥解密。一旦数据经过身份验证，就会使用约定的密码对其进行加密。数字签名对数据的 MD5 摘要值进行加密以确保完整性。身份验证通过使用授权证书进行。证书识别安全传输中的各方，验证它们是否是其所声称的身份。Web 服务器将拥有一个验证其身份的证书，确认其为其声称的服务器。联系服务器的浏览器也将拥有一个标识其身份的证书。这些证书又都是由证书颁发机构签署的，以验证它们是有效证书。证书颁发机构是一个独立的实体，受到双方的信任。

证书包含分配给特定服务器或浏览器的公钥，以及证书颁发机构的数字签名和身份信息，如运行服务器或浏览器的用户或公司名称的有效性。证书的有效性直接取决于签发该证书的证书颁发机构的可靠性。要在互联网上运行安全的 Web 服务器，您应从知名的证书颁发机构（如 `Verisign`）获取证书。`Stronghold` 等商业供应商可以为您完成此操作。许多成熟的公司已经维护自己的证书颁发机构，以确保其公司内部网络传输的安全。SSL 会话通过使用握手序列建立，在此过程中，服务器和浏览器通过交换证书进行身份验证，约定用于加密传输的密码，并选择摘要完整性检查的类型。此外，用于身份验证的公钥加密类型也有选择，可以是 `RSA` 或 `DSA`。对于每个会话，都会建立一个唯一的会话密钥，供浏览器和服务器使用。

有一个免费的开源版 SSL 称为 `OpenSSL`，可用于 Apache（参见 www.openssl.org）。它基于 Eric A. Young 和 Tim J. Hudson 的 `SSLeay`。然而，美国政府的规定阻止 Apache Web 服务器内置 SSL 功能进行自由分发。您必须单独获取 SSL 并更新您的 Apache 服务器以整合此功能。

美国政府维持对超过 40 位加密技术的出口限制。但是，SSL 支持使用 168、128 和 40 位密钥的多种密码（128 被认为安全，因此相比之下，可出口的 40 位版本毫无用处）。这意味着如果 Apache 包含 SSL，它将无法在美国以外分发。然而，在美国以外，有项目使用 `OpenSSL` 为 Apache 分发 SSL。这些项目在美国免费用于非商业用途，但出口限制仍然适用。`Apache-SSL` 项目免费分发内置 SSL 的 Apache（`apache+ssl`）。您可以从其网站 www.apache-ssl.org 下载（虽然对加密技术出口有限制，但对进口没有限制）。此外，`mod_ssl` 项目提供了一个 SSL 模块，您可以使用其补丁更新 Apache Web 服务器以整合 SSL（www.modssl.org）。`mod_ssl` 在类似 Apache 的许可下免费用于商业和非商业用途。Red Hat 在其发行版中包含 `mod_ssl` 模块，位于 `mod_ssl` 软件包中（`/etc/httpd/conf.d/ssl.conf` 配置文件）。

`mod_ssl` 的 SSL 实现提供了一种通过不同端口（`443`）和不同协议（`https`）访问您的 Web 服务器的替代方式。实际上，您同时拥有一个 SSL 服务器和一个非安全版本。要访问安全的 SSL 版本，您在 Web 服务器的 URL 地址中使用 `https` 协议代替 `http`。例如，要访问运行在 `www.mytrek.com` 的 Web 服务器的 SSL 版本，您在其 URL 中使用 `https` 协议，如下所示：

```
https://www.mytrek.com
```

您可以通过在 Apache 配置文件 `httpd.conf` 中使用多个配置指令来配置 `mod_ssl`。在 Red Hat 上，随 Apache 安装的默认配置文件包含一个 SSL 指令部分以及详细的注释。查看 `mod_ssl` 的在线文档 www.modssl.org 获取列出所有指令的详细参考。有全局的、基于服务器的和基于目录的指令可用。

在 Red Hat 的 `httpd.conf` 文件中，SSL 指令的包含由 `HAVE_SSL` 标志启用的 `IfDefine` 块控制。例如，以下代码将加载 SSL 模块：

```
<IfDefine HAVE_SSL>
LoadModule ssl_module modules/libssl.so
</IfDefine>
```

Apache Web 服务器的 SSL 版本在 `httpd.conf` 文件中作为虚拟主机进行设置。SSL 指令由使用 `HAVE_SSL` 标志的 `IfDefine` 块启用。实施了几个默认指令，如 SSL 密钥目录的位置以及服务器 SSL 版本将监听的端口（`443`）。其他指令被注释掉。您可以通过删除前面的 `#` 符号来启用它们，并设置自己的选项。此处展示了几个指令：

```
<IfDefine HAVE_SSL>
#### SSL Virtual Host Context

# Server Certificate:
SSLCertificateFile /etc/httpd/conf/ssl.crt/server.crt

# Server Private Key:
SSLCertificateKeyFile /etc/httpd/conf/ssl.key/server.key

# Certificate Authority (CA):
#SSLCACertificatePath /etc/httpd/conf/ssl.crt
#SSLCACertificateFile /etc/httpd/conf/ssl.crt/ca-bundle.crt
```

在 `/etc/httpd/conf` 目录中，`mod_ssl` 将设置几个 SSL 目录，其中将包含 SSL 身份验证和加密密钥及数据。`ssl.crt` 目录将保存服务器的证书。`ssl.key` 目录保存用于身份验证加密的公钥和私钥。用于吊销过期证书的吊销列表保存在 `ssl.crl` 中。`ssl.csr` 目录保存用于向证书颁发机构请求官方证书的证书签名请求。`ssl.prm` 保存 `DSA` 密钥加密方法使用的参数文件。查看每个目录中的 `README` 文件以获取有关其所含 SSL 文件的详细信息。

`mod_ssl` 安装将为您提供一个名为 `snakeoil` 的演示证书，您可以使用它来测试您的 SSL 配置。当您拥有官方证书时，您可以在 `ssl.crt` 目录内使用 `make certificate` 命令安装它。这将覆盖 `server.crt` 服务器证书文件。

### 第 23 章：代理服务器-Squid

#### 概述
