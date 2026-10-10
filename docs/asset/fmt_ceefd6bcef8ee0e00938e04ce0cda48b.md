
# `listen_ipv4`

`YES` 仅接受来自 IPv4 客户端的连接。此参数或 `listen_ipv6` 必须设置为 `YES`，但不能两者都设置。

默认值：`NO`

Fedora/RHEL：`NO`

# `listen_ipv6`

`YES` 接受来自 IPv6 客户端的连接。当 `listen_address` 未设置或设置为 `::`（“任何”地址）时，`vsftpd` 接受来自 IPv4 和 IPv6 客户端的连接。此参数或 `listen` 必须设置为 `YES`，但不能两者都设置。

默认值：`NO`

Fedora/RHEL：`YES`

# `listen_address`

指定 `vsftpd` 监听传入连接的本地接口的 IP 地址。当此参数未设置时，`vsftpd` 使用默认网络接口。

默认值：无

# `listen_port`

指定 `vsftpd` 监听传入连接的端口。

默认值：`21`

# `max_clients`

指定客户端的最大数量。零（`0`）表示无限制。

默认值：`0`

# `max_per_ip`

指定来自相同 IP 地址的客户端的最大数量。零（`0`）表示来自相同 IP 地址的客户端数量无限制。

默认值：`0`

## 登录

有三类用户可以登录 `vsftpd` 服务器：匿名用户、本地用户和来宾用户。来宾用户很少使用，本章不作介绍。本地用户使用其系统用户名和密码登录。匿名用户使用 `anonymous` 或 `ftp` 及其电子邮件地址作为密码登录。你可以控制这些各类用户是否可以在服务器上登录以及他们登录后可以执行的操作。你还可以在逐用户基础上指定本地用户在服务器上可以执行的操作；有关更多信息，请参阅第 736 页的 `user_config_dir`。

### 本地用户

#### `userlist_enable`

`/etc/vsftpd/user_list` 文件（第 737 页），或由 `userlist_file` 指定的其他文件，包含零个或多个用户的列表。`YES` 会查询此列表并根据 `userlist_deny` 采取行动，要么授予列表中的用户登录服务器的权限，要么拒绝。为了防止明文密码传输，在用户输入用户名后立即拒绝访问。`NO` 不查询此列表。设置为 `NO` 可构建更安全的系统。

默认值：`NO`

Fedora/RHEL：`YES`

#### `userlist_deny`

`YES` 防止列表 `/etc/vsftpd/user_list`（第 737 页）中列出的用户登录服务器。`NO` 允许 *仅* 列表 `/etc/vsftpd/user_list` 中列出的用户登录服务器。使用 `userlist_file` 更改此参数查询的文件名。此参数仅在 `userlist_enable` 设置为 `YES` 时检查。

默认值：`YES`

#### `userlist_file`

当 `userlist_enable` 设置为 `YES` 时查询的文件名。

默认值：`/etc/vsftpd/user_list`

#### `local_enable`

`YES` 允许本地用户（列在 `/etc/passwd` 中的用户）登录服务器。

默认值：`NO`

Fedora/RHEL：`YES`

### 匿名用户

#### `anonymous_enable`

`YES` 允许匿名登录。`NO` 禁用匿名登录。

默认值：`YES`

#### `no_anon_password`

`YES` 跳过向匿名用户询问密码的步骤。

默认值：`NO`

#### `deny_email_enable`

设置为 `YES` 时，系统将检查匿名用户输入密码（电子邮件地址）是否列在 `/etc/vsftpd/banned_emails` 或由 `banned_email_file` 指定的其他文件中。如果列在其中，则不允许该用户登录系统。设置为 `NO` 时，不执行此检查。使用 `firewall-cmd`（第 906 页）阻止特定主机通常比使用此参数更高效。

默认值：`NO`

#### `banned_email_file`

当 `deny_email_enable` 设置为 `YES` 时，将被查阅的文件名。

默认值：`/etc/vsftpd/banned_emails`

## 工作目录和 `chroot` 限制环境

当用户登录 `vsftpd` 服务器时，标准文件系统访问权限控制用户可以访问哪些目录和文件，以及用户可以如何访问它们。三个基本参数控制登录到 `vsftpd` 服务器的用户：

