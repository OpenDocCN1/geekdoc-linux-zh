
将创建新用户（`newuser`），其主目录将被设置为 `/www/newuser`。注意，`useradd` 只会创建最后的目录而不会创建整个路径。例如，如果你指定 `-d /some/new/dir/myuser` 作为选项，只有当 `/some/new/dir/` 存在时，`useradd` 才会创建 `myuser`。

当新主目录创建时，`/etc/skel` 目录中的文件会被复制到新主目录。这些文件通常是默认 shell 的配置文件。例如，如果默认 shell 是 `/bin/bash`，你应该在 `/etc/skel` 目录中拥有 `.bashrc`、`.bash_profile` 和 `.bash_login` 的默认版本，新用户的主目录就可以自动使用这些文件设置。你将在本章稍后的章节中学习更多相关内容。

红帽 Linux 自带的 `useradd` 会为用户创建一个与用户名相同的私有组。例如，如果你运行 `useradd kabir`，则在 `/etc/group` 中创建一个名为 `kabir` 的新组。这种方法允许新用户与其他用户隔离。然而，如果你的账户策略与这种分组的想法冲突，你可以使用 `-g` 选项来覆盖它（`group` 是你的组名）。例如：

```
useradd mjkadir -g users
```

这将使 `useradd` 使用默认组创建用户。

> 你可以使用 `groups` 命令查看用户属于哪些组。

# 第7章：用户管理

## 添加用户到附加组

如果你想让新用户成为系统其他组的成员，可以使用逗号分隔的组列表 `-G`。例如：

```
useradd mjkadir -G wheel,admins
```

在这里，新用户（`mkadir`）将加入 `/etc/group` 中的 `wheel` 和 `admins` 组。

## 创建新组

要创建一个组，使用 `groupadd` 命令。例如：

```
groupadd mygroup
```

这将向 `/etc/group` 添加一个名为 `mygroup` 的组（如果你使用影子密码，则在 `/etc/gshadow` 中添加）。默认情况下，`groupadd` 程序创建一个 GID 超过 499 的组，因为 0-499 被留用于 `root`、`bin` 和 `mail` 等系统账户。因此，如果你的 `/etc/group` 文件最后一个 GID 设置为 511，你用此程序创建的新组 GID 将是 512，依此类推。如果你想专门设置新组的 GID，请使用 `-g GID` 选项。此外，如果你想在 0-499 范围内创建一个组，请使用 `-g gid` 选项强制 `groupadd` 将新组创建为系统组。注意，如果你尝试使用的组或 GID 在 `/etc/group` 中已存在，你将收到错误消息。

## 修改现有用户账户

处理用户遗忘的密码是系统管理员执行的最常见任务。在这里你将学习更改用户账户的各种细节。

### 修改密码

要更改或设置用户的密码，使用 `passwd` 命令。例如：

```
passwd kabir
```

这将允许你更改用户 `kabir` 的密码。你会被要求输入两次密码以确认。确保为你的用户选择良好的密码。不要使用包含常用字典词的简单密码。注意，`passwd` 程序也可以由用户运行来更改自己的密码。当普通用户运行 `passwd` 程序时，不需要用户名参数，因为这将允许她只更改她自己的密码。

### 更改 shell

如果默认 shell 不符合用户需求，您可以将其更改为 `/etc/shells` 中列出的任何 shell。使用 `chsh` 命令可以更改用户的 shell。例如：

```
chsh brian
```

此命令允许您更改用户 `brian` 的当前 shell。如果您指定的任何 `/etc/shells` 中不存在的 shell 或程序名称，用户将无法登录。请注意，用户也可以使用此命令更改自己的 shell。普通用户不需要将用户名作为参数，因为他们唯一可以更改的 shell 就是自己的。

注意，您也可以使用 `usermod` 命令按如下方式修改 shell 信息：

```
usermod -s new_shell path username
```

其中 `new_shell path` 和 `username` 是正确的值。

