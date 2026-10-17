
`/etc/passwd`

`DNSSEC`

`dnssec-keygen`

`dnssec-signzone`

# 第 18 章 ■ 域名服务器 (主题 207) 185

1. 哪个配置文件用作 `BIND` 服务器的默认配置？

   A. `named.conf`
   B. `named.cfg`
   C. `bind.cfg`
   D. `bind.conf`

2. `BIND` 配置中的哪个指令指定允许查询的地址或网络？

   A. `query-addresses`
   B. `allow-query`
   C. `query-allow`
   D. `query-auth`

3. `kill` 命令的哪个信号可以用于指示 `BIND` 应该重新加载配置？

   A. `-15`
   B. `-1`
   C. `-9`
   D. `-2`

4. `dnssec-keygen` 的哪个选项指定密钥使用的算法？

   A. `-a`
   B. `-n`
   C. `-d`
   D. `-e`

5. 下列哪项描述了 `named-compilezone` 和 `named-checkzone` 的基本区别？

   A. `named-checkzone` 和 `named-compilezone` 事情。
   B. `named-checkzone` 检查区域错误，并将输出发送到文件。
   C. `named-checkzone` 执行语法检查，而 `named-compilezone` 将区域转换为不同的格式。
   D. `named-checkzone` 执行语法检查，而 `named-compilezone` 为使用 `BIND` 准备区域。

6. 在创建 `MX` 记录时，下列哪个优先级最高？

   A. `0`
   B. `10`
   C. `20`
   D. `100`

# 第二部分 ■ LPIC-2

7. 区域传输请求在哪个协议和端口上发送？

   A. `UDP/53`
   B. `ICMP/53`
   C. `TCP/143`
   D. `TCP/53`

8. `BIND` 的区域文件存储在下列哪个目录中？

   A. `/var/named`
   B. `/etc/named`
   C. `/var/cache`
   D. `/var/namedzones`

9. 下列哪个命令用于控制 `BIND` 服务器？

   A. `bind-config`
   B. `named-config`
   C. `rndc`
   D. `rdmc`

10. `dig` 命令可以使用哪种类型来测试区域传输？

    A. `xfr`
    B. `transfer`
    C. `zxfr`
    D. `axfr`

11. `BIND` 配置中的哪个指令设置守护进程监听的 IP 地址？

    A. `listeners`
    B. `listen-on`
    C. `listen-in`
    D. `ip-listeners`

12. 在为 `chroot` 场景配置 `BIND` 时，应该在下列哪个文件中为 `chroot` 用户设置主目录？

    A. `/etc/bind.home`
    B. `/etc/bind.user`
    C. `/etc/passwd`
    D. `/etc/bindauth`

13. 哪个命令用于为 `DNSSEC` 签名区域？

    A. `dnssec-signzone`
    B. `signzone`
    C. `bind-signzone`
    D. `dnssec-sign`

# 第 18 章 ■ 域名服务器 (主题 207) 187

14. `host` 命令的哪个选项将查询类型设置为 `ANY`？

    A. `-a`
    B. `-b`
    C. `-c`
    D. `-d`

15. 下列哪项正确地在主机名和 `host web.example.com` 之间创建了 `CNAME` 记录？

    A. `www CNAME web.example.com`
    B. `web.example.com CNAME www`
    C. `www IN CNAME web.example.com.`
    D. `www IN CNAME web.example.com`

16. `BIND forward` 指令的哪个选项将服务器设置为转发服务器？

    A. `only`
    B. `first`
    C. `now`
    D. `required`

17. 当运行递归名称服务器时，下列哪个选项拒绝提供来自给定地址的回答？

    A. `deny-hosts`
    B. `blackhole`
    C. `deny-query`
    D. `deny-answer`

18. 下列哪个是安装 `djbdns` 的先决条件？

    A. `bind9`
    B. `daemontools`
    C. `qmail`
    D. `bind-tools`

19. 哪个命令可以验证 `BIND` 配置文件有效？

    A. `bind9-ver`
    B. `bind-check`
    C. `config-check`
    D. `named-checkconf`

20. 下列哪个 `TTL` 值代表八小时？

    A. `8`
    B. `480`
    C. `28800`
    D. `86400`

