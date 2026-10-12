

```text
wheel::10:root,joe,mary
mail::12:mail
news::13:news
uucp::14:uucp
man::15:
games::20:
gopher::30:
dip::40:
ftp::50:
nobody::99:
users::100:
sales::500:bob,jane,joe,mary
```

组文件中的每一行包含组名、与其关联的组 ID 号以及该组中的用户列表。请注意，mary 被添加到了 wheel 组和 sales 组中。尽管 Mary 的主要组是 users，但不需要在那里添加她的名字。当你包含 -G 标志时，useradd 命令已经为你完成了这一步。

将 mary 添加到 wheel 组实际上具有重要意义。通过这样做，我们授予她使用 sudo 命令以 root 用户身份运行命令的能力（前提是已按照第 10 章中的描述配置了 sudo）。

> 交叉参考：有关 su 和 sudo 命令的说明，请参见第 10 章。

在这个示例中，我们使用 -g 选项将 mary 分配到 users 组。如果省略 -g 参数，useradd 的默认行为是创建一个与用户同名且 ID 号相同的新组，并将其分配为新用户的主要组。例如，请查看以下 useradd 命令：

```text
# useradd -m -G wheel,sales -s /bin/tcsh -c "Mary Smith" mary
```

这将导致 /etc/passwd 文件中出现类似以下内容的行：

```text
mary:x:500:500:Mary Smith:/home/mary:/bin/tcsh
```

它还会生成类似以下内容的新组行：

```text
mary:x:500:
```

注意，此时用户 ID 和组 ID 字段具有相同的数值。如果你以这种方式设置所有用户，系统中的每个用户将拥有一个唯一的组，这可以增加用户之间共享文件的灵活性。

### 使用 Red Hat 用户管理器添加用户

如果你更喜欢使用图形界面来添加、修改和删除用户账户，可以使用 Red Hat 用户管理器窗口。要从 GNOME 桌面打开该窗口，请单击“程序” → “系统” → “用户管理器”（或者以 root 用户身份在终端窗口中输入 redhat-config-users）。图 11-1 显示了该窗口的一个示例：

![](img/1744bde8c889adfab3fc911e1687fecf_439_0.png)

图 11-1：通过 Red Hat 用户管理器窗口管理用户。

当你打开 Red Hat 用户管理器窗口时，你会看到当前已添加到计算机上的所有普通用户的列表。管理员用户（UID 1 至 100）不会显示。对于每个用户，你可以看到用户名、UID、主要组、全名、登录 shell 和主目录。单击其中任何标题可以根据该信息对用户进行排序。

要从 Red Hat 用户管理器窗口添加新用户，请执行以下操作：

1.  单击“新用户”图标。会出现一个“创建新用户”窗口，如图 11-2 所示：

    ![](img/1744bde8c889adfab3fc911e1687fecf_439_1.png)

    图 11-2：创建新用户窗口

2.  输入以下信息：
    -   用户名 — 用于描述用户的单个单词。通常，用户名全为小写，包含用户的真实名字、姓氏，或者（更常见的是）两者的组合（例如 jwjones）。
    -   全名 — 用户的完整姓名（通常包括名字、中间名首字母和姓氏）。此名称通常仅用于显示，因此使用大写字母和小写字母均可。
    -   密码 — 用户的初始密码。（请用户在首次登录新账户时，使用 passwd 命令更改此密码。）
    -   确认密码 — 再次输入相同的密码，以确保你输入正确。
    -   登录 Shell — 用户在打开终端窗口、虚拟窗口或其他 shell 提示符时看到的默认 shell（用于输入命令）。
    -   创建主目录 — 默认情况下，此框已被选中，用户的家目录（如主目录字段所示）会自动创建。
    -   主目录 — 默认情况下，用户将在 /home 目录下获得以其用户名为名的家目录。（例如，用户 sheree 将被分配 /home/sheree 作为其家目录。）如果你想将用户分配到不同的家目录，请更改此字段。
    -   为此用户创建新组 — 如果你想为一个与用户同名的组创建专属于此用户的组，请勾选此框。该名称将被添加到 /etc/group 文件中。
    -   手动指定用户 ID — 通常，你不会勾选此框，以便为新用户自动分配 UID。普通用户的新 UID 从 500 开始。但是，如果你想为特定用户分配特定的 UID（例如，如果你希望将 UID 与网络中另一台计算机上该用户的 UID 匹配），请勾选此框，并在 UID 框中输入你想使用的数字。
