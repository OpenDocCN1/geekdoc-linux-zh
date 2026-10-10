

## 图 11-1：在用户管理器窗口中管理用户。

![图 11-1](img/fb202c163797a743c3c6cf236316bc96_508_0.png)

若要从用户管理器窗口添加新用户，请执行以下操作：

- 单击“添加用户”图标以打开“创建新用户”窗口（参见图 11-2）。

![图 11-2](img/fb202c163797a743c3c6cf236316bc96_508_1.png)

**图 11-2：创建新用户窗口**

- 在以下字段中输入所需信息：
    - **用户名** — 描述用户的单个单词。通常，用户名由八个字符组成，全部小写，包含用户的真实名、姓，或（更常见的）二者的组合（例如 jjones）。
    - **全名** — 用户的全名（通常是名、中间名首字母和姓）。此名称通常仅用于显示，因此使用大写和小写字母均可。
    - **密码** — 用户的初始密码。（请用户在首次登录新账户时使用 `passwd` 命令更改此密码。）
    - **确认密码** — 再次输入密码，以确保输入正确。
    - **登录 Shell** — 当用户首次通过字符界面登录 Fedora 或 RHEL 时看到的默认 shell（用于输入键入的命令）。
    - **创建主目录** — 默认情况下，选中此复选框，并自动创建用户的主目录（如主目录字段所示）。
    - **主目录** — 默认情况下，用户在 `/home` 目录下获得以其用户名命名的主目录。（例如，用户 *sheree* 的主目录将被分配为 `/home/sheree`。）如果您想将用户分配给不同的主目录，请更改此字段。
    - **为用户创建私有组** — 如果您希望为此用户创建一个与用户名同名的组，请勾选此复选框。该名称将被添加到 `/etc/group` 文件中。此功能称为用户私有组（UPGs）。
    - **手动指定用户 ID** — 通常不会勾选此复选框，以便为新用户自动分配 UID。普通用户的新 UID 从 500 开始。然而，如果您想为用户分配特定的 UID（例如，如果您希望与网络中另一台计算机上的用户 UID 匹配），请选择此复选框并在 UID 框中输入要使用的数字。
    - **手动指定组 ID** — 与用户 ID 类似，通常组 ID 会自动分配。然而，您可以分配不同的 GID，将用户分配到特定组。
- 完成后单击“确定”。新用户将被添加到 `/etc/passwd` 和 `/etc/group` 文件中。该用户账户现在可供该用户登录。

**提示：** 使用用户私有组（UPGs）可以方便地在多个用户之间共享文件目录。以下是一个示例：

```bash
# useradd -m projectx
# mkdir /usr/local/x
# chown root.projectx /usr/local/x
# chmod 2775 /usr/local/x
# ls -ld /usr/local/x
drwxrwsr-x 2 root projectx 4096 Aug 18 01:54 /usr/local/x
# gpasswd -a nextuser projectx
```

在此示例中，您创建了一个名为 `projectx` 的用户（并附带名为 `projectx` 的组）。创建 `/usr/local/x` 目录，并将其所有者设置为 root 用户和 `projectx` 组。为组打开 setgid 位（2），为用户和组打开完全读/写/执行权限（77），为其他所有用户打开读和执行权限（5）。将每个用户添加到您希望其能够写入 `project` 目录的组中（将 `nextuser` 替换为要添加的用户）。之后，无论用户的主组是什么，用户在 `/usr/local/x` 目录中创建的任何文件都可以被 `projectx` 组中的任何人读取或修改。

## 设置用户默认值

`useradd` 命令和用户管理器窗口都通过读取 `/etc/login.defs` 文件来确定新账户的默认值。您可以通过使用标准文本编辑器手动编辑该文件，或运行带有 `-D` 选项的 `useradd` 命令来修改这些默认值。如果您选择手动编辑该文件，您看到的是以下内容：

