

## 配置 vsftpd 服务器

**vsftpd** 的配置文件 `/etc/vsftpd.conf` 列出了配置参数（称为指令）的布尔型、数值型和字符串型名称-值对。每个名称-值对通过等号连接，且等号两侧**没有空格**。Ubuntu Linux 提供了一个注释详尽的 **vsftpd.conf** 文件，该文件修改了许多编译时设置的默认值。本节涵盖大多数选项，并注明其默认值以及 Ubuntu Linux 随附的 **vsftpd.conf** 文件中指定的值。

将布尔选项设置为 **YES** 或 **NO**，将数值选项设置为非负整数。八进制数（对设置 **umask** 选项有用）必须以 0（零）开头。没有前导零的数字被视为十进制数。以下是 **vsftpd.conf** 中设置各种类型选项的示例：

```
anonymous_enable=YES
local_umask=022
xferlog_file=/var/log/vsftpd.log
```

指令的说明分为以下几组：

- **独立（Stand-alone）** 模式（第 701 页）
- **登录**（第 702 页）
- **工作** 目录和 **chroot** 监狱（第 703 页）
- **下载** 和上传文件（第 704 页）
- **消息**（第 707 页）
- **显示**（第 707 页）
- **日志**（第 708 页）
- 连接参数（第 708 页）

### 独立模式

请参考第 693 页的“笔记”，以了解关于常规模式和独立模式的讨论。本节描述了影响独立模式的参数。

**listen**

设置为 YES 时以独立模式运行 **vsftpd**；设置为 NO 时以常规模式运行。

默认值：NO

Ubuntu：YES

**listen_address**

在独立模式下，指定 **vsftpd** 监听传入连接的本地接口的 IP 地址。当未设置此参数时，**vsftpd** 使用默认网络接口。

默认值：无

**listen_port**

在独立模式下，指定 **vsftpd** 监听传入连接的端口。

默认值：21

**max_clients**

在独立模式下，指定最大客户端数量。零（0）表示客户端数量无限制。

默认值：0

**max_per_ip**

在独立模式下，指定来自同一 IP 地址的最大客户端数量。零（0）表示来自同一 IP 地址的客户端数量无限制。

默认值：0

### 登录

有三类用户可以登录 vsftpd 服务器：匿名用户、本地用户和访客。访客用户很少使用，本章不予介绍。本地用户使用其系统用户名和密码登录。匿名用户使用 anonymous 或 ftp 登录，并将其电子邮件地址作为密码。你可以控制这些各类用户能否在服务器上登录以及登录后可以执行的操作。你还可以针对每个用户指定本地用户在服务器上可以执行的操作；有关更多信息，请参考第 710 页的 user_config_dir。

#### 本地用户

**userlist_enable** /etc/vsftpd.user_list 文件（第 711 页），或由 userlist_file 指定的其他文件，包含零个或多个用户的列表。设置为 YES 时，系统会参考此列表并根据 userlist_deny 采取行动，授予或拒绝此列表中用户登录服务器的权限。为了防止明文密码传输，在用户输入其用户名后立即拒绝访问。设置为 NO 时，系统不参考此列表。为了更安全的系统，建议将此参数设置为 NO。

默认值：NO

**userlist_deny** 设置为 YES 时，禁止 /etc/vsftpd.user_list（第 711 页）中列出的用户登录服务器。设置为 NO 时，仅允许 /etc/vsftpd.user_list 中列出的用户登录服务器。使用 userlist_file 可以更改此参数参考的文件名。仅当 userlist_enable 设置为 YES 时才会检查此参数。

默认值：YES

**userlist_file** 当 userlist_enable 设置为 YES 时参考的文件名。

默认值：/etc/vsftpd.user_list

**local_enable** 设置为 YES 时，允许本地用户（/etc/passwd 中列出的用户）登录服务器。

默认值：NO

#### 匿名用户

**anonymous_enable** 设置为 YES 时，允许匿名登录。设置为 NO 时，禁止匿名登录。

默认值：YES

Ubuntu：NO

**no_anon_password**

设置为 YES 时，跳过向匿名用户询问密码。

默认值：NO

**deny_email_enable**

设置为 YES 时，检查匿名用户输入的密码（电子邮件地址）是否列在 /etc/vsftpd.banned_emails 或由 banned_email_file 指定的其他文件中。如果列在其中，则不允许该用户在系统上登录。设置为 NO 时，不执行此检查。通常，使用 gufw（第 876 页）或 iptables（第 863 页）阻止特定主机比使用此参数更有效。

