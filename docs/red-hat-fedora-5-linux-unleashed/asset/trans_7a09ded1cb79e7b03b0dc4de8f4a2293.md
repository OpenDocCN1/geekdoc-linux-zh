

http://www.itbilio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Chroot-BIND-HOWTO.html——关于 chroot 如何与 BIND 9 协同工作指南。

http://langfeld.net/DNS-HOWTO/——适用于 BIND 4、8 和 9 版本的 DNS HOWTO 主页。

http://www.itbilio.org/pub/Linux/docs/HOWTO/other-formats/html_single/DNS-HOWTO.html#§4——设置解析和缓存名称服务器。注意，在 Fedora 中，被引用为 /var/named/root.hints 的文件被称为 /var/named/named.ca。

http://spf.pobox.com——发送者策略框架（Sender Policy Framework）的主页，这是一种防止电子邮件地址伪造的方法。

## 第 28 章 LDAP

### 本章内容

- 配置服务器
- 配置客户端
- 管理
- 参考

轻量级目录访问协议（LDAP，发音为 *ell-dap*）是那些虽然隐蔽，但构成企业计算核心基础设施一部分的技术之一。它的功能很简单：存储用户信息。然而，它的强大之处在于它可以与数十种其他服务链接。LDAP 可以为登录认证、公钥分发、邮件路由和地址验证提供支持，最近更是成为了推动单点登录技术发展的核心。

**提示**

大多数人认为，将 LDAP 视为一种高度专业化的数据库服务器时，更容易理解其概念。在幕后，Fedora 使用数据库来存储其所有 LDAP 信息；然而，LDAP 并未提供像 SQL 那样简单的数据操作工具！

OpenLDAP 使用 Sleepycat 软件公司的 Berkeley DB（BDB），强烈建议保留该默认设置。话虽如此，如果你有特定需求，也存在替代方案。

本章讨论 LDAP 服务器的相对基础安装，包括如何托管包含员工姓名和电子邮件地址的公司级目录服务。LDAP 是一种客户端/服务器系统，意味着 LDAP 服务器托管数据，而 LDAP 客户端对其进行查询。Fedora 附带 OpenLDAP 作为其 LDAP 服务器，以及几个启用 LDAP 的电子邮件客户端，包括 Evolution 和 Mozilla Thunderbird。我们将在本章中涵盖这三个应用程序。

由于 LDAP 数据通常可以通过互联网——或者至少你的局域网——访问，因此务必尽一切努力保护你的服务器安全。本章提供了有关 OpenLDAP 密码配置的具体说明；我们建议你严格遵循我们的指示。

### 配置服务器

如果你使用 LDAP 已经好几年了，你就知道它的巨大力量和灵活性。另一方面，如果你是第一次尝试 LDAP，它会像你能想象到的最糟糕的组件一样。LDAP 有非常具体的配置要求，图形化工具严重缺乏，并且有许多缩写词需要记忆。从好的一面看，你付出的所有努力都将物有所值，因为当它工作时，LDAP 会极大地改善你的网络体验。

配置 LDAP 服务器的第一步是安装客户端和服务器应用程序。选择 添加/删除软件；浏览到 服务器 类别并选择 网络服务器；然后点击 可选软件包 按钮。然后点击 系统工具 旁边的 详细信息 按钮，并选择 openldap-clients。安装它们之后，关闭对话框并打开一个终端。

现在，切换到 root 用户，并编辑文本编辑器 /etc/openldap/slapd.conf。这是 OpenLDAP 服务器守护进程 slapd 的主要配置文件。向下滚动直到你看到 database、suffix 和 rootdn 行。

这是 LDAP 系统最基本的配置。你的服务器名称是什么？dc 代表域组件（domain component），即存储在 DNS 中的域名——例如 example.com。在我们的示例中，我们使用 hudzilla.org。LDAP 将域名的每个部分（由点分隔）视为一个域组件，因此域名 hudzilla.org 由域组件 hudzilla 和域组件 org 组成。

将 suffix 行更改为匹配你的域组件，用逗号分隔。例如：

```
suffix "dc=hudzilla,dc=org"
```

下一行定义根 DN，这是另一个 LDAP 缩写词，意为可区分名称（distinguished name）。DN 是目录中一个人的完整描述符：她的名字以及她所在的域。例如：

```
rootdn "cn=root,dc=hudzilla,dc=org"
```

CN 是另一个 LDAP 缩写词，这次意为通用名称（common name）。通用名称就是通常称呼一个人的名字。有些人有多个通用名称。Andrew Hudson 是一个通用名称，但同一个用户也可能有 Andy Hudson 这个通用名称。在我们的 rootdn 行中，我们定义了一个完整的用户：在 hudzilla.org 域中，通用名称为 root。这些行基本上是反向读取的。LDAP 首先访问 org，在 org 中搜索 hudzilla，然后在 hudzilla 中搜索 root。

