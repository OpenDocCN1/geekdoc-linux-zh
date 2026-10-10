

## 使用 GPG

GPG 包含使用公钥加密和数字签名所需的工具。你使用的是 `gpg` 命令。随着你开始使用加密，你可以逐步了解如何使用 GPG。下面向你介绍一些使用 GPG 执行典型任务的示例。

### 生成密钥对

生成密钥对的步骤如下：

- 1. **输入 `gpg --gen-key`**
  
  如果你是首次使用 `gpg`，它会在你的主目录中创建一个 `.gnupg` 目录，并在该目录中创建一个名为 `gpg.conf` 的文件。然后 GPG 会询问你想要哪种类型的密钥：
  
  > 请选择你想要创建的密钥类型：
  > (1) DSA 和 ElGamal（默认）
  > (2) RSA（仅用于签名）
  > (4) RSA（仅用于签名）
  > 你的选择？

- 2. **按 Enter 键选择默认选项，因为这就足够了。**
  
  然后 GPG 会提示你输入密钥长度（位数）。

- 3. **再次按 Enter 键接受默认值 1,024 位。**
  
  GPG 会询问密钥何时过期。默认设置为永不过期。

- 4. **如果默认设置正是你想要的（为什么不呢？），请按 Enter 键。**

- 5. **当 GPG 询问你是否真的希望密钥永不过期时，按 Y 键确认。**
  
  GPG 会提示你输入姓名、电子邮件地址，最后输入一个注释，以便密钥对与你的姓名关联。

- 6. **输入每项要求的信息，然后按 Enter 键。**

- 7. **当 GPG 给你一个更改信息或确认现有信息的机会时，输入 `o` 并按 Enter 键确认。**
  
  接下来 GPG 会提示你输入一个用于保护私钥的口令（passphrase）。

- 8. **输入一个包含大小写字母、数字和标点符号的长短语——越长越好——然后按 Enter 键。**
  
  请务必选择一个你容易记住的口令。
  
  GPG 将生成密钥。它可能会要求你在电脑上进行一些操作，以便随机数生成器能够生成足够的随机数用于密钥生成过程。

### 交换密钥

要与其他人通信，你必须将你的公钥提供给对方。你还需要获取那些可能向你发送消息的人（或者可能签署文件而你希望验证其签名的人）的公钥。GPG 将公钥保存在你的密钥环中。（*密钥环* 本质上只是存储在文件中的公钥，但将其称为密钥环听起来不错，因为现实世界中每个人都有钥匙环，而且这些也算某种意义上的“钥匙”，对吧？）要列出密钥环中的密钥，请输入

```
gpg --list-keys
```

要将公钥发送给某人或将其放置在网站上，你需要将密钥导出到文件中。最好的方式是将密钥以 GPG 文档中称为 *ASCII-armored*（ASCII 装甲）格式进行导出，命令如下：

```
gpg --armor --export naba@comcast.net > nabakey.asc
```

此命令将我的公键以 ASCII-armored 格式（看起来基本上像乱码文本）保存到名为 *nabakey.asc* 的文件中。当然，你应将电子邮件地址替换为你自己的电子邮件地址（即创建密钥时使用的地址），并将输出文件名更改为其他名称。

将公钥导出到文件后，你可以将该文件通过邮件发送给其他人，或将其放置在网站上供其他人使用。

当你从他人处导入密钥时，通常也是以 ASCII-armored 格式获取的。例如，如果我在名为 *uscertkey.asc* 的文件中有一个 *us-cert@us-cert.gov* 的 GPG 公钥（我这是从 *www.us-cert.gov/pgp/email.html* 链接处获取的），我使用以下命令将其导入我的密钥环：

```
gpg --import uscertkey.asc
```

使用 `gpg --list-keys` 命令来验证该密钥是否在你的密钥环中。例如，当我在系统上输入 `gpg --list-keys` 时，看到的内容如下：

```
/home/naba/.gnupg/pubring.gpg
---------------------------------
pub   1024d/7B38728 2005-08-28
uid             Naha Barkakati (Author) <naba@comcast.net>
sub   2048g/3BD6D418 2005-08-28

pub   2048R/F0E187D0 2004-09-08 [expires: 2005-10-01]
uid             US-CERT Operations Key <us-cert@us-cert.gov>
```

