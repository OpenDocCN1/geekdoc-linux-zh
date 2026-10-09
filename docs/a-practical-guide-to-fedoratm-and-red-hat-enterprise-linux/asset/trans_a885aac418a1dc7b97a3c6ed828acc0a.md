

当 Sam 获取该文件时，他会对其进行解密，并将输出（即解密后的文件）发送到 memoC。由于该文件是使用 Sam 的公钥加密的，因此 Sam 必须提供其私钥来解密它。在输出的末尾，`gpg` 确认 Max 的签名有效。

```
$ gpg --output memoC_memoC.gpg

You need a passphrase to unlock the secret key for:
user: "Sam Smith (Sam the Great) <sam@example.com>"
2048-bit RSA key, ID 5698A710, created 2013-10-03 (main key ID D26C84B3)
Enter passphrase:

`gpg`: encrypted with 2048-bit RSA key, ID 5698A710, created 2013-10-03
"Sam Smith (Sam the Great) <sam@example.com>"
`gpg`: Signature made Thu 03 Oct 2013 12:50:51 PM PDT using RSA key ID 643E62B8
`gpg`: Good signature from "Max Wild <max@example.com>"
```

## 签名公钥

如果您相信某个公钥确实属于其声称所属的人，您可以对该公钥进行签名，以增加其可信度。对某个公钥进行签名的人越多，该公钥的可信度就越高。

密钥 ID 用于标识一个密钥。您可以使用 `gpg --list-key` 选项列出密钥环中所有密钥的 ID。以下输出显示 Sam 的密钥长度为 2,048 位，使用 RSA 加密（R），且密钥 ID 为 D26C84B3。

```
$ gpg --list-key
/home/max/.gnupg/pubring.gpg
-

pub   2048R/D26C84B3 2013-10-03
uid          Sam Smith (Sam the Great) <sam@example.com>
sub   2048R/5698A710 2013-10-03
```

在对密钥进行签名之前，请确保该密钥确实属于其声称所属的人。请从多个来源（例如密钥服务器）下载该密钥。每个密钥都有一个独特的指纹，您可以使用它来识别该密钥。使用 `gpg --fingerprint` 选项后跟密钥 ID 来显示密钥的指纹，并比较这些指纹。

```
[max@guava ~]$ gpg --fingerprint D26C84B3
pub   2048R/D26C84B3 2013-10-03
        Key fingerprint = 036A DE6E D653 3769 B243 A9EF 286A C3E0 D26C 84B3
uid          Sam Smith (Sam the Great) <sam@example.com>
sub   2048R/5698A710 2013-10-03
```

通过将指纹与密钥所有者提供的指纹进行比对来检查指纹是否正确。请使用密钥服务器、电话或打印件，而不是电子邮件，来验证指纹。一旦确定您拥有有效的密钥，就可以使用 `gpg --sign-key` 选项后跟刚刚验证的密钥 ID 来对密钥进行签名。以下示例中，Max 对位于其密钥环中的 Sam 公钥副本进行了签名。

```
[max@guava ~]$ gpg --sign-key D26C84B3

pub  2048R/D26C84B3  created: 2013-10-03  expires: never    usage: SC
                      trust: unknown  validity: unknown
sub  2048R/5698A710  created: 2013-10-03  expires: never    usage: E
[  unknown] (1). Sam Smith (Sam the Great) <sam@example.com>

pub  2048R/D26C84B3  created: 2013-10-03  expires: never    usage: SC
                      trust: unknown  validity: unknown
Primary key fingerprint:  036A DE6E D653  3769 B243  A9EE 286A C3E0 D26C 84B3

Sam Smith (Sam the Great) <sam@example.com>

Are you sure that you want to sign this key with your key "Max Wild <max@example.com>" (643E62B8)?

Really sign? (y/N) y

You need a passphrase to unlock the secret key for user: "Max Wild <max@example.com>"
2048-bit RSA key, ID 643E62B8, created 2013-10-03

Enter passphrase:
```

您使用私钥对文档进行签名，以证明该文档是由您签名的。为了访问您的私钥，`gpg` 要求您输入密码短语。

现在，当 Max 验证 Sam 的文档时，`gpg` 会检查信任数据库，显示有关 Sam 公钥的一些信息，并声明 Sam 的签名有效。

```
$ gpg --verify memoA.asc

gpg: Signature made Thu 03 Oct 2013 12:10:39 PM PDT using RSA key ID D26C84B3
gpg: checking the trustdb
gpg: 3 marginal(s) needed,  1 complete(s) needed, PGP trust model
gpg: depth: 0   valid:   1  signed:   1 trust: 0-, 0q, 0n, 0m, 0f, 1u
gpg: depth: 1   valid:   1  signed:   0 trust: 1-, 0q, 0n, 0m, 0f, 0u
gpg: Good signature from "Sam Smith (Sam the Great) <sam@example.com>"
```

## 使用密钥服务器

