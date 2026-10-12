
Modify the expire_date field.

```
-E <expire_date>
```

修改 expire_date 字段。可以指定为 YYYY-MM-DD。

```
-W <warn_days>
```

修改 warn_days 字段。

## chfn

chfn 程序用于更改您的 finger 信息。该程序可让您更改 /etc/passwd 中的 GCOS 字段。如果出于安全原因禁用了 finger，这可能对您不太有用。因为 finger 用于显示用户的信息，例如真实姓名、办公地点和办公电话，如果该服务已启用，这些项目应保持最新。像 chage 一样，chfn 有几个选项：

- `-f <full Name>`
- `-o <Office Location/Number>`
- `-p <Office Phone Number>`
- `-h <home Phone Number>`
- `<userid>`

如果您是 root，可以为其他用户更改此信息。

## chgrp

此命令可让您更改文件的组所有权。chgrp 允许您更改文件、特殊文件或目录的组所有权。在部门重组后或通过合并多个较小的项目形成新项目时可能需要此操作。

```
-c
```

更改时提供更多输出。

```
-f
```

不打印错误信息。

```
--reference=<file>
```

使用 <file> 的所有权，而不是在命令行上指定。

```
-R
```

递归子目录。如果在目录名上给出此参数，组更改将应用于文件系统树中该目录下方的所有文件和目录。

```
-v
```

详细输出。

<new groupname>
将文件(们)的组所有权更改为 <new groupname>。

<file file file ...>
要更改所有权的文件。

## chown

此命令更改文件的所有权。chown 允许您指定给定文件、目录或特殊文件的所有者。随着组织内部的变化，人们离职、新人加入等，文件所有权可能需要调整，以便某人的继任者可以继续处理之前开始的文件。根据情况，组管理可能更有效，或者管理单个文件可能最佳。可以使用 chown 的各种参数如下。

- `-c` 更改时提供更多输出。
- `--dereference` 在符号链接上调用时，将更改应用于其指向的文件而不是链接本身。
- `-f` 不打印错误信息。
- `--reference=<file>` 使用 `<file>` 的所有权，而不是在命令行上指定。
- `-R` 递归子目录。如果在目录名上给出此参数，所有权更改将应用于文件系统树中该目录下方的所有文件和目录。
- `-v` 详细输出。
- `<new owner userid>` 将文件(们)的所有权更改为 `<new owner userid>`。
- `<new groupname>` 将文件(们)的组所有权更改为 `<new groupname>`。
- `<new owner userid>.<new groupname>` 更改文件(们)的所有权和组所有权。
- `<file file file ...>` 要更改所有权的文件。

## chsh

此命令更改您的登录 shell。使用 chsh，您可以设置 /etc/passwd 中的条目，该条目指定登录系统时运行的程序。虽然当今许多用户可能直接进入 GUI shell，但许多经验丰富的用户也可能非常习惯命令行以及特定的 shell。

-s 开关决定使用哪个新 shell。默认情况下，如果 <shell> 不存在于 /etc/shells 中，chsh 将输出警告，但可以通过 PAM 配置为仅允许非 root 用户从 /etc/shells 中选择。请参阅第 24 章“Internet Telephony and Conferencing”中的 PAM 部分。

-l 开关将列出 /etc/shells 中的 shell，如果您是 root，可以更改其他用户的 shell。

## gpasswd

gpasswd 用于管理 /etc/group 和 /etc/gshadow。它允许组管理员和 root 添加和删除用户组，以及更改组的密码。gpasswd 有几个选项：

- `-a <user> <group>` 将 <user> 添加到 <group>。
- `-d <user> <group>` 从 <group> 中删除 <user>。
- `-R <group>` 这禁止通过 newgrp 登录。
- `-A <user,user,...> <group>` 将 <user,user,...> 设为 <group> 的组管理员。这些用户将能够使用 gpasswd 添加和删除该组的用户。这不会使 <user,user,...> 成为该组的成员，因此为了让他们能够 newgrp 到 <group>，他们必须使用 -a 选项自行添加，或者 root 必须添加他们。
- `-M <user,user,...> <group>` 将 <user,user,...> 添加到 <group>。
- `-r` 删除组密码。