- 用户 ID (`UID`)

- 初始工作目录

- 根目录

默认情况下，`vsftpd` 服务器将本地用户的 `UID` 设置为该用户的 `UID`，并将匿名用户的 `UID` 设置为名为 `ftp` 用户的 `UID`。本地用户从其主目录开始，匿名用户从 `/var/ftp` 开始。

默认情况下，为了安全起见，匿名用户被置于 `chroot` 限制环境中；本地用户则不是。例如，当匿名用户登录 `vsftpd` 服务器时，其主目录是 `/var/ftp`。然而，该用户看到的却是其主目录为 `/.`。该用户将 `/var/ftp/upload` 目录视为 `/upload`。由于用户处于 `chroot` 限制环境中，因此无法查看或操作例如 `/home`、`/usr/local` 或 `/tmp` 等目录。有关更多信息，请参阅第 487 页的“设置 `chroot` 限制环境”。

您可以使用 `chroot_local_user` 参数将每个本地用户置于一个以该用户主目录为根目录的 `chroot` 限制环境中。您可以使用 `chroot_list_enable` 将选定的本地用户置于 `chroot` 限制环境中。

#### `chroot_list_enable`

登录时，设置为 `YES` 则检查本地用户是否列在 `/etc/vsftpd/chroot_list`（第 737 页）或由 `chroot_list_file` 指定的其他文件中。

如果用户在列表中，且 `chroot_local_user` 设置为 `NO`，则该用户将被置于其主目录中的 `chroot` 限制环境中。只有列在 `/etc/vsftpd/chroot_list` 中的用户才会被置于 `chroot` 限制环境中。

如果用户在列表中，且 `chroot_local_user` 设置为 `YES`，则该用户不会被置于 `chroot` 限制环境中。未列在 `/etc/vsftpd/chroot_list` 中的用户会被置于 `chroot` 限制环境中。

默认值：`NO`

#### `chroot_local_user`

参见 `chroot_list_enable`。设置为 `NO` 可获得更开放的系统，但请记住在系统添加用户时，根据需要将这些新用户添加到 `chroot_list_file` 中。设置为 `YES` 可获得更安全的系统。新用户将自动受到限制，除非您将其添加到 `chroot_list_file`。

默认值：`NO`

#### `chroot_list_file`

当 `chroot_list_enable` 设置为 `YES` 时，将被查阅的文件名。

默认值：`/etc/vsftpd/chroot_list`

#### `passwd_chroot_enable`

设置为 `YES` 时，允许您更改由 `chroot_list_enable` 和 `chroot_local_user` 设置对本地用户施加的 `chroot` 限制环境的位置。通过在 `/etc/passwd` 中该用户的主目录字符串内包含 `./`，可以将 `chroot` 限制环境的位置向上移动目录结构。此更改对标准系统登录没有影响，正如 `cd .` 命令对工作目录没有影响一样。

例如，将 Sam 在 `/etc/passwd`（第 508 页）中的主目录字段从 `/home/sam` 更改为 `/home/./sam`，允许 Sam 在使用 `vsftpd` 登录后 `cd` 到 `/home`。在拥有适当权限的情况下，Sam 现在可以查看文件并与另一个用户协作。

默认值：`NO`

#### `secure_chroot_dir`

一个用户 `ftp` 不可写的空目录的名称。`vsftpd` 服务器在用户不需要访问文件系统时，使用此目录作为安全的 `chroot` 限制环境。

默认值：`/usr/share/empty`

#### `local_root`

本地用户登录服务器后，此目录成为用户的工作目录。如果指定的目录不存在，不会导致错误。

默认值：`none`

## 下载和上传文件

默认情况下，任何用户——无论是本地用户还是匿名用户——都可以从 `vsftpd` 服务器下载文件，前提是拥有适当的文件系统访问权限和权限。必须将 `write_enable` 参数设置为 `YES`（Fedora/RHEL 如此设置），才能允许本地用户上传文件。`local_umask` 参数默认值为 `077`，但 Fedora/RHEL 将其设置为 `022`，使上传的文件具有 `644` 权限（第 191 页）。这些权限允许用户下载其他用户的文件。将 `local_umask` 更改为 `077`，以便仅允许创建该文件的用户下载和覆盖它。

