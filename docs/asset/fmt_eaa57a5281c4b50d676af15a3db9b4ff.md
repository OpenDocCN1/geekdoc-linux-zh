
## 扩展文件权限：访问控制列表 (ACL)

Solaris 8 通过添加访问控制列表 (ACL) 功能扩展了 Unix 文件权限。ACL 允许你在默认权限（掩码 mask）的基础上为特定的用户和组添加权限。

除了支持针对标准文件用户账户（所有者）的标准读/写/执行权限外，ACL 还可以用于为额外的用户账户设置读/写/执行权限。同样，ACL 支持标准文件组账户的读/写/执行权限，并允许额外的组账户拥有读/写/执行权限。ACL 还支持标准“其他”（所有人）的读/写/执行权限。

ACL 还包含一个掩码功能，用于控制给予除标准文件用户账户和标准文件组账户之外的用户和组的最大允许权限。

例如，假设 root 拥有一个文件并将其 ACL 掩码设置为读/执行。随后，root 为 guest 用户账户向该文件 ACL 添加了读/写/执行权限。由于掩码的存在，写权限被覆盖，guest 账户的有效权限为读/执行。

目录的 ACL 包含默认条目，这些条目决定了分配给在该目录下创建的文件和子目录的权限。可以为标准的 Unix 用户、组和其他定义默认权限，以及针对特定用户或组的默认掩码和默认权限。

使用两个命令来管理 ACL：`setfacl` 命令用于设置 ACL，`getfacl` 命令用于显示 ACL。

**考试提示**
使用 `setfacl` 命令对文件和目录添加、修改和删除 ACL 是一项测试目标。

### 使用 setfacl 设置 ACL

你使用 `setfacl(1)` 命令来设置和修改 ACL。它支持三个命令行参数：

- `-d` — 删除指定的 ACL 条目
- `-m` — 添加/更改指定的 ACL 条目
- `-s` — 用指定的条目替换 ACL

标准用户和组权限的 ACL 条目使用 `entry::permissions` 格式指定（注意两个冒号），其中 `entry` 是关键字 `user` 或 `group`（单字母缩写 `u` 或 `g`），而 `permissions` 是定义权限所需的 `r`、`w`、`x` 和 `-` 的适当组合。

> **注意**：OCR 文字流显示：标准对象的 ACL 条目和用于最大权限的掩码用法略有不同。格式为 `entry::mask`（注意单冒号），其中 `entry` 是关键字 `object` 或 `mask`（单字母缩写 `o` 或 `m`），而 `permissions` 是定义权限所需的 `r`、`w`、`x` 和 `-` 的适当组合。

用于标准对象的 ACL 条目和用于最大权限的掩码用法略有不同。格式为 `entry::mask`（注意单冒号），其中 `entry` 是关键字 `object` 或 `mask`（单字母缩写 `o` 或 `m`），而 `permissions` 是定义权限所需的 `r`、`w`、`x` 和 `-` 的适当组合。

### 使用 getfacl 显示 ACL

要显示文件或目录的 ACL，使用 `getfacl` 命令。以下列表显示了使用 `getfacl` 命令查看 shlog 目录的 ACL：

```bash
## getfacl shlog
## file: shlog
# owner: shlog
## group: staff
user::r-x
group::r-x
mask:r-x
other:r-x
default:user::rw-
default:group::rw-
default:mask:r-
default:other:r--
```

```bash
-rw-rw--r-- 1 root other      636 Feb 28 07:39 list
## chown 1001 data list
## ls -l
total 18
-rw-rw--r-- 1 guest other      120 Feb 28 07:38 data
-rw-rw--r-- 1 guest other      6528 Feb 28 07:38 junk
-rw-rw--r-- 1 guest other      636 Feb 28 07:39 list
#
```

`chown` 命令支持一个递归命令行参数 `-R`。当你使用它来更改目录的所有权时，该目录下任何文件或子目录的所有权也会随之改变。

尽管有单独的命令来更改文件的组所有权，但你可以通过跟随用户账户或 UID（后跟冒号 `:`）以及组账户名称或 GID，来使用 `chown` 命令同时更改组所有权。以下示例展示了使用 `chown` 命令同时更改用户账户所有权和组所有权：

```bash
## ls -l
total 18
-rw-rw--r-- 1 sys staff      120 Feb 28 07:38 data
-rw-rw--r-- 1 sys staff      6528 Feb 28 07:38 junk
-rw-rw--r-- 1 sys staff      636 Feb 28 07:39 list
## chown sys:staff data list
## ls -l
total 18
-rw-rw--r-- 1 sys staff      120 Feb 28 07:38 data
-rw-rw--r-- 1 sys staff      6528 Feb 28 07:38 junk
-rw-rw--r-- 1 sys staff      636 Feb 28 07:39 list
```

如果 `root` 用户以外的任何人使用 `chown` 命令更改具有 `setuid` 权限的文件的所有权，则该 `setuid` 权限会被清除。此操作防止用户设置一个文件、将其所有权更改为他人，并利用该文件访问另一个用户账户。

作为 Solaris 8 的增强安全特性，`chown` 命令的使用被限制在超级用户账户上。你可以通过清除 `/etc/system` 文件中的内核参数并重启系统来移除此限制：

