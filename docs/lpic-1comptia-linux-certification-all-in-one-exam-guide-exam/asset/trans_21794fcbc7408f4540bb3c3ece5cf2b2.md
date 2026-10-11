

**使用 groupdel** 如果你因为某种原因需要删除系统中的现有组，可以在 shell 提示符下使用 `groupdel` 命令来实现。例如，要删除 dbus 用户组，你可以输入 `groupdel dbus.users`。

让我们在下面的练习中实践组的管理。

### 练习 9-2：从命令行管理组

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_393_0.png)

**视频** 更多信息请观看练习 9-2。

在这个练习中，你将在 Linux 系统的 shell 提示符下练习创建和修改组。

假设你的公司正在组建一个新的研发团队，他们将使用你的 Linux 系统。你需要为将作为该团队成员的 users 创建一个新组。请完成以下操作：

- 1. 验证你已登录到系统。
- 2. 如有必要，使用 `su –` 命令切换至你的 root 用户账户。
- 3. 通过以下步骤创建一个名为 research 的新组：
    - a. 在 shell 提示符下，输入 `groupadd research`。
    - b. 在 shell 提示符下输入 `groupmod –A "dtracy,your_username" research`，将你的用户账户和 dtracy 用户账户（在上一个练习中创建）添加到 research 组。
    - c. 在 shell 提示符下输入 `tail /etc/group`，验证用户是否已添加到组中。你应该看到以下内容：

```
research::1000:dtracy,tracy
```

### 章节复习

在本章开头，我讨论了在 Linux 系统上建立基本文件系统安全需求的必要性。我回顾了一种场景，其中同一系统上的多个用户可以相互访问对方的文件，并讨论了由此引发的问题。预防这些问题的方法是首先控制谁可以访问系统，然后控制他们进入系统后可以访问什么。

第一部分是使用 Linux 用户账户来实现的。使用用户账户时，用户必须在被允许访问系统之前提供有效的用户名和密码（称为凭证）。这被称为“登录”或“身份验证”。我指出，Linux 操作系统将根据登录用户的用户名定制系统环境。用户将能够访问他们自己的主目录和定制化的桌面环境。我指出，默认情况下，用户主目录位于 /home，但 root 用户除外，其主目录位于 /root。你可以在 shell 提示符下使用 `finger username` 命令查看特定用户的详细信息。

我还指出，每个 Linux 用户账户都有一个唯一的 ID 编号，称为 UID。在同一系统上，没有两个用户拥有相同的 UID。某些发行版（如 openSUSE）默认将标准用户的 UID 从 1000 开始。其他发行版（如 Fedora）则从 500 开始。无论你使用什么发行版，root 用户的 UID 始终设置为 0。你可以使用 `id username` 命令查看用户的 UID（以及组成员身份）。

然后我讨论了在 Linux 系统上保存用户账户的各种位置。使用本地身份验证时，用户账户保存在 `/etc/passwd` 和 `/etc/shadow` 中。使用 LDAP 身份验证时，用户账户保存在符合 LDAP 标准的目录服务中。使用 NIS 身份验证时，用户账户文件使用 NIS 服务分布在多个系统中。使用 Windows 域身份验证时，用户账户存储在一个中央数据库中，该数据库位于 Windows（或 Linux Samba）域控制器上。

我指出，对于 LPIC-1/CompTIA Linux+ 考试，你只需要熟悉本地身份验证方法。在此配置中，`/etc/passwd` 文件包含你的用户账户信息，而 `/etc/shadow` 文件包含用户的加密密码。`/etc/passwd` 文件按以下格式存储用户账户：

```
Username:Password:UID:GID:Full_Name:Home_Directory:Default_Shell
```

我还指出，`/etc/passwd` 文件包含标准用户账户和系统用户账户。标准用户账户用于登录。系统用户账户不能用于登录。相反，当系统服务需要访问文件系统时，它们会使用这些账户。

