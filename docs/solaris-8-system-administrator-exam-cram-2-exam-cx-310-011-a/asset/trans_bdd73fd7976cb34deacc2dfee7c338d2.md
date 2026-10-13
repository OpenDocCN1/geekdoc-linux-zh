

## 执行属性数据库（exec_attr）

/etc/security/exec_attr 文件用于将特权操作（以指定 UID 和/或 GID 执行的命令）与配置文件相关联。然后您可以将这些配置文件分配给用户帐户或角色。表 17.6 列出了 exec_attr 文件的冒号分隔字段。

**表 17.6 执行属性数据库的字段**

| 字段 | 用途 |
|---|---|
| **名称** | 关联配置文件的名称（必须与 prof_attr 文件条目中的配置文件名称完全匹配）。 |
| **策略** | 安全策略。目前，超级用户策略 **suser** 是唯一有效的条目。 |
| **类型** | 实体类型。目前，命令类型 **cmd** 是唯一有效的条目。 |
| **保留1** | 保留供将来使用（空字段）。 |
| **保留2** | 保留供将来使用（空字段）。 |
| **ID** | 要执行的命令（使用完整路径名或带有元字符的部分路径指定）。 |
| **属性** | 由 key=value 对组成的列表（以分号分隔），用于确定执行期间应用于命令的属性。有效键为 **euid**（设置有效 UID）、**uid**（设置真实 UID）、**egid**（设置有效 GID）和 **gid**（设置真实 GID）。有效值为 UID、用户帐户名、GID 和组帐户名。 |

以下示例显示了与打印机管理配置文件关联的 /etc/security/exec_attr 文件中的两个条目。

```
Printer Management:suser:cmd:::/usr/bin/enable:euid=lp
Printer Management:suser:cmd:::/usr/bin/disable:euid=lp
```

第一个条目将 enable(1) 命令的执行定义为特权操作。该命令将以有效 UID 为 lp 的身份执行。第二个条目将 disable(1) 命令的执行定义为特权操作。该命令同样将以有效 UID 为 lp 的身份执行。

表 17.7 列出了 exec_attr 文件定义的默认特权操作。所有条目的 **策略** 字段均设置为 **suser**，**类型** 字段均设置为 **cmd**。

| 配置文件名称 | 命令 | 属性 |
|---|---|---|
| All | * | |
| Audit Control | /etc/init.d/audit | euid=0;egid=3 |
| Audit Control | /etc/security/bsmconv | uid=0 |
| Audit Control | /etc/security/bsmunconv | uid=0 |
| Audit Control | /usr/sbin/audit | euid=0 |
| Audit Control | /usr/sbin/auditconfig | euid=0 |
| Audit Control | /usr/sbin/auditd | uid=0 |
| Audit Review | /usr/sbin/auditreduce | euid=0 |
| Audit Review | /usr/sbin/praudit | euid=0 |
| Audit Review | /usr/sbin/auditstat | euid=0 |
| Printer Management | /etc/init.d/lp | euid=0 |
| Printer Management | /usr/bin/cancel | euid=0 |
| Printer Management | /usr/bin/lpstat | egid=14 |
| Printer Management | /usr/bin/enable | euid=lp |
| Printer Management | /usr/bin/disable | euid=lp |
| Printer Management | /usr/sbin/accept | euid=lp |
| Printer Management | /usr/sbin/reject | euid=lp |
| Printer Management | /usr/sbin/lpadmin | egid=14 |
| Printer Management | /usr/sbin/lpfilter | euid=lp |
| Printer Management | /usr/sbin/lpforms | euid=lp |
| Printer Management | /usr/sbin/lpmove | euid=lp |
| Printer Management | /usr/sbin/lpshut | euid=lp |
| Printer Management | /usr/sbin/lpusers | euid=lp |

![](img/b957f979417d9f16274c2eb52c8f2c9f_380_0.png)

请熟悉所有四个 RBAC 数据库文件的格式以及每个字段的用途。

## 管理 RBAC

您可以使用以下命令来管理 RBAC：

- **auths(1)** — 显示分配给用户帐户的授权
- **profiles(1)** — 显示分配给用户帐户的配置文件
- **roles(1)** — 显示分配给用户帐户的角色
- **roleadd(1M)** — 添加角色定义
- **roledel(1M)** — 删除角色定义
- **rolemod(1M)** — 修改角色定义

