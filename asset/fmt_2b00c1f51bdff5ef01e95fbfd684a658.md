
Wi-Fi 热点或 VPN 依赖于“DNS 谎言”：强制门户（Captive portals）往往会劫持 `DNS` 以将用户重定向到一个页面，要求用户为 Wi-Fi 服务进行身份验证（或支付）。连接到 VPN 的用户通常需要使用“仅限内部”的 `DNS` 服务器来定位企业网络外部不存在的资源。这需要软件进行额外处理。例如，`dnssc-trigger` 可用于检测热点是否正在劫持 `DNS` 查询，而 `unbound` 可以充当代理名称服务器来处理 DNSSEC 查询。

### 选择支持 DNSSEC 的递归解析器

要部署支持 DNSSEC 的递归解析器，可以使用 `BIND` 或 `unbound`。两者默认都启用 DNSSEC，并配置了 DNSSEC 根密钥。要在服务器上启用 DNSSEC，两者均可工作，但在移动设备（如笔记本电脑）上推荐使用 `unbound`，因为它允许本地用户在使用 `dnssc-trigger` 处理热点时动态重新配置所需的 DNSSEC 覆盖，以及在使用 Libreswan 处理 VPN 时进行配置。`unbound` 守护进程还支持部署列在 `etc/unbound/*/` 目录中的 DNSSEC 例外，这对服务器和移动设备都有用。

### 4.5.3. 理解 Dnssc-trigger

一旦安装并配置了 `/etc/resolv.conf` 中的 `unbound`，所有来自应用程序的 `DNS` 查询都由 `unbound` 处理。`dnssc-trigger` 仅在触发时重新配置 `unbound` 解析器。这主要适用于漫游客户端机器，如连接到不同 Wi-Fi 网络的笔记本电脑。流程如下：

- NetworkManager 在通过 `DHCP` 获取新的 `DNS` 服务器时“触发”`dnssc-trigger`。
- `Dnssc-trigger` 然后对该服务器执行多项测试，并决定其是否正确支持 DNSSEC。
- 如果支持，则 `dnssc-trigger` 重新配置 `unbound`，以将该 `DNS` 服务器用作所有查询的转发器。
- 如果测试失败，`dnssc-trigger` 将忽略新的 `DNS` 服务器并尝试几种可用的回退方法。
- 如果确定无限制的端口 53（`UDP` 和 `TCP`）可用，它将告诉 `unbound` 不使用任何转发器而成为完整的递归 `DNS` 服务器。
- 如果这不可行，例如因为端口 53 被防火墙阻止以访问网络本身的 `DNS` 服务器以外的所有内容，它将尝试使用端口 80 的 `DNS` 或端口 443 的 TLS 封装 `DNS`。运行在端口 80 和 443 上的 `DNS` 服务器可以在 `/etc/dnssc-trigger/dnssc-trigger.conf` 中配置。默认配置文件中应有注释掉的示例。
- 如果这些回退方法也失败，`dnssc-trigger` 提供以不安全方式操作的选择，这将完全绕过 DNSSEC，或以“仅缓存”模式运行，该模式不尝试新的 `DNS` 查询，但会回答缓存中已有的一切。

Wi-Fi 热点越来越多地允许访问互联网之前将用户重定向到登录页面。在上述探测序列中，如果检测到重定向，系统将提示用户询问是否需要登录才能获取互联网访问。`dnssc-trigger` 守护进程每十秒探测一次 DNSSEC 解析器。有关使用 `dnssc-trigger` 图形工具的信息，请参阅第 4.5.8 节，“使用 Dnssc-trigger”。

### 4.5.4. VPN 提供的域名和名称服务器

某些类型的 VPN 连接可以在 VPN 隧道设置过程中传递域名以及该域名要使用的名称服务器列表。在 `Red Hat Enterprise Linux` 上，*NetworkManager* 支持此功能。这意味着 `unbound`、`dnssec-trigger` 和 `NetworkManager` 的组合可以正确支持由 VPN 软件提供的域名和名称服务器。一旦 VPN 隧道建立，`unbound` 本地缓存中与该接收到的域名相关的所有条目都会被清除，以便从通过 VPN 访问的内部名称服务器重新获取该域名内名称的查询结果。当 VPN 隧道断开时，`unbound` 缓存再次被清除，以确保对该域名的查询返回公共 IP 地址，而不是之前获取的私有 IP 地址。请参阅第 4.5.11 节，“配置连接提供域名的 DNSSEC 验证”。

