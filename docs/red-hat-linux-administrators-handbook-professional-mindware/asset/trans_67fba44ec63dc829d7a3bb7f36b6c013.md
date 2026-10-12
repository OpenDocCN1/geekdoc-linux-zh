

## groupmod

例如，以下命令将现有的 novices 组重命名为 experts：

```
groupmod -n experts novices
```

要更改 GID，请使用 `-g new GID` 选项。例如，以下命令将 troublemakers 组当前的 GID 更改为 666：

```
groupmod -g 666 troublemakers
```

## groups

**语法：** `groups [username]`

**groups** 命令显示指定用户当前所属的组列表。如果未指定用户名，则显示当前用户的组。

## last

**语法：** `last [-number] [username] [reboot]`

**last** 命令显示自 `/var/log/wtmp` 创建以来已登录的用户列表。例如，以下命令显示自上次创建 `/var/log/wtmp` 以来用户 julie 登录的次数：

```
last julie
```

以下命令仅显示 julie 最近的十次登录：

```
last -10 julie
```

此命令显示自创建 `/var/log/wtmp` 文件以来系统重启的次数：

```
last reboot
```

## passwd

**语法：** `passwd username`

**passwd** 命令允许您更改用户的密码。只有超级用户可以指定用户名；其他所有人**必须**在不带任何参数的情况下输入 `passwd`，这允许用户更改自己的密码。超级用户可以使用此程序更改任何人的密码。

## su

**语法：** `su [ - ] [ username ]`

`su` 命令可以切换到另一个用户。例如，

```
su john
```

允许您成为用户 *john*。

此命令最常见的用途是切换到 root。例如，如果您在不带任何用户名参数的情况下运行此命令，它会假定您想成为 root，从而提示您输入 root 密码。如果您输入了正确的 root 密码，`su` 将使用 root 的 UID (0) 和 GID (0) 运行一个 shell。这实际上允许您成为 root 用户并执行管理任务。如果您只有对服务器的 Telnet 访问权限，此命令非常有用。您可以作为普通用户 Telnet 到服务器，然后使用它成为 root 以执行系统管理任务。如果您提供 `-` 选项，新 shell 将被标记为登录 shell。成为 root 用户后，您可以 `su` 切换到其他用户，而无需输入任何密码。

## useradd

要从命令行创建用户帐户，请运行 `useradd` 命令。例如，要创建一个名为 `newuser` 的用户，请运行：

```
useradd newuser
```

这将使用系统默认值在 `/etc/passwd` 中添加一个新条目（如果您使用影子密码，则在 `/etc/shadow` 中也会添加）。例如，当我在我的 Red Hat 系统上运行前面的命令时，`/etc/passwd` 会显示如下所示的新行：

```
newuser::11:506:506::/home/newuser:/bin/bash
```

如果您还记得前面讨论的 `/etc/passwd` 字段，您将看到密码字段（第二个字段）被设置为 `!!`。这意味着该密码未设置，newuser 尚无法登录。因此，您需要通过运行 `passwd` 命令为此用户创建密码，如下所示：

```
passwd newuser
```

系统会要求您输入两次密码，密码被接受后，它会被加密并添加到 `/etc/passwd` 文件中的用户条目里。

UID 和 GID 值将由 `useradd` 自动选择。基本上，它只是将 `/etc/passwd` 中的最后一个 UID 加 1，将 `/etc/group` 中的最后一个 GID 加 1，分别为新用户创建 UID 和 GID。您也可以使用命令行开关 `-u` 和 `-g` 分别手动设置 UID 和组。主目录将在默认的顶级主目录中创建。同样，登录 shell 也是从系统默认值中选择的。如果您想覆盖系统默认值，请指定命令行选项。要覆盖默认主目录，请使用 `-d newdirectory` 选项（其中 `newdirectory` 是您的目录名称）。例如：

```
useradd newuser -d /www/newuser
```

