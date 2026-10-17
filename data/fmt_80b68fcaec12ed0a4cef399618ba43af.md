
> 超级用户账户默认称为 `root`。但是，你可以将其名称更改为任何你想要的内容。唯一的要求是 UID 必须为零（`0`）。

保护系统的另一种方法是创建特殊的登录账户，用于执行不需要广泛权限的特定系统任务。通过创建仅被授予有限管理权限的登录账户，你可以保护系统免受无意失误和恶意破坏的影响。

### `su` 命令

`su` 命令使你能够使用与当前登录身份不同的凭证来执行任务。它用于两种不同的场景：

- 当你以普通用户身份登录，需要以 `root` 身份执行某些操作时
- 当你以 `root` 身份登录，希望模拟其他用户时

你不应该在以 `root` 身份登录时执行日常任务，因为这会使你的系统处于风险之中。如果需要执行管理任务，你可以先注销，然后以 `root` 身份登录。在以 `root` 身份登录期间，你可以完成任务，然后注销并重新以普通用户身份登录。

这样做比较耗时，而使用 `su` 命令则提供了一种捷径。如果在命令提示符下输入 `su`，系统会提示输入 `root` 的密码。如果你输入正确的密码，你将切换为 `root` 用户，且工作目录将保持执行该命令前的状态。

如果你想登录为其他用户，请执行以下命令：

```
su username
```

这将提示输入该用户的密码。如果你提供正确的密码，你将登录为该用户。如果你以 `root` 身份登录时运行此命令，则不会提示输入密码。

默认情况下，`HOME` 和 `SHELL` 变量会被重置为该用户的值。如果你也希望读取配置文件中该用户的环境设置，可以使用 `-` 选项。这意味着，如果你输入：

```
su Mary
```

并提供 `Mary` 的正确密码，你的工作目录将保持不变；然而，你将登录为 `Mary`。如果你还希望将 `Mary` 的主目录作为你的工作目录，请输入：

```
su - Mary
```

此时你已登录为 `Mary`，且她的主目录是你的工作目录。

如果使用 `su` 命令时未提供用户名，则默认假设目标用户是 `root`。任何用户都可以使用 `su` 命令登录为 `root` 或任何其他用户，前提是她知道正确的密码。但是，`root` 可以登录为任何其他用户，而无需知道其密码。

### 创建用户账户

即使你是系统中唯一的用户，安装 `Linux` 后你应该处理的第一件事就是为自己创建一个用户账户。你还需要为所有可能需要访问你系统的其他人创建用户账户。

通过让每个用户使用自己的账户，可以提高系统的安全性。你可以定义任何用户对任何资源的访问权限，包括按用户级别设置文件或目录的权限。（有关权限管理的更多信息，请参阅第 9 章“权限”。）此外，这将使你能够跟踪用户的活动。

### `/etc/passwd` 文件

所有关于用户账户的信息都按照特定格式包含在 `/etc/passwd` 文件中。为了通过考试，你需要了解每个字段的用途以及其他程序如何使用这些信息。如表 7.1 所示，该文件包含用户的登录名、用户 ID、密码、全名以及其他信息。

表 7.1 `/etc/passwd` 文件中包含的字段

第 9 章讨论了如何设置 `/etc/passwd` 文件的权限。该文件由 `root` 所有，`root` 具有 `rw-` 权限。其他所有人（包括组）只能读取此文件。

一个示例 `/etc/passwd` 文件可能如下所示：

```
root:Mr cx.kSGtY Q0:0:0:root:/root:/bin/bash
hadden:h4cSU0W27LGjs:503:500:Theressa Hadden,Home Office,555-5555,222-2222:/home/hadden:/bin/bash
bin::1::1::bin:
daemon:*::2::2:daemon:/sbin:
adm:*::3::4:adm:/var/adm:
lp: : 7:1:lp:/var/spool/lpd:
Sync: : 0:0:sync:/sbin:/bin/sync
shutdown: : 0:0:shutdown:/sbin:/sbin/shutdown
halt: : 7:0:halt:/sbin:/sbin/halt
mail: *::8:12:mail:/var/spool/mail:
news: *:: 9:13:news:/var/spool/news:
uucp: *::10:14:uucp:/var/spool/uucp:
operator: *::11:0:operator:/root:
games: *::12:100:games:/usr/games:
gopher: *::13:30:gopher:/usr/lib/gopher-data:
ftp: : 14:50:FTP User:/home/ftp:
nobody:*::99:99:Nobody:/
```

