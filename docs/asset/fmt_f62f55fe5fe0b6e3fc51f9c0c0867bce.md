
CN 是另一个 LDAP 缩写，这次意为 common name。常用名就是其字面意思——一个人通常被称呼的名字。有些人有几个常用名。Andrew Hudson 是一个常用名，但同一个用户也可能有常用名 Andy Hudson。在我们的 `rootdn` 行中，我们定义了一个完整用户：域 `hudzilla.org` 下的常用名 `root`。这些行本质上是反向读取的。LDAP 首先访问 `org`，搜索 `org` 中的 `hudzilla`，然后在 `hudzilla` 中搜索 `root`。

`rootdn` 很重要，因为它不仅仅是目录中的另一个人。`root` LDAP 用户就像 Linux 中的 `root` 用户。它是拥有对系统完全控制权的人，可以做出他想要的任何更改。

现在来到了稍微复杂一点的部分：我们需要为 LDAP `root` 用户设置密码。最简单的方法是打开一个新终端窗口，与现有窗口并行。在新终端中切换到 `root` 并输入 `slappasswd`。此工具使用 SHA1 哈希算法为 OpenLDAP 生成密码哈希。提示时输入密码。当你输入并确认密码后，你应该会看到类似这样的输出：

```
{SSHA}qMVxFT2K1UUmrA89Gd7z6EK3gRLDIo2W
```

那是从你的密码生成的密码哈希。你的与此处显示的不同，但重要的是它以 `{SSHA}` 开头，表示使用 SHA1。现在你需要切换回另一个终端（正在编辑 `slapd.conf` 的那个）并在 `rootdn` 行下方添加此行：

```
rootpw <your password hash>
```

你应该用 `slappasswd` 的完整输出替换 `<your password hash>`，如下所示：

```
rootpw {SSHA}qMVxFT2K1UUmrA89Gd7z6EK3gRLDIo2W
```

这将 LDAP `root` 密码设置为你刚刚用 `slappasswd` 生成的密码。这是你在 `slapd.conf` 文件中需要做的最后一次更改，因此保存更改并关闭编辑器。

回到终端，运行 `slaptest` 命令。这会检查你的 `slapd.conf` 文件是否存在错误，并确保你正确编辑了它。假设没有错误，运行 `/etc/init.d/slapd` 启动 OpenLDAP。

Ubuntu 在每次启动时都会自动启动 OpenLDAP，但该命令会立即启动它。

最后的配置步骤是告诉 Ubuntu 如果未指定，它应该使用哪个 DN。你可以通过进入系统设置并选择身份验证来完成此操作。在出现的对话框中，在用户信息选项卡和身份验证选项卡中均勾选启用 LDAP 支持。接下来，单击配置 LDAP 按钮，为 LDAP 搜索基本 DN 输入你的 DCs（例如 `dc=hudzilla,dc=org`），并为 LDAP 服务器输入 `127.0.0.1`。单击确定，然后再次单击确定。

> **提示**
>
> 勾选启用 LDAP 支持并不会真正改变你的用户登录方式。在幕后，这会强制 Ubuntu 在 `/etc/ldap` 中设置 `ldap.conf` 文件，以便未指定基本搜索起点的 LDAP 搜索被定向到你的 DC。

### 填充你的目录

LDAP 安装、配置并运行后，你现在可以开始向目录中添加人员。这又涉及更多 LDAP 缩写，绝非易事，所以如果你需要重读几遍才能理解，也不用担心。

首先，创建文件 `base.ldif`。你将用它来定义系统的基础组件：域名和地址簿。LDIF 是 LDAP Data Interchange Format 的缩写，是记录用户数据以插入 LDAP 目录的标准方式。下面是我们示例中使用的内容：

```
dn: dc=hudzilla,dc=org
objectClass: top
objectClass: dcObject
objectClass: organization
dc: hudzilla
o: Hudzilla Dot Org
```

```
dn: ou=People,dc=hudzilla,dc=org
ou: People
objectClass: top
objectClass: organizationalUnit
```

此文件包含两个独立的实体，由空行分隔。第一个是我们的组织 `hudzilla.org`。你已经熟悉 `dn` 行，因为它们在目录范围内唯一定义每个对象。`objectClass` 指令指定允许此实体使用哪些属性以及哪些属性是必需的。在此例中，我们用它将 DC 设置为 `hudzilla`，并将 `o`（组织名称）设置为 `Hudzilla Dot Org`。

