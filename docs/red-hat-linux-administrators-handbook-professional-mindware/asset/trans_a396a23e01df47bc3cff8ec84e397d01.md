

而不仅仅是整个路径。例如，如果您指定 `-d /some/new/dir/myuser` 作为选项，useradd 仅当 `/some/new/dir/` 已存在时才会创建 myuser。

当创建新的主目录时，`/etc/skel` 目录中包含的文件会被复制到新的主目录中。这些文件通常是默认 Shell 的点配置文件（dot configuration files）。例如，如果默认 Shell 是 `/bin/bash`，您应该在 `/etc/skel` 目录中有 `.bashrc`、`.bash_profile` 和 `.bash_login` 的默认版本，以便新用户的主目录可以使用这些文件自动设置。

Red Hat Linux 随附的 useradd 会为用户创建一个与用户名同名的私有组。例如，如果您运行 `useradd kabir`，则会在 `/etc/passwd` 文件中创建一个名为 kabir 的新用户，并在 `/etc/group` 文件中创建一个名为 kabir 的新组。这种方法允许新用户与其他用户完全隔离，从而确保用户拥有更高的隐私性。每当新用户创建新文件时，由于这个私有组的作用，该文件仅可由该新用户访问。用户必须显式更改文件权限才能允许其他人查看该文件。

但是，如果您的用户账户理念与这种私有组理念相冲突，您可以使用 `-g group` 选项（其中 `group` 是您的组名）来覆盖它。例如，

```
useradd mykabir -g users
```

会使 useradd 创建新用户（mykabir）并将默认组设置为 users。

![](img/f9ec99365f159bfe663f8ac29732663c_116_0.png)

> **提示**
> 您可以使用 `groups username` 命令来查找某个用户属于哪些组。

如果您希望将新用户作为系统中其他组的成员，请使用 `-G comma-separated list of groups` 选项。例如，

```
useradd mykabir -G wheel,admins
```

将在 `/etc/group` 文件中将新用户（mykabir）添加到 wheel 和 admins 组。

## 创建新组

要创建新组，请使用 groupadd 命令。例如，以下命令在 /etc/group 和 /etc/gshadow 文件（如果您使用的是 shadow passwords）中添加了一个名为 mygroup 的新组：

```
groupadd mygroup
```

默认情况下，groupadd 程序创建的组 GID 大于 499，因为 0 到 499 之间的 GID 是（某种程度上）保留给系统级账户的，例如 root、bin 和 mail。因此，如果您的 /etc/group 文件中最后一个组的 GID 设置为 511，那么通过此程序创建的新组的 GID 将为 512，依此类推。如果您想明确设置新组的 GID，请使用 -g GID 选项。此外，如果您想创建一个 GID 在 0 到 499 范围内的组，请使用 -r 选项结合 -g GID 选项，以强制 groupadd 将新组创建为系统组。请注意，如果您尝试在 /etc/group 中使用的组或 GID 已被占用，您将收到错误消息。

## 修改现有用户账户

处理用户遗忘的密码是系统管理员最常执行的任务之一。本节介绍如何更改用户账户的各种详细信息。

### 更改密码

要更改或设置用户密码，请使用 passwd 命令。例如，以下命令允许您更改用户 kabir 的密码：

```
passwd kabir
```

系统会要求您两次输入密码以进行确认。请为您的用户选择良好的密码。不要使用容易记忆的、使用常见字典单词的密码。请注意，passwd 程序也可以由用户运行以更改其自己的密码。当普通用户运行 passwd 程序时，不需要提供用户名参数，因为它只允许他们更改自己的密码。

### 更改 Shell

如果默认 Shell 不适合某个用户，您可以将其更改为 /etc/shells 中列出的任何 Shell。使用 chsh 命令来更改用户的 Shell。例如，以下命令允许您更改用户 brian 的当前 Shell：

```
chsh brian
```

如果您指定了任何不在 /etc/shells 中的 Shell 或程序名称，该用户将无法登录。请注意，用户可以使用此命令更改自己的 Shell。普通用户不需要将用户名作为参数指定，因为他们只能更改自己的 Shell。

您也可以使用 usermod 命令来修改 Shell 信息，如下所示，

```
usermod -s new shell path username
```

其中 new shell path 和 username 是正确值。

### 更改主目录

要更改现有用户的主目录，请运行 usermod 命令，如下所示，

```
usermod -d new home directory username
```

