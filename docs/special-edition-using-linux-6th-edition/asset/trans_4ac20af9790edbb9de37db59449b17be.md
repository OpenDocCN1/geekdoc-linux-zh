

## 添加用户

用户帐户可以通过直接编辑 `/etc/passwd` 文件，或使用所有 Linux 发行版中都可用的 `useradd` 等工具来添加。每个用户帐户的默认特性由 `/etc/login.defs` 文件中的设置定义，如下所示：

```text
###
# Password aging controls: (used by useradd and pwconv)
#
# Maximum number of days a password may be used:
# (-1 = no password changes are necessary)
PASS_MAX_DAYS -1

# Minimum number of days allowed between password
# changes:
PASS_MIN_DAYS 0

# Number of days warning given before a password expires:
PASS_WARN_AGE 7

# Number of days till account is closed after password
# has expired:
PASS_INACTIVE -1

# Force expiry at given day: (in days after 70/1/1,
# -1 = don't force)
PASS_EXPIRE -1

###
# Default values for useradd
#

# default group:
GROUP 100

# user's home directory: (%s = name of user)
HOME /home/%s

# default user shell:
SHELL /bin/bash

# directory where the home directory skeleton is located:
SKEL /etc/skel

###
# Min/max values for automatic gid selection in groupadd
#
GID_MIN 100
GID_MAX 60000
```

`useradd` 工具默认不会创建新用户的主目录，但如果提供正确的参数，则会创建主目录。例如，使用 `useradd` 为一个名为 natalie 的人创建帐户，并指定以下参数，就会创建 `/etc/passwd` 和 `/etc/shadow` 条目以及 `/home/natalie` 目录：

```bash
# useradd -m -d /home/natalie natalie
```

会创建一个新目录 `/home/natalie`，并用 `/etc/skel` 和 `/etc/skel.d` 目录中的默认文件副本填充（按此顺序）。`/etc/skel` 目录包含以下文件：

```
.bash_logout
.bashrc
.cshrc
.emacs
.gnupg/
.inputrc
.kshrc
.login
.logout
.profile
.profile.ksh
.tcshrc
Desktop/
```

```
.gnupg:
./
../
options

Desktop:
./
../
OpenStore.kdelnk
Register Now!.kdelnk
```

`/etc/skel.d` 目录包含以下内容：

```
.config
bash/
common/
csh/
sh/
tcsh/
```

```
bash:
    .bash_logout
    .bashrc

common:
    .inputrc

csh:
    .cshrc
    .login
    .logout

sh:
    .profile

tcsh:
    .tcshrc
```

`/etc/skel.d/` 中的一些文件与 `/etc/skel/` 中的文件重复。在这种情况下，`/etc/skel.d/` 中的文件将覆盖从 `/etc/skel/` 复制的文件。

使用 `-D` 选项运行 `useradd` 将显示用户帐户的默认特性：

```bash
# useradd -D
GROUP=100
HOME=/home/%s
SHELL=/bin/bash
SKEL=/etc/skel
PASS_MIN_DAYS=0
PASS_MAX_DAYS=-1
PASS_WARN_DAYS=7
PASS_INACTIVE=-1
PASS_EXPIRE=-1
```

这些就是之前看到的参数，定义在 `/etc/login.defs` 文件中。只需修改 `/etc/login.defs` 文件中的条目即可轻松更改这些参数。

## 删除或禁用用户

可以通过简单地修改 `/etc/passwd` 文件中某个用户的条目来禁用用户帐户。例如，可以通过如下更改密码字段来禁用用户 natalie 的帐户：

```text
natalie:x123:100:100:OpenLinux User:/home/natalie:/bin/bash
```

当在 `x` 后面添加任何内容时（此处为 123），shadow 实用程序将不再查看 `/etc/shadow` 文件中的密码，而是会尝试使用密码文件中的此字段作为密码。由于任何内容加密后都不会与此密码匹配，因此该帐户无法使用。将该字段改回单独的 `x` 将再次启用访问。

完全从 `/etc/passwd` 文件中删除该条目也会禁用用户帐户，但如果需要恢复该帐户，则会更加困难。

> **注意**
>
> 禁用或删除用户帐户不会删除用户主目录中的任何数据。如果要删除 `/home/` 目录中的内容，必须专门使用 `rm` 命令。

