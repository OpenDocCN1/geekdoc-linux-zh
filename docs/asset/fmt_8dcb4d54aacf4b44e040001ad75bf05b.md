
将创建新用户（`newuser`），其主目录将设置为 `/www/newuser`。请注意，`useradd` 将仅创建最后一级目录，而不会创建整个路径。例如，如果您将 `-d /some/new/dir/myuser` 指定为选项，只有当 `/some/new/dir` 已经存在时，`useradd` 才会创建 `myuser`。

创建新主目录时，`/etc/skel` 目录中包含的文件将被复制到新主目录中。这些文件通常是默认 shell 的点配置文件。例如，如果默认 shell 是 `/bin/bash`，您应该在 `/etc/skel` 目录中拥有 `.bashrc`、`.bash_profile` 和 `.bash_login` 的默认版本，以便新用户的主目录可以自动设置这些文件。

Red Hat Linux 自带的 `useradd` 会为用户创建一个与用户名同名的私有组。例如，如果您运行 `useradd kabir`，一个名为 `kabir` 的新用户将在 `/etc/passwd` 文件中创建，一个名为 `kabir` 的新组将在 `/etc/group` 文件中创建。这种方法使新用户完全与其他用户隔离，从而确保用户更高的隐私。每当新用户创建新文件时，凭借这个私有组，该文件仅可由新用户访问。用户必须显式更改文件权限，才能允许其他人查看该文件。

但是，如果您的用户帐户与这种私有组的想法冲突，您可以使用 `-g group` 选项覆盖它（其中 `group` 是您的组名）。例如，

```
useradd mjkabir -g users
```

使 `useradd` 创建新用户 (`mjkabir`)，并将默认组设置为 `users`。

如果您想让新用户成为系统上其他组的成员，请使用 `-G comma-separated list of groups` 选项。例如，

```
useradd mjkabir -G wheel,admins
```

将新用户 (`mjkabir`) 添加到 `/etc/group` 文件中的 `wheel` 和 `admins` 组。

## userdel

要删除现有用户，请使用 `userdel` 命令。例如，以下命令删除名为 `snake` 的用户：

```
userdel snake
```

如果您想删除用户的主目录及其所有内容，请使用 `-r` 选项。请注意，如果用户当前已登录，`userdel` 将不会删除该用户。通过发送 `write` 消息（`write username`）要求用户注销，如果无法要求，请使用 `killall` 命令终止与该用户关联的所有进程，然后运行 `userdel` 命令。

要暂时禁用用户帐户，请执行以下操作之一：

- 使用 `usermod -s new shell username` 命令将 shell 更改为 `/bin/false`（确保新 shell 列在 `/etc/shells` 文件中）。这将禁止用户登录系统。
- 如果您使用影子密码，请使用 `usermod -e MM/DD/YY username` 命令导致用户帐户过期。

要暂时禁用所有用户帐户访问，请创建一个名为 `/etc/nologin` 的文件，其中包含一条解释为何不允许访问的消息。只要此文件存在，登录程序将不允许任何非 root 帐户登录。

## usermod

`usermod` 命令用于修改用户帐户。要更改现有用户的主目录，请按如下方式运行 `usermod` 命令：

```
usermod -d new_home_directory username
```

其中 `new_home_directory` 和 `username` 是正确的值。

例如，如果名为 `keller` 的用户将 `/home/keller` 作为其主目录，而您想将其移至 `/home2/keller`，请按如下方式运行 `usermod` 命令：

```
usermod -d /home2/keller keller
```

这将设置新目录作为其主目录。但是，如果您想将其主目录的内容移动到新位置，请使用 `-m` 选项，如下所示：

```
usermod -d -m /home2/keller keller
```

要更改用户的 UID，请按如下方式使用 `usermod` 命令：

```
usermod -u UID username
```

其中 `UID` 和 `username` 是正确的值。

例如，以下命令将用户 `mrfrog` 的 UID 更改为 500：

```
usermod -u 500 mrfrog
```

用户在其主目录中拥有的所有文件和目录将自动反映 UID 的更改。但是，如果用户在其主目录之外拥有文件，您将不得不使用 `chown` 命令手动更改所有权。

## usermod

要更改用户的默认组，请按如下方式使用 `usermod` 命令：

```
usermod -g group name or GID username
```

其中，`group name` 或 `GID` 以及 `username` 均为正确的值。

例如，以下命令将用户 `myfrog` 的默认组更改为 777：

```
usermod -g 777 myfrog
```

如果您使用的是影子密码，可以按如下方式使用 `usermod` 命令更改用户账户的过期日期：

```
usermod -e MM/DD/YY username
```

其中，`MM/DD/YY` 和 `username` 均为正确的值。

例如，以下命令将用户 `kabir` 的账户过期日期重置为 12/31/01：

```
usermod -e 12/31/01 kabir
```

## who

语法： `who`

`who` 命令显示当前登录到系统的用户信息。您也可以使用 `w` 命令达到相同目的。

## whoami

语法： `whoami`

此命令显示您当前的用户名。

## 用于访问网络服务的用户命令

本节讨论的命令可让您访问各种网络服务。

### finger

语法： `finger user@host`

该程序允许您查询指定主机上的 finger 守护进程。例如，

```
finger kabir@blackhole.integrationlogic.com
```

请求连接到在 `blackhole.integrationlogic.com` 服务器上运行的 finger 守护进程。如果指定的主机不允许 finger 连接，此尝试将失败。成功时，finger 请求会显示有关指定用户的信息。如果用户主目录下有 `.plan` 文件，大多数传统的 finger 守护进程也会显示该文件。由于 finger 曾被用于制造安全问题，大多数系统管理员会在其域外禁用 finger 服务。

### ftp

语法： `ftp ftp hostname or IP address`

这是默认的 FTP 客户端程序。您可以使用此程序连接到 FTP 服务器。例如，

```
ftp ftp.cdrom.com
```

将打开到 `ftp.cdrom.com` 的 FTP 连接，并提示您输入用户名和密码。如果您知道用户名和密码，便可登录 FTP 服务器并上传或下载文件。进入 FTP 提示符后，您可以输入 `help` 或 `?` 以获取 FTP 命令的帮助。

### lynx

语法： `lynx [-dump] [-head] [URL]`

`lynx` 是最流行的基于文本的 Web 浏览器。要运行浏览器，只需将所需的 URL 作为命令行参数输入。例如，`lynx http://www.integrationlogic.com/` 将显示该站点的首页。`lynx` 是一个非常实用的程序。例如，若想在不询问网站管理员的情况下快速了解站点使用何种 Web 服务器，请运行以下命令：

```
lynx -head http://www.integrationlogic.com/
```

前述命令显示 `lynx` 浏览器从 Web 服务器接收到的 HTTP 头部。其输出示例如下：

```
HTTP/1.1 302 Moved
Date: Tue, 05 Dec 2000 06:47:27 GMT
Server: Apache/1.3.3 (Unix)
Location: http://www.integrationlogic.com/index.html
Connection: close
Content-Type: text/html
```

此头部显示 `www.integrationlogic.com` 运行在 UNIX 平台上的 Apache 1.3.3 Web 服务器。请注意，并非所有网站都会透露其 Web 服务器平台信息，但大多数会。如果您想避免交互模式，可使用 `-dump` 选项将页面转储到屏幕 (STDOUT)。例如，

```
lynx -dump -head http://www.integrationlogic.com/
```

将头部转储到 STDOUT。`-dump` 功能非常方便。例如，

```
lynx -dump -head http://webserver/new.gif > new.gif
```
