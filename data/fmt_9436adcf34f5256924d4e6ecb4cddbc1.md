
作为 FTP 服务器的管理员，您的职责以确保您以某种方式共享文件，这种方式让人们访问您希望他们拥有的信息，同时不危及系统的安全。这意味着实施强大的安全策略并持续监控系统以防止滥用。

##### FTP 用户类型

几种不同类型的用户可以登录并使用 FTP 服务器。`实际用户`代表那些拥有包含您的 FTP 服务器的 CentOS 系统登录帐户的用户类别（即，您知道他们并已授予他们除 FTP 之外的其他用途权限）。使用`vsFTpd`，如果您选择，您可以为每个实际用户单独配置设置。

`访客用户`类似于实际用户帐户，除了访客用户对计算机文件系统的访问受到更多限制。用户名`anonymous`是提供公共（访客类型）访问的最常见用户名。

`vsFTpd`服务器还支持`虚拟用户`的概念。为`vsFTpd`创建虚拟用户的推荐方法是配置`PAM`（可插拔认证模块）指向每用户配置文件。`vsFTpd`软件包包含用于配置虚拟用户的示例文件。请参考`/usr/share/doc/vsftpd*/EXAMPLE`目录，该目录包含虚拟用户示例配置文件。

> **交叉引用** 有关创建对服务器具有受限访问权限的用户帐户的信息，请参阅第 10 章。

##### 使用非常安全的 FTP 服务器

非常安全的 FTP 服务器 (`vsFTpd`) 是 CentOS 发行版中包含的唯一通用 FTP 服务器软件。`vsFTpd`正在成为需要支持数千个并发下载的网站的首选 FTP 服务器。它还被设计用于保护您的系统免受大多数常见攻击。

###### 第四部分 网络

> **注意**
>
> CentOS 系统随附的分发软件包中包含了简单文件传输协议服务器（`tftp`软件包），它也可以用来提供 FTP 服务。`tftpd`守护进程主要用于支持无盘设备，这些设备需要从 TFTP 服务器获取启动和运行所需的文件。TFTP 并非旨在提供通用的、面向公众的 FTP 服务。由于公开使用 TFTP 被认为存在安全风险，它通常仅用于无法访问公共网络的私有局域网。RPMforge 软件库中现在可用的其他 FTP 服务器软件包包括 `ProFTPD`（http://proftpd.org）和 `Pure-FTPd`（http://pureftpd.org）。

红帽公司（Red Hat, Inc.）在其自身的 FTP 服务器（ftp.redhat.com）上使用 `vsftpd`。开源软件世界中的其他组织也已切换到使用 `vsftpd`，包括 Debian Linux（ftp.debian.org）、OpenBSD（ftp.openbsd.org）以及 GNU 计划（ftp.gnu.org）。

除了安全性和可扩展性外，`vsftpd` 的设计还追求简洁。因此，与仍被广泛使用的较旧 FTP 服务器软件包 `WU-FTPd` 相比，`vsftpd` 的可用配置选项更少，因此期望你依靠标准的 Linux 文件和目录权限来为你的服务器提供精细化的访问控制。开始使用 `vsftpd` 或用它来替代 `WU-FTPd` 是相当直观的。

##### 快速启动 VsFTPd

通过启用 `vsftpd` 服务，你几乎可以立即得到一个使用默认值运行的 FTP 服务（这些默认值设置在 `/etc/vsftpd/vsftpd.conf` 文件中）。以下是让 `vsftpd` 服务器启动并运行的快速步骤。如果你在安装 CentOS 时没有安装 `vsftpd`，请现在通过输入以下命令进行安装：

```
###### yum install vsftpd
```

以下是启动并试用 `vsftpd` 服务的方法。

1. 若要使用 `vsftpd` 服务器，必须确保已安装 `vsftpd` 软件包。

   ```
   # rpm -q vsftpd
   ```

2. 通过输入以下命令（以 `root` 用户身份）启用 `vsftpd` 服务器：

   ```
   # chkconfig vsftpd on
   ```

3. 按如下所示启动 `vsftpd` 服务器：

   ```
   # service vsftpd start
   ```

