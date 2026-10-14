
如果在尝试拨号连接到 Internet 时听到调制解调器意外挂断，或者从未建立 PPP 连接，请查看 `/var/log/messages` 文件中是否有任何可能帮助你识别问题的消息。你应该能够通过遵循提示和命令的交互并进行修正来修改设置以纠正问题。也可能很有帮助使用 `Minicom` 拨号到你的 ISP 并写下获取连接所需的确切提示和正确响应。`Minicom` 实际上无法建立 PPP 连接，但它可能有助于你清楚地看到在提示和响应方面需要做什么。

# 基于文本的 Internet 工具

信不信由你，Internet 在图形化 Web 浏览器出现之前就已存在。在 1990 年 Mosaic 发明之前，网民们使用 Unix 命令行上的基于文本的工具进行电子邮件、文件传输、登录远程机器，甚至浏览 Web。

许多用户实际上更喜欢使用基于文本的客户端（使终端用户能够连接到各种类型 Internet 服务器的工具），因为图形环境会增加大量开销，使其变慢。而且有些人只是更喜欢键盘而不是鼠标。

> 注意：了解从命令行使用网络的基础知识很重要，因为你可能不想（或没有硬件）在系统上运行 X Windows。这些相同的技术在你通过 ISP 拥有 Unix shell 账户时也会派上用场。

# 使用 FTP

FTP（代表文件传输程序或文件传输协议，取决于你把几支铅笔别在口袋保护器里）是 Internet 文件搬运工。你用它在两台计算机之间传输文件。最常见的是，你会用它将软件下载到你的计算机上，所以现在就试试吧。要从 Linux 命令行启动基于文本的 FTP 客户端，输入 `ftp` 命令后跟站点名称，如下所示：

```
ftp ftp.devolution.com
```

在提示时，指定 `anonymous` 作为登录名，将你的电子邮件地址作为密码。你将被连接到 devolution.com 的 FTP 站点，在那里你可以下载 Maelstrom——一款适用于 X Windows 的很酷的类似 Asteroids 的游戏。登录到服务器后，你可以输入以下命令下载 Maelstrom 的压缩二进制文件：

```
bin
cd /pub/maelstrom/Maelstrom-binaries/linux-x86/
get Maelstrom.tar.gz
quit
```

如果你不熟悉 FTP，请使用 `help` 命令。在 `get` 命令完成后，`quit` 将使你返回到 Linux 命令提示符，并且你将在当前目录中拥有一个名为 `Maelstrom.tar.gz` 的文件。要解压缩文件并在你的系统上创建可执行文件，输入以下命令：

```
tar xvfz Maelstrom.tar.gz
```

有关处理压缩文件的信息，请参阅第 11 章“压缩、编码和加密”。

# 使用 TELNET

Telnet 是一个让你登录 Internet 上其他计算机的工具。为什么要这样做？很简单：为了访问那些其他计算机上的有趣内容，例如数据库、游戏、卡片目录和信息服务。如果你有 ISP 的 shell 账户，你可能想从 Linux 系统 `telnet` 到那里并使用 Pine 检查电子邮件。

Telnet 严格是基于文本的——你不能指向或单击任何东西。无论你从命令行还是从 GUI 启动 telnet，你的 Telnet 会话看起来都差不多，并且在 Telnet 会话中的所有导航都是通过键盘进行的。要从 Linux 命令行启动基于文本的 Telnet 客户端，输入 `telnet` 命令后跟站点名称（有时还有端口号），如下所示：

```
telnet cybersurf.com
```

这是一个虚构的示例，展示了你如何登录到 ISP 系统上的 shell 账户。以下是真实示例，将使你连接到布法罗大学的业余无线电呼号簿数据库（你输入的命令以粗体显示）：

```
telnet electra.cs.buffalo.edu 2000
```

```
Connected to electra.cs.buffalo.edu.
Callbook v1.3 -- Type 'help' for help
>> help
Available commands:
    call [filters] callsign    - lookup callsign
    city [filters] city        - lookup city
    name [filters] surname     - lookup last name
    quit                       - exit the server
    zip [filters] zipcode      - lookup zip code
> city Tillson
Call-Sign: WA2TNW            Class: GENERAL
Real Name: DONALD G WOOD     Birthday: OCT 31, 1919
Mailing Address: BOX 873 ROSE AVE, TILLSON, NY 12486
Valid From: DEC 29, 1987     To: DEC 29, 1997
>> quit
```

# 使用 FINGER

Finger 是一个小巧实用的工具，可以告诉你某个电子邮件地址的所有者是谁，有时还能显示其他有趣的数据。顾名思义，使用 Finger 就像是在“指向”某个人。当你对一个地址执行 finger 时，你会向另一台系统发送请求，要求它告诉你关于该地址所知道的一切（或愿意告诉的一切）。Finger 的结果因系统而异，有些系统出于隐私原因甚至完全不响应 Finger 请求。尽管如此，大多数 Finger 请求仍会返回有关用户的一些有限信息，例如用户的真实姓名或用户上次登录系统的时间。要从 Linux 命令行使用 Finger 客户端，输入 `finger` 命令后跟一个电子邮件地址，如下所示：

```
finger jsmith@hotdog.edu
```

Home: `/user/jsmith`    In real life: Janet Smith

Shell: `/bin/csh`

New mail received Thu May 16 13:33:18 1996;

 unread since Tue May 14 07:50:31 1996

Janet Smith (jsmith) is not presently logged in.

而正如你在下面这个例子中看到的，有时人们会把奇怪的东西连接到网络上，并允许你通过 Finger 查询它们...

```
finger coke@cs.cmu.edu
```

M & M          Coke Buttons

/------\        C: CCCCCCCCCCCCCCCCCCCCCCC

[?????]        C: ............   D: ............

[?????]        C: ............   D: ............

[?????]        C: ............   D: ............

[?????]                     C: CCCCCCCCCC

\------/                     S: CCCCCCCCCC

|     Key:

|     0 = warm; 9 = 90% cold; C = cold; . = empty

|     Beverages: C = Coke, D = Diet Coke, S = Sprite

|     Leftmost soda/pop will be dispensed next

----... M&M status guessed.

这个例子展示了如何获取一台可乐机状态，该机器已连接到小型计算机并接入卡内基-梅隆大学的互联网！

# EMAIL HANDLING

在第 10 章“管理你的电子邮件”中，你将学习 `mail` 和 `Pine` 程序，它们是 Linux 系统上的基于文本的电子邮件处理程序。通过 SLIP 或 PPP 连接，你可以向互联网地址发送电子邮件，但如果没有永久连接和注册的域名，就无法直接在系统上接收互联网邮件。不过，如果你没有永久的互联网连接，`fetchmail` 工具是最好的选择。一旦你建立了与 ISP 的拨号连接，`fetchmail` 程序就会将等待在 ISP 邮件服务器上的任何新邮件传输到 Linux 系统上的本地邮件文件夹。然后你就可以使用你喜欢的 Linux 电子邮件客户端阅读和回复邮件。你可能会发现这比使用 `telnet` 登录到你的 ISP 并用 Pine 检查邮件更方便。使用 `man fetchmail` 命令查看使用详情。

如果你想能够直接在 Linux 系统上接收邮件，你需要与你的 ISP 合作注册一个域名并获得永久或 UUCP 连接到互联网。你可以用调制解调器和专用电话线建立永久连接（最高 56 Kbps），或者安装一些昂贵的设备和特殊的电话连接来建立高速链路。
