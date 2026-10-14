
从 `ASSISTANTS` 的用户规范中看到，他们允许通过 `/bin/su` 命令运行所有命令。如你所见，`sudo` 命令在创建具有部分超级用户权限的用户时非常有用。现在你已经掌握了大量关于创建和管理超级用户账户的知识，让我们考虑与普通用户相关的管理问题。

在创建、修改和删除用户账户时，你有两个选择：使用单独命令或 YaST。第一种方法是传统的，第二种是流行的方法。接下来的两个章节将描述如何使用这两种方法。

## 使用命令行工具管理用户

随着 Linux 变得比以往任何时候都流行，SuSE 和整个 Linux 社区正在让使用 Linux 变得更加容易。YaST 项目就是一个很好的例子。然而，仍然需要理解 UNIX 系统的传统方法，以便精通其他 UNIX 操作系统的人员也能轻松地管理 Linux 系统。我们将首先讨论传统方法。

> 后续章节中讨论的命令也适用于影子密码（shadow passwords）。你将在第 17 章中学习影子密码。

## 创建新用户账户

创建新用户账户非常简单。要从命令行创建用户，可以运行 `useradd` 命令。例如，要创建一个名为 `newUser` 的用户，可以如下运行该命令：

```
useradd newUser
```

这将使用系统默认值在 `/etc/passwd` 中添加新条目（如果你使用影子密码，则在 `/etc/shadow` 中添加；详见第 17 章）。例如，当你运行上述命令时，`/etc/passwd` 中添加了以下行：

```
newUser:x:506:100:::/home/newUser:/bin/bash
```

新用户没有设置密码。你必须立即运行 `passwd` 命令为该用户创建密码：

```
passwd newUser
```

你会被要求输入两次密码。一旦密码被接受，它将被加密并添加到 `/etc/passwd` 文件中用户的条目中。GID 值由 `useradd` 自动选择。基本上，`useradd` 将 `/etc/passwd` 中的最后一个用户 UID 加 1，并将 `/etc/group` 中的 GID 加 1，分别为新用户创建 UID 和 GID。主目录创建在默认的顶层主目录下。同样，登录 shell 也从系统默认中选择。你将在本章的“更改 UID”部分学习如何设置这些默认值。如果你想覆盖系统默认值，可以指定命令行选项。要覆盖主目录，使用 `-d` 选项（其中 `d` 是你的目录名称）。在本示例中，创建了新用户（`newUser`），并将主目录设置为 `/home/newUser/`。

```
useradd -d /home/newUser newUser
```

注意，如果你使用 `-d` 选项，`useradd` 会在目录不存在时创建它。例如，如果你指定的目录已存在，`useradd` 将返回错误。如果你想指定不同的 shell，请使用 `-s` 选项：

```
useradd -s /bin/zsh -d /home/newUser newUser
```

## 第 6 章：用户管理

## 修改现有用户账户

处理忘记的用户密码是系统管理员执行的最常见任务。在这里，我们将讨论如何更改用户账户的各种细节。

### 修改密码

要更改或设置用户密码，请使用 `passwd` 命令。例如，以下命令允许你更改用户 `kabir` 的密码：

```
passwd kabir
```

你会被要求输入两次密码以确认。请确保为你的用户选择良好的密码。不要使用常用字典词汇的简单、易记的密码。注意，用户也可以运行 `passwd` 程序来更改自己的密码。当普通用户运行 `passwd` 程序时，不需要用户名参数，因为它允许用户仅更改自己的密码。

### 修改主目录

要更改现有用户的主目录，请按如下方式运行 `usermod` 命令：

```
usermod -d new_home_directory username
```

其中 `new_home_directory` 和 `username` 是正确的值。
例如，如果一个名为 `keller` 的用户主目录为 `/home/keller`，而你想将其移动到 `/home2/keller`，你可以运行以下命令：

```
usermod -d /home2/keller keller
```

这将该新目录设置为她的主目录。但是，如果你想将她的主目录的内容也移动到新位置，请按如下方式使用 `-m` 选项：

```
usermod -m /home2/keller keller
```

### 修改 UID

要更改用户的 UID，请按如下方式使用 `usermod` 命令：

```
usermod -u UID username
```

其中 `UID` 和 `username` 是正确的值。在接下来的示例中，`usermod` 命令将 `myfrog` 的 UID 更改为 500：

```
usermod -u 500 myfrog
```

注意，该用户在其主目录下拥有的所有文件和目录将自动反映 UID 的更改。然而，如果用户在或或主目录之外还拥有文件，你将必须使用 `chown` 命令更改所有权。

> 参阅第 4 章“常用命令”，了解有关如何使用 `chown` 命令的详情。

### 修改默认组

要更改用户的默认组，请按如下方式使用 `usermod` 命令：

```
usermod -g group_name_or_GID username
```

其中 `group_name_or_GID` 和 `username` 是正确的值。

```
groupmod -g 666 troublemakers
```

## 删除或禁用用户账户

要删除现有用户，请使用 `userdel` 命令：

```
userdel snake
```

这将删除一个名为 `snake` 的用户。如果你想删除该用户的主目录及其目录内的所有内容，请使用 `-r` 选项。注意，如果用户当前已登录，`userdel` 将不会删除该用户。向其发送一条写消息（输入 `write username`）要求其注销。如果无法要求，请使用 `killall` 命令终止所有与该用户相关的进程，然后运行 `userdel` 命令。

如果你想临时禁用用户账户，可以采取以下操作之一：

- 使用 `usermod -s new_shell username` 将 shell 更改为 `/bin/false`（确保它在 `/etc/shells` 中）。这将阻止用户登录系统。
- 如果你正在使用影子密码（shadow passwords），可以使用 `usermod -e MM/DD/YY username` 命令让用户账户过期。

如果你想临时禁用所有用户访问，可以创建一个名为 `/etc/nlogin` 的文件，并附上解释为何不允许访问的消息。因此，只要该文件存在，任何非 root 账户将不允许登录。

如果你通过 Telnet 或任何其他方法（如 ssh）管理服务器，请不要创建 `/etc/nlogin`，因为你无法登录系统。这是因为默认情况下，root 或超级用户账户不允许从非安全的 TTY 直接登录（即任何在 `/etc/secure` 中未指定的 TTY）。因此，你可以先作为普通用户登录，然后 `su` 到特权账户。

## 创建默认设置

使用 `useradd` 创建新用户的默认设置来自 `/etc/default/useradd`。该文件的示例见列表 6-2。

列表 6-2：`/etc/default/useradd` 文件

```
# useradd defaults

GROUP=100

HOME=/home
```

## 第二部分：管理用户、进程和网络

```
INACTIVE=-1
EXPIRE=

SHELL=/bin/bash
SKEL=/etc/skel
```

`GROUP=100` 行指定组 ID 为 100。此值仅在使用 `-n` 选项禁用默认私组或与新用户同名的组时使用。你可以指定组名而不是数值。你在该行中指定的值必须存在于 `/etc/group` 中。你可以如下方式更改此值：
