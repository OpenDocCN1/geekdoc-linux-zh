
如果你需要更改密码口令，可以使用`ssh-keygen`命令和`-p`选项来实现。每个用户将有自己的SSH配置目录，称为`.ssh`，位于其主目录下。公钥、私钥以及SSH配置文件都放在这里。从源代码来看，如果你对其进行编译，`make install`操作将自动运行`ssh-keygen`。表 19-3 列出了SSH配置文件。

| 文件 | 描述 |
| :--- | :--- |
| `$HOME/.ssh/known_hosts` | 记录所有登录过的主机（那些不在`/etc/ssh/ssh_known_hosts`中的）的密钥。 |
| `$HOME/.ssh/random_seed` | 随机数生成器的种子。 |
| `$HOME/.ssh/id_rsa` | 包含用户的RSA认证身份。 |
| `$HOME/.ssh/id_dsa` | 包含用户的DSA认证身份。 |
| `$HOME/.ssh/id_rsa.pub` | 包含认证的RSA公钥。此文件的内容应被添加到所有你想使用RSA认证登录的机器的`$HOME/.ssh/authorized_keys`中。 |
| `$HOME/.ssh/id_dsa.pub` | 包含认证的DSA公钥。此文件的内容应被添加到所有你想使用DSA认证登录的机器的`$HOME/.ssh/authorized_keys`中。 |
| `$HOME/.ssh/config` | 用户的配置文件。 |
| `$HOME/.ssh/authorized_keys` | 列出可以用于登录此用户的RSA或DSA密钥。 |
| `/etc/ssh/ssh_known_hosts` | 包含系统级的已知主机密钥列表。 |
| `/etc/ssh/ssh_config` | 包含系统级配置文件。该文件为用户配置文件中未指定的值提供了默认值。 |
| `/etc/ssh/sshd_config` | 包含SSH服务器配置文件。 |
| `/etc/ssh/shrc` | 包含系统默认。当用户登录时，`ssh`会执行此文件中的命令，在用户其shell（或命令）启动之前执行。 |
| `$HOME/.ssh/rc` | 包含用户登录时由`ssh`执行的命令，在用户其shell（或命令）启动之前执行。 |

**表 19-3 SSH 配置文件**

# 第 19 章：Secure Shell 与 Kerberos 365

## 授权密钥 (Authorized Keys)

公钥被用于认证其主机。你在远程系统上使用公钥来允许用户访问。公钥被放置在远程用户账户的`.ssh/authorized_keys`文件中。记住，DSA的公钥在`.ssh/id_dsa.pub`文件中。如果用户想从本地账户远程登录到远程系统上的账户，他们首先需要将他们的DSA公钥放置在目标系统上，他们想要访问的远程系统账户的`.ssh/authorized_keys`文件中。`rabbit.mytrek.com`上的`larisa`账户，其来自`/home/larisa/id_dsa.pub`的Larisa公钥必须被放在`aleina`的`authorized_keys`文件中，即`/home/aleina/.ssh/authorized_keys`。Larisa可以发送密钥或让其复制过去。一个简单的操作可以将密钥追加到授权密钥中。在下一个示例中，用户将`larisa.pub`文件中aleina的公钥添加到授权密钥中。`Larisa.pub`是用户之前收到的`/home/larisa/id_dsa.pub`文件的副本。

```
cat larisa.pub >> .ssh/authorized_keys
```

## 加载密钥 (Loading Keys)

如果你经常连接到各种远程主机，可以使用`ssh-agent`命令将私钥放入内存中，以便可以快速访问并解密传输。`ssh-agent`命令旨在登录会话开始时。对于GNOME，你可以使用由`ssh-add`调用的`openssh-gnome`工具，它允许你在登录GNOME时输入密码。每当你使用SSH客户端时，GNOME会自动提示密码。

尽管`ssh-agent`让你将私钥保留在内存中，但你必须专门使用`ssh-add`命令将私钥加载到内存中。不带参数的`ssh-add`会从你的`.ssh/id_dsa`或`.ssh/id_rsa`文件加载私钥。系统会提示你输入该私钥的密码口令。要从内存中移除密钥，请使用带有`-d`选项的`ssh-add`。如果你有多个私钥，可以将它们都加载到内存中。带有`-l`选项的`ssh-add`会列出当前加载的密钥。

