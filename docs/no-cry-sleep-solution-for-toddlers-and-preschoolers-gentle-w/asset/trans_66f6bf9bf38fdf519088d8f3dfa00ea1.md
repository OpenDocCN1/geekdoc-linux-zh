
## GNU隐私卫士

为了保护您通过电子邮件发送的消息，大多数 Linux 发行版提供了 GNU隐私卫士（GnuPG）加密和身份验证功能。GnuPG 是 GNU 开源软件，其工作原理与良好隐私（PGP）加密非常相似。使用 GnuPG，您既可以加密消息，也可以对其进行数字签名——从而保护消息并验证其来自您。目前，Evolution 和 KMail 都支持 GnuPG 加密和身份验证。在 Evolution 中，您可以从“安全”菜单选择 PGP 加密和签名来使用 GnuPG（在 Red Hat Linux 中，PGP 选项即使用 GnuPG）。在 KMail 中，您可以在“选项”窗口的“安全”面板中选择要使用的加密方式。

GNU隐私卫士（GPG）操作通过 gpg 命令执行，该命令使用命令和选项来执行任务。表16-1中列出了常用的命令和选项。某些命令和选项具有只使用一个连字符的短格式。通常使用两个连字符。第一次使用 gpg 时，系统会在您的主目录中创建一个 .gnupg 目录，其中包含一个名为 options 的文件。.gnupg/options 文件包含 GPG 操作的注释默认选项（在下一个版本 1.2 中改为 .gnupg/gpg.conf）。您可以编辑此文件，取消注释或更改任何希望为 GPG 实现的默认选项。您可以使用不同的选项文件，并在调用 gpg 时使用 --options 参数来指定它。有用的选项包括密钥服务器条目。

**图16-1 公钥加密和数字签名**

![](img/6c226e8ba1efd427dec3bf582418d33f_324_0.png)

.gnupg 目录还保存加密文件，例如用于存放私钥的 secring.gpg（私钥环）、用于存放公钥的 pubring.gpg（公钥环），以及 trustdb.gpg（受信任密钥的数据库）。

**表16-1 GPG命令和选项（续）**

| GPG 命令 | 描述 |
| --- | --- |
| -s, --sign | 对文档进行签名，创建签名。可与 --encrypt 结合使用。 |
| --clearsign | 创建明文签名。 |
| -b, --detach-sign | 创建分离签名。 |
| -e, --encrypt | 加密数据。可与 --sign 结合使用。 |
| --decrypt [file] | 解密文件（如果未指定文件，则解密 stdin），并将其写入 stdout（或通过 --output 指定的文件）。如果解密后的文件已签名，则验证该签名。 |
| --verify [sigfile] [signed-files] | 验证已签名文件。签名可以包含在文件中，也可以是单独的分离签名文件。 |
| --list-keys [names] | 列出密钥环中的所有密钥或指定密钥。 |
| --list-public-keys [names] | 列出公钥环中的所有密钥或指定密钥。 |
| --list-secret-keys [names] | 列出您的私有（秘密）密钥。 |
| --list-sigs [names] | 列出您的密钥及其所有签名。 |
| --check-sigs [names] | 列出密钥及其签名，并验证这些签名。 |
| --fingerprint [names] | 列出指定密钥的指纹。 |
| --gen-key | 生成一组新的私钥和公钥。 |
| --edit-key name | 编辑您的密钥。使用命令执行大多数密钥操作，例如用 sign 对密钥签名，或用 passwd 更改您的口令。 |
| --sign-key name | 使用您的私钥对公钥签名。等同于 --edit-key 中的 sign。 |
| --delete-key name | 从公钥环中移除公钥。 |
| --delete-secret-key name | 从私钥环和公钥环中移除私钥和公钥。 |
| --gen-revoke | 为您的密钥生成撤销证书。 |
| --export [names] | 从您的密钥环中导出指定密钥。不带参数时，导出所有密钥。 |
| --send-keys [names] | 导出指定密钥并将其发送到密钥服务器。必须使用 --keyserver 选项来指定该密钥服务器的名称。 |
| --import [files] | 将文件中的密钥导入到您的公钥环中。 |

| GPG 选项 | 描述 |
| --- | --- |
| -a, --armor | 创建 ASCII 装甲输出，即加密数据的 ASCII 版本。 |
| -o, --output file | 将输出写入指定文件。 |
| --default-key name | 指定用于签名的默认私钥。 |
| --keyserver site | 用于查找不在您密钥环上的公钥的密钥服务器。也可以指定要将您的公钥发送到的站点。host -l pgp.net \| grep www.keys 将列出密钥服务器。 |
| -r, --recipient names | 使用指定用户的公钥为该用户加密数据。 |
| --default-recipient names | 指定用于加密数据的默认收件人。 |

### GnuPG 设置：gpg

在使用 GnuPG 之前，您必须生成私钥和公钥。在命令行（终端窗口）中，输入带 --gen-key 命令的 gpg 命令。随后 gpg 程序会提示您选择不同的选项来创建私钥和公钥。您可以查看 gpg 手册页以了解如何使用 gpg 程序。

```
gpg --gen-key
```

### 创建您的密钥

首先，系统会要求您选择要创建的密钥类型。通常，您只需选择默认条目，按 ENTER 键即可。然后选择密钥大小，通常为默认的 1024。接着指定密钥的有效期——通常设置为无过期。系统还会要求您输入用户 ID、注释和电子邮件地址。按回车键，系统将依次提示您输入各项。这些元素中的任何一个都可以用作密钥名称，它们共同标识该密钥。在执行某些 GPG 任务（如签名密钥或创建撤销证书）时，您需要使用密钥名称。例如，以下元素为用户 Richard Petersen 创建了一个密钥，其注释为“author”（作者），电子邮件地址为 richlp@turtle.mytrek.com：

```
Richard Petersen (author) <richlp@turtle.mytrek.com>
```

