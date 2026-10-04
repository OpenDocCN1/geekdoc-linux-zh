

# LDAP

轻量级目录访问协议（LDAP）是一种允许客户端访问目录服务内部信息的协议。LDAP 是在 X.500（一种目录服务标准协议）之后创建的，这是因为重量型 X.500 客户端开销大且随后的响应缓慢，因此被称为“轻量级”。LDAP 客户端能够访问 Active Directory，这使得除了标准方式访问 Windows 2000 的客户端之外的客户端也能访问 Active Directory。

你注意到 Active Directory 的命名方案也遵循 LDAP 原则。微软制作了一个名为 LDAPexe 的优秀工具（包含在 Windows 2000 资源包中），它允许通过 LDAP 接口对 Active Directory 内容进行低级浏览。图 6.3 是在匿名连接到 Active Directory 服务器（witt.home 域的域控制器）时产生的某些信息示例**最有趣的项目已加粗**）。你会发现，Active Directory 提供的信息范围要大得多，并且可以用于攻击前的侦察。

> 注意：轻量级目录访问协议默认运行在 TCP 端口 389。

# 图 6.3 连接到 Active Directory 服务器的 LDAP 连接转储

```
ld = ldap_open("localhost", 389);
Established connection to localhost.
Retrieving base DSA information...
Result <0>: (null)
Matched DNs:
Getting 1 entries:
>> Dn:
1> currentTime: 12/18/2002 19:16:16 GMT Standard Time GMT Daylight Time:
1> subschemaEntry: CN=Aggregate,CN=Schema, CN=Configuration,DC=witt,
DC=home:
1> dsServiceName: CN=NTDS Settings,CN=TEST1,CN=Servers,CN=Default-First-
```

# 图 6.3 连接到 Active Directory 服务器的 LDAP LDAP 连接

Site-Name,CN=Site,CN=Configuration,DC=witt,DC=home;

```
3> namingContexts:CN=Schema,CN=Configuration,DC=witt,DC=home; CN=
Configuration, DC=witt,DC=home; DC=witt,DC=home;
1> defaultNamingContext: DC=witt,DC=home;
1> schemaNamingContext: CN=Schema,CN=Configuration,DC=witt,DC=home;
1> configurationNamingContext: CN=Configuration,DC=witt,DC=home;
1> rootNamingContext: DC=witt,DC=home;
16> supportedControl: 1.2.840.113556.1.4.619; 1.2.840.113556.1.4.801;
1.2.840.113556.1.4.473; 1.2.840.113556.1.4.528; 1.2.840.113556.1.4.417;
1.2.840.113556.1.4.619; 1.2.840.113556.1.4.481; 1.2.840.113556.1.4.529;
1.2.840.113556.1.4.805; 1.2.840.113556.1.4.521; 1.2.840.113556.1.4.970;
1.2.840.113556.1.4.138; 1.2.840.113556.1.4.474; 1.2.840.113556.1.4.139;
1.2.840.113556.1.4.1340; 1.2.840.113556.1.4.141;
2> supportedPolicies: MaxPoolThreads; MaxDatagrams;
MaxReceiveBuffer; InitTimeout; MaxConnections; MaxConnIdleTime;
MaxActiveQueries; MaxPageSize; MaxQueryDuration; MaxTempSize;
MaxResultSize; MaxNotificationPerConn;
1> highestCommitNN: 28;
2> supportedSASLMechanisms: GSSAPI; GSS-NEGO;
1> dnHostName: TEST.witt.home;
1> ldapServiceName: witt.home;
1> serverName: CN=TEST,CN=Servers,DC=Default-First-Name,
CN=Sites,CN=Configuration,DC=witt,DC=home;
1> supportedCapabilities: 1.2.840.113556.1.4.800;
1> isSynchronized: TRUE;
1> isGlobalCatalogReady: TRUE;
```

如你所见，通过简单的连接就可以看到域、DNS 服务器、服务器名称以及 Active Directory 系统的某些技术参数。

# Active Directory 与 DNS 的集成

Active Directory 与 DNS 紧密集成，以至于微软没有将其命名为 Active！Active Directory 的安装和运行需要在网络支持 DNS。对于那些从非传输控制协议/网际协议（TCP/IP）网络迁移的人来说，这是一个重大变化。在使用 Active Directory 时，DNS 服务受到两个影响：

- 为了让客户端登录由 Active Directory 管理的域，需要 DNS 来定位域控制器（DC）。NetLogon 服务需要支持服务记录（SRV RR）的 DNS 服务器，因为 SRV RR 同时在 DNS 命名空间中注册和标识域控制器。
- Active Directory 可以存储 DNS 区域信息并在整个范围内原生复制，而无需区域传输过程。但这要求 Windows 2000 域控制器也是 DNS 服务器。

![](img/729efc56f204a2ebffb295c3a2dfdfb_281_0.png)

# 第 6 章 • 安全 Active Directory

- TTL：生存时间（Time to Live）。此字段可以留空。
- Class：四种类型之一。IN 是常用的，代表互联网。此字段可以留空。
- Preference（优先级）：0 到 65535 之间的数字，表示目标主机是否应被优先联系。数字越小优先级越高。
- Weight（权重）：1 到 65535 之间的数字，用于当两个或多个目标主机具有相同优先级时的负载均衡。当不使用负载均衡时，通常设置为 0。
- Port（端口）：0 到 65535 之间的数字，表示传输协议。已知服务使用 RFC 1700 列出的端口。
- Target（目标）：提供服务的主机 DNS 节点。

这里是一个 SRV RR 的示例，用于从两个不同的服务器中查找服务：

```
ldap.tcp.wit.home SRV 0 0 389 dns1.root.com
SRV 1 0 389 dns2.branch.root.com
```

Active Directory 对应区域的 DNS 服务器必须与 Active Directory 兼容，否则 Active Directory 将无法运行。即使该区域只有一个 DNS 服务器不兼容，也会产生问题。例如，如果 AD.DOMAIN.COM 的备用 DNS 服务器因为不支持 SRV RR 而不兼容，网络上的任何时刻可能查询该不兼容的 DNS 服务器，从而找不到定位 Active Directory 所需的 SRV RR（因为由于不受理解而被自动从备用区域中删除）。如果不兼容的 DNS 服务器是域的主服务器，情况会更糟，因为所有区域更新都会使用不包含 SRV 的数据库更新备用服务器。

工作方法如图所示。在 IP 地址静态分配给服务器和工作站的网络中，用 IP 地址更新 DNS 区域文件是一项简单的额外工作。DNS 最初初是为人工管理设计的。然而，网络已变得日益动态。DHCP（以及引导协议

