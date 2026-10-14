
“丢失”和平均响应时间为7245毫秒（7.245秒），这非常糟糕。更合理的Ping响应时间应在750毫秒以下。

在尝试通过Telnet或FTP连接之前，你可以使用Ping来测试连接速度。尤其是在使用FTP时，通常会有多个服务器镜像同一组文件，因此选择最快的那一个。

## 使用 TIN 访问 USENET

Tin是一个基于文本的程序，你可以使用它阅读和发布Usenet新闻组。在初始菜单中，你可以选择要阅读的新闻组，Tin会显示该组中的当前帖子，如下所示：

```
Group Selection (news.myserver.com $)
1  884  alt.internet.services
2  167  news.announce.newusers
3  343  news.newusers.questions
4   49  news.answers
5  183  comp.internet.net-happenings

<n>=set current to n, TAB=next unread, /=search pattern, c)atchup,
g)oto, j=line down, k=line up, h)elp, m)ove, q)uit, r=toggle unread,
s)ubscribe, S)ub pattern, u)nsubscribe, U)nsub pattern, y)ank in/out
```

你可以使用光标键进行所有导航操作。
要启动Tin，必须先设置NNTP_SERVER（网络新闻传输协议服务器）环境变量，将其指向ISP的新闻服务器名称（通常使用news即可）。在提示符下执行此处所示的命令，并将其添加到/etc/bashrc文件中（必须以root身份登录），以便下次开机时自动设置。

```
NNTP_SERVER=news
```

设置环境变量后，输入下面显示的其中一个Tin启动命令：

```
rtin -rq      Use the first time only
rtin -rqn     Use after the first time
```

第一次使用Tin时，它会从ISP服务器下载所有可用新闻组的庞大列表，因此如果第一个屏幕要过几分钟才出现，请不要感到惊讶。
有关使用Tin的更多信息，请使用man tin命令阅读该程序的优秀在线帮助。

## 使用 LYNX

Lynx是一个基于文本的Web浏览器。你无法看到网页上的图形，但对某些人来说，这反而是一个优点。许多网页加载了大量无意义的图片，加载时间很长，却几乎没有实际价值。因此，Lynx通常能比图形浏览器更快地让你找到所需信息。下面是一个Lynx屏幕可能的样子：

```
Yahoo!

[ Reuters News Headlines ] [ What's New ] [ Cool Sites ]
[ Write Us ] [ Add URL ] [ Random Link ] [ info ]

Search Options

* Arts -- Humanities, Photography, Architecture ...
* Business and Economy [Xtra!] -- Directory, Investments ...
* Computers and Internet [Xtra!] -- Internet, WWW, Software
* Education -- Universities, K-12, Courses ...
* Entertainment [Xtra!] -- TV, Movies, Music, Magazines ...
* Government -- Politics [Xtra!], Agencies, Law, Military ...
* Health [Xtra!] -- Medicine, Drugs, Diseases, Fitness ...
* News [Xtra!] -- World [Xtra!], Daily, Current Events ...
* Recreation and Sports [Xtra!] -- Sports, Games, Travel ...

Arrow keys: Up/Down to move. Right to follow link; Left to go back.
H)elp O)ptions P)rint G)o M)ain screen Q)uit /=search
```

除了显示网页，Lynx还可以为你浏览FTP站点并下载文件。它还可以发送电子邮件、阅读或发布Usenet新闻组，以及显示存储在gopher服务器上的信息。要从Linux命令行启动Lynx客户端，请输入lynx命令，后面可以跟一个Web地址（URL），如下所示：

- `lynx` 显示默认网页。
- `lynx http://www.yahoo.com` 显示指定的网页。
- `lynx ftp://ftp.netscape.com` 显示FTP站点上的文件。
- `lynx gopher://cwis.usc.edu` 显示gopher站点上的文件。
- `lynx mailto:user@site.com` 准备发送电子邮件。
- `lynx news:rec.humor.funny` 显示新闻组中的帖子。

使用Lynx中的help命令，可以了解更多关于在没有鼠标的情况下浏览网页的信息。

## 使用 WHOIS

whois命令将搜索InterNIC的中央域名注册表，并给出关于某个域的信息，例如该域的所有者、所在位置以及如何联系所有者。以下是whois输出的一个示例：

```
whois aol.com
America Online (AOL-DOM)
12100 Sunrise Valley Drive
Reston, Virginia 22091 USA

Administrative Contact:
O'Donnell, David B (DB03) PMDatropos@AOL.COM
703/453-4255 (FAX) 703/453-4102
Technical Contact, Zone Contact:
America Online (AOL-NOC) trouble@aol.net
703-453-5862
```
