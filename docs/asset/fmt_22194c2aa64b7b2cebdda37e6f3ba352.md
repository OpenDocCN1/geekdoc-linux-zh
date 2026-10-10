
要使 `LDAP` 服务在每次系统重启时自动启动，请输入以下内容：

```bash
chkconfig ldap on
```

默认情况下，`LDAP` 服务将对所有人开放读取权限。

### 设置地址簿

在设置地址簿数据库结构时，我基于组织名称来设置数据库的可分辨名称（`dn`）。

在 `slapd.conf` 文件中，`suffix` 设置为 `example.com`（`suffix "dc=example,dc=com"`，你的会不同），后端数据库被配置为处理指向可分辨名称（`dn`）`example.com` 的查询。接下来，你可以在该可分辨名称下创建该组织的地址簿结构。

> **注意** `dc=` 代表域组件（domain component）。当你将域名作为可分辨名称的一部分时，你放置该域名各部分的顺序是将最接近 DNS 根域的部分放在最后。在此示例中，`dc=example` 位于 `dc=com` 之前。如果你对将域名包含在 `LDAP` 目录中的规范感兴趣，请参阅 `RFC 2247`。

### 设置 LDAP 地址簿服务器

你需要创建一种格式的地址簿文件，以便加载到 `OpenLDAP` 数据库中。你需要的格式被称为 **LDAP 数据交换格式（LDIF）**。你以这种格式输入的信息可用于构建数据库，并一次性从文件向目录中加载大量数据。

以下步骤解释了如何创建包含 `example.com` `LDAP` 目录（可分辨名称）地址簿定义的 `LDIF` 文件，然后将该文件加载到 `LDAP` 服务器中。

1. **创建 LDIF 文件** — 作为 `root` 用户，使用任意文本编辑器创建一个文件来保存你的 `LDAP` 目录条目。在我的示例中，我使用了文件 `/etc/openldap/people.ldif`。

   > **注意** 创建 `LDIF` 文件时，请确保在每个新的可分辨名称（`dn:`）行之前留一个空行。空行告诉 `ldappadd` 开始一个新条目。如果没有空行，`LDAP` 不会认为你正在开始一个新的可分辨名称。此外，请删除每行前的所有空格，确保所有新行从第 1 列开始。（行首的空格表示新行实际上是前一行的一部分。）

2. **定义组织** — 你需要定义将要加载到 `LDAP` 服务器中的目录。在我的示例中，我添加了信息，在可分辨名称 `example.com`（`dc=example, dc=com`）下将组织定义为 `Example Organization`，方法是向 `people.ldif` 文件添加以下信息。

   ```ldif
   dn:               dc=example,dc=com
   objectClass:       dcObject
   objectClass:       organization
   dc:               example
   o:                 Example Organization
   ```

3. **添加组织角色** — 我通过向 `people.ldif` 文件添加以下行来标识地址簿管理员的角色。

   ```ldif
   dn:               cn=Manager,dc=example,dc=com
   objectClass:       organizationalRole
   cn:               Manager
   description:       Example Book Administrator
   ```

4. **添加组织单元** — 由于在这个示例中，地址簿基本上由组织成员的名字和地址组成，因此我将组织单元（`ou`）命名为 `members`。

   ```ldif
   dn:               ou=members,dc=example,dc=com
   objectClass:       top
   objectClass:       organizationalUnit
   ou:               members
   ```

   > **注意** 尽管在我的示例中，我创建了一个位于目录结构顶部的地址簿，但如果你在大公司工作，你可能希望拥有更复杂的目录结构。例如，除了在目录结构顶部有一个地址簿外，你还可以为不同国家、地点或部门创建额外的组织单元。

### 第 4 部分 网络配置

接着，每个部门单元可能都有自己的通讯录。您可能还希望支持每个部门单元下的多个目录。例如，可以有一个独立的目录来跟踪计算机设备或公司车辆。

#### 5. 添加联系人

在目录结构就位，并且在 `example.com` 可区分名称下有一个成员部门单元的情况下，我可以开始向目录中添加联系人。我将每个人定义为 `organizationalPerson` 和 `inetOrgPerson` 对象类。我可以为每个联系人的信息添加许多不同的属性。然而，我所选择的大多数属性都是 `Thunderbird` 邮件客户端（将在本章稍后展示）将会读取的属性。以下是两条条目：

```ldif
cn=John Wilson,ou=members,dc=example,dc=com
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: John Wilson
mail: jwilson@example.com
givenname: John
sn: Wilson
uid: jwilson
o: Example Organization
telephoneNumber: 800-555-1212
homePhone: 800-555-1313
mobile: 800-555-1414
pager: 800-555-1515
facsimileTelephoneNumber: 800-555-1414
title: Account Executive
homePostalAddress: 1234 Broadway, New York NY 99999
```

