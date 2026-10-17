
如果您使用 LDAP 多年了，您深知其巨大的力量和灵活性。另一方面，如果您是第一次尝试 LDAP，它可能会像您能想象到的最坏组件一样。LDAP 有非常具体的配置要求，缺乏图形工具，并且有大量的缩写需要记忆。从积极的一面看，您所做的大量艰苦工作是值得的，因为当它工作时，LDAP 将极大地改善您的网络体验。

## 配置您的 LDAP 服务器

配置您的 LDAP 服务器的第一步是安装客户端和服务器应用程序。选择“添加/删除应用程序”，点击“网络服务器”旁边的“详细信息”按钮，并勾选 `openldap-servers`。然后点击“系统工具”旁边的“详细信息”按钮并选择 `openldap-clients`。安装完成后，关闭对话框并打开一个终端。

现在切换到 root 用户，并在您选择的文本编辑器中编辑 `/etc/openldap/slapd.conf`。这是 OpenLDAP 服务器守护进程 `slapd` 的主要配置文件。向下滚动，直到您看到 `database`、`suffix` 和 `rootdn` 行。

这是您的 LDAP 系统最基础的配置。您的服务器名称是什么？`dc` 代表*域组件*，这是存储在 DNS 中您的域名——例如，`example.com`。在我们的示例中，我们使用了 `hudzilla.org`。LDAP 将域名（由点分隔）的每个部分视为一个域组件，因此域 `hudzilla.org` 由域组件 `hudzilla` 和域组件 `org` 组成。

修改后缀行以匹配您的域组件，用逗号分隔。例如：

```
suffix "dc=hudzilla,dc=org"
```

下一行定义根 DN，这是另一个 LDAP 缩写，意味着*可区分名称*。DN 是您目录中一个人的完整描述符：她的名字和她所在的域。例如：

```
rootdn "cn=root,dc=hudzilla,dc=org"
```

`CN` 是另一个 LDAP 缩写，这次意味着*通用名称*。通用名称就是那个——一个人通常被称呼的名字。有些人有几个通用名称。Andrew Hudson 是一个通用名称，但同一用户可能也有通用名称 Andy Hudson。在我们的 `rootdn` 行中，我们定义了一个完整的用户：域 `hudzilla.org` 中的通用名称 root。这些行在本质上是反向读取的。LDAP 首先前往 `org`，搜索 `org` 中的 `hudzilla`，然后搜索 `hudzilla` 中的 `root`。

`rootdn` 之所以重要，是因为它不仅仅是目录中的另一个用户。LDAP 的 root 用户类似于 Linux 中的 root 用户。该用户拥有系统的完全控制权，可以随意进行任何更改。

接下来是一个稍微复杂的部分：需要为 LDAP root 用户设置密码。最简单的方法是打开一个新的终端窗口，同时保留现有的窗口。在新终端中也切换到 root 用户，并输入 `slappasswd`。此工具使用 SHA1 哈希算法为 OpenLDAP 生成密码哈希值。当提示你输入时，请输入密码。当你输入并确认密码后，你应该会看到类似以下的输出：

`{SSHA}qMwXFT2KlUmrA89Gd7z6EK3gRLD1o2W`

这是根据你的密码生成的密码哈希值。你的哈希值将不同于这里显示的示例，但重要的是它以 `{SSHA}` 开头，这表示它使用 SHA1 算法。现在你需要切换回另一个终端（即正在编辑 `slapd.conf` 的那个终端），并在 `rootdn` 行下方添加以下这一行：

`rootpw <your password hash>`

你需要将 `<your password hash>` 替换为 `slappasswd` 的完整输出，如下所示：

`rootpw {SSHA}qMwXFT2KlUmrA89Gd7z6EK3gRLD1o2W`

这将 LDAP 根密码设置为你刚刚使用 `slappasswd` 生成的那个。这是你在 `slapd.conf` 文件中需要做的最后一次更改，因此请保存你的更改并关闭编辑器。

回到终端，运行 `slaptest` 命令。此命令检查 `slapd.conf` 文件是否存在错误，并确保你正确地编辑了它。假设没有错误，请运行以下两个命令：

```bash
chkconfig ldap on
service ldap start
```

这些命令指示 Fedora 在每次启动时都启动 OpenLDAP，并立即启动它。

