
kali@kali:-$ ./funcarg.sh

Today's random number is: 25207

> 列表 166 - 在 Bash 中向函数传递参数

在这种情况下，我们将一个随机数 `$RANDOM` 传递给函数，函数将其输出为 `$1`，即函数的第一个参数。注意，函数定义 `pass_arg()` 包含括号。在其他编程语言（如 C）中，这些括号将计算预期参数，但在 Bash 中，括号仅起装饰作用。还要注意，函数定义本身必须在调用之前出现在脚本中。

# 攻击安全

保存到：`'index.html'`

`index.html 100%[(2.56 MB) - 12.23K --KB/s in Os`

```
2018-03-18 17:56:54 (2.56 MB) - 'index.html' saved [12520/12520]
```

kali@kali:~ ls -l index.html

`-rw-r--r-- 1 kali 12520 Mar 18 17:56 index.html`

> 列表 170 - 从 megacorp.com 下载 index.html 页面

手动扫描文件，我们看到了很多不需要的行。让我们开始缩小到需要的行范围，并剔除不需要的行。首先，我们使用 `grep "href="` 来提取 `index.html` 中所有包含 HTML 链接的行：

```bash
kali@index:~ grep "href="
```

```html
<a href="http://beta.megacorp.com/util/files/news.html">MegaCorp CEO Joe Sher nominated for Nobel Prize in Physics, Medicine, and Literature prizes.</a><p><small>This is a fictitious company, brought to you by <a href="http://www.offensivesecurity.com" target="_blank">Offensive Security</a></a></a></small></p>
<a href="https://www.facebook.com/Megacorp-One-39357002439695" target="_blank"><i class="fa fa-facebook"></i></a>>
<a href="https://www.twitter.com/joe_sher"><i class="fa fa-twitter"></i></a>>
<a href="https://www.linkedin.com/company/1826898/" target="_blank"><i class="fa fa-linkedin"></i></a>>
<a href="https://github.com/megacorp" target="_blank"><i class="fa fa-github"></i></a>>
```

> 列表 171 - 识别 index.html 文件中的超链接

让我们使用 `grep` 提取包含 `"megacorp"` 的行（这表示存在子域），并使用 `grep -v` 剔除我们已经知道的 `"www.megacorp.com"` 域名：

```bash
kali@kali:~ grep "href=" index.html | grep -v "www.megacorp.com" | head
```

```html
+<a href="http://support.megacorp.com/requests/index.html">Nanoprocessors</a>
<a href="http://sys.megacorp.com/logs/view.php">MegaCorp</a>
```

> 列表 172 - 使用 grep 缩小搜索范围

此输出向我们展示了正在减少的内容。通过以逻辑方式减少数据，使得每次处理后数据都变小，我们正处于最常见的数据处理过程中。

看起来每行都包含一个链接和一个子域，但我们需要去掉链接周围的额外 HTML 代码。在 Bash 中执行任何任务总有多种方法，但我们将使用 `awk` 来设置一个多字符分隔符，而 `cut` 虽然简单但只能处理单字符分隔符。我们将分隔符设置为 `#`，并让 `awk` 找到第二个字段 `{print $2}`，或者该字段之后的所有内容：

```bash
kali@kali:~ grep "href=" index.html | grep ".megacorp" | grep -v "www.megacorp.com" | awk -F "http://" '{print $2}'
```

```html
<a href="admin.megacorp.com/index/index.html">Generation</a>
<a href="intranet.megacorp.com/pear">Immune Systems</a>
<a href="mail.megacorp.com/menu">Cybersation</a>
<a href="mail12.megacorp.com/relay">Weapons Systems</a>
<a href="siem.megacorp.com/home">Entity Assignment</a>
<a href="support.megacorp.com/ticket/requests/index.html">Nanoprocessors</a>
```

每行输出的开头显示我们正处于正确的道路上。现在我们可以使用 `cut` 将分隔符设置为 `/` (`-d`) 并打印第一个字段 (`-f1`)，从而只只剩下子域名：

```bash
kali@kali:~ grep "href=" index.html | grep ".megacorp" | grep -v "www.megacorp.com" | awk -F "http://" '{print $2}' | cut -d "/" -f1
```

```
admin.megacorp.com
intranet.megacorp.com
mail.megacorp.com
mail12.megacorp.com
siem.megacorp.com
support.megacorp.com
```

> 列表 174 - 截取域名

这看起来很棒！然而，一个 Bash 大师看一眼我们的工作就会嗤之以鼻。这是因为我们用一种笨拙的方式使用了基本工具，尽管我们的缩减逻辑是正确的。Bash 及其相关的命令构建非常强大，总有更多值得学习的。

如果我们为了改进而批评自己的工作（我们应该一直这样做），我们可能会发现一些改进方法。首先，我们从 `"href="` 开始并搜索 `http://`。这些本质上是链接，但这要求每行都必须有字符串。如果某行只有该内容但没有 `"href="`，我们就会漏掉一行。冗余是应该避免的，特别是在处理大文件时。此外，除非我们在寻找子域，否则我们不关心链接。另一个考虑因素是，我们花费了大量的时间通过筛选结果来查找并提取子域，这是很笨拙且容易出错的，而良好的正则表达式可以轻松处理这个问题。我们之前提到了正则表达式的力量，现在让我们来看看解决这个问题的硬核方法。

# 攻击安全

在这个例子中，我们将使用一个简单的正则表达式从文件中提取出 `"megacorp.com"` 子域：

```bash
kali@kali:~ grep -o '[^/]*\.megacorp\.com' index.html | sort -u
```

kali@kali:~ cat list.txt

```
admin.megacorp.com
beta.megacorp.com
intranet.megacorp.com
mail12.megacorp.com
siem.megacorp.com
support.megacorp.com
```