```ldif
cn=Andrew Smith,ou=members,dc=example,dc=com
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: Andrew Smith
mail: awsmith@example.com
givenname: Andrew
sn: Smith
uid: awsmith
o: Example Organization
telephoneNumber: 800-555-2893
homePhone: 800-555-4329
mobile: 800-555-8458
pager: 800-555-8955
facsimileTelephoneNumber: 800-555-3838
title: Interior Decorator
homePostalAddress: 167 E Street, Salt Lake UT 99999
```

正如您在此处所见，通讯录目录（称为 `members`）中列出的两个人分别与一个通用名称（`cn`）相关联，即 `John Wilson` 和 `Andrew Smith`，他们位于 `members` 部门单元中，该单元隶属于 `example.com` 域组件。

您可以通过重复此结构向此文件添加任意数量的联系人。（注意，地址中使用逗号来分隔行。）

> **注意** 您可能会发现这里显示的所有属性并不都是必需的，或者您可能想添加其他属性。请参考模式文件以查看 `organizationalPerson`、`inetOrgPerson` 以及您可能希望在通讯录中使用的其他对象类的可用属性列表。

#### 6. 保存 LDIF 文件

将更改保存到您的 `LDIF` 文件（在我的案例中，该文件名为 `/etc/openldap/people.ldif`）。

#### 7. 将信息添加到 LDAP 服务器

您可以使用 `ldapadd` 命令将您创建的 `LDIF` 文件的全部内容添加到您的 `LDAP` 目录中。以下是我用于将我的 `LDIF` 文件（称为 `people.ldif`）的内容添加到我的 `LDAP` 目录的命令：

```bash
ldapadd -xv -D "cn=Manager,dc=example,dc=com" -W -f people.ldif
Enter LDAP Password: mysecret
add objectClass:
    dcObject
    organization
add dc:
    example
add o:
    Example Organization
adding new entry "dc=example,dc=com"
modify complete
add objectClass:
    organizationalRole
add cn:
    Manager
add description:
    Example Address Book Administrator
adding new entry "cn=Manager,dc=example,dc=com"
modify complete
.
.
add cn:
    John Wilson
add mail:
    jwilson@example.com
add givenname:
    John
add sn:
    Wilson
.
.
.
add cn:
    Andrew Smith
add mail:
    awsmith@example.com
add givenname:
    Andrew
add sn:
    Smith
```

这里显示的密码（输入时不会显示）是您在 `slapd.conf` 文件中添加的那个密码。在示例中，我使用 `mysecret` 作为密码。`-x` 表示使用简单身份验证（不使用 `SASL`）。`-D` 表示使用之前在 `slapd.conf` 文件中定义的可区分名称（`cn=Manager, dc=example, dc=com`）。`-W` 表示提示输入密码，而不是在命令行中输入它。`-f` 指示要加载的文件（在本文中给出的示例中，是 `people.ldif`）。

当 `ldapadd` 命令成功添加每个条目时，它会列出与每个条目相关的对象。

#### 8. 重启服务器

此时，您可以输入以下内容来重启服务器：

```bash
/etc/init.d/ldap restart
```

#### 9. 搜索目录

为了确保所有内容都正确插入目录中，您可以运行以下搜索命令：

```bash
ldapsearch -x -W -D 'cn=Manager,dc=example,dc=com' \
-b 'dc=example,dc=com' '(objectClass=*)'
```

输出示例：

```text
extended LDIF
#
LDAPv3
base <dc=example,dc=com> with scope subtree
filter: (objectClass=*)
requesting: ALL
#
#
example.com
dn: dc=example,dc=com
objectClass: top
objectClass: dcObject
objectClass: organization
dc: example
o: Example Organization

Manager, example.com
dn: cn=Manager,dc=example,dc=com
objectClass: organizationalRole
cn: Manager
description: Example Address Book Administrator

members, example.com
dn: ou=members,dc=example,dc=com
objectClass: top
objectClass: organizationalUnit
ou: members

John Wilson, example.com
dn: cn=John Wilson,ou=members,dc=example,dc=com
objectClass: organizationalPerson
objectClass: inetOrgPerson
cn: John Wilson
mail: jwilson@example.com
givenName: John
sn: Wilson
uid: jwilson
o: Example Organization
```

在这个示例中，我请求使用简单身份验证（使用 `-x` 选项的明文密码），从 `example.com` 目录的基底（`-b`）开始搜索，并列出所有对象类（`objectClass=*`）。如果您愿意，可以将输出通过管道传递给 `less`，以便您可以逐页浏览。

#### 10. 调试您的目录

不要指望您的 `LDIF` 文件能在没有任何错误的情况下首次加载。在调试您的通讯录目录时，我建议您使用非生产机器，并在每次尝试加载目录失败后清除数据库文件。假设您将 `LDAP` 目录文件保留在 `/var/lib/ldap` 中，并且在您调试条目时清除整个数据库是可以接受的，您可以执行以下操作：

