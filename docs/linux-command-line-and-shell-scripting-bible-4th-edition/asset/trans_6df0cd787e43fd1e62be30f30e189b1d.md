
密码尚未更改。

## 添加新用户

在 Linux 系统中添加新用户的主要工具是 **useradd**。该命令提供了一种便捷的方式，用于一次性创建新的用户账户并设置用户的 $HOME 目录结构。**useradd** 命令通过结合系统默认值和命令行参数来定义用户账户。要查看您的 Linux 发行版使用的系统默认值，请输入带有 **-D** 参数的 **useradd** 命令：

```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
#
```

> **注意**
>
> **useradd 命令的默认值是通过 /etc/default/useradd 文件设置的。此外，在 /etc/login.defs 文件中还定义了进一步的安全设置。您可以调整这些文件以更改 Linux 系统上的默认安全行为。**

如果未在命令行中指定默认值，**useradd** 命令在创建新用户账户时将使用 -D 参数所示的默认值。此示例显示了以下默认值：

-   新用户将被添加到一个公共组，其组 ID 为 100。
-   新用户将在 /home/$loginname$ 目录中创建一个 $HOME 账户。
-   当密码过期时，该账户不会被禁用。
-   新账户不会设置为在特定日期过期。
-   新账户将使用 bash shell 作为默认 shell。
-   系统会将 `/etc/skel` 目录的内容复制到用户的 `$HOME` 目录。
-   系统将在邮件目录中为该用户账户创建一个文件以接收邮件。

`useradd` 命令允许管理员创建默认的 `$HOME` 目录配置，然后将其作为模板来创建新用户的 `$HOME` 目录。这允许系统自动将默认文件放入每个新用户的 `$HOME` 目录中。在 Ubuntu Linux 系统中，`/etc/skel` 目录包含以下文件：

```
$ ls -al /etc/skel
total 32
drwxr-xr-x  2 root root  4096 2010-04-29 08:26 .
drwxr-xr-x 135 root root 12288 2010-09-23 18:49 ..
-rw-r--r--   1 root root   220 2010-04-18 21:51 .bash_logout
-rw-r--r--   1 root root  3103 2010-04-18 21:51 .bashrc
-rw-r--r--   1 root root   179 2010-03-26 08:31 examples.desktop
-rw-r--r--   1 root root   675 2010-04-18 21:51 .profile
$
```

您应该能从第 6 章“使用 Linux 环境变量”中认出这些文件。这些是 Bash shell 环境的标准启动文件。系统会自动将这些默认文件复制到您创建的每个用户的 `$HOME` 目录中。

您可以通过使用默认系统参数创建一个新的用户账户，然后查看新用户的 `$HOME` 目录来测试这一点：

```
# useradd -m test
# ls -al /home/test
total 24
drwxr-xr-x 2 test test  4096 2010-09-23 19:01 .
drwxr-xr-x 4 root root  4096 2010-09-23 19:01 ..
-rw-r--r--  1 test test   220 2010-04-18 21:51 .bash_logout
-rw-r--r--  1 test test  3103 2010-04-18 21:51 .bashrc
-rw-r--r--  1 test test   179 2010-03-26 08:31 examples.desktop
-rw-r--r--  1 test test   675 2010-04-18 21:51 .profile
#
```

在许多 Linux 发行版中，useradd 命令默认不会创建 $HOME 目录，但 -m 命令行选项指示它创建 $HOME 目录。您可以在 /etc/login.defs 文件中更改该行为。如您所见，在示例中，useradd 命令使用 /etc/skel 目录中包含的文件创建了新的 $HOME 目录。

> **注意**
>
> **要运行本章中的用户账户管理命令，您需要以特殊的 root 用户账户登录，或者使用 sudo 命令以 root 用户身份运行这些命令。**

如果您希望在创建新用户时覆盖默认值或行为，可以使用命令行参数来实现。这些参数如表 7-1 所示。

### 表 7-1 useradd 命令行参数

