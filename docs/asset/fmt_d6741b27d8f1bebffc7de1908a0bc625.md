
Openlitespeed 有多个选项，在 Ubuntu 和 Raspbian 上都需要大量的尝试和错误直到它起作用。在线看起来，它似乎是一个经过精心整理的商业产品，拥有流畅的图形用户界面，并与 WordPress 和其他软件很好地集成，但它缺乏家庭 Web 服务器和测试所需的努力。

Lighttpd 是另一个缺乏来源网络文档的 Web 服务器。幸运的是，它设置和使用的很容易，所以我们避免了徒劳无功。最后，幸运的是，我们有 Google 来寻找额外的解决方案。事实上，我们花了大部分时间来获取配置并让一切完美运行所需的解决方案。

对于 Nginx、Tomcat、Apache 和 Lighttpd，似乎有足够好的论坛问答可以解决我们的问题。Openlitespeed，尽管它在网络上的托管使用排名相当高，但似乎拥有最糟糕的信息和答案。这几乎就像我们的问题没有答案，而且家庭用户对这台服务器的参与非常少。

### 结论

| 服务器 | 得分 | 服务器 | 得分 |
| :--- | :--- | :--- | :--- |
| APACHE | 10/10 | TOMCAT | 9/10 |
| NGINX | 10/10 | OPENLITESPEED | 5/10 |
| LIGHTTPD | 7/10 | | |

Nginx 和 Apache 占据主导地位，在线帮助远超竞争对手。

## 部署和管理

### 服务器是否易于设置和使用？

Web 服务器将通过命令行安装。一些安装非常简单，使用 `apt-get install` 的单行命令，而其他一些需要使用几个额外命令从源代码安装。安装后，服务器可用于快速显示默认网页。由于我们将使用服务器端语言 PHP 和 MySQL 测试我们的服务器，我们将看到它们与每个服务器结合使用的难易程度。深入细节，我们将看到哪些软件与基本命令结合使用最容易，或者只需对配置文件进行非常基本的文本编辑。除此之外，我们将研究配置每个服务器，使其运行更高效，并帮助我们获得所需的结果：一个加载快速、不会让潜在访客因等待页面加载而感到沮丧从而放弃网站的网站。为了达到这个目标，我们使用 Apache 基准测试工具来计算我们 Web 文件的每秒请求率。该工具可以发出数千次请求并模拟并发用户。

### Apache 10/10

在 `apache2` 安装期间，我们可以安装 `mysql-server`、`PHP`、`libapache2-mod-php` 和 `php-mysql`。之后，我们可以简单地编写直接可用的 PHP 脚本，或使用 WordPress、Laravel 或 Magento 等流行工具构建完整的 Web 应用程序。Apache 安装和测试性能方面的易用性使其成为在上传并迁移到某种托管平台（无论是共享托管、VPS 还是专用托管）到互联网之前，构建和测试 Web 应用程序的绝佳选择。由于许多 Web 托管服务商仍在使用 Apache，它提供了一种一致、坚固、统一的测试系统。然而，使用 Apache 时，调整它可能非常重要，因为如果我们不充分利用它，它可能会很慢。为了使测试基本化，我们有一些工具，如浏览器检查器和 Apache 基准测试工具，帮助达到我们的速度目标。

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_127_0.png)

### Nginx 9/10

在 Nginx 安装期间，我们还可以安装 `php-fpm`，以便能够构建和测试 PHP 应用程序。然而，这其中的内容远不止于此。为了能够在 Web 浏览器中打开 PHP 文件，我们还需要编辑文件 `/etc/nginx/sites-available/default` 并取消注释以 `location ~ \.php$ {` 开头的条目。在我们移除阻止 PHP 代码运行的注释后，我们可以重新加载 Nginx，PHP 运行良好。现在，我们可以运行和测试任何 PHP 应用程序，无论是自定义脚本、WordPress、Magento、Joomla、Drupal 还是如此长列表中的许多其他。现在，Nginx 表现非常出色，这是其近年来 popularity 增加的主要原因之一。并且由于 Nginx 设置和运行如此简单，它是第三方 Web 托管的一个绝佳选择。

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_127_1.png)

### 速度和性能

#### 基准测试每秒请求数

