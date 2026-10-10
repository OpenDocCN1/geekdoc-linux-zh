
#### `~/.ssh`：用户文件

当用户连接到远程系统时，OpenSSH 会自动创建 `~/.ssh` 目录及其中的 `known_hosts` 文件。

| 文件 | 用户 | 描述 |
| :--- | :--- | :--- |
| `authorized_keys` | 服务器 | 允许用户在不提供用户登录密码的情况下登录到另一系统或从另一系统复制文件（参见第 700 页）。不过，根据密钥的设置方式，用户可能需要提供口令短语。除所有者外，任何人都不得向此文件写入。 |
| `config` | 客户端 | 用户的私有 OpenSSH 配置文件（参见第 698 页）。这里的条目覆盖 `/etc/ssh/ssh_config` 中的条目。 |
| `environment` | 服务器 | 包含定义服务器环境变量定义的赋值语句，当用户使用 `ssh` 登录时生效。 |

## 更多信息

- 本地手册页：`ssh`、`scp`、`sftp`、`ssh-keygen`、`ssh_config`、`sshd`、`sshd_config`
- Web OpenSSH 主页：`www.openssh.com`
- 搜索 `ssh` 以查找各种 HOWTO 和其他文档：`tldp.org`
- 书籍《实现 SSH：优化安全 Shell 的策略》，作者 Dwid；John Wiley & Sons（2003 年 10 月）
- 书籍《SSH，安全 Shell：权威指南》，作者 Barrett、Silverman 和 Byrnes；O'Reilly Media（2005 年 5 月）

## 运行 `ssh`、`scp` 和 `sftp` OpenSSH 客户端

本节介绍如何设置和使用 `ssh`、`scp` 和 `sftp` 客户端。

### 先决条件

安装以下软件包（两者均默认安装）：

- `openssh`
- `openssh-clients`

OpenSSH 客户端不会运行守护进程，因此没有需要设置的服务。

### 快速入门 1：使用 `ssh` 和 `scp` 连接到 OpenSSH 服务器

除了安装必要的软件包外，`ssh` 和 `scp` 客户端不需要其他设置，尽管您可以创建和编辑文件以便于其使用。要在远程系统上运行安全 shell 或安全地复制文件，必须满足以下标准：远程系统必须正在运行 OpenSSH 守护进程（`sshd`），您必须拥有远程系统上的账户，并且服务器必须向客户端进行积极的身份验证。

以下示例展示了 Zach 如何使用 `ssh` 登录到名为 `plum` 的远程主机，运行 `who`，最后输入 `exit` 命令返回到本地系统的 shell。`who` 实用程序显示了 Zach 登录所从的系统的主机名。

```
[zach@guava ~]$ ssh zach@plum
zach@plum's password:
Last login: Wed Jun 12 16:34:10 2013 from guava
[zach@plum ~]$ who am i
zach     pts/1     2013-06-12 16:38 (guava)
[zach@plum ~]$ exit
logout
Connection to plum closed.
[zach@guava ~]$
```

如果您想以自身身份登录，并且在两个系统上拥有相同的用户名，则可以从命令行中省略 `user@`（`zach` 在前面的示例中）。首次连接到远程 OpenSSH 服务器时，`ssh` 或 `scp` 会要求您确认是否连接到了正确的系统。请参阅第 691 页的“首次身份验证”。

以下示例使用 `scp` 将本地系统工作目录中的 `ty1` 复制到 `plum` 上 Zach 的主目录：

```
$ scp ty1 zach@plum:
zach@plum's password:
ty1     100%  97kB   96.8kB/s   00:00
```

请记住在系统名称后加上冒号（`:`）。如果您省略冒号，`scp` 将在本地复制文件；在这种情况下，您最终会得到一个名为 `zach@plum` 的 `ty1` 副本。

### 配置 OpenSSH 客户端

本节描述如何在客户端端设置 OpenSSH。

#### 推荐设置

Fedora/RHEL 提供的配置文件建立了一个基本安全的系统，这可能符合也可能不符合您的需求。您可能想要更改的一个 OpenSSH 参数是 `ForwardX11Trusted`，它在 `/etc/ssh/ssh_config` 配置文件（第 698 页）中设置为 `yes`。为了提高安全性，并在某些情况下降低易用性，请将 `ForwardX11Trusted` 设置为 `no`。有关 X11 转发的更多信息，请参见第 707 页。

#### 服务器身份验证/已知主机

两个文件列出了本地系统曾连接并成功识别的主机：`~/.ssh/known_hosts`（用户级）和 `/etc/ssh/ssh_known_hosts`（全局级）。除了所有者（第二个文件为 `root`）之外，任何人都不应能够写入这两个文件中的任何一个。除了所有者之外，任何人都不应访问 `~/.ssh` 目录。

**首次身份验证** 当您第一次连接到 OpenSSH 服务器时，OpenSSH 客户端会提示您确认是否连接到了正确的系统。此行为由 `StrictHostKeyChecking`（第 699 页）控制。此检查有助于防止中间人攻击（第 1160 页）：

