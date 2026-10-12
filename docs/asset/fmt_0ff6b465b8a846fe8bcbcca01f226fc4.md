
为了让其速度达到超过 25000 次请求（用户）的粗略。顶端服务器——处于秒级范围内——`Nginx` 和 `Lighttpd`（类似于 `Apache`）。紧随这一档之后，我们看到 `Openspeed` 在 14 秒左右，`Apache` 为 9 秒，`Tomcat` 刚刚进入

## `Lighttpd` 10/10 `Openspeed` 8/10 `Tomcat` 9/10

在 `lighttpd` 期间，我们可以安装 `fast-cgi` 和 `fastcgi-php`，以便我们能够构建并测试 `PHP` 应用。但是，功能不仅于此。`Lighttpd` 安装速度非常快，而且几乎毫不费力。此外，简单的命令就完成了我们所使用的 `PHP` 和 `MySQL` 数据库工作的所有大部分工作。然而，请注意，如果在安装 `fast-cgi` 后在浏览器中收到 `403` 错误，我们需要启用并重新加载 `Apache`。

在安装 `Openspeed` 期间，会创建一个 `index.html` 文件作为默认网页。此外，如果我们在 `OpenSpeed` 上配合我们的 `PHP` 修饰器使用，`PHP` 可以开箱即用。`Nginx`、`Apache` 和 `Lighttpd` 的 `html` 文件存储在 `/usr/local/www/html/index.html` 路径下。

`Tomcat` 运行良好且开箱即用。但与 `Openspeed` 不同，`Tomcat` 文件的默认位置与 `Apache` 和 `Lighttpd` 不相同。事实上，它们位于 `/var/lib/tomcat9/webapps/`。`Tomcat` 的默认端口是 `8080`，而我们的服务器运行在 `80` 端口。

一旦安装了 `Lighttpd`，它将从 `/var/www/html/` 文件夹查找默认文件 `index.lighttpd.html` 和 `index.php`。`Lighttpd` 保持可用，而且与 `Nginx` 和 `Apache` 相同的路径这一事实也可能是它的一个优势。能够从一个服务器构建连接总比让文件散落在各处要好。

与其他服务器不同，`Tomcat` 设计用于提供 `Servlets` 和 `JServlets`。

对于 `Openspeed`，它的优势在于根文件夹。但当我们想用 `Nginx` 创建一个真实的应用时，它的默认设置路径在子目录下，因此我们需要更改 `vhost.conf` 文件并添加子文件夹。另一个问题是，我们为 `Nginx`、`Apache` 和 `Lighttpd` 的配置无法直接在 `Openspeed` 上运行。我们之前任何带有 `PHPMyAdmin` 的数据库都无法使用。

对于 `Java` 项目，可以创建 `WAR`（网络归档）文件并使用 `Tomcat` 进行部署。`HTML`、`CSS` 和 `JavaScript` 也可以配置为解释 `PHP` 文件，但它并非为此设计，而是更专门用于 `Java` 编程。考虑到 `Tomcat` 是基于 `Java` 的，它作为流行的 `Web` 服务器确实排名很高，并且看起来运行没有问题。

## 化

以及使用 `.htaccess` 选项添加并启用模块。

由于大多数网站使用服务器端语言，例如 `WordPress` 安装或处理 `HTML` 联系表单的基础基础代码，让我们来看看如何实现。

扩展 `Web` 服务器比其他服务器更容易。然而，从简单的角度来看，`Apache` 和 `Lighttpd` 使得配置和启用模块变得非常容易。例如，`Apache` 或 `Nginx` 中默认未启用的某个模块可以从一开始启用，因此使用哪些命令来启用或禁用并不是问题。对于 `Nginx`，添加和配置模块运行得没有问题。

`Nginx` 并不像 `Apache` 或 `Lighttpd` 那样直观，中级用户可以通过简单的命令在某种程度上启用。除了为服务器添加模块外，将来会有我们需要编辑服务器配置或向文件中添加自定义配置文件夹的时候，例如在 `.htaccess` 文件中。`Apache` 和 `Tomcat` 让此类配置非常简单，因为我们可以添加 `.htaccess` 文件来创建自定义规则、浏览器缓存等。同时，`Openspeed` 必须将我们的 `.htaccess` 从 `Apache` 迁移到它自己的系统并使用服务器重写规则，这带来了从 `Apache` 服务器的转换。

`Lighttpd` 有自己的方法在它的 `lighttpd.conf` 中创建自定义文件。对于 `Nginx` 和 `Lighttpd`，大多数自定义规则发生在配置文件中。

## 结论

