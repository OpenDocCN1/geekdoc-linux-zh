
## minclasses 字符类最少数量

`history` 主体（principal）历史中保留的密码数量

使用 `kadmin` 程序创建、删除和修改策略。我们创建了默认策略，最大密码有效期为 180 天，最小长度为 6，且密码必须包含属于至少两个不同字符类的字符：

```bash
kadmin: addpol -maxlife "180 days" -minlength 6 -minclasses 2 default

kadmin: getpol default
```

策略: `default`  
最大密码有效期: `15552000`  
最小密码有效期: `0`  
最小密码长度: `6`  
密码类最少数量: `2`  
保留的旧密钥数量: `1`  
引用计数: `0`

除非另有指定，默认策略将分配给所有创建的主体。如果不存在默认策略，新创建的主体将没有任何策略。

时间规范可能非常详尽，如我们在以下示例所示：

- 3 days
- 下个周日
- 2003年1月1日
- 2003年12月31日 10:00:00 CST
- 两周（fortnight）
- 6个月
- 1年6个月
- 下个周一晚上10点

我们不会列出所有规则，但如果规范中包含空格，请忘记将其包含在双引号中。你可以乐于尝试各种奇特的时间规范。一旦被软件接收，时间就会转换为秒，因此你输入的内容与你看到的将会有很大不同：

```bash
kadmin: modprinc -expire "next fortnight" /lettuce.weeorg.com

Principal "host/lettuce.weeorg.com@WEEORG.COM" 已修改。

kadmin: getprinc host/lettuce.com

Principal: host/lettuce.weeorg.com@WEEORG.COM

过期日期: CST 2002年12月12 周四 11:44:28

上次密码更改: CST 2002年11月13日 18:31:51

密码过期日期: [无]

最大票据有效期: 0天 10:00:00

最大可更新有效期: 7天 00:00:00

最后修改: CST 2002年11月14日 11:44:28 (admin/admin@WEEORG.COM)

上次成功认证: [从未发生]

上次失败认证: [从未发生]

密码尝试失败: 0

密钥数量: 2

密钥: vno 3, 带 HMAC/sha 的 Triple DES cbc 模式，无盐

密钥: vno 3, 带 RSA-MD5 的 DES cbc 模式，无盐

属性：

策略: [无]
```

如所示，主体可以像密码一样设置过期。此外，还有许多主体属性，其中大多数指定了颁发给主体的票的性质。详情请参阅 Kerberos 参考文档。顺便说，可能不让服务主体以任何方式过期。因此，我们推荐以以下方式创建服务主体：

```bash
kadmin: addprinc -randkey -clearpolicy host/biserver.weorg.com

Principal "host/biserver.weorg.com@WEORG.COM" 已创建。
```

### 3.3.3 Kerberos 数据库管理

我们使用 `kdb5_util` 程序初始化 Kerberos 数据库。该程序实现了几对对称操作，可以处理整个数据库。创建和销毁，以及导出（`dump`）和加载（`load`）。特别是 `dump` 命令将数据库导出到一个文件，该文件可以传输到另一个主机，然后加载到另一个数据库中。注意，`load` 操作会破坏数据库的现有内容。

`create` 命令仅在开始时使用一次用于初始化数据库。如果由于某些原因数据库损坏，我们必须初始化数据库并从备份中加载数据。

最好单独对 Kerberos 数据库进行备份，因为数据非常敏感，有时很难限制对备份介质的访问。Kerberos 数据库通常很小，通常可以放入软磁盘中。至于格式，也许使用来自 `kdb5_util dump` 命令的文件更好，因为它使用了 ASCII 字符集。

### 3.3.4 Kerberos 数据库复制

Kerberos 采用了一种非常简单的复制方法。使用 `kdb5_util` 程序导出数据库，并将生成的文件传输到从服务器并加载到目标数据库中。所有这些操作通常通过 `cron` 任务完成。经验法是每小时运行一次该过程，但这取决于你的需求和数据库大小。`kprop` 客户端和 `kpropd` 服务器管理数据库传输。向运行从服务器 Kerberos 服务器的主机发送 `dump` 文件非常简单：

```bash
# kprop -f dump_file slave_server
```

当然，`kpropd` 守护进程必须在从服务器主机上运行。它通常通过 `inetd` 超级服务器，因此我们在 `/etc/inetd.conf` 中放置这样的一行：

```text
krb5_prop stream tcp now nowat root /usr/sbin/kpropd kprop
```

`kpropd` 守护进程接收数据库，将其存储在文件中，然后运行带有 `load` 命令的 `kdb5_util` 程序来更新活动数据库。

### 3.4 AIX 网络认证服务 (NAS)

