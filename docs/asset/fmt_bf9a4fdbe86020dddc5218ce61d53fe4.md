
```
Source: http://www.vancraist.com/search/rss.xml?format=Mozilla

<?xml version="1.0" encoding="UTF-8"?>

<rss xmlns="http://www.w3.org/2005/02/rss2"
xmlns:link="http://www.vancraist.com/search/rss.xml"
xmlns:content="http://www.w3.org/2005/01/xml-namespaces#"
xmlns:atom="http://www.w3.org/2005/Atom"
xmlns:n xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:media="http://search.yahoo.com/apps/1.0/"
xmlns:it="http://www.w3.org/rss/1.0/modules/"
xmlns:gd="http://www.w3.org/2005/01/geo/#"
xmlns:tag="http://www.w3.org/dc/elements/1.1/"
xmlns:creator="http://purl.org/dc/elements/1.1/"
xmlns:rights="http://purl.org/dc/elements/1.1/"
xmlns:link href="http://www.vancraist.com/search/rss.xml?format=Mozilla">
<channel>
<title>Search Results</title>
<description>RSS search results</description>
<link>http://www.vancraist.com/search/rss.xml?format=Mozilla</link>
<guid:url>http://www.vancraist.com/search/rss.xml?format=Mozilla</guid:url>
<pubDate>Wed, 21 May 2023 00:00:00 +0000</pubDate>
<item>
<guid:url>http://www.vancraist.com/search/rss.xml?format=Mozilla&q=123</guid:url>
<title>123</title>
<description>description for 123</description>
<link>http://www.vancraist.com/search/rss.xml?format=Mozilla&q=123</link>
<pubDate>Wed, 21 May 2023 00:00:00 +0000</pubDate>
<dc:creator>Vancraist</dc:creator>
<dc:category>Search for 123</dc:category>
</item>
</channel>
</rss>
```

![](img/532f1b7284ceaabe875a6e3330711435_173_1.png)

下载

首页 下载

位置

- 最近 桌面 文档 下载 垃圾 浏览 网络

首先是检查 URL 是否来自 Incom。如果是，将对 Cakebuilder 执行。现在，假设你的自定义 API 来自 Incom，我们将看看结果会落到何处。

使用 utf-8 创建了一个新的 `DOMDocument`。之后，使用 `getParser()` 方法解析 XML。此时，你拥有了来自 Incom 的 XML 对象。对于每个 XML 馈源，结果将是一个 XML 文件，并会带有 Cakebuilder 的每个标签列为 'result'，或者是 `$JobSearchResult`。

对于此示例，关于如何进行解释的说明，你可以直接从 Incom 获取你的 API URL 并将其加载到 `result` 中。它将是一个 XML 文件，并显示每个项目馈源的日期和数据。

一旦看到了馈源中的变量，就会根据 URL 在原始变量 `$origin` 上创建条件。通过这一点，你可以在运行脚本时在浏览器中看到来源。最后，在函数的末尾，`$item_array` 包含了所有创建时的日期和标题。包含每个数据的之前的字符串由逗号分隔。

## 函数与条件

现在往回看一点，你是否注意到 `custom_url()` 函数仅在 URL 不来自 Incom 或 Cakebuilder 时返回？如果它来自 Incom 或 Cakebuilder 之一呢？由于 Incom 和 Cakebuilder 具有不同的 XML 标签，你将获得一组特定的项目进行传递。为了记住这一点，你可以使用代码示例中未的 XML 文件解析技术——只需遵循模式并创建所需的参数。

![](img/532f1b7284ceaabe875a6e3330711435_173_0)

```
Source: http://www.vancraist.com/search/rss.xml?format=Mozilla

<?xml version="1.0" encoding="UTF-8"?>

<rss xmlns="http://www.w3.org/2005/02/rss2"
xmlns:link="http://www.vancraist.com/search/rss.xml"
xmlns:content="http://www.w3.org/2005/01/xml-namespaces#"
xmlns:atom="http://www.w3.org/2005/Atom"
xmlns:n xmlns:dc="http://purl.org/dc/elements/1.1/"
xmlns:media="http://search.yahoo.com/apps/1.0/"
xmlns:it="http://www.w3.org/rss/1.0/modules/"
xmlns:gd="http://www.w3.org/2005/01/geo/#"
xmlns:tag="http://www.w3.org/dc/elements/1.1/"
xmlns:creator="http://purl.org/dc/elements/1.1/"
xmlns:rights="http://purl.org/dc/elements/1.1/"
xmlns:link href="http://www.vancraist.com/search/rss.xml?format=Mozilla">
<channel>
<title>Search Results</title>
<description>RSS search results</description>
<link>http://www.vancraist.com/search/rss.xml?format=Mozilla</link>
<guid:url>http://www.vancraist.com/search/rss.xml?format=Mozilla</guid:url>
<pubDate>Wed, 21 May 2023 00:00:00 +0000</pubDate>
<item>
<guid:url>http://www.vancraist.com/search/rss.xml?format=Mozilla&q=123</guid:url>
<title>123</title>
<description>description for 123</description>
<link>http://www.vancraist.com/search/rss.xml?format=Mozilla&q=123</link>
<pubDate>Wed, 21 May 2023 00:00:00 +0000</pubDate>
<dc:creator>Vancraist</dc:creator>
<dc:category>Search for 123</dc:category>
</item>
</channel>
</rss>
```