下一步是检查新密钥的指纹。我输入以下命令获取 US-CERT 密钥的指纹：

```
gpg --fingerprint us-cert@us-cert.gov
```

GPG 打印出指纹：

```
pub 2048R/FOKE187D0 2004-09-08 [expire: 2005-10-01]
Key fingerprint = 049F E3BA 240B 4CF1 3A76 04DC 1868 49EC F0E1 87D0
uid US-CERT Operations Key <us-cert@us-cert.gov>
```

此时，你需要与 US-CERT 组织的某人验证密钥指纹。对于像 US-CERT 这样的大型组织，你可以从 US-CERT 网页验证指纹（[www.us-cert.gov/pgp/encryptmail.html](http://www.us-cert.gov/pgp/encryptmail.html)）。我检查过，指纹与 US-CERT 网站上显示的一致。

如果你认为密钥指纹没有问题，你可以签署该密钥并进行验证。这是用于签署密钥的命令：

```
gpg --sign-key us-cert@us-cert.gov
```

GPG 会要求确认，然后提示你输入口令。之后，GPG 将签署该密钥。

![](img/792720823146d68f19fd50c99ebfce4b_550_0.png)

由于密钥验证和签署是 GPG 中潜在的薄弱环节，请仔细对待你签署的密钥。签署一个密钥基本上意味着你信任该密钥确实属于该个人或组织。

### 签署文件

如果你向某人发送文件并希望向接收者保证没有人篡改过该文件，且文件确实由你发送，你会发现签署文件很有用。GPG 使签署文件变得非常容易。你可以使用以下命令对名为 `message` 的文件进行压缩和签署：

```
gpg -o message.sig -s message
```

要验证签名，请输入

```
gpg --verify message.sig
```

要获取原始文档，只需输入

```
gpg -o message --decrypt message.sig
```

有时你并不关心保持消息的机密性，但只是想签署它以表明该消息来自你。在这种情况下，你可以使用以下命令生成并附加一个明文签名：

```
gpg -o message.asc --clearsign message
```

![](img/792720823146d68f19fd50c99ebfce4b_550_1.png)

此命令基本上是将明文签名附加到文本消息末尾。下面是一个典型的明文签名块：

```
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.2 (GNU/Linux)

iDEBBQDEhhAtaHlHts4pygRahiqAJ7Qcj0pRMVgKbukYUyZATYap6RJcTqaQ8m
9Cm2hBQ98o2DX9VXS3z18=
=2uc/
-----END PGP SIGNATURE-----
```

当消息附加了明文签名后，你可以使用 GPG 通过以下命令验证签名：

```
gpg --verify message.asc
```

如果你确实签署了该消息，输出的最后一行将说明这是一个有效的签名。

### 加密和解密文档

要加密发送给特定接收者的消息，你可以使用 GPG 的 `--encrypt`（或 `-e`）命令。以下是如何使用 US-CERT 的 GPG 密钥加密一条发给 US-CERT 的消息：

```
gpg -o message.gpg -e -r us-cert@us-cert.gov message
```

该消息使用 US-CERT 的公钥进行加密（没有签名，但你可以通过 `-s` 命令添加签名）。

当 US-CERT 接收到 `message.gpg` 文件后，接收者必须使用 US-CERT 的私钥对其进行解密。以下是 US-CERT 的某人可以使用的命令：

```
gpg -o message --decrypt message.gpg
```

然后 GPG 会提示输入口令以解锁 US-CERT 的私钥，解密消息，并将输出保存到名为 `message` 的文件中。

如果你只是想加密一个文件，且不需要其他人解密该文件，你可以使用 GPG 执行所谓的 *对称加密*。在这种情况下，你提供口令来加密文件，使用以下 GPG 命令：

```
gpg -o secret.gpg -c somefile
```

GPG 会提示你输入口令并要求你重复输入口令（以确保你没有输错）。然后 GPG 使用从口令生成的密钥来加密该文件。

