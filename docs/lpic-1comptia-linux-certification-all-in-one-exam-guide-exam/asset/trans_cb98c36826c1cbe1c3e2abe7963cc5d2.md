

b. 打开一个终端会话，并使用 `su` 命令切换到 root 用户。

c. 在 shell 提示符下，输入 `DISPLAY=X_client_IP_address:0.0`；然后输入 `export DISPLAY`。这告诉 X 服务器将其输出显示在远程 X 客户端上。

d. 编辑 `/etc/ssh/sshd_config` 文件并将 X11Forwarding 选项设置为 yes。保存对文件的更改并退出编辑器。

3. 切换回你的客户端系统。

4. 在客户端系统的 shell 提示符下，输入 `ssh -X -l user_name IP_address_of_SSH_server`。

5. 当提示时，输入远程用户的密码。请注意，现在你已经登录到了服务器系统。

6. 在 shell 提示符下，输入 `gedit` 以启动 gedit 文本编辑器。请注意，尽管你登录的是远程服务器系统，但 X 应用程序却显示在本地桌面上。一个示例如图 18-7 所示。因为使用了 `-X` 选项，所以在系统之间传输的所有 X 流量都是加密的。

在我们结束关于 SSH 的讨论之前，我们需要查看如何配置 SSH 使用公钥认证，而不是用户名和密码。接下来我们将回顾这样操作的方法。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_768_0.png)

### 配置 SSH 使用公钥认证

除了使用用户名和密码组合向 SSH 服务器进行身份验证外，你还可以配置 sshd 守护进程以允许使用 RSA 或 DSA 公钥进行身份验证。为了实现这一点，客户端系统上用户的公钥必须存储在你要作为其进行身份验证的服务器系统上的该用户主目录中的 `~/.ssh/authorized_keys` 文件中。为此，你需要将公钥从客户端系统安全地复制到服务器系统上。当然，私钥仍然保留在客户端系统上。

如果你配置 SSH 服务器使用公钥认证，当 SSH 会话最初建立时，SSH 客户端会告诉 SSH 服务器应该使用哪个公钥进行身份验证。然后，SSH 服务器检查它是否拥有该客户端的公钥；如果有，它会将生成一个随机数，并用该公钥对其进行加密。接着，它将加密后的数字发送给客户端，客户端使用与公钥关联的私钥对其进行解密。然后，客户端计算从服务器接收到的数字的 MD5 校验和。它通过 SSH 服务器系统将该校验和发回，服务器随后计算其原本发送的数字的 MD5 校验和。如果两个校验和匹配，则用户自动登录。

要配置公钥认证，首先需要做的是在客户端系统上创建公钥/私钥对，以便你可以将公钥发送到 SSH 服务器。可以使用 ssh-keygen 命令来完成此操作。请完成以下步骤：

1. 在客户端系统的 shell 提示符下，根据 SSH 服务器支持的加密方法，输入 `ssh-keygen -t rsa` 或 `ssh-keygen -t dsa`。为了安全起见，你可以简单使用这两个命令创建两个密钥对，一个用于 RSA 加密，另一个用于 DSA 加密。

2. 当提示保存私钥的文件名时，按 ENTER 键使用默认文件名 `~/.ssh/id_rsa` 或 `~/.ssh/id_dsa`。相应的公钥将分别保存为 `~/.ssh/id_rsa.pub` 或 `~/.ssh/id_dsa.pub`。

3. 当提示时，为密钥输入密码短语。使用密码短语非常重要。如果你不这样做，任何设法获取你密钥文件副本的人都可以无需输入密码短语即可向 SSH 服务器进行身份验证。为密钥分配密码短语意味着如果你不知道它，密钥就毫无用处。

此时，你的密钥对已经创建。下面展示了一个创建 RSA 密钥对的示例：

```text
rtracy@wsl:~$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/rtracy/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/rtracy/.ssh/id_rsa.
Your public key has been saved in /home/rtracy/.ssh/id_rsa.pub.
The key fingerprint is:
ba:14:a8:14:de:fd:42:40:f2:40:c8:b0:8b:03:a4:6d:fc rtracy@wsl
```

密钥的随机艺术图像如下：

```text
+----[ RSA 2048]----+
| .   ..     |   |
|oo + =    |   |
| O +*+=.+ o|   |
|   O + + O .|   |
|    o E o S.|   |
|.       . o |   |
|        . O |   |
|   . o    . |   |
|     +.    ..   |
+----[RSA 2048]----+
rtracy@wsl:~>
```

