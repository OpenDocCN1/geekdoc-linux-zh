
| `username` | 指定用户名作为查询或修改的账户。 |

| `-l` | 显示用户名的过期信息。 |

| `-m` `mindays` | 设置 `mindays` 为两次密码更改之间允许的最小天数。 |

| `-M` `maxdays` | 设置 `maxdays` 为密码有效的最大天数。 |

**表 29-4（续）**

| OPTION | DESCRIPTION |

| --- | --- |

| `-d` `lastday` | 设置 `lastday` 为最后更改密码的日期，表示为自 1970 年 1 月 1 日以来经过的天数。`lastday` 可以使用更方便的格式设置，例如 2003 年 6 月 21 日或 2003-0621。 |

| `-I` `inactive` | 设置 `inactive` 为密码过期后账户在锁定前允许非活动状态的天数。 |

| `-E` `expired` | 设置 `expired` 为账户过期的日期。 |

| `-W` `warndays` | 设置 `warndays` 为密码过期前发出警告信息的天数。 |

如果不使用任何选项，`chage` 将以交互模式运行，提示用户输入每项信息。使用 `change` 命令的 `-1` 选项可以获得友好的显示：

```bash
# change -1 maryuse
Minimum: 0
Maximum: 99999
Warning: 0
Inactive: -1
Last Change: Apr 04, 2005
Password Expires: Never
Password Inactive: Never
Account Expires: Never
```

`chage` 并不按照字段在 `/etc/shadow` 中出现的顺序显示它们。

## 同时修改多个账户

在繁忙或大型 IT 环境中，系统管理员经常发现自己有创建多个用户账户的必要性。使用 `useradd` 添加一两个账户相对简单，但如果需要创建 10 或 20 个账户，很快就会变得繁琐。幸运的是，密码切换工具包含了 `newusers` 工具，它可以用于创建和更新多个账户。正如本章开头提到的，命令行工具的优势之一是它们可以执行批量或大规模更改。`chpasswd` 和 `newusers` 两个命令可以在一次操作中对用户密码数据库进行多次更改。其语法为：

```bash
newusers userfile
```

`userfile` 是一个文件名，其内容格式与标准密码文件相同，但有以下例外：

- 密码字段以明文形式出现——`newusers` 在添加账户之前对其进行加密。
- 如果用户已存在，对于 shadow 密码，`pw_age` 字段将被忽略。
- GID 可以现有组的名称，也可以是不存在的 GID。如果 GID 是现有组的名称，则将指定的用户添加到该组；如果它是一个不存在的数值，则创建一个具有指定 GID 的新组。
- 如果指定的家目录指向一个不存在的目录，`newusers` 会创建它。如果目录已存在，则将目录的所有权设置为指定用户的所有。

以下代码显示了 `newusers.txt` 的内容，将其传递给 `newusers` 以创建三个新账户：bubba、joebob 和 maryue：

```
bubba:mypass:901:901:Bubba User:/home/bubba:/bin/bash
joebob:yourpass:902:902:Joe Bob:/home/joebob:/bin/bash
maryue:somepass:903:903:Mary Sue:/home/maryue:/bin/bash
```

执行命令 `newusers newcomers.txt` 后，你将在 `/etc/passwd`、`/etc/group` 和 `/etc/shadow` 中看到这些条目。

# 管理用户和组 719

## 表 29-5 组账户管理命令

| 命令 | 描述 |

| --- | --- |

| `gpasswd` | 设置组密码并修改组账户 |

| `groupadd` | 创建新的组账户 |

| `groupdel` | 删除现有的组账户 |

| `groupmod` | 修改现有的组账户 |

如果密码字段中出现 `x`，则该组的非成员无法通过 `newgrp` 命令加入该组。组文件中的典型条可能如下：

```
admins:x:507:jobob, marysue, bubba
```

`groupname` 为 `admins`；password 表示未设置组密码；gid 为 503；userlist 是用户列表为 jobob, marysue, bubba。

### 创建组

