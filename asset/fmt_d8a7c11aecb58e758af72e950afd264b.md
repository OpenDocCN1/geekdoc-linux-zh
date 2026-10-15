
```
01 * 4 * * root-roots /etc/cron.hourly
02 * 4 * * root-roots /etc/cron.daily
22 * 4 * * root-roots /etc/cron.weekly
42 4 1 * * root-roots /etc/cron.monthly
```

前几行为文件中列出的任务设置了几个环境变量。`MAILTO` 环境变量指定了接收文件中 cron 任务输出邮件的用户。

# 336 Linux 任务调度

以 `#` 开头的行是注释行。`run-parts` 注释后的四行代码会在不同时间执行位于 `/usr/bin` 下的 `run-parts` shell 脚本，并将目录名称作为参数。`/etc/cron.hourly`、`/etc/cron.daily`、`/etc/cron.weekly` 和 `/etc/cron.monthly` 都是目录。表 1-11 列出了存放这些脚本的目录以及它们执行的内容。

| 表 1-11 | cron 任务脚本目录 |
|---|---|
| 目录名称 | 脚本执行内容 |
| /etc/cron.hourly | 每小时 |
| /etc/cron.daily | 每天 |
| /etc/cron.weekly | 每周 |
| /etc/cron.monthly | 每月一次 |

# 338 添加用户账户

除了 root 之外创建其他用户账户始终是一个好主意。即使你是系统的唯一用户，以低权限用户的身份登录也是良好的做法，因为你不会无意中损坏任何重要的系统文件。如有必要，你可以输入 `su -` 以 root 身份登录，然后执行系统管理任务。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_357_0.png)

## 使用 GUI 用户管理器管理用户账户

大多数 Linux 发行版都带有用于管理用户账户的 GUI。你可以使用该 GUI 添加新用户账户。该工具显示当前用户账户的列表，并有一个“添加”（Add）按钮用于添加新用户。为了说明，图 2-1 显示了 OpenSUSE 的 YaST 界面。

图 2-1: 在 SUSE 中，从 YaST 控制中心左侧选择“安全与用户”（Security and Users）类别，然后点击窗口右侧的“用户和组管理器”（User and Group Manager）图标。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_357_1.png)

无论使用什么 GUI 工具，基本步骤如下：

- 1. 点击添加用户（Add User）按钮。

对话框提示你输入有关新用户账户用户名和密码变量的信息，如图 2-2 所示。

## 添加用户账户

![](img/71f80d7808bf5b5ad1239cc29be7bab2_358_0.png)

图 2-2: 你可以通过提供所需的变量来创建账户。

## 2. 输入所需信息。

GUI 工具会负责添加新用户账户。

## 3. （可选）点击新用户的其他标签页之一（参考图 2-2）以配置额外信息。

“详细信息”（Details）标签页（如图 2-3 所示）允许你覆盖主目录、shell 和 ID 信息的默认值。

“密码设置”（Password Settings）标签页（如图 2-4 所示）允许你覆盖密码配置的默认值。插件可用于许多参数，但通常用于配额配置（例如文件大小限制和可以创建的 inode 数量）：

- 软限制（Soft limits）会警告用户。
- 硬限制（Hard limits）会停止用户。

> 提示 除用户数据（User Data）以外的标签页用于覆盖系统默认值。如果你想更改系统默认值，请在用户和组管理界面中更改变量。

## 340 添加用户账户

![](img/71f80d7808bf5b5ad1239cc29be7bab2_359_0.png)

图 2-3:

使用“详细信息”配置用户账户定义默认值之外的设置。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_359_1.png)

图 2-4:

使用“密码设置”配置新用户账户定义默认值之外的设置。

## 添加用户账户

注意用于添加新用户的工具被称为“用户和组管理”（User and Group Management），因为它可以配置两种类型的账户：用户和组。选择“组”而不是“用户”允许你向 `/etc/group` 添加新组，如图 2-5 所示。

![](img/71f80d7808bf5b5ad1239cc29be7bab2_360_0.png)

