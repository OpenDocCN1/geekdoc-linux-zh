

rootdn 很重要，因为它不仅仅是目录中的另一个用户。LDAP root 用户就像 Linux 中的 root 用户一样。它是拥有对系统完全控制权的人，可以随意进行任何更改。

接下来是一个稍微复杂一点的部分：我们需要为 LDAP root 用户设置密码。最简单的方法是打开一个新终端窗口，与现有的终端并行使用。在新终端中切换到 root，然后输入 slappasswd。该工具使用 SHA1 哈希算法为 OpenLDAP 生成密码哈希。提示时输入一个密码。输入并确认密码后，你应该会看到类似这样的输出：

```
{SSHA}qMVxFT2K1UUmrA89Gd7z6EK3gRLD1o2W
```

这就是从你的密码生成的密码哈希。你的与此处显示的不同，但重要的是它以 {SSHA} 开头，表示使用 SHA1。现在你需要切换回另一个终端（正在编辑 slapd.conf 的那个），并在 rootdn 行下方添加这一行：

```
rootpw <your password hash>
```

你应该用 slappasswd 的完整输出替换 <your password hash>，如下所示：

```
rootpw {SSHA}qMVxFT2K1UUmrA89Gd7z6EK3gRLD1o2W
```

这样就将 LDAP root 密码设置为刚刚用 slappasswd 生成的密码。这是你在 slapd.conf 文件中需要做的最后一次更改，因此保存更改并关闭编辑器。

回到终端，运行 slaptest 命令。这会检查你的 slapd.conf 文件是否存在错误，并确保你正确编辑了它。假设没有错误，运行 /etc/init.d/slapd 以启动 OpenLDAP。

Ubuntu 在每次启动时都会自动启动 OpenLDAP，但该命令会立即启动它。

最后的配置步骤是告诉 Ubuntu 如果未指定则应使用哪个 DN。你可以通过进入系统设置并选择身份验证来完成此操作。在出现的对话框中，在“用户信息”选项卡和“身份验证”选项卡中均勾选启用 LDAP 支持。接下来，单击配置 LDAP 按钮，输入你的 DC（例如，dc=hudzilla,dc=org）作为 LDAP 搜索基本 DN，并输入 127.0.0.1 作为 LDAP 服务器。单击确定，然后再次单击确定。

## TIP

勾选启用 LDAP 支持并不会真正改变你的用户登录方式。在幕后，这会强制 Ubuntu 在 /etc/ldap 中设置 ldap.conf 文件，以便未指定基本搜索起始点的 LDAP 搜索被定向到你的 DC。

## 填充你的目录

LDAP 安装、配置并运行后，你现在可以开始填充目录中的人员。这涉及更多 LDAP 缩写，绝非易事，因此如果你需要多次重读才能理解，请不要担心。

首先，创建文件 base.ldif。你将使用它来定义系统的基本组件：域和地址簿。LDIF 是 LDAP 数据交换格式的缩写，它是记录用户数据以插入 LDAP 目录的标准方式。以下是我们示例中使用的内容：

```
dn: dc=hudzilla,dc=org
objectClass: top
objectClass: dcObject
objectClass: organization
dc: hudzilla
o: Hudzilla Dot Org

dn: ou=People,dc=hudzilla,dc=org
ou: People
objectClass: top
objectClass: organizationalUnit
```

该文件包含两个独立的实体，由空行分隔。第一个是我们的组织 hudzilla.org。dn 行你已经知道了，因为它们在目录范围内唯一定义每个对象。objectClass 指令指定允许此实体使用哪些属性以及需要哪些属性。在本例中，我们用它将 DC 设置为 hudzilla，并将 o（组织名称）设置为 Hudzilla Dot Org。

下一个实体定义了地址簿 People，所有人员都将存储在其中。它被定义为一个组织单位，这就是 ou 的含义。组织单位实际上只是你公司的一个任意分区。例如，你可能有用于市场营销、会计和管理部门的 OU。

你需要根据自己的需求自定义该文件。具体来说，将 DCs 改为你在 slapd.conf 中指定的那些。

接下来，创建并编辑一个名为 people.ldif 的新文件。这就是你将使用 LDIF 定义地址簿条目的地方。以下是我们示例中使用的联系人：

```
dn: cn=Paul Hudson,ou=People,dc=hudzilla,dc=org
objectClass: inetOrgPerson
cn: Paul Hudson
cn: Hudzilla
mail: paul@hudzilla.org
jpegPhoto: file:///home/paul/paulhudson.jpg
sn: Hudson
```