将创建新用户（`newuser`），其主目录将设置为 `/www/newuser`。请注意，`useradd` 将仅创建最后一级目录，而不会创建整个路径。例如，如果您将 `-d /some/new/dir/myuser` 指定为选项，只有当 `/some/new/dir` 已经存在时，`useradd` 才会创建 `myuser`。

创建新主目录时，`/etc/skel` 目录中包含的文件将被复制到新主目录中。这些文件通常是默认 shell 的点配置文件。例如，如果默认 shell 是 `/bin/bash`，您应该在 `/etc/skel` 目录中拥有 `.bashrc`、`.bash_profile` 和 `.bash_login` 的默认版本，以便新用户的主目录可以自动设置这些文件。

Red Hat Linux 自带的 `useradd` 会为用户创建一个与用户名同名的私有组。例如，如果您运行 `useradd kabir`，一个名为 `kabir` 的新用户将在 `/etc/passwd` 文件中创建，一个名为 `kabir` 的新组将在 `/etc/group` 文件中创建。这种方法使新用户完全与其他用户隔离，从而确保用户更高的隐私。每当新用户创建新文件时，凭借这个私有组，该文件仅可由新用户访问。用户必须显式更改文件权限，才能允许其他人查看该文件。

但是，如果您的用户帐户与这种私有组的想法冲突，您可以使用 `-g group` 选项覆盖它（其中 `group` 是您的组名）。例如，

```
useradd mjkabir -g users
```

使 `useradd` 创建新用户 (mjkabir)，并将默认组设置为 users。

如果您想让新用户成为系统上其他组的成员，请使用 `-G comma-separated list of groups` 选项。例如，

```
useradd mjkabir -G wheel,admins
```

将新用户 (mjkabir) 添加到 `/etc/group` 文件中的 `wheel` 和 `admins` 组。

## userdel

要删除现有用户，请使用 `userdel` 命令。例如，以下命令删除名为 `snake` 的用户：

```
userdel snake
```

如果您想删除用户的主目录及其所有内容，请使用 `-r` 选项。请注意，如果用户当前已登录，`userdel` 将不会删除该用户。通过发送 `write` 消息（`write username`）要求用户注销，如果无法要求，请使用 `killall` 命令终止与该用户关联的所有进程，然后运行 `userdel` 命令。

要暂时禁用用户帐户，请执行以下操作之一：

- 使用 `usermod -s new shell username` 命令将 shell 更改为 `/bin/false`（确保新 shell 列在 `/etc/shells` 文件中）。这将禁止用户登录系统。
- 如果您使用影子密码，请使用 `usermod -e MM/DD/YY username` 命令导致用户帐户过期。

要暂时禁用所有用户帐户访问，请创建一个名为 `/etc/nologin` 的文件，其中包含一条解释为何不允许访问的消息。只要此文件存在，登录程序将不允许任何非 root 帐户登录。

## usermod

`usermod` 命令用于修改用户帐户。要更改现有用户的主目录，请按如下方式运行 `usermod` 命令：

```
usermod -d new_home_directory username
```

其中 `new_home_directory` 和 `username` 是正确的值。

例如，如果名为 `keller` 的用户将 `/home/keller` 作为其主目录，而您想将其移至 `/home2/keller`，请按如下方式运行 `usermod` 命令：

```
usermod -d /home2/keller keller
```

这将设置新目录作为其主目录。但是，如果您想将其主目录的内容移动到新位置，请使用 `-m` 选项，如下所示：

```
usermod -d -m /home2/keller keller
```

要更改用户的 UID，请按如下方式使用 `usermod` 命令：

```
usermod -u UID username
```

其中 `UID` 和 `username` 是正确的值。

例如，以下命令将用户 `mrfrog` 的 UID 更改为 500：

```
usermod -u 500 mrfrog
```

用户在其主目录中拥有的所有文件和目录将自动反映 UID 的更改。但是，如果用户在其主目录之外拥有文件，您将不得不使用 `chown` 命令手动更改所有权。