图 2-5: 组可以类似于用户进行创建和管理。

要添加新用户账户，点击“添加”按钮并在“新本地用户”（New Local User）窗口中输入要求的信息。填写所需信息（包括组配额的任何插件），然后点击“确定”按钮。

注意，图 2-2 中新添加的用户账户现在出现在“组成员”（Group Members）面板的用户列表中，并可以与其他用户一起添加到组中。

如果你愿意，可以添加更多用户或组账户。完成后，点击“确定”按钮以创建你添加的任何新账户；然后会自动退出。

默认情况下，YaST 将所有本地用户置于名为 `users` 的组中。有时你想成为另一个组的成员，以便该用户可以访问该组拥的文件。将用户添加到另一个组很容易。例如，将用户名 `kdulaney` 使用 `wheel` 组，在终端窗口中输入以下命令：

```
usermod -G wheel kdulaney
```

## 342 添加用户账户

> 提示 要删除用户账户，点击用户账户列表中的用户名，然后点击“移除”（Remove）或“删除”（Delete）按钮。

## 使用命令管理用户账户

如果你在文本终端工作，可以使用 `useradd` 命令创建新用户账户。按照以下步骤为新用户添加账户：

- 1. 以 root 身份登录

如果你尚未以 root 登录，输入 `su -` 成为 root

- 2. 输入带有 `-c` 选项的以下 useradd 命令创建账户：

`/usr/sbin/useradd -c "Kristin Delaney" kdulaney`

- 3. 使用 `passwd` 命令设置密码，如下：

`passwd kdulaney`

会被提示输入两次密码。如果你输入了一个别人容易猜到的密码，密码程序会责备你并建议你使用更复杂的密码。

`useradd` 命令通过 `-c` 选项创建账户：

`/usr/sbin/useradd -c "Kristin Delaney" kdulaney`

使用 `passwd` 命令设置密码，如下：

`passwd kdulaney`

会被提示输入两次密码。如果你输入了一个别人容易猜到的密码，密码程序会责备你并建议你使用更复杂的密码。

`useradd` 命令通过 `-c` 选项创建账户：

`/usr/sbin/useradd -c "Kristin Delaney" kdulaney`

使用 `passwd` 命令设置密码，如下：

`passwd kdulaney`

会被提示输入两次密码。如果你输入了一个别人容易猜到的密码，密码程序会责备你并建议你使用更复杂的密码。

```
usermod -g root
```

## 理解 /passwd 文件

`/etc/passwd` 文件是所有用户账户的列表。每行有七个字段，用冒号分隔。这里是一个典型的 /passwd 条目：

```
kdulaney:x:1000:1000:Kristin Delaney:/home/kdulaney:/bin/bash
```

| 表 2-1 | /passwd 中的字段 |
| :--- | :--- |
| 用户名 | 数字用户名（可以超过 8 个字符）。 |
| 密码 | 存在时，x 表示密码存储在 /etc/shadow 文件中。 |
| UID | 作为用户标识符的唯一数字（UID 1 到 999 保留给系统）。 |
| GID | 用户所属组的默认 GID（0 归 root）。 |
| GECO | 关于用户的可选信息（finger 命令使用此字段）。 |
| 主目录 | 用户主目录的名称。 |
| shell | 用户登录时执行的命令解释器（shell），例如 bash (/bin/bash)。 |

`useradd` 命令查询配置文件以获取有关新用户的各种默认信息：

- `/etc/default`: 指定默认 shell（如 /bin/bash）和主目录位置。
- `/etc/login.defs`: 提供自动创建用户的默认参数。
- `/etc/skel`: 包含创建主目录时包含的文件。

你可以使用 `userdel` 命令删除用户账户。只需在提示符输入 `userdel username`，其中 username 是要删除的用户名。要删除主目录，使用 `userdel -r`。

## 344 管理组

组是用户所属的实体。组有一个名称和一个标识符（ID）。在定义组后，用户可以属于这些组中的一个或多个。
