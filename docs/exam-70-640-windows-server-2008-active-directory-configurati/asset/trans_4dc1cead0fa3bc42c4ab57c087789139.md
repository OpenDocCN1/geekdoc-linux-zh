

### AD FS 联合服务代理
此服务创建一个指向联合服务的代理，该代理可以部署在边界网络或 DMZ（非军事区）中。

### 支持声明的智能代理
你可以在托管基于声明的应用程序的 Web 服务器上安装此代理，以使其能够查询 AD FS 安全声明。

### Windows 令牌基于智能代理
你可以在托管传统 Windows NT 令牌基于应用程序的 Web 服务器上安装此代理，以允许你将这些令牌从 AD FS 令牌转换为 Windows NT 令牌。

## 技能总结矩阵

在本课中，你学到了：
- 域名系统 (DNS) 为 Active Directory、互联网以及大多数现代 TCP/IP 网络提供默认的命名解析机制。
- 早于 Windows 2000 的 Windows 操作系统使用 NetBIOS 名称来标识网络上的计算机。
- 资源记录是所有 DNS 服务器中基本的数据存储单元。
- Windows Server 2008 中的 DNS 服务器服务既支持标准 DNS 区域，也支持与 Active Directory 集成的 DNS 区域。
- DNS 根名称服务器是整个命名空间中的最高级别 DNS 服务器。
- 你可以将 DNS 命名空间划分为区域，以将其存储在不同的服务器上，并将其管理委托给不同的人。
- Windows Server 2008 支持主要区域、辅助区域和存根区域。主要区域和存根区域可以与 Active Directory 集成。
- 你可以使用 DHCP 来简化将 DNS 服务器分配给你的客户端以用于命名解析的过程。
- Active Directory 权限管理服务 (AD RMS) 是 Windows Server 2008 中的一项服务，可用于保护 Windows 网络上的敏感数据。
- Active Directory 联合服务 (AD FS) 角色允许管理员为跨多个组织的基于 Web 的应用程序配置单点登录 (SSO)。

## 知识评估

### 匹配题

- a. AAAA
- b. 账户组织
- c. CNAME
- d. in-addr.arpa
- e. NetBIOS
- f. 递归查询
- g. 资源记录
- h. 授权起始 (SOA)
- i. 存根区域
- j. Windows 互联网命名服务 (WINS)

1. \_\_\_\_\_\_\_\_\_\_ 此 DNS 记录标识哪个名称服务器是该域内数据的权威信息来源。
2. \_\_\_\_\_\_\_\_\_\_ 此 DNS 记录类型标识一个 IPv6 DNS 主机。
3. \_\_\_\_\_\_\_\_\_\_ 此类型的 DNS 查询由 DNS 客户端解析器发送到 DNS 服务器。
4. \_\_\_\_\_\_\_\_\_\_ 此 DNS 区域仅包含 SOA 和 NS 资源记录，以及标识区域权威服务器的主机资源记录。
5. \_\_\_\_\_\_\_\_\_\_ 这些包含 AD FS 联合关系中的用户账户。
6. \_\_\_\_\_\_\_\_\_\_ 此服务用于提供集中式机制来管理 Windows 网络上的 NetBIOS 命名解析。
7. \_\_\_\_\_\_\_\_\_\_ 此 DNS 区域专门设计用于支持 IPv4 反向命名解析。
8. \_\_\_\_\_\_\_\_\_\_ 这指的是可以存储在 DNS 区域中的所有 DNS 记录类型。
9. \_\_\_\_\_\_\_\_\_\_ 此 DNS 记录类型为给定主机提供别名，使得称为 server1.adatum.com 的主机可以使用 www.adatum.com 在相同的 IP 地址上访问。
10. \_\_\_\_\_\_\_\_\_\_ 这是在引入 Windows 2000 和 Active Directory 之前，Windows 操作系统使用的默认命名解析协议。

### 选择题

*圈出正确的选项。*

1. 哪种 DNS 服务器配置不在本地托管任何区域？
   - a. 仅缓存服务器
   - b. 条件转发器
   - c. 辅助区域
   - d. 条件辅助区域

2. 在 DNS 服务器之间最常用发送的 DNS 查询类型是什么？
   - a. 转发查询
   - b. 条件转发查询
   - c. 迭代查询
   - d. 递归查询

3. 哪个 AD FS 组件允许基于声明的应用程序查询 AD FS 安全声明？
   - a. AD FS 联合服务代理
   - b. 支持声明的智能代理
   - c. Windows 令牌基于智能代理
   - d. NTLM 声明基于智能代理

4. 哪个 MX 记录属性指示相对优先级，以确定如果为特定域配置了多个记录时将使用哪个 MX 记录？
   - a. 权重
   - b. 优先级
   - c. 偏好
   - d. Exchange

5. 哪种 DNS 区域类型是只读的，包含在托管该区域的计算机上的文本文件中？
   - a. 标准辅助区域
   - b. 与 Active Directory 集成的辅助区域
   - c. 标准主要区域
   - d. 与 Active Directory 集成的主要区域

