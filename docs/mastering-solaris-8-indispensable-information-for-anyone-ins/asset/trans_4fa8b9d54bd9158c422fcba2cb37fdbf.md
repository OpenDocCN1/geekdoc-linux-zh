

# 图 11.24

*组属性* 对话框

![](img/256e02a6afce528d264a8d911fa0ff20_487_0.png)

## 删除组账户

您还可以使用 AdminSuite 删除组账户。请按照以下步骤操作：

- 1. 在“组”窗口中，单击您要删除的组账户。
- 2. 从“操作”菜单中选择“删除”命令。将出现如下图形所示的警告对话框。

![](img/256e02a6afce528d264a8d911fa0ff20_487_1.png)

- 3. 单击“删除”按钮以确认删除操作。
- 4. Solaris 将从组目录服务数据库中的所有条目中删除该组账户。任何将该组指定为主组的用户，其主组指定都将更改为 STAFF 组。

# 管理角色

Solaris 8 增加了基于角色的访问控制（RBAC）功能，允许您为用户账户分配一部分超级用户权限，用于特殊目的。这使得管理员能够将一些通常只有管理员才能执行的系统职责，通过必要的工具，下放给特定类型的用户或用户组。为用户账户创建授权的最简单方法是在 AdminSuite 3 中操作，它允许访问存储角色信息的两个特殊数据库：`auth_attr` 和 `user_attr` 数据库。授权与角色是分开的，但角色会被分配授权或访问权限。

您可以将角色视为用于执行管理任务的特殊用户账户。您不能直接使用角色登录；当您在命令行输入切换用户命令 `su RoleName` 时，您将获得访问该角色的权利和权限。角色账户允许用户针对某些命令获取 root UID，具体由该角色的定义决定。

在 AdminSuite 的认证配置中，您可以创建允许用户执行通常需要 root 访问权限的操作的角色。您通过创建起始设置为 `solaris.admin` 的角色来实现这一点。角色的真正价值在于，它们允许用户在 AdminTool 和 AdminSuite 3 中执行任务，如果没有被授予 root 权限，这些任务将很难甚至无法完成。例如，一旦分配了角色，某个组的 IT 管理员就可以为该组创建和修改用户及组，而这种情况以前需要赋予该组 IT 管理员 root 权限。

通过 RBAC，您可以授予用户和组以下权限：

- 对超级用户功能的访问权限
- 执行配置文件，其中可以将访问权限和命令进行分组，供指定的 UID 和 GID 使用
- 角色，这是一种可以假设以执行特定任务的特殊用户账户

## 角色数据库

以下各节描述了存储被授予超级用户权限的用户访问权限的四个 RBAC 数据库。

## /etc/user_attr

扩展用户属性数据库将用户及其角色与其访问和执行配置文件关联起来。图 11.25 显示了默认的 `user_attr` 文件。

# 图 11.25

![](img/256e02a6afce528d264a8d911fa0ff20_489_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_489_1.png)

请注意，`user_attr` 文件中有五个字段；它们的格式为 username:qualifier:reserved1:reserved2:attribute list。（若要在此文件中续行，请使用反斜杠符号）。术语 qualifier、reserved1 和 reserved2 目前尚未分配；它们是预留给 Sun 随着 `user_attr` 文件的进一步开发而未来使用的。重要的变量是属性列表，它是一个由分号分隔的键值对列表，当对象执行时应用安全级别。

使用的四个键值对为：auths（授权列表，逗号分隔的授权对象名称列表，如 solaris、printer，表示可以访问的对象）；profiles（配置文件列表，逗号分隔的 `prof_attr` 文件中的配置文件名称列表，用户可使用这些配置文件执行命令）；roles（角色，可选的逗号分隔的角色列表，取自将 type 字段设置为 role 的用户账户数据库）；以及最后的 type，对于普通用户为 normal，对于角色为 role，表明此账户用于角色。

