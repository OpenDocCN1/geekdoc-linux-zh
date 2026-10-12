
# 在 SUSE 上运行 FTP 服务器

`226 Directory send OK.`
`ftp>`

如果你在 `ftp` 提示符下输入 `pwd` 来查看你当前所处的目录：

```
ftp> pwd

257 "*"

ftp>
```

你会发现你正处于 FTP 服务器的根目录（就像 Apache Web 服务器的根目录通常是 `/srv/www/` 一样）。因此，无论你在那里放置任何文件或目录，FTP 客户端都能看到。如果你将一个文件 `testfile` 复制到 `/srv/ftp/`，你将可以使用示例所示的 `get` 命令通过 FTP 下载它：

```
ftp> ls

229 Entering Extended Passive Mode (||4024|)

150 Here comes the directory listing.

-rw-r--r-- 4096 Dec 09 18:08 testfile

226 Directory send OK.

ftp> get testfile

local: testfile remote: testfile

229 Entering Extended Passive Mode (||40089)

150 Opening BINARY mode connection for testfile (4096 bytes).

1000|********************************************| 4096

32.65 MB/s 00:00 ETA

226 File received in 00:00 (1.02 MB/s)

ftp>
```

如果你查看服务器上的 `/var/log`，你会发现 `vsftpd` 已经记录了日志和日期：

```
Dec 9 18:09:04 vsftpd: Sun Dec 9 18:09:04 2007 [pid 2878] CONNECT:
Client "192.168.1.1"

Dec 9 18:09:08 vsftpd: Sun Dec 9 18:09:08 2007 [pid 2877] [ftp] OK
LOGIN: Client "192.168.1.1", anon password "password"

Dec 9 18:09:42 vsftpd: Sun Dec 9 18:09:42 2007 [pid 2879] [ftp] OK
DOWNLOAD: "192.168.1.1", "testfile", 4096 bytes, 1265.82Kbyte/sec
```

注意，你可以通过对 `/etc/vsftpd.conf` 进行细微更改，强制 `vsftpd` 将其日志写入指定的日志文件中。只需确保以下行内容如下：

```
log_ftp_protocol=YES
xferlog_enable=YES
vsftpd_log_file=/var/log/vsftpd.log
```

然后注释掉或删除该行：

```
syslog_enable=YES
```

你可以通过在配置文件中包含如下行来创建自定义的 FTP 横幅（banner）：

```
ftpd_banner="Welcome to our very fine FTP service."
```

当用户使用文本 FTP 或专用 FTP 客户端登录时，他们会在登录提示符之前看到以下消息：

```
220 "Welcome to our very fine FTP service."
Name (localhost:user):
```

这可以用于提供服务，但对于使用浏览器连接的用户来说没有用。包含 `README` 和 `README.html` 文件可能很有用，如果这些用户使用图形化客户端，可以点击这些文件。

你还可以在 `/srv/ftp/` 或其任何子目录中放置 `.message` 文件。当用户切换到包含此类文件的目录时，文件的内容将被显示。

```
ftp> cd pub
250-This directory contains useful files
250 Directory successfully changed.
ftp>
```

文件 `/srv/ftp/pub/.message` 仅包含以下行：

```
This directory contains useful files
```

## Setting Up User with vsftpd

注意，你可以通过对 `/etc/vsftpd.conf` 进行细微更改，强制 `vsftpd` 将其日志写入指定的日志文件中。只需确保以下行内容如下：

```
log_ftp_protocol=YES
xferlog_enable=YES
vsftpd_log_file=/var/log/vsftpd.log
```

然后注释掉或删除该行：

```
syslog_enable=YES
```

你可以通过在配置文件中包含如下行来创建自定义的 FTP 横幅（banner）：

```
ftpd_banner="Welcome to our very fine FTP service."
```

当用户使用文本 FTP 或专用 FTP 客户端登录时，他们会在登录提示符之前看到以下消息：

```
220 "Welcome to our very fine FTP service."
Name (localhost:user):
```

## Implementing Network Services in SUSE

通过上述描述的设置，你能够执行以下操作：

```
root@bible:/srv/ftp# ls -A
d-w------ 2 ftp 144 Aug 10 17:31 incoming
```

这些权限意味着用户无法列出目录，但 FTP 守护进程可以写入，因此上传将可行。你还应该考虑一种只写设置，通过创建一个如 `/srv/ftp/incoming/` 的目录并由 `ftp` 用户所有，且具有严格的权限。

## Security Considerations

**注意：** 除非你仔细考虑过自己在做什么，否则我们无法强调允许匿名写入的危险性。特别是，可写目录绝对不应该是 FTP 结构的根目录 `/srv/ftp/`。

## Allowing Uploads

如果你想允许本地用户上传，你需要在 `/etc/vsftpd.conf` 中设置以下内容：

```
write_enable=YES
```

如果你已经执行了此操作，像所示的新会将会成功上传到主目录。

如果你还想允许匿名登录进行上传，你需要启用以下项：

```
anon_upload_enable=YES
```

## 第四部分 在 SUSE Linux 中实现网络服务

```
250 Directory successfully changed.
ftp> put afile
local: afile remote: afile
229 Entering Extended Passive Mode (||62494|)
150 OK to send data.
226 File receive OK.
ftp> ls
229 Entering Extended Passive Mode (||50259|)
150 Here comes the directory listing.
226 Transfer done (but failed to open directory).
ftp>
```