| 参数 | 描述 |
| :--- | :--- |
| -c comment | 在新用户的注释字段中添加文本。 |
| -d home_dir | 指定主目录的不同名称（除登录名外）。 |
| -e expire_date | 指定账户过期的日期，格式为 YYYY-MM-DD。 |
| -f inactive_days | 指定密码过期后多少天禁用账户。值为 0 表示密码过期后立即禁用账户；值为 -1 表示禁用此功能。 |
| -g initial_group | 指定用户登录组的组名或 GID。 |
| -G group ... | 指定用户所属的一个或多个辅助组。 |
| -k | 将 `/etc/skel` 目录内容复制到用户的 $HOME 目录（必须同时使用 `-m`）。 |
| -m | 创建用户的 $HOME 目录。 |
| -M | 不创建用户的 $HOME 目录（用于默认设置为创建该目录的情况）。 |
| -n | 使用与用户登录名相同的名称创建新组。 |
| -r | 创建系统账户。 |
| -p passwd | 指定用户账户的默认密码。 |
| -s shell | 指定默认登录 shell。 |
| -u uid | 为账户指定唯一的 UID。 |

如您所见，只需使用命令行参数，在创建新用户账户时就可以覆盖所有系统默认值。然而，如果您发现自己经常需要覆盖某个值，直接更改系统默认值会更容易。

您可以使用 -D 参数以及代表需要更改值的参数来更改系统默认的新用户值。这些参数如表 7-2 所示。

### 表 7-2 useradd 更改默认值参数

| 参数 | 描述 |
| --- | --- |
| -b default_home | 更改用户主目录的创建位置。 |
| -e expiration_date | 更改新账户的过期日期。 |
| -f inactive | 更改密码过期后多少天禁用账户。 |
| -g group | 更改使用的默认组名或 GID。 |
| -s shell | 更改默认登录 shell。 |

更改默认值非常简单：

```
# useradd -D -s /bin/tcsh
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/tcsh
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
#
```

现在，useradd 命令将在所有创建的新用户账户中使用 tcsh shell 作为默认登录 shell。

## 删除用户

如果您想从系统中删除用户，您需要使用 userdel 命令。默认情况下，userdel 命令仅从 /etc/passwd 和 /etc/shadow 文件中删除用户信息。它不会删除该账户在系统上拥有的任何文件。

如果使用 -r 参数，userdel 将删除用户的 HOME 目录以及用户的邮件目录。然而，系统中可能仍会有其他属于已删除用户账户的文件。在某些环境中，这可能是一个问题。

以下是使用 userdel 命令删除现有用户账户的示例：

```
# userdel -r test
# ls -al /home/test
ls: cannot access /home/test: No such file or directory
#
```

使用 -r 参数后，用户的旧 /home/test 目录不再存在。

> **警告**
>
> 在拥有大量用户的环境中使用 -r 参数时要小心。你永远不会知道用户是否在 HOME 目录中存储了对他人或其他程序重要的文件。在删除用户的 HOME 目录之前，务必进行检查！

## 修改用户

Linux 提供了一些用于修改现有用户账户信息的实用工具。表 7-3 列出了这些工具。

### 表 7-3 用户账户修改工具

| 命令 | 描述 |
| :------- | :---------- |
| usermod | 编辑用户账户字段，并指定主要和次要组成员身份 |
| passwd | 更改现有用户的密码 |
| chpasswd | 读取包含登录名和密码对的 文件，并更新密码 |
| chage | 更改密码的过期日期 |
| chfn | 更改用户账户的注释信息 |
| chsh | 更改用户账户的默认 shell |

每个工具都提供特定的功能来更改有关用户账户的信息。以下部分将描述这些实用工具中的每一个。

### usermod

usermod 命令是用户账户修改工具中最强大的一个。它提供了用于更改 /etc/passwd 文件中大多数字段的选项。要做到这一点，您只需使用与您想要更改的值相对应的命令行参数即可。参数大多与 useradd 参数相同（例如，-c 用于更改注释字段，-e 用于更改过期日期，-g 用于更改默认登录组）。但是，一些额外的参数可能很有用：

-   -l 用于更改用户账户的登录名
-   -L 用于锁定账户，使用户无法登录

