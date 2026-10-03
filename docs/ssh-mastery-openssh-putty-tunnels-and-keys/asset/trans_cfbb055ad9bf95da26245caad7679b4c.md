
工作会话期间只需输入一次 passphrase，无论当天打开多少个 SSH 会话。

典型的一天里，我登录工作站，激活 SSH 代理，并输入一次 passphrase。随后我可以打开无数个通往网络各处服务器和路由器的 SSH 会话，而无需再次输入 passphrase 或密码。当我下班注销时，我的代理会关闭。代理使用的内存会被清除并归还给操作系统。我的私钥再次仅在加密文件中可用。

代理并不能保证安全。只要在你登录期间能够读取计算机内存的任何人，都可以访问解密后的密钥，其中包括 root 账户。如果你不信任桌面上的系统管理员，就不要使用 SSH 代理。¹ 如果你挂起笔记本电脑，解密后的私钥仍会保留在内存中。任何能够唤醒你的笔记本电脑并登录的人，都可以按其访问权限使用该密钥。一个随机的小偷只想快速换点钱，可能根本不知道或不理解他得到了什么，但专门针对你和/或你的雇主的窃贼很可能会检查是否存在活动的私钥。更常见的情况是，如果你在午餐前不锁定桌面，同事可能会利用你未受保护的终端。这些问题最好通过在不积极使用系统时清空或关闭代理来解决。

多用户机器上的代理安全也是一个问题。任何在系统上拥有管理员或超级用户权限的人都可以访问主机上运行的任何 SSH 代理。如果其他人拥有你桌面上的 root 或 Administrator 访问权限，他们可以访问你的代理并冒充你。使用代理是不明智的。

本章稍后我们将讨论 PuTTY 和 OpenSSH 的 SSH 代理。

## 创建 OpenSSH 用户密钥

如果你使用类 Unix 桌面，请使用 ssh-keygen(1) 生成密钥。不要使用任何参数，程序会引导你生成用户身份验证密钥。

```
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/mwlucas/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/mwlucas/.ssh/id_rsa.
Your public key has been saved in /home/mwlucas/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:LK+1dKbb/PtN8KjiXLDDzzOK1fivRkMZIn8YoOrmEvA mwlucas@zfs1
The key's randomart image is:
+---[RSA 2048]----+
...
```

系统会询问新密钥应保存在何处。各种 OpenSSH 程序期望在默认位置找到密钥文件，因此请接受建议。然后系统会要求你两次输入 passphrase，以验证你能多次输入。你的私钥将使用此 passphrase 进行加密。务必使用 passphrase，如几页前所述。

SSH 对主机和用户使用相同的密钥格式。当你生成用户密钥时，会得到密钥指纹和 randomart 图像。对于用户身份验证密钥而言，两者都不是特别有用。

你会在 $HOME/.ssh/id_rsa 找到新的私钥，在 $HOME/.ssh/id_rsa.pub 找到新的公钥。立即将新密钥对备份到离线介质上，例如闪存驱动器或 CD-ROM。如果你的工作站被毁，你将希望能够恢复密钥对。

## 密钥算法

与主机密钥一样，用户密钥也可以使用几种不同的加密算法。如果不指定算法，OpenSSH 工具会使用推荐的算法——目前为 2048 位 RSA。你可以使用 -t 标志指定不同的算法。

```
$ ssh-keygen -t ecdsa
```

为什么要创建多个密钥？密码学家有这种令人不安的习惯，即发现加密算法中的弱点。有一天不可思议的事情会发生，有人会在广泛使用且被普遍信任的算法中发现缺陷。使用该算法的所有密钥将立即变得不可信。如果你的用户密钥使用不同的算法，你可以在 SSH 服务器上禁用损坏的算法，仍然可以访问服务器。

我们的示例假设你使用的是 RSA 密钥，但它们同样适用于使用其他算法生成的密钥。

## 创建 PuTTY 用户密钥

使用 PuTTYgen 程序为 PuTTY 创建用户身份验证密钥。PuTTY 安装程序包含 puttygen，或者你可以从 PuTTY 网站单独下载。当你启动 puttygen 时，你会看到类似图 7-1 的屏幕。

![](img/66dbcb7210a5fe0a8b3a1ecd91eb0e6d_63_0.png)

图 7-1：PuTTYgen 启动

