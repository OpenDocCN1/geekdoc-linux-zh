
![](img/cbcdf34138bb96edef7aa6057d0d0d0e_268_0.png)

*图 7-6. 从公共站点提取个人数据的日历*

烹饪信息小程序非常简单，因为它就是一个烹饪术语和基本换算单位的词典，每个条目都从 `warp/conf/cookery` 中的单独文件加载。如果你打算构建一个基于静态文本文件的小程序，这是一个很好的起点。

联系人小程序提供你所有亲友的完整详细信息，并按用户分别提供。每当有用户登录时，系统都会从 `$MINBASE/etc/users/[username]/contacts.xml` 文件中读取其联系信息，解析后显示在此小程序中。如果用户未登录，那么你将看到属于公共用户的联系信息。

最后，相框小程序是 Minerva 中 Web 通道所独有的。它从 `warp/conf/photoframe/photoframe.conf` 读取照片列表（图像本身保存在名为 `photos` 的子目录中），并一次显示一张，如图 7-7 所示。

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_269_0.png)

*图 7-7. 相框可以在自助终端机上以幻灯片方式运行*

点击主图像后，此应用可以在完整浏览器窗口中工作，因此在机器不充当控制面板时，它适合作为交互式相框使用。你可以使用图像左右两侧的热点循环浏览图像，而底部区域可让你返回非全屏模式。互联网上有大量可用的图片可以放入相框，包括为文化爱好者准备的 `http://www.most-famous-paintings.org` 上的图片。

## 信息

这些小程序提供关于现实世界的信息，这些信息在户外也同样有用和有效。它们与你的生活方式可能存在潜在重叠，但就目前而言，这个区分已经足够好了！

Moonbeam 是一个依赖 MySQL 存储书签列表的小程序，每个书签带有多个标签。它类似于 `http://del.icio.us`，只不过所有数据都保存在你自己的服务器上。要准备数据库，你可以使用现有的 root 帐户运行 `build/applets/moonbeam/createdb.sql` 脚本：

```bash
$ mysql -u your_username -h your_machine_name -p < createdb.sql
```

然后输入你的密码以构建空数据库。你可以将相同的凭据添加到同一目录的 `config.php` 文件中，并运行以下命令，用示例链接填充数据库：

```bash
php init.php
```

然后，你可以将此帐户信息添加到 `conf/moonbeam/config.php` 处的 Moonbeam Web 配置中，并正常使用该小程序。如果你想创建另一个用户来访问 Moonbeam 数据库（推荐这样做），请登录 MySQL 并输入以下内容：

```sql
CREATE USER 'moonbeam'@'localhost' IDENTIFIED BY 'some_pass';
GRANT SELECT on moonbeam.* TO 'moonbeam'@'localhost';
```

并按照前面所示修改 Web 配置。出于安全考虑，moonbeam 用户因而被授予对数据库的只读权限，而真实用户（例如 steev）则能够照常通过数据库添加、更改和删除书签。

天气小程序只读取预缓存的天气预报（当天早些时候由 Minerva 用户的 crontab 生成），这些预报存储在 `/var/log/minerva/cache/weather.txt` 和 `/var/log/minerva/cache/weather_info.txt` 中，并查找匹配字符串，以确定在页面上绘制哪个图标。

还有一个基于 `http://xurrency.com` Web 服务的货币计算器，你在第 6 章中见过该服务。包含它主要是为了教学目的。

另一个小程序只是封装了现有的 Bearskin 命令，由实时发车信息板组成。它调用 `$MINBASE/bin/ldbquery`，从你预设的车站确定下一班列车。这里没有任何配置，因为 `ldbquery` 脚本接受由小程序中硬编码值指定为你旅程出发站和到达站的参数。

最后，RSS 新闻小程序使用 `news-read` 命令将最新新闻故事呈现到你的浏览器中。每个新闻源由站点 ID 和用户名的唯一配对管理，该配对会呈现存储在 `$MINBASE/etc/users/public/news/slashdot` 中的文件（例如），其中保存着 RSS 源的站点名称和 URL：