要创建一个新组，请使用 `groupadd` 命令。其语法为：

```
groupadd [-g gid [-o]] [-r] [-f] groupname
```

`groupname` 是唯一必需的参数，且必须是一个不存在的组名。`groupadd` 会创建该组并为其分配第一个大于 500 且未被使用的 gid。指定 `-f` 可强制 `groupadd` 接受已存在的 `groupname`。如果你想指定新组的 gid，请使用 `-g` 选项，将 `gid` 替换为唯一的 G（`-o` 选项用于强制 `groupadd` 接受非唯一的 G）。要创建一个具有特殊权限的系统组，可以使用以下命令创建一个名为 admins 的新组：

```
# groupadd admins
```

这是在 `/etc/group` 中创建的相应条目：

```
admins:x:507:
```

此时，`admins` 没有成员，且密码字段中有一个 `x`，这意味着除了 root 之外的任何人（此时是所有人）都无法通过 `newgrp` 加入该组。

### 修改和删除组

创建新组后，你可能想向其添加用户账户。有两个命令可以修改组账户，每个命令都有不同的用途。`groupmod` 允许你更改组的 GID 或名称，而 `gpasswd` 允许你设置和修改组的身份验证及成员信息。你很少需要更改组的名称或 GID；你需要自行阅读 `groupmod` 的简要手册。我们更感兴趣 `gpasswd`，它允许 root 用户管理组账户的所有方面，并将管理责任委托给组管理员。为了简单起见，接下来的讨论仅解释 root 可用的 `gpasswd` 用法。然后它将涵盖组管理员可以执行的 `gpasswd` 调用。

从权限的角度来看，`gpasswd` 的语法为：

```
gpasswd [-A username] groupname
```

root 可以使用 `-A username` 将 `username` 指定为组的组管理员。`-M username` 将 `username` 添加到组成员列表中。使用 `-A` 分配组管理员不会让该管理员成为组的成员；你必须使用 `-M` 将管理员作为组成员添加。可以使用 `-A` 和 `-M` 指定多个 `username`。以下命令显示了如何将 marys 和 joebob 添加到 admins 组：

```
# gpasswd -M marys,joebob admins
```

> 注意：使用 `-A` 选项时，影子组文件 `/etc/gshadow` 必须存在。请阅读“使用影子组文件”章节以了解使用影子组文件的影响。

在此更改后，`/etc/group` 中的 admins 条目应该类似于：

```
admins!:507:marys,joebob
```

注意，向 admins 组账户添加用户将密码字段中的 `x` 替换为了 `!`，这意味着禁用了基于密码（使用 `newgrp`）的组访问。

对于组管理员，`gpasswd` 的语法为：

```
gpasswd [-R] [-r] [-a username] [-d username] groupname
```

仅带 `groupname` 运行 `gpasswd` 会更改组密码。一旦设置了密码，组成员仍可以使用 `newgrp` 加入该组而无需密码，但组的非成员必须提供密码。例如，以下命令显示了当 root 设置了组密码（顺便说，这是秘密的）后，用户 bubba 使用 `newgrp` 加入组时会发生什么：

> 注意：`newgrp` 将调用用户的组标识更改为 `groupname`。在成功调用 `newgrp` 之后，文件访问权限将根据新的 GID 计算。如果省略了组名，则 GID 将更改为调用用户的主（登录）GID。

```bash
$ newgrp admins
Password:
$ groups
admins bubba
```

相比之下，这里是作为 admins 成员的 jobob 使用 `newgrp` 加入 admins 组时发生的情况。注意 jobob 没有像 bubba 那样被提示输入密码：

```bash
$ newgrp admins
$ groups
admins jobob
```

相反，如果没有设置组密码，则只有组成员可以使用 `newgrp` 加入该组。要移除组密码，请使用 `-r` 选项。接下来的代码片段显示了在移除组密码后，bubba 尝试加入 admins 时会发生什么。请记住，使用 `-r` 密码后，组文件中的密码字段将变为空：

