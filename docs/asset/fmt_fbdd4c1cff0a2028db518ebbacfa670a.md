
```
$student01@server01 ~] su - manderson
Password:
Last login: Mon Jan 7 13:34:08 GMT 2019 on pts/1
[manderon@server01 ~] 
```

![](img/b739f72e1850e8363a4e440b6c753d29_27_0.png)

### 以其他用户身份登录

用另一个用户替换当前用户。

### 语法

`su` 命令的语法是 `su [- [user name]]`。

注意：在没有用户名参数的情况下，`su` 命令将假设你想以 root 登录。

### sudo 命令

通过 `su` 命令，任何知道 root 密码的人都可以“获取 root”身份并执行 root 用户可以做的任何事情。使用 `su – root` 的账户本质上就是服务器管理员。这通常远超过了本应委托给用户的权限。更好的做法是将特定功能委托给用户，而不是授予系统 root 权限。

`sudo` 命令允许服务器管理员将特定命令委托给特定用户，而无需授予 root 的完全权限。权限的委派通过使用 `visudo` 编辑器在 `/etc/sudoers` 文件中完成的。可以向用户和组授予特定的命令，以便他们能够在运行这些命令时履行其职责，而无需完全的管理员权限。

### 语法

`sudo` 命令的语法是 `sudo [options] [command]`。

### sudoedit 命令

Linux 文件需要 root 权限才能编辑。这可以通过 sudo 配置来实现；一个更简单更安全的选项是使用 `sudoedit` 命令。该命令允许用户使用自己的凭据编辑文件，即使该文件仅对 root 用户可用。此外，你可以使用他们喜好的文本编辑器。

要使用 `sudoedit`，你必须在 sudoers 文件中创建一个条目。例如，可以将以下行添加到 sudofile 文件中：

`%editors ALL = sudoedit /path/to/file`

`editors` 组的任何成员都可以遵循以下命令编辑文件：`sudoedit /path/to/file`

`sudo` 配置适用于需要以提升权限执行的命令，而 `sudoedit` 选项适用于需要以提升权限编辑的文件。

### 语法

`sudoedit` 命令的语法是 `sudoedit [options] [file name]`。

### visudo 命令

虽然 `/etc/sudoers` 文件是一个普通的文本文件，但至关重要的是不要使用 Vim 或 nano 等标准文本编辑器编辑它。`/etc/sudoers` 文件控制着所有提升权限的访问，该文件中的错误可能导致无法在服务器上获得 root 权限。大多数发行版都会为 `/etc/sudoers` 设置默认编辑器（通常是 Vim 或 nano）。当使用 `visudo` 命令时，系统会在提交更改之前验证 `/etc/sudoers` 文件的语法，为管理员提供了在错误成为运行配置的一部分之前进行修正的机会。

```
/etc/sudoers
root@server01:~
### 允许 users 组的成员关闭系统
# %users localhost=/sbin/shutdown -h now

## 从 /etc/sudoers.d 读取包含入式文件（这里的 # 并不表示注释）
#includedir /etc/sudoers.d
student01 ALL=(ALL) NOPASSWD:ALL
授予 root 权限的条目
```

包含向用户账户授予 root 权限条目的 `/etc/sudoers` 文件。

### 语法

`visudo` 命令的语法是 `visudo [options]`。

### 命令

以下是你可以与 visudo 一起使用的选项：

-c 检查 sudoers 文件。

-f [file name] 编辑不同位置的 sudoers 文件。

-s 在严格模式下检查。

-x [file name] 输出 sudoers 文件。

### wheel 组

root 系统的用途远不止于任务。许多发行版禁用了用户实际的 root 账户，转而通过加入 wheel 组来允许管理功能。wheel 组的成员可以使用 `sudo` 命令来避免损坏系统。你可以将用户添加到 wheel 组以赋予他们权限。对于 wheel 组的成员身份要非常谨慎。