最后的配置步骤是告诉 Fedora，在未指定 DN 时应该使用哪个 DN。你可以通过转到系统设置并选择身份验证来做到这一点。在弹出的对话框中，在用户信息选项卡和身份验证选项卡中都勾选启用 LDAP 支持。接下来，点击配置 LDAP 按钮，为 LDAP 搜索基础 DN 输入你的 DC（例如，`dc=hudzilla,dc=org`），并为 LDAP 服务器输入 `127.0.0.1`。点击确定，然后再次点击确定。

**提示**

勾选启用 LDAP 支持实际上并不会改变用户登录的方式。在幕后，这会强制 Fedora 在 */etc/openldap* 中设置 *ldap.conf* 文件，从而将未指定基本搜索起点的 LDAP 搜索指向你的 DC。

# 填充你的目录

随着 LDAP 的安装、配置和运行，你现在可以将目录填入人员信息。这涉及更多 LDAP 缩写，绝对不是一件容易的事，所以如果你需要重读几遍才能理解，请不要担心。

首先，创建文件 *base.ldif*。你使用此文件来定义系统的基本组件：域和地址簿。LDIF 是 LDAP 数据 interchange 格式（LDAP Data Interchange Format）的缩写，它是将用户数据记录到 LDAP 目录中的标准方式。以下是我们在示例中使用的文件内容：

```ldif
dn: dc=Hudzilla,dc=org
objectClass: top
objectClass: dcObject
objectClass: organization
dc: Hudzilla
o: Hudzilla Dot Org

dn: ou=People,dc=Hudzilla,dc=org
ou: People
objectClass: top
objectClass: organizationalUnit
```

此文件包含两个独立的实体，由空行分隔。第一个是*组织*，*hudzilla.org*。你已经知道 `dn` 行；它们在目录范围内唯一地定义了每个对象。`objectClass` 指令指定哪些属性允许用于此实体，哪些属性是必需的。在这种情况下，我们用它将 `DC` 设置为 `hudzilla`，并将 `o`（组织名称）设置为 `Hudzilla Dot Org`。

下一个实体定义了地址簿 *People*，我们将所有人员存储在此处。它被定义为一个组织单元，即 `ou` 代表的内容。*组织单元* 实际上只是你公司的任意分区。例如，你可能有用于市场营销、会计和管理的 OU。

你需要根据自己的需求定制该文件。具体来说，将 `DC` 更改为你在 *slapd.conf* 中指定的那些。

接下来，创建并编辑一个新文件 *people.ldif*。你将在此处使用 LDIF 定义地址簿条目。以下是我们在示例中使用的用户：

```ldif
dn: cn=Paul Hudson, ou=People, dc=hudzilla, dc=org
objectClass: inetOrgPerson
cn: Paul Hudson
cn: Hudzilla
mail: paul@hudzilla.org
jpegPhoto: file:///home/paul/paulhudson.jpg
sn: Hudson

dn: cn=Andrew Hudson, ou=People, dc=hudzilla, dc=org
objectClass: inetOrgPerson
cn: Andrew Hudson
cn: IzAndy
mail: andrew@hudzilla.org
sn: Hudson

dn: cn=Nick Veitch, ou=People, dc=hudzilla, dc=org
objectClass: inetOrgPerson
cn: Nick Veitch
cn: CrackAttackKing
mail: nick@hudzilla.org
sn: Veitch
```

那里有三个条目，同样由空行分隔。每个人都有一个 DN，由他的通用名称（CN）、组织单元（OU）和域组件（DC）组成。他还有一个 `objectClass` 定义，`inetOrgPerson`，这赋予他标准属性，如电子邮件地址、照片和电话号码。`inetOrgPerson` 类型的实体必须拥有 CN 和 SN（姓氏），因此你会在这段代码中看到它们。

还要注意，每个人都有两个通用名称：他的真名和一个昵称。并非所有 LDAP 客户端都支持多个 CN，但只要主要名称排在第一位并出现在 DN 中，拥有多个名称并无害处。

> **提示**
>
> 拥有多个键值对，例如多个 CN，是 LDAP 的定义特征之一。在当今互联的世界中，很少有人能用单一的一组属性来定义，因为他们有家庭电话号码、工作电话号码、手机号码，以及几个电子邮件地址，甚至可能还有几个他们热座办公的办公室。使用多个 CN 和其他属性可以让你正确记录这些复杂场景。
