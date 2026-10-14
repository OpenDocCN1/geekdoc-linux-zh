
```
debug: got SSH2_MSG_SERVICE_ACCEPT
debug: authentications that can continue: publickey,password,keyboard-interactive
debug: next auth method to try is pubkey
debug: userauth pubkey: trying agent /home/gamerler/.ssh/id_rsa
debug: ssh-userauth success:method pubkey
debug: channel 0: new [client-session]
debug: send open
debug: Entering session.
debug: client_init id 0
debug: channel request 0: shell
debug: channel 0: open max 16384
Last login: Tue Mar 19 08:51:48 2002 from Sun Microsystems Inc. SunOS 5.8 February 2000 Sun Microsystems Inc. SunOS 5.8 February 2000

Agent pid 16936 [cardinal.com:/home/gamerler]
$ exit
Exiting
Killing SSH Agent
Agent pid 16936
debug: channel 0: rcvd request for exit-status
debug: cb_event 91
debug: channel 0: rcvd eof
debug: channel 0: output open->drain
debug: channel 0: rcvd close
debug: channel 0: input open->closed
debug: channel 0: ob empty
debug: channel 0: output drain->closed
debug: channel 0: close_write
debug: channel 0: send close
debug: channel 0: full closed
debug: channel_free: status: The following connections are open: client-session (exit -1)
```

```
Connection to cardinal closed.
debug: Transferred: stdin 0, stdout 0, stderr 32 bytes in 5.5
debug: Bytes per second: stdin 0.0, stdout 0.0, stderr 5.9
debug: Exit status -1
$
```

## 环境变量

`ssh` 通常设置以下环境变量。

```
DISPLAY 变量指示 X11 服务器的位置。它由 ssh 自动设置，指向格式为 hostname:n 的值，其中 hostname 表示运行 shell 的主机，而 n 是大于或等于 1 的整数。ssh 使用此特殊值通过安全通道转发 X11 连接。用户通常应该显式设置 DISPLAY，因为这样做会使 X11 连接变得不安全（并且需要用户手动复制任何授权 cookie）。
```

### ssh 1325

- `HOME` 设置为用户主目录路径。
- `LOGNAME` `USER` 的同义词。用于与使用该变量的系统兼容。
- `MAIL` 设置为用户的邮箱。
- `PATH` 设置为编译 `ssh` 时指定的默认 `PATH`。
- `SSH_AUTH_SOCK` 用于与代理通信的 UNIX 套接字路径。
- `SSH_CLIENT` 连接的客户端。该变量包含三个空格分隔的值：客户端 IP 地址、客户端端口号和服务器端口号。
- `SSH_TTY` 设置与当前 shell 或命令关联的 TTY（设备路径）。如果当前话没有 TTY，则不设置此变量。
- `TZ` 如果守护进程启动时设置了时区，则守护进程会将该值传递给新连接。
- `USER` 设置为登录的用户名。

此外，`ssh` 读取 `$HOME/.ssh/environment` 并将格式为 `VARNAME=value` 的行添加到环境变量中。

## 退出状态

- `0` 完成。
- `1` 发生错误。

## 文件

- `$HOME/.ssh/known_hosts` 记录用户登录过且不在 `/etc/ssh/known_hosts` 中的所有主机的密钥。参见 `sshd(1M)`。
- `$HOME/.ssh/identity` `$HOME/.ssh/id_rsa` 包含用户的 RSA 和 DSA 认证身份。这些文件包含敏感数据，应由用户读取但其他人不可访问（读/写/执行）。注意，如果私钥文件可被其他人访问，`ssh` 将忽略该文件。在生成密钥时可以指定密码文件。密码被用于用 3DES 加密此文件的敏感部分。

### 1326

`$HOME/.ssh/identity.pub`

`$HOME/.ssh/id_rsa.pub`

