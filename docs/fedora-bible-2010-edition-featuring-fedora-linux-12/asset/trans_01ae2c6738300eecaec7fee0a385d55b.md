
**注意：** 389 目录服务器（最初名为 Fedora 目录服务器）于 2005 年 6 月发布，作为本章节中描述的 OpenLDAP 软件的开源 LDAP 服务器替代方案。389 目录服务器现在是 Fedora 存储库的一部分（389-ds-base 和 389-ds-base-devel 软件包）。要了解有关 389 DS 的更多信息，请参阅 `http://directory.fedoraproject.org`。

## 理解 LDAP

LDAP 允许人们创建信息目录，这些目录可以通过网络在客户端应用程序之间共享。它特别适用于那些需要反复查询相对稳定的信息的应用程序（换句话说，即被查看的次数多于被修改次数的信息）。这就是为什么 LDAP 在存储人员、地址和其他可能需要高访问频率但更改较少的数据方面很受欢迎的原因。

由于 LDAP 具有极其灵活的设计，作为 LDAP 开发人员或管理员，您对以下方面拥有很大的控制权：

- 目录中信息的组织方式。
- 信息的访问方式以及访问者是谁。
- 信息分发的规模，从本地到全球。（信息可以以任何您选择的规模复制到其他服务器并自动同步。）

然而，尽管 LDAP 具有灵活性，但您不必从头开始设计每个创建的目录。LDAP 有许多预定义的信息结构，您可以依赖这些结构来构建您的 LDAP 目录。这些数据结构定义在几个不同的标准文档中，称为 RFC（Request for Comments，征求意见），您可以从 IETF 站点列出（`http://www.ietf.org/rfc.html`）。几乎互联网协议和相关应用服务的每个方面都有 RFC。与 LDAP 定义相关的重要 RFC 包括：

- **RFC 2252** — 定义了 LDAP 的框架。
- **RFC 2256** — 定义了 LDAPv3 的 X.500 用户模式。
- **RFCs 1274, 2079, 2247, 2307, 2587, 2589** — 定义了将用户属性、统一资源标识符 (URI)、域名、NIS 数据、公钥基础设施 (PKI) 和动态目录服务包含在 LDAP 目录中的规范。

这些 RFC 基于的文档包括 CCITT X.500 标准和相关的 ISO IS9594 目录服务标准。特别是，X.521 和 X.520 定义了一些最基本的对象类和属性类型。

但是，请记住，这些标准仅提供指导原则。当您构建自己的 LDAP 目录时，您的 OpenLDAP 服务器必须直接处理在 OpenLDAP 服务器上实现这些标准的模式。

**提示：** 微软的 Active Directory (AD) 通常被称为“基于 LDAP”的实体，这让一些用户对整合 OpenLDAP 和 AD 抱有较高的期望。虽然可以在 AD 和 OpenLDAP 之间交换信息，但这需要大量的耐心和技巧。除非您必须与 AD 互操作，否则支持 Windows 客户端的更好路径是通过使用 OpenLDAP 和 Samba。

## 在模式中定义信息

组成 LDAP 目录的元素被组织成所谓的*模式*。当您创建或使用 LDAP 目录时，您将要处理的模式中的信息类型包括以下类型的项：

- **对象类** — 对象提供用于将一组属性归类的名称。因此，在通讯录中，您可以包括 inetOrgPerson 对象类，并在其下存储与人员相关的属性。
- **属性** — 顾名思义，属性保存与对象类相关的部分信息。例如，inetOrgPerson 对象类可以具有电话号码、电子邮件地址等属性。

**注意：** 如果您熟悉数据库，LDAP 目录术语可能会显得有些不同。LDAP 更像是一个目录结构提供者，而不是真正的数据库。您可以将属性视为字段，将对象类视为表。

对象类的例子包括*国家*、*地区*和*组织*。对于每个对象类，可能都需要属性以及可选属性列表。您可以在任何 LDAP 服务器附带的模式文件中看到许多标准对象类和属性的定义。

在 OpenLDAP 中，`/etc/openldap/schema` 目录中包含了几个默认模式。本章展示如何创建的电子邮件地址书示例完全依赖于 OpenLDAP 提供的模式。为了完成本章的示例，您无需自己创建任何模式文件。如果您需要比默认提供的更多对象和属性，您可以从其他地方获取模式或创建自己的模式。

**交叉引用：** 有关 OpenLDAP 包含的模式的信息，请参阅 OpenLDAP 模式规范页面（<http://www.openldap.org/doc/admin24/schema.html>）。该页面还描述了解决如何扩展这些模式的方法。在创建您自己的对象类或属性之前，请检查这些模式以及前面描述的 RFC 中的模式定义。