使用 RSA、ECDSA 或 ED25519 密钥。DSA 密钥即将被淘汰，而 SSH-1 RSA 密钥早已过时。验证位数至少为 2048。更多并不一定有帮助。你可能会为专门用于古老服务器（如 VAX 或 Alpha）的用户密钥使用更少的位数。单击 Generate。下一个 PuTTYgen 屏幕会要求你通过在空白区域拖动鼠标来生成随机性。一旦生成足够的熵，PuTTYgen 就会创建你的密钥，如图 7-2 所示。

![](img/66dbcb7210a5fe0a8b3a1ecd91eb0e6d_64_0.png)

图 7-2：PuTTYgen 密钥和口令短语

这里你可以填写三个字段。第一个是密钥注释。我建议将注释更改为反映你生成密钥的机器和创建日期。现在两次输入你的 passphrase。

现在单击 Save public key。你会得到一个标准的 Windows “另存为” 对话框，要求你选择保存密钥的位置。将文件保存在只有你有权限访问的位置。你可以使用 Documents 下的文件夹，但请确保稍后进入并设置权限，以便机器上的其他用户无法查看文件。我通常将这些文件命名为它们创建的机器和日期。Puttygen 默认不会分配文件扩展名，因此请使用 .pub 扩展名。²

现在保存私钥。对公钥和私钥使用相同的名称。PuTTYgen 对私钥使用 .ppk 扩展名，因此它们不会相互覆盖。

你现在拥有一个公钥。恭喜！但不要退出 PuTTYgen。

屏幕顶部显示密钥采用 OpenSSH 友好的 authorized_keys 格式。将其复制到一个文件中，全部放在一行。我通常将该文件命名为密钥生成的机器、日期，并加上 authorized_keys 字符串。

## 安装公钥

无论你使用哪个客户端，在使用它登录之前都必须将公钥安装在服务器上。每当你 SSH 到主机时，OpenSSH 服务器会检查本地文件 $HOME/.ssh/authorized_keys。该文件包含公钥，每行一个（非常长）。SSH 服务器将客户端提供的公钥与文件中的密钥进行比较。如果密钥匹配，并且客户端能够成功使用该密钥交换数据，则客户端已证明其拥有对应的私钥。访问被授予。如果没有 authorized_keys 文件，服务器会回退到下一个身份验证方法（通常是密码）。

如果你是请求访问仅接受公钥身份验证的服务器的用户，系统管理员会要求你提供 authorized_keys 文件。如果你第一次使用公钥身份验证，这不是安全风险——记住，你的公钥文件是公开的。任何人都可以拥有它。如果没有对应的私钥，它完全无用。

最常见的用户密钥类型是 RSA 密钥。OpenSSH 将客户端的 RSA 公钥存储在文件 $HOME/.ssh/id_rsa.pub 中。PuTTY 的密钥生成器要求你自行命名密钥文件，你会有几个不同的密钥文件。你需要的是包含 authorized_keys 友好版本的那个文件。如果你遵循了我的建议，文件名将包含 authorized_keys。为了简化示例，我们将使用文件名 id_rsa_authorized_keys.pub。必要时请替换为你的 PuTTY 文件。

要使用你的公钥，你必须将客户端的公钥文件复制到服务器上你账户中的 authorized_keys 文件。你可以使用图形界面的复制粘贴功能，但容易出错。通过 SFTP 或 SCP 上传公钥文件然后将其连接到 authorized_keys 更可靠。记住，每个密钥在 authorized_keys 中必须且只能占一行。我多次尝试简单的复制粘贴，结果都以眼泪告终，然后威胁要改行做骆驼走私，最后在最近的 gelato 店进行躁郁症式的暴饮暴食。让机器复制文件。它比你做得好。

这里，我使用 scp(1) 将客户端的 id_rsa_authorized_keys.pub 复制到服务器 sloth。

```
$ scp .ssh/id_rsa_authorized_keys.pub sloth:
```

服务器仍会要求输入密码来上传密钥文件；你已创建密钥，但尚未安装。

PuTTY 用户应使用 WinSCP 友好的拖放文件复制。

现在登录服务器并将 id_rsa_authorized_keys.pub 的内容附加到 authorized_keys 文件中。如果你第一次安装公钥，可以将密钥文件复制到 authorized_keys。如果你养成这种习惯，
