

要检查文件的数字签名，请使用带有 `--verify` 选项的 `gpg` 命令。这假设发送方已对该文件进行了签名。

```bash
$ gpg --verify myfile.asc
```

## 解密数字签名

您需要拥有签名者的公钥才能解码并检查数字签名。如果没有，您将收到一条消息，提示未找到公钥。在这种情况下，您必须先获取签名者的公钥。您可以访问一个您认为可能拥有该公钥的密钥服务器，或者直接从网站或签名者处请求公钥。然后按照前述方法导入该密钥。

## 对消息进行签名

对文件进行签名时，您无需加密该文件。数字签名是一个独立的组件。您可以将签名与给定文件结合，也可以单独生成。要将签名与文件结合，您需要生成一个新版本，该版本同时包含这两者。使用 `--sign` 或 `-s` 选项来生成包含数字签名的文档版本。在以下示例中，`mydoc` 文件被数字签名，生成的 `mydoc.gpg` 文件同时包含原始文件和签名。

```bash
$ gpg -o mydoc.gpg --sign mydoc
```

相反，如果您只想生成单独的签名文件，则使用 `--detach-sig` 命令。这样做的好处是不必生成原始文件的完整副本，原始文件保持原样。签名文件通常具有 `.sig` 扩展名。在以下示例中，用户为 `mydoc2` 文件创建了一个名为 `mydoc2.sig` 的签名文件。

```bash
$ gpg -o mydoc2.sig --detach-sig mydoc2
```

若要使用分离签名验证文件，接收方用户必须同时指定签名文件和原始文件。

```bash
$ gpg --verify mydoc2.sig mydoc2
```

要验证可信签名，您可以使用 `gpgv`。

您还可以生成清晰签名，用于文本文件。*清晰签名* 是签名的文本版本，可以附加到文本文件。文本文件可以进一步通过任何文本编辑器进行编辑。使用 `--clearsign` 选项创建清晰签名。以下示例创建一个名为 `mynotice.txt` 的文本文件的清晰签名版本。

```bash
$ gpg -o mysignature.txt --clearsign mynotice.txt
```

> **注意** 在 www.gnupg.org 上，GnuPG 有许多图形用户界面（GUI）前端和过滤器。GPA（GNU Privacy Assistant）提供了一个基于 GNOME 的前端，可以轻松加密和解密文件。您可以选择要编码的文件，选择收件人（要使用的公钥），并添加数字签名（如果愿意）。您还可以使用 GPA 解码接收到的编码文件。您还可以管理您的公钥集合——即密钥环文件中的密钥。

> **提示** 隐写术是一种加密形式，它将数据隐藏在其它类型的对象中，例如图像。您可以使用 JPEG Hide and Seek 软件（PJHS）在 JPEG 图像（*jphide* 和 *jpseek*）中编码和检索数据。更多详情请参见 linuxu01.gwgud.de/alatham/stego.html。

## 检查软件包数字签名

数字签名非常有效的用途之一是验证软件包是否未被篡改。软件包在传输过程中可能会被拦截，其中的某些系统级文件可能会更改或被替换。来自您的发行版的软件包，以及由知名 GNU 和 Linux 项目提供的软件包，都经过数字签名。签名提供了修改摘要信息，用于检查包的完整性。数字签名可能随包文件一起提供，也可能作为单独的文件发布。您使用带有 **--verify** 选项的 **gpg** 命令来检查文件的数字签名。

> **提示** Fedora 和 Red Hat 会将 Red Hat 公钥安装在 RPM 文档目录中，文件名为 **RPM-GPG-KEY**.\$usr/share/doc/rpm-4.4.2。Fedora 和 Red Hat 使用此密钥在安装过程中检查 RPM 软件包。版本号会随未来的 RPM 版本发布而更改。

### 导入公钥

然而，首先需要确保您拥有签名者的公钥。数字签名是使用软件发行商的私钥加密的。该发行商就是签名者。一旦您拥有该签名者的公钥，您就可以检查从他们那里接收的任何数据。对于诸如 Fedora、**rpm.livna.org** 或 **freshrpms.net** 等软件仓库，当您首次尝试从其网站安装任何软件时，系统会提示您安装其公钥。一旦安装了密钥，您就不需要再次安装。使用 Yum 时，这通常只是一个安装密钥的提示，请求输入 y 或 n 进行确认，或者请求点击 OK 的对话框。诸如 Livna 和 **freshrpms.net** 之类的仓库会将它们的密钥包含在其 Yum 配置软件包中。如果您愿意，还可以从它们的网站手动下载并安装。