配置文件 A11 是分配给用户账户的最低级别，表明用户可以发出所有命令，但不进行额外分配。例如，`user_attr` 文件中的条目可能如下所示：

```
root:::type=normal;auths=solaris.*,solaris.grant;profiles=A11
```

当分配了角色后，此条目将变更为如下形式：

```
sysadmin:::type=role;profile=Device Management,
Machine Administration,User Groups & Mailing Lists,All
sosinsky:::type=normal,auths=solaris,system.date;
roles=sysadmin;profiles=A11.
```

您可以将 `user_attr` 数据库视为 `passwd` 和 `shadow` 文件的附属数据库。在该数据库文件中存储了扩展用户属性，指向授权或访问权限以及执行配置文件。在分配角色时，只需要 `user_attr` 文件，您可以在此数据库中分配权限和角色，无需考虑其他安全因素。

## /etc/security/auth_attr

授权属性数据库存储用户和组对受限功能的访问权限，并将这些权限链接到相应的帮助文件。授权可以直接分配，或分配给执行配置文件，而执行配置文件再分配给用户。此数据库包含授权列表以及每个授权的创建者；每个集合由唯一的字符串标识。程序使用 `auth_attr` 数据库来确定用户是否具有执行操作所需的授权。例如，为了让用户能够修改另一个用户的 crontab 文件，`solaris.jobs.admin` 授权会在 `auth_attr` 数据库中检查此权限。图 11.26 显示了 `/etc/security/auth_attr` 文件的默认状态。

![](img/256e02a6afce528d264a8d911fa0ff20_490_0.png)

在系统中添加 AdminSuite 会通过向 auth_attr 数据库文件添加许多管理授权来修改该文件。您在图 11.26 中看到的六个字段条目格式为 authname: reserved1: reserved2: short_description: long_description:attribute list（若要在此文件中续行，请使用反斜杠符号）。

术语 reserved1 和 reserved2 目前尚未分配；它们是预留给 Sun 随着 auth_attr 文件的进一步开发而未来使用的。short_description 字段用于存储在图形用户界面中显示的名称，而 long_description 提供对授权的描述、该授权适用的应用程序以及可能使用该授权的用户类型。这里的重要变量（如前所述）是属性列表，它是一个由分号分隔的键值对列表，当对象执行时应用安全级别。

authname 字段以 `<prefix.authname>` 格式存储认证名称，作为由分号分隔的列表。所有 Solaris 授权都使用 Solaris 作为前缀，并分配诸如 `admin.usermgr.pswd` 的后缀来指定授权的功能和操作。任何非 Solaris 特有的授权都按 Internet 顺序反转给出，因此前缀形式为 `com.somisky-group`。当 `<authname>` 不使用后缀且名称以句点结尾时，如 `admin.usermgr.`，该授权允许以图形形式使用应用程序，让用户访问用户账户管理器。如果 `<authname>` 以 `grant` 结尾，则表明已获得该授权的用户可以使用该服务，并可以将该授权授予其他用户。因此，拥有 `solaris.usermgr.grant` 授权的用户可以将 `solaris.usermgr.admin` 分配给其他用户。您可以通过用 Web 浏览器打开 `/usr/lib/help/auths/local/C/index.html` 文件来获取任何关键字的帮助。

例如，auth_attr 文件中的条目可能如下所示：

```
solaris.admin.usermgr:::Users, Groups & Mailing Lists::help=UserMgrHeader.html
```

当分配了授权后，您将看到以下内容：

```
sosinsky:::::type=normal, auths=solaris.usermgr;
roles=sysadmin;profiles=All
```

## /etc/security/prof_attr

配置文件执行属性数据库存储标识用户或组拥有哪些访问权限的配置文件定义。它还提供了相应的帮助文件。配置文件通过真实或会话 UID 或 GID 分配给用户或角色，最常见的分配是将 UID 分配给 root。程序使用系统中的 prof_attr 文件来检查本地执行配置文件。图 11.27 显示了 prof_attr 文件的默认状态。

