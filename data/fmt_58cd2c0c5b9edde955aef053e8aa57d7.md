
```bash
# tar -cvzf /tmp/backup.gz /etc
# gpg -c /tmp/backup.gz
Enter passphrase: ********
Repeat passphrase: ********
# gpg -d /tmp/backup.tar.gz
Enter passphrase: ********
```

解密文件使用 `gpg`。例如，如果你将文件交给另一个用户，他们可以运行 `gpg -d` 并提供密码。结果是原始文件被解密并复制到 `/tmp/backup.gz`。如果系统上运行着 `gpg-agent`，密码会被缓存，因此无需输入密码即可解密文件。

# 第23章：理解高级 Linux 安全

对称密钥加密相当且易于理解。非对称加密复杂得多，往往引起困惑。

## 非对称密钥加密

非对称加密也称为私钥/公钥加密，使用称为密钥对的两个密钥。密钥对由公钥和一个私钥组成。公钥不需要保密。私钥需要保密。非对称加密的基本思想如图 23.2 所示。明文使用密钥对的公钥加密。加密后的文件可以安全地传输给另一个人。解密文件使用私钥。因此，使用公钥加密的数据只能用其私钥解密。非对称加密的优点是安全性提高。缺点是速度和密钥管理。

图 23.2 基本非对称加密

你可以使用 `gpg` 在 Linux 系统上执行非对称加密。它是一个多功能的加密工具。在加密文件之前，你必须先创建密钥对和一个“密钥环”。接下来的示例使用了 `gpg --gen-key` 命令。该命令根据用户的规范为用户 创建公钥/私钥对。它还生成了一个存储密钥的密钥环。

```bash
$ gpg --gen-key
gpg (GnuPG) 2.0.22; Copyright (C)
2013 Free Software Foundation, Inc.

Please select what kind of key you want:
(1) RSA and RSA (default)
(2) DSA and Elgamal
(3) DSA (sign only)
(4) RSA (sign only)
Your selection? 1
RSA keys may be between 1024 and 4096 bits.
What keys do you want? (2048) 2048
Requested keysize 2048 bits
Please specify how long the key should be valid.
0 = key does not expire
<n> = key expires in n days
<w> = key expires in n weeks
<m> = key expires in n months
<y> = key expires in n years
Key is valid for? (0) 7
Key expires on Mon 05 Dec 2016 03:55:29 AM EST
Is this correct? (y/N) y

You need a user ID to identify your key.

Real name: John Doe
Email address: jdoe@example.com
Comment: The User
You selected the USER-ID:
"John Doe (The User) <jdoe@gmail.com>"

Change (N)ame, (C)oment, or (E)mail or (Q)uit? O
You need a passphrase to protect your secret key.
Enter passphrase: ***********
Repeat passphrase: ********
```

gpg: `/home/johndoe/.gnupg/trustdb.gpg`: trustdb created

gpg: key `3B2E4D6D` marked as ultimately trusted

public and secret created and signed.

```
pub 2048/3B2E4D6D 2015-01-08 [expires: 2015-12-15]

Key fingerprint = E202 8E43 3784 69EF 118B

275C BA45 7DBF 3B2E 46D5

uid John Doe (The User) <jdoe@example.com>

sub 2048/0F0E0672 2015-12-08 [expires: 2016-12-15]
```

## 第23章：理解高级 Linux 安全

在上一个示例中，`gpg2` 工具要求提供几项规范以生成所需的私钥/公钥：

- 加密算法——示例中选择了 `RSA`。
- 位数——密钥越长，安全性越高。
- 有效期——示例中选择了七天。
- 用户 ID `UID`——这用于标识公钥/私钥对中的密钥部分。
- 密码——这用于识别和保护公钥/私钥对中的私钥。

注意：从公钥推导出私钥是非常困难的，甚至在数学上是不可能的。然而，人们发现了一个潜在的漏洞。密钥对是通过两个随机数生成的。其原理是标识出两个密钥。安全研究人员发现，生成的随机数并不十分随机。因此，可能会与互联网上的其他人拥有相同的密钥对。如果你与他人共享密钥对，你就有能力解密他们公钥加密的消息。因此，你至少应该使用 2048 位的密钥来减少这种潜在情况造成的损害。

用户 `johndoe` 可以使用 `gpg2 --list-keys` 命令检查他的密钥环，如下所示所示。注意密钥的用户 ID `UID` 是按照创建时的状态显示的，包含了 `johndoe` 的真实姓名和电子邮件地址。

```
$ gpg2 --list-keys

/home/johndoe/.gnupg/pubring
```

| pub 2048/3B2BE46DS 2015-12-08 [expires: 2016-12-15] <johndoe@example.com> |
| uid John Doe (The User) <johndoe@example.com> |
| sub 2048/F0E0672 2015-12-15 [expires: 2016-12-15] |

生成密钥对和密钥环后，就可以对文件进行加密和解密。首先，必须从密钥环中提取公钥以便共享。在接下来的示例中，使用 `gpg2` 工具从 `johndoe` 的密钥环中提取公钥。提取出的密钥被放入文件中共享。文件名可以是你想要的任何名称。在这种情况下，用户 `johndoe` 选择了文件名 `JohnDoe.pub`。

```
$ gpg2 --export John Doe > JohnDoe.pub

$ ls -l

JohnDoe.pub
```

包含公钥的文件可以通过任何方式共享。公钥可以作为邮件附件发送，也可以发布在网页上，没有必要隐藏它。在接下来的示例中，`johndoe` 已将包含其公钥的文件交给了 `jill`。`jill` 使用 `gpg2 --import` 命令将 `johndoe` 的公钥添加到她的密钥环中。用户 `jill` 使用 `gpg2 --list-keys` 命令查看她的密钥环，以验证 `johndoe` 的公钥已已添加。

## 第五部分：学习安全技术

```
$ ls *.pub

JohnDoe.pub

$ gpg2 --import JohnDoe.pub

gpg: directory '/home/jill/.gnupg' created

...

gpg: key 3B2E46DS:

    public key "John Doe (The User) <jdoe@example.com> imported

    gpg: Total number processed: 1

        imported: 1 (RSA: 1)

$ gpg2 --list-keys

/home/jill/.gnupg/pubring.pub
```

pub   2048R/3B2E46DS 2016-12-12 [expires: 2016-12-15]
uid   John Doe (The User) <jdoe@example.com>
sub   2048R/0F0E672 2016-12-08 [expires: 2016-12-15]

密钥添加到密钥环后，可以使用公钥为公钥的所有者加密数据。在下面的示例代码中，请注意以下点：

- `jill` 为用户 `johndoe` 创建了一个文本文件 `MessageForJohn.txt`。
- 她使用他的公钥对文件进行加密。
- 加密后的文件 `MessageForJohn` 通过 `--out` 选项创建。
- `--recipient` 选项仅通过密钥 UID 中引号中的真实部分 "John Doe" 来识别 `johndoe` 的公钥。

```
$ gpg2 --out MessageForJohn --recipient "John Doe" \
--encrypt MessageForJohn.txt

$ ls
```