```bash
$ newgrp admins
newgrp: Permission denied.
```

这一次，bubba 甚至没有被提示密码。然而，jobob 没有任何问题：

```bash
$ newgrp admins
$ groups
admins jobob
```

使用 `-R` 选项调用 `gpasswd` 将禁用对 a 的访问。

## 第 29 章

要将用户添加到组，组管理员必须使用 `-a` 选项。`-d` 选项从组中移除用户。接下来的示例显示了如何添加和移除用户：

```bash
# gpasswd -a bubba admins
将用户 bubba 添加组
# grep /etc/group
admins:x:507:bubba

# gpasswd -d bubba admins
从组移除用户 bubba
# grep /etc/group
admins::507:
```

### 使用影子组文件

如果存在影子文件 `/etc/gshadow`，上述行为将不再适用。特别是，如果使用影子文件：

- 添加组会在影子文件中创建如下条目：

`admins::`

`gshadow:admins::`

- 将用户添加到组会同时更新组文件和影子文件：

`# gpasswd -M marys admins`

`# grep /etc/group`

`admins:507:marys`

- 影子文件的第三字段持有组管理员的名称而非 GID，如果使用 gpasswd 添加管理员：

`# gpasswd -A marys admins`

`# grep /etc/gshadow`

`admins::marys`

- 除非账户也是组的成员，否则组管理员无法加入组。同样，组管理员可以添加或删除她的账户。

## 管理用户和组 723

- 只有组成员可以使用 `newgrp` 加入该组。换句话说，组的非成员即使知道密码也无法通过 `newgrp` 加入组。事实上，密码对非成员无效的，因为他们不需要使用。

删除组非常简单。使用 `groupdel` 命令，除了组名外不接受任何选项。例如，以下命令删除了 admins 组：

```
# groupdel admins
```

> 注意：如果你觉得命令很麻烦，下一节“使用 User Manager 管理用户和组”将向你介绍如何使用 Red Hat 的 GUI 工具 User Manager。

### 使用用户私有组

你需要理解用户私有组（UPG）方案的语义，以及 UPG 方案如何使用早期 Red Hat 发版采用并在 Fedora Core 和 RHEL 中沿用的设置目录。UPG 的目的是让 Linux 更易使用。虽然 UPG 方案没有增加或更改 Linux 处理组的标准，但它引入了一种与传统不同的惯例：当你创建一个新用户时，Fedora Core 和 RHEL 会为该用户创建一个组。尽管这很罕见且偏离了传统，但在习惯了 UPG 方案后，你会发现这种方式非常自然且合理。UPG 方案具有以下显著特征：

- 每个用户都有一个与用户名相同的原始组。例如，名为 bubba 的用户有一个初始组名为 bubba。
- 每个用户都是其原始组的唯一成员。因此，用户 bubba 是 bubba 组的唯一成员。
- 每个用户的 umask 默认为 002；因为在 UPG 方案中每个用户都有自己的私有组，所以普通 umask 022 提供的组保护是不必要的。

# 724 第 29 章

- 组特定目录（例如项目目录）启用了 set-GID（设置组 ID）。如果你在目录上设置了 set-GID 位，则在该目录中创建的所有文件的组都将设置为该目录的组。set-GID 目录的行为并非仅用于 UPG（用户项目组），而 UPG 方案利用了 set-GID 特性。

> 提示 默认的 umask 设置在 `/etc/profile` 中。

例如，假设财务部门在 `/opt/finance` 目录下维护着大量文件，并且许多人每天都要处理这些文件。如果你想使用 set-GID 目录和 UPG 方案，首先创建一个名为 finance 的组，使用 `chgrp` 命令更改 `/opt/finance` 的组所有权，使用 `chmod` 命令在 `/opt/finance` 上设置 set-GID 位，然后将相应的用户添加到 finance 组。结果是，finance 组中的所有用户都可以编辑 `/opt/finance` 目录中的现有文件。同样，在 `/opt/finance` 目录中创建新文件时，这些文件的所有权将被分配给 finance 组，所有 finance 组的成员都可以无需任何特殊步骤即可编辑它们。

