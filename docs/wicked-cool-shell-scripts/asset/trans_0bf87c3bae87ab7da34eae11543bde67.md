

### 结果

在网页浏览器中打开脚本，结果来自 DuckDuckGo，正如预期的那样，如图 8-2 所示。

![](img/4ffb1cc24a1b24b49254839643abedb2_237_0.png)

在繁忙的网站上，你会毫无疑问地发现，使用命令 `tail -f searchlog.txt` 监控搜索非常有信息量，因为你能了解到人们在线上搜索什么。

### 改进脚本

如果搜索框在网站的每个页面上都使用，那么知道用户在执行搜索时所在的页面就会很有用。这可以带来关于特定页面是否解释得足够清楚的好见解。例如，用户是否总是从某个给定页面搜索该主题的更多澄清？记录用户搜索来源页面的额外信息，例如 Referer HTTP 头，将是对脚本的极大补充。

## #65 即时构建网页

许多网站每天都有图形和其他元素的变化。像 Bill Holbrook 的 Kevin & Kell 这样的网络漫画就是一个很好的例子。在他的网站上，首页始终展示最新的条漫，而且该网站对单个漫画使用的图像命名约定很容易逆向工程，从而允许你将卡通包含在自己的页面中，如清单 8-6 所述。

> 警告 我们律师的一句话：当你从另一个网站抓取内容用于自己的网站时，有很多版权问题需要考虑。对于本示例，我们已获得 Bill Holbrook 的明确许可，将他的漫画条带包含在本书中。我们鼓励你在自己网站上复制任何受版权保护的材料之前，先获得许可，以免自己陷入被律师包围的深坑。

### 代码

```bash
#!/bin/bash

# kevin-and-kell--Builds a web page on the fly to display the latest
# strip from the cartoon "Kevin and Kell" by Bill Holbrook.
# <Strip referenced with permission of the cartoonist>

month="$(date +%m)"
day="$(date +%d)"
year="$(date +%y)"

echo "Content-type: text/html"
echo ""

echo "<html><body bgcolor=white><center>"
echo "<table border=\"0\" cellpadding=\"2\" cellspacing=\"1\">"
echo "<tr bgcolor=\"#000099\">"
echo "<th><font color=white>Bill Holbrook's Kevin &amp; Kell</font></th></tr>"
echo "<tr><td><img "

# Typical URL: http://www.kevinandkell.com/2016/strips/kk20160804.jpg

/bin/echo -n " src=\"http://www.kevinandkell.com/20${year}/"
echo "strips/kk20${year}${month}${day}.jpg\"/>"
echo "</td></tr><td align=\"center\">"
echo "<p>"
echo "&copy; Bill Holbrook. Please see"
echo "<a href=\"http://www.kevinandkell.com/\">kevinandkell.com</a>"
echo "for more strips, books, etc."
echo "</td></tr></table></center></body></html>"

exit 0
```

清单 8-6：kevin-and-kell 脚本

### 工作原理

快速查看 Kevin & Kell 首页的源代码可知，某部漫画的 URL 由当前年份、月份和日期构建，如下所示：

```
http://www.kevinandkell.com/2016/strips/kk20160804.jpg
```

要即时构建包含该条漫的页面，脚本需要确定当前的年份（两位数字值）、月份和日期（两者如需则带前导零）。其余脚本只是 HTML 包装，使页面看起来漂亮。事实上，考虑到由此产生的功能，这个脚本非常简单。

### 运行脚本

与本章中的其他 CGI 脚本一样，该脚本必须放置在适当的目录中，以便可以通过网络访问，并具有适当的文件权限。然后只需从浏览器调用正确的 URL 即可。

### 结果

网页每天自动更改。对于 2016 年 8 月 4 日的条漫，结果页面如图 8-3 所示。

![](img/4ffb1cc24a1b24b49254839643abedb2_239_0.png)

图 8-3：即时构建的 Kevin & Kell 网页

### 改进脚本

如果有灵感，这个概念可以应用于网络上的几乎任何东西。你可以抓取 CNN 或南华早报的头条新闻，或从杂乱的网站获取随机广告。同样，如果你要将内容作为你网站的组成部分，请确保它是公共领域的，或者你已安排好许可。