21. 假设有以下 `BIND` 区域文件部分，值 `1800` 代表什么？

```
@ IN SOA cwa.example.org. root.example.org. (
201607400
3600
1800
604800
86400
)
```

    A. `Refresh`
    B. `Retry`
    C. `Default TTL`
    D. `Serial`

22. 哪种资源记录类型用于 `SPF` 记录？

    A. `SPF`
    B. `MX`
    C. `TXT`
    D. `MAIL`

23. 下列哪项定义了一个优先级为 `10` 的 `MX` 记录？

    A. `MX 10 mail.example.com.`
    B. `10 MX mail.example.com.`
    C. `mail.example.com 10 MX`
    D. `mail.example.com MX 10`

24. 在哪个哪个文件中可以为 `dig` 命令创建每个用户的默认设置？

    A. `/etc/dig.cfg`
    B. `/etc/dig.conf`
    C. `~/.digrc`
    D. `~/.dig.conf`

25. `mount` 命令的哪个选项有助于方便在 `chroot` 环境中运行 `BIND`？

    A. `--bind`
    B. `--chroot`
    C. `--lift`
    D. `--secure`

26. 在设置递归名称服务器时，根根提示文件（root hints file）设置的是哪种类型的区域？

    - A. 主节点 (Master)
    - B. 从节点 (Slave)
    - C. 递归 (Recurse)
    - D. 提示 (Hint)

27. 对 `DNS` 区域进行更改后，可以使用以下哪个命令重新加载区域使更改生效？

    - A. `rndc reload`
    - B. `rndc restart-zones`
    - C. `rndc zone-reload`
    - D. `rndc-rel`

28. `BIND` 区域配置中的哪个配置选项指定了允许请求区域传输的主机？

    - A. `allow-axfr`
    - B. `allow-xfr`
    - C. `allow-trans`
    - D. `allow-record`

29. 哪种 `DNS` 记录用于指定 `POP3` 服务器？

    - A. `POP`
    - B. `PO`
    - C. `MX`
    - D. 没有针对 `POP3` 服务器的特定类型。

30. `BIND` 配置中的哪个指令允许指定允许使用服务器进行递归查询的主机或网络？

    - A. `allow-recurs`
    - B. `allow-recursive`
    - C. `allow-recursion`
    - D. `allow-rec`

31. 下列哪项是 `named-checkzone` 命令的正确格式？

    - A. `named-checkzone <zone> <zonefile>`
    - B. `named-checkzone -z <zone>`
    - C. `named-checkzone -f <zonefile>`
    - D. `named-checkzone <zonefile> <zone>`

## 190 第二部分 ■ LPIC-2

32. 使用 `dnssec-keygen` 生成密钥时，`rndc` 认证 必须使用哪种算法？

    - A. `sha1`
    - B. `sha256`
    - C. `md5`
    - D. `hmac-md5`

33. 下列哪条配置指令告诉 `BIND` 不要公布其版本号？

    - A. `allow-version { none }`
    - B. `version none;`
    - C. `allow-query-version { none; }`
    - D. `query-version no;`

34. `named-checkconf` 的哪个选项用于对配置文件中列出的所有主区域进行测试？

    - A. `-l`
    - B. `-f`
    - C. `-z`
    - D. `-d`

35. 你在区域中的一个单独记录中指定 `TTL` 为 `300`，而区域本身具有 `86400` 的默认 `TTL`。当你在重启 `BIND` 后，对该单独记录进行更改，需要多长时间更改才能传播到外部解析器？

    - A. 最长 `86400` 秒
    - B. 最长 `300` 秒
    - C. 重启后更改立即生效。
    - D. 从所提供的信息无法判断。

36. 下列哪个包分别在 `Debian` 和 `Red Hat` 上安装 `PowerDNS` 权威名称服务器？

    - A. `Debian` 上的 `pdns-server` 和 `Red Hat` 上的 `pdns`
    - B. `Debian` 上的 `pdns` 和 `Red Hat` 上的 `pdns-server`
    - C. `Debian` 和 `Red Hat` 上均使用 `pdns`
    - D. `Debian` 和 `Red Hat` 上均使用 `pdns-server`

