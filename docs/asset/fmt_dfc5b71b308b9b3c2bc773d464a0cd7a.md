
## 正向 DNS 区域文件配置

`@ IN SOA nsl.centos7.home.admin.centos7.home.`

; 2015082400 ; Serial yyyymmddn
; 3h ; Refresh After 3 hours
; 1h ; Retry After 1 hour
; 1w ; Expire after 1 week
; 1h) ; Minimum negative caching

### 11. 添加文件的其余内容

```bash
; add your name servers for your domain
   IN NS nsl.centos7.home.

; add your mail server for the domain
   IN MX 10 mailhost.centos7.home.

; now follows the actual domain name to IP
; address mappings:
```

```bash
; first add all referenced hostnames from above
nsl        IN A 192.168.1.7
mailhost  IN A 192.168.1.8

; add all accessible domain to ip mappings here
router    IN A 192.168.1.0
www       IN A 192.168.1.9
ftp       IN A 192.168.1.10

; add the private clients on the Lan here
client1   IN A 192.168.1.11
client2   IN A 192.168.1.12
client3   IN A 192.168.1.13

; finally we define some aliases for
; existing domain name mappings
webserver IN CNAME www
johnny    IN CNAME client2
```

### 12. 创建反向区域文件

完成后，只需保存并关闭文件，然后为域名使用的私有子网创建反向区域文件（C 类是将点分隔的前三个数字（八字节）：`XXX.XXX.XXX`。例如，对于 `192.168.1.0/24` 子网，C 类是 `192.168.1`）。

```bash
vi /var/named/db.<C-Class of your search IP in reverse order>
```

### 13. 示例反向区域文件

在示例中，解析 `centos7.home` 的 `192.168.1` C 反向区域文件将是：

```bash
vi /var/named/db.1.168.192
```

### 14. 填充反向区域内容

首先放入与第 10 步中完全相同的 SOA，然后在文件末尾追加以下内容：

```bash
; add your name servers for your domain
   IN NS nsl.centos7.home.

; here add the actual IP octet to
; subdomain mappings:
```

```bash
7         IN PTR nsl.centos7.home.
8         IN PTR mailhost.centos7.home.
9         IN PTR www.centos7.home.
```

## 域名操作

| | | | |
|---|---|---|---|
| 10 | IN | PTR | `ftp.centos7.home` |
| 11 | IN | PTR | `client1.centos7.home` |
| 12 | IN | PTR | `client2.centos7.home` |
| 13 | IN | PTR | `client3.centos7.home` |

15. 保存文件，并将新的区域对添加到 `named` 配置中。要做到这一点，再次打开 `named.conf`。

16. 保存文件，并将新的区域对添加到 `named` 配置中。要做到这一点，再次打开 `named.conf`。

17. 保存文件，并将新的区域对添加到 `named` 配置中。要做到这一点，再次打开 `named.conf`。

18. 保存文件，并将新的区域对添加到 `named` 配置中。要做到这一点，再次打开 `named.conf`。

## 域名操作

随后，我们开始创建并自定义正向 DNS 区域文件，文件名为 `/var/named/<domain>.<top-level domain>.db`。该文件使用 `$TTL` 控制语句打开，代表**生存时间 (Time to Live)**，它为其他名称服务器提供一个时间值，该值决定了它们缓存此区域记录的持续时间。与许多将秒作为默认时间值的配置不同，你也可以使用 BIND 特定的格式使用其他单位，包括分钟 (`m`)、小时 (`h`)、天 (`d`) 和周 (`w`)。接下来，我们提供了一个**区域起始 (Start of Authority, SOA)** 记录。此记录包含关于整个区域的特定信息。它以区域名称 (`@`) 开始，指定了类 (`IN`)，该名称服务器在 `hostname.domain.TLD` 格式下的完全限定域名 (FQDN)，以及一个管理员的电子邮箱地址。该值通常为 `hostname.domain.TLD` 格式，它是通过将符号 `@` 替换为点 (`.`) 形成的。完成这一步后，只需打开括号签署区域的序列号、刷新值、重试值、过期值和负缓存生存时间值。这些指令总结如下：

- 序列号是一个数值，通常采用反转的日期格式 (`YYYYMMDD`) 并附带一个额外值 (`VV`)，每当区域文件被修改或更新时，该值就会递增，以指示 `named` 名称服务器重新加载该区域。值 `VV` 从 `00` 开始，下次你修改此文件时，将其递增到 `01`、`02` 或 `03`，依此类推。
- 刷新时间 (`time-to-refresh`) 值决定了辅助或从名称服务器检查区域是否发生更改的频率。
- 重试时间 (`time-to-retry`) 值决定了在服务器故障后，辅助名称服务器检查主服务器的频率。如果在由过期时间 (`time-to-expire`) 指定的时间范围内发生故障，辅助名称服务器将停止作为请求的权威响应。
- 最小 TTL (`minimum-TTL`) 值决定了其他名称服务器缓存负响应的时间。

在完成此部分并关闭相应的括号后，我们继续添加权威名称服务器信息 (`NS`)，格式为 `IN NS <FQDN of the nameserver>.domain`。通常情况下，除非你至少有两个名称服务器（将每个名称服务器的 FQDN 放在新的 `NS` 行中），否则也可以只设置一个名称服务器，这在你在办公室或家庭环境中运行服务器并希望享受本地名称解析的好处（例如 `.home.lan.dev`）时特别有用。下一步要求我们包含对**邮件交换器 (Mail Exchanger, MX)** 记录的引用，以便为该区域指定邮件服务器。格式为 `IN MX <priority> <mailserver>`。如果你定义了多个邮件服务器（每个都在单独的 `IN` 行上），优先级变得重要——数字越小，优先级越高。在这方面，辅助邮件服务器应该具有较高的值。

![](img/a6dbf7df749be83c0faae2334e970c0b_632_0.png)

## 第 9 章

在 SOA、NS 和 MX 行中，我们已经引用了未定义为 IP 映射（A 记录）的主机名。之所以这样做是因为区域文件不是按顺序处理的。但不要忘记为每个主机名创建相应的 A 行。

根据你的需求，你可能还打算将你的名称服务器用作邮件服务器（此时你将写 `MX 10 ns1.centos7.home.`），尽管你可能像示例那样有另一个专门用于该角色的服务器。

接下来是创建 A 记录（A 代表地址）并将 IP 地址分配给所示的值。这是任何基于服务器的名称解析请求的核心。A 记录用于将 FQDN 链接到 IP 地址，但你可以定义所有想要映射的本地主机。由于我们已经在区域文件之前使用并引用了一些域名（如 `nameserver` 或 `mailserver`），我们将从这些项开始。之后，你可以为公用客户端和内部客户端使用 IP 映射。当使用 A 记录时，你可以将同一个 IP 地址映射到多个不同的主机名。如果你没有为网络中的每个服务设置专用服务器，而是用一台服务器运行你所有的 DNS、邮件、Web 和 `ftp` 服务，你可以写下以下行：

```
ns1 IN A 192.168.1.7
mailhost IN A 192.168.1.7
www IN A 192.168.1.7
ftp IN A 192.168.1.7
```
