
```bash
# useradd -m steve
# passwd steve
Enter new UNIX password: ******
Retype new UNIX password: ******
passwd: password updated successfully
```

向系统中添加用户账户（并设置其密码）

`useradd` 命令用于创建新的用户账户。在上述示例中，执行 `useradd -m steve` 为用户创建了一个基本的登录账户。`-m` 选项用于自动为指定用户创建主目录（推荐）。然后使用之前讨论过的 `passwd` 命令为新用户设置密码。

> **注意：** 在新用户能够登录之前，必须使用 `passwd` 命令为其设置密码。

`userdel` 命令用于从系统中删除用户账户。下一个示例演示了如何使用 `userdel` 删除账户。可选的 `-r` 选项用于在删除用户账户后自动删除该用户的主目录。

**用法语法：** `userdel [OPTIONS] [USER]`

```bash
# userdel -r steve
```

删除用户账户

> **注意：** 在某些 Unix 和 BSD 系统上，可以使用 `rmuser` 命令替代 `userdel`。

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `useradd [USER]` | 创建指定的用户账户 |
| `useradd -m [USER]` | 自动为用户创建主目录 |
| `userdel [USER]` | 删除指定的用户账户 |
| `userdel -r [USER]` | 删除用户账户及其主目录 |

### adduser / deluser

**用途：** 在 Linux 系统上创建/删除用户账户。

**用法语法：** `adduser [OPTIONS] [USER]`

```bash
# adduser mike
Adding user 'mike' ...
Adding new group 'mike' (1002) ...
Adding new user 'mike' (1002) with group 'mike' ...
Creating home directory '/home/mike' ...
Copying files from '/etc/skel' ...
Enter new UNIX password: ******
Retype new UNIX password: ******
passwd: password updated successfully
Changing the user information for mike
Enter the new value, or press ENTER for the default
    Full Name [:] : Mike Smith
    Room Number [:] : Computer Room
    Work Phone [:] : 555-1212
    Home Phone [:] :
Is the information correct? [y/N] y
```

使用 `adduser` 命令创建用户

`adduser` 命令是之前讨论的 `useradd` 命令的用户友好型前端。通过提示输入创建账户时所需的信息（而不是指定多个命令行选项），它简化了 Linux 系统上用户账户的创建过程。上述示例展示了 `adduser` 命令的典型用法。

`deluser` 命令用于删除用户账户，如下例所示。

**用法语法：** `deluser [OPTIONS] [USER]`

```bash
# deluser mike
Removing user 'mike' ...
Warning: Removing group 'mike', since no other user is part of it.
Done.
```

使用 `deluser` 命令删除用户

> **注意** `adduser` 和 `deluser` 命令的默认设置存储在 `/etc/adduser.conf` 和 `/etc/deluser.conf` 中。

常见用法示例：
- `adduser [USER]` 创建用户账户
- `deluser [USER]` 删除用户账户

### groupadd / groupdel

**用途：** 添加/删除组。

**用法语法：** `groupadd [GROUP]`

```bash
# groupadd accounting
```

使用 `groupadd` 创建新组

`groupadd` 命令用于创建新的组账户。组在管理多用户环境中文件和目录的访问权限方面非常有用。在上述示例中，创建了一个名为 `accounting` 的新组。生成的组条目显示在 `/etc/group` 文件中如下所示。

```bash
# grep accounting /etc/group
accounting:x:1002:
```

显示 `/etc/group` 文件中的组条目

`groupdel` 命令用于从系统中删除组。下一个示例演示了如何使用 `groupdel` 命令从系统中删除之前创建的 `accounting` 组。

**用法语法：** `groupdel [GROUP]`

```bash
# groupdel accounting
```

使用 `groupdel` 删除组

常见用法示例：
- `groupadd [GROUP]` 创建新组
- `groupdel [GROUP]` 删除组

### usermod / groupmod

**用途：** 修改用户和组账户设置。

**用法语法：** `usermod [OPTIONS] [USER]`

```bash
# usermod -aG sales nick
```

使用 `usermod` 命令更改用户的组成员身份

`usermod` 命令用于修改用户账户设置。在上述示例中，`-aG` 选项用于将用户 `nick` 添加到 `sales` 组。你还可以使用 `usermod` 命令通过 `-d` 选项更改用户的主目录位置，或通过 `-s` 选项更改默认 Shell。

`groupmod` 命令用于修改组。其主要用途是重命名组。在下一个示例中，使用 `groupmod -n` 将 `accounting` 组重命名为 `finance`。

**用法语法：** `groupmod [OPTIONS] [GROUP]`

```bash
# groupmod accounting -n finance
# grep finance /etc/group
finance:x:1002:
```

使用 `groupmod` 命令重命名组

常见用法示例：

| 命令 | 描述 |
| :--- | :--- |
| `usermod -s [SHELL] [USER]` | 更改用户的默认 Shell |
| `usermod -d [DIR] [USER]` | 更改用户的主目录位置 |
| `usermod -aG [GROUP] [USER]` | 将用户添加到指定的组 |
| `groupmod [OLD] -n [NEW]` | 重命名指定的组 |

### wall

**用途：** 向系统上的所有用户广播消息。

**用法语法：** `wall [FILE]`

```bash
### wall
Anyone want some tacos?
<CTRL + D>
```

使用 `wall` 命令向登录到系统的所有用户发送消息

`wall` 命令向当前登录到系统的所有用户发送消息。在上述示例中输入的文本将显示在所有本地终端和当前登录到系统的远程会话中。

> **注意** 按下 `CTRL + D` 结束消息编辑器并发送消息。

下一个示例展示了系统上其他用户看到的 `wall` 消息输出样本。

```text
$
Broadcast Message from root@e6400 (/dev/pts/0) at 11:56 ...
Anyone want some tacos?
```

`wall` 消息在所有终端上的输出

除了手动输入消息外，还可以使用包含预写消息的文本文件与 `wall` 命令一起使用，如下例所示。

```bash
# wall /home/nick/message.txt
```

使用文本文件通过 `wall` 命令发送消息

常见用法示例：
- `wall` 向所有用户发送消息
- `wall [FILE]` 向所有用户发送指定文件中的消息

### ulimit

**用途：** 显示/设置系统资源限制。

**用法语法：** `ulimit [OPTIONS] [LIMIT]`

| 命令 | 描述 |
| :--- | :--- |
| `$ ulimit -a` | 使用 `ulimit` 命令显示已定义的资源限制 |
| core file size | core 文件大小 (blocks, -c) 0 |
