

## 7
## WEB AND INTERNET USERS

![](img/4ffb1cc24a1b24b49254839643abedb2_204_0.png)

Unix 在互联网领域真正大放异彩。无论你想在桌子底下运行一台高速服务器，还是仅仅想智能高效地上网冲浪，对于互联网交互而言，几乎没有什么不能嵌入到 shell 脚本中的。

互联网工具是可以脚本化的，即使你可能从未这样想过。例如，FTP，这款永远困在调试模式的程序，可以以非常有趣的方式被脚本化，正如第 174 页的脚本 #53 所探讨的那样。Shell 脚本通常可以改善大多数处理互联网某方面的命令行工具的性能和输出。

本书的第一版向读者保证，互联网脚本编写者工具箱中最好的工具是 lynx；现在我们推荐改用 curl。两种工具都提供纯文本的网页界面，但 lynx 试图提供类似浏览器的体验，而 curl 专门为脚本设计，会直接输出你想检查的任何页面的原始 HTML 源代码。

例如，下面展示了使用 curl 获取的 Dave on Film 主页源代码的前七行：

```
```bash
$ curl -s https://www.daveonfilm.com/ | head -7
<!DOCTYPE html>
<html lang="en-US">
<head>
<meta charset="UTF-8" />
<link rel="profile" href="http://gmpg.org/xfn/11" />
<link rel="pingback" href="http://www.daveonfilm.com/xmlrpc.php" />
<title>Dave on Film: Smart Movie Reviews from Dave Taylor</title>
```
```

如果你没有 curl，也可以用 lynx 实现同样的结果，但如果两者都有，我们推荐使用 curl。这就是本章将要使用的工具。

> 本章中网站抓取脚本的一个限制是，如果自本书出版以来网站更改了布局或 API，脚本可能会失效。但如果你能修复 HTML 或 JSON（即使你并不完全理解），你应该能够阅读这些脚本中的任何一个。追踪其他网站的问题正是可扩展标记语言（XML）被创建的原因：它允许网站开发者将网页内容与布局规则分开提供。

### #53 通过 FTP 下载文件

互联网最初的杀手级应用之一就是文件传输，而最简单的解决方案之一就是 FTP，文件传输协议。从根本上说，所有的互联网交互都基于文件传输，无论是网页浏览器请求 HTML 文档及其配套图像文件、聊天服务器在两端之间中继讨论行，还是电子邮件从地球的一端旅行到另一端。

原始的 FTP 程序仍然存在，虽然其界面粗糙，但该程序功能强大、能力出众，值得充分利用。周围有许多更新的 FTP 程序，其中最著名的是 FileZilla（http://filezilla-project.org/）和 NcFTP（http://www.ncftp.org/），此外还有大量漂亮的图形界面可以添加到 FTP 以使其更易于使用。借助一些 shell 脚本包装器的帮助，FTP 对于上传和下载文件来说已经足够好了。

例如，FTP 的典型用例是从互联网下载文件，我们将在列表 7-1 中的脚本中实现这一点。相当频繁地，这些文件位于匿名 FTP 服务器上，其 URL 类似于 ftp://<some server>/<path>/<filename>/。

### The Code

```
#!/bin/bash

# ftpget--Given an ftp-style URL, unwraps it and tries to obtain the
# file using anonymous ftp

anonpass="$LOGNAME@$(hostname)"

if [ $# -ne 1 ] ; then
 echo "Usage: $0 ftp://..." >&2
 exit 1
fi

# Typical URL: ftp://ftp.ncftp.com/unixstuff/q2getty.tar.gz

if [ "$(echo $1 | cut -c1-6)" != "ftp://" ] ; then
 echo "$0: Malformed url. I need it to start with ftp://" >&2
 exit 1
fi

server="$(echo $1 | cut -d/ -f3)"
filename="$(echo $1 | cut -d/ -f4-)"
basefile=$(basename $filename)

echo "$0: Downloading $basefile from server $server

ftp -np << EOF
open $server
user ftp $anonpass
get "$filename" "$basefile"
quit
EOF

if [ $? -eq 0 ] ; then
 ls -l $basefile
fi

exit 0
```

列表 7.1：ftpget 脚本

### How It Works

该脚本的核心是从第 1 行开始馈送给 FTP 程序的命令序列。这体现了批处理文件的本质：馈送给另一个程序的一系列指令，使得接收程序（在本例中为 FTP）认为指令是由用户输入的。在这里我们指定要打开的服务器连接，指定匿名用户