`/etc/shadow` 文件按以下格式存储用户密码信息：

```
Username:Password:Last_Modified:Min_Days:Max_Days:Days_Warn:Disabled_Days:Expire
```

`/etc/passwd` 和 `/etc/shadow` 文件必须保持同步。为此，应避免使用文本编辑器直接编辑这些文件。相反，你应该使用系统上的各种用户和密码管理工具。要检查你的文件，可以使用 `pwck` 命令。如果你怀疑文件不同步，可以使用 `pwconv` 命令将 `/etc/passwd` 中的账户添加到 `/etc/shadow`。

然后我讨论了你可以从 shell 提示符使用的不同实用工具，用于管理 Linux 系统上的用户账户。要添加用户，使用 `useradd` 实用工具。如果在创建用户时未提供任何选项，则使用 `useradd` 时，将使用 `/etc/default/useradd` 和 `/etc/login.defs` 文件中包含的默认值。

要在 shell 提示符下设置用户密码，可以使用 `passwd` 实用工具。要查看用户账户的状态，可以使用带有 `-S` 选项的 `passwd`。要修改现有的用户账户，使用 `usermod` 实用工具。要删除用户账户，使用 `userdel` 实用工具。默认情况下，`userdel` 在删除账户时不会删除用户的主目录。如果你想删除用户的主目录，可以使用带有 `-r` 选项的 `userdel`。

然后我转换思路，讨论了 Linux 组的作用。组通过将需要文件系统中文件和目录的相同访问级别的用户分组在一起，从而简化管理工作。Linux 组存储在 `/etc/group` 中。`/etc/group` 中的组记录使用以下语法表示：

```
Group:Password:GID:Users
```

某些发行版在 `/etc/group` 中存储组密码。其他发行版将它们存储在 `/etc/gshadow` 中的一个单独文件（加密格式）中，就像用户账户存储在 `/etc/passwd` 和 `/etc/shadow` 中一样。你使用 `groupadd` 命令在 Linux 系统中创建组。如果你在 `groupadd` 命令中未指定任何选项，则组将使用 `/etc/login.defs` 中找到的默认参数创建。

要在 shell 提示符下将用户添加到组，必须使用带有 `-A` 选项的 `groupmod` 命令。你还可以使用 `groupdel` 命令删除组。

### 快速复习

- 你需要控制谁可以访问 Linux 系统，以及他们进入系统后可以对文件系统中的文件和目录做什么。
- 要在系统中进行身份验证，用户必须提供用户名和密码（称为凭证）。
- 当用户登录时，Linux 恢复用户特定的信息，例如主目录和桌面环境。
- 用户主目录默认在 /home 中创建。
- root 用户的主目录是 /root。
- 可以使用 `finger` 命令查看用户账户的信息。
- 每个 Linux 用户账户都分配有一个唯一的用户 ID（UID）编号。
- root 用户的 UID 是 0。
- 某些发行版中标准用户的起始 UID 是 1000，其他发行版是 500。
- 可以使用 `id` 命令查看用户的 UID。
- 你可以在 Linux 系统上使用多种不同的身份验证方法。
- 对于你的 LPIC-1/CompTIA Linux+ 考试，你需要知道如何使用本地身份验证。
- 使用本地身份验证时，用户账户存储在 `/etc/passwd` 和 `/etc/shadow` 中。
- `/etc/passwd` 文件存储用户账户信息。
- `/etc/shadow` 文件存储加密的用户密码。
- 可以使用 `pwck` 实用工具验证 `/etc/passwd` 和 `/etc/shadow` 是否同步。
- 可以使用 `pwconv` 实用工具将 `/etc/passwd` 中缺失的用户复制到 `/etc/shadow`。
- 可以使用 `useradd` 实用工具向 Linux 系统添加用户。
- 当不使用任何选项时，`useradd` 使用包含在 `/etc/default/useradd` 和 `/etc/login.defs` 中的系统默认值创建用户账户。