如果您希望与全世界共享您的公钥，可以将其上传到密钥服务器。让您的密钥存在于密钥服务器上，使得多个人对其签名变得更加容易。这也使得人们更容易找到并使用该密钥来加密他们发送给您的文档。一旦上传，该密钥将分发到所有密钥服务器；无需上传到多个服务器。keys.gnupg.net 的 URL 使用轮询 DNS，每次引用它时都会指向不同的密钥服务器。

以下示例将用户密钥环中密钥 ID 为 `99ZZ99ZZ` 的公钥发送到 keys.gnupg.net 所指向的密钥服务器。`gpg` 工具默认使用 keys.gnupg.net；您可以使用 `--keyserver` 选项指定不同的密钥服务器。`--send-keys` 选项后的参数指定了 `gpg` 要发送的、位于用户密钥环中的公钥的密钥 ID。

```
$ gpg --send-keys 99ZZ99ZZ
gpg: sending key 99ZZ99ZZ to hkp server keys.gnupg.net
```

如果您想要对存储在密钥服务器上的密钥进行签名，请先确定该密钥的密钥 ID（从朋友处获取或在密钥服务器上查找 [例如，pgp.mit.edu]）。然后下载该密钥。同样，`gpg` 默认使用 keys.gnupg.net。`--recv-keys` 选项指定了您要下载的密钥的密钥 ID。`gpg` 工具会将该密钥存储在您的密钥环中。

```
$ gpg --recv-keys 99ZZ99ZZ
gpg: requesting key 99ZZ99ZZ from hkp server keys.gnupg.net
gpg: key 99ZZ99ZZ: public key "Zach Brill <zach@example.com>" imported
gpg: Total number processed: 1
imported: 1
```

接下来，使用 `--fingerprint` 选项后跟刚下载的密钥的密钥 ID，以显示该密钥的指纹。

```
$ gpg --fingerprint 99ZZ99ZZ
pub 1024D/99ZZ99ZZ 1998-10-23
      Key fingerprint: 5E1C 544D 838F D3D0 6E09  61EA C1B2 A984 68DB 67AE
uid                 Zach Brill <zach@example.com>
sub 2048g/C348F7C0 1998-10-23
```

请始终确保您签名的密钥确实属于其声称所属的人，并且该人是真实存在的。从密钥服务器以外的来源获取该密钥的指纹，并在对密钥进行签名之前验证指纹。在以下示例中，`--sign-key` 选项后的参数指定了用户将在密钥服务器上签名的密钥的密钥 ID。由于此命令是在密钥服务器上对密钥进行签名，因此无需从您的密钥环上传该密钥。

```
$ gpg --keyserver keys.gnupg.net --sign-key 99ZZ99ZZ
pub 1024D/99ZZ99ZZ  created: 1998-10-23  expires: never     usage: SCA
 trust: unknown      validity: unknown
sub 2048g/C348F7C0  created: 1998-10-23  expires: never     usage: E
[ unknown] (1). Zach Brill <zach@example.com>

pub 1024D/99ZZ99ZZ  created: 1998-10-23  expires: never     usage: SCA
 trust: unknown      validity: unknown
Primary key fingerprint: 929Z 999Z 99ZZ 929Z 999Z  929Z 999Z 929Z 999Z 99ZZ

Zach Brill <zach@example.com>

Are you sure that you want to sign this key with your
key "Max Wild <max@example.com>" (643E6288)

Really sign? (y/N) y

You need a passphrase to unlock the secret key for
user: "Max Wild <max@example.com>"
2048-bit RSA key, ID 643E6288, created 2013-10-03

Enter passphrase:
```

## 安全资源

许多免费和商业程序可以增强系统安全性。下表 C-1 列出了其中的一些。这些网站中的许多都链接到其他有趣的网站，值得一看。

**表 C-1** 安全资源

| **工具** | **功能** | **获取方式** |
| :--- | :--- | :--- |
| AIDE | 高级入侵检测环境。与 *tripwire* 类似，具有可扩展的验证算法。 | sourceforge.net/projects/aide |
| BugTraQ | 一个经过审核的邮件列表，用于宣布和详细讨论计算机安全漏洞的所有方面。 | www.securityfocus.com/archive/1 |
| CERT | 计算机应急响应团队。关于重大安全事件的论文和数据库，以及安全工具列表。 | www.cert.org |
| dsniff | 嗅探和网络审计工具套件。免费。 | monkey.org/~dugsong/dsniff |
| GIAC | 一个安全认证和培训网站。 | www.giac.org |
| hping | 多用途网络审计和包分析工具。 | www.hping.org |
| ISC² | 根据国际标准对行业专业人士和从业人员进行教育和认证。 | www.isc2.org |
| John | John the Ripper：快速、灵活的弱密码检测器。 | www.openwall.com/john |
| Kerberos | 完整、安全的网络身份验证系统。 | web.mit.edu/kerberos/www |
| LinuxSecurity.com | 一个专注于 Linux 安全问题的扎实新闻网站。 | www.linuxsecurity.com |
| LWN.net | 所有主要 Linux 发行版的安全警报数据库。 | lwn.net/Alerts |

