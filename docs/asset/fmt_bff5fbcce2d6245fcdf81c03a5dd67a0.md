
`deny-uid` 和 `deny-gid` 条目防止所有 ID 为 99 或以下或 65534 或以上的用户账户或组账户访问 FTP 服务。`allow-uid` 和 `allow-gid` 行通过允许 ftp 用户和组使用 FTP 服务来对拒绝规则设置例外。

- *guestuser* — 此行允许所有用户默认将其主目录作为其根目录。如果你的主目录是 `/home/jake` 且你向计算机建立了 FTP 连接，你将只能看到 `/home/jake` 或其子目录中的文件。（要更改此行为，请在该行前添加注释字符 `#`，或者添加一条 `realuser` 行，将 `user` 替换为想要允许更改其目录之外的用户名）。
- *email root@localhost* — 默认情况下，给 FTP 服务器管理员的电子邮件将定向到本地计算机上的 root 用户。
- *loginfails* — FTP 连接在连续五次登录失败后终止。（这可以记录下那些试图猜测你服务器密码的人。）
- *readme README* — 当用户登录（`login`）或更改任何可访问目录（`cwd*`）时，如果存在 README 文件，将通知用户其。默认情况下，这些文件都不存在。对于任何带有 README 单词的文件，服务器将显示一条“请阅读 README，无论如何”的消息。
- *message* — 这表示当用户登录 FTP 时，应该显示包含在 `/.welcome.msg` 文件中的消息。类似的行表示，当用户进入包含此类文件的目录时，将显示 `.message` 文件。默认情况下，这些文件都不存在。如果你想在 FTP 服务器上使用它们，必须手动创建它们。

> 注意：`/.welcome.msg` 文件相对于 FTP 用户使用的根目录。访客用户（如 anonymous）默认将 `/var/ftp` 作为其根目录。因此，`welcome.msg` 文件将位于 `/var/ftp` 目录下。

- *compress all* — 这为所有用户启用 FTP 站点的文件压缩功能。`compress` 命令是 UNIX 系统中的标准压缩命令（尽管在 Linux 等免费操作系统中更多使用 `gzip`）。执行压缩的 `compress` 命令定义在 `/etc/ftpconversions` 中。（由 `compress` 存储的文件带有 `.z` 后缀）。
- *tar yes all* — 这为 FTP 站点的所有用户启用 tar 压缩。`tar` 命令是用于创建多个文件存档的标准 UNIX 命令。执行压缩的 `tar` 命令定义在 `/etc/ftpconversions` 中。（由 `tar` 存储的文件具有 `.tar`、`.tar.gz` 或 `.tar.Z` 后缀）。

## 第 20 章：设置 FTP 服务器

- `chmod guest, anonymous` — 防止访客和匿名用户名称更改任何文件或目录的权限。
- `delete no anonymous` — 防止匿名用户删除文件或目录。
- `overwrite no anonymous` — 防止匿名用户覆盖现有的文件或目录。
- `rename no anonymous` — 防止匿名用户重命名文件或目录。
- `log transfers anonymous, guest, real inbound, outbound` — 记录匿名用户、guest 用户以及所有真实用户（即在 Linux 系统中拥有所有者账户的用户）的传输记录。上传（入站）和下载（出站）传输均会被记录。
- `shutdown/etc/shutmsg` — 检查 `/etc/shutmsg` 文件查看服务器是否即将关闭。如果是，你的 FTP 服务器将向当前 FTP 用户发送消息，警告他们在关机前的指定时间断开连接。（默认情况下，`/etc/shutmsg` 文件不存在）。请参阅本章稍后关于设置 FTP 关闭的章节，获取有关如何为计划的 FTP 设置关闭文件。
- `password-check rfc822 wann` — 检查匿名登录密码是否符合 rfc822 标准的地址。换句话说，FTP 服务器要求任何有效的电子邮件地址作为匿名登录的密码。如果地址不符合标准（即格式不是 `user@host.domain`），服务器将向用户发出“警告”，但仍允许其登录。
- FTP 根目录 — 对于以匿名用户身份登录的用户，`/var/ftp` 目录被分配为该用户的根目录。这意味着匿名用户无法 `cd` 进入 `/var/ftp` 目录以上（甚至不知道 `/var/ftp` 目录结构之外存在哪些文件）。

