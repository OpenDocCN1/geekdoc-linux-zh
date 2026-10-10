
# useradd -c "Joe Smith"

```
> **提示：** 当您选择用户名时，以数字开头（例如 `06smith`）。此外，最好使用小写字母，不要包含控制字符或空格，且长度最多为八个字符。`adduser` 命令允许多达 32 个字符，但某些应用程序无法处理过长的用户名。像 `ps` 等工具会显示 UID 而不是过长的名称。拥有 `Jsmith` 和 `jsmith` 用户可能会导致不区分大小写的程序（如 `sendmail`）产生混淆。此外，某些非常老旧应用程序可能无法处理超过八个字符的用户名。
```

接下来，使用 `passwd` 命令为 Joe 设置初始密码。密码命令会提示您输入两次密码。（此处用星号 `*` 表示您输入的密码。在输入密码时，实际上不会显示任何内容。）

```
# passwd joe

Changing password for user joe.

New password: ***********

Retype new password: ***********
```

**交叉引用：** 请参阅第 14 章获取选择良好密码的提示。

在为 Joe 创建账户时，`useradd` 命令执行了若干操作：

- 读取 `/etc/login.defs` 文件以获取创建账户时的默认值。
- 检查命令行参数以确定要覆盖哪些默认值。
- 根据默认值和命令行参数在 `/etc/passwd` 和 `/etc/shadow` 文件中创建新用户条目。
- 在 `/etc/group` 文件中创建任何新组条目。
- 根据用户名称创建主目录并将其放置在 `/home` 目录下。
- 将位于 `/etc/skel` 中的任何文件复制到新的主目录中。这通常包括登录和应用程序脚本。

上述示例仅使用了 `useradd` 可用选项之一。大多数账户设置使用默认值分配。以下是一个包含更多选项的示例：

```
# useradd -m -g -G wheel,sales -s /bin/bash "Mary Smith"
```

在这种情况下，`useradd` 命令被指示为用户创建一个主目录 (`-m`)，将用户设为其所属的主组 (`-g`)，将她加入 `wheel` 和 `sales` 组 (`-G`)，并将 `tsch` 分配为她的主 shell (`-s`)。请注意，为了使此示例生效，`wheel` 和 `sales` 组必须已经存在。其结果会在 `/etc/passwd` 文件中添加类似下面的一行内容：

```
mary:x:502:100:Mary Smith:/home/mary:/bin/bash
```

`/etc/passwd` 文件的每行代表一个单一的用户账户记录。每个字段之间用冒号 (`:`) 分隔。字段在序列中的位置决定了它的含义。如您所见，登录名在第一个。密码字段包含 `x`，是因为 Fedora 正在使用 shadow 密码文件存储加密密码数据。`useradd` 命令选择的用户 ID 是 502。主组 ID 为 100，对应于 `/etc/group` 文件中的 `users` 组。注释字段被正确设置为 Mary Smith，主目录自动分配为 `/home/mary`，命令行 shell 被分配为 `/bin/bash`，完全与 `useradd` 选项中指定的一致。

`/etc/group` 文件存储了您的 Fedora 或 RHEL 系统上不同组的信息以及属于这些组的用户。组对于允许多人共享相同文件的访问权限，同时拒绝他人的访问非常有用。如果您查看 `/etc/group` 文件，将会发现类似以下的内容：

```
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,daemon
tty:x:5:
disk:x:6:root
wheel:x:7:daemon,lp
mem:x:8:
kmem:x:9:
wheel:x:10:root,joe,mary
nobody:x:99:
users:x:100:
chris:x:501
sheree:x:501
sales:x:601:bob,jane,joe,mary
```

组文件的每行都包含组名、关联的组 ID 数字以及该组中的用户列表。默认情况下，每个用户都会被添加到自己的组中，从 GID 500 开始。请注意，`mary` 被加入了 `wheel` 和 `sales` 组，而不是拥有自己的组。

## 第 11 章：设置和支持用户

