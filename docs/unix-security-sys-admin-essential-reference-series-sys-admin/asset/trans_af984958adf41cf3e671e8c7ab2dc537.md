

## 实现

我们购买了一份 WordPerfect Office SMTP 网关的拷贝，需要安装在一台独立的 PC 上。我们翻新了一台运行在 16MHz 上的 IBM PS/2 80386，内存为 4Mb。为了准备安装，我们安装了所需的两张网卡：一张 Pronet 10 卡（一种专有的 10Mb 令牌环技术）和一张 IBM 16Mb Token-Ring 卡。无需硬盘，因为我们计划将大部分驱动程序、守护进程和程序从 Novell 文件服务器运行。

我们与网关一起使用的 TCP/IP 软件是 Novell 的 LANWorkPlace，它在 Novell 的 ODI 驱动程序下运行。由于 Pronet 10 卡使用的是 .obj（链接）版本的 IPX，我们对将其与 ODI 驱动程序一起使用有点担心，但一切都运行良好。我们使用 Novell 的 NETX 来引导工作站，并从文件服务器加载其他所有内容（包括 ODI 驱动程序和 TCP/IP）【图 14.2】。

我们按如下方式构建了 NetWare 设置。机器从软盘驱动器加载 IPX 和 NETX，并登录到网络。无需密码，因此可以无人值守重启。我们使用 SYSCON 为登录设置了站点限制，有效地将无密码登录限制为 SMTP 网关的 MAC 地址和 IPX 网络号。 （不要使用 TCP/IP 卡的 MAC 地址！）此外，我们使用 SYSCON 将登录添加到组 MACHINES，该组通常在我们的本地登录脚本中使用，以避免“按任意键继续”提示等。授予的唯一受托人权限是访问 WordPerfect Office Domain 目录（例如，F:\WPDOMAIN）和登录的主目录（我们将其映射为 H: 驱动器的根目录）。

```
CONFIG.SYS
  device=himem.sys
  device=emm386.exe ram
  files=80
  buffers=40
  dos=high,umb

AUTOEXEC.BAT:
  prompt $p$g
  rem gen rd IPX via Pronet-10:
  ipx
  netx ps=chat
  f:
  login chat/smtp
```

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_174_0.png)

令人惊讶的是，一切第一次就成功了！好吧，一切第二次就成功了，一旦我们意识到我们忘记将网关机器添加到我们的 DNS（域名服务）数据库中。一旦 DNS 重建，从我们局域网上的一台工作站发送给我的朋友 Jim 的测试邮件 chat.smtp:(jreich@decbert.ece.cmu.edu) 实际上到达了！

但我们的惊讶是短暂的。那种写电子邮件地址的方法很快就会让人厌倦。而且我们可以想象从 WordPerfect Office 的各种用户那里接听支持电话：“有多少个括号？引号是在外面还是在里面？先是 chat 还是 smtp？这个 smtp 到底是什么东西？我以为我们有 Internet 邮件！”

## 改进

幸运的是，WPO 易于配置并支持“简化直通寻址”。使用 ad.exe 程序，我们创建了一个新的域，类型为“Foreign”，域名为“Internet”。然后我们编辑了我们的主域 Chat，将其链接到我们的新 SMTP 网关。

我们选择了“消息服务器配置”，然后选择“网络链接”。在域连接对话框中，我们选择了新建的域“Internet”，并选择“编辑链接”。在“方式”对话框中，我们选择了“网关”，然后选择“SMTP”。起初，我错误地认为这会传播到所有子域。并非如此。您必须为所有子域执行此操作。

重新配置后，我可以用地址 Internet:jreich@decbert.ece.cmu.edu 给 Jim 发送邮件。

一旦发件邮件流程稳定且易于使用，我们就研究了收件邮件的改进。来自外部到 user@wpo.co.chatham.ga.us 的邮件如果用户姓名中没有特殊字符则可以正常工作。不幸的是，对我们来说，我们的大多数用户确实有 SMTP 网关认为的“特殊字符”（即下划线）。例如，我们的 WPO 管理员最初将我的用户名设置为“J_FELDMAN。这意味着外部用户必须发送邮件到 J##J#FELDMAN@wpo.co.chatham.ga.us。WPO 网关对井号（#）的处理方式类似。几次令人沮丧的与供应商的电话，试图拼写出我们的用户名，让我们确信这种方法行不通。

幸运的是，WPO 还支持“本地 SMTP 网关别名”。从 ad.exe 程序中，我们选择了用户所属的域，按“Enter”键编辑该用户名，然后在“编辑用户”对话框中点击“网关别名”。从“网关”对话框中，我们创建了一个新的别名，类型为“SMTP”。我们在“本地网关地址”中输入用户的外部别名。例如，我选择了域 CHAT，用户 J_FELDMAN，并输入“jonathan”作为本地网关地址

