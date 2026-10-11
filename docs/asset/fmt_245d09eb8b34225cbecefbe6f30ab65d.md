
第三个原因是安全。一些人可能将其归类为“工作分类”。换句话说，即用户权限。所以，这并不仅仅是一个担忧，而是为特定用户开启的功能。例如，如果 Mary（账户）登录系统，她将能够使用会计系统并检查所有账户和记录。相比之下，作为数据录入员的 John 访问会计系统添加新的运输订单和库存记录。此外，John 只能运行与其职责相关的电子表格和文字处理应用程序。这既显示了对安全的关注，也显示了对系统中角色的关注。我们不希望 John 访问会计系统查看每个人的信息。从相对角度来看，我们希望允许 John 只运行电子表格和文字处理应用程序。

为了帮助处理这种情况（以及其他情况），Linux 提供了多用户同时登录的支持。每个用户都有唯一的名称和一个用于标识的用户名。你无法查看特定于某个用户的用户名——情况比这要复杂得多。

# 管理用户

本节深入探讨了管理的世界。

## `/etc/passwd`

`/etc/passwd` 文件的结构与其他配置文件类似。每行代表一个项。表 22.1 标识了这些字段。

| 字段 | 说明 |
| :--- | :--- |
| `Username` (用户名) | 这是唯一标识系统一个用户的用户名。 |
| `Password` (密码) | 这是特定于用户名的密码加密形式。 |
| `Numeric user ID` (数字用户 ID) | 每个用户在系统内被标识为某个组的成员。 |
| `Numeric group ID` (数字组 ID) | 这通常保留给用户的全名（姓和名）。 |
| `Home directory` (家目录) | 该字段是指示用户家目录的目录路径。 |
| `Login shell` (登录 shell) | 这标识用户登录系统后要运行的 shell 程序。 |

如前所述，这些每个字段（文件数据）之间都用冒号隔开，每行代表 `/etc/passwd` 文件的一个典型条目：

```
scat:gtFs4gQf::122:100:Simpson J. Cat:/home/scat:/bin/bash
```

在示例条目中，用户名是 `scat`。第二个字段是不可读的密码项。第三项是与用户名关联的唯一数字 ID。下一个字段是与 `scat` 关联的数字组 ID，100。项 `Simpson J. Cat` 是全名项，第六个字段是 `scat` 的家目录。最后一个字段是要启动的 shell 命令，即 `/bin/bash`。

以下是 `/etc/passwd` 文件。

```
stimpy $ cat /etc/passwd
root:x:0:root:root:/bin/bash
demon:x:1:daemon:/bin/bash
daemon:x:2:daemon:/bin/bash
np:x:47:daemon:/var/spool/lppd:/bin/bash
ess:x:9:system:/etc/news:/bin/bash
uu:x:65:nolog:/usr/sbin/colorconfig:/bin/bash
gawget:x:102:nolog:/root:/bin/bash
post:x:103:post:/var/spool/post:/bin/bash
pat:x:24:uuc:/var/spool/uuc:/bin/bash
at:x:25:25::/var/spool/atd:/bin/bash
index:x:27:index:Database User:/usr/bin:/bin/bash
mysql:x:28:28:mysql User:/var/lib/mysql:/bin/bash
swww:x:30:30:www:/var/run/apache:/bin/bash
dnbus:x:31:dbus:/var/lib/dbus:/bin/bash
query:x:33:65534:proxy User:/var/lib/postgresql:/bin/bash
gnats:x:34:65534:Gnu Backtracker:/usr/lib/gnats:/bin/bash
bin:x:35:65534:/var/lib/bin:/bin/bash
tp:x:37:65534:FTP User:/var/lib/ftp:/bin/bash
irc:x:39:65534:IRC User:/var/lib/ircd:/bin/bash
mail:x:40:65534:Mail User:/var/spool/mail:/bin/bash
sync:x:42:42:sync Account:/usr/sync:/bin/false
infoma:x:43:43:Information User:/var/info:/bin/bash
dbfenc2:x:46:46:Database User:/usr/bin:/bin/bash
dfs2inst:x:47:47:Instance User:/var/spool/nfs:/bin/bash
gd:x:50:65534:nobody:/bin/false
ssbody:x:53:65534:nobody:/bin/bash
stimpy $
```

