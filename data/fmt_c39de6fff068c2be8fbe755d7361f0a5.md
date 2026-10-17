
如果你正在升级软件包，旧配置文件将被重命名为带有`.rpmsave`扩展名，新文件将取代其位置。同样，你将收到一条警告消息，告知此事已经发生。

如果你正在移除软件包，且工具检测到配置文件已被修改，它会向你发出警告，并保留该文件的一个带有`.rpmsave`扩展名的版本——因此，如果你需要它，它仍然可用。

这种情况不太可能经常发生，但现在你已经意识到了这些问题，以防遇到这种情况。请记住安装和升级处理配置文件之间的区别。这将使我们受益匪浅，接下来我们将查看命令行软件包安装程序（`RPM`）。

## `RPM` 命令行工具

到目前为止，我们已经讨论了如何使用 `Red Hat` 的图形化软件包管理工具来安装和移除软件包。虽然这个工具使用起来很简单，但它在功能上有所欠缺。例如：

- 它无法通过网络、`FTP` 或 `HTTP` 连接安装软件包。
- 它不显示软件包中文件安装的位置。
- 它缺乏查询系统中已安装的特定软件包的能力。
- 它不提供 `RPM` 软件包的全部详细信息——例如供应商、构建日期、签名、描述等。
- 它没有验证软件包的功能。这意味着它无法比较从软件包安装的文件信息（如大小、`MD5` 校验和、权限、类型、所有者和组）与原始软件包中的相同信息。
- 它不显示产品中的所有可用软件包。因此，你并不总是知道是否已经获取了完整的东西。

`RPM` 命令行界面工具（`RPM`）提供了软件包管理器局限性的解决方案。`RPM` 非常多功能，可以用于多种方式来操作软件包。在本节的其余部分，我们将查看你很可能想要执行的一些最常见任务，并考虑如何最好地完成它们。

> *输入`man rpm`可在命令提示符下找到`RPM`所有选项的完整详情；因为选项非常多，我们在这里只介绍最常用的部分。*

### 查询软件包

让我们从讨论**查询**软件包开始。`RPM` 在一个数据库中保留系统中所有已安装软件包的记录。通过查询数据库，你可以获得系统中已安装软件包的完整列表。如果你愿意，你可以进一步查询每个单独的软件包，以获取有关其自身的更多详细信息。

基本查询的语法如下：

```
rpm -q [options] <filename>
```

## 试一试：查询 `RPM` 以获取有关软件包的信息

- 1. 打开一个终端窗口（通过选择 **主菜单 | 系统工具 | 终端**）。

- 2. 只有具有 `root` 权限的用户才能执行 `RPM` 软件包操作。因此，如果您没有以 `root` 身份登录，请立即使用`su`命令进行登录：

```
$ su -
Password:
```

- 3. 将您的 `Red Hat` 系统中的 `CD 2` 插入并挂载后，输入以下内容，切换到软件包目录：

```
# cd /mnt/cdrom/RedHat/RPMS/
```

- 4. 现在，让我们查找`lynx`软件包（`Lynx` 是一个基于文本的浏览器）的信息。为此，请在命令行中输入以下内容：

```
# rpm -qip lynx-2.8.5-11.i386.rpm
```

在这里，`-qip`表示命令选项（我们稍后会更详细地讨论它们），而`lynx-2.8.5-11.i386.rpm`是我们感兴趣的 `RPM` 软件包文件。片刻之后，您应该会看到以下响应：

