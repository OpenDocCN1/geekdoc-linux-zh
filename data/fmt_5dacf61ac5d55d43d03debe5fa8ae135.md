
文件包含两个实体，用空行分隔。第一个是组织 `hullzilla.org`。你已经知道 `dn` 行，它们在目录范围内唯一地定义了对象。`objectClass` 指令指定了该实体允许哪些属性以及哪些属性是必须的。在这种情况下，我们使用将 `dc` 设置为 `hullzilla`，将 `o`（组织名称）设置为 `Huzilla Org`。

下一个实体定义了地址录 `People`，我们所有人将存储在此处。它被定义为一个组织单元（organizational unit），这就是 `ou` 的含义。组织单元只是你公司的一个任意划分。例如，你可能会有市场部、会计和管理部的 OU。

你需要根据自己的需求自定义文件。具体来说，将 DCs 修改为你在 `slapd.conf` 中指定的那些。

接下来，创建并编辑名为 `people.ldif` 的新文件。你将在这里使用 LDIF 为你的地址录定义条目。

# 配置服务器 555

```
dn: cn=Paul Hudson,ou=People,dc=huddzilla,dc=org
objectClass: inetOrgPerson
cn: Paul Hudson
cn: Hudzilla
mail: paul@huddzilla.org
jpegPhoto:< file:///home/paul/paulhudson.jpg
sn: Hudson

dn: cn=Andrew Hudson,ou=People,dc=huddzilla,dc=org
objectClass: inetOrgPerson
cn: Andrew Hudson
cn: IzAndy
mail: andrew@huddzilla.org
sn: Hudson

dn: cn=Nick Veitch,ou=People,dc=huddzilla,dc=org
objectClass: inetOrgPerson
cn: Nick Veitch
cn: CrackAttackKing
mail: nick@huddzilla.org
sn: Veitch
```

这里三个条目，每个条目之间用空行分隔。每一个人都有一个 DN，它由通用名称（CN）、组织单元（OU）和域名组件（DCs）组成。他们还拥有 `objectClass` 定义，即 `inetOrgPerson`，这为他们提供了标准属性，如电子邮件地址、照片和电话号码。`inetOrgPerson` 类型的实体必须具有 CN 和 SN（姓氏），你会在这段代码中看到它们。

注意，每个人都有两个通用名称：他的真实姓名和昵号。并不是所有的 LDAP 客户端都支持多个 CN，但只要其中一个在前面并列在 DN 中，拥有多个 CN 也没有什么坏处。

> 提示 拥有多个键/值对（例如多个 CN）是 LDAP 的定义特征之一。在当今这个互互通的世界里，很少有人能用单组属性来定义，因为他们有电话号码、工作电话、手机号，以及多个电子邮件地址，甚至可能还有好几个办公的地点。使用多个 CN 和其他属性可以让你妥善地记录这些复杂的场景。

第一个实体的 `jpegPhoto` 属性具有非常特殊的语法。在冒号之后，你会看到一个左角括号（`<`），后面是一个空格，然后是人物照片的位置。由于照片是本地的，所以它带有 `file://` 前缀。它位于 `/home/paul/paulhudson.jpg`，因此整个 URL 为 `file:///home/paul/paulhudson.jpg`。

编辑完文件以包含你组织中的人员后，保存文件并关闭编辑器。以 root 身份执行以下两条命令：

```
ldapadd -x -D "cn=root,dc=hudzilla,dc=org" -f base.ldif
```

```
ldapadd -x -D "cn=root,dc=hudzilla,dc=org" -f people.ldif
```

`ldapadd` 命令用于将 LDIF 转换为实时目录内容，最重要的是，它可以在你的 LDAP 服务器运行时执行。`-x` 参数意味着使用基本身份验证，这意味着你需要指定 root 用户名和密码。`-W` 表示提示输入密码。`-D` 让你为用户名指定 DN，在 `-D` 之后，我们指定了早些在 `slapd.conf` 中设置的 root DN。最后，`-f` 表示使用后续文件的 LDIF。

当你运行它时，系统会提示你输入之前设置的 root 密码。输入密码后，你应该会看到条目被添加的确认消息，例如：
`new entry "cn=Paul Hudson,ou=People,dc=huddzilla,dc=org"`

如果你看到类似 `ldap_bind: Can't contact LDAP server (-1)` 的错误，你需要通过输入 `ldap start` 来启动 LDAP 服务器。其他条目最可能的来源是输入错误。LDIF 是一种精确的格式，甚至连空格的使用也是如此。

要测试目录已填充且你的配置设置正确，请运行此命令：

```
ldapsearch -x 'objectclass=*'
```

`ldapsearch` 命令的作用正如你预期的那样：从命令行查询 LDAP 目录。同样，`-x` 意味着使用简单身份验证，尽管在这种情况下你提供任何凭据，因为你只需要读取目录。`objectclass=*` 搜索指定你正在搜索任何 `objectclass` 的条目，因此搜索将返回目录中的所有条目。

你可以修改搜索以使其更具体，例如：

```
ldapsearch -x 'cn=Ni*'
```
