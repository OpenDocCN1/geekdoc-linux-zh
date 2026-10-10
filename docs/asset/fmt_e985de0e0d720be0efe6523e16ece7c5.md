
- C. Debian 和 Red Hat 上均使用 `pdns`

- D. Debian 和 Red Hat 上均使用 `pdns-server`

12. 下列哪个命令可以重启 `BIND` 服务器，使 `named.conf` 文件的更改生效？

- A. `rndc reload`

- B. `rndc reconfig`

- C. `named reboot`

- D. `restart bind`

## HTTP 服务

（主题 208）

本章涵盖了以下 LPIC-2 考试主题：

- 208.1 基础 Apache 配置

  - Apache 2.4 配置文件、术语和工具

  - Apache 日志文件配置和内容

  - 访问限制方法和文件

  - `mod_perl` 和 PHP 配置

  - 客户端用户身份认证文件和工具

  - 最大请求数、最小和最大服务器及客户端的配置

  - Apache 2.4 虚拟主机实现（带和不带专用 IP 地址）

  - 在 Apache 配置中使用重定向语句来自定义文件访问

  - 以下是所用文件、术语和工具的部分列表：

    - 访问日志和错误日志

    - `.htaccess`

    - `httpd.conf`

    - `mod_auth_basic`, `mod_authz_host` 和 `mod_access_compat`

    - `htpasswd`

    - `AuthUserFile`, `AuthGroupFile`

    - `apachectl`, `apache2`

    - `httpd`, `apache2`

- 208.2 HTTPS 的 Apache 配置

  - SSL 配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  ![](img/84990579543ce21a46ac6dc507fcde32_230_0.png)

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.3 Squid 的配置

  - SSL 配置配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.4 作为反代理的 Squid

  - SSL 配置配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.5 作为反代理的 Nginx

  - Nginx 配置

  - SSL 配置配置文件、工具和实用

  - 为商业 CA 生成服务器私钥和 CSR

  - 生成自签名证书

  - 安装密钥和证书，包括中间 CA

  - 使用 SNI 配置虚拟主机

  - 了解虚拟主机和 SSL 使用中的问题

  - SSL 使用过程中的安全问题，禁用不安全的协议和加密算法

  - 以下是所用文件、术语和工具的部分列表：

  - Apache2 配置文件

  - `/etc/ssl/`, `/etc/pki/`

  - `openssl`, `CA.pl`

  - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`

  - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

## 域名解析服务器（主题 207）

1. 在设置递归名称服务器时，根根提示文件（root hints file）设置的是哪种类型的区域？

- A. 主节点

- B. 从节点

- C. 递归

- D. 提示

2. 对 DNS 区域进行更改后，可以使用以下哪个命令重新加载区域使更改生效？

- A. `rndc reload`

- B. `rndc restart-zones`

- C. `rndc zone-reload`

- D. `rndc-rel`

3. `BIND` 区域配置中的哪个配置选项指定了允许请求区域传输（zone transfer）的主机？

- A. `allow-axfr`

- B. `allow-xfr`

- C. `allow-trans`

- D. `allow-record`

4. 哪种 DNS 记录用于指定 POP3 服务器？

- A. `POP`

- B. `PO`

- C. `MX`

- D. 没有针对 POP3 服务器的特定类型。

5. `BIND` 配置中的哪个指令允许指定允许使用服务器进行递归查询的主机或网络？

- A. `allow-recurs`

- B. `allow-recursive`

- C. `allow-recursion`

- D. `allow-rec`

6. 下列哪项是 `named-checkzone` 命令的正确格式？

- A. `named-checkzone <zone> <zonefile>`

- B. `named-checkzone -z <zone>`

- C. `named-checkzone -f <zonefile>`

- D. `named-checkzone <zonefile> <zone>`

7. 使用 `dnssec-keygen` 生成密钥时，`rndc` 认证必须使用哪种算法？

- A. `sha1`

- B. `sha256`

- C. `md5`

- D. `hmac-md5`

8. 下列哪条配置指令告诉 `BIND` 不要公布其版本号？

- A. `allow-version { none }`

- B. `version none;`

- C. `allow-query-version { none; }`

- D. `query-version no;`

9. `named-checkconf` 的哪个选项用于对配置文件中列出的所有主区域进行测试？

- A. `-l`

- B. `-f`

- C. `-z`

- D. `-d`

10. 你在区域中的一个单独记录中指定 `TTL` 为 300，而区域本身具有 86400 的默认 `TTL`。当你在重启 `BIND` 后，对该单独记录进行更改，需要多长时间更改才能传播到外部解析器？

- A. 最长 86400 秒

- B. 最长 300 秒

- C. 重启后更改立即生效。

- D. 从所提供的信息无法判断。

11. 下列哪个包分别在 Debian 和 Red Hat 上安装 `PowerDNS` 权威名称服务器？

- A. Debian 上的 `pdns-server` 和 Red Hat 上的 `pdns`

- B. Debian 上的 `pdns` 和 Red Hat 上的 `pdns-server`

- C. Debian 和 Red Hat 上均使用 `pdns`

- D. Debian 和 Red Hat 上均使用 `pdns-server`

12. 下列哪个命令可以重启 `BIND` 服务器，使 `named.conf` 文件的更改生效？

- A. `rndc reload`

- B. `rndc reconfig`

- C. `named reboot`

- D. `restart bind`

19. 以下哪一个 `RedirectMatch` 指令会在用户尝试查看 `.git` 目录时向用户提供“页面未找到”（Page Not Found）错误？

- A. `RedirectMatch 404 /\.git(/|$)`

- B. `RedirectMatch PageNotFound /.git/`

- C. `RedirectMatch 404 .git`

- D. `RedirectMatch .git 404`

20. Apache 配置中的以下哪一个指令告诉服务器 SSL 私钥的路径？
