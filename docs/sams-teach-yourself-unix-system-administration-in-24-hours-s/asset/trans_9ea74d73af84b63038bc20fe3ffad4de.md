

```apache
</VirtualHost>

<VirtualHost *>
ServerName www.sherlockworld.com
DocumentRoot /web/sherlockworld
ServerAlias sherlockworld.com holmes.sherlockworld.com
</VirtualHost>
```

请注意，尽管第一个虚拟主机定义指定了新的 ErrorLog、CustomLog 和 ServerAdmin，但第二个域名可以继承整个服务器的值（例如，配置文件中先前定义的值）。然而，sherlockworld.com 也将子域名 holmes.sherlockworld.com 作为别名；它将在与主站点 sherlockworld.com 相同的 DocumentRoot 下提供相同的网页。（当然，你仍然需要为 holmes.sherlockworld.com 提供 DNS 记录，但如果需要，可以将其添加到主 sherlockworld.com 的 DNS 记录中。）

Apache 虚拟主机的一个伟大特性是，每个虚拟主机都可以自动拥有自己的访问日志和错误日志文件副本。这意味着作为系统管理员，你无需从中央日志文件中拆分出特定域名的流量，这是一大福音。此外，它还确保其他域名的日志流量可以保持私密，因为网站所有者并不总希望别人看到他们的实际流量。

请注意，每个 VirtualHost 都有一个新 DocumentRoot。这是至关重要的，而且每个 DocumentRoot 必须唯一，虚拟主机才能正常工作。如果忽略了这一重要步骤，你会发现多个域名最终指向同一个主页，从而破坏了虚拟主机的目的。

3. 虚拟主机主配置的另一半是为每个新的 DocumentRoot 指定一个 Directory 块（虽然从技术上讲，你可以让它默认为配置文件顶部为 / 设置的权限，但最好明确指示特定域名的所有者可以做什么或不能做什么，以便你随时快速复查任何给定用户的安全性）：