`/var/ftp` 目录中包含了使 FTP 正常工作所需的目录和文件，而无需访问文件系统中的其他文件。`/bin` 目录包含 FTP 可能需要的可执行命令（如 `compress`、`ls` 和 `gzip`）。`/etc` 目录包含 `passwd` 和 `group` 条目。`/lib` 目录存放 FTP 所需的对象库。最后，`/pub` 目录可用于放置希望向匿名用户开放的文件。

## 创建 FTP 用户

可以使用你服务器 FTP 服务的不同类型用户包括：匿名用户名、已添加到计算机的任何真实用户（在 `/etc/passwd` 中），以及你设置的任何特殊访客账户。后续章节将描述这些类型的用户以及如何设置它们。

## 匿名 FTP 用户

由于大多数从互联网访问你 FTP 站点的游客没有你计算机的个人登录账户，因此在公共 FTP 站点使用了匿名用户名。通常，`minimal` 意味着用户只能读取。这是一个示例：

```
anonymous@example.com:x:42:42::/ftp:/sbin/nologin
ftp:x:42:/var/ftp:/sbin/nologin
```

## 真实用户

拥有计算机有效登录账户的用户也可以通过 FTP 访问计算机。

# 访客用户

访客介于真实用户和匿名用户之间。你可以为访客用户分配任何名称。然而，访客用户被限制在文件系统的某个受限区域，通常是用户的家目录。

使用访客账户是允许特定用户向你文件系统的特定部分添加和删除文件的极佳方法，但不允许他们进行其他许多操作。例如，如果你想给用户提供一个设置自己的 Web 页面的地方，这种方法非常有用。

通常情况下，FTP 用户将在 Linux 的 `/etc/passwd` 文件中设置账户，然后该用户将在 `/etc/ftpasswd` 文件中被定义为 `guestuser` 或 `guestgroup`。以下是设置 FTP 访客账户的示例（你必须是 root 用户才能执行此操作）：

- 1. 像往一样添加用户账户。例如，要添加一个名为 mike、家目录为 /home/mike 的用户，输入以下内容（作为 root 用户）：

```bash
# username mike
```

- 2. 使用 `passwd` 命令为 mike 添加密码（根据提示输入两次）

```bash
# passwd mike
Changing password for user mike
New password: ********
Retype new password: ********
```

- 3. 编辑 `/etc/passwd` 中的账户信息，将用户的根目录更改为受限目录（例如，用户的家目录）。这里是名为 mike 的用户新条目的显示方式：mike:x:501:guest acct:/home/mike/:/pub:/etc/ftponly

- 4. `/home/mike` 之后的 `.` 使 FTP 服务器上的 `/home/mike` 目录成为 mike 的根目录。当 mike 登录时，他的当前目录是 /home/mike/pub。`/etc/ftponly` 的值防止了如果 mike 登录普通的 Linux 提示符时启动 shell（如 `/bin/bash`）。

- 5. 将访客文件复制到 `/etc` 并按如下方式执行：

- 6. 将行 `/etc/ftponly` 添加到 `/etc/shells` 文件中。

- 7. 创建访客家目录所需的目录，以确保 FTP 正常运行所需的所有内容。为了做到这一点，我只是（作为 root 用户）从 `/var/ftp` 目录结构复制了所有内容到我的访客用户家目录（/home/mike）。之后，我将我的访客账户在 /home/mike/pub 的组分配更改为 mike：

```bash
# cp -r /var/ftp/* /home/mike
# chgrp mike /home/mike/pub
```

# 第20章：设置 FTP 服务器

- 8. 向 `/etc/ftpaccess` 中添加必要的定义。如果你更改了默认值（`guestuser *`），这会将所有真实用户变成访客用户，你需要将该用户定义为访客登录。例如，将 mike 定义为访客登录，在 `/etc/ftpaccess` 中添加以下内容：

```bash
guestuser mike
```

> 交叉引用：只需定义了 `guestuser mike`，用户 mike 就拥有 /home/mike 作为他的根目录，并可以获取文件（但不能上传到服务器）。此外，他只能浏览 /home/mike-like 下的目录。如需添加或更改权限，请参阅本章稍后关于控制 FTP 访问的节。

在此时，访客用户可以使用 `ftp` 命令连接到服务器，并仅访问该用户受限目录下的文件和目录。

# 设置 FTP 目录、消息文件和欢迎语

作为 FTP 站点管理员，你负责设置站点上使用的目录结构。你还有机会通过在站点上提供各种消息文件和 README 文件，以及更改你 FTP 服务器上的欢迎语，让用户在站点上的导航更加容易。以下章节描述了这些功能。

