
- 6. 服务器也会计算校验和，如果它们相同，则用户已成功通过身份验证。
- 7. 如果公钥认证失败且允许密码认证，则会提示用户输入登录密码。

密钥应由密码短语保护。没有密码短语保护，仅拥有包含私钥的文件就足以成功进行身份验证。然而，如果密钥额外受密码短语保护，在不知道密码短语的情况下，该文件将毫无用处。

## 创建密钥对

使用 ssh-keygen 命令创建密钥对。SSH1 和 SSH2 需要不同的密钥。因此，您需要为每个版本创建单独的密钥对。

使用选项 -t keytype 指定密钥类型：

- `ssh-keygen -t rsa1` 生成 SSH1 的密钥对。
- `ssh-keygen -t rsa` 和 `ssh-keygen -t dsa` 生成 SSH2 的密钥对。

密钥存储在目录 ~/.ssh 中。对于 SSH1，这些文件的默认名称为 ~/.ssh/identity（私钥）和 ~/.ssh/identity.pub（公钥）。对于 SSH2，默认文件分别为 ~/.ssh/id_rsa 和 ~/.ssh/id_dsa，外加相应的带 .pub 扩展名的公钥文件。

以下示例展示了如何使用选项 -t（必需）生成协议版本 2 的 DSA 密钥对：

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

使用 RSA 或 DSA 密钥进行身份验证时，您需要将公钥复制到服务器，然后将公钥追加到文件 ~/.ssh/authorized_keys 中。

例如，您可以使用 scp 命令将密钥复制到服务器，如下所示：

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

使用密钥进行身份验证时，登录服务器或使用 scp 复制时需要密码短语。如果您三次输入密码短语错误，将被要求输入通常的登录密码。（sshd 配置允许您更改此行为；请参阅表 5-3。）

可以使用 ssh-agent 避免在每次连接时都输入此密码短语。启动 ssh-agent 后，您需要使用 ssh-add 命令输入密码短语。此后，ssh-agent 会监控所有 SSH 请求并在需要时提供所需的私钥。

ssh-agent 可作为任何其他进程（例如 shell 或 X 服务器）的包装器。以下示例显示了通过 ssh-agent 启动 bash shell 的过程：

```
geeko@da10:~> ssh-agent bash
geeko@da10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```

对于从此 shell 输入的所有 ssh 或 scp 命令（已配置密钥身份验证），代理将自动提供私钥。

您也可以将 ssh-agent 与图形登录一起使用。登录图形界面时，会启动 X 服务器。如果您使用显示管理器登录，X 服务器将加载文件 `/etc/X11/xdm/sys.xsession`。

为了使 ssh-agent 在 X 服务器启动时自动启动，您只需在文件 sys.xsession 中输入以下参数：

`usessh="yes"`

```
usessh="yes"
```

此条目在 SUSE Linux Enterprise Desktop 10 中已默认设置。

输入 yes 参数后，ssh-agent 将在用户下次登录图形界面时自动启动。后台运行的代理必须一次性提供密码短语，如下所示：

```
geeko@da10:~> ssh-add .ssh/id_dsa
Enter passphrase for .ssh/id_dsa:
Identity added: .ssh/id_dsa (.ssh/id_dsa)
```

对于随后使用公钥程序进行身份验证的连接，现在不再需要提供密码短语。此 ssh-agent 会处理私钥。当 X 服务器终止时，ssh-agent 也会关闭。密码短语永远不会存储在文件中；私钥仅在用户再次注销之前由 ssh-agent 存储在内存中。

![](img/9129877170834ca9d5fdac5319bf5f12_161_0.png)

## 练习 5-4：执行公钥认证

在本练习中，您将练习使用 SSH 进行公钥认证。本练习需要与合作伙伴一起完成。

创建一个 ssh 密钥对，将公钥添加到合作伙伴计算机上的文件 `~geeko/.ssh/authorized_keys` 中，并注意使用或不使用公钥登录之间的差异。然后，使用 ssh-agent 缓存私钥，并再次以 geeko 身份登录到合作伙伴的机器。

以 root 身份更改 SSH 服务器配置，仅允许公钥认证。重新启动 sshd，然后以 root 身份尝试 `ssh geeko@localhost`。

### 完成此练习的详细步骤

要执行公钥认证，请执行以下操作：

- 1. 以用户 geeko 身份打开一个终端窗口。
- 2. 生成 RSA 密钥对：
  - a. 从终端窗口输入
  - b. 通过按 Enter 键接受密钥的默认位置（`/home/geeko/.ssh/id_rsa`）。
  - c. 输入密码短语或密钥。
有关您的密钥对的信息，例如标识和公钥的位置，将显示出来。

```
ssh-keygen -t rsa
```

- 3. 将 RSA 公钥添加到合作伙伴的 ~geeko/.ssh/authorized_keys 文件：
  - a. 使用密码 novell，通过输入以下内容将文件复制到合作伙伴的 geeko 主目录：
`scp .ssh/id_rsa.pub geeko@partner_IP_address`
  - b. 通过输入以下内容使用 ssh 以 geeko 身份登录到合作伙伴的计算机
`ssh -l geeko partner_IP_address`
  - c. 输入 `ls -al`。
查找 .ssh 目录。
  - d. （条件）如果不存在 .ssh 目录，通过输入以下内容创建它
`mkdir .ssh`
  - e. 通过输入以下内容将公钥复制到 ~/.ssh/authorized_keys 文件
`cat id_rsa.pub >> .ssh/authorized_keys`

- 4. 通过输入 exit 从合作伙伴的计算机注销。
- 5. 通过输入以下内容使用 ssh 以 geeko 身份登录到合作伙伴的计算机
`ssh -l geeko partner_IP_address`
会提示您输入密码短语，而不是密码。
- 6. 通过输入 secret 登录；然后通过输入 exit 注销。
- 7. 为了跟踪身份验证，通过输入以下内容启动 ssh-agent
`ssh-agent bash`
- 8. 通过输入以下内容将您的私钥添加到代理以进行身份验证
`ssh-add .ssh/id_rsa`
然后输入密码短语 secret。
- 9. 通过输入以下内容使用 ssh 以 geeko 身份登录到合作伙伴的计算机
`ssh -l geeko partner_IP_address`
这次不会提示您输入密码或密码短语。
- 10. 通过输入 exit 从合作伙伴的计算机注销。
- 11. 切换到用户 root（su -，密码 n0v3ll）。
- 12. 在您选择的编辑器中打开 /etc/ssh/sshd_config 文件，例如 gedit。
  - a. 找到包含 PasswordAuthentication 的行，并确保其设置为 no。
  - b. 找到包含 UsePAM 的行，并将其设置从 yes 改为 no。
  - c. 保存文件并关闭编辑器。