请注意，`root` 账户的 UID 为 0。`root` 也称为超级用户账户（superuser）。超级用户账户并不必须是 `root`，尽管这是标准做法。例如，如果你喜欢，可以使用 `king` 或 `master` 作为名字。无论你选择什么名字，系统都会据此确定 UID。

第一个字段是分配给用户的名称。大多数组织都有一套命名规范策略。最流行的命名规范是用户首名（首字母）和姓氏的组合。在之前的示例中，`Stimpon J. Cat` 使用了名字的首字母加在姓氏前面。这是最常用的约定，尽管也可以采用其他方案。另一种流行的方案是写出用户的名字，后面跟一个下划线（`_`），然后是用户的姓。例如，在这种情况下我们使用 `stimpy_cat`。这可以避免因名字首字母加姓氏可能产生的冲突。Valarie Findlay 和 Vincent 很难找到用户名，是因为系统限制了用户名长度为八个字符。创建用户名时可以使用字母、数字、下划线（`_`）和点（`.`）。

第二个字段是密码，由于它是加密格式，因此无法使用。密码对人类来说是不可读的，这很有道理。Linux 系统上的每个用户都可以……（此处原文截断）。

第三个字段是分配给用户的 UID。第四个字段是组 ID（GID）。第五个字段是用户的描述信息（GECOS字段）。第六个字段是用户的家目录，用户登录后通常会进入该目录。最后一个字段指定了用户登录时启动的 shell 路径。

用户名（或登录名）是一个长度不超过八个字符的字符串，尽管 Linux 发行版允许更多字符。合法的字符可以由字母、数字、点（`.`）、下划线（`_`）和连字符（`-`）组成。第一个字符必须是字母或数字。通常的惯例是使用小写字母作为用户名。大多数 `useradd` 版本在你没有遵守这些规则时会产生一条警告信息。

### 手动创建新用户

你可以手动创建用户账户，而无需使用 `adduser` 或 `useradd` 命令。下面的步骤详细说明了所需的顺序。在开始之前提点一点：你的系统可能无法使用 `v`（或 `vi`）命令；视情况使用合适的编辑器均可。

- 1. 使用 `vi` 命令编辑 `/etc/passwd` 文件。插入名称和所需的字段。你不应该使用其他编辑器来编辑此文件；`vi` 命令在编辑时会给 `/etc/passwd` 文件加上适当的锁。验证你是否已提供了用户名、UID、GID、用户全名、家目录以及用户的登录 shell。对于密码，使用 `(*)` 字段设置默认密码。目前，密码处使用 `*` 将禁止使用该用户名。
- 2. 创建你在 `/etc/passwd` 文件中标识的用户家目录。例如，如果用户名是 `newuser`，执行命令 `mkdir /home/newuser`。
- 3. 在创建用户家目录后，将 `/etc/skel/` 中的所有文件复制到用户的家目录。使用我们的示例，使用命令 `cp -r /etc/skel/ /home/newuser`。
- 4. 接下来，你需要使用 `chown` 和 `chmod` 命令设置所有权权限。推荐的命令序列如下：`chown /home/newuser`、`chown -R newuser:group` 以及 `chmod -R 755 /home/newuser`。
- 5. 最后，你需要使用 `password` 命令设置初始密码。该命令用于更改指定用户名的密码及其属性。如果你的发行版使用 `/etc/shadow` 文件，你必须确保将用户也添加到该文件中。

如果你为该用户需要一个新组，你将不得不编辑 `/etc/group` 文件。要编辑此文件，你需要使用 `vi` 命令，其操作与 `vippr` 命令类似。为新组账户提供相应的属性并保存文件。

在你完成最后一步（设置密码）后，该账户应该是可以访问的。密码步骤应该是该过程的最后一步。如果你作为早期用户就更改了密码，则该用户必须在你完成剩余步骤之前登录。
