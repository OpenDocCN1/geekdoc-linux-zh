
`logfile`=`"/var/www/wicked/searchlog.txt"`

```
if [ ! -f $logfile ]; then

  touch $logfile

  chmod +rw $logfile

fi

if [ -w $logfile ]; then

  echo "$(date): $QUERY_STRING" | sed 's/q=\//g;s/+/ /g' >> $logfile

fi

echo "location: https://duckduckgo.com/html/?$QUERY_STRING"

echo ""

exit 0
```

### 列表 8-5：log-duckduckgo-search 脚本

## 工作原理

脚本中最显著的元素与 Web 服务器和 Web 客户端之间的通信有关。输入搜索框的信息以变量 `QUERY_STRING` 的形式发送到服务器，编码方式是将空格替换为 `+`，并将其他非字母数字字符替换为相应的字符序列。然后，当记录搜索模式时，所有的 `+` 都会被安全且简单地转换回空格。否则，搜索模式将不会解码，以防止用户可能尝试的任何花招。（更多细节请参见本章引言）。

一旦记录完成，浏览器将通过 `Location:` 头部值重定向到实际 DuckDuckGo 搜索页面。请注意，无论模式多简单或复杂，简单的追加 `?$QUERY_STRING` 就足以将搜索模式传递到其最终目的地。

此脚本产生的日志文件在每个字符串前都带有当前日期和时间，从而构建出一个数据文件，显示可以按每天、星期、月份等对热门搜索进行分析。这个脚本可以透露许多关于繁忙网站的信息！

## 运行脚本

要使用此脚本，你需要创建 HTML 表单，并且需要确保脚本位于你的服务器上且具有可执行权限。（更多细节请参见第 201 页“运行本章中的脚本”）。不过，我们可以使用 `curl` 来测试脚本。要测试脚本，使用 `curl` 执行一个带有带有查询参数 `q` 的 HTTP 请求：

```
$ curl '10.37.129.5/cgi-bin/log-duckduckgo-search.cgi?q=metasploit'

<!DOCTYPE HTML "-//I//DTD HTML 2.0//EN">

<html

<head>

<title>302 Found</title>

</head>

<body>

<h1>Found</h1>

<p>The document has moved <a href="https://duckduckgo.com/http?=metasploit">here</a>a<a>.</a>.</p>

<hr>

<address>Apache/2.4.7 (Ubuntu) Server at 10.37.129.5 Port 80</address>

</body>

</html>

$
```

> 然后，通过将搜索日志的内容打印到控制台屏幕来验证搜索是否已记录：

```
$ cat searchlog.txt

Thu Mar 9 17:20:56 CST 2017: metasploit

$
```

## 结果

在浏览器中打开脚本，结果完全如预期般来自 DuckDuckGo，如 8-2 所示。

![](img/954a28cc04c09826495e330f44c0085b_237_0.png)

图 8-2：DuckDuckGo 搜索结果出现了，但搜索被记录了！

在繁忙的日子里，你无疑会发现 `tail -f searchlog.txt` 命令监控搜索非常有参考价值，因为你可以了解到人们在网上在寻找什么。

# 破解脚本

如果在网站的每个页面都使用该脚本，那么了解用户在执行搜索时的状态将很有用。这可以让你对某些解释良好的特定页面获得深刻见解。例如，用户是否总是从特定页面搜索对某个主题的更详细说明？记录关于用户从哪个页面搜索的额外信息（如 `Referer` HTTP 头部）将是脚本的一个极佳补充。

## #65 动态构建网页

许多网站都有每天都在变化的图形和其他元素。诸像 Bill Holbrook 的 *Kevin & Kell* 这样的网络漫画就是一个很好的例子。在他的网站上，首页始终显示最新的漫画，而且该网站为单个漫画使用的命名约定很容易进行逆向，允许你将漫画包含在自己的页面中，如 8-6 所示。从另一个网站抓取内容时，有很多版权问题需要考虑。在本例中，我们获得了 Bill Holbrook 的明确许可，可以在自己的网站上复制任何版权保护材料。

## 代码

```
#!/bin/bash

# kevin-and-kell--动态构建一个网页来显示

# 来自 Bill Holbrook 的最新 "Kevin and Kell" 漫画

# 引用权限

month="$(date +%m)"

day="$(date +%d)"

year="$(date +%Y)"

echo "Content-type: text/html"

echo "<html><body bgcolor=white><center>"

echo "<table border=\"0\" cellpadding=\"2\" cellspacing=\"2\">"

echo "<tr><th color=white>Kevin & Kell</th></tr>"

echo "<tr><td><img src=\"http://www.kevinandell.com/${year}/${day}.jpg\" alt=\"Kevin & Kell\"></td></tr>"

echo "</table>"

echo "</center></body></html>"
```

### 列表 8-6：动态构建网页的脚本

## 工作原理

脚本中最显著的元素与 Web 服务器和 Web 客户端之间的通信有关。输入搜索框的信息以变量 `QUERY_STRING` 的形式发送到服务器，编码方式是将空格替换为 `+`，并将其他非字母数字字符替换为相应的字符序列。然后，当记录搜索模式时，所有的 `+` 都会被安全且简单地转换回空格。否则，搜索模式将不会解码，以防止用户可能尝试的任何花招。（更多细节请参见本章引言）。

一旦记录完成，浏览器将通过 `Location:` 头部值重定向到实际 DuckDuckGo 搜索页面。请注意，无论模式多简单或复杂，简单的追加 `?$QUERY_STRING` 就足以将搜索模式传递到其最终目的地。

此脚本产生的日志文件在每个字符串前都带有当前日期和时间，从而构建出一个数据文件，显示可以按每天、星期、月份等对热门搜索进行分析。这个脚本可以透露许多关于繁忙网站的信息！

## 运行脚本

要使用此脚本，你需要创建 HTML 表单，并且需要确保脚本位于你的服务器上且具有可执行权限。（更多细节请参见第 201 页“运行本章中的脚本”）。不过，我们可以使用 `curl` 来测试脚本。要测试脚本，使用 `curl` 执行一个带有查询参数 `q` 的 HTTP 请求：

```
$ curl '10.37.129.5/cgi-bin/log-duckduckgo-search.cgi?q=metasploit'

<!DOCTYPE HTML "-//I//DTD HTML 2.0//EN">

<html

<head>

<title>302 Found</title>

</head>

<body>

<h1>Found</h1>

<p>The document has moved <a href="https://duckduckgo.com/http?=metasploit">here</a>a<a>.</a>.</p>

<hr>

<address>Apache/2.4.7 (Ubuntu) Server at 10.37.129.5 Port 80</address>

</body>

</html>

$
```

> 然后，通过将搜索日志的内容打印到控制台屏幕来验证搜索是否已记录：

```
$ cat searchlog.txt

Thu Mar 9 17:20:56 CST 2017: metasploit

$
```
