

某些软件以该格式打包，它们的作用类似于 .exe 文件，只需双击即可开始安装过程。

## 更多终端命令

以下是一些你需要内化并在系统中加以使用的其他基本终端命令。彻底理解这些基础知识，将为后续的学习打下坚实的基础。

- cp – “cp image1.jpg image2.jpg” – 将第一个参数复制（并重命名）为第二个指定的参数。使用 -r 参数复制目录。
- mv – “mv cat.jpg /home/Pictures” – 将指定文件移动到给定目录。
- shutdown – “shutdown -h now” – 关闭计算机。-h 是表示“停止”的标签，但你也可以使用权用 -r 来重启。Now 指的是执行前的等待时间。
- date – “date” – 显示当前日期和时间。
- free – “free –g” – 显示当前程序的 RAM 使用情况。
- du – “du –h” – 显示 HDD 使用情况。
- ps – “ps” – 显示正在使用 CPU 时间的活动进程。
- touch – “touch memo.txt” – 用于在当前目录下创建一个具有指定名称的新空白文件。
- ifconfig – “ifconfig” – 这是 Linux 中 ipconfig 的等价命令，用于显示网络信息。

某些命令具有相关的“标签”或“开关”。这些就是由破折号开头的字母。它们的作用各不相同，而了解针对特定目的应使用哪些开关，最好是通过该命令的手册页来学习。有关如何打开手册，请参阅高级部分。

从命令行出发，nano 是最有用的程序之一。它是一个简单的文本编辑器，可用于编辑文件并快速更改设置或脚本。通过在命令行中输入“nano”即可访问它。你可以输入所需的文件，然后按 ctrl+x 保存并退出。保存时，你会为其指定相关的名称和文件扩展名；例如，notes.txt 将创建一个名为“notes”的文本文件。或者，你可以通过输入“nano notes.txt”来编辑文件。在该示例中，我们在编辑器中打开 notes 并以可编辑状态显示其内容。

Nano 可能非常简洁，但它无疑功能强大，对于快速更改和创建文件来说是一个省时的好工具。

## 连接 Windows / Mac 计算机

Windows 和 OSX 计算机内置了工作组、域、共享等功能。将 Linux 计算机集成到由 Windows 服务器计算机主导的网络基础设施中相当容易，正确的设置将允许你查看 Windows 共享并加入企业域。

实现互连的第一步是安装“samba”软件包。你可以通过软件中心找到它，或者输入“sudo apt-get install samba”来获取并安装必要的软件。

将 Ubuntu 机器上的文件共享给其他计算机需要创建一个 samba 共享。Samba 使用与其他流行文件共享方法相同的协议，因此从 Ubuntu 机器共享的文件可以 easily 在 Windows 上被看到。安装 samba 后，使用“sudo nano /etc/samba/smb.conf”开始编辑配置文件。在文件的最底部添加这些行：

```
[share]
comment = File Share from Ubuntu
path = /srv/samba/share
browsable = yes
guest ok = yes
read only = no
create mask = 0755
```

现在，创建“path”中指定的文件夹（sudo mkdir -p /srv/samba/share）并设置权限（sudo chown nobody:nogroup /srv/samba/share/），以便任何人可以访问其内容。将任何想要共享的文件放置在该目录内，然后重启服务（sudo restart smbd, sudo restart nmbd）以使共享生效。最后，登录到你的另一台计算机并导航到网络共享。在 Windows 中，它们将显示在文件资源管理器的左侧面板中。如果共享没有自动出现，请在文件路径框中输入 IP 地址（使用 ifconfig 查找 Ubuntu 的 IP）。现在，你可以从其他操作系统访问 Ubuntu 的文件了。

你可能还需要在 Ubuntu 计算机上查看来自其他操作系统的文件。首先，打开 Ubuntu 文件资源管理器。从菜单栏中，点击“files”，然后选择“connect to server”。在出现的框中，输入你想要访问的共享的 URL。它可以是一个 ftp 地址（ftp://ftp.test.com），一个 http 地址（http://test.com），或者一个共享地址（smb://share/Folder）。无需额外的硬件或设置，你就可以通过这种方式查看文件。