AIX 5L 版本 2.5 对 Kerberos 有完全支持。`telnet` 和 `ftp` 服务已 Kerberos 化（Kerized）。

主服务器。我们建议您在从 LDAP 服务器上应用相同的架构更改。这样，我们在下文中创建的 Kerberos 域（realm）就会自动复制到从服务器。您应该验证复制情况是否正常。

#### 创建 Kerberos 域

Kerberos 域是 Kerberos 数据树的顶端。它是一个由 `KrbRealm-V2` 和 `KrbRealmExt` 对象类描述的对象。名为 `realm.ldap` 的模板文件与架构文件位于同一目录下。将此文件复制并重命名（例如改为 `ourrealm.ldap`），然后对其进行编辑以反映您的 Kerberos 配置。我们在示例 3-3 中展示了 LDIF 格式的我们的域的呈现。然后，使用 `ldapadd` 命令将数据放入目录：

```bash
# ldapadd -h host -D rootdn -w secret ourrealm.ldap
```

示例 3-3：LDIF 格式的 Kerberos 域

```ldif
dn: krbrealmName-V2=WEEORG.COM,dc=weeorg,dc=com

objectClass: KrbRealm-V2

objectClass: KrbRealmExt

krealmName-V2: WEEORG.COM

krbprincSubtree: krbrealmName-V2=WEEORG.COM,dc=weeorg,dc=com

krbDeleteType: 4
```

```ldif
dn: cn=principal, krbrealmName-V2=WEEORG.COM,dc=weeorg,dc=com

objectClass: container

cn: principal
```

```ldif
dn: cn=policy, krbrealmName-V2=WEEORG.COM,dc=weeorg,dc=com

objectClass: container

cn: policy
```

如果后缀（suffix）没有数据，该命令可能会失败。如果发生此类情况，请在 LDIF文件的顶部插入以下片段：

```ldif
dn: dc=com

dc: com

objectClass: top

objectClass: domain
```

```ldif
dn: dc=weeorg,dc=com

dc: weeorg

objectClass: domain
```

当然，如果您的后缀具有不同的属性或更多层级，您应该进行相应的修改。

使用 `ldapsearch` 程序验证目录中是否存在域数据：

```bash
# ldapsearch -h r-aix.weeorg.com -b dc=weeorg,dc=com objectclass=krbreal-V2

kbrealName-V2WEEORG.COM,dc=weeorg,dc=com

objectclass=KrbRealm

objectclass=KrbRealExt

objectclass=top

krbrealmme-v2WEEORG.COM

krbprincubtree=krbrealmName-v2WEEORG.COM,dc=weeorg,dc=com
```

`krbDeleteType` 决定了 Kerberos 对象从 LDAP 目录中的移除方式，更准确地说，是移除的程度。该架构以及相应的分布式计算环境（DCE）支持的数据。如果是如此，请在 AIX 5L 版本 2.5 NAS 管理员和用户指南中查找适当的设置（该文件位于 `/usr/ll/krb5/doc/pdf/en_US/ADMINDG.PDF`），以确保两个包之间不发生冲突。否则，如果 NAS 是 LDAP 中数据的唯一使用者，您应该将其设置为 `4`，否则可能会因为残留旧的主体容器而导致复杂问题。

LDAP 服务器现在已就绪。如您所见，有两个 `container` 类的对象将“持有”所有 Kerberos 数据。

#### 用户主体（User principals）

之前描述的 Kerberos 树足以存储所有主体。然而，如果 LDAP 中已经定义了用户（正如我们在第 15 页第 2 章“集中化用户管理”中所述），那么将主体数据与其他用户信息一起存储可能会很有益。LDAP 条目作为用户条目的父级是 Kerberos 主体子树。`krbPrincipalSubtree` 属性可能包含多个值，因此我们只需添加另一个包含父级 DN（目录名称）的值即可。继续第 15 页第 2 章“集中化用户管理”中的示例，我们定义了以下 LDIF 文件来实现：

```ldif
dn: krbrealmme-v2WEEORG.COM,dc=weeorg,dc=com

changetype: modify

add: krbPrincipalSubtree

krbprincubtree=ou-people,dc=weeorg,dc=com
```

下一步是将以下内容添加到配置中：

```ini
replica_type = readwrite

preference = 4

ldap-1.weeeorg.com = (

bind_dn = cn=krbadm

bind_pw = secret

ssl_port = 636

keyring = /etc/ldap/key.kdb

replica_type = readonly

preference = 5

)
```

此时，您可以使用 `kadmin` 程序来添加主体（principals）或定义并应用策略。

> 注意：在任何情况下，域内数据发生更改，必须重启 KDC 和管理服务器才能更改生效。

