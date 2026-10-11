
# SSL

SSL 用于在 Web 浏览器和 Web 服务器之间建立加密连接，确保信息不被窃听（如 `FTP` 等协议）。SSL 提供三项功能：通过数字签名验证客户端和服务器身份，通过加密防止数据窃听，通过哈希保护数据完整性。SSL 通过受信任机构（`CA`）签署的证书允许客户端和服务器交换密钥。生成的随机密钥用于加密连接（防止中间人攻击）。生成的随机密钥用于加密会话。U.S. 出口限制国外仅使用 40 位密钥，这可以被破解。SSL：如果你想设置 SSL Web 服务器，需要从 `CA` 获取证书。此外，如果你在美国境外，获取 128 位密钥将很困难。SSL 的密钥位于德国 Chaos Club。

要点：SSL 不被广泛使用的主要原因是它对服务器造成了巨大的性能损耗。特别是，最大的损耗来自于持有公钥。硬件加速使得公钥加密和对称加密变得日益流行：SSI 最初由 Netscape（传输层安全）开发，并在 IETF 标准名称。

## 历史

1996 年，Netscape 的实现被发现存在缺陷（即可以破解），由于随机生成器的问题。使用秒和毫秒作为 `PID`（进程 ID）和 `PPID`（父进程 ID）生成种子。由于这些很容易猜测，生成的随机会话密钥复杂度仅为 20 位，可以被暴力破解。后续序列不相关，这意味着 `PRNG` 只需要发现一次。

要点：协商的加密算法（也称为“密码算法”）。SSL 的某些加密算法包括：40 位密钥的 `RC2`、40 位密钥的 `RC4`、128 位密钥的 `RC4`、128 位密钥的 `IDEA`、40 位密钥的 `DES` 以及 112/168 位密钥的三重 `DES`。交换密钥验证服务器和客户端（之前已交换）。来自 Hacking-lesson `http://www.tdlp.org/LDP/Linux–Dictionary/html/index.html`

## SSL

安全套字（Netscape, RSA, WWW, 加密）来自 VERA `http://www.tdlp.org/LDP/Linux-Dictionary/index.html`

### SSL（Server Socket Layer）

由 Netscape Communications 设计，用于在互联网上建立加密、认证的通信。来自 Matise `http://www.tdlp.org/LDP/Linux-Dictionary/index.html`

### SSL（Server Socket Layer）

Netscape Communications 提出的一种安全标准，并集成到其 Netscape Navigator 浏览器和 Netscape Commerce Server 软件中。与其主要的竞争对手安全超文本传输协议（`HTTPS`）不同，SSL 适用于所有互联网工具，而不只是万维网（`WWW`）。使用 SSL 公钥加密的应用程序可以确保无论通过互联网传输什么信息，都没有人能

## Linux 字典

拦截该信息。Netscape Communications 已将 SSL 规范作为一种标准发布给互联网社区。Terisma 目前正在开发一种混合的 SSL/安全 HTTP 规范，确保任何浏览器都能访问任何安全的网站。参见公钥加密。未经授权的用户无法对保护的数据进行检查或复制。主机系统通过将计算机和质存储介质锁定，并仅允许通过配备显示器但无驱动器的远程终端进行访问来确保安全。一些专家认为，出于相同的原因，应该使用特定的本地局域网（`LAN`），因为主机计算机系统的去中心化是开发个人电脑的原因之一。对安全的关注会阻止经理向下属分配计算能力和计算自主权。足够先进的数据加密和密码保护方案甚至可以令最熟练、最坚定的黑客失效。来自 QUED

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

用于替换 `ssleep` 为 `openssl` 的便捷包已被你使用 `openssl` 时安装的此包所取代。在升级后，你可以使用 `dpkg --remove ssleep` 移除此包。来自 Debian 3.0r APT

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSL/TLS

安全套接层 / 传输层安全 (`RSA`, 加密, `TLS`), "`SSL/TLS`" 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### sslwrap

使用 `TLS/SSL` 的简单 `TCP` 加密。`sslwrap` 是一个运行在任何使用 `POP3`、`IMAP`、`SMTP` 的简单 `TCP` 服务上的简单服务，并使用 `TLS/SSL` 加密连接上的所有数据。它使用 `ssl` 支持 `SSL` 版本 2 和 3。它可以在 `inet` 中运行。它可以为位于另一台计算机上的服务加密数据。它可以与你已有的服务器配合，不需要对你的现有服务器进行任何修改。更多信息可以在 `sslwrap` 网站 `http://www.rick.com/sswrap/` 找到。来自 Debian 3.0r0 APT

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSM

设置系统掩码 (`Set System Mask`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSM

简化存储管理 (`Simplified Storage Management`, `HSM`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSM

源特定多组播 (`Source Specific Multicast`, `IETF`, `WG`, `Multicast`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

极其简单的 `MTA`（邮件传输代理），用于将邮件发送到你的邮件枢纽。从邮件枢纽获取邮件的安全、高效且简单的方法。它不包含二进制文件或其他危险物品——没有可以翻找的邮件池，也没有在后台运行的守护进程。邮件简单地转发到配置的邮件。配置极其简单。警告：以上就是它做的一切；它不接收邮件、不扩展别名或管理队列。这些应该由带有系统管理员的邮件枢纽完成。来自 Debian 3.0r0 APT

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSP

业务交换点 (`Service Switching Point`, `IN`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSP

硅胶交换处理器 (`Silicon Switch Processor`, `Cisco`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSP

标准打印端口 (`Standard Printer Port`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSP

结构化支持程序 (`Structured Support Program`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSP

交换机交换协议 (`Switch to Switch Protocol`, `DLSW`, `RFC 1795`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSP

系统栈指针 (`System Stack Pointer`) 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSPI 系统程序

`SSPI System Program`, `OS`, `IBM` 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSR 安全支持提供者接口

`SSR Security Support Provider Interface` 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSSD 固态继电器端口

`SSSD Solid-State Relay Port` 来自 VERA (`FDD`), "`SS/SD`"

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

### SSSNA 单面/单密度 [磁盘]

`SSSNA Single-Sided/Single-Density [disk]`, (`FDD`), "`SS/SD`" 来自 VERA

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`