```bash
set rstchown = 0
```

将 `rstchown` 设置为 `1` 并重启系统将重新强制执行限制。

## 修改文件组账户

`chgrp` 命令更改与文件或目录关联的组账户。只有当前拥有文件的用户账户或超级用户账户（root）才能更改组所有。默认情况下，文件所有者只能更改该用户所属的组账户。

你通过组账户名称或关联的 GID，以及一个或多个应由指定组账户拥有的文件名进行指定。以下列表显示了使用 `chgrp` 命令将多个文件的所有权更改另一个组账户（该组 GID 为 1）。每个 `chgrp` 命令的前后都跟着 `ls` 命令，它用于列出文件的所有权和权限：

```bash
## ls -1
total 18
-rw-rw-r-- 1 sys staff     120 Feb 28 07:38 data
-rw-rw-r-- 1 sys staff     6528 Feb 28 07:38 junk
-rw-r--r-- 1 sys staff     636 Feb 28 07:39 list
## chgrp other junk
## ls -1
total 18
-rw-rw--r-- 1 sys staff     120 Feb 28 07:38 data
-rw-rw--r-- 1 sys other     6528 Feb 28 07:38 junk
-rw-r--r-- 1 sys other     636 Feb 28 07:39 list
## chgrp 1 data list
total 18
-rw-rw--r-- 1 sys other     120 Feb 28 07:38 data
-rw-rw--r-- 1 sys other     6528 Feb 28 07:38 junk
-rw-r--r-- 1 sys other     636 Feb 28 07:39 list
#
```

与 `chmod` 一样，`chgrp` 命令支持递归命令行参数 `-R`。当你使用它更改目录的组所有权时，该目录下任何文件或子目录的组所有权也会随之改变。

如果非 root 账户且没有相应权限的账户使用 `chgrp` 命令，且文件具有 `setuid` 特殊权限或 `setgid` 特殊权限，则 `setuid` 或 `setgid` 权限会被清除。此操作防止用户设置一个 `setuid` 或 `setgid` 文件，将其所有权更改为他人，然后利用该文件访问另一个用户账户或组账户。

作为 Solaris 8 的增强安全特性，`chgrp` 命令受到限制，要求尝试更改组所有权的用户账户必须是新组的成员。你可以通过更改 `/etc/system` 文件中的以下内核参数并重启系统来移除此限制：

```bash
set rstchown = 0
```

将 `rstchown` 设置为 `1` 并重启系统将重新强制执行限制。

## 显示文件权限和所有权

`ls(1)` 命令显示文件权限和所有权。`ls` 命令支持表 5.5 中描述的命令行参数。

**表 5.5: `ls` 命令的命令行参数**

| Argument | Description |
| --- | --- |
| name | 要显示信息的目录或文件的名称 |
| -a | 包括以 `.` 和 `..` 开头的所有文件 |
| -d | 列出目录本身而非内容 |
| -C | 尽可能多列显示 |
| -c | 显示最后状态更改的时间 |
| -F | 为条目添加指示字符以显示类型 |
| -g | 使用数字 GID 列出组所有权 |
| -h | 以易读格式打印大小 |
| -i | 每个文件的 inode 号 |
| -L | 跟随符号链接 |
| -n | 使用数字列出用户和组 |
| -o | 使用数字 GID 列出组所有权 |
| -r | 反转排序 |
| -R | 递归列出目录 |
| -s | 以块打印每个文件的大小 |
| -t | 按修改时间排序 |
| -u | 按访问时间排序 |
| -x | 按列显示输出 |
| -1 | 每行列出一个条目 |

`ls` 命令支持多种命令行参数，可以显示和排序任何人想知道的关于目录和文件的信息。

当你使用一种长列表格式（`-g`、`-l`、`-n` 或 `-o`）时，文件权限和额外信息显示在每个目录/文件的前 11 个字符中。表 5.6 列出了用于第一个字符的字符。

**表 5.6: ls 显示的文件权限中的第一个字符**

| Character | Description |
|---|---|
| b | 块特殊文件 |
| c | 字符特殊文件 |
| d | 目录 |
| D |  |
| l | 符号链接 |
| p | FIFO 或命名管道 |
| s | 套接字 |
| - | 普通文件 |

**表 5.7: ls 显示的文件权限中第 2 到 10 位的字符**

| Character | Description |
|---|---|
| l | 强制锁定 |
| r | 读权限 |
| s | 设置 UID（第四位）或设置 GID（第七位） |
| S | 未定义状态 |
| t | 粘滞位 |
| T | 未定义状态 |
| w | 写权限 |
| x | 执行权限 |
| - | 未授予权限 |

第 11 位通常是一个空格，除非在目录/文件上定义了 ACL。在这种情况下，第 11 个位置会出现一个加号 (`+`)。下面的列出列表显示了 `ls` 命令生成的输出中权限字段部分的示例：

```bash
## ls -l
total 2
drwxrxrwt 2 sarah other 512 Jan 24 13:49 dirl
-rwxrxr-x 1 sarah other 1112 Jan 24 13:53 file1
lrwxrxr-x 1 sarah other 1112 Jan 24 13:53 file2
-rwxrrwx+ 1 sarah other 1112 Jan 24 13:53 file3
```