接下来你需要做的是将你刚创建的公钥复制到 SSH 服务器。一种简单（且安全）的方法是使用本章前面介绍的 `scp` 命令。其语法是

```text
scp ~/ssh/key_name.pub user_name@address_of_SSH_server:filename
```

在此处展示的示例中，本地 WS1 上 `rtracy` 用户的 RSA 公钥被复制到 WS3 上 `rtracy` 用户的主目录，并保存为名为 `keyfile` 的文件。

```text
rtracy@ws1:~> scp ~/.ssh/id_rsa.pub ws3:keyfile
Password:
id_rsa.pub                                100%  392     0.4KB/s   00:00
rtracy@ws1:~>
```

此时，需要将你刚复制的密钥文件的内容追加到你要连接 SSH 服务器所使用用户的 `~/.ssh/authorized_keys` 文件末尾。一个简单的方法是使用标准的（基于密码验证的）SSH 会话连接到 SSH 服务器系统，然后使用 cat 命令将密钥文件的内容追加到用户主目录中 `~/.ssh/authorized_keys` 文件的末尾。如何执行此操作的示例如下所示。

```text
rtracy@ws1:~> ssh -l rtracy ws3
Password:
Last login: Thu Jun 2 15:05:34 2011 from 192.168.1.84
rtracy@ws3:~> mkdir ~/.ssh
rtracy@ws3:~> cat keyfile >> ~/.ssh/authorized_keys
rtracy@ws3:~>
```

在此示例中，我通过 SSH 连接以远程 `rtracy` 用户身份登录到 WS3 系统，然后在该用户的主目录中创建隐藏的 `.ssh` 目录。之所以需要创建该目录是因为它尚不存在。如果 `.ssh` 目录已经存在，你可以跳过此步骤，直接将密钥文件的内容追加到 `authorized_keys` 文件的末尾。请注意，在此示例中，我使用带有 `>>` 重定向字符的 `cat` 命令将名为 `keyfile` 的文件的内容添加到 `authorized_keys` 文件的末尾。

在此示例中，`authorized_keys` 文件尚不存在，因此重定向过程自动为我创建了该文件。正因为如此，实际上我本来也可以使用单个 `>` 重定向字符，因为该文件尚不存在。

另一方面，如果 authorized_keys 文件已经存在，请记住使用 `>>` 重定向字符而不是 `>` 非常重要。记住，使用 `>>` 会将命令的输出追加到指定文件的末尾。使用单个重定向 `>` 字符会用命令的输出覆盖整个文件。如果 authorized_keys 文件中已经包含几个你想保留的密钥，这将是一件坏事。

现在你可以测试配置，看看公钥认证是否正常工作。如果你仍登录在 SSH 服务器上的 SSH 会话中，请退出该会话。然后与服务器建立一个新的 SSH 会话。你应该被提示输入密钥文件的密码短语，而不是用户名和密码，如图 18-9 所示。

输入密码短语后，你将被验证到 SSH 服务器。请注意在下一个示例中，建立 SSH 会话时并未要求密码：

```text
rtracy@ws1:~$ ssh -l rtracy ws3
Last login: Thu Jun 2 16:13:39 2011 from 192.168.1.84
rtracy@WS3:~>
```

如果需要，你可以使用 ssh-agent 命令来消除每次建立 SSH 连接时都需要输入密码短语的需求。请完成以下步骤：

1. 在你的客户端系统的 shell 提示符下，输入 `ssh-agent bash`。

2. 在 shell 提示符下，根据你创建的是哪个密钥文件，输入 `ssh-add ~/.ssh/id_rsa` 或 `ssh-add ~/.ssh/id_dsa`。

3. 当提示时，输入密钥文件的密码短语。这样做后，你应该会收到身份已添加的提示。示例如下：

```text
rtracy@ws1:~$ ssh-agent bash
rtracy@ws1:~$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/rtracy/.ssh/id_rsa:
Identity added: /home/rtracy/.ssh/id_rsa (/home/rtracy/.ssh/id_rsa)
rtracy@ws1:~>
```

完成后，ssh-agent 进程将密码短语存储在内存中。然后它会监听 SSH 请求，并在请求时自动为你提供密钥密码短语。让我们在下面的练习中实践配置 SSH 使用公钥认证：

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_771_0.png)

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_771_1.png)