37. 下列哪个命令可以重启 `BIND` 服务器，使 `named.conf` 文件的更改生效？

    - A. `rndc reload`
    - B. `rndc reconfig`
    - C. `named reboot`
    - D. `restart bind`

# HTTP 服务

## (主题 208)

本章涵盖了以下 `LPIC-2` 考试主题：

- 208.1 基础 `Apache` 配置
  - `Apache` 2.4 配置、术语和工具
  - `Apache` 日志文件配置和内容
  - 访问限制方法和文件
  - `mod_perl` 和 `PHP` 配置
  - 客户端用户身份认证文件和工具
  - 最大请求数、最小和最大服务器及客户端的配置
  - `Apache` 2.4 虚拟主机实现（带和不带专用 IP 地址）
  - 在 `Apache` 配置中使用重定向语句（`redirect`）来自定义文件访问
  - 以下是所用文件、术语和工具的部分列表：
    - 访问日志和错误日志
    - `.htaccess`
    - `httpd.conf`
    - `mod_auth_basic`, `mod_authz_host` 和 `mod_access_compat`
    - `htpasswd`
    - `AuthUserFile`, `AuthGroupFile`
    - `apachectl`, `apache2`
    - `httpd`, `apache2`

- 208.2 `HTTPS` 的 `Apache` 配置
  - `SSL` 配置、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  ![](img/84990579543ce21a46ac6dc507fcde32_230_0.png)
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.3 `Squid` 的配置
  - `SSL` 配置文件、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.4 作为反代理的 `Squid`
  - `SSL` 配置文件、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

- 208.5 作为反代理的 `Nginx`
  - `Nginx` 配置
  - `SSL` 配置文件、工具和实用
  - 为商业 `CA` 生成服务器私钥和 `CSR`
  - 生成自签名证书
  - 安装密钥和证书，包括中间 `CA`
  - 使用 `SNI` 配置虚拟主机
  - 了解虚拟主机和 `SSL` 使用中的问题
  - `SSL` 使用过程中的安全问题，禁用不安全的协议和加密算法
  - 以下是所用文件、术语和工具的部分列表：
    - `Apache2` 配置文件
    - `/etc/ssl/`, `/etc/pki/`
    - `openssl`, `CA.pl`
    - `SSLEngine`, `SSLCertificateKeyFile`, `SSLCertificateFile`, `SSLCertificatePath`
    - `SSLProtocol`, `SSLCipherSuite`, `ServerTokens`, `TraceEnable`

# 域名解析服务器 (主题 207)

1. 在设置递归名称服务器时，根根提示文件（root hints file）设置的是哪种类型的区域？
   - A. 主节点
   - B. 从节点
   - C. 递归
   - D. 提示

2. 对 `DNS` 区域进行更改后，可以使用以下哪个命令重新加载区域使更改生效？
   - A. `rndc reload`
   - B. `rndc restart-zones`
   - C. `rndc zone-reload`
   - D. `rndc-rel`

3. `BIND` 区域配置中的哪个配置选项指定了允许请求区域传输（`zone transfer`）的主机？
   - A. `allow-axfr`
   - B. `allow-xfr`
   - C. `allow-trans`
   - D. `allow-record`

4. 哪种 `DNS` 记录用于指定 `POP3` 服务器？
   - A. `POP`
   - B. `PO`
   - C. `MX`
   - D. 没有针对 `POP3` 服务器的特定类型。

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

7. 使用 `dnssec-keygen` 生成密钥时，`rndc` 认证 必须使用哪种算法？
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

10. 你在区域中的一个单独记录中指定 `TTL` 为 `300`，而区域本身具有 `86400` 的默认 `TTL`。当你在重启 `BIND` 后，对该单独记录进行更改，需要多长时间更改才能传播到外部解析器？
    - A. 最长 `86400` 秒
    - B. 最长 `300` 秒
    - C. 重启后更改立即生效。
    - D. 从所提供的信息无法判断。

11. 下列哪个包分别在 `Debian` 和 `Red Hat` 上安装 `PowerDNS` 权威名称服务器？
    - A. `Debian` 上的 `pdns-server` 和 `Red Hat` 上的 `pdns`
    - B. `Debian` 上的 `pdns` 和 `Red Hat` 上的 `pdns-server`