3.  完成后单击“确定”。新用户将被添加到 /etc/passwd 和 /etc/group 文件中。现在，该用户账户可供该用户登录使用。

### 设置用户默认值

useradd 命令和 Red Hat 用户管理器窗口都通过读取 /etc/login.defs 文件来确定新账户的默认值。你可以通过使用标准文本编辑器手动编辑该文件，或者通过运行带有 -D 选项的 useradd 命令来修改这些默认值。如果你选择手动编辑该文件，你将面对以下内容：

```text
# *REQUIRED*
# Directory where mailboxes reside, _or_ name of file, relative
# to the home directory. If you _do_ define both, MAIL_DIR
# takes precedence.
# QMAIL_DIR is for Qmail
#
#QMAIL_DIR Maildir
MAIL_DIR /var/spool/mail
#MAIL_FILE .mail

# Password aging controls:
#
# PASS_MAX_DAYS Maximum number of days a password may be used.
# PASS_MIN_DAYS Minimum number of days allowed between password changes.
# PASS_MIN_LEN   Minimum acceptable password length.
# PASS_WARN_AGE Number of days warning given before a password
# expires.
#
PASS_MAX_DAYS		99999
PASS_MIN_DAYS		0
PASS_MIN_LEN		5
PASS_WARN_AGE		7

#
# Min/max values for automatic uid selection in useradd
#
UID_MIN			500
UID_MAX			60000

#
# Min/max values for automatic gid selection in groupadd
#
GID_MIN			500
GID_MAX			60000

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for users by
# default. On RH systems, we do. This option is ORed with on
# the -m flag useradd command line.
#
CREATE_HOME yes
```

useradd 命令会忽略空行和以井号（#）开头的注释。所有其他行都包含关键字/值对。例如，第一个非注释行是关键字 **MAIL_DIR**，后跟一些空白和值 `/var/spool/mail`。这告诉 useradd 初始用户电子邮件信箱应在该目录中创建。随后是其他关键字/值对，它们允许你自定义自动分配的用户 ID 号或组 ID 号的有效范围。每个关键字之前都有一个解释该关键字用途的注释部分。更改默认值很简单，只需编辑与该关键字关联的值，然后保存 `login.defs` 文件即可。

如果你想要查看默认值，请按照以下方式输入带有 -D 选项的 useradd 命令：

```text
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
```

你也可以使用 -D 选项来更改默认值。当以此标志运行时，`useradd` 不会实际创建新的用户账户；相反，它将额外提供的选项保存为 `/etc/login.defs` 中的新默认值。并非所有 useradd 选项都可以与 -D 选项结合使用。你只能使用表 11-2 中列出的五个选项。

#### 表 11-2：用于更改用户默认值的 useradd 选项

| 选项 | 描述 |
| :--- | :--- |
| -b `default_home` | 设置创建用户家目录的默认目录。用要使用的目录名替换 `default_home`。通常这是 `/home`。 |
| -e `default_expire_date` | 设置用户账户被禁用的默认过期日期。`default_expire_date` 值应替换为 MM/DD/YYYY 形式的日期——例如，10/15/2001。 |
| -f `default_inactive` | 设置密码过期后多少天禁用账户。用代表天数的数字替换 `default_inactive`。 |
| -g `default_group` | 设置新用户将被放置的默认组。通常 `useradd` 会创建一个与用户同名且 ID 号相同的新组。用要使用的组名替换 `default_group`。 |
| -s `default_shell` | 设置新用户的默认 shell。通常这是 `/bin/sh`。用你希望作为新用户默认 shell 的完整路径替换 `default_shell`。 |

要设置任何默认值，首先提供 -D 选项；然后添加你想要设置的任何默认值。例如，要将默认家目录位置设置为 `/home/everyone`，将默认 shell 设置为 `/bin/tcsh`，请输入以下内容：

```text
# useradd -D -b /home/everyone -s /bin/tcsh
```