```
The authenticity of host 'plum (192.168.206.181)' can't be established.
RSA key fingerprint is d1:9d:1b:5b:97:5c:80:8e:4b:41:9a:b7:bc:1a:ae:a1.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'plum,192.168.206.181' (RSA) to the list of
known hosts.
```

在响应上述查询之前，请确保您正在登录到正确的系统，而不是冒充者。如果您不确定，给在该系统本地登录的人员打个电话可以帮助验证您是否在预期的系统上。当您回答 `yes`（必须拼写完整）时，客户端会将服务器的公开主机密钥（服务器上 `/etc/ssh/ssh_host_rsa_key.pub` 或 `/etc/ssh/ssh_host_dsa_key.pub` 文件中的单行）追加到本地系统上用户的 `~/.ssh/known_hosts` 文件，必要时创建 `~/.ssh` 目录。为了跟踪 `known_hosts` 中的哪一行适用于哪个服务器，OpenSSH 会在该行前加上服务器名称和服务器 IP 地址。

随后当您使用 OpenSSH 连接到该服务器时，客户端将此密钥与服务器提供的密钥进行比较，以验证是否连接到了正确的服务器。

**known_hosts** `~/.ssh/known_hosts` 文件使用一或两个非常长的行来标识它跟踪的每个主机。每行以该系统对应的主机名和 IP 地址开头，随后是使用的加密类型和服务器的公开主机密钥。当 `HashKnownHosts`（第 699 页）设置为 `yes`（默认为 `no`）时，OpenSSH 会对系统名称和地址进行哈希处理以提高安全性。由于 `HashKnownHosts` 分别对主机名和 IP 地址进行哈希处理，OpenSSH 会在 `known_hosts` 中为每个主机放置两行。以下行（这是一个逻辑行，但在物理上换行显示）来自 `known_hosts`，用于使用 RSA（第 1271 页）加密连接到 `192.168.206.181` 上的 `plum`：

```
$ cat ~/.ssh/known_hosts
plum,192.168.206.181 ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDhblRVTfi
v9gy7oP+5T3HjZmrKt2q6dyKmL1HNuJZFXMH4CdKj3TpTFj4wy260UAZBwvRlBPG9k
...
```

您可以使用带有 `–R` 选项后跟主机名的 `ssh-keygen` 来删除条目，即使是经过哈希处理的条目也可以。或者，您可以使用文本编辑器来删除条目。`ssh-keygen` 的 `–F` 选项会显示 `known_hosts` 文件中与指定系统对应的行，即使该条目是经过哈希处理的：

```
$ ssh-keygen -F plum
# Host plum found: line 1 type RSA
plum ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDhblRVTfi9vy7oP+5T3HjZmr
Kt2q6dyKmL1HNuJZFXMH4CdKj3TpTFj4wy260UAZBwvRlBPG9kYA+KRClGfywROUwxQ
...
```

![](img/243613168ac865b539f12460d966088e_748_0.png)

OpenSSH 会自动将其连接过的服务器的密钥存储在用户私有文件中（`~/.ssh/known_hosts`）。这些文件仅适用于其所在目录的用户。以 `root` 权限运行并使用文本编辑器，您可以将非哈希行从用户的私有已知主机列表复制到 `/etc/ssh/ssh_known_hosts` 中的公共列表，以便在本地系统上全局识别服务器。

以下示例展示了 Sam 如何将 `known_hosts` 文件中的哈希条目放入全局 `ssh_known_hosts` 文件。首先，以他自己身份操作，Sam 将 `ssh-keygen` 的输出通过 `tail` 去除 "Host plum found" 行，并将输出重定向到主目录中名为 `tmp_known_hosts` 的文件。接下来，以 `root` 权限操作，Sam 将他刚创建的文件内容追加到 `/etc/ssh/ssh_known_hosts`。如果此文件不存在，该命令会创建它。最后，Sam 返回到自己身份操作并删除他创建的临时文件。

```bash
$ ssh-keygen -F plum | tail -1 > ~/tmp_known_hosts
$ su
Password:
# cat ~/tmp_known_hosts >> /etc/ssh/ssh_known_hosts
# exit
$ rm ~/tmp_known_hosts
```

如果在远程系统的公钥存储在已知主机文件之一中之后，远程系统在系统连接时提供了不同的指纹，OpenSSH 将显示以下消息并不完成连接：

```
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@       WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the RSA host key has just been changed.
The fingerprint for the RSA key sent by the remote host is:
f1:6f:ea:87:bd:1b:df:cd:e3:45:24:60:d3:25:b1:0a.
Please contact your system administrator.
Add correct host key in /home/sam/.ssh/known_hosts to get rid of this message.
Offending key in /home/sam/.ssh/known_hosts:1
RSA host key for plum has changed and you have requested strict checking.
Host key verification failed.
```

如果您看到此消息，您可能正在遭受中间人攻击。然而，更有可能的是，远程系统中的某些东西发生了变化，导致其提供新的指纹。请与远程系统的管理员联系。如果一切正常，请从指定文件中删除违规密钥（上述消息中倒数第三行指向您需要删除的行）并再次尝试连接。您可以使用带有 `-R` 选项后跟主机名的 `ssh-keygen` 来删除哈希条目。OpenSSH 将验证您是否连接到正确的系统，因此您将再次经历首次身份验证（第 691 页）。请遵循初始连接到远程主机时的相同步骤。

