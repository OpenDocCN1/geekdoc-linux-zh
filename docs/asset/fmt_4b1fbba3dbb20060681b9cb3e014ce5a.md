
gpg: `/usr/bin/gpg`

如果你没有安装 GPG，可以从 `www.rmpfind.net`、`www.gpg.org/download.html` 或随书附的 CD（`gnupg-1.0.41-i386`）下载 GPG。使用 GPG，你将能够加密文件和电子邮件。你还可以导入和导出公钥，以验证从下载的 tar 包和 RPM 文件中生成的 PGP 和 GPG 密钥。

你的决定是？1

输入一个可选的描述；并以空行结束：

>

撤销原因：密钥已泄露

这样可以吗？y

你需要一个口令来解锁用户 "jamesroot
(root) <james@root.test.com>" 的秘密密钥

1024 位 DSA 密钥，ID 3B36I145，创建于 2000-07-01

已强制执行 ASCII 铠装输出。

请将其移动到你可以隐藏起来的介质中；如果 Mallory（恶意攻击者）获取了此证书，他可以使用它使你的密钥无法使用。

将此证书打印并妥善保存是明智之举，以防你的介质无法使用。但需要注意：你机器的打印系统可能会存储这些数据并让其他人访问！

在确认你拥有密钥和撤销证书后，你现在准备好导入和导出密钥了。要导出你的密钥，请使用以下命令：

```
gpg --armor yourname.asc
```

此命令将创建一个包含你公钥的文件。你可以将此密钥分发给任何人并建立信任关系。

有了此功能，你现在可以使用 RPM 命令检查由其他人生成的签名和公钥。例如，假设你希望将 Red Hat Linux 版本更新到某个安全警报版本。要验证该包未被篡改，且它确实源自 Red Hat，你可以在 `www.redhat.com` 获取 Red Hat 的签名，并获取该网站以及你想要下载的 RPM 文件的公钥。

图 1.8 显示了 Red Hat 公钥。在撰写本文时，该密钥位于 `www.redhat.com/about/contact/redhat2.asc`。

现在你已经创建了密钥环（这是你存储想要通信的人的公钥的地方），你现在可以使用以下 GPG 命令将 Red Hat 公钥导入 GPG：

```

```

![](img/a7a9caa80ec85507179284d91e216f9f_30_0.png)

![](img/a7a9caa80ec85507179284d91e216f9f_31_0.png)

你想要导入的公钥可能有不同的扩展名。现在，对此密钥进行签名。未签名会导致在你尝试使用它时返回错误信息。确保你没有对此文件进行任何更改。一旦此密钥被导入，你需要对其进行签名。记住，你刚刚从受信任源下载了它，并且相当确定可以信任此密钥。你可以使用 `gpg --sign` 命令对其签名，也可以使用 GPG 的交互模式，如下序列操作所示：

```
gpg (GnuPG) 1.0.2; Copyright (C) 2000 Free Software Foundation, Inc.

此程序不带任何担保。

这是一项免费软件，欢迎在符合条件下重新分发它。

详情请阅 COPYING 文件。

pub 1024D/DB842A60E created: 1999-09-23 expires: never trust: -f

sub 2048g/961630A2 created: 1999-09-23 expires: never
```

Command> sign
你真的确定要用你的密钥对此密钥签名吗：
*yourkey (key) <yourkey@yoursystem.domain.com>"

![](img/a7a9caa80ec85507179284d91e216f9f_31_1.png)

真的签名吗？y
你需要一个口令来解锁用户 "jamesroot
(root) <james@root.test.com> 的秘密密钥
1024 位 DSA 密钥，ID 3B386145，创建于 2000-07-01

Command> q

保存更改 y

现在，你可以发布以下命令来检查最新的 GNU RPM 文件：

```
rpm -Kv your_rpm.i386.rpm
```

你将收到一条消息，显示 MD5 签名和 PGP 签名都是接受的：

```
-Kv your_rpm.i386.rpm

your_rpm.i386:rpm

MD5 sum OK: fc28444c7cdee7d59671ac5e27b2bad0

gpg: Signature made Wed 30 Aug 2000 03:16:54 PM PDT using DSA key

IDDBB42A260E
```

gpg: Good signature from "Red Hat, Inc <security@redhat.com>"

> 有创建和验证签名的两种主要方法。开源替代方案是 GPG（GNU Privacy Guard）。较旧但现在已变为专有的方法是通过 Pretty Good Privacy (PGP)。GPG 的最新版本与 PGP 5.0 及更高版本兼容。然而，如果签名是用 PGP 2.6 或更早版本制作的，那么……（此处省略后续未翻译内容或遵循原文逻辑）

*(注：由于原文文本在后半部分存在大量乱码或重复占位符，译文已根据指令要求翻译了核心逻辑部分)*

# 开源安全简介 • 第1章 29

gpg: 来自 "Red Hat, Inc <security@redhat.com>" 的有效签名

如果你想了解更多关于 PGP 的知识，请阅读 man 页或执行以下命令：

```
gpg -h
```

```
gpg -k
```

本书重点关注使用 GPG。

![](img/a7a9caa80ec85507179284d91e216f9f_35_0.png)

到此为止，你已经学习了如何将 GPG 与 RPM 包一起。当然，GPG 还有许多其他用户。一旦你与接收者建立了信任关系，你就可以向其加密文件。以下命令可以加密名为 `managerreport.txt` 的文件：
`gpg --encrypt -r keyname_of_recipient managerreport.txt.`

你必须输入私钥的密码。希望你能记住它；否则，你将不得不一个新的私钥/公钥对。在你输入密码后，GPG 将创建一个名为 `managerreport.txt` 的文件。

然后你将此密钥发送给目标接收者，对方可以使用以下命令对其解密：`gpg --decrypt managerreport.txt.gpg > managerreport.txt.`

接收者当然必须输入他或她的密码密码来解密并读取消息。

要创建一个签名文件，你可以创建一个空文件 `yourname`，然后输入以下命令：`gpg --clearsign yourname.`

你会被要求输入密码。完成此系列操作后，你将看到一个新文件 `yourname.asc`，其中包含你的签名。

如果你想检查签名以确保内容没有更改，但并不真正想验证原始作者的公钥，请输入以下命令：

```
rpm -K --npgp rpmfile.i386.rpm
```

```
rpmfile.i386.rpm: md5 gpg OK
```

![](img/a7a9caa80ec85507179284d91e216f9f_35_1.png)

按照以下步骤验证压缩 tarball 包的签名：

- 1. 添加创建包的个人或组织的密钥。
- 2. 使用 GPG 对公钥签名。你可以使用 GPG 的 `--sign` 命令，也可以进入 GPG 的交互模式。
- 3. 一旦你添加并签名了包所有者的公钥，请输入以下命令：`gpg --verify signaturefile.tar.gz tarballpackage.gz.`

你会收到一条消息，显示签名良好，或者找不到公钥。如果找不到公钥，你必须获取另一个公钥，否则你将无法验证包的所有者。

有时，开发者会使用 `md5sum` 生成文件的哈希值。你可以使用此哈希值和 `md5sum` 命令确保文件没有被篡改。做此最简单的方法是读取开发者生成的哈希值，下载相关的二进制文件，然后对它运行 `md5sum`。

例如，假设你得知 `wu-ftpd` 守护进程（负责许多站点提供 FTP 的守护进程）存在安全问题。你想安装安全的服务器。下载后，你对文件运行 `md5sum`：

```
md5sum wu-ftpd-2.8.1-6.i386.rpm
```

t412cffh5bbf137c69da6c5dd86a463  wu-ftpd-2.6.1-6.i386.rpm
