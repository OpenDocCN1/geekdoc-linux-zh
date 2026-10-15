
# 第 15 章 在网络上工作

已连接，包括它的名称、内核、日期时间以及你最后登录的时间。你现在可以在那台机器上运行任何你有权限运行的命令，就好像直接坐在它面前一样。从 `ssh` 和 `eliot` 的角度来看，你身处地球的任何地方都并不重要——你已经登录并准备就绪。

但是，如果这是你第一次连接到 `eliot`，你将看到一条不同的消息：

```bash
$ ssh tom@192.168.0.25

The authenticity of host '192.168.0.25'
→(192.168.0.25)' can't be established.

RSA key fingerprint is 54:53:c3:1c:9a:07:22:0c:82:
7b:38:53:21:23:ce:53.

Are you sure you want to continue connecting
→(yes/no)?
```

基本上，`ssh` 正在告诉你它不认识这台机器，并要求你验证该机器的身份。输入 `yes` 并按回车，你就会看到另一条消息以及密码提示符：

> Warning: Permanently added '192.168.0.25' (RSA)
> to the list of known hosts.
> tom@192.168.0.25's password:

从这里开始，一切恢复正常。你只有在第一次连接到 `eliot` 时才会看到此消息，因为 `ssh` 将它提到的 RSA 密钥指纹存储位于 `~/.ssh/known_hosts` 的文件中。查看该文件，你会发现里面增加了一行。根据你的 `/etc/ssh/ssh_config` 文件中是否启用了 `HashKnownHosts` 选项，该行会以两种格式之一出现。如果 `HashKnownHosts` 设置为 `no`，它看起来像这样：

```
192.168.0.25 ssh-rsa SkxPuQLYXZknsstN6b2HK5AmnC6E
- pg4psdnL69R5pHbQi3krWNNNNO3AmnP1p2rNNNOVJNN9mu5FZe
- 16zkKoIkIfJFbH/M9k0BnBXr6prfcXc09VBEAHIYteLMMYZLHB
- xSr6ehj/9FxFkCHYLDKFmfxafgaA60U2ZUXN5P6r4ctfqqAY69E
- 5cUD3xEj/gj2zv0bh630zehrgc=
```

你可以清楚地看到 IP 地址以及加密哈希，但与你开启 `HashKnownHosts` 后看到的相比，完全无法比拟：

```
NNNMO3AmnP1p2rNNNOVNNVRgajOx0T3GIh01PD6BIU1k
- At6nQJoJMVt2tbB5KIFL4ZDwbZZ/j/0zcCIQnPwDUF6YIku
- FCCegagldDB79Q5aoJ0JPL1inRzcQqP1Xfu6j1agFjzQJUY
- E+Lw8yjmPidCvU0CZ0LKH4hfqvkNEXqymmy6izb2wp?
```

一切都被哈希处理了，甚至是机器的 IP 地址或域名。从安全角度来看这是好事，但如果 `eliot` 上的操作系统发生变化就会成为问题。换句话说，如果你需要重装 `eliot` 上的 Linux，下次你从 `pound` 登录时将看到此警告：

> @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
> @ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! @
> @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
> IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY
> Someone could be eavesdropping on your right now
> (man-in-the-middle attack)!
> it is also possible that the RSA host key has just just
> - been changed.
> The fingerprint for the RSA key sent by the remote
> > host is
> 19:85:59:5c:6a:24:85:53:07:7a:dc:34:37:c6:72:1b.
> Please contact your system administrator.
> Add correct key in /home/pound/.ssh/
> - known_hosts to get rid of this message.

# 安全：登录另一台计算机

在 `/home/pound/.ssh/known_hosts` 中的冲突密钥：

```
nRSA host key for 192.168.0.125 has changed and you
have requested strict checking.
Host key verification failed.
```

问题在于，自从重装操作系统以来，`eliot` 的 `ssh` 密钥已经更改，当 `ssh` 检查 `eliot` 的密钥时，它在 `pound` 的 `known_hosts` 文件中存储的是新密钥，发现不匹配并向你发出警告。要修复这个问题，只需删除 `pound` 的 `known_hosts` 中对应 `eliot` 的那行，保存文件并重新连接。对于 `ssh` 来说，这是你第一次连接，因此它会询问你是否想要接受该密钥。说 `yes`，一切就正常了。

# 在机器之间安全地传输文件

从 `username ezra` 到 `eliot` (`192.168.0.25`; `username tom`)，你只需要使用此命令：

```bash
$ sftp tom@192.168.0.25

Connecting to 192.168.0.25...

tom@192.168.0.25's password:

sftp>
```

如果你读过之前的章节“无密码安全地登录到另一台机器”，你可能在奇怪为什么会提示你输入密码。你是正确的：之前的示例是在一个没有设置密码的连接之前完成的。在完成该操作后，你将看到类似所示的登录界面：

```bash
$ sftp tom@192.168.0.25

Connecting to 192.168.0.25...

sftp>
```

通过 `sftp` 登录后，你可以运行的命令非常标准。表 15.1 列出了一些常用命令；欲需完整列表，请查看 `man sftp`。

## 表 15.1 有用的 SFTP 命令

| 命令 | 含义 |
|---|---|
| `cd` | 切换目录 |
| `exit` | 关闭与远程 SSH 服务器的连接 |
| `get` | 将指定的文件复制到本地机器 |
| `help` | 获取命令帮助 |
| `lcd` | 切换本地机器的目录 |
| `lls` | 列出本地机器的文件 |
| `ls` | 列出远程 SSH 服务器工作目录下的文件 |
| `put` | 将指定的文件复制到远程 SSH 服务器 |
| `rm` | 从远程 SSH 服务器删除指定的文件 |

## 在主机之间安全地复制文件

如果你急于时间并且需要从一台机器安全地复制文件到另一台机器，那么 `scp`（安全复制）就是你需要的。本质上，使用 `scp` 的基本模式如下：

`scp user@host1:file1 user@host2:file2`

这与语法与老的 `cp` 基本相同，但现在扩展到了网络。一个示例会让情况变得更清晰。假设你想使用 `scp` 将 `pound` (`192.168.0.15`; `username ezra`) 的 `backup.sh` 复制到 `eliot` (`129.168.0.25`; `username tom`) 的 `/home/tom/bin`：

```bash
$ pwd

/home/ezra

$ ls ~/bin

backup.sh

$ scp ~/bin/backup.sh tom@192.168.0.25/home/tom/bin

backup.sh                   100% 8806      8.6KB/s      00:00

$
```

你没有被提示输入密码，是因为你早早在“无密码安全地登录到另一台机器”中设置了内容，因此 `ssh` 在从 `pound` 连接到 `eliot` 时不需要密码，而 `scp` 依赖于 `ssh`，所以在这里也不需要密码。如果你没有做过那样，在继续操作之前你会被要求输入 `tom` 的密码。

假设你有几个 JPEG 文件想从 `pound` 传输到 `eliot`。没问题——只需使用通配符即可：

```bash
$ ls -1 /covers

earth_wind_&fire.jpg

handel___chamber_music.jpg

smiths_best_1.jpg

strokes__is_this_it.jpg

u2_pop.jpg

$ scp *.jpg tom@192.168.0.25:/home/tom/album_covers
```