## `ssh`：登录远程系统或在其上执行命令

`ssh` 命令行的格式如下：

```
ssh [options] [user@]host [command]
```

其中，`host` 是你想要连接的 OpenSSH 服务器（即远程系统）的名称，它是唯一必需的参数。`host` 可以是本地系统名称、互联网上某系统的全限定域名（FQDN，见第 1250 页）或 IP 地址。

使用命令 `ssh host`，你可以使用与本地系统相同的用户名登录到远程系统 `host`。远程系统会显示 shell 提示符，你可以在 `host` 上运行命令。输入命令 `exit` 以关闭与 `host` 的连接并返回到本地系统的提示符。当你希望使用与本地系统不同的用户名登录时，请包含 `user@`。根据服务器的配置情况，你可能需要提供在远程系统上使用的密码。

当包含 `command` 时，`ssh` 会登录到 `host`，执行 `command`，关闭与 `host` 的连接，并将控制权返回给本地系统。远程系统永远不会显示 shell 提示符。

在下面的示例中，登录在 `guava` 上的 Sam 使用 `ssh` 登录到 `plum`，输入显示系统名称和类型的 `uname` 命令，并使用 `exit` 关闭与 `plum` 的连接并返回到本地系统的提示符：

```
[sam@guava ~]$ ssh plum
sam@plum's password:
Last login: Wed Jun 12 16:55:47 2013 from guava
[sam@plum ~]$ uname -nm
plum x86_64
[sam@plum ~]$ exit
logout
Connection to plum closed.
[sam@guava ~]$  
```

以下示例使用 `ls` 显示远程系统 `plum` 上 `memos` 目录中的文件列表。该示例假设运行命令的用户（Sam）在 `plum` 上有登录权限，且 `memos` 目录位于 Sam 在 `plum` 上的主目录中：

```
$ ssh plum ls memos
sam@plum's password:
memo_0921
memo_draft
$ 
```

当你运行 `ssh` 时，在远程系统上运行的命令的标准输出会被传递给本地 shell，就像该命令在本地系统上运行一样。与所有 shell 命令一样，你必须对不希望本地 shell 解释的特殊字符进行引号转义。

在下一个示例中，在远程系统上运行的 `ls` 命令的标准输出被发送到本地系统的 `ls.out` 文件。

```
$ ssh plum ls memos > ls.out
sam@plum's password:
$ cat ls.out
memo_0921
memo_draft
```

在前面的 `ssh` 命令中，重定向符号（`>`）没有加引号，因此它由本地 shell 解释，并在本地系统上创建 `ls.out` 文件。下一条命令类似，但重定向符号加了引号，因此本地 shell 不会解释它，而是将其传递给远程 shell。第一条命令在远程系统上创建 `ls.out2` 文件，第二条命令显示该文件。

```
$ ssh plum 'ls memos > ls.out2'
sam@plum's password:
$ ssh plum cat ls.out2
sam@plum's password:
memo_0921
memo_draft
```

对于下一个示例，假设本地系统的工作目录中有一个名为 `memo.new` 的文件。你不记得这个文件是否包含某些更改，或者你是否在 `plum` 上的 `memos` 目录中的文件 `memo.draft` 上做了这些更改。你可以将 `memo.draft` 复制到本地系统，并对两个文件运行 `diff`（见第 227 页），但这样你会在两个系统之间分散三个类似的文件副本。如果在完成后不仔细删除旧副本，你几天后可能又会感到困惑。你可以使用 `ssh` 代替复制文件。这个示例表明两个文件之间只有日期行不同：

```
$ ssh plum cat memos/memo.draft | diff memo.new -
sam@plum's password:
1c1
< Wed Jun 14 12:22:14 PDT 2013
---
> Wed Jun 12 17:05:51 PDT 2013
```

在前面的示例中，`plum` 上 `cat` 命令的输出通过本地系统上的管道发送到在本地系统上运行的 `diff`，它将本地文件 `memo.new` 与标准输入（`-`）进行比较。以下命令行具有相同的效果，但会导致 `diff` 在远程系统上运行：

```
$ cat memo.new | ssh plum diff - memos/memo.draft
sam@plum's password:
1c1
< Wed Jun 14 12:22:14 PDT 2013
---
> Wed Jun 12 17:05:51 PDT 2013
```

远程系统上 `diff` 的标准输出被发送到本地 shell，并在屏幕上显示出来（因为它没有被重定向）。

## 选项

本节描述了你可以与 `ssh` 一起使用的一些选项。

- `-C`（压缩）：启用压缩（见第 710 页）。在 ssh 的商业版本中，`-C` 禁用压缩，而 `+C` 启用压缩。
- `-f`（非前台）：在询问密码后、执行命令前将 ssh 发送到后台。当你希望在后台运行命令但必须提供密码时很有用。隐含 `-n`。
