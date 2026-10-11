
请注意，第一行将目录 `~/public_html` 定义为各个用户放置其 HTML 内容的位置，这些内容将通过 URL `www.example.com/~user` 提供访问。在这种情况下，您允许对整棵目录树进行完全开放的访问，除非用户在他们的本地 `.htaccess` 文件中另行指定。

您可能需要限制内容树的一部分，仅允许那些主机名和/或 IP 地址符合特定条件的客户端访问。例如，为了将 URL `www.example.com/intranet/` 的访问限制在 `10.10.10.0/24` 子网中的主机，请使用以下指令：

```apache
DocumentRoot "/var/www/html1"
<Directory /var/www/html1/intranet/>
    Allow from 10.10.10.0/24
</Directory>
```

在以下示例中，您正在将同一 URL 的访问限制为反向 DNS 查找（PTR 记录）位于 `example.com` 域名下的主机：

```apache
DocumentRoot "/var/www/html1"
<Directory /var/www/html1/intranet/>
    Allow from .example.com
</Directory>
```

除了 `Allow from` 指令外，Apache 还支持 `Deny from` 指令，并且可以控制这两条指令（`Deny` 和 `Allow`）的评估顺序。考虑以下示例。Apache 服务器在评估 `Allow from` 指令之前先评估 `Deny from` 指令，并且默认允许访问。结果是，除了 `10.10.10.0/24` 网段中的所有主机外，其他所有主机都被允许访问。然而，主机 `10.10.10.1` 是被允许的。

```apache
<Directory /var/www/html1/intranet/>
    Order deny,allow
    Deny from 10.10.10.0/24
    Allow from 10.10.10.1
</Directory>
```

现在考虑下一个示例。在这种情况下，您在评估 `deny from` 指令之前先评估 `allow from` 指令，并且采用“拒绝所有”的策略。这导致除了来自 `10.10.10.0/24` 的连接外，所有客户端连接都被拒绝。在以下示例中，`10.10.10.1` 网段将被允许：

```apache
<Directory /var/www/html1/intranet/>
    Order allow,deny
    Allow from 10.10.10.0/24
    Deny from 10.10.10.1
</Directory>
```

最后，您需要向 `httpd.conf` 文件中添加代码，以防止 Web 用户查看内容树中任何目录下的 `.htaccess` 文件，因为它包含授权信息。以下指令指示 Apache 查找内容树中任何以字符 `.ht` 开头的文件名，并拒绝所有用户访问这些文件。该指令不仅保护了 `.htaccess` 文件，还保护了任何 `.htpasswd` 文件（一种常用于存储密码信息的常见文件名）的出现。

```apache
<Files "^.ht">
    Order allow,deny
    Deny from all
</Files>
```

### 强化 Apache 服务器

与运行在您的 Linux 服务器上的任何其他应用程序一样，您需要确保服务器的操作不会因试图获得未授权访问系统的人侵者而被破坏。除了关注 `www.apache.org` 和 `www.cert.org` 上的最新安全公告和补丁外，在安装过程中进行仔细规划可以在多个方面极大地提高安全性。

**Apache 用户**
虽然 Apache 守护进程必须由 `root` 启动，但至关重要的是，Apache 守护进程不应在具有特权权限的用户名下运行。`httpd.conf` 文件支持两个指令：

- `user apache-user`
- `group apache-group`

`apache-user` 和 `apache-group` 是服务器运行所基于的用户 ID 和组 ID。应将 Apache 用户添加到 `/etc/passwd` 中，并为其设置安全的密码，其主目录应设为内容树。所有内容管理都应使用此用户进行操作。

**内容树的拥有权和权限**
只有 `apache-user` 和 `apache-group` 应该能够写入内容树，且该树应由此用户名/组名组合拥有。以下命令是分配此拥有权的示例：

```bash
[ramon]$ sudo chown -Rh apache:apache /var/www/html
```

**隐藏目录内容**
默认情况下，当浏览器在 URL 中请求目录列表时，Apache 会返回 `DirectoryIndex` 指令下列出的某个文件的内容，例如：

```apache
DirectoryIndex index.html index.htm index.shtml index.php index.php4 index.php3 index.cgi
```

然而，如果这些文件中的某一个暂时不可用，用户实际上可能会看到该目录中所有文件的列表，包括您可能不希望用户列出的脚本文件和头文件。为了防止这种情况，请确保通过执行以下命令关闭内容目录中“组”和“其他”用户的读取权限：

```bash
[ramon]$ cd /var/www
[ramon]$ ls -ld html
drwxr-xr-x 2 apache apache 1024 Dec 4 20:44 html
[ramon]$ sudo -u apache chmod go-r html
[ramon]$ ls -ld html
drwx--x--x 2 apache apache 1024 Dec 4 20:44 html
```

**CGI 脚本**
通用网关接口（CGI）脚本允许您的用户响应 HTTP 输入执行代码，并向远程浏览器返回有意义的内容。与任何可执行文件一样，请确保您的用户编写的是安全的脚本，并且这些脚本的拥有权和权限是正确的。为此，Apache 允许您使用如下 `httpd.conf` 指令将所有 CGI 脚本限制在单个目录中：