下一个实体定义了地址簿 `People`，所有人员都将存储在其中。它被定义为一个组织单位，这就是 `ou` 的含义。组织单位本质上只是公司的一个任意分区。例如，你可能有用于市场、会计和管理部门的 OU。

你需要根据自己的需求自定义该文件。具体来说，将 DCs 改为你在 `slapd.conf` 中指定的内容。

接下来，创建并编辑一个名为 `people.ldif` 的新文件。你将在其中使用 LDIF 定义地址簿的条目。下面是我们示例中使用的联系人：

```
dn: cn=Paul Hudson,ou=People,dc=hudzilla,dc=org
objectClass: inetOrgPerson
cn: Paul Hudson
cn: Hudzilla
mail: paul@hudzilla.org
jpegPhoto:< file:///home/paul/paulhudson.jpg
sn: Hudson
```

```
dn: cn=Andrew Hudson,ou=People,dc=hudzilla,dc=org
objectClass: inetOrgPerson
cn: Andrew Hudson
cn: IzAndy
mail: andrew@hudzilla.org
sn: Hudson
```

```
dn: cn=Nick Veitch,ou=People,dc=hudzilla,dc=org
objectClass: inetOrgPerson
cn: Nick Veitch
cn: CrackAttackKing
mail: nick@hudzilla.org
sn: Veitch
```

这里有三个条目，同样由空行分隔。每个人都有一个 DN，由其常用名（CN）、组织单位（OU）和域名组件（DCs）组成。他还有一个 `objectClass` 定义 `inetOrgPerson`，它为其提供标准属性，如电子邮件地址、照片和电话号码。类型为 `inetOrgPerson` 的实体必须具有 CN 和 SN（姓氏），因此你会在代码中看到它们。

还请注意，每个人都有两个常用名：他的真实姓名和昵称。并非所有 LDAP 客户端都支持多个 CN，但只要主要名称排在最前面并列在 DN 中，拥有多个 CN 也无害。

### TIP

拥有多个键/值对，例如多个 CN，是 LDAP 的定义特征之一。在当今互联的世界里，很少有人能用单一属性集来定义，因为人们现在拥有家庭电话号码、工作电话号码、手机号码、寻呼机号码，外加多个电子邮件地址，甚至可能有多处热办公地点。使用多个 CN 和其他属性可以让你正确记录这些复杂情况。

第一个实体的 `jpegPhoto` 属性具有非常特定的语法。在冒号之后，你使用一个左尖括号（`<`），后跟一个空格，然后是人物图片的位置。因为图片是本地的，所以它以 `file://` 为前缀。它位于 `/home/paul/paulhudson.jpg`，因此整个 URL 为 `file:///home/paul/paulhudson.jpg`。

在你编辑完文件以包含组织中的人员后，保存并关闭编辑器。以 `root` 身份执行以下两个命令：

```
ldapadd -x -W -D 'cn=root,dc=hudzilla,dc=org' -f base.ldif
ldapadd -x -W -D 'cn=root,dc=hudzilla,dc=org' -f people.ldif
```

`ldapadd` 命令用于将 LDIF 转换为实时的目录内容，最重要的是可以在 LDAP 服务器运行时执行。`-x` 参数表示仅使用基本身份验证，这意味着你需要提供 `root` 用户名和密码。`-W` 表示提示你输入密码。`-D` 允许你指定用户名对应的 DN；并且在 `-D` 之后，我们指定了 `slapd.conf` 中之前设置好的 `root` DN。最后，`-f` 表示使用以下文件中的 LDIF。

当你运行它们时，会提示你输入之前设置的 `root` 密码。输入后，你应该会看到确认信息，条目被添加，例如：

```
adding new entry "cn=Paul Hudson,ou=People,dc=hudzilla,dc=org"
```

如果看到类似 `ldap_bind: Can't contact LDAP server (-1)` 的错误，你需要通过输入 `/etc/init.d/slapd start` 来启动 LDAP 服务器。其他错误的可能来源大多是输入错误。LDIF 是一种精确的格式，甚至对其空白字符的使用也很严格。

要测试目录是否已填充并且你的配置设置是否正确，运行以下命令：

```
ldapsearch -x 'objectclass=*'
```