```
Warning: lynx-2.8.5-11.i386.rpm: V3 DSA signature: NOKEY, key ID db42a60e
Name   : lynx                    Relocations: (not relocatable)
Version  : 2.8.5                   Vendor: Red Hat, Inc.
Release  : 11                      Build Date: Sat 25 Jan 2003 05:10:43 GMT
Install Date: Thu 15 May 2003 11:41:58 BST   Build Host: porky.devel.redhat.com
Group  : Applications/Internet   Source RPM: lynx-2.8.5-11.src.rpm
Size   : 4021040                 License: GPL
Signature : DSA/SHA1, Mon 24 Feb 2003 06:34:45 GMT, Key ID 219180cddb42a60e
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL    : http://lynx.isc.org/
Summary  : A text-based Web browser.
Description :
Lynx is a text-based Web browser. Lynx does not display any images,
but it does support frames, tables, and most other HTML tags. One
advantage Lynx has over graphical browsers is speed; Lynx starts and
exits quickly and swiftly displays webpages.
```

*注意到第一行的警告了吗？我们将在本章后面涵盖验证部分时对此进行解释。*

很有用，不是吗？您可以使用这些信息来确保您安装的是您认为要安装的内容，并检查您是否拥有正确版本的软件。

- 5. `RPM` 也可以用于查询系统中已安装的具体软件包。以 `root` 身份发出以下命令：

```
rpm -qi lynx
```

在这里，`-qi`表示命令选项，而`lynx`是我们感兴趣的 `RPM` 软件包文件名。片刻之后，您应该会看到以下响应：

```
Name       : lynx
Version    : 2.8.5
Release    : 11
Install Date: Mon 26 May 2003 14:50:02 BST
Group      : Applications/Internet
Size       : 4021040
Signature  : DSA/SHA1, Mon 24 Feb 2003 06:34:45 GMT, Key ID 219180cddb42a60e
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL        : http://lynx.isc.org/
Summary    : A text-based Web browser.
Description:
Lynx is a text-based Web browser. Lynx does not display any images,
but it does support frames, tables, and most other HTML tags. One
advantage Lynx has over graphical browsers is speed; Lynx starts and
exits quickly and swiftly displays webpages.
Relocations: (not relocatable)
Vendor: Red Hat, Inc.
Build Date: Sat 25 Jan 2003 05:10:43 GMT
Build Host: porky.devel.redhat.com
Source RPM: lynx-2.8.5-11.src.rpm
License: GPL
```

- 6. 现在让我们尝试一些略有不同但同样有用的操作。发出以下命令（仍然以 `root` 身份）：

```
# rpm -qa
```

此命令查询您系统上安装的所有软件包；响应应该类似于以下内容：

```
rpmi04-python-4.0.4-8x.27
ksymoops-2.4.5-1
libgail9-0.19.2-4
setup-2.5.25-1
...gnome-media-2.2.1.1-4
redhat-switch-printer-0.5.16-1
sharutils-4.2.1-14
vnc-server-3.3.3r2-47
```

- 7. 这是另一个示例。您很可能会遇到需要知道拥有系统中某个特定命令的软件包的情况。例如，让我们找出哪个软件包拥有`/usr/bin/lynx`命令。为此，请在命令行中输入以下内容：

```
# rpm -qf /usr/bin/lynx
```

您应该得到以下响应：

```
lynx-2.8.5-11
```

因此，每当用户调用命令`/usr/bin/lynx`时，系统使用的就是`lynx-2.8.5-11`软件包。

- 8. 最后，`RPM` 还提供了一个命令，允许我们查找包含在 `RPM` 软件包中的所有文件列表。让我们看看`samba-client`软件包中包含了哪些文件…… 为此，请输入以下内容：

```
# rpm -ql lynx
```

这是您应该得到的响应：

```
/etc/lynx-site.cfg
/etc/lynx.cfg
/etc/lynx.cfg.cs
/etc/lynx.cfg.ja
/etc/lynx.cfg.sk
/usr/bin/lynx
......
/usr/share/locale/sl/LC_MESSAGES/lynx.mo
/usr/share/locale/sv/LC_MESSAGES/lynx.mo
/usr/share/man/man1/lynx.1.gz
```

#### 工作原理

当我们使用 `RPM` 命令行选项查询 `RPM` 软件包文件时，它会显示软件包的信息，如名称、版本、发行版、组、摘要和描述。查询的确切类型和结果输出的格式取决于我们指定的命令选项：