在我们的性能测试中，我们使用了浏览器和 Apache 基准测试工具。浏览器测试相当简单，我们在页面上右键单击，选择“网络”，刷新页面并单击显示我们 URL 的行。单击该行后，我们可以访问请求和响应头。这些头让我们能够看到一些性能方面的内容，如服务器本身（即 Nginx、Apache 或 Lighttpd）、Keep-alive、gzip 和缓存控制。就 Apache HTTP 基准测试工具而言，我们用它来测试获取图像 25,000 次，因为这是估算每台服务器每秒请求数的粗略想法的好方法。为了考验它们的能力，我们设置它们运行以获取 200Kb JPEG 文件的超过 25,000 次请求，并发请求（用户）为 50。

前两台服务器 – 都在八秒范围内 – 是 Nginx 和 Lighttpd（又称 Lighty）。紧随其后的是 Openlitespeed，出现在大约 14 秒处，Apache 在 19 秒，最后，Tomcat 以略超过 20 秒的成绩落在最后。

查看每秒请求数的细节，我们看到 Nginx 管理着大约 3,011 次，Lighttpd 紧随其后为 2,890 次。其余的稍微靠后地聚集在一起，Openlitespeed 为 1,776，Apache 为 1,314，Tomcat 为 1,229。尽管这些时间相当分散，肉眼无法分辨使用的是哪台服务器，因为所有平台上的图像和页面加载都足够快。因此，所有工具都适合在本地机器上测试 Web 应用程序。当使用完整的 URL 进行测试时，例如默认 WordPress 安装，各服务器在图像请求方面的速度差异结果非常相似。

#### 结论

| 服务器 | 得分 | 服务器 | 得分 |
| :--- | :--- | :--- | :--- |
| APACHE | 7/10 | TOMCAT | 7/10 |
| NGINX | 10/10 | OPENLITESPEED | 8/10 |
| LIGHTTPD | 10/10 | | |

`Nginx` 和 `Lighttpd` 开箱即用的速度就是快。

### Lighttpd 10/10

在安装 `lighttpd` 期间，我们可以安装 `fast-cgi` 和 `fastcgi.php`，以便构建和测试 PHP 应用程序。但事情远不止于此。Lighty 安装速度非常快，输入命令后几乎能即时响应。此外，简单的命令为我们完成了繁重的工作，PHP 和 MySQL 数据库都能按预期正常工作。然而，我们必须注意，如果在安装 `fast-cgi` 后没有启用并重载 Lighty，我们的浏览器将会收到 403 错误。

Lighty 安装完成后，它会从 `/var/www/html` 文件夹中查找其中一个默认文件（`index.html`、`index.lighttpd.html` 和 `index.php`）。快速设置 Lighty 且所有文件和文件夹都位于与 Nginx 和 Apache 相同的路径这一事实，使其也成为一颗瑰宝。能够在一个位置构建并在同一地点测试所有服务器，而不是让文件散落各处，这确实很美好。

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_128_0.png)

### Openlightspeed 8/10

在安装 Openlightspeed 期间，会创建一个 `index.html` 文件，用作默认网页。此外，PHP 开箱即用，因为它自带名为 `LiteSpeed SAPI PHP` 的处理器。与 Nginx、Apache 和 Lighttpd 不同，html 文件存储路径为 `/usr/local/lsws/Example/html/index.html`。

对于 Openlightspeed 而言，其优势在于测试根文件夹中的简单 HTML 和 PHP 文件。然而，一旦我们想要测试像 WordPress 或 Laravel 框架这样的实际应用，其默认配置就会显得力不从心。如果我们在子目录中工作，我们需要修改 `vhconf.conf` 文件并手动添加子文件夹。另一个问题是，那些能无缝配合 Nginx、Apache 和 Lighttpd 工作的 MySQL 安装，却无法直接配合 Openlightspeed 工作。我们之前用 `PhpMyAdmin` 构建的任何数据库都无法最初使用。

![](img/3f314b57ad3c8b08d25e5d1ab47de56d_128_1.png)

### Tomcat 9/10

`Tomcat` 安装后即刻可用。然而，与 Openlightspeed 类似，`Tomcat` 的文件默认位于不同于 Apache、Nginx 和 Lighttpd 的位置。实际上，它们位于 `/var/lib/tomcat7/webapps/ROOT` 目录中。此外，与其他在 80 端口运行的 Web 服务器不同，其默认端口是 8080。