最后，加入诸如 Active Directory 之类的域，可以使你的计算机与网络上的其他操作系统交互，并执行其他面向业务的任务。无论是小型家庭网络，还是将 Linux 计算机添加到企业域中，过程都是一样的。安装一些额外的软件包（realmd, sssd, sssd-tools, samba-common, samba-common-bin, samba-libs, krb5-user, adcli, packagekit）。在安装过程中，它会询问你的域名。请输入全大写的域名。输入“kinlt -V adminname”，并用域中的实际管理员账户名称替换该名称。输入密码后，你将通过域的身份验证。现在，使用“realm --verbose join -U adminname domainname.loc”来完成加入。

如果失败，这意味着我们设备上的 DNS 配置有误。输入“echo ‘ad_hostname = nix01.domainname.loc’ >> /etc/sssd/sssd.conf”，然后输入“echo ‘dyndns_update = True’ >> /etc/sssd/sssd.conf”，最后使用“service sssd restart”根据这些新设置重启服务。第一行设置了我们计算机的 FQDN，因此需要根据我们的域设置更改该行。在成功重启并正确配置设置后，终端将显示它已加入域。使用“realm list" 进行测试。现在连接到 AD，你可以从服务器管理 Linux 设备！

然而，对于大多数用户来说，创建共享和加入域远远超出了连接需求。通过 USB 驱动器传输或使用 Dropbox 等简单的服务来共享文件要好得多。事实上，Dropbox 可以安装在三大主要操作系统上，并且无需额外设置即可在它们之间同步文件。在 Ubuntu 上，你可以直接从网站下载 .deb 文件，从软件中心安装，或者使用 "sudo apt-get install nautilus-dropbox" 获取该应用程序。在 Dropbox 文件夹内放置任何你希望在不同计算机之间传输的文件，它会自动下载并更新到你拥有的其他所有 Dropbox 计算机上。

当你将它们连接在一起时，使用其他操作系统并不复杂。只要计算机位于同一网络上，你就可以创建文件共享，将它们加入域，或使用 Dropbox 这样简单的服务。

## 实用应用程序

以下是适用于你的 Ubuntu 系统的最佳应用程序列表，它们将帮助你最大限度地发挥计算机的性能。

- 办公效率 – Abiword, VI, Emacs, LibreOffice, nano
- 多媒体 – VLC, DeaDBeeF, Cmus, AquaLung, MPlayer, Miro
- Web 浏览 – Firefox, Chromium, Midori, W3M
- 创造力 – Audacity, GIMP
- 其他 – Kupfer, Thunderbird, qBittorrent

对于有助于提高易用性的程序，选择如此多样化，取决于你要完成的任务。发现程序的最佳方法是在互联网上搜索你希望添加的功能。例如，如果你在寻找一种快速打开和关闭终端的方法，你可能会遇到“Guake”程序。或者，如果你想在终端内使用音频，它可能会推荐“Cmus”。为你找到完美的应用程序是 Linux 定制方面的一部分，这使得每个用户的安装体验都更具个性化。

## 管理

如果你在寻找某种“控制面板”，你可以在“系统设置”应用程序中找到管理工具（如网络、打印、键盘、外观等）的快捷方式。一些 Ubuntu 变体使用“设置管理器”或仅使用“设置”来实现相同的目的。

启动后，会有指向其他默认配置应用程序的链接；只需点击你需要更改的设置，即可获得一个包含一些选项的图形用户界面（GUI）。但并非所有管理任务都可以通过 GUI 完成。大多数底层设置只能通过命令行访问，因此你需要确切知道要输入什么来编辑它们。

例如，向 Ubuntu 添加新用户需要“adduser”命令。通过在命令后跟一个用户名，终端将提示输入基本信息和密码。使用“usermod -aG sudo nameofuser”可以将该新用户设置为管理员。此外，可以使用“deluser”删除用户。这些选项通过 GUI 难以找到，但可以通过终端在几秒内完成。