```apache
<Directory "/web/niftylister">
Options Indexes FollowSymLinks ExecCGI
AllowOverride None
Order allow,deny
Allow from all
</Directory>
<Directory "/web/sherlockworld">
Options Indexes FollowSymLinks ExecCGI Includes
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

在这种特定配置中，两者几乎具有相同的权限和选项设置，但请注意，通过从 Options 行中省略 Includes，niftylister.com 的服务器端包含（server-side includes）已被禁用。

4. 这就是全部所需！仅剩的步骤是确保新的 DocumentRoot 目录存在，并至少有一些基本的欢迎页面，以避免出现“页面未找到”的错误信息。

请亲自访问这三个域名，看看这些网站有多么不同，尽管它们都来自同一台 Web 服务器：staging.intuitive.com、www.sherlockworld.com 和 www.niftylister.com。

有必要简要展示一下 /web 目录的组织结构：

```console
# ls -l /web
total 12
drwxr-xr-x 2 root root 1024 Nov 22 09:25 campusdev
drwxr-xr-x 10 root root 1024 Dec 18 21:23 cbs
drwxr-xr-x 2 root root 1024 Nov 22 09:35 cbfacilities
drwxr-xr-x 10 root root 1024 Dec 18 05:20 chatter
drwxr-xr-x 8 root root 1024 Nov 22 09:45 launchline
drwxr-xr-x 5 root root 1024 Nov 22 22:40 niftylister
drwxr-xr-x 5 root root 1024 Nov 22 09:58 niftyseller
drwxr-xr-x 2 root root 1024 Nov 22 10:06 sherlockworld
drwxr-xr-x 2 root root 1024 Dec 18 05:20 smartpage
drwxr-xr-x 6 root root 1024 Mar 21 16:20 staging
drwxr-xr-x 5 root root 1024 Nov 22 10:18 windward
```

你可以看到，实际上有不少域名由这个系统提供服务。进入任何一个目录，你会看到该网站的各个 HTML 文件、图片等，正如预期的那样，它们与服务器上的所有其他网站整齐地分离开来：

```console
# ls sherlockworld
about.html            gutnavbar.js          scandal-bohemia.html
beryl-coronet.html    gutsmallprint.js      smallprint.js
blue-carbuncle.html   hmenu.js              speckled-band.html
boscombe-valley.html  holmes.css            the-small-print.html
case-of-identity.html how-to-access.html    topnavbar.js
copper-beeches.html   index.html            topnav.js
crashcourse.js        noble-bachelor.html   twisted-lip.html
engineers-thumb.html  originals-from-gutenberg.txt
five-orange-pips.html red-headed-league.html
```

而且，正如我们从 httpd.conf 文件中所知，为 sherlockworld.com 提供服务的默认页面是 index.html：

```
# head sherlockworld/index.html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<HTML>
<META HTTP-EQUIV="content-type" CONTENT="text/html; charset=iso-8859-1">
<META NAME="keywords" CONTENT="Sherlock Holmes,Arthur Conan Doyle,Dr. Watson,John Watson,Sherlockian,Baker Street,221b,Moriarty,detective,mystery,London,England,Jeremy Brett,Christopher Plummer,Scotland Yard">
<META NAME="description" CONTENT="A reader-friendly library of some of the best Sherlock Holmes stories, as written by Arthur Conan Doyle and narrated by Dr. Watson. Inspired by the work of Project Gutenberg. Note: Site won't work with Netscape 4.x">
<META NAME="ROBOTS" CONTENT="ALL">
<TITLE>The Adventures of Sherlock Holmes, by Arthur Conan Doyle</TITLE>
```

虚拟主机概念简单，执行也简单，是 Unix 作为互联网服务器的一款“杀手级应用”。作为系统管理员，如果你在 ISP 或任何其他提供网站服务的公司工作，配置和维护这类设置是你的职责，因此，它如此简单直接应该让你感到宽慰。

到目前为止，我运行不同的 Web 托管服务器已将近 10 年（说实话，真有点不可思议！），我的经验让我得出两条强烈建议：

1. 将所有网站放在不同的分区或不同的物理磁盘上。这有助于管理磁盘空间并为客户维护配额（有关如何设置简单的 Web 托管磁盘使用配额的更多详细信息，请参阅第 12 小时“管理磁盘配额”）。
2. 设置别名，这样当用户连接到服务器时，要么直接进入他们的 Web 托管账户（总体而言这不是一个糟糕的策略——例如，只需将主目录设置为 /web/sherlockworld），要么在主目录中有一个链接，将他们带到文件系统上适当的位置（也许是 public_html，以便与其他托管公司保持一致）。

如果能够避免，就不要让人们通过 telnet 或 ssh 访问系统。可以为他们设置 ftp（参见第 19 小时“运行互联网服务”），并且同样将他们的主目录也设为他们的 Web 目录。

只需几分钟的组织和正确设置，你就能轻松管理一台托管数百个网站的服务器。

## 保持系统安全

前面关于设法避免授予用户 telnet 或 ssh 访问系统权限的评论，只是冰山一角：Unix 系统安全。

尽管我们显然没有足够的篇幅（或时间）来深入讨论这个主题，但在《24小时学会Unix系统管理》的结尾，简要涉足系统和服务器安全领域是值得的。

安全有两个基本类别——把人们挡在外面和把人们限制住。我思考安全问题时，总记得它是一门权衡之学：你的系统越安全，它的可访问性就越低。如果过于安全，没有人能使用它；如果过于不安全，任何人——包括坏人——都可以为所欲为。

显然，找到适当的平衡点、折中之道，才是计算机安全的目标。对于给定系统，安全与能力之间的精确平衡取决于该系统的用途，以及其用户群体的成熟度、能力、可信度和类型。

如果你是在为一所本地大学的计算机科学专业本科生管理一个共享 Unix 系统，我想说，你正处于麻烦的爆发点：那些聪明、好奇的计算机类型的人，肯定会到处查看并尝试实验。在这种情况下，最大的危险很可能来自用户群体内部，而不是外部人员。

另一方面，如果你管理的是一组托管服务器，只有六名经过审查和担保的公司管理员才能访问，那么你可以大幅调高安全级别，并知道你的最大危险将来自未经授权的外部人员。

那么，Unix 如何让你管理这些安全问题呢？通过特定安全工具、第三方软件以及有关安全和使用的具体站点策略的结合来实现。

### 密码

第一层也是最简单的安全层是密码。是的，这听起来显而易见甚至有点愚蠢，但破解系统最常见的方法是通过选择不当的密码。过去，名字或字典单词之类的密码很容易成为攻击目标（例如，如果 Joe 的密码是 eoj 或 joseph）。如今，计算机速度如此之快，如果破解者拿到加密密码字符串的副本，他一两个小时就能加密字典中的所有单词以及大量常见变体（例如 jump! 或 ?jump）。因此，确保系统安全的最简单步骤，就是确保你的用户定期更改密码，并且生成的密码要复杂且变化足够多，使得破解者需要几天而不是几秒钟才能猜中密码。

哦，还有，不要把你的密码写下来。你永远不知道……

### rlogin

还有一种 Unix 工具叫做 rlogin，它把一种用于访问受信任远程系统的简单“无需登录”机制与访问该功能所需的软件结合起来。这不是一个好主意，聪明的破解者会立即在系统上搜索 .rhosts 或 /etc/hosts.equiv 文件（其中包含受信任的主机列表；

