
## 密码文件

用户通过提供正确的登录名和密码来获取账户访问权限。系统在密码文件中维护密码，以及登录信息（如用户名和用户 ID）。像 `passwd` 命令这样的工具允许用户通过修改这些文件来更改密码。传统上，`/etc/passwd` 文件存储用户密码，尽管是以加密形式。然而，所有用户都被允许读取 `/etc/passwd` 文件，这使得用户能够访问加密后的密码。为了增强安全性，密码条目保存在 `/etc/shadow` 文件中，该文件仅允许 root 用户访问。

### /etc/passwd

当您添加用户时，会在 `/etc/passwd` 文件（通常称为密码文件）中创建该用户的条目。每个条目占一行，包含由冒号分隔的多个字段。这些字段如下：

- **用户名**：用户的登录名
- **密码**：用户账户的加密密码
- **用户 ID**：系统分配的唯一数字
- **组 ID**：用于标识用户所属组的数字
- **注释**：任何用户信息，例如用户的全名
- **主目录**：用户的主目录
- **登录 Shell**：用户登录时运行的 Shell；这是默认 Shell，通常是 `/bin/bash`

根据是否使用 shadow 密码，密码字段（第二个字段）将是 `x` 或用户密码的加密形式。Red Hat 默认实施 shadow 密码，因此这些条目的密码应为 `x`。以下是 `/etc/passwd` 条目的示例。对于这些条目，必须使用 `passwd` 命令创建密码。还要注意，在这个特定系统中，用户 ID 从 500 开始并递增 1。在 Red Hat 中，分配的组不是通用的 User 组，而是一个仅由该用户组成的唯一组。例如，`dylan` 用户属于名为 Dylan 的组，而不是通用的 User 组。

```
dylan:x:500:500:Dylan:/home/dylan:/bin/bash
chris:x:501:501:Chris:/home/chris:/bin/bash
```

**提示** 如果关闭 shadow 密码支持，passwd 文件中的条目将显示加密密码。由于任何用户都可以读取 `/etc/passwd` 文件，入侵者可以访问并可能破解加密后的密码。

**提示** 虽然在技术上可以直接编辑 `/etc/passwd` 文件中的条目，但不建议这样做。特别是，删除条目不会移除与用户相关的其他信息、权限和数据，这可能导致安全漏洞，使入侵者能够接管被删除用户的 ID 或磁盘空间。

### /etc/shadow 和 /etc/gshadow

`/etc/passwd` 文件是一个简单的文本文件，容易受到安全漏洞的影响。如果任何人获取了对 `/etc/passwd` 文件的访问权限，他们可能会通过暴力破解攻击来解密或破解加密密码。shadow 应用程序套件实施了更高级别的安全措施。这包括 `useradd`、`groupadd` 及其对应的更新和删除程序的版本。大多数其他用户配置工具，包括 redhat-config-users，都支持 shadow 安全措施。使用 shadow 安全机制后，密码不再保存在 `/etc/passwd` 文件中。相反，密码保存在名为 `/etc/shadow` 的单独文件中。访问权限限制为 root 用户。

以下示例显示了两个用户的 `/etc/shadow` 条目，列出了它们的加密密码。`chris` 的条目在其 Password 字段中为 `x`，表示尚未为该用户创建密码：

```
dylan:YOTPd3Pyy9hAc:500:500:Dylan:/home/dylan:/bin/bash
chris:x:501:501:Chris:/home/chris:/bin/bash
```

还有一个对应的密码文件，称为 `/etc/gshadow`，用于维护需要密码的组。Red Hat 默认支持 shadow 密码。您可以使用 Red Hat 认证工具手动指定是否希望使用 shadow 密码。

## 密码工具

若要更改特定用户的任何特定字段，应使用提供的用户管理工具，例如本章中讨论的 `passwd` 命令、redhat-config-users、`adduser`、`usermod`、`useradd` 和 `chage`。`passwd` 命令仅允许更改密码。其他工具，如 redhat-config-users，不仅在 `/etc/passwd` 文件中创建条目，还为用户创建主目录并在用户主目录中安装初始化文件。

