
接下来，使用 `passwd` 命令设置 Mary 的初始密码。它提示你输入两次密码。（这里显示的星号 * 表示你输入的密码。在你输入密码时，实际上不会显示任何内容。）

```bash
# password mary
Changing password for user mary.
New password: *****
Retype new password: *****
```

交叉引用：请参考第 14 章有关选择良好密码的提示。

在为 Mary 创建账户时，`useradd` 命令执行了若干操作：

- 读取 `/etc/login.defs` 文件以获取创建账户时使用的默认值。
- 检查命令行参数以确定要覆盖哪些默认值。
- 根据默认值和命令行参数在 `/etc/password` 和 `/etc/shadow` 文件中创建新用户项。
- 在 `/etc/group` 文件中创建任何新组项。
- 如果指定了 `-m`，则为用户创建家目录。
- 从 `/etc/skel` 复制任何文件到新的家目录。

`/etc/group` 文件包含组名、与其关联的组 ID 数字以及属于该组的用户列表。Fedora 或 RHEL 系统上的组允许多人共享访问权限，同时拒绝他人访问。如果你查看 `/etc/group` 文件，应该发现类似于如下的内容：

```
bin:x:1:
daemon:x:2:
sys:x:3:
adm:x:4:
tty:x:5:
disk:x:6:
lp:x:7:
mem:x:8:
kmem:x:9:
wheel:x:10:
nobody:x:99:
users:x:500
chris:x:501
sheeree:x:501
sales:x:601
```

组文件中的每行包含组名、与其关联的组 ID 数字以及用户列表。默认情况下，每个用户被添加到他们自己的组中，从 500 开始。注意，mary 被添加到 `wheel` 和 `sales` 组，而不是她自己的组。

mary 被添加到 `wheel` 组实际上具有重要意义。通过这样做，赋予了她使用 `sudo` 命令作为 root 用户运行命令的能力，前提是 `/etc/sudoers` 文件中的 `wheel` 行已取消注释（如第 10 章所述），这在默认情况下并不是。

在示例中，我们使用 `-g` 选项将 mary 分配到 `users` 组。如果你省略 `-g` 参数，默认行为是 `useradd` 创建一个与用户相同名称和 ID 数字的新组，并将其作为新用户的主组。例如，查看以下 `useradd` 命令：

```bash
# useradd -m -G wheel,sales -s /bin/tcsh -c "Mary Smith" mary
```

它将产生如下的 `/etc/passwd` 行：

```
mary:x:502:Mary Smith:/home/mary:/bin/tcsh
```

它还会产生如下的新的新组行：

```
mary:x:502:
```

用户 ID 和组 ID 字段现在具有相同的数量。如果你按照这种方式设置所有用户，将为系统中的每个用户都创建一个唯一的组，这允许用户之间共享文件时更高的灵活性。

## 使用用户管理器添加用户

如果你倾向于使用图形窗口来添加、更改和删除用户账户，可以使用用户管理器（User Manager）。要从 GNOME 桌面打开该窗口，请点击系统设置 -> 用户，或者在终端窗口中以 root 用户身份运行 `system-config-users`。图 11-1 显示该窗口的示例。

![](img/8aa80810fdd3df400bb7ee72b296baad_473_0.png)

**图 11-1：** 从用户管理器管理用户。

当你打开用户管理器窗口时，你会看到当前添加到你的计算机的所有普通用户列表。管理员用户（UID 1 到 499）不会显示。对于每个用户，你可以看到用户名、UID、主组、全名、登录 shell 和家目录。点击这些标题中的任意一个根据该信息对用户进行排序。

要从用户管理器窗口添加新用户，请执行以下操作：

1. 点击“添加用户”图标打开创建新用户窗口（参见图 11-2）。
2. 在以下字段中输入所需信息：
   - **用户名 (User Name)** — 描述用户的单个单词。通常，用户名为八个字符，全部小小写，包含用户的真实名、姓或（更常见的是）两者的组合（例如 jwones）。
   - **全名 (Full Name)** — 用户的全名（通常是名、中间名字母缩写和姓）。此名称通常仅用于显示，因此使用大写字母均可。
   - **密码 (Password)** — 用户的初始密码。（在用户首次登录新账户时，使用 `passwd` 命令要求其更改此密码。）
   - **确认密码 (Confirm Password)** — 再次输入密码，以确保输入正确。
   - **登录 shell (Login Shell)** — 用户从字符显示器登录 Fedora 或 RHEL 时看到的默认 shell（用于执行键入命令）。
   - **创建家目录 (Create home directory)** — 默认勾选此复选框，并自动创建用户的家目录（如“家目录”字段所示）。
   - **家目录 (Home Directory)** — 默认情况下，用户将在 `/home` 目录下获得一个以用户名命名的家目录。（例如，用户 sheeree 将被分配 `/home/sheeree` 作为其家目录。）如果你想将用户分配到不同的目录，请更改此字段。
   - **为用户创建私有组 (Create a private group for the user)** — 如果你想为该用户创建一个与用户同名的组，请勾选此复选框。名称将被添加到 `/etc/group` 文件。此功能称为用户私有组 (UPGs)。
   - **手动指定用户 ID (Specify user ID manually)** — 通常你不会勾选此框，这样系统就会自动为新用户分配 UID。新 ID 从 500 开始。然而，如果你想为用户分配特定的 UID（例如，如果你想让 UID 与网络上另一台计算机上的用户 UID 匹配），请点击此框并在 UID 框中输入你想使用的数字。

![](img/8aa80810fdd3df400bb7ee72b296baad_474_0.png)

3. 完成后点击确定。新用户被添加到 `/etc/passwd` 和 `/etc/group` 文件中。用户账户现在可以供该用户登录。

提示：使用用户私有组 (UPGs) 对于在多个用户之间共享文件目录很有处。这里有一个示例：

```
# useradd -m projectx
# mkdir /usr/local/x
# chown root.projectx /usr/local/x
# chmod 2775 /usr/local/x
# ls -id /usr/local/x
drwxwxrxr-2 root projectx 4096 Aug 18 01:54 /usr/local/x
```

在这个示例中，你创建了一个用户 `projectx`（组名为 `projectx`）。创建了 `/usr/local/x` 目录并使其由 root 和 `projectx` 组所有。为组设置了 setuid 位 (7)，为用户和组打开读/写权限 (7)，并为其他人打开读取和执行权限 (5)。将每个用户添加到你希望他们能够写入的组中（将 user 替换为你想添加的用户）。之后，无论用户的主组是什么，在 `/usr/local/x` 目录中创建的任何文件都可以被 `projectx` 中的任何人读取或修改。

## 设置用户默认值

`useradd` 命令和用户管理器窗口都通过读取 `/etc/login.defs` 来确定新账户的默认值。你可以通过使用文本编辑器手动编辑它们，或者运行带有 `-D` 参数的 `useradd` 命令来修改它们。如果你选择手动编辑文件，你将面对以下：

```
# 邮件箱所在的目录，或相对于家目录的文件名。如果同时使用两者，则 DIR 具有优先权。
# MAIL_DIR 用于邮件
MAIL_DIR /etc/mail

# 密码老化策略控制：
# PASS_MAX_DAYS 密码可以使用的最大天数。
# PASS_MIN_DAYS 密码更改之间允许的最小天数。
# PASS_MIN_LEN 最小接受长度。
# PASS_WARN_AGE 密码过期前的警告天数。
```

```
PASS_MAX_DAYS   9999
PASS_MIN_DAYS   0
PASS_MIN_LEN   5
PASS_WARN_AGE   7
```
