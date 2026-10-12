
## /etc/default/useradd 配置说明

该文件中的各项配置如下：

- **GROUP=100.** 指定默认 GID 为 100。此值仅在你禁用（使用 `-n` 选项）默认私有组（与新用户同名）时使用。你也可以指定组名称而不是数字值。在此行中指定的值必须存在于 `/etc/group` 中。你可以按如下方式更改此值：
  ```bash
  useradd -D -g newsgroup name or GID
  ```
  其中 *newsgroup name* 和 *GID* 是相应的值。

- **HOME=/home.** 指定新用户默认的最高级主目录。例如，当你创建一个名为 *joe* 的新用户时，默认主目录为 */home/joe*。你可以将此值更改为符合你需求的目录。请确保该目录已存在。你可以按如下方式更改此值：
  ```bash
  useradd -D -d directory
  ```

- **INACTIVE=-1.** 指定账户在密码过期后多少天变为不活跃。这仅在你使用影子密码时有效。默认值 `-1` 表示账户永不会变为不活跃。你可以按如下方式更改此值：
  ```bash
  useradd -D -f number of days
  ```

- **EXPIRE=-** 指定何时禁用账户。这仅在你使用影子密码时有效。默认情况下，账户永远不会被禁用。你可以按如下方式更改此值：
  ```bash
  useradd -D -e MM/DD/YY
  ```

- **SHELL=/bin/bash.** 指定默认登录 Shell 路径。你可以按如下方式更改此值：
  ```bash
  useradd -D -s /bin/tosh
  ```

注意，useradd 程序不会检查你指定的路径是否为有效的 Shell，甚至是否不存在。因此，请确保你指定的路径是有效的 Shell 并列在 `/etc/shells` 文件中。

- **SKELETON=/etc/skel.** 指定保存各种用户配置文件的目录，例如 Shell 的 dot 文件、X Window 等。此目录中的文件将被复制到新用户账户的新主目录中。通常，你不希望将此路径更改为其他目录。另一方面，如果你确实想要更改它，你必须使用编辑器修改 `/etc/default/useradd` 文件，或者简单地创建一个指向目标目录的符号链接 `/etc/skel`。

如果你使用影子密码，另一个默认配置文件 `/etc/login.defs` 用于创建用户账户。列表 5-3 展示了此文件的示例。

### 列表 5-3 /etc/login.defs 文件示例

```bash
#REQUIRED

#  Directory where mailboxes reside, _or_ name
#  of file, relative to the home directory.
#  If you _do_ define both, MAIL_DIR takes precedence.

    QMAIL_DIR  is for Qmail

#QMAIL_DIR     Maildir
MAIL_DIR  /var/spool/mail

#MAIL_FILE    .mail
# Password aging controls:

#   PASS_MAX_DAYS  Maximum number of days a
#                  password may be used.
#
#   PASS_MIN_DAYS  Minimum number of days allowed
#                  between password changes.
#
#   PASS_MIN_LEN   Minimum acceptable password length.
#
#   PASS_WARN_AGE  Number of days warning given before
#                  a password expires.

PASS_MAX_DAYS  99999
PASS_MIN_DAYS  0
PASS_MIN_LEN   5
PASS_WARN_AGE  7

#
# Min/max values for automatic uid
# selection in useradd
#
UID_MIN  500
UID_MAX  60000

#
# Min/max values for automatic gid
# selection in groupadd
#
GID_MIN  500
GID_MAX  60000

#
# Require password before chfn/chsh can make
# any changes.
#
CHFN_AUTH  yes

#
# Don't allow users to change their "real name"
# using chfn.
#
CHFN_RESTRICT  yes

#
# If defined, this command is run when removing a user.
# It should remove any at/cron/print jobs etc. Owned by
# the user to be removed (passed as the first argument).
#
#USERDEL_CMD /usr/sbin/userdel_local

#
# If useradd should create home directories for
# users by default on RH systems, we do. This option is
# ORed with the -m flag on useradd command line.
#
CREATE_HOME yes
```

