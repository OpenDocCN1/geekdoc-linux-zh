
关于将 FreeNX 引入 KDE 的 KDE 开发者访谈，可以在 `www.osnews.com/printer?news_id=8139`。令人置信的是，FreeNX 实际上只是一个 BASH 脚本——几百行的 BASH 脚本，但它终毕竟是一个 BASH 脚本！

什么样的机器可以支持 FreeNX 服务器？对于每个 KDE 用户会话，你大约需要 40MB 内存和大约 100MHz 的 CPU，这并不差。如果你有一台良好且快速的机器，例如大约 3GHz、1GB 内存，可以支持大约 25 个并行会话。这很不错！

FreeNX 的结果是：与其他机器建立极快速、安全的连接——而且是免费的！

## 设置 FreeNX

要启动 NX 服务器，选择 Knoppix → Services → Start NX Server。弹出的对话框会警告你将创建一个名为 `nxuser` 的新用户，其可以访问 FreeNX 服务器。继续点击 OK。另一个对话框打开，提示你为新的 `nxuser` 创建密码。为了现在保持简单，也使用 `nxuser` 作为密码，然后点击 OK。

## 注意事项

不要在你的机器上使用 `nxuser` 作为密码！请请创建一个良好的密码来保护你的机器和数据。关于如何创建良好密码的帮助，请阅读 Security Focus 上的标题为“The Chocolate”的文章，地址为 `www.securityfocus.com/columnists/245`。

FreeNX 生成加密密钥，以便使用其协议发送的所有通信免受数据嗅探的侵害；它会产生一个窗口，你可以在其中观察过程。

同时，另一个对话框打开，通知你现在可以使用新创建的 `nxuser` 账户登录。注意，你可以使用系统上的任何用户登录，因此默认没有设置密码的 `knoppix` 也可以登录。当你点击 OK 关闭对话框时，FreeNX 产生的 shell 窗口消失，FreeNX 正在运行。

## FreeNX 服务器的命令行控制

使用命令行更改 FreeNX 服务器非常简单。一旦你运行 root 权限（只需在命令行输入 `su -` 并按回车即可以超级用户身份运行），就可以输入以下命令进行修改：

- `nxserver -listuser`：显示 FreeNX 用户列表，如果你想验证谁可以登录你的账户，这非常有帮助。
- `nxserver -adduser username`：添加新用户，你可能不需要这样做，因为 `nxuser` 已经足够了。
- `nxserver -deluser username`：删除用户。
- `nxserver -passwd username`：提示为指定用户输入密码，同样可能不需要执行，假设你在最初被提示时为 `nxuser` 选择了合适的密码。
- `nxserver -status`：FreeNX 正在运行吗？通过此命令查询。
- `nxserver -start`：如果 FreeNX 服务器未运行，则启动它。
- `nxserver -stop`：如果 FreeNX 服务器正在运行，则停止它。
- `nxserver -restart`：如果 FreeNX 服务器正在运行，则重启它；如果没有运行，则启动它。警告：当你运行此命令时，任何连接到你 FreeNX 服务器的人都会被粗鲁地断开，除非你使用下一个命令。
- `nxserver -broadcast message`：将你的消息发送给所有登录用户，你应该在重启服务器之前这样做。

要查看可能的选项列表，只需以 root 身份在命令行输入 `nxserver` 并回车。

## 理解 FTP

FTP（文件传输协议）是网上仍在使用的最古老的协议之一。它于 1971 年 4 月在 RFC 114 中提出（`www.ietf.org/rfc/rfc114.txt`），每天被使用数百万次，即使是那些完全不知道自己通过 Web 浏览器下载的文件是由于一项使用了 30 多年的技术而到达他们电脑的人。

遗憾的是，FTP 有一个很大的问题：安全性。因为太老了，FTP 在设计之初根本没有考虑安全性。因此，用户名、密码以及所有后续流量都是明文传输的，让任何嗅探包的人都能轻易找到你的敏感信息。Knoppix 没有附带 FTP 服务器软件，这没关系：无论如何你应该使用 SSH 和 SFTP，后者会加密所有流量。然而，Knoppix 确实附带 FTP 客户端软件，如果你必须连接到不支持 SFTP 的服务器，这可能会派上用场。

