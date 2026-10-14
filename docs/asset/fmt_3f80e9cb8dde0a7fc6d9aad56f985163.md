
1. 从终端窗口，以 `geeko` 身份登录到您合作伙伴的计算机：

   a. 从命令行，输入以下内容：

      `ssh -l geeko partner_IP_address`

   b. （条件）如果您收到有关远程主机真实性的警告，请通过输入 `yes` 继续。

   c. 输入密码 `novell`。

      您现在已以 `geeko` 身份登录到您合作伙伴的计算机。

   d. 通过输入 `exit` 注销。

2. 使用密码 `pN0v3ll`，通过输入以下内容检查您合作伙伴系统上正在运行的进程

   `ssh -l root partner_IP_address ps aux`

   显示您合作伙伴计算机上当前运行的所有进程的列表。

3. 使用密码 `novell`，通过输入以下内容将您合作伙伴的 `/etc/hosts` 文件复制到您的 `/tmp` 目录

   `scp geeko@partner_IP_address:/etc/hosts /tmp/`

4. 使用密码 `novell`，通过输入以下内容将您的 `/etc/hosts` 文件复制到您合作伙伴计算机上 `geeko` 的目录

   `scp /etc/hosts geeko@partner_IP_address:`

5. 通过输入以下内容以 `geeko` 身份使用 `sftp` 连接到您合作伙伴的计算机

   `sftp geeko@partner_IP_address`

6. 通过输入以下内容将 `/bin/date` 程序复制到您自己的计算机上 `geeko` 的目录

   `get /bin/date /home/geeko/`

7. 通过输入以下内容退出 `sftp`

   `exit`

## 公钥身份验证管理

除了密码身份验证外，用户还可以使用公钥程序进行身份验证。协议版本 1 仅支持 RSA 密钥。协议版本 2 通过 RSA 和 DSA 密钥提供身份验证。

要管理公钥身份验证，您需要了解以下内容：

- 公钥身份验证过程
- 创建密钥对
- 配置和使用公钥身份验证

### 公钥身份验证过程

要使用公钥身份验证，用户公钥必须存储在服务器上被访问的用户账户的主目录中。这些公钥存储在服务器上的文件 `~/.ssh/authorized_keys` 中。相应的私钥必须存储在客户端计算机上。

将密钥存储在适当位置后，公钥身份验证过程中会发生以下情况：

1. 客户端通知服务器正在用于身份验证的公钥。
2. 服务器检查公钥是否已知。
3. 服务器使用公钥加密一个随机数并将其传输给客户端。
4. 只有客户端能够使用其私钥解密随机数。
5. 客户端向服务器发送其从该数字计算得出的 MD5 校验和。
6. 服务器也会计算校验和，如果它们相同，则用户已成功通过身份验证。
7. 如果公钥认证失败且允许密码认证，则会提示用户输入登录密码。

密钥应由密码短语保护。没有密码短语保护，仅拥有包含私钥的文件就足以成功进行身份验证。然而，如果密钥额外受密码短语保护，在不知道密码短语的情况下，该文件将毫无用处。

## 创建密钥对

使用 `ssh-keygen` 命令创建密钥对。SSH1 和 SSH2 需要不同的密钥。因此，您需要为每个版本创建单独的密钥对。

使用选项 `-t keytype` 指定密钥类型：

- `ssh-keygen -t rsa1` 生成 SSH1 的密钥对。
- `ssh-keygen -t rsa` 和 `ssh-keygen -t dsa` 生成 SSH2 的密钥对。

密钥存储在目录 `~/.ssh` 中。对于 SSH1，这些文件的默认名称为 `~/.ssh/identity`（私钥）和 `~/.ssh/identity.pub`（公钥）。对于 SSH2，默认文件分别为 `~/.ssh/id_rsa` 和 `~/.ssh/id_dsa`，外加相应的带 `.pub` 扩展名的公钥文件。

以下示例展示了如何使用选项 `-t`（必需）生成协议版本 2 的 DSA 密钥对：

```
geeko@dal0:~> ssh-keygen -t dsa
Generating public/private dsa key pair.
Enter file in which to save the key (/home/geeko/.ssh/id_dsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/geeko/.ssh/id_dsa.
Your public key has been saved in /home/geeko/.ssh/id_dsa.pub.
The key fingerprint is:
ef:73:c6:f6:8a:ff:9d:d1:50:01:cf:07:65:c5:54:8b geeko@dal0
```

## 配置和使用公钥认证

使用 RSA 或 DSA 密钥进行身份验证时，您需要将公钥复制到服务器，然后将公钥追加到文件 `~/.ssh/authorized_keys` 中。

例如，您可以使用 `scp` 命令将密钥复制到服务器，如下所示：

```
geeko@dal0:~> scp .ssh/id_dsa.pub da50:geeko-pubkey
```

然后应将密钥添加到文件 `~/.ssh/authorized_keys` 中，且不会覆盖现有密钥，如下所示：

```
geeko@da10:~> ssh da50
Password:
Last login: Tue May 30 12:03:29 2006 from da10.digitalairlines.com
geeko@da50:~> cat geeko-publickey >> ~/.ssh/authorized_keys
geeko@da50:~> exit
geeko@da10:~>
```

![](img/9129877170834ca9d5fdac5319bf5f12_160_0.png)

实用程序 `ssh-copy-id` 可用于简化将密钥复制到另一台计算机并将其追加到 `~/.ssh/authorized_keys` 的前述步骤。有关更多信息，请输入 `man ssh-copy-id`。

现在您可以启动客户端以查看 DSA 密钥的身份验证是否正常工作，如下所示：

```
geeko@da10:~> ssh da50
Enter passphrase for key '/home/geeko/.ssh/id_dsa':
Last login: Tue May 30 12:03:40 2006 from da10.digitalairlines.com
geeko@da50:~>
```

您可以使用选项 `-i` 输入具有不同名称或位置的私钥的文件名。

使用密钥进行身份验证时，登录服务器或使用 `scp` 复制时需要密码短语。如果您三次输入密码短语错误，将被要求输入通常的登录密码。`sshd` 配置允许您更改此行为；请参阅表 5-3。

可以使用 `ssh-agent` 避免在每次连接时都输入此密码短语。启动 `ssh-agent` 后，您需要使用 `ssh-add` 命令输入密码短语。此后，`ssh-agent` 会监控所有 SSH 请求并在需要时提供所需的私钥。

`ssh-agent` 可作为任何其他进程（例如 shell 或 X 服务器）的包装器。以下示例显示了通过 `ssh-agent` 启动 `bash` shell 的过程：

```
geeko@da10:~> ssh-agent bash
geeko@da10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```

对于从此 shell 输入的所有 `ssh` 或 `scp` 命令（已配置密钥身份验证），代理将自动提供私钥。

您也可以将 `ssh-agent` 与图形登录一起使用。登录图形界面时，会启动 X 服务器。如果您使用显示管理器登录，X 服务器将加载文件 `/etc/X11/xdm/sys.xsession`。

为了使 `ssh-agent` 在 X 服务器启动时自动启动，您只需在文件 `sys.xsession` 中输入以下参数：

`usessh="yes"`

```
usessh="yes"
```

此条目在 SUSE Linux Enterprise Desktop 10 中已默认设置。

输入 `yes` 参数后，`ssh-agent` 将在用户下次登录图形界面时自动启动。后台运行的代理必须一次性提供密码短语，如下所示：

```
geeko@da10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```