如果你想阻止 natalie 在本地登录，但不阻止她从系统中收取邮件，可以将 natalie 的 shell 改为 `/bin/false`。你必须确保 `/bin/false` 列在 `/etc/shells` 中。

> **警告**
>
> 如果删除了一个用户帐户，而该用户的任何文件仍留在系统上，那么使用已删除用户 UID 添加的新用户将完全访问已删除用户的文件（这存在隐私方面的安全风险）。在重新使用该 UID 之前，请确保系统中已删除用户的所有痕迹都已移除。运行以下命令：
>
> ```bash
> find / -nouser -exec rm -Rf {} \;
> ```
>
> 将删除 `/etc/passwd` 中不属于任何人的所有文件和目录。（详细信息请阅读 `find` 的手册页。）

## 组

*组标识符*（GID）的目的是将资源或文件按逻辑分组到给定组的成员。例如，源代码文件可能需要在工程部门的用户之间共享。通过创建工程组并将适当的成员添加到该组中，文件就可以在工程部门成员之间共享，同时可防止其他人访问他们不应看到的文件。其他部门或组也是如此：文件可以在会计、销售或服务部门内共享，而不会有未经授权的用户访问数据的风险。

### 创建组

通过向 `/etc/group` 文件添加条目来创建组。该文件的默认列表如下：

```
root::0:
wheel::10:
bin::1:bin,daemon
daemon::2:bin,daemon
sys::3:bin,adm
adm::4:adm,daemon
tty::5:
disk::6:
lp::7:daemon,lp
mem::8:
kmem::9:
operator::11:
mail::12:mail
news::13:news
uucp::14:uucp
man::15:
majordom::16:
database::17:
games::20:
gopher::30:
dip::40:
ftp::50:
users::100:
nobody::65534:
```

`/etc/group` 文件中的每一行表示一个组。你会注意到，许多预定义组直接对应于特定服务。例如，`lp` 组用于打印机服务。表 11.3 列出了 `/etc/group` 文件格式的说明。

**表 11.3 — `/etc/group` 文件的字段说明**

| 字段 | 说明 |
|---|---|
| 1 | 第一个字段是组名。例如，工程组可能是 `eng`，会计组可能是 `acct`。 |
| 2 | 这是组的密码。通常不使用，但可以设置。 |
| 3 | 这是组标识符（GID）编号。作为该组默认成员的用户帐户，其 `/etc/passwd` 条目中包含此编号。 |
| 4 | 最后一个字段是与该组关联的用户帐户列表。 |

每个用户帐户必须至少属于一个组。OpenLinux 中的默认组是 `users`。关联的组标识符（GID）为 100。其他发行版可能有所不同。

> **注意：** 用户被纳入默认组是通过每个用户的 `/etc/passwd` 条目中存在的组标识符（GID）实现的。用户帐户名不必出现在 `/etc/group` 文件中即可被纳入默认组。

### 将用户帐户添加到组

用户可以属于的组数没有限制。但是，要加入除初始默认组之外的其他组，只能通过将用户帐户名添加到 `/etc/group` 文件中的用户帐户名列表来实现。只需将用户名添加到 `/etc/group` 文件组条目的最后一个字段，即可将用户帐户添加到特定组。添加用户帐户后，即授予对该组共享文件的访问权。`/etc/group` 文件中包含多个成员（用户帐户）的条目类似于以下内容：

```
eng::100:kelsey,brittany,ryan,natalie
```

上述示例最后一个字段中列出的所有用户帐户都是 `eng` 组的成员。

可以使用 `groupadd` 命令向 `/etc/group` 文件添加新组。其一般语法很简单：

```bash
groupadd -g GID groupname
```

`-g GID` 参数将组 ID 分配给新组。例如，以下命令创建一个名为 `eng` 的新组，并为其分配组 ID 201：

```bash
groupadd -g 201 eng
```

### 从组中移除用户帐户

从特定组中移除用户，只需从 `/etc/group` 文件的列表中移除用户名即可。这样做不会删除数据或更改权限，只会将特定用户帐户排除在访问特定组所包含的文件之外。

### 其他实用工具

要获取你被分配到的所有组的列表，请使用 `groups` 命令。要获取自己的列表，只需执行不带参数的 `groups`；要获取其他人的列表，请以用户名作为参数执行 `groups`。