```apache
ScriptAlias /cgi-bin/ "/var/www/cgi-bin/*"
```

该指令确保所有 CGI 脚本位于 `/var/www/cgi-bin` 目录中，您可以轻松地跟踪和监控它们。您应定期检查此目录，确保其中没有可被所有用户写入的脚本文件。

**服务器端包含（SSI）**
服务器端包含（SSI）是对静态 HTML 内容的扩展，允许有条件地执行外部程序，以及进行“即时”内容修改。SSI 代表了一个潜在的安全问题，因为很难对 HTML 文件允许执行的程序设定界限。

使用以下指令禁用执行外部程序的 SSI（此功能被称为 `exec`）：

```apache
Options IncludesNOEXEC
```

一旦您以负责任的安全方式安装并配置了 Apache，请监控应用程序日志中的可疑活动。本书的下一节将描述 Apache 的日志设施及其日志文件的内容。

## 应用程序日志

Apache 的标准日志设施提供了全面的诊断功能，允许系统和安全管理员审计常规事件（如成功的 HTTP 请求）以及可疑和潜在的恶意事件。有两个日志文件需要定期检查：

- **`access_log`**
  `access_log` 文件包含针对 HTTP 服务器发出的每个成功请求的一行记录。其通用格式如下：
  ```text
  _remote_host remote_user time_stamp request_type request_status_
  ```
  例如，以下两条记录显示了一个客户端 IP 地址为 `209.1.78.12` 的远程用户试图访问两个对 Apache 服务器不可用的文件（`/etc/shadow` 和 `/etc/passwd`）：
  ```text
  209.1.78.12 - - [04/Dec/2000:21:03:45 -0500] "GET /etc/passwd HTTP/1.1" 404 139
  209.1.78.12 - - [04/Dec/2000:21:03:47 -0500] "GET /etc/shadow HTTP/1.1" 404 139
  ```
  请注意，`request_status` 为 `404` 指的是“文件未找到”的状态。定期搜索此状态代码可能会为那些正在四处寻找未保护内容的潜在入侵者提供重要线索。

- **`error_log`**
  `error_log` 文件记录 Apache 服务器的管理事件，包括服务器启动、停止以及执行特权 CGI 脚本的失败尝试。它还报告与脚本本身特定的执行错误。其通用格式如下：
  ```text
  _time_stamp error_type client_id error_description_
  ```
  例如，考虑以下一组 `error_log` 条目。此示例显示了 Apache 应用程序的非正常关闭，随后立即重启。这是应通过自动日志扫描软件包（如第 3 章“系统监控和日志”中讨论的 `logcheck` 和 `swatch`）进行监控的日志条目之一。
  ```text
  [Mon Dec 4 02:20:50 2000] [notice] httpd: caught SIGTERM, shutting down
  [Mon Dec 4 02:20:57 2000] [notice] Apache/1.3.14 (Unix) configured -- resuming normal operations
  [Mon Dec 4 02:21:00 2000] [warn] pid file /usr/local/apache/var/run/httpd.pid overwritten -- Un clean shutdown of previous apache run?
  ```

## mod_ssl

`mod_ssl` 最初由 Ralf S. Engelschall 于 1998 年初开发，它是 Eric Young 和 Tim Hudson 开发的流行 OpenSSL 实现的 Web 接口。此实现利用了 Apache 的模块化架构，并将安全套接字层（Secure Sockets Layer, SSL）扩展作为外部模块实现于标准的 Apache 源代码树中。

SSL 允许数据隐私。通信的两个端点执行初步握手，并使用对称密钥算法（如 DES 或 RC4）定义用于数据加密的秘密密钥。SSL 还使用消息摘要算法（如 SHA 或 MD5）确保交换的数据的完整性。在通信之前，SSL 端点必须使用公钥密码学进行相互身份验证，其中连接的每一端都必须出示由通常受信任的证书颁发机构（CA）签发的数字证书（通常为 X.509 格式）。

Netscape 开发了最初的 SSL 规范。基于其广泛的成功，IETF 起草了一个类似的标准，称为传输层安全性（Transport Layer Security, TLS），如 RFC 2246 所述。TLS 1.0 基于 SSL v3，虽然它提供了一种 TLS 对等端降级到 SSL v3 的方法，但 TLS 在很大程度上与 SSL 不兼容。OpenSSL 同时支持 SSL 和 TLS。

通过在 TCP 层和 HTTP 应用层之间插入 OpenSSL，`mod_ssl` 使用 SSL 和 TLS 为 Web 客户端与 Apache HTTP 服务器之间的传输添加强身份验证、数据完整性和隐私性。请注意，`mod_ssl` 可以与非安全版本的 Apache 共存。实际上，虽然普通 HTTP 使用 TCP 端口 80 进行控制和数据交换，但所有 HTTPS（安全 HTTP 或基于 SSL 的 HTTP）流量都通过 Linux 服务器上的 TCP 端口 443 传输。

`mod_ssl` 受标准 BSD 许可证保护，使其可免费用于商业和非商业用途。在撰写本书时，`mod_ssl` 占互联网上 Apache 总安装量的 10% 以上，且该数字一直在增长