其中 new home directory 和 username 是正确值。

例如，如果名为 keller 的用户其主目录为 /home/keller，而您想将其移动到 /home2/keller，请运行以下 usermod 命令：

```
usermod -d /home2/keller keller
```

这将新目录设置为她的新主目录。但是，如果您想将她主目录的内容移动到新的位置，请使用 -m 选项，如下所示：

```
usermod -d -m /home2/keller keller
```

### 更改 UID

要更改用户的 UID，请使用 `usermod` 命令，如下所示，

```
usermod -u UID username
```

其中 `UID` 和 `username` 是正确值。

例如，以下命令将用户 `mrfrog` 的 UID 更改为 500：

```
usermod -u 500 mrfrog
```

该用户主目录内所有属于该用户的文件和目录将自动反映 UID 的更改。但是，如果该用户拥有其主目录以外的文件，您将必须使用 `chown` 命令手动更改所有权。

### 更改默认组

要更改用户的默认组，请使用 `usermod` 命令，如下所示，

```
usermod -g group_name or GID username
```

其中 `group_name` 或 `GID` 和 `username` 是正确值。

例如，以下命令将用户 `mrfrog` 的默认组更改为 777：

```
usermod -g 777 mrfrog
```

### 更改账户过期日期

如果您使用的是 shadow passwords，请使用 `usermod` 命令更改用户账户的过期日期，如下所示，

```
usermod -e MM/DD/YY username
```

其中 `MM/DD/YY` 和 `username` 是正确值。

例如，以下命令将用户 `kabir` 的账户过期日期重置为 12/31/99：

```
usermod -e 12/31/99 kabir
```

### 更改 finger 信息

如果您允许用户使用 finger 程序来查找彼此，或者运行 finger 守护进程以便外部人员可以 finger 您的账户，您也可以更改 finger 信息，例如全名和电话号码。运行 chfn 命令来更改用户的 finger 信息。

例如，以下命令允许您更改用户 jennifer 的 finger 信息，这些信息存储在 /etc/passwd 文件中：

```
chfn jennifer
```

用户也可以使用此程序更改自己的 finger 信息。用户还可以在主目录中创建一个 .plan 文件，该文件将被追加到 finger 程序显示的信息中。

## 修改现有组

要修改现有组的名称或 GID，请使用 groupmod 命令。要将组重命名为新名称，请使用以下语法：

```
groupmod -n new group current group
```

例如，以下命令将现有的 novices 组重命名为 experts：

```
groupmod -n experts novices
```

要更改 GID，请使用 -g new GID 选项。例如，以下命令将 troublemakers 组的当前 GID 更改为 666：

```
groupmod -g 666 troublemakers
```

## 删除或禁用用户账户

要删除现有用户，请使用 userdel 命令。例如，以下命令删除名为 snake 的用户：

```
userdel snake
```

如果您想删除用户的主目录及其所有内容，请使用 -r 选项。请注意，如果用户当前已登录，userdel 将不会删除该用户。请让用户通过发送写入消息（*write username*）来注销，如果要求用户注销不可行，请使用 killall 命令终止与该用户相关的所有进程，然后运行 userdel 命令。

如果您想暂时禁用用户账户，您可以执行以下操作之一：

- 使用 usermod -s new shell username 命令将 Shell 更改为 /bin/false（确保新 Shell 已列在 /etc/shells 文件中）。这将禁止用户登录系统。
- 如果您使用的是 shadow passwords，请使用 usermod -e MM/DD/YY username 命令使该用户账户过期。

如果您想暂时禁用所有用户账户的访问，您可以创建一个名为 /etc/nologin 的文件，其中包含一条解释为何不允许访问的消息。只要该文件存在，登录程序就不允许任何非 root 账户登录。

## 注意

> 如果您通过 Telnet 或其他方式（如 secure shell (ssh) 访问）管理服务器，请勿创建 /etc/nologin，因为您将无法登录您的系统。这是因为，默认情况下，root 或超级用户账户不允许直接从非安全 TTY（即未在 /etc/securetty 中指定的任何 TTY）登录，因此您不能先以普通用户登录，然后 su 到特权用户账户。

## 创建默认用户设置

使用 useradd 创建新用户的默认设置来自 /etc/default/useradd。该文件的一个示例如图 5-2 所示。

### 图 5-2 /etc/default/useradd 文件示例

```
# useradd defaults file
GROUP=100
HOME=/home
INACTIVE=-1
```