这些工具还允许您控制用户对其账户的访问权限。您可以为用户设置过期日期，或锁定他们的账户。账户被锁定的用户在 `/etc/shadow` 文件中的密码前缀将是无效字符串 `!!`。解锁账户会移除此前缀。

**提示** 使用 Red Hat 认证工具（authconfig-gtk，参见第 4 章），您可以启用和配置各种认证工具，如 NIS 和 LDAP 服务器，以及启用 shadow 密码、LDAP 和 Kerberos 认证（可通过系统设置菜单和窗口中的 Authentication 访问）。

## 管理用户环境

每次用户登录时，都会执行两个配置文件脚本：一个对所有用户都相同的系统配置文件脚本，以及一个可以根据每个用户需求自定义的用户登录配置文件脚本。当用户注销时，会运行用户注销脚本。此外，每次生成 shell（包括登录 shell）时，都会运行用户 shell 脚本。不同的 shell 使用不同类型的脚本。在 Red Hat 中，常用的默认 shell 是 BASH shell。作为替代方案，用户可以使用不同的 shell，例如 TCSH 或 Z shell，它们都安装在 Red Hat Linux 中。

### 配置文件脚本

对于 BASH shell，每个用户都有一个名为 `.bash_profile` 的 BASH 登录配置文件脚本，位于他们的主目录中。系统配置文件脚本位于 `/etc` 目录中，名为 `profile`，前面没有点号。BASH shell 用户 shell 脚本称为 `.bashrc`。`.bashrc` 文件还会运行 `/etc/bashrc` 文件以实现全局定义，例如 `PS1` 和 `TERM` 变量。`/etc/bashrc` 文件还会执行 `/etc/profile.d` 目录中的任何专用初始化文件，例如用于 KDE 和 GNOME 的文件。`.bash_profile` 文件运行 `.bashrc` 文件，并通过它运行 `/etc/bashrc` 文件，以实现全局定义。

作为超级用户，您可以编辑这些配置文件或 shell 脚本中的任意一个，并放入任何希望在每个用户登录时执行的命令。例如，您可能希望定义命令的默认路径，以防用户未这样做。或者，您可能希望通知用户最近的系统新闻或账户更改。

### /etc/skel

当您首次向系统添加用户时，必须为用户提供其登录、shell 和注销初始化文件的骨架版本。对于 BASH shell，这些文件是 `.bash_profile`、`.bashrc` 和 `.bash_logout`。`useradd` 命令以及其他用户管理工具（如 Red Hat User Manager）会自动添加这些文件，将 `/etc/skel` 目录中的任何文件复制到用户的新主目录中。`/etc/skel` 目录包含 `.bash_profile`、`.bashrc` 和 `.bash_logout` 文件的骨架初始化文件；如果您使用 TCSH shell 作为登录 shell，则包含 `.login`、`.tcshrc` 和 `.logout` 文件。`/etc/skel` 目录还包含桌面的默认文件和目录。这包括 X Window 系统的 `.screenrc` 文件、KDE 桌面的 `.kde` 目录，以及包含 GNOME 桌面默认配置文件的 `Desktop` 目录。

作为超级用户，您可以按任意方式配置 `/etc/skel` 目录中的 `.bash_profile` 或 `.bashrc` 文件。通常，包含基本的系统变量赋值，用于定义命令和命令别名的路径名。`PATH` 和 `BASH_ENV` 变量在 `.bash_profile` 中定义。一旦用户拥有自己的 `.bash_profile` 或 `.bashrc` 文件，他们就可以根据需要重新定义变量或添加新命令。

### /etc/login.defs

用户和组创建实用程序（如 `useradd` 和 `groupadd`）使用的系统级值保存在 `/etc/login.defs` 文件中。在这里，您会找到可能的用户 ID 和组 ID 的范围。`UID_MIN` 保存用户 ID 的最小数字，`UID_MAX` 保存最大数字。各种密码选项控制密码限制——例如 `PASS_MIN_LEN`，它确定密码中允许的最小字符数。诸如 `CREATE_HOME` 等选项可以设置，以告知 `useradd` 等用户工具默认为新账户创建主目录。这些条目的示例如下所示：

```
MAIL_DIR /var/spool/mail
PASS_MIN_LEN 5
CREATE_HOME yes
```

### /etc/login.access