默认值：NO

**banned_email_file**

当 deny_email_enable 设置为 YES 时参考的文件名。

默认值：/etc/vsftpd.banned_emails

### 工作目录和 chroot 监狱

当用户登录 vsftpd 服务器时，标准文件系统访问权限控制用户可以访问哪些目录和文件，以及用户如何访问它们。三个基本参数控制登录到 vsftpd 服务器的用户：

- 用户 ID (UID)
- 初始工作目录
- 根目录

默认情况下，vsftpd 服务器将本地用户的用户 ID 设置为该用户的用户名，将匿名用户的用户 ID 设置为 ftp。本地用户从其主目录开始，匿名用户从 /srv/ftp 开始。

出于安全考虑，默认情况下，匿名用户会被置于 chroot 监狱中；本地用户则不会。例如，当匿名用户登录 vsftpd 服务器时，其主目录是 /srv/ftp。然而，用户看到的是其主目录为 /。用户看到 /srv/ftp/upload 目录为 /upload。由于用户处于 chroot 监狱中，因此无法看到或操作 /home、/usr/local 或 /tmp 等目录。有关更多信息，请参考第 466 页的“设置 chroot 监狱”。

你可以使用 chroot_local_user 选项将每个本地用户置于一个 chroot 监狱中，该监狱的根目录为用户的主目录。你可以使用 chroot_list_enable 将选定的本地用户置于 chroot 监狱中。

**chroot_list_enable**

登录时，设置为 YES 时检查本地用户是否列在 /etc/vsftpd.chroot_list（第 711 页）或由 chroot_list_file 指定的其他文件中。

当用户在列表中且 **chroot_local_user** 设置为 NO 时，该用户被置于其主目录的 chroot 监狱中。只有列在 /etc/vsftpd.chroot_list 中的用户才会被置于 chroot 监狱中。

当用户在列表中且 **chroot_local_user** 设置为 YES 时，该用户不会被置于 chroot 监狱中。未列在 /etc/vsftpd.chroot_list 中的用户会被置于 chroot 监狱中。

默认值：NO

| 项目 | 描述 |
| :--- | :--- |
| **chroot_local_user** | 参见 **chroot_list_enable**。对于更开放的系统设置为 NO，但请记住，当向系统添加用户时，如有需要请将新用户添加到 **chroot_list_file** 中。对于更安全的系统设置为 YES。除非将新用户添加到 **chroot_list_file**，否则新用户会自动受到限制。<br>默认值：NO |
| **chroot_list_file** | 当 **chroot_list_enable** 设置为 YES 时参考的文件名。<br>默认值：/etc/vsftpd.chroot_list |
| **passwd_chroot_enable** | 设置为 YES 时，允许更改 **chroot_list_enable** 和 **chroot_local_user** 设置对本地用户施加的 chroot 监狱的位置。<br>可以通过在 /etc/passwd 中该用户的主目录字符串中包含 /../ 来将 chroot 监狱的位置向上移动目录结构。此更改对标准系统登录没有影响，正如 cd 命令对工作目录没有影响一样。<br>例如，将 /etc/passwd（第 494 页）中 Sam 的主目录字段从 /home/sam 更改为 /home/../sam，允许 Sam 在使用 vsftpd 登录后 cd 到 /home。在权限允许的情况下，Sam 现在可以查看文件并与另一用户协作。<br>默认值：NO |
| **secure_chroot_dir** | 一个用户 **ftp** 不可写的空目录的名称。**vsftpd** 服务器在用户不需要访问文件系统时使用此目录作为安全的 chroot 监狱。<br>默认值：/var/run/vsftpd/empty |
| **local_root** | 本地用户登录服务器后，此目录成为用户的工作目录。如果指定的目录不存在，不会引发错误。<br>默认值：无 |

### 下载和上传文件

默认情况下，任何用户——无论是本地还是匿名用户——只要具备适当的文件系统访问权限和权限，都可以从 vsftpd 服务器下载文件。若要允许本地用户上传文件，必须将 **write_enable** 从 NO（默认值）更改为 YES。默认情况下，**local_umask** 设置为 077，使上传的文件具有 600 权限（第 215 页）。这些权限仅允许创建该文件的用户下载

