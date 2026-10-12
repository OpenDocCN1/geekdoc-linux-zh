
## 10.3. 用户、组和用户私有组

用户的*主要组*。有关如何使用组的详细信息，请参见第 10.3.3 节。

| 用户 | UID | GID | HOME 目录 | Shell |
| :--- | :--- | :--- | :--- | :--- |
| root | 0 | 0 | /root | /bin/bash |
| bin | 1 | 1 | /bin | |
| daemon | 2 | 2 | /sbin | |
| adm | 3 | 4 | /var/adm | |
| lp | 4 | 7 | /var/spool/lpd | |
| sync | 5 | 0 | /sbin | /bin/sync |
| shutdown | 6 | 0 | /sbin | /sbin/shutdown |
| halt | 7 | 0 | /sbin | /sbin/halt |
| mail | 8 | 12 | /var/spool/mail | |
| news | 9 | 13 | /var/spool/news | |
| uucp | 10 | 14 | /var/spool/uucp | |
| operator | 11 | 0 | /root | /bin/bash |
| games | 12 | 100 | /usr/local/games | |
| gopher | 13 | 30 | /usr/lib/gopher-data | |
| ftp | 14 | 50 | /usr/ths/ftp | |
| nobody | 99 | 99 | /root | |

**图 10.1：标准用户**

### 10.3.2 标准组

表 10.3.2 列出了安装过程设置的标准组（这基本上是 */etc/group* 文件）。

| 组 | 组 ID | 成员 |
| --- | --- | --- |
| root | 0 | root |
| bin | 1 | root,bin,daemon |
| daemon | 2 | root,bin,daemon |
| sys | 3 | root,bin,adm |
| adm | 4 | root,adm,daemon |
| tty | 5 | |
| disk | 6 | root |
| lp | 7 | daemon,lp |
| mem | 8 | |
| kmem | 9 | |
| wheel | 10 | root |
| mail | 12 | mail |
| news | 13 | news |
| uucp | 14 | uucp |
| man | 15 | |
| games | 20 | |
| gopher | 30 | |
| dip | 40 | |
| ftp | 50 | ftp |
| nobody | 99 | |
| users | 100 | |

**图 10.2：标准组**

### 10.3.3 用户私有组

Red Hat Linux 采用用户私有组（UPG）机制，这使得使用 UNIX 组变得更加容易。UPG 机制并没有在标准 UNIX 处理组的方式中添加或更改任何内容。它只是提供了一种处理组的新约定。每当您创建一个新用户时，默认情况下，该用户拥有一个唯一的组。该机制的工作原理如下：

- **用户私有组** 每个用户都有自己的主要组，且仅该用户是该组的成员。

- **umask = 002** 传统的 UNIX umask 为 022，它防止其他用户和*用户主要组的其他成员*修改用户的文件。由于在 UPG 机制中每个用户都有自己的私有组，因此不需要这种“组保护”。umask 为 002 将防止用户修改其他用户的私有文件。umask 在 */etc/profile* 中设置。

- **目录的 SGID 位** 如果您在目录上设置 SGID 位（使用 *chmod g+s directory*），则在该目录中创建的文件其组将设置为该目录的组。

大多数计算站点喜欢为每个主要项目创建一个组，并将人员分配到他们所在的组中。然而，传统上管理文件很困难，因为当某人创建文件时，该文件归属于其主要组所属的组。当一个人同时处理多个项目时，很难使文件归属于与该项目关联的组。在 UPG 机制中，组是根据项目自动分配给文件的，这使得管理组项目变得非常简单。

假设您有一个名为 *devel* 的大型项目，许多人正在 *devel* 目录中编辑 *devel* 文件。创建一个名为 *devel* 的组，使用 *chgrp* 将 *devel* 目录更改为 *devel* 组，并将所有 *devel* 用户添加到 *devel* 组中。现在，所有 *devel* 用户都可以编辑 *devel* 文件并在 *devel* 目录中创建新文件，并且这些文件将始终保留 *devel* 组属性。因此，它们始终可以被其他 *devel* 用户编辑。

如果您有多个像 *devel* 这样的项目，以及从事多个项目的用户，这些用户在项目之间切换时，永远不需要更改他们的 umask 或组。每个项目主目录上的 SGID 位会“选择”正确的组。

由于每个用户的 HOME 目录由该用户及其私有组所有，因此在 HOME 目录上设置 SGID 位是安全的。然而，默认情况下，文件是以用户的主要组创建的，因此 SGID 位是多余的。

#### 用户私有组的理由

由于 UPG 机制是新的，许多人对此有疑问，并想知道它为什么是必要的。以下是该机制的理由。

