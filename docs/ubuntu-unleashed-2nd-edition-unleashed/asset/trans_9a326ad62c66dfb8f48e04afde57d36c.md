

## 填充你的目录

LDAP 安装、配置并运行后，你现在可以开始向目录中添加人员。这又涉及更多 LDAP 缩写，绝非易事，所以如果你需要重读几遍才能理解，也不用担心。

首先，创建文件 base.ldif。你将用它来定义系统的基础组件：域名和地址簿。LDIF 是 LDAP Data Interchange Format 的缩写，是记录用户数据以插入 LDAP 目录的标准方式。下面是我们示例中使用的内容：

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

此文件包含两个独立的实体，由空行分隔。第一个是我们的组织 hudzilla.org。你已经熟悉 dn 行，因为它们在目录范围内唯一定义每个对象。objectClass 指令指定允许此实体使用哪些属性以及哪些属性是必需的。在此例中，我们用它将 DC 设置为 hudzilla，并将 o（组织名称）设置为 Hudzilla Dot Org。

下一个实体定义了地址簿 People，所有人员都将存储在其中。它被定义为一个组织单位，这就是 ou 的含义。组织单位本质上只是公司的一个任意分区。例如，你可能有用于市场、会计和管理部门的 OU。

你需要根据自己的需求自定义该文件。具体来说，将 DCs 改为你在 slapd.conf 中指定的内容。

接下来，创建并编辑一个名为 people.ldif 的新文件。你将在其中使用 LDIF 定义地址簿的条目。下面是我们示例中使用的联系人：

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

这里有三个条目，同样由空行分隔。每个人都有一个 DN，由其常用名（CN）、组织单位（OU）和域名组件（DCs）组成。他还有一个 objectClass 定义 inetOrgPerson，它为其提供标准属性，如电子邮件地址、照片和电话号码。类型为 inetOrgPerson 的实体必须具有 CN 和 SN（姓氏），因此你会在代码中看到它们。

还请注意，每个人都有两个常用名：他的真实姓名和昵称。并非所有 LDAP 客户端都支持多个 CN，但只要主要名称排在最前面并列在 DN 中，拥有多个 CN 也无害。

### TIP

拥有多个键/值对，例如多个 CN，是 LDAP 的定义特征之一。在当今互联的世界里，很少有人能用单一属性集来定义，因为人们现在拥有家庭电话号码、工作电话号码、手机号码、寻呼机号码，外加多个电子邮件地址，甚至可能有多处热办公地点。使用多个 CN 和其他属性可以让你正确记录这些复杂情况。

第一个实体的 jpegPhoto 属性具有非常特定的语法。在冒号之后，你使用一个左尖括号（<），后跟一个空格，然后是人物图片的位置。因为图片是本地的，所以它以 file:// 为前缀。它位于 /home/paul/paulhudson.jpg，因此整个 URL 为 file:///home/paul/paulhudson.jpg。

在你编辑完文件以包含组织中的人员后，保存并关闭编辑器。以 root 身份执行以下两个命令：

```
ldapadd -x -W -D 'cn=root,dc=hudzilla,dc=org' -f base.ldif
ldapadd -x -W -D 'cn=root,dc=hudzilla,dc=org' -f people.ldif
```