不应使用 `config.krb5` 脚本来配置从用 KDC 服务器。然而，由于不需要使用 Kerberos 工具传播数据库，设置从用服务器非常简单。您应该从主服务器复制 `/etc/krb5/krb5.conf` 和 `/var/krb5/krb5kdc/kdc_ldap_data`，并可选地对其编辑以满足从用 KDC 服务器的需求。

## 3.5 Linux Kerberos 支持

与 AIX 不同，Linux 拥有“原生”的 MIT Kerberos 版本。`Heimdal` 是另一个开源且免费的 Kerberos 软件包，但我们讨论的是 MIT 版本。`Heimdal` 不由 Red Hat 提供，但在 Debian Linux 等其他发行版包含。当然，它可以在任何运行中的 Linux 上进行编译。

### 3.5.1 Red Hat Linux Kerberos 软件包

在 Red Hat Linux 版本 8.0 主机上，您应该安装以下 RPM 包：

- `krb5-libs-1.2.5-6`
- `krb5-workstation-1.2.5-6`
- `krb5-server-1.2.5-6`
- `pam_krbs-1.56-1`
- `cyrus-sas1-gssapi-2.1.7-2`

注意版本号在未来可能会发生。安装非常简单；获取包后，只需使用 `rpm` 程序即可：

```bash
# rpm -i cyrus-gssapi-2.1.7-2.1386.rpm krb5-libs-1.2.5-6.1386.rpm \ 
krb5-server-1.2.5-6.1386.rpm krb5-workstation-1.2.5-6.1386.rpm \ 
pam_krb5-1.56-1.1386.rpm
```

### 3.5.2 在 Linux 上配置 Kerberos

除 Red Hat Linux 外，Linux 发行版通常不包含任何类型的 Kerberos 配置。作为标准的 Kerberos 实现，您在设置 Kerberos 环境时不应遇到任何问题。遵循我们在第 54 页 3.2 节“Kerberos 配置”中提供的说明即可。

## 3.6 发现 Kerberos 服务

通常，Kerberos 客户端依赖 `krb5.conf` 文件来发现 Kerberos 配置。最近引入了两种机制，Kerberos 客户端可以使用它们自动找到 KDC 服务器代码的位置。一种实现在 MIT 的原始 Kerberos 源码发行中，利用新的 DNS `SRV` 记录。另一种是 AIS NAS 和 LDAP 部分。

除了客户端自动查找服务位置的方便外，这种 Kerberos 客户端设置作为与实际环境解耦的方法也非常。例如，如果我们添加另一个从用 Kerberos 服务器，只需要更改一处的配置（主 DNS 服务器或主 LDAP 服务器），所有客户端将自动学习它。

### 3.6.1 使用 AIS NAS 和 LDAP 发现 Kerberos 服务

如果配置了 LDAP 插件，NAS Kerberos 客户端可以使用 LDAP 发现 KDC 和管理服务器。注意，如果 NAS 配置为使用本地文件系统上的标准（旧）数据库，则可以使用 LDAP 用于服务。`ksetup` 管理程序用于配置 LDAP 服务器环境中的 NAS 条目：

```bash
ksetup -h localhost -n=root -p secret

ksetup adddc r-kerberos.weeeorg.com

ksetup adddc kerberos-1.weeeorg.com

ksetup addaddin kerberos.weeeorg.com

ksetup addpwd kerberos.weeeorg.com

ksetup listdkc

kerberos.weorg.com:88

kerberos-1.weorg.com:88

ksetup exit
```

以 `add` 开头的命令（如 `adddkc` 或 `addhost`）安装托管相应服务的计算机名称：`kdc` 用于 Kerberos 分发中心 (KDC)，`admin` 用于管理服务器 (`kadmind`)，`pwd` 用于密码更改服务（也由 `kadmind` 提供）。正如您可能猜到的，也可以可用以 `list` 和 `del` 开头的命令，如 `listdkc`、`listhost`、`delkdc` 和 `delost`。程序的完整描述位于《AIX 5.2 NAS 管理员和用户指南》中，该指南可以在 `/usr/lib/krb5/doc/pdf/en_US/ADMINSD/ADMINDG.PDF` 文件中找到。

当然，程序应该知道如何访问 LDAP 服务器。`config.krb5` 脚本可能如下配置客户端主机：

```bash
# config.krb5 -C WEORG.COM -d weorg.com -l ldap.weorg.com

Initializing configuration...

Creating /etc/krb5.conf...

The command completed successfully.
```

脚本将从头创建 `krb5.conf` 文件并包含特别感兴趣的行：

```ini
[libdefaults]

use_ldap_lookup = 1

ldap_server = ldap.weorg.com
```