### 显示 RBAC 分配

如果您使用 auths、profiles 和 roles 命令时不带命令行参数，则会列出分配给当前用户帐户的授权、配置文件和角色。要列出分配给其他用户帐户的授权、配置文件和角色，请将用户帐户指定为命令行参数，如下例所示：

```sh
$ auths root
solaris.*,solaris.grant

$ profiles root
All

$ roles root
roles: root : No roles
$
```

### 角色管理

roleadd、rolemod 和 roledel 命令用于管理 RBAC 角色。

#### 使用 roleadd 命令创建角色

roleadd(1M) 命令提供了一种快速添加新角色的方法。至少必须将角色名称指定为命令行参数。表 17.8 列出了 roleadd 命令支持的命令行参数。

![](img/b957f979417d9f16274c2eb52c8f2c9f_381_0.png)

> roleadd 命令支持与 useradd 命令完全相同的命令行参数，但 roleadd 不支持 -R 命令行参数，因为角色不能包含其他角色。

**表 17.8 roleadd 命令的命令行参数**

| 参数 | 说明 |
|---|---|
| *role* | 指定新角色的名称（必填）。 |
| **-A authorizations** | 指定一个或多个授权（以逗号分隔）。 |
| **-b base** | 定义基本目录。如果未指定主目录（**-d**），则会将角色名称添加到 *base* 中并用作主目录。 |
| **-c comment** | 指定放置在 `/etc/passwd` 文件的注释（**gcos**）字段中的注释。 |
| **-d directory** | 定义角色的主目录。 |
| **-e date** | 指定角色的过期日期。在指定日期之后，该角色将被禁用。 |
| **-f days** | 指定角色在被禁用之前可以处于非活动状态的最大天数。 |
| **-g group** | 定义将成为角色主组的现有组的 GID 或名称。 |
| **-G group** | 定义将成为角色辅助组的现有组的 GID 或名称。 |
| **-k template_dir** | 指定包含用于用户配置文件的模板（默认）`.profile` 的目录。 |
| **-m** | 如果主目录不存在，则创建该主目录。主目录由 **-b** 和角色名称或 **-d** 定义。 |
| **-o** | 允许指定现有 UID——即允许使用重复的 UID 创建角色（参见 **-u**）。 |
| **-p profiles** | 指定一个或多个执行配置文件（以逗号分隔）。 |
| **-s shell** | 指定登录 shell；默认为 Bourne shell（`/bin/sh`）。 |
| **-u uid** | 指定角色的 UID。它必须是十进制整数。如果未指定，则分配下一个可用的最高 UID。 |

以下示例使用 **roleadd** 命令创建一个角色：

```
# roleadd -A solaris.system.date -P "Printer Management" prt_adm
#
```

此命令创建 prt_adm 角色。它将 solaris.system.date 授权和 Printer Management 配置文件分配给该角色。

为方便起见，**roleadd** 命令还支持 **-D** 命令行参数，该参数允许为授权（**-A**）、基本目录（**-b**）、组（**-g**）、过期日期（**-e**）、最大非活动天数（**-f**）和执行配置文件（**-P**）分配默认值。后续使用 **roleadd** 命令时，如果未指定这些值，将使用这些默认值。

![](img/b957f979417d9f16274c2eb52c8f2c9f_383_0.png)

> 使用 **roleadd** 命令创建的角色没有密码。这些角色处于锁定状态，无法使用，直到通过 **passwd(1)** 命令为该角色定义密码。

#### 使用 rolemod 命令修改角色

**rolemod**(1M) 命令用于修改现有角色。其命令行参数与 **roleadd** 命令的参数相同，但以下情况除外：

- 基本目录（**-b**）不可用。请使用 **-d** 指定新目录。如果主目录不存在，请不要忘记包含 **-m**。
- 设置默认值（**-D**）不可用。
- 模板目录（**-k**）不可用。
- 如果角色名称被修改，则使用 **-l role** 指定新的角色名称。

请记住，如果角色被更改，主目录的名称不会更改，除非使用了 **-d** 和 **-m** 命令行参数。

#### 使用 roledel 命令删除角色

**roledel**(1M) 命令用于删除角色。不仅会从 user_attr 文件中删除角色定义，其他 user_attr 条目中的所有角色分配也会被修改。角色被指定为命令行参数。仅支持另一个命令行参数：**-r** 用于删除与该角色关联的主目录。