<group> 如果单独给出此参数，系统会提示输入新的组密码。如果组未设置密码，则只有组成员才能使用 newgrp 命令切换到该组。

## groups

打印您所属的组。然而，它不会列出您是管理员的组。当与 <userid> 一起使用时，它会打印另一个用户所属的组。

## passwd

此命令更改密码令牌。passwd 用于更改您的密码，如果您是 root，则可更改其他密码。

-u 开关仅更改已过期的密码令牌，并保留未过期的令牌。这仅在具有多个具有不同过期时间的身份验证令牌的复杂 PAM 配置中才有用。（请参阅第 24 章关于 PAM 的讨论。）

当 passwd 与 <username> 结合使用时，它会更改 <username> 的密码。只有 root 可以执行此操作，并且身份验证按原样进行。

## su

su（switch user）用于让一个用户暂时“成为”另一个用户。系统会提示用户输入新用户的密码，如果身份验证成功，将使用新用户在 /etc/passwd 中的 shell 参数生成一个新的 shell。如果 shell 参数不可执行，则使用 /bin/sh。

简单的 - 开关将运行新用户的 shell 初始化脚本以重新初始化环境。如果没有此选项，新的 shell 将使用旧用户的环境，但使用新用户的 ID。-c 开关后跟一个命令将导致命令以新用户身份运行，而不是启动交互式 shell。对于 csh 和 tcsh shell，-f 开关将绕过读取 .cshrc，而对于 bash 和 sh，则会禁用文件名模式扩展。

-p 开关将保留当前环境。HOME、USER、LOGNAME 和 SHELL 环境变量不会被触及。SHELL 中指示的 shell 将运行，而不是新用户的 shell，除非原始用户不是 root 且旧用户的 shell 受限。（不在 /etc/shells 中。）

最后，-s 开关后跟一个 shell 名称将运行指定的 shell，而不是从 /etc/passwd 获取的新用户的 shell。

## usermod

此命令允许您修改 /etc/passwd 和 /etc/shadow 中的用户条目。如果用户已登录，则无法更改其用户名。usermod 有几个参数和选项可供使用。它们包括以下内容：

- `-c <comment>` 更改 `/etc/passwd` 中用户的注释/GCOS 字段。通常使用 chfn 更改。
- `-h <home dir>` 将用户的主目录更改为 `<home dir>`。
- `-e <expire date>` 设置帐户将被禁用的日期。`<expire date>` 的格式为 YYYY-MM-DD。
- `-f <inactive days>` 设置密码过期后帐户将被禁用的天数。0 表示密码过期后立即禁用帐户，-1 表示密码过期时永不禁用帐户。
- `-g <group name/GID>` 这设置用户初始或默认组。
- `-G <group,group,...>` 这设置用户除初始组之外的成员资格。在应用此列表之前，所有组成员资格将被删除。
- `-l <userid>` userid 将更改为 `<userid>`。您可能同时想重命名用户的主目录。如果用户当前已登录，此选项将失败。您还必须更改该用户可能正在运行的 cron 和 at 作业的所有权。
- `-s <shell>` 将用户的 shell 更改为 `<shell>`。空白条目表示系统将使用默认 shell。
- `-u <UID>` 将用户的 UID 更改为 `<uid>`。此值在 `/etc/passwd` 中必须是唯一的。请注意，用户将不再能够访问其旧 UID 拥有的文件。您必须找到具有旧 UID 的文件并将其 chown 到新 UID，以便用户能够像以前一样访问它们。请注意，在更改时确保旧 UID 在系统上不拥有任何进程。
- `-o` 此标志禁用 `-u` 选项的唯一性检查，以便多个用户可以具有相同的 UID。

## Summary

在本章中，我们介绍了几种管理用户和组的不同方法。我们讨论了为什么需要有效地管理用户和组，以及如果用户获得超出适当范围的系统访问权限会发生什么。

除了讨论用户和组管理外，我们还查看了可用于自动化相关任务的工具。这些工具有多种形式。它们包括手动编辑相关文件、命令行程序、批处理例程，甚至是 Linuxconf 工具，该工具同时提供文本格式和 X Windows GUI。

最后，我们查看了几个“utility”命令，这些命令允许用户或 root 在必要时快速轻松地调整用户和组参数。