6. 哪种 DNS 记录类型是 Active Directory 允许客户端定位 AD 资源所需的？
   - a. NS 记录
   - b. A 记录
   - c. MX 记录
   - d. SRV 记录

7. 哪个 Active Directory 应用程序分区将 DNS 数据复制到 Active Directory 域内所有已配置为运行 DNS 服务器角色的域控制器？
   - a. DomainDNSZones
   - b. 域 NC
   - c. 配置 NC
   - d. ForestDNSZones

8. 在主名称服务器上配置了什么，以便它可以在主区域中有可用更改时通知其辅助服务器？
   - a. Active Directory 复制列表
   - b. Active Directory 复制伙伴
   - c. 通知列表
   - d. 更改通知列表

9. 哪个程序生成对 DNS 信息的请求并将其发送到 DNS 名称服务器以进行解析？
   - a. 迭代查询
   - b. 递归查询
   - c. 解析器
   - d. 通知列表

10. 哪些 DNS 服务器位于 DNS 命名空间的最高级别？
    - a. 根名称服务器
    - b. .com 名称服务器
    - c. cache.dns 名称服务器
    - d. 转发名称服务器

### 案例场景

#### 场景 12-1：为 Margie 的旅行社提供咨询

你是 Margie Shoop（Margie's Travel 的所有者）的计算机顾问。Margie 拥有一个单一的 Active Directory 域结构，域名为 ad.margiestravel.com。ad.margiestravel.com 的域控制器和 DNS 服务器部署在内部网络上；Margie's Travel 还在其 DMZ（非军事区）部署了若干台 Windows Server 2008 服务器，以为 Margie's Travel 提供互联网存在。Margie 与众多邮轮公司和旅游公司建立了合作伙伴关系，这些公司为 Margie 的客户提供旅行游览服务。为了推广这些公司（其中一些是个人或家族经营的小型企业），Margie 开始利用其公司的 Active Directory 和网络基础设施，使她的合作伙伴能够使用 Margie's Travel 网络维护万维网（WWW）存在。Margie's Travel 已与一家小型公司提供在巴哈马进行海豚观赏之旅的公司达成协议，为其网站提供命名解析。这包括为名为 SERVER1 的服务器提供对外部客户的命名解析。由于大多数客户难以记住在公司域名前输入 SERVER1，海豚观赏旅游公司希望人们能够使用更知名的 WWW 别名来访问该服务器。

根据关于 Margie's Travel 的这些信息，回答以下问题：

1. Margie's Travel 需要提供什么来为其合作伙伴公司提供命名解析？
2. Margie's Travel 需要提供什么才能在访问合作伙伴公司网站时使用名称 WWW 来访问 SERVER1？
3. 托管在问题 1 中创建的主要 DNS 区域的服务器因硬件故障离线了几个小时。如果再次发生这种情况，Margie's Travel 如何为 DMZ 中的标准 DNS 区域提供容错能力？

![](img/a8ee53dbf1310726255b6fbb9f296fb2_308_0.png)

## 配置 Active Directory 证书服务

### 目标域矩阵

| 技术技能 | 目标域 | 目标域编号 |
| :--- | :--- | :--- |
| 安装 Active Directory 证书服务 | 安装 Active Directory 证书服务。 | 6.1 |
| 配置证书吊销 | 管理证书吊销。 | 6.5 |
| 配置证书模板 | 管理证书模板。 | 6.3 |
| 管理证书注册 | 管理注册。 | 6.4 |
| 配置 CA 服务器设置 | 配置 CA 服务器设置。 | 6.2 |

### 关键术语

- Active Directory 证书服务 (AD CS)
- 自动注册
- 自动证书请求
- 证书
- 证书实践声明 (CPS)
- 证书请求向导
- 证书吊销列表 (CRL)
- 证书服务客户端--自动--注册
- 证书模板
- 证书颁发机构 (CA)
- 证书颁发机构 Web 注册
- certutil
- 数字证书
- 数字签名
- 加密文件系统 (EFS)
- 注册智能代理
- 企业 CA
- 企业信任
- 层次结构
- 中间 CA
- 颁发 CA
- 密钥归档
- 密钥恢复智能代理
- 网络设备注册服务 (NDES)
- OCSP 响应签名证书
- 在线证书状态协议 (OCSP)
- 在线响应器
- 最小权限原则
- 私钥
- 公钥
- 公钥加密
- 公钥基础设施 (PKI)
- 公钥策略
- 恢复智能代理
- 响应器阵列
- 受限注册智能代理
- 根 CA
- 自我注册
- 共享密钥
- 已签名
- 简单证书注册协议 (SCEP)
- 智能卡
- 智能卡注册站
- 智能卡读卡器
- 独立 CA
- 从属 CA
- 受信任的根证书颁发机构
- 双因素身份验证
- Web 注册