set-GID 目录的另一个优点是，任何处理多个项目的用户在不同项目目录之间移动时，无需更改他们的 umask 或组。每个项目目录的 set-GID 位会自动为其在该目录及其子目录中创建的所有文件设置主组。

在用户级别，每个用户的家目录都由该用户及其私有组所有。虽然在家目录上设置 set-GID 位是安全的，但没有必要。为什么呢？默认情况下，文件的创建使用用户的主组，且用户是该主组的唯一成员。对于用户的家目录及其子目录来说，set-GID 位是冗余的。

以下步骤说明了上述的场景和过程。此练习的目的是为红帽的 UPG 方案提供具体的说明，因此在后面的章节将讨论相关选项和用法。

- 1. 创建 finance 组：

```
# /usr/bin/groupadd finance
```

- 2. 将 `/opt/finance` 的组所有权更改为 finance 组，以便 finance 组更改目录内容：

```
# /bin/chgrp -R finance /opt/finance
```

- 3. 将正确的用户添加到组（在此例中添加用户 bubba）：

```
# /usr/bin/gpasswd -a bubba finance
```

将 bubba 添加到 finance 组

- 4. 为了 finance 组成员能够创建文件，使目录对组可写：

```
# /bin/chmod g+w /opt/finance
```

- 5. 在 `/opt/finance` 上设置 set-GID 位，使得 `/opt/finance` 树中新创建的文件具有 finance 组所有权：

```
# /bin/chmod g+s /opt/finance
```

执行此命令后，生成 `/opt/finance` 属性的详细列表时，在通常显示组执行位（用字母 x 表示）的地方会出现字母 s：

```
ls -ld /opt/finance
drwxrxr-x 2 root finance group 6 Apr 20 19:26 /opt/finance
```

使用默认掩码 002，bubba 在 `/opt/finance` 中创建的文件归用户 bubba 所有，且 finance 组对用户和组所有者都具有读/写权限，允许其他财务组的用户修改该文件：

- `touch /opt/finance/20050420`
- `ls -1 /opt/finance/20050420`
- `-rw-xr-r-- 1 bubba 0 Apr 20 19:29 /opt/finance/20050420`

总结来说，目录上的 set-GID 位结合红帽 UPG 方案，使得创建项目组变得非常简单，允许组成员在组的公共目录写入文件，而不会给用户带来过重的负担。

# 使用 User Manager 管理用户和组

User Manager（用户管理器）是一个用于管理用户和组账户的图形工具。要使用它，你必须以 root 身份登录或拥有 root 权限。要启动 User Manager，点击主菜单 ⊞ 系统设置 -> 用户和组。你也可以在终端窗口中使用命令 `system-config-users` 从命令行界面启动它。初始界面类似于图 29-1。

从此界面，你可以查看、修改和删除现有的用户和组账户，或创建新账户。要减少显示的账户列表或搜索特定账户，在按文本过滤（Filter by text）框中输入账户名称的首字母，并点击应用过滤器按钮。你可以通过点击工具栏上的刷新（Refresh）按钮来更新窗口。要获取上下文帮助，点击工具栏上的帮助（Help）按钮；若要查看整个 User Manager 手册，从工具栏选择帮助 ⮕ 手册（Manual）。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_762_0.png)

图 29-1 红帽 User Manager 主对话框。

## 创建用户账户

添加新用户：

- 1. 点击添加用户（Add User）按钮。出现如图 29-2 所示的创建新用户（Create New User）对话框。
- 2. 在用户（User）框中输入新账户名。
- 3. 在全名（Full Name）框中输入用户的全名。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_762_1.png)

图 29-2 添加用户。

- 4. 在密码（Password）和确认密码（Confirm Password）字段中输入用户的密码。
- 5. 从登录 shell（Login Shell）下拉框中选择备用 shell。
- 6. 通过编辑家目录（Home Directory）框更改家目录。