### 使用用户管理器添加用户

如果您倾向于使用图形界面来添加、更改和删除用户账户，可以使用用户管理器（User Manager）。要打开用户管理器，点击系统 -> 管理 -> 用户。

当您打开用户管理器时，您会看到所有用户的列表。对于每个用户，可以看到用户名、UID、主组、全名、登录 shell 和主目录。管理员用户（1-499）不会显示。

要从用户管理器添加新用户，请执行以下操作：

1. 点击“添加”图标打开“新用户”窗口。

2. 在以下字段中输入所需信息：

   - **用户名 (User Name)**：描述用户的单个单词。通常，用户名为八个字符，全小写，包含用户的真实名、姓或（更常见的）两者的组合。

   - **全名 (Full Name)**：用户的全名（通常是名、中间字母缩写和姓）。此名称通常用于显示，大小写均可。

   - **密码 (Password)**：用户的初始密码。（要求用户首次登录新账户时使用 `passwd` 命令更改此密码。）

   - **确认密码 (Confirm Password)**：再次输入密码，以确保输入正确。

   - **登录 shell (Login Shell)**：用户登录 Fedora 或 RHEL 时看到的默认 shell（用于输入命令）。

   - **创建主目录 (Create home directory)**：默认勾选此框，并会自动创建（如“主目录”字段所示）的主目录。

   - **主目录 (Home Directory)**：默认情况下，用户在 `/home` 目录下获得与其同名的主目录。例如，用户 `sheree` 将分配 `/home/sheree` 作为其主目录。如果您想为用户分配不同的主目录，请更改此字段。

   - **为用户创建私有组 (Create a private group for the user)**：勾选此框，将为该用户创建一个与其同名的组。该名称会被添加到 `/etc/group` 文件中。此功能被称为用户私有组 (UPG)。

## 第三部分：管理 Fedora RHEL

- **手动指定用户 ID**：通常情况下，你不会勾选此框，这样新用户的 UID 将被自动分配。普通用户的新 UID 从 500 开始。然而，如果你想为用户分配特定的 UID（例如，如果你想让该 UID 与网络上另一台计算机上的用户 UID 匹配），请勾选此框并在 UI 文本框中输入你想要使用的数字。

![](img/74f214fbb2938b570bec5f957507ac66_503_0.png)

**图 11-2：** 创建新用户窗口

- 3. 完成后点击 OK。新用户被添加到 `/etc/passwd` 和 `/etc/group` 文件中。该用户账户现在可以供该用户登录了。

> **提示：** 使用用户私有组（UPGs）可以作为在多个用户之间共享文件目录的优势。这里有一个示例：

```bash
# useradd -m projectx
# mkdir /usr/local/x
# chown root.projectx /usr/local/x
# chmod 2775 /usr/local/x
# ls -ld /usr/local/x
drwxrxr-x 2 root projectx 4096 Aug 18 01:54 /usr/local/x
# gpasswd -a nextuser projectx
```

## 第 11 章：设置和支持用户

在这个示例中，你创建了一个名为 `project` 的用户（带有一个名为 `project` 的组）。创建一个 `/usr/local/x` 目录，并让所有权属于 `root` 用户和 `project` 组。将 setgid 位设置为组权限（2），为用户和组打开完全的读/写/执行权限（77），并为所有人打开读取和执行权限（5）。将每个用户添加到你希望其能够写入项目目录的组中（将 `nextuser` 替换为你想添加的用户）。此后，无论用户的主组是什么，用户在 `/usr/local/x` 目录中创建的任何文件都可以被项目组中的任何人读取或修改。

### 设置用户默认值

`useradd` 命令和用户管理器（User Manager）都通过读取 `/etc/login.defs` 文件来确定新账户的默认值。你可以通过标准文本编辑器手动编辑该文件来修改这些默认值，或者通过运行带有 `-D` 的 `useradd` 命令。如果你选择手动编辑文件，你将面对以下内容：
