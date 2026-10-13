
## su

语法：

```
su [-] [username]
```

su 命令可用于切换到另一个用户。例如，

```
su john
```

允许你成为用户 john。

此命令最常见的用途是成为 root。例如，如果你在不带任何用户名参数的情况下运行此命令，它会假定你想成为 root，因此会提示你输入 root 密码。如果你输入正确的 root 密码，su 将使用 root 的 UID（0）和 GID（0）运行一个 shell。这有效地允许你成为 root 用户并执行管理任务。如果您只有 Telnet 访问服务器，此命令非常有用。你可以以普通用户身份通过 Telnet 登录到服务器，并使用它成为 root 以执行系统管理任务。如果提供 - 选项，则新 shell 将被标记为登录 shell。成为 root 用户后，你可以 su 到其他用户而无需输入密码。

## useradd

要从命令行创建用户帐户，可以运行 useradd 命令。例如，要创建一个名为 newuser 的用户，可以按如下方式运行此命令：

```
useradd newuser
```

这会使用系统默认值在 /etc/passwd 中添加一个新条目（如果使用 shadow 密码，则在 /etc/shadow 中）。例如，当我在我的 Red Hat 系统上运行前面的命令时，/etc/passwd 显示如下新行：

```
newuser::!:506:506::/home/newuser:/bin/bash
```

如果你记得前面讨论中的 /etc/passwd 字段，你会看到密码字段（第二个字段）设置为 !。这意味着此密码未设置，newuser 尚无法登录。因此，你需要通过运行以下命令为此用户创建密码：

```
passwd newuser
```

系统会要求你两次输入密码，密码被接受后，它会被加密并添加到 /etc/passwd 文件中用户的条目中。

UID 和 GID 值将由 useradd 自动选择。基本上，它只是将 /etc/passwd 中最后一个 UID 增加 1，并将 /etc/group 中最后一个 GID 增加 1，分别创建新用户的 UID 和 GID。你也可以使用命令行开关 -u 和 -g 手动设置 UID 和组。主目录在默认的顶级主目录中创建。同样，登录 shell 从系统默认值中选择。如果你想覆盖系统默认值，可以指定命令行选项。要覆盖默认主目录，请使用 -d newdirectory 选项（其中 newdirectory 是你的目录名称）。例如，

```
useradd newuser -d /www/newuser
```

新用户（newuser）将被创建，其主目录将被设置为 /www/newuser。请注意，useradd 只会创建最后一个目录，而不是整个路径。例如，如果你指定 -d /some/new/dir/myuser 作为选项，useradd 只会在 /some/new/dir/ 已存在的情况下创建 myuser。

当创建新的主目录时，/etc/skel 目录中的文件会被复制到新的主目录中。这些文件通常是默认 shell 的点配置文件。例如，如果默认 shell 是 /bin/bash，则 /etc/skel 目录中应有 .bashrc、.bash_profile 和 .bash_login 的默认版本，以便新用户的主目录可以自动使用这些文件进行设置。

随 Red Hat Linux 提供的 useradd 会为用户创建一个与用户名同名的私有组。例如，如果你运行 useradd kabir，则 /etc/passwd 文件中会创建一个名为 kabir 的新用户，并且 /etc/group 文件中会创建一个名为 kabir 的新组。这种方法允许新用户完全与其它用户隔离，从而确保用户有更大的隐私。无论何时新用户创建一个新文件，由于这个私有组，该文件只能由新用户访问。用户必须显式更改文件权限才能允许其他人查看该文件。

然而，如果你的用户帐户理念与这种私有组想法相冲突，你可以通过使用 -g group 选项（其中 group 是你的组名）来覆盖它。例如，

```
useradd mjkabir -g users
```

使 useradd 创建新用户（mjkabir），其默认组设置为 users。

如果你想使新用户成为系统上其他组的成员，可以使用 -G 以逗号分隔的组列表选项。例如，

```
useradd mjkabir -G wheel,admins
```

将新用户（mjkabir）添加到 /etc/group 文件中的 wheel 和 admins 组。

## userdel

要删除现有用户，请使用 userdel 命令。例如，以下命令删除名为 snake 的用户：

```
userdel snake
```

如果你想删除用户的主目录及其所有内容，请使用 -r 选项。请注意，如果用户当前已登录，userdel 将不会删除该用户。通过发送写消息（write username）要求用户注销，如果要求不是一个选项，请使用 killall 命令终止与该用户关联的所有进程，然后运行 userdel 命令。

- 如果你想暂时禁用用户帐户，可以执行以下操作之一：
  - 使用 usermod -s new shell username 命令将 shell 更改为 /bin/false（确保新 shell 列在 /etc/shells 文件中）。这会禁止用户登录系统。
  - 如果你使用 shadow 密码，请使用 usermod -e MM/DD/YY username 命令使用户帐户过期。

如果你想暂时禁用所有用户帐户访问，可以创建一个名为 /etc/nologin 的文件，其中包含解释为何不允许访问的消息。只要此文件存在，login 程序将不允许任何非 root 帐户登录。

## usermod

usermod 命令用于修改用户帐户。要更改现有用户的主目录，请按如下方式运行 usermod 命令：

```
usermod -d new home directory username
```

其中 new home directory 和 username 是正确的值。

例如，如果一个名为 keller 的用户的主目录是 /home/keller，而你想将其移动到 /home2/keller，可以按如下方式运行 usermod 命令：

```
usermod -d /home2/keller keller
```

这会将新目录设置为她的主目录。但是，如果你想将她主目录的内容移动到新位置，请使用 -m 选项如下：

```
usermod -d -m /home2/keller keller
```

要更改用户的 UID，请按如下方式使用 usermod 命令：

```
usermod -u UID username
```

其中 UID 和 username 是正确的值。

例如，以下命令将用户 mrfrog 的 UID 更改为 500：

```
usermod -u 500 mrfrog
```

用户主目录内由用户拥有 的所有文件和目录将自动反映 UID 更改。但是，如果用户拥有主目录之外的文件，你将必须使用 chown 命令手动更改所有权。

要更改用户的默认组，请按如下方式使用 usermod 命令：

```
usermod -g group name or GID username
```

其中 group name or GID 和 username 是正确的值。

例如，以下命令将用户 mrfrog 的默认组更改为 777：

```
usermod -g 777 mrfrog
```

如果你使用 shadow 密码，可以使用 usermod 命令按如下方式更改用户帐户的到期日期：

```
usermod -e MM/DD/YY username
```

其中 MM/DD/YY 和 username 是正确的值。

例如，以下命令将用户 kabir 的帐户到期日期重置为 12/31/99：

```
usermod -e 12/31/99 kabir
```

如果你使用 shadow 密码，可以使用 usermod 命令按如下方式更改用户帐户的到期日期：

```
usermod -e MM/DD/YY username
```

其中 MM/DD/YY 和 username 是正确的值。

例如，以下命令将用户 kabir 的帐户到期日期重置为 12/31/99：

```
usermod -e 12/31/99 kabir
```

## who

语法：
who

who 命令显示当前登录到系统的用户的信息。你也可以使用 w 命令用于相同目的。

## whoami

语法：
whoami

此命令显示你当前的用户名。
