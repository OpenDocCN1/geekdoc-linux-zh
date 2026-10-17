
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? o

系统现在应提示输入密码短语。如果您在 GNOME 桌面环境中工作，则会显示图 10-13 所示的窗口。

在您输入密码短语时，系统会根据长度、使用大小写字符、数字和标点符号来评估其质量。当然，会再次出现类似的窗口，让您第二次输入密码短语。

此时，`gpg2` 命令开始工作。特别是对于较大的密钥，它似乎会在创建随机字节的消息上暂停几分钟。您可能需要运行一些其他程序来刺激该过程。完成后，它会显示类似以下的消息：

```
gpg: key D385AFDD marked as ultimately trusted

public and secret key created and signed.
```

为确保公钥和私钥确实已写入，请运行以下命令：

```
$ gpg2 --list-key
```

输出应包括最新的密钥，以及从用户主目录 `.gnupg/` 子目录中创建的任何其他密钥。对于给定的选项，如果这是本地帐户上的唯一密钥对，您会看到类似于以下输出的内容：

```
/home/michael/.gnupg/pubring.gpg

pub 2048D/1665FB84 2011-02-02 [expires: 2011-04-03]
uid Michael Jang (DSA and Elgamal) <michael@example.com>
sub 2048g/EEC05210 2011-02-02 [expires: 2011-04-03]
```

### 图 10-13

提示输入密码短语。

![](img/9139201cfcaf4292284a0eed074928e5_608_0.png)

## 使用 GPG2 密钥保护文件

现在您可以将公钥发送到远程系统。要开始该过程，您需要导出公钥。对于刚刚创建的密钥对，您可以使用以下命令执行此操作。将“Michael Jang”替换为您自己的姓名。

```
$ gpg2 --export Michael Jang > gpg.pub
```

现在将该密钥复制到远程系统。传递媒介，例如电子邮件、USB 记忆棒或此处所示的 `scp` 命令并不重要。此特定命令从用户 `michael` 的帐户复制 `gpg.pub` 密钥到 `tester1.example.com` 系统上用户 `michael` 的主目录。如果您愿意，可以替换 IP 地址。

```
$ scp gpg.pub tester1.example.com:
```

现在转到远程系统，即 `tester1.example.com`。登录用户 `michael` 的帐户（或您复制 `gpg.pub` 密钥的帐户主目录）。如果需要，您甚至可以使用 `ssh` 等命令远程登录到该系统。连接到该系统后，首先使用以下命令检查现有的 GPG 密钥：

```
$ gpg2 --list-key
```

如果这是一个没有先前 GPG 密钥的系统，列表应为空，并且此命令的输出中不会出现任何内容。现在使用以下命令将 `gpg.pub` 文件导入本地 GPG 密钥列表：

```
$ gpg2 --import gpg.pub
```

通过再次运行 `gpg2 --list-key` 命令确认导入。

现在在远程系统上，您可以使用 `gpg2` 命令加密文件。以下示例加密本地 `keepthis.secret` 文件：

```
$ gpg2 --out underthe.radar --recipient 'Michael Jang' --encrypt
keepthis.secret
```

此处的用户名为‘Michael Jang’。如果您刚刚导入了私钥，则 `gpg2 --list-key` 命令输出中显示的用户名可能不同。请酌情替换。

现在当 `underthe.radar` 文件被复制到原始系统 `server1.example.com` 时，您可以使用以下命令使用私钥开始解密过程：

```
$ gpg --out keepthis.secret --decrypt underthe.radar
```