由于该文件中的注释足以解释配置细节，因此这里不再进一步讨论。

## 使用 linuxconf 管理用户

linuxconf 命令可用于执行所有用户管理任务。本节使用基于 X Window 的 linuxconf 界面。

### 添加新用户账户

要访问 linuxconf 中的用户管理界面，请选择 Config → User accounts → Normal → User accounts 选项。
要添加新用户，请遵循以下步骤：

1. 点击窗口右侧的 Add 按钮。将出现一个新窗口，其中包含多个选项卡。
2. 在 Base Info 选项卡中，输入 Login name (username)、Full name、group、Supplementary groups (optional)、Home directory (optional)、Command interpreter (optional) 和 User ID (optional)。你还可以通过取消选中 This account is enabled 复选框来选择创建此账户但尚未启用它。
3. 你可以使用其他选项卡（Params 和 Privileges）来设置有关此账户的附加信息。Privileges 选项卡中发现的特权选项仅适用于 linuxconf。换句话说，如果你为普通账户分配权限，该权限仅在用户能够运行 linuxconf 时适用。例如，如果你希望此用户能够运行 linuxconf，你可以在 Privileges 选项卡中选择允许这样做。
4. 在你选择适当的权限（如果有）后，点击 Accept 以添加用户。请注意，用户不会立即被添加，直到你通过 Control -> Control Panel -> Activate configuration 选项告知 linuxconf 激活配置，或者允许它在退出应用程序前激活配置。

### 修改现有用户账户

要在 linuxconf 中修改用户账户，请执行以下操作：

1. 在 linuxconf 窗口左侧选择 Config -> User accounts -> Normal -> User accounts。
2. 在右侧点击账户名称，你将看到一个包含所有预加载用户账户信息的标签。修改任何你想更改的内容，然后使用 Control -> Control Panel -> Activate configuration 选项立即激活更改，或者在退出应用程序时激活它们。

### 删除或禁用现有用户账户

要删除或禁用用户账户，请执行以下操作：

1. 选择 Config -> User accounts -> Normal -> User accounts 选项。
2. 在右侧点击账户名称，你将看到一个包含所有预加载账户信息的标签。要删除此账户，点击 Del 按钮。要禁用它，取消选中 This account is enabled 复选框。

### 添加、修改和删除组

要添加、修改或删除组，请执行以下操作：

1. 选择 Config -> User accounts -> Normal -> Group definitions 选项。
2. 要添加新组，点击 Add。这将打开一个新窗口。输入名称，可选地输入 GID、成员等。点击 Accept。当你激活在 linuxconf 中做出的更改时，新组将生效。
3. 要修改现有组，点击现有组名称。将出现一个新标签，其中包含所选组的信息预加载。进行必要的更改并点击 Accept。当你激活在 linuxconf 中做出的更改时，修改后的组将生效。
4. 要删除现有组，点击现有组名称。将出现一个新标签，其中包含所选组的信息预加载。点击 Delete。当你激活在 linuxconf 中做出的更改时，删除将生效。

虽然 linuxconf 试图使用户管理变得非常简单，但当你更改系统中的某些内容时，它往往会失效。例如，当我升级我的 SMTP 邮件传输代理 (sendmail) 时，linuxconf 的用户管理方面不再那么好用。它无法定位随 sendmail 提供的程序 (makemap)，因此每次我想要添加、修改或删除用户时，它都会不断询问我（即使我指定了该程序的路径）。在我升级到最新版本后，问题得到了解决。

## 对用户使用磁盘配额

在多服务器系统上，磁盘空间可能是一种相当稀缺的资源。经验表明，只要插入新驱动器并提供大量空间，用户往往会迅速用完这些空间。因此，你添加得越多，你就需要得越多。确保系统拥有足够磁盘空间的最好方法是强制实施磁盘配额。本节将解释如何操作。