- 您希望让一组人员处理位于例如 /usr/lib/emacs/site-lisp 目录中的一组文件。您信任少数人在那里进行更改，但肯定不是所有人。
- 因此您输入：
  ```text
  chown -R root.emacs /usr/lib/emacs/site-lisp
  ```
  并将适当的用户添加到组中。
- 为了允许用户实际在目录中创建文件，您输入：
  ```text
  chmod 775 /usr/lib/emacs/site-lisp
  ```
- 但当用户创建新文件时，它会被分配给用户的默认组（通常是 users）。为了防止这种情况，您输入
  ```text
  chmod 2775 /usr/lib/emacs/site-lisp
  ```
  这将导致目录中的一切都以“emacs”组创建。
- 但新文件需要模式 664，以便 emacs 组中的其他用户能够编辑它。为此，您将默认 umask 设为 002。
- 嗯，这一切都运行得很好，除了如果您的默认组是“users”，您在主目录中创建的每个文件都将可被“users”中的每个人（通常是所有人）写入。
- 为解决此问题，您让每个用户拥有一个“私有组”作为其默认组。

此时，通过设置默认 umask 为 002 并赋予每个人一个私有默认组，您可以轻松设置用户可以利用的组，而无需进行任何复杂操作。只需创建组，添加用户，并对组的目录执行上述 chown 和 chmod 操作即可。

## 10.4. PAM

赋予用户某种特权的程序需要能够验证用户的身份。当您登录系统时，您提供姓名和密码，登录过程使用这些信息来验证登录——以核实您是否如所言属实。除了密码之外，还有其他的身份验证形式，并且密码也可以以不同的方式存储。

PAM 代表“可插拔身份验证模块”（Pluggable Authentication Modules），它允许系统管理员设置身份验证策略，而无需重新编译执行身份验证的程序。使用 PAM 时，您可以通过编辑配置文件来控制模块如何插入程序。

大多数 Red Hat Linux 用户永远不需要接触此配置文件。当您使用 RPM 安装需要进行身份验证的程序时，它们会自动做出所需的更改以执行正常的密码身份验证。但是，您可能希望自定义配置，在这种情况下，您需要理解该配置文件。

### 10.4.1 模块

PAM 标准定义了四种类型的模块。*auth* 模块提供实际的认证，例如请求并检查密码，以及设置“凭证”，如组成员资格或 kerberos“票据”。*account* 模块检查身份验证是否被允许（账户未过期，用户允许在此时登录等）。*password* 模块用于设置密码。*session* 模块在用户通过身份验证后使用，使其能够使用其账户，例如挂载用户的主目录或使其邮箱可用。

这些模块可以*堆叠*，从而使用多个模块。例如，登录通常使用至少两种身份验证方法：如果“rhosts”身份验证成功，则允许连接即可；如果失败，则执行标准的“unix”密码身份验证。

可以随时添加新模块，并且支持 PAM 的应用程序随后可以配置为使用它们。例如，如果您有一个一次性密码计算器系统，并且可以编写支持它的模块（系统包含编写模块的文档）。支持 PAM 的程序可以使用新模块并与新的一次性密码计算器协同工作，而无需重新编译或以其他方式修改。

Red Hat Linux 中有一个模块，我们为了完整性而包含它，但目前不推荐仅基于实验目的使用：`pam_pwdb.so`。`pwdb` 软件包和 `pam_pwdb.so` 模块目前是 alpha 质量的软件，但具有您可能希望尝试的有趣功能。目前 Red Hat Software **不支持**它们。

### 10.4.2 服务

使用 PAM 的每个程序都定义自己的“服务”名称。登录程序定义服务类型 `login`，`ftp` 定义服务类型 `ftp` 等。通常，服务类型是用于*访问*服务的程序名称，而不是（如果有区别）用于*提供*服务的程序。

### 10.4.3 配置文件

文件 `/etc/pam.conf` 用于配置所有 PAM 应用程序。每个应用程序（实际上是每个**服务**）都有自己的“段”（stanza）。段看起来像这样：

```
# login authorization
login auth required /lib/security/pam_secrety.so
login auth required /lib/security/pam_unix_auth.so
login auth required /lib/security/pam_nologin.so
login account required /lib/security/pam_unix_acc.so
login password required /lib/security/pam_unix_passwd.so
login session required /lib/security/pam_unix_session.so
```

第一行是注释。任何以 `#` 字符开头的行都是注释。接下来的三行堆叠了三个用于登录授权的模块。第一个确保*如果*用户试图以 root 身份登录，他们登录所在的 `tty` 在 `/etc/secrety` 中列出