对于软件发行商，您可以从其网站或密钥服务器下载其公钥。一旦拥有其公钥，您就可以检查他们分发的任何软件。

如前所述，您可以从 Red Hat 网站的安全资源页面下载 Red Hat 公钥，或者使用安装在 **RPM** 文档目录中的版本。一旦获得公钥，您可以使用 **-import** 选项将其添加到您的密钥环中，并指定您给下载密钥文件的名称（在此情况下为 **myredhat.asc**）：

```bash
# gpg --import redhat.asc
gpg: key CBA29BF9: public key imported
gpg: Total number processed: 1
gpg: imported: 1 (RSA: 1)
```

若要改为从密钥服务器下载，您使用 **--keyserver** 选项和密钥服务器名称。

要导入 RPM 目录中的 Red Hat 公钥，您需要指定 **RPM-GPG-KEY** 文件。这是由 Red Hat 发行版在您 DVD-ROM 或 CD-ROM 上提供的密钥。尽管该密钥在安装过程中使用，但在软件包安装完成后，若要再次验证软件包，必须导入该密钥。

```bash
# rpm --import /usr/share/doc/rpm-4.2.2/RPM-GPG-KEY
```

### 验证公钥

如果需要，您可以使用 **--fingerprint** 选项来检查密钥的有效性。如果您确信密钥有效，则可以随后使用 **--sign-key** 命令对其进行签名。在以下示例中，用户使用密钥名称中的字符串 "Red Hat" 来引用 Red Hat 密钥，对该密钥进行签名。用户还被要求输入其密码短语，以允许使用其私钥对 Red Hat 公钥进行签名。

```bash
# gpg --sign-key "Red Hat"
# gpg 1024R/CBA29BF9  created: 1996-02-20  expires: never  trust: -/g
(1)  Red Hat Software, Inc. <redhat@redhat.com>
# gpg 1024R/CBA29BF9  created: 1996-02-20  expires: never  trust: -/g
Fingerprint: 6D 9C BA DF D9 60 52 06 23 46 75 4E 73 4C FB 50
Red Hat Software, Inc. <redhat@redhat.com>
# gpg Are you really sure that you want to sign this key
with your key: "Richard Petersen (author) <richlp@turtle.mytrek.com>"
Really sign? yes
You need a passphrase to unlock the secret key for
user: "Richard Petersen (author) <richlp@turtle.mytrek.com>"
1024-bit DSA key, ID 73F0A73C, created 2001-09-26
Enter passphrase:
# gpg
```

### 检查 RPM 软件包

来自 Fedora 等任何 Yum 仓库的 RPM 软件包会自动检查公钥。如果您单独下载了 RPM 软件包，则可以手动检查该包。一旦拥有软件提供方的公钥，您就可以使用 **rpm** 命令和 **-K** 选项检查 Fedora 或 Red Hat 的任何 RPM 软件包。以下示例检查 xcdroast 软件包的有效性：

```bash
# rpm -K xcdroast-0.98alpha9-1.i386.rpm
xcdroast-0.98alpha9-1.i386.rpm: md5 OK
```

许多以压缩存档形式（**.tar.gz** 或 **.tar.bz2**）提供的软件包会在以 **.sig** 扩展名结尾的单独文件中提供签名。要检查这些文件，您使用带有 **--verify** 选项的 **gpg** 命令。例如，最新的 Sendmail 软件包以压缩存档 **.tar.gz** 的形式分发。其数字签名在单独的 **.sig** 文件中提供。首先，您需要下载并安装从 Sendmail 网站获取的 Sendmail 软件公钥（密钥名称中可能包含年份）。

```bash
# gpg --import sendmail2006.asc
```

然后，您应该对刚刚导入的 Sendmail 公钥进行签名。在此示例中，使用了电子邮件地址作为密钥名称。

```bash
# gpg --sign-key sendmail@Sendmail.ORG
```

您还可以检查密钥的指纹以进行额外验证。

