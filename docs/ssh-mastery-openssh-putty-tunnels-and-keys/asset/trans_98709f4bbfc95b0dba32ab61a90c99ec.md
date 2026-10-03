
## 安装主机证书

一旦你在服务器上安装了证书，请在 *sshd_config* 中使用 HostCertificate 关键字进行配置。由于我很容易混淆，我把 HostCertificate 关键字放在相关的 HostKey 关键字旁边。

```
HostKey /etc/ssh/ssh_host_rsa_key
HostCertificate /etc/ssh/ssh_host_rsa_key-cert.pub
...
HostKey /etc/ssh/ssh_host_ed25519_key
HostCertificate /etc/ssh/ssh_host_ed25519_key-cert.pub
```

重启 sshd。现在你就可以使用主机证书了！

## 测试主机证书

一旦你在 sshd(8) 中配置了证书并设置了客户端的 */etc/ssh/ssh_known_hosts*，你就可以尝试基于证书的主机密钥验证了。

将你的 *$HOME/.ssh/known_hosts* 文件移开，或如果你非常非常有信心就删除它。现在通过 SSH 登录到服务器。你应该会得到登录提示，而不会被提示验证主机密钥。

如果主机证书不能正常工作，在你的 `ssh` 命令行中添加一个或两个 -v。客户端是否看到了证书？如果没有，以调试模式运行 `sshd`，看看它是否加载了证书，如果没有加载，为什么没有。`ssh` 是否看到了证书但未识别它？如果是这样，你弄错了你的 *ssh_known_hosts* 条目。

## 吊销证书

证书很棒，直到有人入侵你的服务器并窃取一个已签名的密钥对。窃贼可以用该签名密钥冒充被入侵的主机。这很糟糕。幸运的是，你可以使用 RevokedHostKeys *ssh_config* 关键字告诉客户端不要信任某个公钥。

```
RevokedHostKeys /etc/ssh/revoked-hosts
```

吊销的主机密钥文件包含一个公钥列表，每行一个。即使它们带有相应的证书，客户端也不会接受这些公钥。

你的企业需要能够更新客户端的吊销密钥文件，并必须定期测试它。虽然实时更新最好，但即使是登录脚本也比没有好。

## 查看证书

你可以使用 `ssh-keygen -L` 查看证书的内容。使用 `-f` 指定证书文件。

```
# ssh-keygen -Lf ssh_host_ed25519_key-cert.pub
ssh_host_ed25519_key-cert.pub:
Type: ssh-ed25519-cert-v01@openssh.com host certificate
Public key: ED25519-CERT SHA256:nNtyIQidY3MXAEfpwZ0wzKXKQFnCoQhe0CRI1dc4EB8
Signing CA: RSA SHA256:ZQHNMc2TmW1nygGy9+UoOYFK92RdbguzNi+cX4gA414
Key ID: "sloth"
Serial: 0
Valid: from 2017-12-04T11:52:00 to 2017-12-25T11:53:17
Principals:
    sloth.mwl.io
```

关键选项：(none)
扩展：(none)

这里最关键的细节是 key ID（sloth，对应主机名）和有效日期。如果你有多个证书颁发机构，你可能会发现 signing CA 字段很有用。principals 字段给出此证书有效的实体，每行一个。如果你把密钥文件弄得如此混乱，以至于需要将公钥字段与服务器上的密钥进行比较，请重新开始。

定义关键选项和扩展的字段对于用户证书很有用。

## 用户证书

用户证书比主机证书更复杂，主要是因为用户比主机更复杂。SSH 用户证书允许你复制 authorized_keys 中的所有内容，包括第 12 章“Automation”中讨论的限制和限制。这需要更深入地了解 SSH 证书。

SSH 证书的一个关键概念是 principal。principal 定义了此证书适用于哪些实体。对于主机证书，principal 是主机名。用户证书的 principal 通常是证书所针对的用户名，但它也可能包含限制、限制和其他信息。没有 principal 的用户证书可用于作为任何用户进行身份验证。你必须为每个证书分配一个 principal，除非你真的想要一个通配符身份验证证书。

我们将在本节中始终引用 principal。起初你可以把它想成用户名，但随着我们继续前进，其含义会扩展。

## 创建和查看用户证书

获取用户的公钥身份验证密钥，通常是 id_rsa.pub，并将其复制到你的证书颁发机构机器。你需要它来生成证书。公钥不是保密的，因此在网络上传输它没有风险。

创建用户证书的命令与创建主机证书非常相似。使用 -s 指定用户 CA 密钥的路径。-I 标志定义证书标识，-n 给出证书 principal。使用 -v 定义过期时间。最后一个参数是要签名的公钥文件。在这里，我让我的用户 CA 签署我其中一个用户的公钥，使其对用户名 djm 有效。我将有效期设置为 52 周，即一年，因为如果在此之前过期而用户提交续期，我将完全归咎于他。

```
# ssh-keygen -s user-mwlca-key -I user_djm -n djm -V +52w id_rsa.pub
```

我输入 CA 密码并得到一个证书文件 id_rsa-cert.pub。如果你以前从未做过此操作，请查看证书。

```
# ssh-keygen -Lf id_rsa-cert.pub
id_rsa-cert.pub:
    Type: ssh-rsa-cert-v01@openssh.com user certificate
```

