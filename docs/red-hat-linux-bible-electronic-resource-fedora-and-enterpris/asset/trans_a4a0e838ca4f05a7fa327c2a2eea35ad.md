
-   **FTP 根目录** — 对于以匿名用户登录的用户，`/var/ftp` 目录被分配为用户的根目录。换句话说，匿名用户无法更改 `/var/ftp` 目录之上的目录（甚至不知道 `/var/ftp` 目录结构之外存在哪些文件）。

在 `/var/ftp` 目录内是使 FTP 正常工作所需的那些目录和文件，而无需您访问文件系统中的其他文件。`/bin` 目录包含 FTP 可能需要的可执行命令（例如 `compress`、`ls` 和 `gzip`）。`/etc` 目录包含 passwd 和 group 条目。`/lib` 目录存放 FTP 所需的共享对象库。最后，`/pub` 目录可用于放置您希望对匿名用户普遍可用的文件。

## 创建 FTP 用户

可以使用您服务器的 FTP 服务的不同类型的用户包括匿名用户名、已添加到计算机的任何真实用户（在 `/etc/passwd` 中），以及您设置的任何特殊访客帐户。以下各节描述了这些类型的用户以及如何设置它们。

### 匿名 FTP 用户

由于大多数从互联网访问 FTP 站点的访客没有计算机的个人登录帐户，因此在公共 FTP 站点上使用匿名用户名。有了匿名用户名，任何能够从网络访问 FTP 站点的人都可以登录到服务器并具有最小的使用权限。通常，“最小”意味着匿名用户只能从 FTP 服务器复制文件（而不能向其写入文件），并且只有选定的目录甚至可见。

这是一个匿名用户登录会话的示例：

```
$ ftp maple
Connected to maple
220 maple FTP server (Version wu-2.6.2-8) ready.
Name (maple:mike): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password: ********
230 Guest login ok, access restrictions apply.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
ftp> bye
221-You have transferred 0 bytes in 0 files.
221-Total traffic for this session was 313 bytes in 0 transfers.
221-Thank you for using the FTP service on maple.
221 Goodbye.
```

当我登录到 FTP 服务器时，我可以访问服务器允许匿名用户访问的所有文件和目录。这可能仅包括服务器系统的有限区域（默认情况下，在 Red Hat Linux 系统上为 `/var/ftp` 目录）。作为匿名用户，我在服务器上可以更改、删除或创建的内容可能也存在限制。

匿名 FTP 的一大优势是它可以很容易地自动化。用户无需使用 `ftp` 命令，只需在 Web 浏览器中输入服务器的 FTP 地址即可。用户在访问 FTP 站点时甚至不需要知道自己是以匿名用户身份登录。请求的文件和目录列表就会简单地显示出来。

> **提示：** 假设您已安装 `anonftp` 软件包并启动了 FTP 服务，则默认情况下匿名用户会被授予访问您 FTP 服务器的权限。这假设您的防火墙未阻止对该服务的访问，并且文件 `/etc/xinetd.d/wu-ftpd` 中 `disable = yes` 已更改为 `disable = no`。要防止匿名用户访问您的 FTP 服务器，请在您的 `/etc/ftpaccess` 文件中添加以下行：
> 
> `defaultserver private`

## 真实用户

拥有对计算机有效登录帐户的用户也可以通过 FTP 访问计算机。这些用户可以使用管理员定义的任何用户名。要使用 FTP，他们只需在 FTP 提示符下输入其用户名和密码即可。此时，他们将登录到 FTP 服务器。

> **交叉引用：** 有关设置常规真实用户帐户的信息，请参阅第 11 章。

然而，与其将 `/var/ftp` 作为其根目录，真实用户在登录时将其常规主目录（例如 `/home/user`，其中 `user` 为用户名）作为其根目录和当前目录。与匿名用户一样，真实用户在文件系统方面也有特殊限制。默认情况下，真实用户无法访问其主目录和相关子目录之外的任何文件。

> **注意：** 如果您在版本 7.3 之前的 Red Hat Linux 系统中使用了 WU-FTPD，您可能记得真实用户的访问权限并未限制在其主目录中。如果您的用户投诉，您可以考虑重新配置 `ftpaccess` 文件。

无需在 `/etc/ftpaccess` 文件中进行特殊配置即可允许具有真实帐户的用户通过 FTP 连接到服务器。但是，如果您希望为一个或多个真实用户提供与直接登录时相同的对文件系统的访问权限，则可以通过为用户或组分别设置 `realuser` 或 `realgroup` 值来重新定义该用户或组为真实用户。（例如，添加一行 `realuser joe` 以赋予名为 `joe` 的用户访问其主目录之外文件的权限。）

