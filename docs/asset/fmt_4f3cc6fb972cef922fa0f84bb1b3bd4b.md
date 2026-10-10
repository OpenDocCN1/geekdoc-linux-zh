
chage 选项的列表见表 28-2。

# 使用 useradd、usermod 和 userdel 添加和删除用户

Linux 还提供 `useradd`、`usermod` 和 `userdel` 命令来管理用户账户。所有这些命令都以命令行选项的形式接收所有信息。如果未指定选项，它们将使用预定的默认值。这些是命令行操作。要在桌面上使用它们，你首先需要打开一个终端窗口（在桌面上右键单击并选择“打开终端”），然后在 shell 提示符处输入命令。

如果你正在使用 Red Hat 和 Fedora 发行版的桌面接口，你应该使用 `system-config-users` 来管理用户账户（参见第 4 章）。你可以从 系统 | 管理 | 用户和组 菜单条目访问 `system-config-users`。它仅标记为“用户和组”。表 28-3 列出了用户管理工具。

## 表 28-3 用户和组管理工具

| 工具 | 描述 |
| :--- | :--- |
| system-config-users | 用于添加、删除和修改用户和组的 Fedora 桌面工具，参见第 1 章（系统 I 管理：用户和组） |
| Kuser | 用于添加、删除和修改用户和组的 K 桌面工具 |
| useradd username options | 添加一个用户 |
| userdel username | 删除一个用户 |
| usermod username options | 修改用户属性 |
| groupadd groupname options | 添加一个组 |
| groupdel groupname | 删除一个组 |
| groupmod groupname options | 修改组名 |

## useradd

使用 `useradd` 命令时，你需要在命令行中通过选项输入值（例如用户名）来创建用户账户。该命令会利用新账户的所有默认特性，为指定名称创建一个新的登录名和目录。

```
# useradd chris
```

`useradd` 实用程序首先检查 `/etc/login.defs` 文件以获取创建新账户的默认值。对于未在 `/etc/login.defs` 文件中定义的默认值，`useradd` 会提供其自身的默认值。你可以使用带有 `-D` 选项的 `useradd` 命令来显示这些默认值。默认值包括组名、用户 ID、主目录、`skel` 目录以及登录 Shell。用户在命令行中输入的值将覆盖相应的默认值。组名是新账户所属组的名称。默认情况下，这是 `other`，意味着新账户不属于任何组。用户 ID 是识别用户账户的数字。`skel` 目录是保存初始化文件副本的系统目录。当用户的新主目录创建时，这些初始化文件会被复制到其中。登录 Shell 是用户计划使用的特定 Shell 的路径名。

`useradd` 命令具有与每个默认值对应的选项。表 28-4 列出了你可以与 `useradd` 命令一起使用的所有选项。在创建特定账户时，你可以使用具体值来替代这些默认值中的任何一个。在完成设置之前，登录是不可访问的。在下面的示例中，`chris` 账户的组名被设置为 `intro1`，用户 ID 被设置为 578：

```
# useradd chris -g intro1 -u 578
```

添加新的用户登录后，你需要为新登录设置密码。密码条目放置在 `/etc/passwd` 和 `/etc/shadow` 文件中。使用 `passwd` 命令为用户创建新密码，如下所示。你输入的密码不会显示在屏幕上。系统会提示你重复输入密码。随后会显示一条消息，表明密码已成功更改。

## 表 28-4 useradd 和 usermod 的选项