## SSH 客户端 (SSH Clients)

SSH最初设计用于替代远程操作，如`rlogin`、`rcp`和`Telnet`，这些操作不提供加密，并增加了如明文传输密码等安全风险。你还可以使用SSH来编码变量以及进行FTP传输（`sftp`）。`ssh-clients`包包含了用于替代这些应用程序的SSH客户端。通过`ssh`或`ssh`，你可以从远程主机登录以执行命令并运行应用程序；例如`scp`，你可以在远程主机和网络主机之间复制文件，就像`rcp`一样。通过`sftp`，你可以传输FTP文件。

## SSH

SSH最初设计用于替代远程操作，如`rlogin`、`rcp`和`Telnet`，这些操作不提供加密，并增加了如明文传输密码等安全风险。你还可以使用SSH来编码变量以及进行FTP传输（`sftp`）。`ssh-clients`包包含了用于替代这些应用程序的SSH客户端。通过`ssh`或`ssh`，你可以从远程主机登录以执行命令并运行应用程序；例如`scp`，你可以在远程主机和网络主机之间复制文件，就像`rcp`一样。通过`sftp`，你可以传输FTP文件。

SSH最初设计用于替代远程操作，如`rlogin`、`rcp`和`Telnet`，这些操作不提供加密，并增加了如明文传输密码等安全风险。你还可以使用SSH来编码变量以及进行FTP传输（`sftp`）。`ssh-clients`包包含了用于替代这些应用程序的SSH客户端。通过`ssh`或`ssh`，你可以从远程主机登录以执行命令并运行应用程序；例如`scp`，你可以在远程主机和网络主机之间复制文件，就像`rcp`一样。通过`sftp`，你可以传输FTP文件。

SSH最初设计用于替代远程操作，如`rlogin`、`rcp`和`Telnet`，这些操作不提供加密，并增加了如明文传输密码等安全风险。你还可以使用SSH来编码变量以及进行FTP传输（`sftp`）。`ssh-clients`包包含了用于替代这些应用程序的SSH客户端。通过`ssh`或`ssh`，你可以从远程主机登录以执行命令并运行应用程序；例如`scp`，你可以在远程主机和网络主机之间复制文件，就像`rcp`一样。通过`sftp`，你可以传输FTP文件。

SSH最初设计用于替代远程操作，如`rlogin`、`rcp`和`Telnet`，这些操作不提供加密，并增加了如明文传输密码等安全风险。你还可以使用SSH来编码变量以及进行FTP传输（`sftp`）。`ssh-clients`包包含了用于替代这些应用程序的SSH客户端。通过`ssh`或`ssh`，你可以从远程主机登录以执行命令并运行应用程序；例如`scp`，你可以在远程主机和网络主机之间复制文件，就像`rcp`一样。通过`sftp`，你可以传输FTP文件。

SSH最初设计用于替代远程操作，如`rlogin`、`rcp`和`Telnet`，这些操作不提供加密，并增加了如明文传输密码等安全风险。你还可以使用SSH来编码变量以及进行FTP传输（`sftp`）。`ssh-clients`包包含了用于替代这些应用程序的SSH客户端。通过`ssh`或`ssh`，你可以从远程主机登录以执行命令并运行应用程序；例如`scp`，你可以在远程主机和网络主机之间复制文件，就像`rcp`一样。通过`sftp`，你可以传输FTP文件。

# 第 19 章：Secure Shell 与 Kerberos 367

在下一个示例中，用户`george`从用户`celesia`的家目录复制了`mydoc1`文件：

```
[george@turtle]$ scp celesia@turtle.mytrek.com:mydoc1
celesia@turtle.mytrek.com's password:\mydoc1 0% | 0 ---
ETA
mydoc1 100% | *********************| 17 00:00
[george@turtle george]$
```

在Windows系统上，你也可以使用如`winscp`等`scp`客户端，它们可以与启用了`scp`的Linux系统进行交互。

## sftp 和 sftp-server