现在你已经拥有超级用户权限，可以开始为组织中的用户创建账户了。在某些时候，你还需要根据需要修改和删除这些账户。

### useradd 命令

`useradd` 命令用于创建用户账户并配置基本设置。在创建账户的过程中，`useradd` 会引用几个文件：

- 账户存储在 `/etc/passwd` 文件中。
- 账户根据 `/etc/login.defs` 中的各种选项进行配置。
- 用户的家目录创建在 `/home/<account name>` 目录下。
- 账户的家目录使用 `/etc/skel` 目录中的文件填充。

默认情况下，`useradd` 命令不会为账户设置密码。由于大多数 Linux 发行版均不允许空密码，因此账户将存在但尚且无法使用。

### 语法

`useradd` 命令的语法为 `useradd [options] [user name]`。

### useradd 命令选项

`useradd` 命令包含许多自定义用户账户的选项，详如下表。

| 选项 | 说明 |
| :--- | :--- |
| -c | 设置注释字段，通常用作用户的全名字段。 |

示例

```
useradd -c "User One" user1
```

- -e | 设置账户过期日期。`useradd -e 2019/12/31`
- -s | 设置用户的默认 shell。
- -D | 查看新用户的默认配置。`useradd -s /bin/ksh useradd -D`

### passwd 命令

root 用户使用 `passwd` 命令为任何用户设置或重置密码。用户可以使用 `passwd` 命令重置自己的密码。它还被用于在用 `useradd` 命令创建账户后为用户设置初始密码。

> ：：当用户设置密码时，屏幕不会显示任何输出。某些用户可能会误认为这是一个问题，但实际上实际上是 Linux 隐藏了密码中使用的字符数。

```
manderon@server01 ~]$ passwd
Changing password for user manderon
Changing password for manderson.
(current) UNIX password:
New password: * 
Enter desired password
```

一个用户正在更改自己的密码的示例。

### 语法

`passwd` 命令的语法为 `passwd [user name]`。root 用户可以使用它设置特定用户的密码。

### /etc/passwd 文件

`/etc/passwd` 文件存储用户账户信息。所有账户（无论是默认还是用户特定的）都可以在此文件中找到。管理员经常引用此文件来了解系统上的特定账户。每个账户包含七字段信息。每个字段由冒号隔开。字段并不一定会被填充。

| 字段 | 内容 |
| :--- | :--- |
| User name | 用户登录系统时使用的名称。 |
| Password | 分配给用户的密码，通常表示为 x，指示密码存储在其他处。 |
| User ID | 系统中代表用户的唯一数字。 |
| Group ID | 表明用户主组成员身份的唯一数字。通常代表用户的全名。 |
| Home directory | 用户家目录的绝对路径。 |
| Login shell | 用户登录时启动的 shell 路径（通常为 /bin/bash）。 |

### 编辑 /etc/passwd 文件

编辑 `/etc/passwd` 文件的正确方法是通过通过 `useradd`、`usermod` 和 `userdel` 命令进行。手动编辑该文件可能会导致错误，从而使系统无法使用。

### /etc/shadow 文件

曾经 `/etc/passwd` 文件被用于存储密码的加密哈希版本。然而，该文件是全局可读的这意味着这意味着用户可以看到另一个用户密码的哈希版本。通过在密码破解工具中输入哈希密码，用户可以发现另一个用户的密码。

`/etc/shadow` 文件是存储哈希密码以及额外账户信息的现代存储位置。这些额外信息包括密码要求和过期信息。只有 root 有权访问 `/etc/shadow` 文件，防止用户尝试破解彼此的密码。

![](img/b739f72e1850e8363a4e440b6c753d29_32_0.png)

### /etc/shadow 文件格式

下表描述了 `/etc/shadow` 文件的格式。

| 字段 | 内容/附加信息 |
| :--- | :--- |
| User name | 用户登录系统的名称。 |
| Password | 分配给用户的密码的哈希值。 |
