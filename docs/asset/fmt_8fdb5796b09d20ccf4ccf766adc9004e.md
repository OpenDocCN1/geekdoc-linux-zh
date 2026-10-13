
```
rolemed -A
solaris.admin.usermgr.pswd,solaris.admin.system.shutdown, \
solaris.admin.fsmgr.write,solaris.admin.logsvc.purge \
adminus
```

# 第 20 章 基于角色的访问控制 (RBAC) 737

如果您想删除一个角色账户，请如下所示使用 `roleled` 命令：

```
roleled [-r] <role account name>
```

`-r` 选项从系统中删除该角色的主目录。例如，要删除 `admin` 角色账户，请执行以下命令：

```
roleled -r admin
```

> `roleled` 命令不会增加现有的权限；它会替换任何现有的权限设置。

下一节将详细讨论每个 RBAC 数据库，并描述在执行 `roleadd` 和 `usermod` 命令时创建的条目。

# RBAC 组件

RBAC 依赖于以下四个数据库为用户提供访问特权操作的能力：

* `user_attr`（扩展用户属性数据库）。将用户和角色与权限及配置关联起来。
* `auth_attr`（权限属性数据库）。定义权限及其属性，并识别相关的帮助文件。
* `prof_attr`（配置属性数据库）。定义配置，列出配置分配的权限，并识别相关的帮助文件。
* `exec_attr`（配置属性数据库）。定义分配给配置的特权操作。

这四个数据库之间相互作用。

# 扩展用户属性 (user_attr)

`/etc/user_attr` 数据库补充了 `passwd` 和 `shadow` 数据库。它包含了扩展的用户属性，例如权限和配置。它还允许将分配给用户。以下是 `/etc/user_attr` 数据库的副本：

```
# /etc/user_attr
# Copyright (c) 1999 by Sun Microsystems, Inc. All rights reserved.
#:::
# /etc/user_attr:::
#:::
# user attributes. see user_attr(4)::::
#:::
#pragma ident "@(#)user_attr 1.2 99/07/14 SMI"::::
#:::
root:::type=normal;auth=solaris.*,solaris.grant;profiles=All
admin:::type=role;auth=solaris.admin.usermgr,passwd/
solaris.system:::type=normal;solaris.admin.fsmgr.write;profiles=All
eil:::type=normal;roles=adminusr
```

`user_attr` 数据库中的以下字段用冒号分隔：

```
user:qualifier:res1:res2:attr
```

表 20.3 描述了。TABLE 20.3 USER_ATTR FIELDS

| 字段名 | 描述 |
| --- | --- |
| user | `passwd` 数据库中的用户名称。 |
| qualifier | 预留用。 |
| res1 | 预留用。 |
| res2 | 预留用。 |
| attr | 包含了应用于命令的键值对。四个有效的键：`auths`, `roles` 和 `type`。 |

# 第 20 章 基于角色的访问控制 (RBAC) 739

| 字段名 | 描述 |
| --- | --- |
| auths | 从 `auth_attr` 数据库中选择的逗号分隔的权限名称。权限名称可以包含星号 (`*`) 作为通配符。例如，`solaris.*` 意味着所有的设备。 |
| profiles | 从 `prof_attr` 中选择的逗号分隔的配置名称。决定了用户以哪些属性执行命令。配置的顺序很重要；类似于 Solaris 路径。我们将在“权限 (`auth_attr`)”节中进一步描述配置。 |
| roles | 可以使用逗号分隔的角色名称分配给用户。注意角色是在 `_attr` 数据库中定义的。 |
| type | 如果此账户是普通用户，则设置为 `normal`；如果是角色，则设置为 `role`。 |

在前节中，我执行如下 `roleadd` 命令添加了一个名为 `adminus` 的角色：

```
roleadd -m -d /export/home/adminus -c "Admin Assistant" \
-A solaris.admin.usermgr.pswd,solaris.admin.system.shutdown,
solaris.admin.fsmgr.write
```

`roleadd` 命令在 `user_attr` 数据库中创建了以下条目：

```
adminus:::type=role;auths=solaris.admin.usermgr.pswd,solaris.system.shutdown,solaris.admin.fsmgr.write;profiles=All
```

我执行了以下命令将角色分配给用户 `neil`：

```
usermod -R neil
```

并在 `user_attr` 数据库中创建了以下条目：

```
neil:::type=normal;roles=adminus
```

# 权限 (auth_attr) 数据库

权限是授予访问受限功能的权利。在前节中，系统管理员想将某些管理任务委托给 Neil。将权限分配给名为 `adminus` 的角色实现了这一点。权限是一个唯一的字符串，标识被授权的内容以及创建权限的人。记住我们使用了以下权限赋予 Neil 修改用户密码、关闭系统和挂载共享文件系统的能力：

```
solaris.admin.usermgr.pswd
solaris.system.shutdown
solaris.admin.fsmgr.write
```

某些特权程序检查权限以确定用户是否可以执行功能。例如，`solaris.jobs.admin` 权限允许用户编辑另一个用户的 `crontab`。

所有权限都存储在 `auth_attr` 数据库中。如果没有使用命名服务，数据库位于文件 `/etc/security/auth_attr`。权限也可以直接分配给用户（或角色），在这种情况下，它们被输入到 `user_attr` 数据库中。权限也可以分配给配置，配置再分配给用户。我们将在“权利配置 (`prof_attr`)”节中描述它们。

## 第 20 章 基于角色的访问控制 (RBAC) 741

## 表 20.4

## AUTH_ATTR 字段

| 字段名称 | 描述 |
| --- | --- |
| autname | 一个唯一的字符字符串，格式为 `prefix:[suffix]`，用于标识授权。Solaris 操作环境的授权使用 `solaris` 作为前缀。所有其他授权应使用以创建该授权的组织的反向互联网域名开头的前缀（例如 `com.xyzcompany`）。后缀表示被授权的内容，通常是功能区域和操作。当不存在后缀时（即 `autname` 由前缀和功能区域组成并以句号结尾），`autname` 作为应用程序在其 GUI 中使用的标题，而不是授权。`autname` `solaris.prim` 是标题的一个示例。当 `autname` 以单词 `grant` 结尾时，该 `autname` 授权授权允许用户将相关授权（即具有相同前缀和功能区域的授权）委托给其他用户。`autname` `solaris.primgr.grant` 是授权授权的一个示例；它赋予用户将此类 `solaris.primgr.admin` 和 `solaris.primgr.nobanner` 等授权委托给其他用户的权利。 |
| res1 | 留用字段。 |
| res1 | 留用字段。 |
| short_desc | 授权的短名称，适用于显示在用户界面中，例如 GUI 中的滚动列表。 |
| long_desc | 描述说明了授权的用途、使用的应用程序以及对该授权感兴趣的用户类型。长描述可以显示在应用程序的帮助文本中。 |
| attr | 一个可选列表，由分号（;)隔隔的键值对组成，描述授权的属性。可以指定零或多个键。 |

关键字 `help` 标识一个 HTML 帮助文件。可以从 `/usr/lib/help/auths/locale/C/` 目录下的 `index.html` 文件访问帮助文件。

## 742 第二部分 第二部分

以下是可以在默认 `auth_attr` 数据库中找到的一些典型值：

```
solaris.admin.usermgr.pswd::=Change User Passwords::UserMgrPswd.html
solaris.system.shutdown::=Shutdown the System::help=SysShutdown.html
solaris.admin.fsngr::=Mount/Share File Systems::help=FsmgrWrite.html
```

观察 `auth_attr` 数据库和 `user_attr` 数据库之间的关系，这种方式变得清晰了：
