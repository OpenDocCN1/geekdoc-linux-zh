
### 修改用户

Linux 提供了一些用于修改现有用户账户信息的实用工具。表 7-3 列出了这些工具。

#### 表 7-3 用户账户修改工具

| 命令 | 描述 |
| :------- | :---------- |
| `usermod` | 编辑用户账户字段，并指定主要和次要组成员身份 |
| `passwd` | 更改现有用户的密码 |
| `chpasswd` | 读取包含登录名和密码对的 文件，并更新密码 |
| `chage` | 更改密码的过期日期 |
| `chfn` | 更改用户账户的注释信息 |
| `chsh` | 更改用户账户的默认 shell |

每个工具都提供特定的功能来更改有关用户账户的信息。以下部分将描述这些实用工具中的每一个。

#### `usermod`

`usermod` 命令是用户账户修改工具中最强大的一个。它提供了用于更改 `/etc/passwd` 文件中大多数字段的选项。要做到这一点，您只需使用与您想要更改的值相对应的命令行参数即可。参数大多与 `useradd` 参数相同（例如，`-c` 用于更改注释字段，`-e` 用于更改过期日期，`-g` 用于更改默认登录组）。但是，一些额外的参数可能很有用：

- `-l` 用于更改用户账户的登录名
- `-L` 用于锁定账户，使用户无法登录
- 使用 `-p` 更改账户的密码
- 使用 `-u` 解锁账户，以便用户可以登录

`-L` 参数特别实用。使用它可以锁定账户，这样用户就无法登录，且无需删除账户和用户数据。若要恢复账户至正常状态，只需使用 `-u` 参数。

#### `passwd` 和 `chpasswd`

快速更改特定用户密码的方法是 `passwd` 命令：

```bash
# passwd test
Changing password for user test.
New UNIX password:
Retype new UNIX password:
password: all authentication tokens updated successfully.
#
```

如果仅单独使用 `passwd` 命令，它将更改您自己的密码。系统中的任何用户都可以更改自己的密码，但只有 root 用户可以更改他人的密码。

`-e` 选项是一种方便的方法，可强制用户在下次登录时更改密码。这允许您将用户的密码设置为简单值，然后强制他们更改为更复杂且容易记住的密码。

如果需要为系统中的大量用户进行批量密码更改，`chpasswd` 命令将非常有帮助。`chpasswd` 命令从标准输入读取登录名和密码对的列表（以冒号分隔），自动加密密码，并将其设置为用户账户的密码。您还可以使用重定向命令将包含 `username:password` 对的文件重定向到该命令：

```bash
# chpasswd < users.txt
#
```

#### `chsh`、`chfn` 和 `chage`

`chsh`、`chfn` 和 `chage` 实用程序用于特定的账户修改功能。`chsh` 命令允许您快速更改用户的默认登录 Shell。必须使用 Shell 的完整路径名，而不仅仅是 Shell 名称：

```bash
# chsh -s /bin/csh test
Changing shell for test.
Shell changed.
#
```

`chfn` 命令提供了一种标准方法，用于在 `/etc/passwd` 文件的注释字段中存储信息。而不是插入随机文本（如姓名或昵称），甚至保持注释字段为空，`chfn` 命令使用 Unix `finger` 命令所需的特定信息来存储注释字段中的数据。`finger` 命令允许您轻松查找 Linux 系统中人员的信息：

```bash
# finger rich
Login: rich          Name: Rich Blum
Directory: /home/rich   Shell: /bin/bash
On since Thu Sep 20 18:03 (EDT) on pts/0 from 192.168.1.2
No mail.
No Plan.
#
```

> 注意
>
> 出于安全考虑，大多数 Linux 发行版默认不安装 `finger` 命令。请注意，安装该命令可能会使系统面临攻击漏洞。

如果您不带任何参数使用 `chfn` 命令，它会提示您输入要填入注释字段的适当值：

```bash
# chfn test
Changing finger information for test.
Name []: Ima Test
Office []: Director of Technology
Office Phone []: (123)555-1234
Home Phone []: (123)555-9876
Finger information changed.
```

```bash
# finger test
Login: test Name: Ima Test
Directory: /home/test Shell: /bin/csh
Office: Director of Technology Office Phone:
(123)555-1234
Home Phone: (123)555-9876
Never logged in.
No mail.
No Plan.
#
```

如果您现在查看 `/etc/passwd` 文件中的条目，其内容如下：

```bash
# grep test /etc/passwd
test:x:504:504:Ima Test, Director of Technology, (123)555-1234, (123)555-9876:/home/test:/bin/csh
#
```

所有 `finger` 信息都整齐地存储在 `/etc/passwd` 文件条目中。

最后，`chage` 命令有助于管理用户账户的密码老化过程。设置单个值时有几个参数，如表 7-4 所示。

#### 表 7-4 chage 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `-d` | 设置自密码上次更改以来的天数。 |
| `-E` | 设置密码过期的日期。 |
| `-I` | 设置密码过期后不活动多少天锁定账户。 |
| `-m` | 设置两次密码更改之间的最小天数。 |
| `-M` | 设置密码有效的最大天数。 |
| `-W` | 设置密码过期前多少天显示警告消息。 |

`chage` 的日期值可以使用以下两种方法之一表示：

- `YYYY-MM-DD` 格式的日期
- 代表自 1970 年 1 月 1 日以来天数的数值

`chage` 命令的一个实用功能是可以为账户设置过期日期。利用此功能，您可以创建在特定日期自动过期的临时用户账户，而无需记住删除它们！过期账户与锁定账户类似。账户仍然存在，但用户无法用它登录。

## 使用 Linux 组

用户账户对于控制单个用户的安全非常有用，但不太适合让一组用户共享资源。为了实现这一点，Linux 系统使用了另一个称为*组*的安全概念。

组权限允许多个用户共享系统中对象的通用权限集，例如文件、目录或设备（稍后将在“解码文件权限”章节中详细介绍）。

Linux 发行版在处理默认组成员资格方面略有不同。一些 Linux 发行版仅创建一个组，其中包含所有用户账户作为成员。如果您的 Linux 发行版这样做，您需要小心，因为您的文件可能会被系统中的其他所有用户读取。其他发行版为每个用户创建独立的用户账户，以提供更高的安全性。

每个组都有唯一的 GID，与 UID 一样，它是系统中的唯一数值。除了 GID 之外，每个组都有唯一的组名称。有一些组实用程序可用于在 Linux 系统上创建和管理您自己的组。本节讨论组信息如何存储，以及如何使用组实用程序创建新组并修改现有组。

#### `/etc/group` 文件

与用户账户一样，组信息存储在系统中的文件中。`/etc/group` 文件包含系统中使用的每个组的信息。以下是典型 Linux 系统 `/etc/group` 文件中的几个示例：

```bash
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
rich:x:500:
mama:x:501:
katie:x:502:
jessica:x:503:
mysql:x:27:
test:x:504:
```

与 UID 一样，GID 使用特殊格式分配。用于系统账户的组分配 500 以下的 GID，用户组分配从 500 开始的 GID。`/etc/group` 文件使用四个字段：

- 组名
- 组密码
- GID
- 属于该组的用户账户列表

组密码允许非组成员通过使用密码暂时成为组成员。这个功能并不常用，但它确实存在。