- 在上述示例的五个查询中，我们都使用了`-q`。`q`表示我们要进行查询。
- 在步骤 4 和 5 中，我们使用了`-qip`。`p`表示我们正在查询一个软件包，而`i`表示我们要查看软件包信息。
- 在步骤 6 中，我们使用了`-qa`。`a`表示我们要查询*所有*当前已安装的软件包。
- 在步骤 7 中，我们使用了`-qf`。`f`表示我们希望查询拥有指定文件的软件包。
- 最后，在步骤 8 中，我们使用了`-ql`。`l`表示我们希望查询包含在指定软件包中的文件列表。

### `RPM` 软件包安全性

多年来 `RPM` 已经发布了多个版本，最新版本（其中一个版本随您的系统附带）有一些新功能。对我们感兴趣的一个新功能是在查询、安装或升级软件包时，`RPM` 现在会检查软件的**签名**。

检查软件包的签名可以确保它来自可信的来源。所有官方 `Red Hat` 软件包都由 `Red Hat` 使用其 `GnuPG` 密钥进行签名，`RPM` 会将软件包的 `GnuPG` 签名与 `Red Hat GnuPG` 密钥进行比对，以确保软件包声称其为何种类型。如果您没有安装用于验证签名的适当密钥，您将收到类似以下的警告消息（我们之前提到过，还记得吗？）：

```
warning: lynx-2.8.5-11.i386.rpm: V3 DSA signature: NOKEY, key ID db42a60e
```

警告消息的具体内容取决于具体情况。例如，如果 `RPM` 无法验证软件包的 `GnuPG` 签名，您将看到以下错误消息：

```
error: V3 DSA signature: BAD, key ID 0352860f
```

相反，如果 `RPM` 找不到用于验证软件包签名的适当密钥，您将收到此警告：

```
warning: V3 DSA signature: NOKEY, key ID 0352860f
```

`GnuPG` 签名是非常难以伪造的数字签名。签名是使用唯一的秘密密钥创建的，并可以由接收者使用公钥进行验证。数字签名对文档进行时间戳，如果有人试图篡改或修改它，签名验证将失败。

#### `Red Hat GNU Privacy Guard (GPG)` 密钥

要在已安装的系统上安装 `Red Hat` 的 `GPG` 密钥，请发出以下命令：

```
# rpm --import /usr/share/rhn/RPM-GPG-KEY
```

或者，使用以下内容从 `CD-ROM` 安装它们（确保驱动器中放的是正确的光盘）：

```
# rpm --import /mnt/cdrom/RPM-GPG-KEY
```

这些命令将把 `Red Hat` 的公共 `GPG` 密钥安装到您的系统上。您也可以以类似的方式导入其他供应商的 `GnuPG` 密钥；只需将文件名更改为他们提供给您的那个。

要显示用于系统中 `RPM` 软件包验证的所有已安装 `GnuPG` 密钥列表，请发出以下命令：

```
# rpm -qa gpg-pubkey*
gpg-pubkey-db42a60e-37ea5438
```

这将返回一个结果列表。如果您已安装 `Red Hat` 密钥，您应该会在其中看到以下内容：

```
gpg-pubkey-db42a60e-37ea5438
```

通过执行以下命令，我们可以获取 `Red Hat GPG` 键的更完整详细信息：

```
# rpm -qi gpg-pubkey-db42a60e-37ea5438
```

在上述命令中，请注意`gpg-pubkey-db42a60e-37ea5438`是 `Red Hat GnuPG` 密钥的名称，它是从命令`rpm -qa gpg-pubkey*`的输出中获取的。

## 第 4 章

这将产生以下响应——相当详细，不是吗？最重要的是，它揭示了供应商名称和签名日期，如果你系统中有一个密钥但不确定它是谁的，或者它是否仍在有效期内，这些信息会很有用：