**安全** 有关允许本地用户上传文件时创建的安全漏洞的信息，请参阅第 725 页的“安全”。

以下操作将 `vsftpd` 设置为允许匿名用户上传文件：

1. 将 `write_enable`（见下文）设置为 `YES`。（Fedora/RHEL 将此参数设置为 `YES`。）

2. 在 `/var/ftp` 下创建一个目录，匿名用户可以写入但不可读取（模式 `333`）。你并不希望恶意用户能够查看、下载、修改并上传由另一个用户最初上传的文件。以下命令创建一个任何人可写入但无人可读取的 `/var/ftp/uploads` 目录：

   ```bash
   # mkdir /var/ftp/uploads
   # chmod 333 /var/ftp/uploads
   ```

   由于安全风险，当匿名用户（`ftp`）可以写入 `/var/ftp` 时，`vsftpd` 会阻止匿名连接。

3. 将 `anon_upload_enable`（第 732 页）设置为 `YES`。

4. 查看本节中的其他参数。

### 本地用户的下载/上传

#### `local_umask`

本地用户的 `umask`（第 469 页）设置。

默认值：`077`
Fedora/RHEL: `022`

#### `file_open_mode`

本地用户上传文件的权限。会将 `umask`（第 469 页）应用于此值。更改为 `0777` 以使上传的文件可执行。

默认值：`0666`

#### `write_enable`

设置为 `YES` 允许用户创建和删除文件和目录（假设具有适当的文件系统权限）。设置为 `NO` 阻止用户对文件系统做出更改。

默认值：`NO`
Fedora/RHEL: `YES`

### 匿名用户

#### `anon_mkdir_write_enable`

设置为 `YES` 时，当 `write_enable` 设置为 `YES` 且匿名用户有权写入工作目录时，允许匿名用户创建新目录。

默认值：`NO`

#### `anon_other_write_enable`

设置为 `YES` 时，除了 `anon_mkdir_write_enable` 和 `anon_upload_enable` 授予的权限外，还授予匿名用户写入权限。例如，设置为 `YES` 允许匿名用户删除和重命名文件，假设她有权写入工作目录。对于更安全的站点，请勿将此参数设置为 `YES`。

默认值：`NO`

#### `anon_root`

匿名用户登录服务器后，此目录成为用户的工作目录。如果指定的目录不存在，不会导致错误。

默认值：`none`

#### `anon_umask`

匿名用户的 `umask`（第 469 页）设置。默认设置仅允许匿名用户访问由匿名用户上传的文件；将此参数设置为 `022` 以让所有人都能读取这些文件。

默认值：`077`

#### `anon_upload_enable`

当 `write_enable=YES` 且匿名用户有权写入目录时，设置为 `YES` 允许匿名用户上传文件。

默认值：`NO`

#### `anon_world_readable_only`

设置为 `YES` 时，将用户可以下载的文件限制为那些文件所有者、与文件关联的组的其他成员以及其他用户可以读取的文件。可能不希望允许一个匿名用户下载由另一个匿名用户上传的文件。将此参数设置为 `YES` 可以避免这种情况。

默认值：`YES`

#### `ascii_download_enable`

设置为 `YES` 允许用户使用 ASCII 模式（第 720 页）下载文件。将此参数设置为 `YES` 可能会带来安全风险（第 720 页）。

默认值：`NO`

#### `ascii_upload_enable`

设置为 `YES` 允许用户使用 ASCII 模式（第 720 页）上传文件。

默认值：`NO`

#### `chown_uploads`

设置为 `YES` 时，由匿名用户上传的文件将归 `root`（或由 `chown_username` 指定的其他用户）所有。为了提高安全性，如果将此参数设置为 `YES`，请将 `chown_username` 更改为 `root` 以外的名称。

默认值：`NO`

#### `chown_username`

参见 `chown_uploads`。

默认值：`root`

#### `ftp_username`

匿名用户的用户名。

默认值：`ftp`

#### `nopriv_user`