| 选项 | 描述 |
| :--- | :--- |
| -d dir | 设置新用户的主目录。 |
| -D | 显示所有设置的默认值。也可用于重置主目录（-b）、组（-g）、Shell（-s）、过期日期（-e）和密码过期（-E）的默认设置。 |
| -e mm/dd/yy | 为账户设置过期日期（默认无）。指定为月/日/年。 |
| -f days | 设置密码过期后账户保持活跃的天数。 |
| -g group | 设置一个组。 |
| -m | 如果用户主目录不存在，则创建该目录。 |
| -m -k skel-dir | 设置保存骨架文件的骨架目录（如 .profile 文件），这些文件在用户主目录创建时会自动复制过去；默认是 /etc/skel。 |
| -M | 不创建用户主目录。 |
| -p password | 提供加密后的密码（crypt 或 MD5）。如果没有参数，账户立即被禁用。 |
| -r | 一个特定于 Red Hat 和 Fedora 的选项，用于创建系统账户（其用户 ID 低于 login.defs 中设置的最小值）。除非指定 -m，否则不创建主目录。 |
| -s shell | 设置新用户的登录 Shell。默认是 /bin/bash，即 BASH Shell。 |
| -u userid | 设置新用户的用户 ID。默认值是迄今为止使用的最高数字的递增。 |

```
# passwd chris

Changing password for user chris

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully

#
```

## usermod

`usermod` 命令允许你更改这些特性的任意值。你可以更改主目录或用户 ID。你甚至可以更改账户的用户名。`usermod` 命令接受与 `useradd` 相同的选项，这些选项列在表 28-4 中。

## userdel

当你想从系统中移除用户时，可以使用 `userdel` 命令删除该用户的登录信息。使用 `-r` 选项时，用户的主目录也将被移除。在下面的示例中，用户 `chris` 被从系统中移除：

```
# userdel -r chris
```

## 组管理

你可以使用 Shell 命令或 `system-config-users` 等窗口实用程序来管理组。组是管理访问权限的有效方式，让你仅通过组名就能控制多个用户。

## /etc/group 和 /etc/gshadow

保存组条目的系统文件称为 `/etc/group`。该文件由组记录组成，每行一条记录，字段之间用冒号分隔。组记录包含四个字段：组名、密码、组 ID 以及属于该组的用户。密码字段可以留空。组记录的字段如下：

- `组名` 组的名称，必须唯一
- `密码` 实现了影子安全机制时，此字段为 x，密码在 `/etc/gshadow` 文件中指示
- `组 ID` 系统分配的用于标识该组的数字
- `用户` 属于该组的用户列表，用逗号分隔

以下是 `/etc/group` 文件中一个条目的示例。该组名为 `engines`，密码由影子安全管理，组 ID 为 100，属于该组的用户是 `chris`、`robert`、`valerie` 和 `aleina`：

```
engines:x:100:chris,robert,valerie,aleina
```

与 `/etc/passwd` 文件的情况类似，最好使用 `groupmod`、`groupadd` 或 `system-config-users` 等组管理实用程序来更改组条目。所有用户都可以读取 `/etc/group` 文件。在影子安全机制下，如密码等安全的组数据保存在 `/etc/gshadow` 文件中，只有 root 用户可以访问该文件。

## 用户私有组

可以将新用户分配到一个专门为该用户设立并以其用户名命名的特殊组中。因此，新用户 `dylan` 会被分配到一个默认组，该组也称为 `dylan`。组 `dylan` 也会出现在组的列表中。这种分配默认用户组的方法称为用户私有组（UPG）方案。目前在 Red Hat 和 Fedora 系统上使用 UPG。补充组是用户可能希望加入的额外组。传统上，所有用户都被分配到一个名为 `users` 的组，该组会对所有用户应用 `users` 组的权限控制。在 UPG 中，每个用户都有自己的组，拥有自己的组权限。

## 组目录

与用户类似，你可以为组创建主目录。为此，只需在 `/home` 目录中为该组创建一个目录，并将其名称更改为组名，同时允许该组的任何成员访问即可。以下示例创建了一个名为 engines 的目录，并将其组更改为 engines 组：

```
mkdir /home/engines

chgrp engines /home/engines
```

然后，应使用本章稍后介绍的 `chmod` 命令设置组级别的读取、写入和执行权限：

```
chmod g+rwX /home/engines
```
