
# Load backend modules

`dn`: `cn-module,cn=config`

`objectClass`: `olcModule`

`cn`: `module`

`lcModulepath`:`/usr/lib/ldap`

`lcModuleLoad`: `back_hnb`

## Database settings

`dn`: `olcDatabase=mdb,cn=config`

`objectClass`: `olcDatabaseConfig`

`objectClass`: `olcHdbConfig`

`lcDatabase`=`{1}hdb`

`lcSuffix`: `dc=mattthewhelmke,dc=com`

`lcDBDirectory`:`/var/lib/ldap`

`lcRootDN`: `cn=admin,dc=mattthewhelmke,dc=com`

```
*(注：原文代码中存在多处拼写错误，如 lcModulepath 应为 olcModulePath，lccHdbConfig 应为 olcDBConfig 等，此处保留原文)*
```
```
*(注：原文代码中还存在大量截断或错误的属性行，翻译时遵循原文结构)*
```
```
*(注：由于原文代码块存在大量不完整和重复错误，此处严格按照提供的文本内容进行对齐处理)*
```
```
*(注：由于原文代码块存在大量截断，此处错误按照提供的文本文本进行处理)*
```

以 `.schema` 结尾的文件中的示例，以及一些已转换为 LDIF 格式的示例。使用时，文件必须是 LDAP 数据交换格式（LDIF），或者当作为文件后缀时为 `.ldif`。你可以转换一个示例 schema，也可以创建自己的 schema。

## 配置客户端

虽然 Ubuntu 自带了一系列客户端，但没有足够的空间涵盖所有的客户端。因此，我们决定介绍最常用的两个客户端：默认的 Evolution 和 Thunderbird。两者都是强大的消息解决方案，因此它们与 LDAP 配合得都很好。在这两者中，Thunderbird 似乎配置更简单。过去，我们在 Thunderbird 第一次就能正常工作的情况下，Evolution 遇到过问题。

### Evolution

要为 Evolution 配置 LDAP，点击“新建”（New）按钮旁边的箭头并选择“地址录”（Address Book）。会出现一个新屏幕；其第一个提示询问您要创建的地址录类型。在 LDAP 服务器上。

对于“名称”（Name），只需输入 Address book，对于“服务器”（Server），输入你的 LDAP 服务器的 IP 地址（如果你在服务器上操作，则输入 `127.0.0.1`），如图 30.1 所示。将端口保持为 `389`，这是 `slapd` 的默认端口。切换到“详情”（Details）选项卡，并将“搜索基准”（Search Base）设置为你地址录的完整 DN（例如，`ou=People,dc=matthewhelmke,dc=com`）。将“范围”（Scope）设置为 Sub（子级），这样 Evolution 就会执行全面搜索。要查找，点击“添加地址录”（Add Address Book）。

### Thunderbird

Thunderbird 的配置比 Evolution 稍微简单，并且通常运行更好，特别是对于具有多个 CN 的条目。要启用它，进入“编辑”（Edit）菜单，点击“首选项”（Preferences），然后从上方选项卡中选择“编写”（Composition）。

在“地址”（Addressing）子标签中，点击“目录服务器”（Directory Server）框并点击右侧的“编辑目录”（Edit Directories）按钮。在出现的对话框中，点击“添加到新目录”（Add to a new directory）。你可以给它任何想要的名称，这主要用于显示。如图 30.2 所示，将“主机名”（Hostname）设置为你的 LDAP 服务器的 IP 地址（如果你在服务器上操作，则输入 `127.0.0.1`）。将“基 DN”（Base DN）设置为你地址录的 DN（例如，`ou=People,dc=matthewhelmke,dc=com`），并保留端口号 `389`。连续点击 OK 返回主界面。

## 管理

在你设置好 LDAP 客户端后，在外部发生变化之前，它们几乎不需要维护。具体来说，如果你的目录中的某人发生了变化，例如更改了电话号码、结婚了（更改了姓氏 [surname]）等，你需要能够更新目录以反映这些变化。

### 管理

# 573

![](img/e5934b384118c0ba38d424f9d13b7b0a_603_0.png)

图 30.1 捕捉 Evolution 使用 LDAP 用于地址对于匿名连接来说很容易。

![](img/e5934b384118c0ba38d424f9d13b7b0a_603_1.png)

图 30.2 Thunderbird 的选项比 Evolution 隐藏得更深，但它允许你下载 LDAP 目录供离线使用。

我们早些通过 `ldap-utils` 包安装了一些实用工具。以下是我们的操作：每个操作都需要管理员权限，我们使用 `sudo`：

- `ldapsearch`—打开到 LDAP 服务器的连接并在其目录中搜索请求的信息。
- `ldapmodify`—打开到 LDAP 服务器的连接并允许你添加或修改条目。
- `ldapadd`—打开到 LDAP 服务器的连接并允许你添加条目。
- `ldapdelete`—打开到 LDAP 服务器的连接并允许你删除一个或多个条目。

这些都不容易使用，但它们的帮助页（man pages）中都有相当大量的文档。

更智能的选项是使用 `phpLDAPAdmin`，它是一个 LDAP 管理工具，允许你完全通过网络浏览器添加和修改条目。该程序在 Ubuntu 软件仓库中作为 `phpldapadmin` 提供。

启动、停止或重启 `slapd` 守护进程的方法与系统守护进程通常相同（对于尚未编写 Upstart 方法的）：

```
sudo /etc/init.d/slapd start/stop/restart
```