### 4.5.5. 推荐的命名实践

Red Hat 建议静态名称和临时名称都应与机器在 DNS 中使用的*完全限定域名*（FQDN）匹配，例如 `host.example.com`。

互联网名称与数字地址分配机构（ICANN）有时会将之前未注册的顶级域（如 `.yourcompany`）添加到公共注册表中。因此，Red Hat 强烈建议不要使用未授权给您的域名，即使在私有网络上也是如此，因为这可能导致域名解析结果因网络配置不同而存在差异。其结果是，网络资源可能变得不可用。使用未授权给您的域名还会使 DNSSEC 的部署和维护变得更加困难，因为域名冲突需要手动配置才能启用 DNSSEC 验证。有关此问题的更多信息，请参阅*关于域名冲突的 ICANN 常见问题解答*。

### 4.5.6. 理解信任锚

在分层加密系统中，*信任锚* 是一个被假定为可信的权威实体。例如，在 X.509 架构中，根证书是一个信任锚，信任链由此导出。信任锚必须事先由信任方持有，以便进行路径验证。

在 DNSSEC 的上下文中，信任锚由与某个 `DNS` 名称关联的公钥（或该公钥的哈希值）组成。它表示为 Base 64 编码的密钥。它类似于证书，是一种交换信息（包括公钥）的手段，可用于验证和认证 `DNS` 记录。*RFC 4033* 将信任锚定义为已配置的 DSKEY RR 或 DSKEY RR 的 DS RR 哈希值。验证型安全感知解析器使用此公钥或哈希值作为构建指向签名 DNS 响应的认证链的起点。一般来说，验证型解析器必须通过 DNS 协议之外的某种安全或可信方式获得其信任锚的初始值。信任锚的存在还意味着解析器应期望该信任锚所指向的区域已被签名。

### 4.5.7. 安装 DNSSEC

#### 4.5.7.1. 安装 unbound

为了在本地机器上使用 DNSSEC 验证 `DNS`，必须安装 `DNS 解析器 unbound`（或 `bind`）。在移动设备上，只需安装 `dnssec-trigger`。对于服务器，`unbound` 通常就足够了，但根据服务器所在位置（局域网或互联网），可能需要配置本地域名的转发设置。`dnssec-trigger` 目前仅有助于全局公共 `DNS` 区域。`NetworkManager`、`dhclient` 和 VPN 应用程序通常可以自动收集域名列表（以及名称服务器列表），但 `dnssec-trigger` 和 `unbound` 不行。

要安装 `unbound`，请以 `root` 用户身份输入以下命令：

```bash
# yum install unbound
```

#### 4.5.7.2. 检查 unbound 是否正在运行

要确定 `unbound` 守护进程是否正在运行，请输入以下命令：

```bash
$ systemctl status unbound
```

输出：

```
unbound.service - Unbound recursive Domain Name Server
   Loaded: loaded (/usr/lib/systemd/system/unbound.service; disabled)
   Active: active (running) since Wed 2013-03-13 01:19:30 CET; 6h ago
```

如果 unbound 服务未运行，`systemctl status` 命令将报告 unbound 为 `Active: inactive (dead)`。

#### 4.5.7.3. 启动 unbound

要为当前会话启动 unbound 守护进程，请以 `root` 用户身份输入以下命令：

```bash
# systemctl start unbound
```

运行 `systemctl enable` 命令，以确保 unbound 在每次系统启动时都启动：

```bash
# systemctl enable unbound
```

unbound 守护进程允许使用以下目录配置本地数据或覆盖设置：

- `/etc/unbound/conf.d` 目录用于为特定域名添加配置。这用于将域名的查询重定向到特定的 DNS 服务器。这通常用于仅存在于企业广域网内的子域名。