```text
# *REQUIRED*
# Directory where mailboxes reside, or name of file, relative to the
# home directory. If you define both, MAIL_DIR takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR       /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed between password changes.
# PASS_MIN_LEN Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password
# expires.

PASS_MAX_DAYS  99999
PASS_MIN_DAYS  0
PASS_MIN_LEN   5
PASS_WARN_AGE  7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN        500
UID_MAX        60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN        500
GID_MAX        60000

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for users by default.
# On RH systems, we do.  This option is overridden with the -m flag on
# useradd command line.

CREATE_HOME yes
# The permission mask is initialized to this value. If not
# specified, the permission mask will be initialized to 022.
UMASK            077

# This enables userdel to remove groups if no members exist.
#
USERGROUPS_ENAB yes
# Use MD5 or DES to encrypt password? RedHat use MD5 by default.
MD5_CRYPT_ENAB yes
```

空行和以井号（#）开头的注释将被忽略。所有其他行都包含关键字/值对。例如，关键字 MAIL_DIR 后面跟着一些空白和值 /var/spool/mail。这告诉 useradd 初始用户电子邮件邮箱将在该目录中创建。接下来是允许自定义自动分配的用户 ID 号或组 ID 号的有效范围的行。每个关键字前都有一个解释该关键字用途的注释部分。修改默认值只需编辑与该关键字关联的值，然后保存 login.defs 文件即可。

如果您想查看默认值，请按如下所示输入带有 -D 选项的 useradd 命令：

```bash
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
CREATE_MAIL_SPOOL=yes
```

您也可以使用 -D 选项更改默认值。当使用此标志运行时，useradd 不会实际创建新的用户账户；相反，它将额外提供的选项保存为 /etc/login.defs 中的新默认值。并非所有的 useradd 选项都可以与 -D 选项配合使用。您只能使用表 11-2 中列出的五个选项。

**表 11-2：用于更改用户默认值的 useradd 选项**

| 选项 | 描述 |
| :-- | :-- |
| -b default_home | 设置创建用户主目录的默认目录。将 default_home 替换为要使用的目录名。通常这是 /home。 |
| -e default_expire_date | 设置用户账户被禁用的默认到期日期。default_expire_date 值应替换为 MM/DD/YYYY 格式的日期——例如，10/15/2007。 |
| -f default_inactive | 设置密码过期后禁用账户的天数。将 default_inactive 替换为代表天数的数字。 |
| -g default_group | 设置新用户将被放置的默认组。在 Fedora 中，useradd 会创建一个与用户具有相同名称和 ID 号的新组，因此此值被忽略。要为某用户设置不同的主组，您必须在命令行上使用 -g 选项显式设置。 |
| -s default_shell | 设置新用户的默认 shell。通常这是 /bin/bash。将 default_shell 替换为您希望作为新用户默认的 shell 的完整路径。 |

要设置任何默认值，请先给出 -D 选项；然后添加您要设置的任何默认值。例如，要将默认主目录位置设置为 /home/everyone 并将默认 shell 设置为 /bin/tcsh，请输入以下内容：

```bash
# useradd -D -b /home/everyone -s /bin/tcsh
```

除了设置用户默认值外，管理员还可以创建默认文件，这些文件将被复制到每个用户的主目录中以供使用。这些文件可以包括登录脚本和 shell 配置文件（如 .bashrc）。以下各节描述了这些文件中的几个。

### 提供初始登录脚本

许多 Linux 应用程序，包括命令 shell 本身，在启动时都会读取配置文件。传统做法是，这些配置文件存储在用户的主目录中。这样，每个用户都可以定制命令 shell 和其他应用程序的行为，而不会影响其他用户的行为。这样，可以从 /etc/profile 分配全局默认值，然后由用户的个人文件来增强这些设置。

例如，bash 命令 shell 在启动时会在当前用户的主目录中查找名为 .bashrc 的文件。同样，tcsh 命令 shell 也会查找一个文件

