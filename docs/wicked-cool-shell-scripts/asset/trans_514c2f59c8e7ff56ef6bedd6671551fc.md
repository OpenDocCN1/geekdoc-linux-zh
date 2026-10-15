

# 运行脚本

脚本可以通过以下行嵌入到符合 SSI 的网页中：

```
<!--#exec cmd="randomquote.sh samplequotes.txt"-->
```

大多数服务器要求包含此服务器端包含的网页使用 .shtml 文件扩展名，而不是更传统的 .html 或 .htm。通过这样简单的更改，randomquote 命令的输出将被合并到网页的内容中。

# 结果

你可以通过直接调用它在命令行上测试此脚本，如清单 8-10 所示。

```
$ randomquote samplequotes.txt
Neither rain nor sleet nor dark of night...
$ randomquote samplequotes.txt
The rain in Spain stays mainly on the plane? Does the pilot know about this?
```

清单 8-10：运行 randomquote 脚本

# 修改脚本

让 randomquote 使用的数据文件包含一组图形图像名称的列表会很简单。然后你就可以使用此脚本在图形集之间轮换。一旦你想到这一点，你会意识到可以用这个想法做很多事情。

# 9

# WEB AND INTERNET ADMINISTRATION

![](img/4ffb1cc24a1b24b49254839643abedb2_248_0.png)

如果你正在运行 Web 服务器或负责一个网站，无论是简单还是复杂，你很可能会频繁地执行某些任务，尤其是识别损坏的内部和外部站点链接。使用 shell 脚本，你可以自动化其中许多任务，以及一些常见的客户端/服务器任务，例如管理受密码保护的网站目录上的访问信息。

# 69 识别损坏的内部链接

第 7 章中的一些脚本强调了 lynx 纯文本 Web 浏览器的功能，但在这个强大的软件应用程序中还隐藏着更多功能。对 Web 管理员特别有用的一个功能是遍历功能（使用 -traversal 启用），它会导致 lynx 尝试遍历站点上的所有链接以查看是否有任何损坏。此功能可以在一个简短的脚本中利用，如清单 9-1 所述。

# 代码

```
#!/bin/bash
# checklinks--Traverses all internal URLs on a website, reporting
# any errors in the "traverse.errors" file

# Remove all the lynx traversal output files upon completion.
trap "$(which rm) -f traverse.dat traverse2.dat" 0

if [ -z "$1" ]; then
  echo "Usage: checklinks URL" >&2
  exit 1
fi

baseurl=$(echo $1 | cut -d/ -f3 | sed 's/http:\/\//')

lynx -traversal -accept_all_cookies -realm "$1" > /dev/null

if [ -s "traverse.errors" ]; then
  /bin/echo -n "$(wc -l < traverse.errors)" errors encountered.
  echo Checked $(grep '^http' traverse.dat | wc -l) pages at ${1}:
  sed "s|$1|g" < traverse.errors
  mv traverse.errors ${baseurl}.errors
  echo "A copy of this output has been saved in ${baseurl}.errors"
else
  /bin/echo -n "No errors encountered.";
  echo Checked $(grep '^http' traverse.dat | wc -l) pages at ${1}
fi

if [ -s "reject.dat" ]; then
  mv reject.dat ${baseurl}.rejects
fi

exit 0
```

清单 9-1：checklinks 脚本

# 工作原理

此脚本中的绝大多数工作由 lynx 完成；脚本只是对生成的 lynx 输出文件进行调整以总结并以吸引人的方式显示数据。lynx 输出文件 reject.dat 包含指向外部 URL 的链接列表（请参阅第 220 页的脚本 #70，了解如何利用此数据），traverse.errors 包含无效链接的列表（此脚本的核心），traverse.dat 包含检查过的所有页面的列表，而 traverse2.dat 与 traverse.dat 相同，只是它还包括访问的每个页面的标题。

Lynx 命令可以接受很多不同的参数，在本例中我们需要使用 -accept_all_cookies，这样程序就不会停下来询问我们是否要接受或拒绝来自页面的 cookie。我们还使用 -realm 来确保脚本只检查该点或站点树中“更低”位置的页面，而不是它遇到的每个链接。如果没有 -realm，它会像疯子一样遍历，可能挖掘出成千上万的页面。当我们在没有 -realm 的情况下对 http://www.intuitive.com/wicked/ 运行 -traversal 时，它在运行了两个多小时后找到了超过 6,500 个页面。使用 -realm 标志，它在几分钟内就确定了 146 个页面需要检查。

# 运行脚本

要运行此脚本，只需在命令行上指定一个 URL。你可以遍历并检查你想要的任何网站，但要小心：检查像 Google 或 Yahoo! 这样的网站将花费永远，并且在过程中耗尽你的磁盘空间。

# 结果

让我们检查一个没有错误的小型网站（清单 9-2）。

```
$ checklinks http://www.404-error-page.com/
No errors encountered. Checked 1 pages at http://www.404-error-page.com/
```

清单 9-2：在没有错误的网站上运行 checklinks

果然，一切都很好。如何关于稍大一点的站点？清单 9-3 显示了 checklinks 对于可能存在损坏链接的站点可能打印的内容。

```
$ checklinks http://www.intuitive.com/library/
5 errors encountered. Checked 62 pages at http://intuitive.com/library/:
index/ in BeingEarnest.shtml
Archive/f8 in Archive/ArtOfWriting.html
Archive/f11 in Archive/ArtOfWriting.html
Archive/f16 in Archive/ArtOfWriting.html
Archive/f18 in Archive/ArtOfWriting.html
A copy of this output has been saved in intuitive.com.errors
```

清单 9-3：在存在损坏链接的较大网站上运行 checklinks

这意味着文件 BeingEarnest.shtml 包含一个无法解析的链接到 /index/：文件 /index/ 不存在。ArtOfWriting.html 文件中还有四个奇怪的链接错误。最后，在清单 9-4 中，让我们检查 Dave 的电影评论博客，看看可能潜伏着什么链接错误。

```
$ time checklinks http://www.daveonfilm.com/
No errors encountered. Checked 982 pages at http://www.daveonfilm.com/

real 50m15.069s
```

