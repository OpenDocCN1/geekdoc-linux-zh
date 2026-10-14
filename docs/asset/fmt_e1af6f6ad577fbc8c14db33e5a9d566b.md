
只有在没有用户将此组分配为主组时，才能删除该组。

- `groupmod` — 修改现有组的设置（如 GID、组名和用户）。

以下为示例：

- 更改 GID：

`groupmod --g 201 sports`

- 将组名从 sports 改为 water：

`groupmod --n water sports`

- 将用户 geeko 添加到组：

`groupmod --A geeko water`

- `gpasswd` — 更改组账户的密码。只有管理员可以更改任何组的密码。组密码可使用选项 `-r` 移除。

![](img/9129877170834ca9d5fdac5319bf5f12_295_0.png)

你可以通过查阅在线手册页（如 `man groupadd`）或在线帮助页（如 `groupadd --help`）了解有关这些命令的更多信息。

如果你想了解你所属的组的信息，请输入 `groups`。你可以通过输入 `group user` 指定特定用户。

```
geeko@da10:~> groups geeko
geeko : users dialout video
geeko@da10:~>
```

`newgrp` 命令允许你更改执行用户的有效组。

```
geeko@da10:~> id
uid=1000(geeko) gid=100(users)
groups=16(dialout),33(video),100(users)
geeko@da10:~> newgrp video
geeko@da10:~> id
uid=1000(geeko) gid=33(video)
groups=16(dialout),33(video),100(users)
geeko@da10:~> exit
geeko@da10:~> id
uid=1000(geeko) gid=100(users)
groups=16(dialout),33(video),100(users)
geeko@da10:~>
```

在此示例中，你可以看到当前 shell 被替换为新 shell。如果组有密码且用户未在组文件中列为该组的成员，则会要求输入密码。

## 用户和组配置文件

使用 YaST 或命令行工具创建或编辑用户和组时输入的信息会保存到以下用户管理文件中：

- `/etc/passwd`

- `/etc/shadow`

- `/etc/group`

![](img/9129877170834ca9d5fdac5319bf5f12_296_0.png)

尽可能不要使用编辑器修改这些文件。而应使用 YaST 中提供的“安全和用户”模块或“管理用户”中描述的命令行工具。使用编辑器修改这些文件可能导致错误（尤其是在 `/etc/shadow` 中），例如用户（包括 root 用户）无法再登录。

### /etc/passwd

`/etc/passwd` 文件存储每个用户的相关信息，如用户名、UID、home 目录和登录 shell。

过去，`/etc/passwd` 也包含加密密码。然而，由于该文件需要对所有人可读（例如，使用 `ls -l` 时显示用户名和组名），加密密码现在存储在 `/etc/shadow` 中，后者仅 root 和 shadow 组成员可读。

以下是 `/etc/passwd` 文件的示例：

```text
at:x:25:25:Batch jobs daemon:/var/spool/atjobs:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
ftp:x:40:49:FTP account:/srv/ftp:/bin/bash
games:x:12:100:Games account:/var/games:/bin/bash
gdm:x:50:15:Gnome Display Manager daemon:/var/lib/gdm:/bin/bash
haldaemon:x:101:102:User for haldaemon:/var/run/hal:/bin/false
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
...
geeko:x:1000:100:Geeko Chameleon:/home/geeko:/bin/bash
```

`/etc/passwd` 文件中的每一行代表一个用户，并包含图 9-9 所示的信息（以冒号分隔）。

![](img/9129877170834ca9d5fdac5319bf5f12_297_0.png)

请注意每行中字段的以下内容：

- `用户名`—这是用户登录系统时输入的名称（登录名）。

- `密码`—此字段中的 x 表示密码存储在 `/etc/shadow` 文件中。

- `UID`—根据 Linux 标准，保留了三个数字范围：

  - 0 用于 root

  - 1–99 用于系统本身

  - 100–499 用于特殊系统用户（如服务和程序）

  - 1000+ 用于普通用户

- `GID`—组编号。根据 Linux 标准，保留了两个数字范围：

  - 0–99 用于特殊系统组，包括 root（如服务和程序）

  - 100+ 用于普通组

- `注释字段`—通常在此处存储用户的全名。房间号或电话号码等信息也可以存储在此处。

- `主目录`—用户的个人目录通常位于 `/home` 目录下，并与用户（登录）名相同。

- `登录 Shell`—用户成功登录后启动的 shell。在 Linux 中，这通常是 `/bin/bash`（Bourne Again shell）。shell 必须列在 `/etc/shells` 文件中。

![](img/9129877170834ca9d5fdac5319bf5f12_298_0.png)

有关此文件的更多信息，请输入 `man 5 passwd`。

shell 必须列在 `/etc/shells` 文件中。

## /etc/shadow

`/etc/shadow` 文件存储加密的用户密码和密码过期信息。大多数 Linux 系统使用 shadow 密码。

该文件只能由 root 用户更改，并可由 root 用户和 shadow 组成员读取。以下是 `/etc/shadow` 文件的示例：

```
at:!:13181:0:99999:7:::
bin:*:13181::::::
daemon:*:13181::::::
ftp:*:13181::::::
games:*:13181::::::
gdm:!:13181:0:99999:7:::
lp:*:13181::::::
root:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181:0:99999:7:-1::
xay0u3:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181::::::
sshd:!:13181:0:99999:7:::
ucp:*:13181::::::
wwwrun:+:13181::::::
geeko:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181:0:99999:7:-1::
```

`/etc/shadow` 文件中的每一行属于一个用户，并包含图 9-10 所示的字段。

![](img/9129877170834ca9d5fdac5319bf5f12_298_1.png)

Figure 9-10

图 9-10 显示了用户 geeko 的条目，其中包含加密密码。明文密码是 novel1。

加密密码使用 Blowfish 算法编码。加密词由字母、数字和一些特殊字符组成。如果在 Password 字段中出现无效字符（如“*”或“!”），则该用户具有无效密码。

许多用户，如 wwwrun（Apache Web 服务器）或 bin，在 Password 字段中有星号（“*”）。这意味着这些用户无法登录系统，但对于特殊应用程序是必需的。

如果 Password 字段为空，则用户可以在不输入密码的情况下登录系统。Linux 系统中应始终设置密码。

每行末尾的信息决定了一些限制：

- `上次更改`—上次密码更改日期。该数字代表自 1970 年 1 月 1 日以来的天数。

- `下次可更改`—用户可以在更改密码之前密码的最小使用期限。

- `下次必须更改`—用户可以在密码过期前使用同一密码的天数。

- `警告`—密码过期前用户获得警告的天数。输入 −1 以禁用警告。

- `限制`—密码过期后用户仍可登录的天数。输入 −1 表示无限访问。（当然，这没有意义。）

- `锁定`—账户过期的日期。日期必须采用 YYYY-MM-DD 格式。如果账户永不过期，请将字段留空。

## /etc/group

`/etc/group` 文件存储组信息。以下是 `/etc/group` 文件的示例。