要防止任何真实用户使用 FTP 服务，您只需将该人员的用户名添加到 `/etc/ftpusers` 列表中。默认情况下，这些用户被排除在外，因为它们位于此列表中：`root`、`bin`、`daemon`、`adm`、`lp`、`sync`、`shutdown`、`halt`、`mail`、`news`、`uucp`、`operator`、`games`。和 nobody。 其中大多数是可能被利用的管理员帐户。在 `/etc/ftpaccess` 文件中，除 ftp 用户和组之外的所有管理员帐户默认情况下均被拒绝访问 FTP 服务。

## 访客用户

访客用户在某种程度上介于真实用户和匿名用户之间。您可以将任何名称分配为访客用户。但是，访客用户仅限于文件系统的受限区域，通常是用户的主目录。

使用访客用户帐户是让特定用户有权向文件系统的特定部分添加文件并从中删除文件，但不允许他们做太多其他事情的绝佳方法。例如，如果您想让用户拥有设置自己的网页的位置，这很有用。

一般来说，FTP 访客用户将在 Linux /etc/passwd 文件中设置帐户，然后该用户将在 `/etc/ftpaccess` 文件中定义为 guestuser 或 guestgroup。以下是设置 FTP 访客用户帐户的示例（您必须是 root 用户才能执行此过程）：

-   1. 按通常方式添加用户帐户。例如，要添加一个名为 mike 且主目录为 /home/mike 的用户，请按以下方式输入（以 root 用户身份）：

```
# useradd -m mike
```

-   2. 使用 `passwd` 命令为 mike 添加密码（按提示输入两次）：

```
# passwd mike
Changing password for user mike.
New password: ******
Retype new password: ******
```

-   3. 编辑 /etc/passwd 中用户的帐户信息，以便将用户的根目录更改为受限目录（例如用户的主目录 /home）。以下是该新条目对于名为 mike 的用户的外观示例：

```
mike:x:501:501:guest acct:/home/mike:/. /pub:/etc/ftponly
```

-   4. /home/mike 后的点 (.) 使 /home/mike 目录在 FTP 服务器上成为 mike 的根目录。当 mike 登录时，他的当前目录是 /home/mike/pub。/etc/ftponly 值可防止在 mike 从常规 Linux 提示符登录时启动 shell（例如 /bin/bash）。

-   5. 按如下方式将示例 ftponly 文件复制到 /etc 并使其可执行：

```
# cp /usr/share/doc/wu-ftpd*/examples/ftponly /etc/
# chmod 755 /etc/ftponly
```

-   6. 将行 /etc/ftponly 添加到 /etc/shells 文件。

-   7. 创建访客用户主目录所需的所有 FTP 正常工作所需的目录。为此，我只是将 `/var/ftp` 目录结构中的所有内容（以 root 用户身份）复制到我的访客用户主目录（`/home/mike`）。之后，我将 `/home/mike/pub` 的组分配更改为 mike：

```
# cp -r /var/ftp/* /home/mike
# chgrp mike /home/mike/pub
```

-   8. 向 `/etc/ftpaccess` 添加必要的定义。如果您更改了默认设置（guestuser *）使所有真实用户都成为访客用户，则需要将用户定义为访客登录。例如，要将 mike 定义为访客登录，请将以下内容添加到 `/etc/ftpaccess`：

```
guestuser mike
```

> **交叉引用：** 仅定义 `guestuser mike` 时，用户 mike 的根目录为 `/home/mike`，他可以获取文件（但不能将其放在服务器上）。此外，他只能浏览 `/home/mike` 下的目录结构。要添加或更改权限，请参阅本章后面有关控制 FTP 访问的章节。

此时，访客用户可以使用 `ftp` 命令连接到服务器，并仅访问用户受限目录下的文件和目录。

## 设置 FTP 目录、消息文件和问候语

作为 FTP 站点管理员，您负责设置站点上使用的目录结构。您还有机会通过在站点上提供各种消息文件和 README 文件以及更改 FTP 服务器上的问候语来使用户更轻松地浏览您的站点。以下各节描述了这些功能。

### 创建 FTP 目录结构

由于您向使用 FTP 服务的人员提供文件系统的有限视图，因此您必须在他们可以访问的根文件系统内（通常为 `/var/ftp`）提供他们所需的一切。有关为 FTP 设置最小目录结构的说明，请参阅有关设置访客用户的部分。

在 Red Hat Linux 中安装 FTP 服务（具体来说是 `anonftp` 包）时，会在 `/var/ftp` 目录中提供可行的目录结构。之后，您希望与公众共享的大多数内容都可以在您创建的 `/pub` 目录结构中安排。对于包含仅限于某些用户类别的信息的目录，您可能希望创建不同的根目录（例如 `/local`）。

可以使用 `/etc/ftpaccess` 文件中的各种参数在目录结构中包含或排除特定目录。您可以选择哪些目录允许上传和下载。您还可以设置用户是否可以重命名、删除、覆盖或更改
