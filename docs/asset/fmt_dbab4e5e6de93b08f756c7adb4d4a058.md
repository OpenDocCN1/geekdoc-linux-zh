
如果您希望以当前用户身份登录，且在两个系统中用户名相同，则可以从命令中省略 `user@host`（前例中的 `zach@grape`）。首次连接到远程 OpenSSH 服务器时，`ssh` 或 `scp` 会提示您确认是否连接到正确的系统。参见第 `626` 页的“首次身份验证”。

以下示例将本地系统工作目录中的 `ty1` 复制到 `grape` 上的 Zach 的主目录。尾部的冒号至关重要；没有它，您将进行的是文件的本地复制。

```
$ scp ty1 zach@grape:
  zach@grape's password:
  ty1  100%  |************************************| 1311  00:00
```

# 设置

本节描述如何在客户端侧设置 OpenSSH。

## 推荐设置

`X11` 转发 Fedora/RHEL 提供的配置文件建立了一个相对安全的系统，但不一定满足您的需求。Fedora/RHEL 配置文件覆盖的重要 OpenSSH 默认值是 `ForwardX11Trusted`，在 Fedora/RHEL 的 `/etc/ssh/ssh_config` 配置文件中设置为 `yes`（第 `637` 页）。有关 X11 转发的更多信息，请参见第 `638` 页。

## 服务器身份验证/已知主机

`known_hosts`, `ssh_known_hosts` 两个文件列出了本地系统连接过并成功标识的主机：`~/.ssh/known_hosts`（用户）和 `/etc/ssh/ssh_known_hosts`（全局）。除所有者外（第二个文件的 owner 为 root），任何人都不应能写入这两个文件。除所有者外，任何人都不应有权访问 `~/.ssh` 目录。

**首次身份验证** 当您首次连接到 OpenSSH 服务器时，OpenSSH 客户端会提示您确认是否连接到正确的系统。此检查有助于防止中间人攻击（第 `1048` 页脚注 `3`）：

```
The authenticity of host 'grape (192.168.0.3)' can't be established.
RSA key fingerprint is c9:03:c1:9d:cc:29:55:50:e8:19:2b:eb:36:ef:73:78.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'grape,192.168.0.3' (RSA) to the list of known hosts.
```

在响应上述查询之前，请确保您登录的是正确的系统，而不是假冒系统。如果您不确定，给在该系统上本地登录的人打个电话可以帮助验证您是否在预期的系统上。当您回答 `yes`（必须拼写完整）时，客户端会将服务器的公钥主机密钥（服务器上的 `/etc/ssh/ssh_host_rsa_key.pub` 或 `/etc/ssh/ssh_host_dsa_key.pub` 文件中的单行）追加到本地客户端用户目录下的 `~/.ssh/known_hosts` 文件中，如有必要则创建 `~/.ssh` 目录。为了跟踪 `known_hosts` 中哪一行适用于哪个服务器，OpenSSH 会在该行前面加上服务器名称和服务器 IP 地址（默认情况下）。

当您随后使用 OpenSSH 连接到该服务器时，客户端会将此密钥与服务器提供的密钥进行比较，以验证是否连接到正确的服务器。

**known_hosts 文件** `known_hosts` 文件使用一行非常长的字符串来标识其跟踪的每个主机。每行以该行之对应的系统的主机名和 IP 地址开始，后跟使用的加密类型和服务器的公钥主机密钥。以下来自 `known_hosts` 的行（这是一行逻辑行，换行为四行物理行）用于使用 RSA（第 `1104` 页）加密连接到位于 `192.168.0.3` 的 `grape`：

```
$ cat ~/.ssh/known_hosts
grape,192.168.0.3 ssh-rsa AAAAB3NzaC1yc2EAAAABiwaAAIEAiRnPgSaLUsn5L4v7b
T5IksF7Ko5csIkk7wqm+2sJE4C3xrvXN5+M0/064Uxp5qQ0HBMeLCCFsCtjs13g8sxeuVkg91w0
BKKQd1ZdBNVqF5Z7enJ0bQTFF+oFTPIDI1p8w6fTHQdM8hZ//dIqq5gxq0Mh+Mpac3IpQXAXxgY
SP8nYGb3Xl8=
```

OpenSSH 会自动将其连接过的服务器的密钥存储在用户私有文件中（`~/.ssh/known_hosts`）。这些文件仅对该用户有效，即位于该用户目录中的文件。以 root 身份工作并使用文本编辑器，您可以将用户私有已知主机列表中的行复制到 `/etc/ssh/ssh_known_hosts` 中的公共列表，从而在本地系统中全局识别该服务器。更多信息请参阅 `sshd` man 手册页并搜索 `KNOWN`。

如果在远程系统的公钥存储在一个已知主机文件中后，当系统连接时远程系统提供了不同的指纹，OpenSSH 会显示以下消息并不完成连接：

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!    @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is:
  16:6f:ea:87:bb:1b:df:cd:e3:45:2d:60:d3:25:b1:0a.
Please contact your system administrator.
Add correct host key in /home/sam/.ssh/known_hosts to get rid of this message.
Offending key in /home/sam/.ssh/known_hosts:1
RSA host key for grape has changed and you have requested strict checking.
Host key verification failed.
```

如果您看到此消息，您可能正在遭受中间人攻击。不过，更可能的情况是远程系统上的某些内容发生了变化，导致其提供新的指纹。请与远程系统管理员联系。如果一切正常，请从指定文件中删除有问题的密钥（前例中倒数第三行指向您需要删除的行）并尝试再次连接。OpenSSH 验证您是否连接到正确的系统时，您会再次看到首次身份验证（第 `626` 页）。按照最初连接远程主机时的相同步骤操作。

# ssh：连接远程系统或在远程系统上执行命令

`ssh` 命令行的格式为

```
$ssh [选项] [用户@]主机 [命令]
```

其中，`host`（您想要连接的 OpenSSH 服务器名称）是唯一必需的参数。`host` 可以是本地系统名称、互联网系统的 FQDN 或 IP 地址。输入命令 `ssh host` 以登录到远程

使用与本地系统相同的用户名的 `host` 系统。如果你希望使用与本地系统不同的用户名登录，请在用户名前加上 `user@`。根据具体配置情况，你可能需要提供密码。

如果不指定 `command`，`ssh` 会登录到 `host`。远程系统会显示 shell 提示符\，你可以在 `host` 上运行命令。输入 `exit` 命令即可关闭与 `host` 的连接并返回到本地系统的提示符：

```
[bravo]$ ssh speedy
alex@speedy's password:
Last login: Sat Sep 16 06:51:59 from bravo
Have a lot of fun...
You have new mail.
[speedy]$
...
[speedy]$ exit
Connection to speedy closed.
[bravo]$
```

当你包含 `command` 时，`ssh` 会登录到 `host`，执行 `command`，关闭与 `host` 的连接，并将控制权交回给本地系统。远程系统永远不会显示提示符。

以下示例在远程系统 `speedy` 的 `memos` 目录中运行 `ls`。该示例假设运行该命令的用户（Alex）在 `speedy` 上有一个登录账户，且 `memos` 目录位于 Alex 在 `speedy` 上的主目录中：