包含用于认证的公钥，即身份文件以可读格式表示的公部分。对于您想要使用 RSA 认证登录的所有机器，应将 `$HOME/.ssh/identity.pub` 文件的内容添加到这些机器的 `$HOME/.ssh/authorized_keys` 中。对于您想要使用 DSA 认证登录的所有机器，应将所有机器上 `$HOME/.ssh/authorized_keys` 的内容添加到这些机器的 `$HOME/.ssh/authorized_keys` 中。这些文件并不敏感，且**不能**被任何人读取。这些文件永远不会被自动使用，也不是必要的。提供它们仅是为了方便用户。

`$HOME/.ssh/config`

每个用户配置文件。该文件的格式见上文描述。此文件由 `ssh` 客户端使用。此文件通常不包含任何敏感信息，但建议的权限为用户读/写，其他人不可访问。

`$HOME/.ssh/authorized_keys`

列出可以用于此用户登录的 DSA 密钥。该文件并非高度敏感，但建议的权限为用户读/写，其他人不可访问。

`/etc/ssh/ssh_known_hosts`

系统级已知主机列表，`/etc/ssh/ssh_known_hosts` 包含 RSA 密钥。该文件应由系统管理员准备，包含组织内所有机器的公主机密钥，并应该是所有人可读的。该文件包含公钥，每行一个，格式如下，字段由空格分隔：系统名称、位数、指数、模以及可选的注释字段。当同一台机器使用不同名称时，应列出这些名称并用逗号分隔。参见 `ssh`。

`sshd` 在登录时使用规范的系统名称（由名称服务器返回）来验证客户端主机。之所以需要其他名称，是因为 `ssh` 在检查密钥之前，不会将用户提供的名称转换为规范名称，以防止某些能够访问名称服务器的人欺骗主机认证。

`/etc/ssh/ssh_config`

系统级配置文件。该文件为用户配置文件中未指定的值以及那些没有配置文件的用户提供了默认值。该文件 必须对所有人可读。

# ssh

## 1327

```
$HOME/.rhosts
```

此文件用于 `.rhosts` 认证，列出允许登录的主机/用户对。（注意，此文件也被 `.login` 和 `rsh` 使用，这使得该文件变得不安全。）文件的每行包含一个主机名（名称服务器返回的规范形式）和该主机上的用户名，中间用空格分隔。在某些机器上，如果用户的家目录在 NFS 分区上，则此文件可能需要对所有人可读，因为 `sshd()` 以 root 身份读取它。此外，此文件必须由用户所有，且不能给任何其他人写写权限。大多数机器建议的权限为用户读/写，其他人不可访问。

请注意，默认情况下，`ssh(IM)` 的安装方式要求在允许 `.rhosts` 认证之前必须已成功通过 RSA 认证。如果您的服务器在 `/etc/ssh_known_hosts` 中没有客户端的主机密钥，您可以将其存储在 `$HOME/.ssh/known_hosts` 中。最简单的方法是从服务器机器通过 `ssh` 重新连接客户端，以自动将主机密钥添加到 `$HOME/.ssh/known_hosts` 中。

```
$HOME/.shosts
```

使用方法与 `.rhosts` 完全相同。此文件允许使用 `ssh` 进行用户认证，但不允许允许通过 `login(1)` 或 `rsh(1)` 登录。

```
/etc/hosts.equiv
```

在 `.rhosts` 认证期间使用。该文件包含规范的主机名，每行一个。（参见 `sshd(IM)` 获取完整的格式描述。）如果在该文件中找到客户端主机，则只要客户端和服务器的用户名相同，就会自动允许登录。此外，通常需要成功的 RSA 主机认证。此文件应允许 root 写入。

```
/etc/ssh/shosts
```

此文件中的命令会在用户登录时，在用户的 shell 或命令启动之前由 `ssh` 执行。欲需更多信息请参见 `sshd(IM)`。

```
$HOME/.ssh/rc
```
