
```bash
# /usr/sbin/useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

此示例显示，新账户默认会被分配到 GID 为 `100` 的组中，并且其主目录默认会作为 `/home` 目录的子目录创建。如果未指定 shell，则默认使用 Bash 作为默认 shell，并会从 `/etc/skel` 复制主目录内容。

你可以使用 `useradd` 命令的 `-D` 参数，后跟表 3.2 中列出的一个或多个参数来更改这些设置。

### 表 3.2 — 用于更改默认设置的 useradd 命令参数

| 参数 | 描述 |
|---|---|
| `-b <directory>` | 对于创建时未指定主目录的账户，使用指定的目录作为其主目录的前缀。 |
| `-g <Group name or GID>` | 对于创建时未指定组的账户，使用指定的组作为其默认组。 |
| `-s <shell>` | 对于创建时未指定 shell 的账户，使用指定的 shell 作为其默认 shell。 |

例如，你的站点可能有以下特殊要求：

- 所有用户的主目录都应采用 `/u/<username>` 的形式，而不是 `/home/<username>`。
- 所有用户都应使用 C shell 而不是 Bash。

在这种情况下，你可以使用以下命令更改 `useradd` 的默认设置，这样就不必在每次创建账户时都列出这些特殊要求：

```bash
# useradd -D -b /u -s /bin/csh
```

完成此操作后，使用 `useradd -D` 将显示 `useradd` 的默认设置，这些设置应反映上述更改：

```text
# /usr/sbin/useradd -D
GROUP=100
HOME=/u
INACTIVE=-1
EXPIRE=
SHELL=/bin/csh
SKEL=/etc/skel
```

## 更改用户信息（用户名、默认 shell 等）

你可以根据要更改的信息通过多种方式更改用户信息，具体如下：

- **用户名：** 编辑 `/etc/passwd` 文件，如有需要，更改主目录的名称。
- **密码：** 使用 `passwd` 命令。
- **UID：** 理想情况下，你不应更改用户的 UID，但如果确实需要更改，请编辑 `/etc/passwd` 文件，然后使用 `find` 和 `chown` 命令更改该用户拥有的所有文件的所有权。
- **GID：** 编辑 `/etc/passwd` 和 `/etc/group` 文件。
- **全名：** 编辑 `/etc/passwd` 文件。
- **主目录：** 如有必要，将用户的主目录移动到新位置，然后编辑 `/etc/passwd` 文件。
- **默认 shell：** 使用 `chsh` 命令或手动编辑 `/etc/passwd` 文件。

### 更改账户的用户名

要更改账户的用户名，只需按照前面“编辑 `/etc/passwd` 文件”部分所述，使用 `vipw` 命令编辑 `/etc/passwd` 文件。由于内核使用 UID 来识别用户，因此所有对用户名的引用（例如目录列表中的所有权标识）都会反映用户名的更改，因为 UID 并未改变。

例如，如果你将某个账户的用户名从 `user1` 更改为 `user2`，在更改之前，该账户拥有的文件在目录列表中显示为：

```text
-rw-rw-r-- 1 user1 somegrp 12 Jan 28 18:31 foo
```

在编辑 `/etc/passwd` 文件中的用户名之后，同一文件在目录列表中显示为：

```text
-rw-rw-r-- 1 user2 somegrp 12 Jan 28 18:31 foo
```

除了编辑 `/etc/passwd` 文件之外，你还需要编辑 `/etc/group` 文件，并将其中对 `user1` 的引用全部更改为 `user2`。

如果你希望主目录与账户用户名保持同步，则需要移动主目录并编辑 `/etc/passwd` 中该账户的条目以反映更改。例如，如果更改前用户的主目录是 `/home/user1`，你可能希望将其更改为 `/home/user2`。

首先，使用以下命令将主目录移动到新位置：

```text
# mv /home/user1 /home/user2
```

接下来，使用 `vipw` 命令编辑 `/etc/passwd` 文件以反映更改。

### 更改账户的密码

`root` 用户可以使用 `passwd` 命令更改任何用户的密码，具体格式为：`passwd <username>`。作为 `root` 用户，更改用户密码时不需要知道该用户的现有密码。例如，要更改用户密码，请使用以下命令：

```text
# passwd user1
Changing password for user user1
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully
```

### 更改账户的 UID

更改账户的 UID 是一项剧烈的操作，应尽量避免。它会改变账户的标识符，实际上会使内核将其视为不同的账户。如果你更改某个账户的 UID，该账户将立即失去其之前拥有的所有文件或目录的所有权，而且如果应用程序配置为通过 UID 而非用户名来识别该账户，它们将不再识别该账户。

要更改账户的 UID，首先按照前面“编辑 `/etc/passwd` 文件”部分所述，使用 `vipw` 命令编辑 `/etc/passwd`，更改该账户条目中的 UID。请务必记下该账户的原始 UID，因为你将需要它来更改该账户拥有的所有文件的所有权。

在 `/etc/passwd` 文件中更改 UID 后，该账户将不再拥有其文件。例如，如果你将 `user1` 的 UID 从 `500` 更改为 `999`，在更改之前，该账户拥有的文件和目录在目录列表中显示如下：

```text
-rw-rw-r--  1 user1  somegrp     12 Jan 28 18:31 foo
```

更改之后，该文件在目录列表中显示如下：

```text
-rw-rw-r--  1 500    somegrp     12 Jan 28 18:31 foo
```

请注意，该文件不再归属于 `user1`，但仍然归属于 UID `500`。

一旦在 `/etc/passwd` 文件中更改了 UID，你就需要查找所有由 UID `500` 拥有的文件，并将所有权更改为 `user1` 账户。为此，请使用 `find` 命令查找所有由 UID `500` 拥有的文件和目录，然后使用 `-exec` 选项调用 `chown` 命令来更改文件的所有权：

```text
# find / -uid 500 -print -exec chown user1 {} \;
```

### 更改账户的 GID

要更改账户的默认组，请按照前面“编辑 `/etc/passwd` 文件”部分所述，使用 `vipw` 编辑 `/etc/passwd` 文件，并将该账户的 GID 字段更改为新默认组的 GID。

接下来，编辑 `/etc/group` 文件，将用户从原始默认组的用户列表中删除。然后将该用户添加到新默认组的用户列表中。

### 更改账户的全名

要更改账户的全名，只需按照前面“编辑 `/etc/passwd` 文件”部分所述，使用 `vipw` 命令编辑 `/etc/passwd` 文件并进行必要的更改。

更改账户的全名不会影响账户的运行，因为系统或其应用程序不会以任何方式使用全名来标识账户。全名仅用于描述目的，绝不影响系统或任何应用程序的运行。

### 更改账户的主目录

要更改账户的主目录，你需要移动主目录，然后编辑 `/etc/passwd` 文件中该账户的条目以反映更改。首先，使用 `mv` 命令将主目录移动到新位置：

```
# mv <old location> <new location>
```

接下来，使用 `vipw` 命令编辑 `/etc/passwd` 文件以反映更改。

### 更改账户的默认 Shell

你可以使用 `chsh` 命令将账户的默认 Shell 更改为 `/etc/shells` 文件中列出的任何有效 Shell。其最简单的形式是，向 `chsh` 命令指定账户的用户名，`chsh` 会提示你输入新的默认 Shell：

```
# chsh user1
Changing shell for user1.
New shell [/bin/bash]: /bin/csh
Shell changed.
```

如果你输入的 Shell 未在 `/etc/shells` 文件中列出，`chsh` 会警告你该 Shell 无效，但仍会更改账户的默认 Shell：
