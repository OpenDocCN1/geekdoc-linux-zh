
`username` : `password` : `user ID` : `group ID` : `comment` : `home directory` ;

- `login command`

一个基础的 `/etc/passwd` 文件看起来如下：

```
root::0:0:root:/bin/bash
bin:1:1:bin:/bin
daemon*:2:2:daemon:/sbin
adm:3:4:adm:/var/adm
lp*:4:7:lp:/var/spool/lpd
sync*:5:0:sync:/sbin:/bin/sync
shutdown:*:6:0:shutdown:/sbin:/sbin/shutdown
```

![](img/fbfff30e42d507bc7531108a281d6cf4_668_0.png)

## 系统管理与维护

```
halt*:7:0:halt:/sbin:/sbin/halt
mail*:8:12:mail:/var/spool/mail:
news*:9:13:news:/usr/lib/news:
uucp*:10:14:uuc:/var/spool/uucpublic:
operator*:11:0:operator:/root:/bin/bash
games*:12:100:games:/usr/games:
man*:13:15:man:/usr/man:
postmaster*:14:12:postmaster:/var/spool/mail:/bin/bash
nobody*:1:100:nobody:/dev/null
tftp*:14:50://home/ftp/bash
```

如果某个字段没有需要输入的内容，则留空（参见 `ftp` 条目）。但仍然有一个冒号将该字段与其他字段隔开。以下是每个字段的简要描述：

- `username`: 用户的唯一标识
- `password`: 用户的加密密码
- `user ID` (`UID`): 操作系统用于识别用户的唯一数字
- `group ID` (`GID`): 识别用户组的唯一数字
- `comment`: 执行 `finger` 命令时显示的信息，通常是用户名
- `home directory`: 用户登录时进入的目录
- `login command`: 用户登录时执行的命令，通常是 `shell`

后续章节将对这些字段的内容进行详细说明。

### 用户名

用户名是一个单一字符串。通常在 8 个字符以内。该用户名唯一标识用户，并且应该便于用户识别和记忆。系统通过这个名称识别用户。通常，用户名是由姓和名的字母组合而成的。虽然用户名的命名有一些传统（企业习惯），但计算机并不关心用户名是什么，只要它是唯一的即可。事实上，你可以在用户名中使用下划线、点和某些特殊字符。此外，大小写是有区别的；`dpitts` 或 `DPitts`

### 密码

系统将用户的加密密码存储在密码字段。如果系统使用 `shadow` 密码系统，该字段的值为 `x`。`*` 的值会阻止该账户的登录，因为 `*` 不是加密字段的有效字符。在设置完成后，绝不应手动编辑此字段；你应该使用 `passwd` 程序以确保正确的加密。如果手动更改此字段，旧密码将失效，且可能需要由 `root` 修改。

如果系统使用 `shadow` 密码系统，一个名为 `/etc/shadow` 的单独文件包含密码（当然是加密过的）。`/etc/shadow` 文件的仅允许 `root` 读取。

### 用户 ID

每个用户都有唯一的用户 ID 数字。与用户关联的其他信息并不一定是唯一的，或者在某些情况下，它们与其他用户完全相同。用户 ID (`UID`) 是操作系统识别用户的唯一数字。

### 注释

注释字段是执行 `finger` 命令时显示的信息，通常是用户名。此字段有时被称为 `GECO`。

### 家目录

家目录是用户登录时进入的目录。这通常是 `/home/<username>`。

### 登录命令

登录命令是用户登录时执行的命令，通常是 `shell`。如果此字段留空，系统将默认使用 `/bin/bash`。

![](img/fbfff30e42d507bc7531108a281d6cf4_670_0.png)

# 核心系统管理
第 20 章 635

```
tty::5:
disk::6:root
lp::7:daemon,lp
mem::8:
kmem::9:
wheel::10:root
mail::12:mail
news::13:news
uuccp::14:uucp
man::15:
games::20:
gopher::30:
dp::40:
ftp::50:
nobody::99:
users::100:
utmp:x:101:
xfs:x:102:
floppy:x:103:
solex:x:119:
console:x:103:
gdm:x:42:
ppusers:x:230:
popusers:x:231:
slipusers:x:232:
postgres:x:233:
slocate:x:21:
squid:x:234:
```

每行包含四个部分，与 `passwd` 文件一样，它通过冒号分隔：

组名 : 密码 : 组 ID : 用户

如果某个字段不需要输入内容，则该字段将留空（注意密码字段）。但仍会有冒号将该字段与其他字段分隔。以下是每个字段的简要描述：

- 组名 (`group name`)：组的唯一标识符
- 密码 (`password`)：通常留空或为 `*`，但也可以分配密码
- 组 ID (`group ID`)：操作系统识别组的唯一数字
- 用户 (`users`)：属于该组的所有用户 ID 列表

与 `/etc/passwd` 文件一样，编辑此文件有两种方法。第一种是使用脚本，例如 `addgroup` 或 `groupadd`；第二种是使用文本编辑器手动编辑文件。（顺便说，在编辑文件之前，务必确保已创建文件的备份。）向此文件中添加组时，只需遵循其他行的格式即可。

![](img/fbfff30e42d507bc7531108a281d6cf4_672_0.png)

添加一个唯一的组，必要时为其分配密码，赋予一个唯一的组 ID，然后列出与该组相关的用户。顺便说，用户之间用逗号分隔。如果行格式不正确或在其他方面有误，用户可能无法使用该组 ID。

如果系统使用影子密码系统（`shadow password system`），则密码字段将移动到 `/etc/shadow.group`，并为该字段分配一个 `x`。

完成编辑 `/etc/group` 文件后，双检其权限。它应该由 `root` 所有，其所属组应为 `root` 或 `sys`（组 ID 为 0）。权限应为 `root` 具有读写权限，而其他人只有读取权限（八进制为 644）。

组列表不需要任何特定的顺序。每个组中的用户列表也无关。Red Hot Linux 将搜索整个文件，直到找到它正在寻找的行。

虽然用户可以属于多个组，但 Linux 仅允许他们在任何时刻处于一个组中。起始组（通常称为主组）是在 `/etc/passwd` 文件中标识的组。如果用户想切换到另一个组（且根据 `/etc/group` 他属于该组），用户必须执行 `newgrp` 命令进行切换。

从组中删除组或用户非常简单，只需编辑 `/etc/group` 文件并删除整行或要删除的特定用户。您还应该检查 `/etc/passwd` 文件，以确保您删除的组没有定义任何用户。

# 创建家目录并将文件复制到新家目录

如果新用户已添加到 `/etc/passwd` 和 `/etc/group` 文件，下一步是创建用户的新家目录。在本章的剩余部分中，假设家目录为 `/home/username`。

要创建目录，请进入 `/home` 目录（`cd home`），并执行 `mkdir` 命令。传递给 `mkdir` 命令的参数是您想要创建的目录。在接下来的示例中，我正在为 `tpowerell` 创建用户目录：

```
shell:/home/dpitts$ cd /home
shell:/home/dpitts$ mkdir tpowerell
```

现在我为我的朋友 Tim 准备了一个目录。有了这个目录，我需要从 `/etc/skel` 将文件复制到新家目录。这通过 `cp` 命令完成，如下例所示：

```
shell:/home/dpitts$ cp /etc/skel/* /home/tpowerell
```