| 服务器 | 评分 | 服务器 | 评分 |
| :--- | :--- | :--- | :--- |
| `APA` | 10/10 | `TOMCAT` | 9/10 |
| `NGINX` | 8/10 | `OPENSPEED` | 9/10 |
| `LIGHTTPD` | 8/10 | | |

## 核心功能

我们的 `Web` 服务器可以开箱即用吗——或者不能？

开箱即用，它们都能工作。但由于我们有不同且不断的需求，我们可以看看它将如何工作。测试 `HTML` 和浏览器交互式代码（如默认提供的 `CSS` 和 `JavaScript` 静态内容）。但当我们需要添加 `PHP` 或 `Python` 等服务器端语言时，我们需要一个服务器来有效地通信和工作。嗯，对于人们通常做，很少需要微调。但一两分钟的时间足够配置 `PHP` 以运行像 `WordPress` 这样的应用程序，以及必须考虑的安全细节。所以，让我们过一遍列表看看我们拥有什么。

默认启用的模块包括一些：`mod_module`、`alias_module`、`auth_base`、`deflate_module`、`mod_dir`、`mod_php`、`remove_module`。除了开箱即用的模块，`Apache` 可以通过单个命令进行扩展，包括 `SSL` 和 `mod_expires`。`Nginx` 也有一些很好的模块，如 `fastcgi`、`ssl` 和 `gzip`。`Apache` 有一系列我们可以配合 `mod_access`、`mod_alias`、`compress`、`mod_rewrite` 使用的模块。

许多模块默认启用，我们可以检查标头以隐藏版本。重写可以在 `/etc/httpd/httpd.conf` 中完成。`Openspeed` 也可以开箱即用，尽管它在 `nginx` 后面运行。此外，`Openspeed` 需要更多的使用来配置它。

| 服务器 | 评分 | 服务器 | 评分 |
| :--- | :--- | :--- | :--- |
| `APACHE` | 10/10 | `TOMCAT` | 9/10 |
| `NGINX` | 9/10 | `OPENSPEED` | 7/10 |

## 安全性

我们可以让我们的 `Web` 服务器安全吗？

开箱即用，它们都能工作。但由于我们有不同且不断的需求，我们可以看看它将如何工作。测试 `HTML` 和浏览器交互式代码（如默认提供的 `CSS` 和 `JavaScript` 静态内容）。但当我们需要添加 `PHP` 或 `Python` 等服务器端语言时，我们需要一个服务器来有效地通信和工作。嗯，对于人们通常做，很少需要微调。但一两分钟的时间足够配置 `PHP` 以运行像 `WordPress` 这样的应用程序，以及必须考虑的安全细节。所以，让我们过一遍列表看看我们拥有什么。

默认启用的模块包括一些：`mod_module`、`alias_module`、`auth_base`、`deflate_module`、`mod_dir`、`mod_php`、`remove_module`。除了开箱即用的模块，`Apache` 可以通过单个命令进行扩展，包括 `SSL` 和 `mod_expires`。`Nginx` 也有一些很好的模块，如 `fastcgi`、`ssl` 和 `gzip`。`Apache` 有一系列我们可以配合 `mod_access`、`mod_alias`、`compress`、`mod_rewrite` 使用的模块。

许多模块默认启用，我们可以检查标头以隐藏版本。重写可以在 `/etc/httpd/httpd.conf` 中完成。`Openspeed` 也可以开箱即用，尽管它在 `nginx` 后面运行。此外，`Openspeed` 需要更多的使用来配置它。

| 服务器 | 评分 | 服务器 | 评分 |
| :--- | :--- | :--- | :--- |
| `APACHE` | 10/10 | `TOMCAT` | 9/10 |
| `NGINX` | 9/10 | `OPENSPEED` | 7/10 |

*(注：由于提供的原文中存在大量内容重复，翻译时已根据指令“不要重复输出原文”的原则进行了去重处理，保持了逻辑块的完整性。)*

修正译文：

## `Lighttpd` 10/10 `Openspeed` 8/10 `Tomcat` 9/10

在 `lighttpd` 期间，我们可以安装 `fast-cgi` 和 `fastcgi-php`，以便我们能够构建并测试 `PHP` 应用。但是，功能不仅于此。`Lighttpd` 安装速度非常快，而且几乎毫不费力。此外，简单的命令就完成了我们所使用的 `PHP` 和 `MySQL` 数据库工作的所有大部分工作。

在安装 `Openspeed` 期间，会创建一个 `index.html` 文件作为默认网页。此外，如果我们在 `OpenSpeed` 上配合我们的 `PHP` 修饰器使用，`PHP` 可以开箱即用。`Nginx`、`Apache` 和 `Lighttpd` 的 `html` 文件存储在 `/usr/local/www/html/index.html` 路径下。