4. 尝试以 `anonymous`（匿名）身份登录到 FTP 服务器（使用任何电子邮件地址作为密码）：

   ```
   $ ftp localhost
   Connected to yourhost (127.0.0.1)
   220 (vsftpd 2.0.7)
   Name (localhost:timothy): anonymous
   331 Please specify the password.
   Password: *****
   230 Login successful.
   Remote system type is UNIX.
   Using binary mode to transfer files.
   ftp>
   ```

如果你看到了与上述类似的消息，说明你的 `vsftpd` 服务器现已启动并运行。接下来，请尝试从网络中的另一台计算机访问该服务器，以确保其可访问。

> **注意** 如果你的 FTP 服务器无法被外部世界访问，你可能需要确保网络配置正确，并且防火墙允许访问端口 21 以及可能的端口 20。快速的方法是运行 `system-config-securitylevel` 并将 FTP 添加为受信任的服务。此外，如果启用了 `SELinux`，它可能会阻止你正常预期可以工作的 FTP 服务器访问。要将 `SELinux` 设置为宽容模式，请以 `root` 身份输入 `setenforce 0`。或者输入 `man ftpd_selinux` 来了解如何在使用 `vsftpd` 时配置 `SELinux`。

下一部分将解释 `/etc/vsftpd/vsftpd.conf` 配置文件。

###### 配置 VsFTpd

`vsftpd` 的大部分配置是在 `/etc/vsftpd/vsftpd.conf` 文件中完成的。虽然 `vsftpd.conf` 中未明确设置许多值，但你可以通过在此文件中设置 `option=value` 语句来覆盖默认值。你可以设置诸如哪些用户有权访问你的 `vsftpd` 服务器、如何进行日志记录以及如何设置超时等参数。

阅读以下各节以了解 `vsftpd` 的默认配置方式以及如何进一步配置你的 `vsftpd` 服务器。

###### 用户账户

默认情况下，能够访问你的 `vsftpd` 服务器的用户是匿名用户以及系统中拥有真实用户账户的所有用户。访客用户只是被限制在其自身主目录中的真实用户账户。以下行用于设置这些用户访问功能：

```
anonymous_enable=YES
local_enable=YES
```

`anonymous_enable` 行允许用户使用 `anonymous` 或 `ftp` 用户名匿名登录。如果你想禁用匿名用户访问，不要仅仅注释掉 `anonymous_enable`。匿名访问默认是开启的，因此你必须设置 `anonymous_enable=NO` 来禁用它。

在 `/etc/passwd` 中具有本地账户和有效密码的任何用户都可以将 `local_enable` 设置为 YES 时登录到 FTP 服务器。该规则的一个例外是，默认情况下，列在 `/etc/vsftpd/user_list` 文件中的所有用户账户都被拒绝访问。

> **注意** 在你开始使用个人用户名和密码登录 FTP 服务之前，请记住 FTP 服务使用明文密码。由于这一事实，网络嗅探器有可能看到这些信息。如果你想使用 FTP 接口通过个人账户访问 FTP 服务器上的文件，请考虑使用 `Cyphssh`（`www.openssh.org/`）的 `sftp` 命令，而不是普通的 FTP 客户端。如果 FTP 服务器包含 SSH 服务器，你可以使用 `sftp` 通过加密密码连接到该服务器。

检查用户列表文件，查看哪些用户被拒绝访问 `vsftpd` 服务器。请注意，`root` 和其他管理登录已被排除。你可以将其他用户添加到列表中，或通过设置 `userlist_file` 参数到你想要的文件来更改列表位置。要将用户添加到用户列表或通过 `userlist_file` 参数创建新列表，你还必须将 `userlist_enable` 设置为 YES（默认即为 YES）。例如：

```
userlist_file=/etc/vsftpd/user_list_local
userlist_enable=YES
```

如果需要，你可以更改 `/etc/vsftpd/user_list` 文件的含义，使只有列出的用户才允许使用 `vsftpd` 服务。设置 `userlist_deny=no` 并更改 `/etc/vsftpd/user_list` 以仅包含你希望授予服务器访问权限的用户名。所有其他用户，包括 `anonymous` 和 `ftp`，都将被拒绝访问。

###### 设置 FTP 访问权限