即使某个字段为空，仍然需要用冒号（`:`）将其定义出来。例如，用户账户 `mail` 的记录以冒号结尾，因为该用户未定义登录命令。几乎所有 `UNIX` 系统都使用相同的格式。

> **关键概念**

> `/etc/passwd` 文件中的每一行必须包含七个字段。尽管其中一些字段可能为空，但仍需用冒号将它们定义出来。

### 用户名字段

第一个字段是用户名。它必须在系统中唯一。通常由八个或更少的字符组成，可以包含字母、数字、下划线、句号以及一些特殊字符。但是，使用非字母数字字符可能会导致某些应用程序出现问题。此外，用户名区分大小写，因此用户名 `thadden` 和 `Thadden` 代表两个不同的用户。

由于用户名用于许多用途（包括电子邮件）且必须在系统中唯一，你需要考虑如何分配用户名。如果你的系统只有少数几个用户，用户名的一致性并不是特别重要。然而，当系统规模较大时，如果没有合理的方法来分配用户名，就很难识别某个用户是谁。

命名用户的一种方法是使用名字首字母姓氏的一部分或全部的组合。例如，名为 `Theressa Hadden` 的用户将被赋予用户名 `thadden`。另一种组合可能是名字和姓氏首字母，例如 `theresh`。无论你决定使用哪种方法，都要保持一致性。

### 密码字段

`/etc/passwd` 文件中每条记录的下一个字段是密码。这些密码由操作系统以加密形式存储。如果此字段以某种方式损坏，该用户将无法登录到系统，直到管理员为此账户分配新密码。

你可以通过在此字段中放置一个星号（`*`）来阻止用户登录系统。虽然用户将无法登录，但他们仍可能通过远程方式访问并运行命令，因此不要将此方法作为唯一的防御手段。

如果你需要暂时限制用户的访问权限，请在其账户的密码字段开头放置一个星号。请小心不要对该字段进行其他修改。虽然这并非 100% 可靠，但通常已经足够。你可以将此方法用于度假或长期外出的用户。

如果此字段留空，则登录时只需输入用户名。用户不会被要求输入密码。虽然这在某些情况下很有帮助（例如，如果你想要一个访客账户），但这也是一个严重的安全风险。如果你有一个密码为空的账户，请务必尽可能严格限制该账户的访问权限。

### 用户 ID 字段

每条记录中的第三个字段是用户 ID（`UID`）。系统通过 `UID` 而非名称来跟踪用户。例如，当用户启动一个进程时，其 `UID` 与该进程相关联，并使用 `ps` 命令时会显示出来。

通常，`UID` 的范围用于定义账户类型。小于 `100` 的 `UID` 通常保留给系统账户，`root` 始终具有 `UID 0`，而普通用户被分配大于 `100` 的 `UID`。用户 ID 的起始编号因不同的发行版而异，但原理相同。起始用户 ID 在 `/etc/login.defs` 文件中定义，该文件的一个示例可能如下所示：

```
##### *REQUIRED*
##### Directory where mailboxes reside, _or_ name of file, relative to the
##### home directory.  If you _do_ define both, MAIL_DIR takes precedence.
##### QMAIL_DIR is for Qmail

#MAIL_DIR       Maildir
MAIL_DIR        /var/spool/mail
#MAIL_FILE        .mail

##### Password aging controls:
#
#	PSS_MAX_DAYS		Maximum number of days a password may be used.
#	PSS_MIN_DAYS		Minimum number of days allowed between password changes.
#	PSS_MIN_LEN		Minimum acceptable password length.
#	PSS_WARN_AGE		Number of days warning given before a password expires.
#
PASS_MAX_DAYS       99999
PASS_MIN_DAYS       0
PASS_MIN_LEN        5
PASS_WARN_AGE       7
```