`vsftpd` 使用的具有最小特权的用户名称。由于其他程序使用 `nobody`，为了增强安全性，您可以将 `nobody` 替换为专用用户的名称，例如 `ftp`。

默认值：`nobody`

## 消息

您可以替换 `vsftpd` 在用户登录系统时显示的标准欢迎横幅（`banner_file` 和 `ftp_banner`）。您还可以在每次用户进入目录时显示消息（`dirmessage_enable` 和 `message_file`）。当设置 `dirmessage_enable=YES`，每次用户使用 `cd` 命令进入目录时，`vsftpd` 会显示该目录下名为 `.message`（或由 `message_file` 指定的其他文件）的内容。

### `dirmessage_enable`

当 FTP 用户通过输入 `cd` 命令进入新目录时，`YES` 会显示 `.message` 文件或 `message_file` 指定的其他文件。

默认值：`NO`

Fedora/RHEL：`YES`

### `message_file`

参见 `dirmessage_enable`。

默认值：`.message`

### `banner_file`

用户连接服务器时显示的文件绝对路径。

覆盖 `ftpd_banner`。

默认值：无

### `ftpd_banner`

覆盖用户连接服务器时显示的标准 `vsftpd` 问候横幅。

默认值：无；使用标准 `vsftpd` 横幅

# 显示

本节描述可通过控制 `vsftpd` 显示信息的方式来改进安全性和性能的参数。

### `hide_ids`

`YES` 会在目录列表中将所有用户和组列为 `ftp`。`NO` 会列出实际的所有者。

默认值：`NO`

### `setproctitle_enable`

`NO` 会导致 `ps` 显示运行 `vsftpd` 的进程为 `vsftpd`。`YES` 会导致 `ps` 显示 `vsftpd` 当前正在执行的操作（如上传等）。设置为 `NO` 可使系统更安全。

默认值：`NO`

### `text_userdb_names`

`NO` 通过在目录列表中显示数字 `UID` 和 `GID` 来提高性能。

`YES` 会显示名称。

默认值：`NO`

### `use_localtime`

`NO` 会导致 `ls`、`mls` 和 `modtime` FTP 命令显示 UTC 时间（第 1279 页）。`YES` 会导致这些命令显示本地时间。

默认值：`NO`

### `ls_recurse_enable`

`YES` 允许用户输入 `ls -R` 命令。将此参数设置为 `YES` 可能会带来安全风险，因为在大型目录层级的顶部输入 `ls -R` 命令可能会消耗大量系统资源。

默认值：`NO`

# 日志

默认情况下，日志记录功能是关闭的。但是，随 Fedora/RHEL 提供的 `vsftpd.conf` 文件会将其打开。本节描述控制日志细节和位置的参数。

`vsftpd` 服务器可以生成两种格式的日志：`vsftpd` 和 `xferlog`。默认的 `vsftpd` 日志格式比 `xferlog` 格式更易于阅读，但不能被处理 `xferlog` 文件以生成统计摘要的程序所处理。请在互联网上搜索 `xferlog` 以获取有关此命令的更多信息。

#### `log_ftp_protocol`

`YES` 会在默认的 `vsftpd` 日志格式中记录 FTP 请求和响应，前提是 `xferlog_std_format` 设置为 `NO`。

默认值：`NO`

#### `xferlog_enable`

`YES` 会在 `/var/log/vsftpd.log`（或由 `xferlog_file` 指定的其他文件）中维护传输日志。`NO` 不会创建日志。

默认值：`NO`

Fedora/RHEL：`YES`

#### `xferlog_std_format`

只要 `xferlog_file` 被显式设置，`YES` 就会使传输日志（不涵盖连接）以标准 `xferlog` 格式（如 `wu-ftpd` 所使用的格式）写入。如果 `xferlog_std_format` 设置为 `YES` 且 `xferlog_file` 未显式设置，则日志记录功能关闭。将此参数设置为 `NO` 会使 `vsftpd` 以 `vsftpd` 日志格式生成日志，前提是 `log_ftp_protocol` 设置为 `YES`。

默认值：`NO`

Fedora/RHEL：`YES`

#### `xferlog_file`

参见 `xferlog_enable` 和 `xferlog_std_format`。

默认值：`/var/log/xferlog`

# 连接参数