**rootdn** 很重要，因为它不仅仅是目录中的另一个人。LDAP 根用户就像 Linux 中的 root 用户一样。它是拥有系统完全控制权并可以进行任何想要修改的人。

现在是一个稍微复杂的部分：我们需要为 LDAP 根用户设置密码。最简单的方法是开一个与你现有终端并排的新终端窗口。在新的终端中也切换到 root，并输入 **slappasswd**。这个工具使用 SHA1 哈希算法为 OpenLDAP 生成密码哈希。当它提示时，输入一个密码。当你输入并确认密码后，你应该看到类似的输出：

```
{SSHA}qmVxFt2K1UumrA896d7z6EKG3RLDio2W
```

这是从你的密码生成的密码哈希。你得到的结果将与此处显示的有所不同，但重要的是，它以 `{SSHA}` 开头，表示它使用 SHA1。现在你需要切换回另一个终端（正在编辑 **slapd.conf** 的那个），并在 **rootdn** 行下方添加这一行：

```
rootpw <your password hash>
```

你应该用 **slappasswd** 的完整输出替换 <your password hash>，如下所示：

```
rootpw {SSHA}qmVxFt2K1UumrA896d7z6EKG3RLDio2W
```

这将 LDAP 根密码设置为你刚刚使用 **slappasswd** 生成的密码。这是你在 **slapd.conf** 文件中需要做的最后一个更改，因此保存你的更改并关闭编辑器。

回到终端，运行 **slaptest** 命令。这会检查你的 **slapd.conf** 文件是否有错误，并确保你正确编辑了它。假设没有错误，运行这两个命令：

```
chkconfig ldap on
service ldap start
```

这些命令告诉 Fedora 每次启动时都启动 OpenLDAP，并且现在立即启动它。

最后一个配置步骤是告诉 Fedora 在未指定 **任何** DN 时应该使用哪个 DN。这是通过前往 系统设置 并选择 认证 完成的。在出现的对话框中，在 用户信息 选项卡和 认证 选项卡中勾选 **启用 LDAP 支持**。接下来，点击 **配置 LDAP** 按钮，为你的 DCs（例如 `dc=Hudzilla,dc=org`）输入 LDAP 搜索基础 DN，并为 LDAP 服务器输入 **127.0.0.1**。点击确定，然后再次点击确定。

**提示**

勾选 启用 LDAP 支持 实际上并不会改变用户登录的方式。在幕后，这强制 Fedora 在 `/etc/openldap` 中设置 `ldap.conf` 文件，以便未指定基本搜索起点的 LDAP 搜索会指向你的 DC。

### 填充你的目录

安装、配置并运行 LDAP 后，你现在可以向目录中填充人员。这涉及到更多的 LDAP 缩写词，而且绝不是一个简单的任务，所以如果你需要重读几次才能理解，请不要担心。

首先，创建文件 base.ldif。你使用此文件来定义系统的基本组件：域和地址簿。LDIF 是 LDAP 数据 interchange 格式（LDAP Data Interchange Format）的缩写词，它是记录用户数据以插入 LDAP 目录的标准方式。以下是我们在示例中使用的内容：

```
dn: dc=hudzilla, dc=org
objectClass: top
objectClass: dcObject
objectClass: organization
dc: hudzilla
o: Hudzilla Dot Org

---

dn: ou=People,dc=hudzilla,dc=org
ou: People
objectClass: top
objectClass: organizationalUnit
```

此文件包含两个独立的实体，由空行分隔。第一个是我们的组织 `hudzilla.org`。你已经知道的 `dn` 行；它们在目录范围内唯一地定义每个对象。`objectClass` 指令指定了该实体允许哪些属性以及需要哪些属性。在这种情况下，我们用它将 `dc` 设置为 `hudzilla`，并将 `o`（组织名称）设置为 Hudzilla Dot Org。

下一个实体定义地址簿 `People`，我们将存储所有人员信息。它被定义为一个组织单位，这就是 `ou` 所代表的。*组织单位* 实际上只是你公司的任意分区。例如，你可以为市场营销、会计和管理部门设置 OU。

你需要根据自己的需求自定义文件。具体来说，将 `DC`s 更改为你在 `slapd.conf` 中指定的那些。

接下来，创建并编辑一个新文件，名为 `people.ldif`。这是你将要使用 LDIF 定义地址簿条目的地方。以下是我们在示例中使用的这些人：