`vsftpd` 服务器软件提供了一种简单且看似安全的访问权限方法。与使用 FTP 服务设置来有选择地阻止特定目录的下载和上传（如 `WU-FTPD` 等 FTP 服务器所做的那样）不同，你可以使用标准的 Linux 文件和目录权限来限制访问。不过，在 `/etc/vsftpd/vsftpd.conf` 文件中有一些通用设置，允许用户从你的 `vsftpd` 服务器获取文件以及向你的 `vsftpd` 服务器放置文件。

###### 下载文件

默认情况下，拥有有效登录凭证的任何用户（匿名用户或真实用户，除某些管理登录外）都可以从 `vsftpd` 服务器下载文件。下载特定文件或从特定目录下载文件的能力受以下基本 Linux 特性控制：

- **文件和目录权限** — 标准文件和目录权限作为一种限制对特定文件访问的手段，即使在可访问的文件系统中也适用。如果 `root` 用户将一个权限为 600（仅限 `root` 读写）的文件放在 `/var/ftp` 目录中，匿名用户将无法下载该文件。

- **根目录** — 匿名用户的根目录（chroot）是 `/var/ftp`。普通用户的根目录是计算机的整个根目录（`/`），尽管他们连接到 FTP 后的当前目录是 `/home/user`，其中 `user` 是用户名。因此，匿名用户仅限于从 `/var/ftp` 目录结构下载，而普通用户潜在地可以访问整个文件系统。另一种可能性是通过将部分或所有用户限制在其主目录中来创建访客账户。

###### 设置 FTP 服务器

你可以使用 `chroot_local_user` 选项更改普通用户的根目录，从而限制他们只能访问其主目录。若要在使用 `vsFTPd` 时限制所有普通用户只能访问其主目录，请向 `vsftpd.conf` 文件中添加以下行：

```
chroot_local_user=YES
```