# 创建 FTP 目录结构

由于你向使用你 FTP 服务的人提供了文件系统的受限视图，你必须在他们可以访问的根文件系统（通常是 /var/ftp）中提供他们所需的所有内容。如何为 FTP 设置最小目录结构在设置访客用户的节中进行了描述。

在 Red Hat Linux 中安装 FTP 服务（特别是 `anftpd` 软件包）时，`/var/ftp` 目录中提供了一个可行的目录结构。之后，你想与用户共享的大部分内容可以在你创建的 `/pub` 目录结构中安排。对于包含某些类型用户限制信息的目录，你可能想要创建一个不同的根目录（例如 `/local`）。

可以使用 `/etc/ftpaccess` 文件中的各种参数在目录结构中包含或排除特定目录。你可以选择哪些目录允许上传下载。你还可以设置用户是否可以重命名、删除、覆盖或更改文件的权限。有关设置用户目录和文件的更多信息，请参阅控制 FTP 访问的节。

# 添加帮助信息

你的 Red Hat Linux 计算机上的 FTP 服务被设置为自动显示消息，并在用户导航你的站点不同时间提醒用户 README 文件的存在。然而，在安装 FTP 时，这些文件并不存在。因此，为了帮助站点的导航，你需要创建这些文件。

### 创建 README 文件

```
readme      README*     login
readme      README*     cwd=
```

README 末尾的星号表示任何带有 README 单词的文件都会匹配（如 README.info、README-help 或 README.txt）。README 文件通常是纯文本，因此任何人都可以阅读。你可以使用任何文本编辑器创建一个。将 README 文件添加到 `/var/ftp` 目录中（以描述内容）。

### 创建消息文件

### 更改欢迎语

# 第20章：设置 FTP 服务器

### 修改初始欢迎语

如果你不更改任何内容，用户登录时的默认欢迎语如下：

```
$ ftp maple
Connected to maple (10.0.0.11).
220 maple FTP server (Version wu-6-7) ready.
Name (mike):
```

这就是完整的欢迎语。要简化用户看到的欢迎语，你可以在 /etc/ftpaccess 文件中将 greeting 选项设置为 brief 或 terse：

```bash
greeting terse
```

terse 选项会在登录提示符之前显示较短的输出。示例如下：

```
$ ftp maple
Connected to maple (10.0.0.11).
220 FTP server ready.
Name (mike):
```

### 修改 FTP 服务器主机名

通常，当有人连接到你的 FTP 服务时，会显示系统主机名。如果你想为连接到你 FTP 服务器的连接分配特殊的主机名，可以在 /etc/ftpaccess 文件中更改该名称。以下是你输入的行的示例：

```bash
hostname ftppine
```

下次 FTP 用户连接时，将使用 ftppine 作为主机名。

### 登录前添加消息

如果你想在用户连接到你的 FTP 服务之后、登录提示符之前显示消息，可以通过 /etc/ftpaccess 文件中的 banner 选项来实现。首先，你需要创建一个包含你想打印的消息的文本文件。接下来，添加一行 banner 行指向该文件（相对于你的系统根，而不是 FTP 相对根）。例如：

```bash
banner /etc/ftpbanner.msg
```

通过此示例，下次用户连接到 FTP 服务时，/etc/ftpbanner.msg 文件的内容将在连接消息之后、登录提示符出现显示。

# 782 第四部分：Red Hat Linux 网络和服务器设置

确切地哪些目录是可读可写的。你可以限制同时访问你的 FTP 服务器的用户数。你还可以为个人或组设置资源的权限或限制。接下来的章节描述了你的一些选项。

## 创建用户类

通过设置用户类，你创建了一种方法，为不同的用户组分配不同资源的访问权限。任何不属于某个类的用户都将无法访问你的 FTP 服务器。这就是为什么默认类通过以下代码行包含所有用户：

```
class      all             real,guest, anonymous
```

你首先需要决定的是你想对哪些用户组进行单独处理。一种有效的技术是将本地用户定义为一个类，将所有其他用户定义为另一类。`class` 关键字允许你根据网络地址和该地址内的用户类型（即真实、访客或匿名）来分配类。你可能想为你的 Internet 域内的所有用户分配一组权限，并为其他人分配另一组权限。操作方法如下：

```
class  home    real,guest, anonymous  10.0.0.0/8
class  world   real,guest, anonymous  *
```
