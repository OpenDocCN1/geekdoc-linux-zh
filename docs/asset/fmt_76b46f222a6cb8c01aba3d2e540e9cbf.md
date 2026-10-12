
或将其放入启动脚本中。类似地，在不存在`X`窗口系统的情况下，可以使用`ssh-agent`来调用`shell`，例如：

```
$ ssh-agent /bin/bash
```

在这两种情况下，通过`ssh-agent`调用您的会话将赋予您使用其功能的能力。

初始时，`agent`（守护进程）不持有任何密钥。为了向`agent`添加`用户密钥（User Keys）`，您需要使用`ssh-add`命令。在不带任何参数的情况下执行`ssh-add`会提示输入与调用用户相关的`口令短语（Passphrase）`。随后，它会将口令短语、`私钥`（Private User Key，存储于`$HOME/.ssh/identity`）以及`公钥`（Public User Key）传递给`ssh-agent`。示例 11-27 展示了`ssh-add`的执行过程。

### 示例 11-27 使用 ssh-add

```
$ ssh-add
Need passphrase for /home/mary/.ssh/identity (mary@roadrunner).
Enter passphrase:
Identity added: /home/mary/.ssh/identity (mary@roadrunner)
```

为了验证身份标识（实际上是用户密钥）已添加成功，我们可以使用`ssh-add -l`列出由`ssh-agent`维护的所有身份标识，如示例 11-28 所示。由于迄今为止只添加了一个，因此仅列出了一个条目。请注意，这里只显示了`公钥`。

### 示例 11-28 使用 ssh-add -l 列公钥

```
$ ssh-add -l
1024 35 155971740030589148116564771700556225351216129681204625440861171985785404328780148218606181339964509183365357756486802315214738633357473332241382028429363955986112247262292709855592609872044558116006382036446829938117899220034468062566418833671363 0151162868686560525258186487512130262828369447587841 mary@roadrunner$
```

`Agent`可以持有很多密钥。虽然它默认期望密钥位于`$HOME/.ssh/identity`和`$HOME/.ssh/identity.pub`，但可以通过将文件名作为参数传递给`ssh-add`来轻松覆盖这一行为。`ssh-add`的选项见表 11.11。

`Agent`持有密钥，直到其终止或被`ssh-add -d`或`ssh-add -D`告知删除为止。一旦`agent`获取了用户密钥，它将代替用户管理`RSA`认证对话，这样用户就不会被提示输入私钥口令短语。这被称为`agent 转发`。此外，它还建立必要的`X`认证信息并设置`DISPLAY`环境变量。此过程由`ssh`调用，如示例 11-29 所示。请注意，它会告知您正在为该会话生成`MIT-MAGIC-COOKIE`。这些`cookie`对`underdog`及其`IP`地址（在主机名解析失败的情况下）都有效。在此时，您调用的任何`X Window System`应用程序都会通过`SSH`加密隧道进行转发。

### 表 11.11 ssh-add 的选项

| 选项 | 描述 |
|:---|:---|
| `file` | 指定包含`私钥`的文件名称，替代默认的`$HOME/.ssh/identity`。 |
| `-P` | 指示从标准输入或管道读取口令短语。在脚本中很有用，但请注意不要在文件中存储口令短语。 |
| `-l` | 列出`agent`存储的所有密钥。 |
| `-d` | 从`agent`中删除与`$HOME/.ssh/identity`或指定`file`匹配的`用户密钥`。 |
| `-D` | 从`agent`中删除所有密钥。 |

### 示例 11-29 使用具有 Agent 转发的 ssh

```
[root@topcat .ssh]# ssh underdog
Last login: Fri Jul 2 15:04:57 1999 from pluto
Environment:
HOME=/root
USER=root
LOGNAME=root
PATH=/usr/bin:/bin:/usr/bin
MAIL=/var/spool/mail/root
SHELL=/bin/bash
SSH_CLIENT=10.13.33.111 1023 22
SSH_TTY=/dev/pts/5
TERM=xterm
DISPLAY=underdog:10.0
SSH_AUTH_SOCK=/tmp/ssh-root/ssh-2598-agent
Running /usr/X11R6/bin/xauth add underdog:10.0 MIT-MAGIC-COOKIE-1
57cb55807403833150e832e37c85dd9
Running /usr/X11R6/bin/xauth add 10.13.1.9:10.0 MIT-MAGIC-COOKIE-1
57cb55807403833150e832e37c85dd9
No mail.
[root@underdog]#
```

> **警告！**
>
> 如果手动将`DISPLAY`环境变量设置为其他值，随后调用的任何`X`应用程序将不会被加密。

`MIT-MAGIC-COOKIE`存储在用户主目录中的`.Xauthority`文件中。如果其他人获取了此文件的内容，他们就能利用该系统的显示设备，这可能导致进一步泄露敏感信息。因此，`.Xauthority`文件的权限应设置为`600` (`rw-------`)，并由该用户所有，即该文件出现在哪个用户的主目录下，就该由哪个用户拥有。

### 禁用 X 和 Agent 转发

如果在服务器的`/etc/ssh/ssh_config`中将`X11Forwarding`设置为`no`，和/或在正在使用的密钥的`/etc/ssh/authorized_keys`中设置`no-x11-forwarding`，那么此功能将被禁止。通过在`/etc/hosts.deny`中设置适当的条目（RPM 包编译时默认包含`libwrap`支持），也可以在服务器上禁用`X Window System`转发。`/etc/hosts.deny`中以下`sshd-wx11`条目将禁止`pluto`和`topcat`使用`X Window System`转发：

```
sshd-wx11: pluto, topcat
```

`Agent`转发——即使用`ssh-agent`——可以通过在`$HOME/.ssh/config`文件或`/etc/ssh/ssh_config`文件中的`ssh`命令行将`ForwardAgent`设置为`no`来在客户端关闭。也可以使用`ssh`的`-a`标志。

## 基于密码的认证

如果三种非密码认证方案都失败，`sshd`将提示用户输入其密码。密码将通过加密隧道传输，如果输入成功，`sshd`将为用户提供一个`shell`或执行用户指定的命令。默认情况下，用户名和服务器主机名会出现在密码提示中。您可以在`$HOME/.ssh/config`文件或`/etc/ssh/ssh_config`文件中的`ssh`命令行将`PasswordPromptLogin`和`PasswordPromptHost`关键字设置为`no`来禁用这些显示。您也可以通过在服务器上的`/etc/ssh/ssh_config`中将`PasswordAuthentication`设置为`no`来完全禁用密码认证。

## 使用 PAM 进一步限制访问

如果您配置`SSH`的服务端以验证传递的密码，您可以使用`pam_access`基于`/etc/security/access.conf`进一步限制登录。这是因为`pam_access`属于账户模块类型，而`SSH`支持该模块类型。由于`SSH`不支持`auth`模块类型，因此像`pam_listfile`这样的仅限`auth`的访问控制模块不可用。使用`pam_access`的详细信息见第 104 页的`使用 pam_access`。

请注意，如果非密码认证成功，通过`pam_access`施加的任何限制都将被忽略。

## 探索 SSH 功能

在本节中，我们将查看使用`ssh`和`scp`的各种示例。我们从类似于`rsh`和`rcp`用法的示例开始，然后过渡到端口转发。在所有示例中，我们假设所有服务器都正在运行`sshd`。认证将按前述方式进行，所有会话都是加密的。

### SSH 示例

`ssh`最简单的用途是登录到远程系统。这可以非常简单地通过以下方式完成：

```
$ ssh remote_host
```