如果你不知道如何使用命令行，那么在这一点上你会会得非常被手。另一方面，如果你知道如何使用 `cd` 及相关命令进行导航，以及如何使用 `vi` 等基于终端的编辑器运行程序和处理数据，那么这里就是你的乐场。

# 使用 SFTP

如果你必须来传输文件，请使用 SFTP 而不是 FTP，原因仅仅是为了安全。FTP 会以明文形式发送你的用户名、密码和所有数据，导致任何截获流量的人（将在第 6 章中讨论）都能窃听；而 SFTP 则通过 SSH 传输并加密所有内容，这正是你想要的。

如果你愿意，可以在命令行中使用 SFTP。如果你熟悉命令行 FTP，你会觉得非常自如，因为一切都是那样的。要使用命令行连接，只需在 Konsole 中输入 `sftp username@machine` 并按回车（使用上一节的示例，你输入 `sftp scott@work.wiley.com`）。在提示时输入密码即可开始使用。如果你需要复习可以使用的命令，只需输入 `help` 并查看生成的列表即可。

如果你更倾向于使用 GUI——这在很多情况下显然更简单——那么你可以回到你熟悉的 Konqueror，它处理 SFTP 的能力和 FTP 一样好。一切都完全相同，只是你在位置栏中使用 `sftp` 而不是 `ftp://`。这并不意味着你可以直接将任何网站的 `ftp` 改为 `sftp` 并让其工作。事实上，这在大多数情况下都会失败，因为大多数使用 FTP 的服务器并不一定使用 SFTP。

如何使用 Konqueror 连接到支持 SFTP 的服务器？打开 Konqueror，在位置栏中输入你的服务器地址（类似于 `sftp://work.sftpserver.com`），并按回车。接下来你应该看到一个与图 3-4 类似的警告框。

![](img/2fb32174ccf4cfbddb3c8b1d8e3e3b4c_99_0.png)

图 3-4：第一次连接到机器时，必须接受该机器的密钥。

记住，通过 SSH 发送的所有流量都是加密的。为了实现加密，你的计算机与要连接的服务器之间会交换密钥。这个警告是 SSH 在告诉你，它没有办法知道服务器密钥是否有效——换句话说，如果你确定知道密钥是有效的，且不是中间人攻击的受害者——请尽管点击“是”，将密钥添加到你在 `~/.ssh/known_hosts` 中找到的列表中（如果因为重装操作系统导致服务器上的密钥发生变化，你需要在 `known_hosts` 中找到相应的行，将其删除，并重新连接服务器以重新接受并重新输入密钥）。

添加密钥后，系统会提示你输入用户名和密码。继续输入，几秒钟你你就能看到 SFTP 服务器的内容。

想了解更多关于中间人攻击的信息？请查看维基百科关于该主题的文章：`http://en.wikipedia.org/wiki/Man_in_the_middle_attack`。

使用 SFTP 下载和上传文件与 FTP 相同：只需拖放，或者右键点击并选择“复制到”。如果你计划在运行 Knoix 期间多次使用某个 SFTP 站点，请将其书签化以便以后访问。

安全第一：当你有选择时，请使用 SSH 而不是 FTP。

我在家里内部网络上使用 SCP，部分是因为我有偏执症，部分是因为它现在是自动的。养成同样的习惯是个好主意。

## 使用 SCP

如果你是一个命令行发烧友并且赶时间，SCP（安全拷贝）是使用 SSH 将文件从一台机器快速复制到另一台机器的好方法。SCP 基本遵循此模式：`scp user@host1:file @host2:file`。不过，如果你处理的文件之一是本地的，可以省略 `user@host`，稍后你会看到。

例如，假设你想用 `scp` 将 `me.jpg` 从当前目录复制到你在另一台机器（称为 wiley.com）上的网站。在命令行中输入以下内容并按回车：

```bash
$ scp me.jpg username@wiley.com:/var/www/mywebsite/images
```

系统会提示你输入密码，片刻后 `me.jpg` 就会出现在你的网站上供周围的人查看。

有几个 JPEG 想要传输？简单！

```bash
$ scp *.jpg username@wiley.com:/var/www/mywebsite/images
```

要将服务器上所有的 JPEG 复制到当前机器，但复制到与当前目录不同的目录，请输入：

```bash
$ scp username@work.wiley.com:/var/www/mywebsite/images ~/pix/website
```

# 76 第一部分 — 导航神奇的 Knoppix 工具箱