> **警告** 您即将擦除您创建的 `LDAP` 目录文件。如果您的 `LDAP` 目录文件中包含没有保存在 `LDIF` 文件中的信息，请不要执行此步骤。不要擦除您的 `LDIF` 文件，因为您需要它来重新创建您的目录文件。

```bash
/etc/init.d/ldap stop
rm /var/lib/ldap/*
/etc/init.d/ldap restart
slapadd -x -D "cn=Manager,dc=example,dc=com" -W -f people.ldif
```

重复此过程，直到您觉得您的 `LDIF` 文件及其包含的所有信息都已正确加载到您的 `LDAP` 目录文件中。

此时，您可以决定是否需要对 `LDAP` 目录进行进一步调整（如“更多 LDAP 配置方式”一节中所述）。在那之后，我建议通过尝试使用 `Thunderbird` 的联系人功能（将在本章稍后描述）访问您的 `LDAP` 通讯录目录，来检查其是否正常工作。

### 更多 LDAP 配置方式

如果您计划将 `LDAP` 目录扩展以用于更多的小型办公室或家庭邮件服务器，您可能需要考虑一些额外的配置选项。以下是一些建议：

- **复制 LDAP 目录** — 您可以使您的 `LDAP` 目录可被多个 `LDAP` 服务器访问，并使目录的更新传播到这些服务器。有关设置 `LDAP` 目录复制的信息，请参见 `slurpd` 守护进程（处理更新复制）的 man 页面和 *OpenLDAP 管理员指南*（`/usr/share/doc/openldap-servers*/guide.html`）。
- **添加证书** — 传输层安全（`TLS`）内置于 `OpenLDAP` 服务器中。有关定义 `slapd` 守护进程将接受的证书和加密算法的信息，请参阅 `slapd.conf` man 页面。
- **更改日志级别** — 您可以指定 `slapd` 守护进程执行的调试级别。通过向 `slapd.conf` 文件添加 `loglevel <integer>` 选项，您可以让 `slapd` 执行以下类型的日志记录：

| 日志级别 | 描述 |
| :--- | :--- |
| 1 | 跟踪函数调用 |
| 2 | 调试数据包处理 |
| 4 | 重型跟踪调试 |
| 8 | 连接管理 |
| 16 | 打印发送和接收的数据包 |
| 32 | 搜索过滤器处理 |
| 64 | 配置文件处理 |
| 128 | 访问控制列表处理 |
| 256 | 统计日志连接/操作/结果 |
| 512 | 统计日志发送的条目 |
| 1024 | 打印与 shell 后端的通信 |
| 2048 | 条目解析 |

默认情况下，`loglevel` 为 256。要记录所有内容，请将 `loglevel` 设置为 4095。要获取 `loglevel` 功能的组合，只需将您想要的数字相加即可。例如，对于跟踪函数调用、重型跟踪调试和连接管理，使用数字 13（即 `1 + 4 + 8`）。

- **限制搜索** — 您可以限制搜索可以返回的条目数量（默认为 `sizelimit 500`）以及 `slapd` 响应搜索请求所花费的时间（秒为单位）（`timelimit 3600`）。将您希望用于 `LDAP` 目录的新值添加到您的 `slapd.conf` 文件中。
- **添加访问控制策略** — 在 `slapd.conf` 文件中，默认的数据库访问设置为允许任何能够访问数据库的人进行读取访问。如果您想改变这种行为，您可以添加访问行有选择地决定谁可以读取和写入您的数据库。在这个示例中，我希望允许每个人都能从数据库读取，但只允许人们更改自己的信息。有关更多信息，请参阅 `slapd.conf` man 页面。

### 在 Thunderbird 中访问 LDAP 地址簿

配置并运行好 `LDAP` 地址簿后，你应该可以使用它从任何支持 `LDAP` 目录的电子邮件客户端获取电子邮件地址。假设你的 `LDAP` 目录已启动并运行，以下示例展示了如何使用 `Thunderbird`（`CentOS` 发行版附带此软件）在 `LDAP` 目录中搜索电子邮件地址。

1. 在 `Thunderbird` 中，点击“地址簿”按钮。
2. 在地址簿窗口中，选择**文件** ➤ **新建** ➤ **LDAP 目录**。在出现的 `Thunderbird` 目录服务器属性窗口中，在“常规”选项卡上至少输入以下信息：
   - **名称** — 在 `LDAP` 服务器列表中用于标识该服务器的名称
   - **主机名** — 托管 `LDAP` 内容的计算机的名称或 `IP` 地址
   - **基础 DN** — 指示在 `LDAP` 目录中开始搜索的位置。你可以选择**查找**让 `Thunderbird` 检查你的 `LDAP` 服务器以获取搜索基础。在示例中，`dc=example, dc=com` 是搜索基础。
   - **端口** — 输入 `LDAP` 服务器的 `IP` 地址。默认端口号为 `389`。

图 21-1 显示了刚才填写好的目录服务器属性窗口。

#### 图 21-1

输入有关你的 `LDAP` 目录服务器的信息，以便从 `Thunderbird` 搜索地址。