### 更改家目录

要更改现有用户的家目录，请按如下方式运行 `usermod` 命令：

```
usermod -d new_home_directory username
```

其中 `new_home_directory` 和 `username` 是正确的值。

例如，如果一个名为 `keller` 的用户其家目录为 `/home/keller`，而您想将其移动到 `/home2/keller`，您可以按如下方式运行命令：

```
usermod -d /home2/keller keller
```

这将新目录设为她的家目录。但是，如果您想将她的家目录内容移动到新位置，请使用 `-m` 选项，如下：

```
usermod -d -m /home2/keller keller
```

### 更改 UID

要更改用户的 UID，请按如下方式使用 `usermod` 命令：

```
usermod -u UID username
```

其中 `UID` 和 `username` 是正确的值。

例如：

```
usermod -g 500 myfrog
```

这将将用户 `mrfrog` 的 UID 更改为 500。请注意，用户家目录下拥有的所有文件和目录会自动反映 UID 的更改。然而，如果用户在自己的家目录之外拥有文件，您将必须使用 `chown` 命令手动更改所有权。（有关如何使用 `chown` 命令的详情请参见第 5 章。）

### 更改默认组

要更改用户的默认组，请按如下方式使用 `usermod` 命令：

```
usermod -g group_name or GID username
```

其中 `group_name` 或 `GID` 以及 `username` 是正确的值。
例如：

```
usermod -g 777 myfrog
```

此命令将用户 `mrfrog` 的默认组更改为 `777`。

### 更改账户过期日期

如果您使用影子密码（shadow passwords），可以使用如下方式的 `usermod` 命令更改用户账户的过期日期：

```
usermod -e MM/DD/YY username
```

其中 `MM/DD/YY` 和 `username` 是正确的值。
例如：

```
usermod -e 12/31/99 kabir
```

此命令将用户 `kabir` 的账户过期日期重置为 12/31/99。

### 更改 finger 信息

如果您允许用户相互查询 finger 或为用户账户之外的人运行 finger 守护进程，您也可以更改 finger 信息，例如全名和电话号码。运行 `chfn` 命令更改用户的 finger 信息。例如：

```
chfn jennifer
```

这将允许您更改用户 `jennifer` 的 finger 信息，这些信息存储在 `/etc/passwd` 文件中。用户也可以使用此程序更改自己的 finger 信息。用户还可以在其家目录下创建一个 `.plan` 文件，该文件将追加到 finger 程序显示的信息之后。

## 修改现有组

要修改现有的组名或 GID，请使用 `groupmod` 命令。要将组重命名为新名称，请使用以下语法：

```
groupmod -n new_group current_group
```

例如：

```
groupmod -n experts novices
```

这里现有的 `novices` 组被重命名为 `experts`。要更改 GID，请使用 `-g GID` 选项。例如：

```
groupmod -g 666 troublemakers
```

此命令将 `troublemakers` 组的当前 GID 更改为 666。

## 删除或禁用用户账户

要删除现有用户，请使用 `userdel` 命令。例如：

```
userdel snake
```

这将删除用户 `snake`。如果您想删除用户的家目录及其目录内的所有内容，请使用 `-r` 选项。请注意，如果用户当前已登录，`userdel` 将不会删除用户。通过发送 `write` 消息（`write username`）要求用户注销，如果不可行，请使用 `killall` 命令终止与用户相关的所有进程，然后运行 `userdel` 命令。

如果您想临时禁用用户账户，可以执行以下操作之一：

- 使用 `usermod -s shell username` 命令将 shell 更改为 `/bin/false`（确保它存在于您的 `/etc/shells` 中）。这将阻止用户登录系统。
- 如果您使用影子密码，可以使用 `usermod -e MM/DD/YY username` 命令使用户账户过期。

如果您想禁用所有用户账户...

```bash
# PASS_MIN_LEN 最可接受密码长度。
```