```
Public key: RSA-CERT SHA256:CfVbRUF+AaUcOxml6wI5Cf5nvtjzBDH6NcXaGU4...
Signing CA: RSA SHA256:CKZFZXRgOy1ji8zmUhU0zjJQFN s9gLEqAwSjA8pB4dg
Key ID: "user_djm"
Serial: 0
Valid: from 2017-12-04T07:31:00 to 2018-12-23T07:32:37
Principals:
djm
Critical Options: (none)
Extensions:
  permit-X11-forwarding
  permit-agent-forwarding
  permit-port-forwarding
  permit-pty
  permit-user-rc
```

顶部看起来与主机证书非常相似，但用户在下方会得到不同的信息。我们的 principal 是 djm，因此此证书仅适用于此用户。我们没有关键选项，但 Extensions 列出了几个关键字。这些是授予此用户的 SSH 权限，我们将在“受限证书”中很快看到。

将此证书返回给用户。

## 使用用户证书

将证书复制到 $HOME/.ssh。用户的公钥身份验证密钥应该已经在那里。

你应该已经设置了 TrustedUserCAKeys 关键字，如本章“信任你的证书颁发机构”中所述。如果是这样，请将用户的 authorized_keys 文件移开。让用户通过 SSH 登录到服务器。如果服务器配置正确，用户应该能够登录，而服务器对该特定密钥没有任何信息。

如果你想要的就是这个，你就完成了。但让我们看看一些更困难的东西。

## 吊销用户证书

通常，你不会吊销用户证书。你吊销与证书关联的公钥，使用 RevokedKeys sshd_config 关键字。

```
RevokedKeys /etc/ssh/revoked
```

轮换你的 CA 的一个原因是它限制了你的吊销证书列表的长度。你不希望五年前被盗的笔记本电脑的证书仍然在你的吊销证书文件中！

如果你有一个复杂的吊销密钥列表，请调查 ssh-keygen(8) 中的 Key Revocation Lists (KRLs)。

## 受限证书

正如你可以限制帐户和密钥的访问一样，你也有权力限制证书。你可以使用 ssh-keygen 的 -O 标志来做到这一点。-O 标志有一长串可能的限制，与第 12 章中 authorized_keys 的限制相同。这些选项包括 no-agent-forwarding、no-port-forwarding、no-pty、no-user-rc 和 no-x11-forwarding。所有这些 no-限制都有对应的 permit-版本：permit-agent-forwarding、permit-port-forwarding、permit-pty、permit-user-rc 和 permit-x11-forwarding。此外，你还有 source-address 限制，它规定了可以使用此证书进行身份验证的 IP 地址。还有 clear 限制，它与 authorized_keys 中的 restrict 类似，关闭所有特权，允许你通过 permit- 语句有选择地打开它们。最后，force-command 强制用户运行该特定命令。

自动化的一种常见情况是当你有一个只能运行单个任务的密钥时。我想创建一个只能用于运行命令 /usr/local/scripts/backup.sh 的密钥的证书。在客户端创建一个名为 backup 的密钥，并将 backup.pub 发送给 CA 进行签名。我想使用 clear 选项从此证书中删除所有权限，然后使用 force-command 强制运行备份脚本。我使用 -O 两次来分配这些权限。否则，它看起来像任何其他用户密钥签名。

```
# ssh-keygen -s user-mwlca-key -I user_backup -n backup -V +52w -O clear -O force-command="/usr/local/scripts/backup.sh" backup.pub
```

这会生成证书文件 backup-cert.pub。查看其内容。

```
# ssh-keygen -Lf backup-cert.pub
backup-cert.pub:
    Type: ssh-rsa-cert-v01@openssh.com user certificate
    Public key: RSA-CERT SHA256:UL4ctioc5p8aSN1S318FI5RpsS1rnxJdr0EDb/B69Jg
    Signing CA: RSA SHA256:CKZFZXRg0y1ji8zmUhU0zjJQFN s9gLEqAWsJ8aP8B4dg
    Key ID: "user_backup"
    Serial: 0
    Valid: from 2017-12-05T07:56:00 to 2018-12-04T07:57:50
    Principals:
        backup
    Critical Options:
        force-command /usr/local/scripts/backup.sh
    Extensions: (none)
```

将此密钥与我们刚刚创建的常规用户证书进行比较。用户密钥没有关键选项，而此证书将 force-command 语句列为关键选项。用户密钥在 Extension 下有一堆特权，而此密钥没有。此证书只授予使用一个命令的权利。

目前没有创建 SSH 隧道的特定特权。如果你的组织大到需要证书，它应该有标准声明可接受的 VPN 类型。³

## 禁用 authorized_keys

一旦你完全部署了用于用户身份验证的 SSH 证书，你可能会决定禁用 authorized_keys 文件。这在 sshd_config 中很容易完成。

```
AuthorizedKeysFile none
```

但是，如果你有不支持证书的客户端，你将需要为这些客户端提供登录方式。一些组织要求所有系统管理员使用基于 Unix 的桌面，以便他们可以支持证书。一些大型组织如 Facebook 禁止从客户端进行 SSH 访问，除非到中央
