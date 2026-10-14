
- **当前默认（有效）组**：`gid=100(users)`

- **geeko所属的所有组**：`groups=16(dialout), 33(video), 100(users)`。

如果你想获取所属组的信息，输入 `groups`。你可以通过输入 `groups user` 指定特定用户。

```
geeko@da51:~ groups geeko
geeko : users dialout video
geeko@da51:~
```

你可以通过输入 `finger user` 显示本地用户的额外信息，如下所示：

```
geeko@da51:-> finger geeko
Login: geeko Name: Geeko Chameleon
Directory:/home/geeko Shell: /bin/bash
On since Fri Feb 10 12:50 (MST) on :0 (messages off)
On since Fri Feb 10 13:38 (MST) on pts/0.0
No Mail.
No Plan.
geeko@da51:->
```

# 普通用户 vs. 系统用户

在 Linux 操作系统中，有两种基本的用户账户类型：

- 普通用户（Regular users）。这些是允许登录 Linux 环境的用户账户。这种登录方式为人们访问数据和应用程序提供了一个安全环境。这些用户账户由系统管理员管理。

- 系统用户。这些是在安装期间创建的用于账户，供服务、工具和其他应用程序在服务器上有效运行。这些用户不需要任何维护。

所有用户都存储在 `/etc/passwd` 和 `/etc/shadow` 文件中。

# 用户和组配置文件

Linux 系统将所有用户和组配置数据存储在以下文件中：

- `/etc/passwd`

- `/etc/shadow`

- `/etc/group`

在可能的情况下，你不应该使用编辑器修改这些文件。相反，请使用 YaST 提供的“安全与用户”模块，或使用 8-27 节“从命令行管理用户和组账户”中描述的命令行工具。

使用编辑器修改这些文件可能会导致错误（特别是在 `/etc/shadow` 中），例如用户（包括 root 用户）无法再次登录。

## `/etc/passwd`

`/etc/passwd` 文件存储了每个用户的信息，例如用户名、UID、家目录和登录壳（shell）。

在过去，`/etc/passwd` 还包含加密后的密码。然而，由于该文件需要对所有用户可读（例如，在使用 `ls -l` 时显示用户和组名），现在加密后的密码被存储在 `/etc/shadow` 中，该文件只有 root 用户和 shadow 组的成员可读。

## 以下是 `/etc/passwd` 文件的示例：

```
at:x:25:25:Batch daemon:/var/spool/jobs:/atjobs:/bin/bash
bin:x:1:1:bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
ftp:x:40:49:FTP account:/srv/ftp:/bin/bash
games:x:12:100:Games /var/games:/bin/bash
gdm:x:50:15:nome Display Manager:/var/lib/gdm:/bin/bash
haldaen:x:101:102:User for haldaen:/var/run/halib:/bin/false
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
mail:x:8:12:Mailer daemon:/var/spool/clientqueue:/bin/false
man:x:13:62:Manual pages viewer:/var/cache/man:/bin/bash
ndsd:x:78:65534:mdNSResponder runtime:/var/lib/mdns:/bin/false
messagebus:x:101:101:User for D-BUS:/var/run/db:/bin/false
news:x:9:9:News system:/etc/news:/bin/bash
nobody:x:103:65534:65534:nobody:/var/lib/nobody:/bin/bash
tp:x:74:103:NTP daemon:/var/lib/ntp:/bin/false
postfix:x:51:51:Postfix Daemon:/var/spool/postfix:/bin/false
root:x:0:0:root:/bin/bash
sshd:x:71:65:SSH daemon:/var/lib/sshd:/bin/bash
uucp:x:10:14:Unix-to-Unix Copy system:/etc/uucp:/bin/bash
wwwrun:x:30:8:WW daemon apache:/var/lib/wwwrun:/bin/false
geeko:x:1000:1000:Geeko Chameleon:/home/geeko:/bin/bash
```

`/etc/passwd` 文件中的每一行代表一个用户，并包含以下信息（用冒号分隔）：

![](img/428e877abd09b1c11149d179d3458f12_274_0.png)

| 用户名 | UID | GID | 密码 | 家目录 | 登录 shell |

| :--- | :--- | :--- | :--- | :--- | :--- |

注意每行中字段的以下几点：

- `用户名`。这是用户登录系统时输入的名称（登录名）。

- `密码`。此字段中的 `x` 表示密码存储在 `/etc/shadow` 文件中。

- `UID`。根据 Linux 标准，有三个保留的数字范围：

  - 00–99 用于系统本身。

  - 100–499 用于特殊系统用户（如服务和程序）。

  - 普通用户从 UID 1000 开始。

- `GID`。组的编号。根据 Linux 标准，有两个保留的数字范围：

  - 00–99 用于特殊系统组（如服务和程序）。

  - 普通组从 GID 100 开始。

- `注释字段`。通常情况下，这里存储用户的全名。也可以存储房间号或电话号码等信息。

- `家目录`。用户的个人目录通常位于 `/home` 目录下，并与用户名（登录名）相同。

- `登录 shell`。这是用户成功登录后为其启动的 shell。在 Linux 中，这通常是 `/bin/bash` (Bourne Again Shell)。

该 shell 必须在 `/etc/shells` 文件中列出。

有关此文件的更多信息，请输入 `man 5 passwd`。

## `/etc/shadow`

`/etc/shadow` 文件存储加密的用户密码和密码过期信息。大多数 Linux 系统使用 shadow 密码。

该文件只能由 root 用户更改，并由 shadow 组的成员读取。以下是 `/etc/shadow` 的示例：

```
at::13181:0:99999:7::
bin::13181:0:99999:7::
daemon::13181:0:99999:7::
ftp::13181:0:99999:7::
games::13181:0:99999:7::
gdm::13181:0:99999:7::
haldaen::13181:0:99999:7::
lp::13181:0:99999:7::
mail::13181:0:99999:7::
man::13181:0:99999:7::
ndsd::13181:0:99999:7::
messagebus::13181:0:99999:7::
news::13181:0:99999:7::
nobody::13181:0:99999:7::
tp::13181:0:99999:7::
postfix::13181:0:99999:7::
root::13181:0:99999:7::
sshd::13181:0:99999:7::
uucp::13181:0:99999:7::
wwwrun::13181:0:99999:7::
geeko::13181:0:99999:7::
```

*(注：由于原文中 `/etc/shadow` 示例存在大量重复的占位符，译文保持了其逻辑结构，但根据示例要求不翻译代码块内容。此处为保持格式对齐，实际翻译中通常保持代码块原样)*

*修正：由于原文文本中 `/etc/shadow` 示例部分似乎存在重复错误，根据“代码块不需要翻译”的原则，应保持其原始样貌。*
