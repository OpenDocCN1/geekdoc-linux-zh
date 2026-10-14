

使用 scp，你可以将公钥复制到你的服务器，如下所示：

```
scp id_dsa.pub 10.0.0.1:
```

这会将 id_dsa.pub 放置在 10.0.0.1 上的你的主目录中。下一步是以正常方式 SSH 登录到 10.0.0.1 并将该密钥设置为授权密钥。因此，你可以以自己的身份 SSH 登录，然后输入

```
touch .ssh/authorized_keys
cat id_dsa.pub >> .ssh/authorized_keys
chmod 400 .ssh/authorized_keys
```

touch 命令会创建 authorized_keys 文件（如果它尚不存在）；然后你使用 cat 将 id_dsa.pub 的内容追加到已授权密钥列表中。最后，使用 chmod 将 authorized_keys 设置为只读。

完成此操作后，你可以输入 exit 以断开与远程机器的连接并返回到本地机器。然后你可以尝试再次运行 ssh。如果提示输入你的密码短语，则说明你已成功配置基于密钥的身份验证。

这台当前机器已得到保护，但其他机器呢？仍然可以从另一台机器仅使用密码登录，这意味着你的远程机器仍然容易受到攻击。

解决此问题的方法是切换到 root 并编辑 /etc/ssh/sshd_config 文件。查找 PasswordAuthentication 行并确保其内容为 no（并且前面没有用 # 注释掉）。保存文件，然后运行 kill -HUP `cat /var/run/sshd.pid` 以使 sshd 重新读取其配置文件。完成此操作后，sshd 仅接受来自具有授权密钥的客户端的连接，这阻止了黑客通过暴力破解的方式进入。

TIP

> 为了额外安全，请考虑在 /etc/ssh/sshd_config 中将 PermitRootLogin 设置为 no。这样设置后，就无法使用 root 账户通过 SSH 登录你的机器——你必须使用普通用户账户连接，然后使用 su 或 sudo 切换到 root。这是有利的，因为大多数暴力破解尝试都针对 root 账户，因为它是服务器上唯一 guaranteed 存在的账户。
> 此外，即使黑客知道你的用户账户，她也必须猜出你的用户密码和 root 密码才能控制你的系统。

## Remote X

到目前为止我们所看的全部都是命令行远程操作，迄今为止尚未提及如何启动图形用户界面。在 Linux 中有两种方法可以做到这一点：X Display Manager Control Protocol（XDCMP）和 Virtual Network Computing（VNC）。前者特定于 X Windows，并且与图形系统的其余部分紧密集成，但也很不安全。VNC 更现代且非常普及，但在某些实现中也不安全。两者都在 Ubuntu 上使用，因此我们将在此处介绍两者。

## XDMCP

除非你将 Ubuntu 配置为自动登录特定用户，否则你会熟悉启动时出现的用户登录屏幕。你看到的是 Gnome Display Manager（GDM），它运行你的 X 会话、检查密码等。你所做的是登录到本地机器，因为这是默认配置。

然而，GDM 也配备了允许其他网络用户通过 XDMCP 协议连接到你的机器的功能。使用 XDMCP 的原因有很多，其中最流行的是许多现代机器体积庞大且噪音很大。它们拥有大容量硬盘、带巨大风扇的 CPU 和强大的显卡，因此不适合放在安静的客厅里。另一方面，瘦客户端（CPU 能力非常低且没有自己硬盘的机器）是静音的，但功率不足以运行 Gnome 或 OpenOffice.org。

解决方案是将你的强大机器锁在某个壁橱里并连接 Wi-Fi，而将安静的瘦客户端放在客厅里也连接到 Wi-Fi。瘦客户端连接到强大机器并从那里运行所有程序，所有图形都通过网络中继。

在 Ubuntu 中，这很容易做到。首先从服务器端开始，选择 System > Administration > Login Window；然后选择 Remote 选项卡并将 Style 选项更改为 "Plain with face browser"。在客户端，打开相同的对话框并确保从 Local 选项卡中勾选了 Show Actions Menu 框。

现在，从客户端注销桌面，以便返回到 Ubuntu 登录屏幕。当它提示你输入用户名时，查找 Options 按钮并选择 Remote Login with XDMCP。会出现一个新对话框，其中列出了愿意接受你连接的本地 XDMCP 服务器——你应该能在其中看到你的服务器。选择它并点击 Connect；你将看到来自该服务器的登录屏幕，邀请你登录。当然，你需要在服务器上拥有有效账户才能登录；然而，这就是你唯一需要的。

正如你所见，由于 XDMCP 是 X Windows 系统的核心，因此设置起来很容易。然而，正如你使用时所发现的，XDMCP 速度非常慢——即使在千兆以太网网络上，它也会消耗相当一部分带宽。它也不安全。任何人只需做很少的工作就可以监控你的操作。由于这两个缺陷，XDMCP 不应在受信任网络之外使用。

## VNC

从 XDMCP 升级的下一步是 VNC，它是在英国 AT&T 的剑桥研究实验室开发的。VNC 在 Linux 世界中广泛使用，在 Windows 世界中也使用到一定程度。其主要优势在于其广泛性：几乎所有 Linux 发行版都捆绑了 VNC，并且客户端可用于各种平台。

