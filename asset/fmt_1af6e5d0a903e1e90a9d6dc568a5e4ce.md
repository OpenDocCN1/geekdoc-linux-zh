
| Attributes | `key=value` 对的列表（以分号分隔），用于确定配置文件中包含的授权和操作。有效的键为 `auth` 和 `help`。 |

以下示例显示了 `/etc/security/prof_attr` 文件中的两个条目。为了改善可读性，这些行被断开并换行。

```
Audit Review::View the audit trail:auths=solaris.audit.read;
    help=AuditReview.html
Printer Management::Control Access to Printer:
    help=PrinterMgmt.html
```

第一个条目定义了 Audit Review 配置文件。短语“View the audit trail”（查看审计跟踪）虽然略显简洁，但描述准确。`Attributes` 字段引用了 `solaris.audit.read` 授权，并标识了帮助文件（位于 `/usr/lib/help/profiles/locale/C` 目录下）。`exec_attr` 文件中标识为与 Audit Review 配置文件关联的任何特权操作也都会被允许。

第二个条目定义了 Printer Management 配置文件。`Attributes` 字段中仅标识了帮助文件。但是，该配置文件允许 `exec_attr` 文件中与 Printer Management 关联的任何操作。表 17.3 列出了由 `prof_attr` 文件定义的默认配置文件。请注意，Device Management 配置文件的 `Attributes` 字段使用了短语 `solaris.device.*`；此元字符表达式表示包含所有 `solaris.device` 授权。

### 表 17.3 默认 RBAC 配置文件

| 名称 | 描述 | 授权 | 帮助 |
| --- | --- | --- | --- |
| All | 标准 Solaris | N/A | All.html |
| Audit Control | 管理审计子系统 | `solaris.audit.config`, `solaris.jobs.admin` | AuditControl.html |
| Audit Review | 查看审计跟踪 | `solaris.audit.read` | AuditReview.html |
| Device Management | 控制对可移动介质的访问 | `solaris.device.*` | DevMgmt.html |
| Printer Management | 控制对打印机的访问 | N/A | PrinterMgmt.html |

## 授权属性数据库 (auth_attr)

`/etc/security/auth_attr` 文件用于定义可以按单个用户帐户授予的授权（使用受限函数的权利）。然后，您可以在 `user_attr` 文件中引用这些授权，以将其分配给角色或直接分配给用户帐户。表 17.4 列出了 `auth_attr` 文件的冒号分隔字段。

以下示例显示了 `/etc/security/auth_attr` 文件中的三个条目：

```
solaris.grant:::Grant All Rights::help=PriAdmin.html
solaris.audit:::Audit Management::help=AuditHeader.html
solaris.audit.config:::Configure Auditing::help=AuditConfig.html
```

### 表 17.4 授权属性数据库的字段

| 字段 | 用途 |
| --- | --- |
| Name | 授权的名称，由一个或多个以句点分隔的关键字组成，用于标识系统、子系统和功能。如果名称以句点结尾，则此条目只是一个描述一组相关授权的标题。 |
| Res1 | 保留供将来使用（空字段）。 |
| Res2 | 保留供将来使用（空字段）。 |
| Short Description | 授权的简短描述。 |
| Long Description | 授权的详细描述。 |
| Attributes | 零个或多个 `key=value` 对的列表（以分号分隔），用于描述授权。目前，唯一有效的键是 `help`；它定义与该授权关联的帮助文件。 |

第一个条目定义了 `solaris.grant` 授权。`Short Description` 字段将此授权标识为 Grant All Rights（授予所有权限）。`Attributes` 字段标识了帮助文件（位于 `/usr/lib/help/auths/locale/C` 目录下）。

第二个条目为审计管理授权集定义了 `Short Description` 字段。（请注意 `Name` 字段末尾的句点。）第三个条目定义了 `solaris.audit.config` 授权，该授权允许配置系统审计。（帮助文件定义为 `AuditConfig.html`。）

表 17.5 列出了由 `auth_attr` 文件定义的默认授权。

### 表 17.5 默认 RBAC 授权

| 名称 | 描述 | 帮助 |
| --- | --- | --- |
| All | 标准 Solaris | All.html |
| `solaris.*` | 主要管理员 | PriAdmin.html |
| `solaris.grant` | 授予所有权限 | PriAdmin.html |
| `solaris.audit.config` | 配置审计 | AuditConfig.html |
| `solaris.audit.read` | 读取审计跟踪 | AuditRead.html |
| `solaris.device.allocate` | 分配设备 | DevAllocate.html |
| `solaris.device.config` | 配置设备属性 | DevConfig.html |
| `solaris.device.grant` | 委派设备管理 | DevGrant.html |
| `solaris.device.revoke` | 撤销或收回设备 | DevRevoke.html |
| `solaris.jobs.admin` | `cron` 和 `at` 管理 | JobsAdmin.html |
| `solaris.jobs.grant` | 委派 `cron` 和 `at` 管理 | JobsGrant.html |
| `solaris.jobs.user` | 创建 `cron` 或 `at` 作业 | JobsUser.html |
| `solaris.login.enable` | 启用登录 | LoginEnable.html |
| `solaris.login.remote` | 远程登录 | LoginRemote.html |
| `solaris.pfmgmr.assign` | 将配置文件分配给用户或角色 | ProfmgrAssign.html |
| `solaris.pfmgmr.write` | 创建、修改和删除配置文件 | ProfmgrWrite.html |
| `solaris.role.assign` | 将角色分配给用户 | RoleAssign.html |
| `solaris.role.write` | 添加、修改和删除角色 | RoleWrite.html |
| `solaris.system` | 机器管理 | SysHeader.html |
| `solaris.system.date` | 设置日期和时间 | SysDate.html |
| `solaris.system.shutdown` | 关闭系统 | SysShutdown.html |

请注意，所有这些授权都是针对 Solaris 系统（由 Sun Microsystems 开发）的。如果其他组织添加了新的授权，则应使用创建该授权的组织的反向 Internet 域名来标识。例如，由 `unixcert.net` 组织创建的授权将以 `net.unixcert` 前缀开头。

## 执行属性数据库（exec_attr）

`/etc/security/exec_attr` 文件用于将特权操作（以指定 UID 和/或 GID 执行的命令）与配置文件相关联。然后您可以将这些配置文件分配给用户帐户或角色。表 17.6 列出了 `exec_attr` 文件的冒号分隔字段。

### 表 17.6 执行属性数据库的字段

| 字段 | 用途 |
|---|---|
| `名称` | 关联配置文件的名称（必须与 `prof_attr` 文件条目中的配置文件名称完全匹配）。 |
| `策略` | 安全策略。目前，超级用户策略 `suser` 是唯一有效的条目。 |
| `类型` | 实体类型。目前，命令类型 `cmd` 是唯一有效的条目。 |
| `保留1` | 保留供将来使用（空字段）。 |
| `保留2` | 保留供将来使用（空字段）。 |