```text
Slashdot
http://rss.slashdot.org/Slashdot/slashdot
```

这些新闻会按需下载，可以显式地使用 `news-get public slashdot`，也可以在阅读故事时通过 `news-read slashdot public text 0 headline` 隐式下载。此时，RSS 内容会被下载并存储在本地缓存中，各种元素都可以从中读取。这个系统非常智能，如果内容足够新，就不会重新下载，并且可以将输出呈现为文本、HTML 或适合语音的文本。后一种情况会移除所有标记。WARP 小程序使用前面显示的 `news-read` 参数分别显示元素、标题、URL 和故事。同样的方法也可以在命令行中使用，这样闹钟就可以包含下面这样一行，在早上为你提供头条新闻：

```bash
$MINBASE/bin/say default (`news-read slashdot public vox 0 headline`)
```

## 管理

这些都是非常简单的小程序，用于快速查看状态日志、进程和服务器，而无需通过 SSH 登录。你需要有权使用这些工具，因此请通过以下命令给自己授权：

```bash
minuser auth [myusername] system set rw
```

这里可用的典型小程序会报告以下内容：

- 可用磁盘空间（具体设备可在 `warp/conf/diskfree/diskfree.conf` 中指定）
- 浏览器的用户代理（主要用于调试）
- Samba 状态
- 处理器使用率排名（top）
- UPS 状态
- 各种日志文件
- 蓝牙扫描结果

[^5]: 模拟电视传输在英国和其他国家几乎已经绝迹，因此这一功能很快也会随之消亡。

[^6]: 例如 `http://toki-woki.net/p/scroll-clock` 或来自 `http://sgxengine.com/examples/clockface/html5/default.htm` 的 HTML5 时钟。

## 创建你自己的小程序

要充分理解小程序的开发方法，有必要对 WARP 稍有了解。WARP 是构建在 WebFace 之上的系统，它抽象了网页设计的基本元素，以确保控制逻辑和表现元素严格分离。这意味着你不能在页面中用下面的方式添加链接：

```
<a href="process.php?bedroom_light=on">Switch Light On</a>
```

相反，你必须请求小程序管理器为你生成一个链接：

```
$html = $appMan->getAppletLink($applet, "on", "bedroom_light", "Switch Light On");
```

然后你可以像这样取出该参数：

```
$prm = $appMan->queryParameter($applet, "bedroom_light");
```

这种方法有几个好处。自然，它强制逻辑与显示分离，这鼓励编写更有结构的代码；同时，由于链接中不需要提及页面本身，你可以把小程序放到任何你喜欢的页面上。但更重要的是，它提供了一条简单的升级路径。WARP 基于某种类似 RESTful 的方法。因为 HTTP 是一种无状态协议，所以没有办法在页面之间记住用户操作。有些网站通过使用大量不同的页面来实现这一点，页面本身隐式地提示着状态。有些则会创建服务器端对象来记住状态，这些对象在你的浏览器停留在该页面期间一直存在，或直到某个任意超时。WARP 的做法是将状态记录为 URL 的一部分；由于每个页面会出现多个小程序，每个小程序必须在 URL 中有自己的部分来表示自己的状态。一个典型的 URL 可能如下所示：

```
http://my.minervahome.net/minerva/wm.php?WRP001X1_user=0&WRP001X1_day=0&WRP002X3_dpage=0&WRP002X3_fpage=0&WRP004X6_current=0&WRP004X6_dpage=0&WRP004X6_fpage=0&wintype=main&content=WRP002X&max=WRP002X4
```

如果你仔细剖析这个 URL，就会发现每个参数都符合这样的模式：`WRP`，后跟三位小程序代码、一个 `X` 分隔符、参数索引号、一个下划线，再后跟一个名称/值对。还有一些参数以 `wintype`、`content` 和 `max` 的形式描述 WARP 的内部状态。自然，尝试手动生成或解析这种 URL 是鲁莽之举！

### WARP 目录
