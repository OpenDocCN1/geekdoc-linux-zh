

$ su -c 'systemctl enable vsftpd.service'
$ su -c 'systemctl start vsftpd.service'

修改 vsftpd 配置文件后，再次执行第二条命令，将 start 替换为 restart 以让 vsftpd 重新读取这些文件。

## 注意事项

- **安全性**：最安全的策略是不允许用户通过 FTP 进行身份验证；而是仅使用 FTP 进行匿名访问。如果你确实允许本地用户进行身份验证并向服务器上传文件，务必将本地用户放入 chroot 监狱（第 729 页）。由于 FTP 以明文形式发送用户名和密码，恶意用户可以轻松嗅探（第 1276 页）它们。一旦掌握了用户名和密码，同一用户可以冒充本地用户，上传特洛伊木马（第 1281 页），并进而入侵系统。

- **防火墙**：FTP 服务器通常使用 TCP 21 端口。如果服务器运行着防火墙或位于防火墙之后，你需要打开此端口。请输入以下命令，以便在系统每次启动时（永久）以及在运行中的系统上打开此端口；有关 firewall-cmd 的信息，请参阅第 906 页：

```
$ su -c 'firewall-cmd --add-service=ftp'
$ su -c 'firewall-cmd --permanent --add-service=ftp'
```

- **SELinux**：当 SELinux 设置为使用 targeted 策略时，FTP 会受到 SELinux 的保护。有关更多信息，请参阅第 476 页的“使用 system-config-selinux 设置 Targeted 策略”。

## 快速入门 II：启动 vsftpd FTP 服务器

默认情况下，在 Fedora/RHEL 中，vsftpd 仅允许本地用户和匿名用户登录服务器；它不会设置来宾账户。当某人以匿名用户身份登录时，该用户在 /var/ftp 目录中工作，可以下载文件但不能上传文件。你不需要配置任何内容。

## 故障排除

首先确保防火墙和 SELinux（如上所述）已设置允许用户通过 ftp 登录并复制文件。另外，请确保设置了 `listen` 或 `listen_ipv6`，但不要同时设置两者为 YES（第 727 页）。接下来，通过从服务器系统登录来确保 vsftpd 正在运行。你可以在命令行中将服务器引用为 localhost 或使用其主机名。以用户身份登录并提供该用户的密码：

```
$ ftp localhost
Trying ::1...
Connected to localhost (::1).
220 (vsFTPd 3.0.2)
Name (localhost:sam): sts
331 Please specify the password.
Password:
230 Login successful...
```

如果你无法连接到服务器，首先确保服务器正在运行：

```
# systemctl status vsftpd.service
vsftpd.service - vsftpd ftp daemon
Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; disabled)
Active: active (running) since Tue 2013-09-10 13:02:09 PDT; 58min ago
Process: 9351 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf (code=exited, status=0/SUCCESS)
Main PID: 9352 (vsftpd)
   CGroup: name=systemd:/system/vsftpd.service
           ??9352 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

Sep 10 13:02:09 guava.example.com systemd[1]: Started vsftpd ftp daemon.
```

如果你希望允许用户以 anonymous 或 ftp 身份登录，必须在 /etc/vsftpd/vsftpd.conf 中将 **anonymous_enable** 设置为 YES（默认为 YES，第 728 页）。如果你更改了 *vsftpd.conf*，请重启 *vsftpd* 守护进程（第 724 页）。对于这些登录名称，任何密码都是可接受的。

```
$ ftp localhost
Trying ::1...
Connected to localhost (::1).
220 (vsFTPd 3.0.2)
Name (localhost:sam): anonymous
331 Please specify the password.
Password:
230 Login successful.
...
```

接下来检查 /var/ftp 的权限，或者 /etc/passwd 中指定的 ftp 主目录的权限，是否设置为 755，并且该目录的所有者不是 ftp。如果 ftp 用户可以写入 /var/ftp，连接将失败。

```
$ ls -ld /var/ftp
drwxr-xr-x. 3 root root 4096 06-13 10:09 /var/ftp
```

一旦你能从本地系统登录，请从另一个系统登录——可以是局域网内的系统，或者是能够访问服务器的其他系统。在命令行中，使用局域网内部的主机名，或者使用局域网外部的 FQDN（第 1250 页）。对话过程应与之前的示例相同。如果你无法从一个非局域网系统登录，请使用 *ping*（第 305 页）测试连接，然后确保防火墙已设置以允许 FTP 访问。请参阅第 715 页的“FTP 连接”，了解活动模式和被动模式以及每种模式使用的端口的讨论。

