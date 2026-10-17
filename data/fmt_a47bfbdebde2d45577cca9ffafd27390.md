
正是`/etc/passwd`文件中的用户帐户条目允许匿名用户连接到FTP服务器。尽管用户帐户条目是`ftp`，但连接到FTP服务器时接受用户ID `anonymous`。事实上，许多人错误地认为`anonymous`是唯一可用的用户ID。

### 控制访问

可以通过以下四种方式之一控制对FTP服务器的访问：

- 删除或注释掉`/etc/passwd`文件中的FTP用户
- 将要排除的用户添加到`/etc/ftpusers`文件中
- 从`/etc/ftpaccess`文件中删除用户类别
- 通过`ftpshut`关闭FTP服务器

`/etc/ftpaccess`文件用于配置对FTP服务器的访问。初始安装时，该文件的内容如下：

```text
class       all    real,guest,anonymous  *

email root@localhost

loginfails 5

readme  README*  login

readme  README*  cwd=*

message /welcome.msg          login

message .message              cwd=*

compress       yes             all

tar             yes             all

chmod           no              guest,anonymous

delete          no              guest,anonymous

overwrite       no              guest,anonymous

rename          no              guest,anonymous

log transfers anonymous,real inbound,outbound

shutdown /etc/shutmsg

passwd-check rfc822 warn
```

此文件中定义的每个条目都在`ftpaccess`的手册页中详细描述。`/etc/ftpaccess`文件中的条目不仅控制谁能访问FTP服务器，还控制他们在建立连接后能做什么。

> **提示**
> 要禁止系统上所有真实帐户访问FTP服务器，请删除`/etc/ftpaccess`文件`class`行中的`real`条目。

`/etc/ftpusers`文件用于控制哪些用户无权访问FTP服务器。默认情况下，`/etc/ftpusers`文件中放置了以下条目：

- `root`
- `bin`
- `daemon`
- `adm`
- `lp`
- `sync`
- `shutdown`
- `halt`
- `mail`
- `news`
- `uucp`
- `operator`
- `games`
- `nobody`

如果用户名包含在`/etc/ftpusers`文件中，则该用户无法访问FTP服务器。如果尝试使用此文件中包含的某个用户名连接到FTP服务器，将返回以下消息：

```text
# ftp ftp.kcpartners.com

Connected to ftp.kcpartners.com.

220 router.kcpartners.com FTP server (Version wu-2.4.2-academ[BETA-17](1)

Wed Aug 19 02:55:52 MST 1998) ready.

Name (kcpartners.com:col): ftp

530 User ftp access denied.

Login failed.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp>
```

### 关闭FTP服务器

`ftpshut`命令可用于在指定时间中止FTP服务。它提供了一种通知用户FTP服务器暂时关闭、可以稍后重试的方法。`ftpshut`命令在`/etc`目录中创建一个名为`shutmsg`的文件。当尝试连接到FTP服务器时，FTP服务器会检查该文件是否存在。如果找到该文件，将显示以下消息：

```text
# ftp router

Connected to router.kcpartners.com.

500 router.kcpartners.com FTP server shut down -- please try again later.

ftp>
```

> **注意：** 发出`ftpshut`命令后，必须删除`/etc/shutmsg`文件才能重新建立FTP服务。

### 文件放置

由于FTP服务器默认启用匿名用户访问，因此放置文件以供FTP访问是一个简单的步骤。匿名FTP访问的默认目录结构经过配置，只需将文件放在`/home/ftp/pub`目录中即可。请注意，`/home/ftp`目录中的另外两个目录`/home/ftp/bin`和`/home/ftp/etc`在通过FTP连接时不可访问。将所有可公开访问的文件放在`/home/ftp/pub`目录下，或放在`/home/ftp/pub`内的子目录树结构中。

> **注意：** 请记得将FTP服务器上的所有文件权限设置为只读。`/home/ftp/pub`的目录权限默认就是这样设置的。

### 故障排除

*我尝试以root身份连接到ftp，但一直收到530 Login incorrect。Login Failed。我知道我使用了正确的密码。*

默认情况下，`root`被拒绝ftp访问。这是在PAM中配置的。大多数Linux发行版安装的`/etc/pam.d/ftp`文件包含一个`auth`行，列出`pam_listfile.so`并指向`/etc/ftpusers`。`sense=deny`意味着文件中列出的任何用户都会被拒绝ftp访问。`root`用户以及所有系统帐户都列在`/etc/ftpusers`文件中。您有两个选择：注释掉`/etc/pam.d/ftp`中的`auth`行，或注释掉`/etc/ftpusers`中的用户`root`（只需在该行开头放一个`#`）。然而，从安全角度来看，启用`root`对FTP的访问是一个非常糟糕的主意。如果这样做，您将严重削弱系统的安全性。即使在今天，对于仅偶尔使用调制解调器连接的系统，这也是一个值得关注的问题。

*我想关闭FTP服务器，但只是暂时关闭，而不是永久关闭。我该怎么做？*

使用`ftpshut`命令。此命令将写入一个默认路径为`/etc/shutmsg`的文件。（您可以在`/etc/ftpaccess`中更改此路径，`shutdown`变量指定了该文件。）当您准备再次允许访问时，只需删除`/etc/shutmsg`文件。在FTP关闭期间，任何尝试连接的用户都会在屏幕上看到`shutmsg`的内容。

*我想配置FTP，使某些用户无法登录或被锁定在特定目录中。我该怎么做？*

![](img/c741b1b6b6eccaba2ad43454c979a7f8_635_0.png)

我建议您在 Web 浏览器中打开 Webmin，并在“服务器”页面上查看 FTP 服务器模块。该模块将帮助您配置 FTP 服务器的各个方面。FTP 模块在每个页面上都包含一个帮助链接，该链接特定于该页面上的信息。浏览不同的图标并阅读帮助。

### 如何判断谁在访问我的 FTP 服务器？

如果已打开日志记录（请检查 Webmin FTP 服务器模块下的日志记录模块），则对 FTP 服务器的登录将被记录到 `/var/log/messages`。对于匿名用户，这将包括他们的“密码”，该密码应为电子邮件地址。您可以通过进入匿名 FTP 模块、将 FTP 密码检查设为 RFC822 并拒绝登录来强制执行此操作。这不会阻止任何人使用虚假的电子邮件地址，但会检查电子邮件地址是否符合 RFC822。

### 我有一个装满文件想上传的目录。我该怎么做？

最简单的方法是使用 FTP 客户端的多个 `put` 命令（`mput`）。通过使用 `*`，您可以指定所有文件。默认情况下，系统会提示您输入每个文件。如果您不想被提示，请在开始之前键入 `prompt` 关闭提示。登录并更改到上传目录后，您可能希望按顺序使用的命令如下：

```
binary

hash

prompt

mput *
```
