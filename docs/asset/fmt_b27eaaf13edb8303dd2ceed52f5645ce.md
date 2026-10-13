
## 访问控制列表 (ACLs)

当传统的 UNIX 文件权限不足时，访问控制列表（缩写 `ACLs`，读作 "ackkls"）对文件权限提供了更细粒度的控制。UNIX 文件保护为三类用户（所有者、组和其他用户）提供读、写、执行权限。`ACL` 通过允许你为所有者、所有者所属组、其他人、特定用户和组定义文件权限，从而提供了更好的文件安全性。它还允许你为这些类别中的每一个定义默认权限。

例如，你可能有两个组需要访问某个文件的权限：一个组用于读取，另一个组用于写入。或者，你可能有一个文件，希望该组中的每个人都能读取它，那么你只需给该文件设置组读取权限即可。假设你只想让该组中的两个人能够写入该文件。在标准的 UNIX 权限下，你无法只给组中的两个成员授予写入权限。但是，你可以为文件设置 `ACL`，仅授予该组中的两个人对该文件的写入权限。

`ACL` 是标准 UNIX 文件权限的扩展。`ACL` 信息单独存储并与每个文件关联。

## ACL 命令

你使用表 107 中列出的 `ACL` 命令和选项为文件或目录定义 `ACL`。每个 `ACL` 条目由以下字段组成，字段之间用冒号分隔。

### 表 107 ACL 命令和选项

| 命令/选项 | 说明 |
| :--- | :--- |
| `getfacl` | 显示 `ACL` 条目。 |
| `-a` | 显示文件名、所有者、组和文件的 `ACL`。 |
| `-d` | 显示文件的文件名、所有者和组。即使文件没有 `ACL` 也会显示这些信息。 |
| `setfacl` | 设置、添加、修改和删除 `ACL` 条目。 |
| `-s acl-entries` | 设置文件的 `ACL`，移除所有旧条目并将其替换为新指定的 `ACL`。 |
| `-m acl-entries` | 为文件添加或修改 `ACL` 条目。 |
| `-x acl-entries` | 从文件中移除 `ACL` 条目。 |
| `-f file` | 指定包含 `ACL` 条目的文件。 |
| `-v` | 详细输出，显示文件的 `ACL` 条目。 |

## 文件安全

| 参数 | 说明 |
| :--- | :--- |
| `entry-type` | `ACL` 条目类型（用户、组、掩码）。 |
| `UID` | 用户名或 ID。 |
| `GID` | 组名或 ID。 |
| `perm` | 权限 (`r`, `w`, `x`)。 |

## 理解系统安全

## 目录的 ACL 权限

你可以为目录设置默认 `ACL`，使其适用于其中创建的文件。在具有默认 `ACL` 条目的目录中创建的文件具有与目录相同的 `ACL`。

当你第一次为特定用户和组设置默认 `ACL` 条目时，必须为所有者组、其他人以及掩码设置默认 `ACL` 条目。

- `[default]:u[ser]::perm` - 设置所有者的默认权限。
- `[default]:g[roup]::perm` - 设置组的默认权限。
- `[default]:o[ther]::perm` - 设置其他人的默认权限。
- `[default]:m[ask]::perm` - 设置默认 `ACL` 掩码。
- `[default]:u[ser]:UID:perm` - 设置特定用户的默认权限。
- `[default]:g[roup]:GID:perm` - 设置特定组的默认权限。

## 判断文件是否具有 ACL

你可以通过两种方式之一判断文件是否具有 `ACL`。

- 使用 `ls -l` 命令。
- 使用 `getfacl` 命令。

当你使用 `ls -l` 命令时，任何具有 `ACL` 的文件的模式字段右侧都会显示加号 (`+`)。

注意：如果你为文件定义 `ACL` 但没有指定任何额外的用户或组，即使文件具有基础 `ACL`，模式字段右侧也不会显示加号。只有当 `ACL` 中包含额外的用户或组时，才会显示加号。

在下面的示例中，文件 `foo` 具有 `ACL`，且列表中至少有一个条目。

```
$ castle ls -l foo
-rwxrxrxr+ 1 winsor staff 0 Oct 3 14:22 foo
$ castle
```