## 配置 vsftpd 服务器

vsftpd 的配置文件 /etc/vsftpd/vsftpd.conf 列出了配置参数（称为指令）的布尔值、数值和字符串名称-值对。每个名称-值对由等号连接，两侧均无空格。Fedora/RHEL 提供了带有详细注释的 vsftpd.conf 文件，该文件更改了许多内置默认值。本节涵盖了许多参数，并注明了它们的默认值以及在 Fedora/RHEL 随附的 vsftpd.conf 文件中指定的值。

将布尔参数设置为 YES 或 NO，将数值参数设置为非负整数。八进制数对于设置 **umask** 参数非常有用，必须以 0（零）开头。没有前导零的数字被视为基数为 10 的数字。以下是设置每种类型参数的示例：

```
anonymous_enable=YES
local_umask=022
xferlog_file=/var/log/vsftpd.log
```

指令的描述分为以下几组：

- 服务器设置（下一个主题）
- 登录（下一页）
- 工作目录和 **chroot** 监狱（第 729 页）
- 下载和上传文件（第 730 页）
- 消息（第 732 页）
- 显示（第 733 页）
- 日志（第 734 页）
- 连接参数（第 734 页）
- 其他（第 736 页）
- 其他配置文件（第 737 页）

### 服务器设置

**listen**
YES 仅接受来自 IPv4 客户端的连接。此参数或 **listen_ipv6** 必须设置为 YES，但不能两者都设置。

默认值：NO
Fedora/RHEL：NO

**listen_ipv6**
YES 接受来自 IPv6 客户端的连接。当 **listen_address** 未设置或设置为 ::（“任何”地址）时，**vsftpd** 接受来自 IPv4 和 IPv6 客户端的连接。此参数或 **listen** 必须设置为 YES，但不能两者都设置。

默认值：NO
Fedora/RHEL：YES

**listen_address**
指定 **vsftpd** 监听传入连接的本地接口的 IP 地址。当此参数未设置时，**vsftpd** 使用默认网络接口。

默认值：无

**listen_port**
指定 **vsftpd** 监听传入连接的端口。

默认值：21

**max_clients**
指定客户端的最大数量。零（0）表示无限制。

默认值：0

**max_per_ip**
指定来自相同 IP 地址的客户端的最大数量。零（0）表示来自相同 IP 地址的客户端数量无限制。

默认值：0

## 登录

有三类用户可以登录 vsftpd 服务器：匿名用户、本地用户和来宾用户。来宾用户很少使用，本章不作介绍。本地用户使用其系统用户名和密码登录。匿名用户使用 **anonymous** 或 **ftp** 及其电子邮件地址作为密码登录。你可以控制这些各类用户是否可以在服务器上登录以及他们登录后可以执行的操作。你还可以在逐用户基础上指定本地用户在服务器上可以执行的操作；有关更多信息，请参阅第 736 页的 user_config_dir。

### 本地用户

**userlist_enable**
*/etc/vsftpd/user_list* 文件（第 737 页），或由 userlist_file 指定的其他文件，包含零个或多个用户的列表。YES 会查询此列表并根据 **userlist_deny** 采取行动，要么授予列表中的用户登录服务器的权限，要么拒绝。为了防止明文密码传输，在用户输入用户名后立即拒绝访问。NO 不查询此列表。设置为 NO 可构建更安全的系统。

默认值：NO
Fedora/RHEL：YES

**userlist_deny**
YES 防止列表 */etc/vsftpd/user_list*（第 737 页）中列出的用户登录服务器。NO 允许 *仅* 列表 */etc/vsftpd/user_list* 中列出的用户登录服务器。使用 **userlist_file** 更改此参数查询的文件名。此参数仅在 **userlist_enable** 设置为 YES 时检查。

默认值：YES

**userlist_file**
当 **userlist_enable** 设置为 YES 时查询的文件名。

默认值：*/etc/vsftpd/user_list*

**local_enable**
YES 允许本地用户（列在 */etc/passwd* 中的用户）登录服务器。

默认值：NO
Fedora/RHEL：YES

### 匿名用户

**anonymous_enable**
YES 允许匿名登录。NO 禁用匿名登录。

默认值：YES

**no_anon_password**
YES 跳过向匿名用户询问密码的步骤。

默认值：NO

