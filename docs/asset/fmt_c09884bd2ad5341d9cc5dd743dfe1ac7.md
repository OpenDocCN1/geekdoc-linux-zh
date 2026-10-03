
| -o | 允许指定现有 UID。即允许使用重复的 UID 创建角色（见 -u）。 |

表 17.8: roleadd 命令的命令行参数。

| 参数 | 描述 |
| --- | --- |
| -p profiles | 指定一个或多个执行配置文件（用逗号分隔）。 |
| -s shell | 指定登录 shell；默认是 Bourne shell (`/bin/sh`)。 |
| -u uid | 指定角色的 UID。必须是十进制整数。如果没有，则分配下一个可用的 UID。 |

## 考试提示

`roleadd` 支持的命令行参数与 `useradd` 相同，但 `roleadd` 不支持 `-R` 命令行参数，因为角色不能包含其他角色。

以下示例使用 `roleadd` 命令创建一个角色：

```bash
$ roleadd -A solaris.*,solaris.grant -p root root
```

表 17.7 列出了 `exec_attr` 文件定义的默认特权操作。所有操作的 `Policy` 字段均设置为 `suser`，且 `Type` 字段均设置为 `cmd`。

## 考试提示

`roleadd` 支持的命令行参数与 `useradd` 相同，但 `roleadd` 不支持 `-R` 命令行参数，因为角色不能包含其他角色。

以下示例使用 `roleadd` 命令创建一个角色：

```bash
$ roleadd -A solaris.*,solaris.grant -p root root
```

## 修改角色

`rolemod(1)` 命令修改现有角色。

## 删除角色

`roledel(1)` 命令删除角色定义。

## 考试提示

`roleadd` 支持的命令行参数与 `useradd` 相同，但 `roleadd` 不支持 `-R` 命令行参数，因为角色不能包含其他角色。

以下示例使用 `roleadd` 命令创建一个角色：

```bash
$ roleadd -A solaris.*,solaris.grant -p root root
```

## 考试提示

熟悉所有四个 RBAC 数据库文件的格式以及字段的作用。

## 显示 RBAC 分配

如果你在不带命令行参数的情况下使用 `auth`、`profiles` 和 `roles` 命令，将列出分配给当前用户账户的权限、配置文件和角色。要列出分配给另一个用户账户的权限、配置文件和角色，请将用户账户作为命令行参数。例如：

```bash
$ auth root
$ profiles root
$ roles root
roles: No roles$
```

## 角色管理

`roleadd`、`rolemod` 和 `roledel` 命令用于管理 RBAC 角色。

## 使用 roleadd 命令创建角色

`roleadd(1)` 命令提供了一种添加新角色的快速方法。至少必须作为命令行参数指定角色的名称。表 17.8 列出了 `roleadd` 支持的命令行参数。

表 17.8: roleadd 的命令行参数。

| 参数 | 描述 |
| --- | --- |
| role | 指定新角色的名称（必选）。 |
| -A authorizations | 指定一个或多个权限（用逗号分隔）。 |
| -b base | 定义基目录。如果没有指定主目录 (-d)，则将角色名称添加到 `base` 中并用作主目录。 |
| -c comment | 指定要放置在 `/etc/passwd` 文件注释 (ECO) 字段中的注释。 |
| -d directory | 定义角色的主目录。 |
| -e date | 指定角色的过期日期。在指定日期之后，该角色将被禁用。 |
| -f days | 指定角色在禁用之前处于非活动状态天数。 |
| -g group | 定义现有组的 GID 或名称，该组将作为角色的主组。 |
| -G group | 定义现有组的 GID 或名称，该组将作为角色的辅助组。 |
| -k template_dir | 指定包含模板（默认）.profile 的目录，用于用户配置文件。 |
| -m | 如果主目录不存在，则创建它。主目录由 `-b` 和角色名称或 `-d` 定义。 |
| -o | 允许指定现有 UID。即允许使用重复的 UID 创建角色（见 -u）。 |

表 17.8: roleadd 命令的命令行参数。

| 参数 | 描述 |
| --- | --- |
| -p profiles | 指定一个或多个执行配置文件（用逗号分隔）。 |
| -s shell | 指定登录 shell；默认是 Bourne shell (`/bin/sh`)。 |
| -u uid | 指定角色的 UID。必须是十进制整数。如果没有，则分配下一个可用的 UID。 |

## 考试提示

`roleadd` 支持的命令行参数与 `useradd` 相同，但 `roleadd` 不支持 `-R` 命令行参数，因为角色不能包含其他角色。

以下示例使用 `roleadd` 命令创建一个角色：

```bash
$ roleadd -A solaris.*,solaris.grant -p root root
```

表 17.7 列出了 `exec_attr` 文件定义的默认特权操作。所有操作的 `Policy` 字段均设置为 `suser`，且 `Type` 字段均设置为 `cmd`。

## 考试提示

`roleadd` 支持的命令行参数与 `useradd` 相同，但 `roleadd` 不支持 `-R` 命令行参数，因为角色不能包含其他角色。

以下示例使用 `roleadd` 命令创建一个角色：

```bash
$ roleadd -A solaris.*,solaris.grant -p root root
```

## 考试提示

`roleadd` 支持的命令行参数与 `useradd` 相同，但 `roleadd` 不支持 `-R` 命令行参数，因为角色不能包含其他角色。

以下示例使用 `roleadd` 命令创建一个角色：

```bash
$ roleadd -A solaris.*,solaris.grant -p root root
```
