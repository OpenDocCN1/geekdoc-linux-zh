

# 第 4 章：应用概述

## Wget

| | |
|--- |--- |
| 优点 | 灵活、命令行操作、支持 SSL、免费 |
| 缺点 | 无法在 HTML 中搜索注释、电子邮件地址等 |
| 最终分析 | 命令行爱好者的极佳镜像克隆工具 |

Wget (http://www.gnu.org/wget/wget.html) 是一款适用于 Windows 和 Unix 的命令行工具，用于下载网站内容。其用法非常简单：

```
[root@medle] # wget -r www.victim.com
--18:17:30-- http://www.victim.com/
  => http://www.victim.com/index.html'
Connecting to www.victim.com:80... connected!
HTTP request sent, awaiting response... 200 OK
Length: 21,924 [text/html]
OK.......................... 100 % 88.84 KB/s
18:17:31 (79 KB/s) -- www.victim.com/index.html' saved [21924/21924]
Loading robots.txt; please ignore errors.
--18:17:31-- http://www.victim.com/robots.txt
  => `www.victim.com/robots.txt'
Connecting to www.victim.com:80... connected!
HTTP request sent, awaiting response... 200 OK
```

## Hacking Exposed Web Applications

Length: 458 [text/html]
OK
100% @ 22.36 KB/s
...(持续下载整个站点)...



“-r”或“递归”（recursive）选项指示 wget 跟踪首页上的每一个链接。这将创建一个“www.victim.com”目录，并用该网站的所有 HTML 文件和目录填充该目录。wget 的一个主要优势是它会跟踪每一个可能的链接。它将下载应用程序传递给页面的每个参数的输出。例如，网站的 viewer.asp 文件可能会被下载四次：

- viewer.asp@ID=555
- viewer.asp@ID=7
- viewer.asp@ID=42
- viewer.asp@ID=23

@ 符号代表原始 URL 中的 ? 隔分隔符。ID 是传递给 viewer.asp 文件的第一个参数。某些网站可能需要更高级的选项，例如支持代理和 HTTP Basic 身份认证。认证受以下内容保护：

```
[root@medle] wget -r --http-user:dwayne --http-path:wodoelf \
> https://www.victim.com/secure/
--20:19:11-- https://www.victim.com/secure/
=> 'www.victim.com/secure/index.html'
```

Connecting to www.victim.com... connected!
HTTP request sent, awaiting response... 200 OK
Length: 251 [text/html]
100% @ 21.99 KB/s
OK
...持续下载整个站点...

Wget 的目的很明确：从网站检索文件。筛选结果则需要任何 UNIX 系统或 Windows Cygwin 上可用的其他简单命令行工具。

## Teleport Pro

| 优点: | 易于使用、不支持 SSL、商业软件 |
| 缺点: | 无法在 HTML 中搜索注释、电子邮件地址等 |
| 最终分析: | 适用于查找静态文件 |

当然，对于 Windows 用户来说，总有 GUI 界面。Teleport Pro (http://www.tenmax.com/teleport/pro/home.htm) 为 wget 以及收集信息的筛选工具引入了图形界面。

使用 Teleport Pro，你可以指定 URL 的任何部分来开始爬取，控制其索引的深度和文件类型，并在本地保存副本。该工具的主要缺点是它将镜像站点保存在 Teleport Pro 项目中，此 TPP 文件无法用 grep 等工具进行搜索。Teleport Pro 如图 4-2 所示。

## Black Widow

| 优点: | 搜索功能、命令行 |
| 缺点: | 支持 SSL、商业软件 |
| 最终分析: | 极佳的 GUI 镜像工具 |

Black Widow (http://www.softbytelabs.com/Blackow/) 通过提供搜索和收集界面扩展了 Teleport Pro 的功能。Black Widow 的另一个优点是你可以将文件下载到硬盘上的目录。

![](img/2c61c2d28445b77d9266972920f432d_147_0.png)

图 4-2 Teleport Pro 的许多选项

该目录对于 grep 和 findstr 等工具更加友好。Black Widow 如图 4-3 所示。

## WebSleuth

| | |
| --- | --- |
| 优点 | 表单、Cookie、参数 URL 等 |
| 缺点 | 必须手动访问网站的每个页面 |
| 最终分析 | 强大的工具，对输入验证攻击更有用 |

WebSleuth (http://geities.com/dzzie/sleuth/) 是一款优秀的工具，结合了爬虫和 Achilles 等个人代理的功能。我们将在后面的章节讨论输入验证攻击时详细查看 WebSleuth。现在我们使用 URL 摘要功能。此快照包含了外部脚本引用（服务器上 JavaScript 文件的链接）、Cookie 信息、HTML 注释等。

WebSlash 基本上是封装在 Visual Basic 中的 Internet Explorer，但不要被这个描述误导了。它是一个强大的工具。其界面如图 4-4 所示。

一个示例报告包含了各种有用信息：

```
2/1/2002    11:40:46 AM    Saved as: D:\temp\Sleuth_Report.txt
如果你想保存此文件，请执行另存为，否则它将被下一个报告自动覆盖！
```

```
Page: https://www3.victim.com/lcs_corp/Logon
Cookie: DataKey=0002SNJ4PT00GCFLPR2N3G2
Links:
```

![](img/2c61c2d28445b77d9266972920f432d_148_0.png)

图 4-3 Black Widow 将站点内容镜像到本地硬盘。

