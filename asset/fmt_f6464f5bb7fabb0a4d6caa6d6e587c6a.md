
## 附录 A：命令

# ZMAN 命令摘要（续）

|  | --weekly=<MWF> | 指定执行操作的星期几。如果指定，操作将每七天重复一次。示例：`"MWF"` 表示在周一、周三和周五执行操作。周一 = `M`，周二 = `TU`，周三 = `W`，周四 = `TH`，周五 = `F`，周六 = `SA`，周日 = `SU`。 |
|  | --monthly=<DD> | 指定执行操作的每月几几。如果指定，操作将每月重复一次。不能指定多个日期。 |
|  | --yearly=<MM-DD, MM-DD,...> | 指定执行操作的每年哪些日期。如果指定，操作将每年重复一次。日期格式为 `"MM-DD"`。多个日期之间可用逗号分隔。 |

| 命令 | 用法/选项 | get |
|---|---|---|
|  | --repeat=<DD:HH:MM> | 指定操作的重复频率，格式为 `"DD:HH:MM"`。天数可选。 |
|  | --gmt | 所有给定的时间均视为 GMT。如果未给出，所有时间均视为目录移除包 (`crb`)。 移除包（bundle）与目录（catalog）之间的关联。 |
| `server-remove-bundle` (`srb`) | `zman server-remove-bundle <options><Server>` | 设备与一个或多个包之间的关联。 |
| `server-list-catalogs` (`slc`) | `zman server-list-catalogs <options><Server>` | 列出设备关联的目录。 |
| `server-add-catalog` (`sac`) | `zman server-add-catalog <options><Server><catalog>` | 将一个或多个目录与设备关联。 |
|  | --time=<HH:MM> | 指定执行操作的每日时间。时间格式为 `"HH:MM"`，采用 24 小时制。 |
|  | --date=<YYYY-MM-DD> | 指定执行操作的特定日期。格式为 `"YYYY-MM-DD"`。 |
|  | --now | 指定尽快执行该操作。可以指定重复频率。如果未指定计划，则默认为现在。 |
|  | --relative=<DD:HH:MM> | 指定在相对于当前的一个时间执行操作。时间格式为 `"DD:HH:MM"`。可以指定重复频率。 |

# ZMAN 命令摘要（续）

| 命令 | 用法/选项 | get |
|---|---|---|
| `server-remove-catalog` (`src`) | `zlman server-remove-catalog <options> <Server>` | 移除设备与多个目录之间的关联。 |
| `server-list-policies` (`slp`) | `zlman server-list-policies <options> <Server>` | 列出设备关联的策略。 |

## 附录 A：命令

# ZMAN 命令摘要（续）

| 命令 | 用法/选项 | get |
|---|---|---|
| `server-add-policy` (`sap`) | `zlman server-add-policy <options> <Server> <policy> --time=<HH:MM>` | 将一个或多个策略与设备关联。 |

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 描述 |
| --- | --- | --- |
| `ruleset-remove-rule` (`rsrr`) | `zlman ruleset-remove-rule <options> <Name or Position> <Rule Position>` | 从规则集中删除一条规则。 |
| `ruleset-add-workstation-group` (`rsaw`) | `zlman ruleset-add-workstation-group <options> <Name or Position> <group>` | 为通过特定规则集导入的对象添加服务器组成员。 |
| `ruleset-add-server-group` (`rsas`) | `zlman ruleset-add-server-group <options> <Name or Position> <group>` | 为通过特定规则集导入的对象添加工作站组成员。 |
| `ruleset-remove-workstation-group` (`rrsw`) | `zlman ruleset-remove-workstation-group <options> <Name or Position> <group>` | 从规则集中删除工作站组成员关系。 |
| `ruleset-remove-server-group` (`rsrs`) | `zlman ruleset-remove-server-group <options> <Name or Position> <group>` | 从规则集中删除服务器组成员关系。 |
| `license-info` (`li`) | `zlman license-info <options>` | 显示许可信息。 |
| `license-activate` | `zlman license-activate <options> <key>` | 激活您的系统。 |
| `license-set-seats` (`lss`) | `zlman license-set-seats <options> <count>` | 设置允许的活动设备数量。 |
| `target-list` (`tl`) | `zlman target-list <options> -r,--recursive -f,--filter=<filter>` | 显示所有 OS 目标列表。包含子文件夹中的对象。仅显示匹配指定过滤的对象（如果过滤器过滤，可以使用通配符 `*` 和 `?`）。 |
| `target-create` (`tc`) | `zlman target-create <options> <arch> <Package Manager> <Primary Role> <Product Name> <Vendor> <Version> <Detect String>` | 创建一个新的 OS 目标。 |

## 附录 A：命令

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 描述 |
|---|---|---|
| `target-info` (`ti`) | `zlman target-info <options> <target>` | 显示 OS 目标的详细信息。 |
| `target-update` (`tu`) | `zlman target-update <options> <target>` | 修改用户创建的 OS 目标的值。 |
|  | --arch=<arch> | 指定新的架构值。 |
|  | --pkgmgr=<Package Manager> | 指定新的包管理器。 |
|  | --enable | 启用禁用的 OS 目标。 |
|  | --disable | 禁用启用的 OS 目标。 |
|  | --role=<Primary Role> | 指定主角色。 |
|  | --product=<Product Name> | 指定产品名称。 |
|  | --vendor=<Vendor> | 指定供应商。 |
|  | --detect=<Detect String> | 指定 检测字符串。 |
|  | --version=<Version> | 指定新版本。 |
| `target-delete` (`td`) | `zlman target-delete <options> <target>` | 删除用户创建的 OS 目标。 |
| `queue-list` (`ql`) | `zlman queue-list <options> <status>` | 列出所有队列条目 |
|  | -r, --recursive | 包含子文件夹中的对象。 |
|  | -f, --filter=<filter> | 仅显示匹配过滤器的（如果过滤器过滤，可以使用通配符 `*` 和 `?`）。 |
| `queue-reset` (`qr`) | `zlman queue-reset <options> <status>` | 重置队列。 |
| `queue-flush` (`qf`) | `zlman queue-flush <options> <status>` | 刷新队列。 |
| `hotlist` | `zlman hotlist <options>` | 显示带有警告或错误的列表。 |
| `policy-list` (`pl`) | `zlman policy-list <options> <folder>` | 列出文件夹中的策略。 |
|  | -r, --recursive | 包含子文件夹中的对象。 |

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 描述 |
| --- | --- | --- |
| -f, --filter=<filter> | 仅显示匹配过滤器的（如果过滤器过滤，可以使用通配符 `*` 和 `?`）。 |