| 字段 | 值 | 字段 | 值 |
| :--- | :--- | :--- | :--- |
| `Name` | `gpg-pubkey` | `Relocations` | (not relocatable) |
| `Version` | `db42a60e` | `Vendor` | (none) |
| `Release` | `37ea5438` | `Build Date` | Sun 20 Apr 2003 14:10:53 BST |
| `Install Date` | Sun 20 Apr 2003 14:10:53 BST | `Build Host` | `localhost` |
| `Group` | `Public Keys` | `Source RPM` | (none) |
| `Size` | 0 | `License` | `pubkey` |
| `Signature` | (none) | | |

摘要：`gpg(Red Hat, Inc <security@redhat.com>)`

描述：

```
-----BEGIN PGP PUBLIC KEY BLOCK----
版本：rpm-4.1 (beecrypt-2.2.0)：
mQGiBDFqVd9gRBADBKr3Bl6PO8BQOHoSJoD6p9U7Yv17pjTZqioviPwXFc+DCW4du8HQZcxzA5
7m88sAlLlKiF9x9coJuHDZm130+p5Bgn9mWSWHLaB3R31KXdpQXYccovTMQgx6wvYRG15Psw8QyD
LhjVfUF51X14Xt6bpPbWUB6vY2KZ5Z37pB1UUOiMrx3wCgobNVYEDGawYJucc5z5ZB1oF/41G8kE
AKii6q7Gu/vhXxNLS6mi5oNnPvybyngiw/23dKjSZGV7rKANEK2mxgi1VB+vc/uC4k49XJJ
fCZg1igusPFV3G5a+Y/7jsiLktQvcIILPncoTdiV+ENmHRsBdidP9DzKBVbgWnSDnqG6KrZ7
T6AL274VMpjGxxxWU6vV2xSWXCLPA/9P/vt1mA8CZNjxggT-K5GGTLDNJ/cmHuvu5VnFmwFg4b
/VGo2Jr8mhLUgo1EbE6zeGMaZbUcpDco8D5fiQmfTs+ ++pC6pRJLJKzKe1/32N2w4qzPcR
MCiBURxESPjCLd4Y5+rpO8E4K4OHC/4BuHN931iCScPlOcrWsQZ7UdqfQ5LQlUmVkIEhhdCwg
SW5jIDxzdXNlcm1lOeUBvZW8RYXQYxY29+PoHVBMRaGAvaBQJ361Q4AwsKAwMLvAWpDIGBAh
AAOJCEGRGm3b0gqvOesBQAnRVTg7BZ5HmllPHCap8FPedKdKi2AJ9ao8BSxLDmPOEF175mpTr
KYHFPr6cRDQQ361RlyEagAokgjX2Jb+3bZsk8JrAR0RIXBHD05UlMh27qFzLbT6npXwXYIotVn
OKZ/+1MDj+oEBlA2au40dddYalWp06v3d+Xy50t+5ab22fiQ2dh7wCwqxRkzR+/H5TlbmG+
hv+TdY1fqIXOWEfOXMtWWGSSVwyUsmN3yj3L01a8+QqSCstCauD20FoIGHwnb/glHu1NmNE
S6uDUqjFBE6EANgQhPcoOoIhHJ2oIO8ujQjt+vNarU8Hj/8/izqv5e7MxOGvSJKe/WX3StB
B/t/WYutpyl2wh1JJsFDblLv/t8Co2tXpJgx5mVA3RK3l+/Ta+On+1iEUuLoB+1lfft7GV/0cAc
waZDBQyrE4SKQRWamBS8KX0lOmYGmpXvPhYHInbDMLOkrwMTNnqSFRooJJRhexDxWmpTWK
ti/PRr9L2J1lP2ed0Xyzm8+v3gLYouliSba+8GLy+ p1T2QoSOGasVfZ7AQ80XbWJyRymX
Qp+8DeTeOTELKOL2/itDOpGHM07SsVVOR6cmX4ViRrcWB5KejaNVdrE54XfDOD4NmGwi63u
```