若要启用访客用户概念，你可以选择仅将特定用户限制在其主目录中。方法是设置 `chroot_list_enable` 为 YES，然后将访客用户列表添加到由 `chroot_list` 文件选项指定的文件中。以下示例允许你向 `/etc/vsftpd/chroot_list` 文件添加此类列表（每行一个用户名）：

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd/chroot_list
```

![](img/2f265415ceec72538dd3c78ffca75c10_790_0.png)

若要将用户限制为仅使用 FTP 访问，请在 `/etc/passwd` 文件中将该用户的 shell 设置为 `/sbin/nologin`。通过运行 `system_config users` 命令或 `usermod` 命令并更改用户属性来实现，具体方法请参阅第 10 章。

你可以向 `vsftpd.conf` 文件添加设置以影响文件下载方式。若要启用 ASCII 下载，可以按如下方式启用该功能：

```
ascii_download_enable=YES
```

如果不进行此更改，所有下载均以二进制模式进行。尽管 `vsFTPd` 似乎允许用户切换到 `ascii` 模式，但如果此设置为 NO，`ascii` 模式将不起作用。允许 ASCII 文件传输被视为安全风险（易受使用 `size` 命令检查服务器上大型文件大小的 FTP 客户端发起的拒绝服务攻击），应避免使用。在禁用 ASCII 下载的情况下，客户端负责在需要时处理 ASCII 字符乱码问题。

###### 从本地用户上传（写入）文件

`vsftpd.conf` 文件中设置的两个值允许在 `vsFTPd` 会话期间上传文件。以下默认设置允许拥有常规本地用户账户的任何用户上传文件：

```
write_enable=YES
local_umask=022
```

如果你打算允许任何用户向 FTP 服务器写入，`write_enable` 值必须设置为 YES。`umask=022` 值设置了本地用户在服务器上创建文件时使用的默认文件权限。022 值会导致创建的文件具有 644 权限，允许用户具有读和写权限，而其他用户仅具有读权限。

与下载类似，默认情况下禁止以 `ascii` 模式上传。尽管 `ascii` 下载会对服务器资源造成潜在的安全漏洞，但 `ascii` 上传似乎不那么危险，并且对于上传文本文件很有用。若要允许 `ascii` 上传，请添加以下行：

```
ascii_upload_enable=YES
```

###### 从匿名用户上传（写入）文件

对于匿名 FTP 用户，上传文件的功能默认是关闭的。如果你希望开启它，请向 `vsftpd.conf` 文件中添加以下行：

```
anon_upload_enable=YES
```

若要使用匿名上传，必须激活全局写入启用。你还必须确保 `/var/ftp` 目录中包含一个或多个对匿名用户开放写权限的目录。例如，你可能希望创建一个 `incoming` 目录并开放其权限（`chmod 777 /var/ftp/incoming`）。

匿名用户上传的文件默认以 600 权限创建（`ftp` 用户具有读/写权限，其他用户无法访问，甚至上传文件的用户也无法删除或查看这些文件）。若要允许 644 权限，例如，你可以添加以下行：

```
anon_umask=022
```

当你允许匿名用户上传文件时，你可以授予其有限的更改所上传文件的能力。通过添加以下行，你可以允许匿名用户重命名或删除任何属于匿名用户的文件，前提是这些文件位于用户具有写权限的目录中：

```
anon_other_write_enable=YES
```

如果你还想允许匿名用户创建自己的目录，请添加以下行：

```
anon_mkdir_write_enable=YES
```

默认情况下，`ftp` 用户拥有匿名用户上传的文件的所有权。如果你想指定匿名上传的文件由另一个用户（你选择的用户）所有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果你有一个名为 `mynewuser` 的用户账户，可以如下设置这些选项：

```
chown_uploads=YES
chown_username=mynewuser
```

当然，你可以创建并使用任何你想要的用户名。但是，出于安全原因，你不应该使用 `root` 登录或其他管理登录来执行此操作。

###### 添加消息文件

虽然 `vsFTpd` 不支持诸如 `WU-FTP` 等 FTP 服务器所支持的 `README` 和欢迎文件的排列，但你可以向 `vsFTpd` 服务器上的任何可访问目录添加消息文件。然后，如果你使用默认的 `dirmessage_enable` 选项如下所示，当用户进入该目录时，`.message` 文件中的文本将显示出来：

```
dirmessage_enable=YES
```

你可能至少想为匿名用户的 FTP 服务器根目录添加一个 `.message` 文件。默认情况下，该位置是 `/var/ftp/.message`。如果你想使用 `.message` 文件以外的文件，可以设置 `message_file` 选项。例如，若要在你进入目录时显示 `mymessage` 文件中的文本，可以添加以下行：

```
message_file=mymessage
```

`.message` 文件为你提供了添加服务器内容信息、版权信息或软件使用说明的机会。通过允许不同的消息文件，你可以根据访问者在文件服务器上的位置，定制你想对他们说的话。

你还可以设置一条单行消息，使其在登录提示之前显示。你可以通过输入以下行来实现，将文本替换为你想说的任何内容：

```
ftpd_banner=Welcome to My FTP service.
```

作为一种安全措施，你可以考虑添加一个显示与你正在运行的操作系统不同的横幅。任何能够阻碍潜在入侵者查明你正在运行什么软件的信息，都有助于你更容易地将入侵者拒之门外。

###### 记录 vsFTPpd 活动

`vsFTPd` 默认启用日志记录，你的 `vsFTPd` 站点活动会被写入 `/var/log/xferlog.file`。以下选项启用日志记录并将日志文件更改为 `/var/log/vsftpd.log`：

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

如果需要，你可以通过将 `YES` 更改为 `NO` 来关闭日志记录。但请注意，日志记录允许你监视潜在的入侵，因此不建议关闭。你可以通过更改 `xferlog_file` 选项的值来更改日志文件的位置。请记住，由于使用量大，你的 FTP 服务器可能会产生大量日志消息。因此，为了使其有用，你需要相当频繁地监控日志。

如果你希望使用生成传输统计数据的工具，可以令 `vsFTPd` 以标准 `xferlog` 格式写入日志数据，该格式由 `WU-FTPD` 和其他 FTP 服务器使用。若要将以 `xferlog` 格式存储传输数据，请设置以下选项：

```
xferlog_std_format=YES
```

###### 设置超时

`vsftpd` 中默认设置了以下超时（这些值已内置，因此你无需对 `/etc/vsftpd/vsftpd.conf` 文件进行任何更改即可使其生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```