## 文件安全

当你不带任何选项使用 `getfacl filename` 命令时，该文件的 `ACL` 信息将以以下格式显示：

```
# file: filename
# owner: uid
# group: gid
user::perm
user:uid:perm
group::perm
group:gid:perm
mask:perm
other:perm
default:user:perm
default:v:uid:perm
default:group:perm
default:group:gid:perm
```

在下面的示例中，文件 `foo` 的 `ACL` 赋予了所有者 `rwx` 权限，赋予用户 `ray` 只读权限。

```
castle$ getfacl foo
# file: foo
# owner: winsor
# group: staff
user::r--
user:ray:r-- #effective:r-
group:rw- #effective:rw-
mask:rw-
other::---
castle$
```

注意：你可以使用 `getfacl` 命令以相同的格式显示任何 `UFS` 文件或目录的权限。文件不需要具有 `ACL`。

为了对比，下面的示例显示了文件 `bar` 的 `ls -l` 和 `getfacl` 命令的输出，该文件没有 `ACL`。

```
castle$ ls -l bar
-rwx------ 1 winsor staff 0 Oct 3 14:22 bar
castle$ getfacl bar
# file: bar
# owner: winsor
# group: staff
user::rwx
group:rw- #effective:rw-
mask:rw-
other::---
castle$
```

## 设置 ACL 文件权限

使用 `setfacl` 命令为文件设置 `ACL` 权限。你可以从命令行设置文件或一组文件的权限，也可以通过在文件中列出权限并使用该文件作为 `setfacl` 命令的参数来设置。你可以以下语法指定权限：

```
u[ser]:perm
u[ser]:uid:perm
group:perm
group:gid:perm
m[ask]:perm
o[other]:perm
d[default]:u[ser]:perm
d[default]:u[ser]:uid:perm
d[default]:g[roup]:perm
d[default]:g[roup]:gid:perm
d[default]:m[ask]:perm
d[default]:o[other]:perm
```

注意。你可以使用八进制值或符号值来设置权限。

在命令行上，使用逗号分隔每个权限语句。
在 `ACL` 文件中，将每个语句单独放在一行。这些语句不需要遵循任何特定顺序。

## 从命令行设置文件权限

要从命令行设置 `ACL` 权限，你必须至少指定用户、组、其他和掩码（`mask`）的基础权限。输入以下命令设置 `ACL` 权限：`setfacl -s u:perm,g:perm,m:perm, [u:UID:perm], [g:GID:perm]`

你可以通过用户名或 `UID` 数字来设置用户。请注意，在使用用户名参数之前，用户账户必须已经存在于 `Passwd` 数据库或本地的 `/etc/passwd` 文件中。你可以通过名称为任何 `UID` 分配权限，无论该用户账户是否存在。

同样地，你可以通过组名或 `GID` 数字来设置组名。

下面的示例将所有权限分配给用户，将组权限限制为只读，并拒绝其他（`other`）的权限。默认掩码设置了读写权限，并且用户 `ray` 被赋予了文件 `foo` 的读写权限。

首先，查看文件的当前权限。

```
castle% ls -l foo
-rw-rw-rw- 1 winsor      staff      0 Oct 3 14:22 foo
```

然后，设置用户、组、所有者和掩码的权限，并向 `ACL` 添加一个用户。

```
castle$ setfacl -s u:rwx,g:r--,o:---,mask:rw-,u:ray:rw- foo
```

使用八进制值（如下面的示例所示）可以得到结果。

```
castle$ setfacl -s u:7,g:4,o:0,mask:6,u:ray:6 foo
```

接下来，验证权限已设置以及文件是否具有 `ACL`。

```
castle$ ls -l -rwxrwx------ 1 winsor staff 0 Oct 3 14:22 foo
```

如你所示，文件的权限已更改，权限字段后的加号表示该文件具有 `ACL`。最后，使用 `getfacl` 命令验证所有设置都已正确完成。

```
castle$ getfacl foo
# file: foo
# owner: winsor
# group: staff
user:rw-
user:ray:rw-      #effective:rw-
```