当您开始处理 LDAP 目录时，您将按名称访问对象类和属性。然而，对于 LDAP 服务器来说，这些项目中的每一个都由唯一的数字和点字符串表示。每个字符串被称为对象标识符 (OID)。如果您没有创建自己的对象类或属性，则不需要处理 OID。

要了解 OID 是什么以及何时可能想要获取自己的 OID 分配，请参考侧边栏“理解 OID”。

## 构建您的 LDAP 目录

虽然使用标准文档来保持 LDAP 目录中的对象类、属性和其他元素的唯一性，但您可以自由地按您想要的方式将这些元素组合成您自己的 LDAP 目录。用于创建 LDAP 数据库的结构是 LDAP 数据互换格式 (LDIF)。

您存储在 LDAP 目录中的每个信息片段都必须属于一个基础可区分名称（或基础 dn）。由于如今许多组织可以由唯一的互联网域名表示，因此域名是识别 LDAP 基础 dn 的流行方式。事实上，在本章的示例中，我使用的基础可区分名称是 linuxtoys.net。如果您正在为可以用域名表示的组织创建 LDAP 目录，您可以将 linuxtoys.net 替换为您的域名。

如果您正在为较大的组织创建 LDAP 目录结构（换句话说，不仅仅是我这里做的单个通讯录），请仔细考虑您希望如何组织目录。对于跨国公司的基础可区分名称下，您可能希望添加国家代码（us, de, it 等）。

## 设置 OpenLDAP 服务器

设置 OpenLDAP 服务器所需的所有软件包都包含在 Fedora 中。作为替代方案，您可以轻松地使用 yum 通过互联网安装这些软件包。安装这些软件包后，您可以开始配置 OpenLDAP 服务器。

### 安装 OpenLDAP 软件包

要配置 OpenLDAP 服务器，请首先从 Fedora 安装所有 openldap 软件包。首先，检查安装了哪些 openldap 软件包：

```bash
# rpm -qa "openldap*"
```

只有在开发 LDAP 应用程序时才需要 openldap-devel 软件包。否则，您可以从随本书提供的 DVD 或通过网络输入以下命令安装 openldap、openldap-clients 和 openldap-servers 软件包：

```bash
# yum install openldap openldap-clients openldap-servers
```

### 配置 OpenLDAP 服务器 (slapd.conf)

您在配置文件 `/etc/openldap/slapd.conf` 中配置 OpenLDAP 数据库的访问和使用。作为替代方案，您也可以将您的 slapd.conf 添加到 `/etc/openldap/slapd.d` 目录中的信息数据库。此过程使用旧版的 `slapd.conf` 方法。

> 注意：有关在 `slapd.conf` 文件中可以使用的功能的更完整描述，请参阅 slapd.conf 手册页。

1. **删除 slapd.d 目录。** 如果您愿意，可以将 `slapd.conf` 文件转换为存储在 `/etc/openldap/slapd.d` 目录中（有关将该文件转换为较新格式的信息，请参阅 slaptest 手册页）。要使用旧式的 `slapd.conf` 文件，请删除 `slapd.d` 目录，方法如下：

   ```bash
   # rm -rf /etc/openldap/slapd.d
   ```

2. **编辑 slapd.conf。** 备份 `/etc/openldap/slapd.conf` 文件，然后使用任何文本编辑器以 root 用户身份打开该文件。以下步骤告诉您一些您可能想要更改的信息。

3. **审查模式。** 在 `slapd.conf` 文件中，通常用于创建 LDAP 目录的模式是从 `/etc/openldap/schema` 目录包含的。您可能使用的其他模式通常依赖于包含这些模式。因此，除非您确定不需要它们，否则不要删除这些模式中的任何一个：

   ```text
   include /etc/openldap/schema/corba.schema
   include /etc/openldap/schema/core.schema
   include /etc/openldap/schema/cosine.schema
   include /etc/openldap/schema/duconf.schema
   include /etc/openldap/schema/dyngroup.schema
   include /etc/openldap/schema/inetorgperson.schema
   include /etc/openldap/schema/java.schema
   include /etc/openldap/schema/misc.schema
   include /etc/openldap/schema/nis.schema
   include /etc/openldap/schema/openssl.schema
   include /etc/openldap/schema/policy.schema
   include /etc/openldap/schema/collective.schema
   ```

由于模式是纯文本文件，您可以使用任何文本编辑器打开它们。模式的几个部分对我们感兴趣。`corba.schema` 文件是所有 LDAP 目录必需的。`cosine.schema` 和 `inetorgperson.schema` 文件特别有用（且此过程需要）。`nis.schema` 文件用于在 LDAP 目录中提供网络信息服务 (NIS) 数据。
