

457 ?? I 0:00.01 /usr/local/sbin/httpd
458 ?? I 0:00.03 /usr/local/sbin/httpd
459 ?? I 0:00.02 /usr/local/sbin/httpd
460 ?? I 0:00.02 /usr/local/sbin/httpd
461 ?? I 0:00.02 /usr/local/sbin/httpd
462 ?? I 0:00.03 /usr/local/sbin/httpd
489 p1 R+ 0:00.01 grep httpd

如本例所示，Apache 会创建自身的多个实例。这种方式允许服务器响应连接，并迅速将其移交给其某个进程。每个 Apache 进程处理一个客户端连接。如果连接的客户端数量超过了 Apache 进程的数量，服务器会生成更多的自身副本以应对需求。

刚安装完 Apache 后，服务器并未运行。在您按照期望配置好服务器后，可以通过输入其名称来启动它：

```
# /usr/local/sbin/httpd
```

> **注意** 更改网站文件后不需要重启 Apache，但当更改其配置文件时必须重启。您可以通过输入 `killall -HUP httpd` 来执行此操作。

## Apache 配置文件

Apache 2 的配置文件是 `/usr/local/etc/apache2/httpd.conf`。Apache 将该文件中的设置称为*指令*（directives），其形式如下：

```
Directive value
```

某些指令定义了一组值的块。这些指令由尖括号（< >）包围，其定义的块以斜杠（/）加上指令名称结束。中间的行包含其他指令。例如，以下指令出现在默认配置文件中（尽管在实际文件中，所示的行之间夹杂着注释）：

```
<Directory "/usr/local/www/data">
Options Indexes FollowSymLinks
AllowOverride None
Order allow,deny
Allow from all
</Directory>
```

该指令，包括其*包含*的所有指令，指定了服务器如何处理特定目录。此主题将在下一节“设置服务器目录选项”中进一步描述。

井号（#）表示注释；以该字符开头的行将被忽略。默认的 FreeBSD `httpd.conf` 文件包含许多注释，您可以阅读这些注释以了解文件的结构及其选项的作用。某些配置选项是被注释掉的；您可以移除注释字符来激活这些选项。

## 设置基本功能

对于简单的 Web 服务器配置，您可以保留标准 `httpd.conf` 中大多数（甚至所有）指令不变。不过，在某些情况下，您可能希望微调一些设置。最可能需要调整选项包括：

- **备用服务器选项**：`StartServers`、`MinSpareServers` 和 `MaxSpareServers` 指令控制保持运行的 Apache 进程数量。`StartServers` 告知 Apache 启动多少个自身实例。`MinSpareServers` 和 `MaxSpareServers` 决定保持运行的“备用”实例（即那些未积极处理请求的实例）数量。如果连接请求堆积，Apache 会启动额外的自身实例，以便快速处理传入请求——始终保持至少 `MinSpareServers` 个副本在运行且没有连接。随着负载降低，备用实例会被终止，以将数量保持在 `MaxSpareServers` 之下。默认的 5、5 和 10 的值对于小型站点是合理的，但繁忙站点可能需要增加这些值。`MaxSpareServers` 应始终大于 `MinSpareServers`。这些指令都包含在 `IfModule` 指令内。FreeBSD 使用 `<IfModule prefix.c>` 指令集；默认配置文件中其他指令是为在其他平台上运行的 Apache 设计的。

- **MaxClients**：此指令设置 Apache 在任一时刻服务的最大客户端数量。默认值 150 对于小型甚至某些中型站点是合理的，但对于大型站点，您可能需要增加此值。此类站点还需要更好的硬件（大量 RAM、快速 CPU 等）；`MaxClients` 部分用于防止因传入服务器的请求过多而导致系统不可用。

- **Listen**：此指令默认值为 80，指定 Apache 绑定的端口（80 是 HTTP 的传统端口）。有时在非标准端口上运行 Web 服务器是可取的，例如您希望在一个系统上运行两个完全不同的 Web 服务器。您还可以在 `Listen` 指令中添加 IP 地址，使 Apache 仅绑定到指定接口的特定端口，这在计算机有多个接口时可能很有用。例如，`Listen 172.17.2.217:80` 将 Apache 绑定到与 172.17.2.217 地址相关的网络硬件的 80 端口。

- **User 和 Group**：这些选项告知 Apache 用于运行各种 Apache 子进程的账户。每个选项的默认值 *www* 适用于大多数安装，但如果您想修改系统的安全配置，可能会为此目的创建一个新账户。

> **警告** 不要以 *root* 甚至普通具有正常登录权限的用户身份运行 Apache。这样做会大大增加运行 Web 服务器的风险。

- **ServerAdmin**：此指令设置负责维护 Web 服务器的个人的电子邮件地址。此选项在正常运行时不重要，但在某些类型的错误发生时会将其值返回给客户端，因此您应该将其设置为适合您系统的合理值。

- **ServerName**：此指令设置服务器的名称和端口，例如 `www.threeroomco.com:80`。Apache 通常会自动正确设置它，但手动指定它可以防止在 Apache 启动时出现临时 DNS 错误时引发的问题。

- **TypesConfig**：通过 HTTP 传输的文件包含多重用途互联网邮件扩展（MIME）类型，这是一种识别文件类型（纯文本、特定的图形格式等）的代码。**TypesConfig** 指令指定了一个文件，其中包含文件扩展名和 MIME 类型之间的映射。默认设置效果良好，但如果您向 Web 页面添加了非常规类型的文件，可能需要编辑此文件。

- **DefaultType**：如果 Apache 无法确定文件类型，它将使用此指令指定的类型，默认值为 `text/plain`。此类型会导致浏览器将文件解释为纯文本。

- **HostnameLookups**：此指令可以设置为 *On* 或 *Off*，它控制 Apache 是记录客户端的主机名还是仅记录其 IP 地址。如果您有兴趣了解谁在访问您的服务器，记录主机名可能很方便，但这会增加服务器使用的带宽，因为它必须为每个连接执行 DNS 查找。

此列表仅是 `httpd.conf` 文件中可用指令的抽样。在此列出的指令中，**ServerAdmin** 是您肯定应该更改的唯一一个。修改其他指令可能会提高性能、增强安全性，或使服务器更好地与客户端交互或提供 Web 页面。

除了上述选项，Apache 还提供若干与 Web 页面传输相关的指令。其中大多数围绕定义用于存储 Web 页面的目录，并在下一节中进行了描述。

## 设置服务器目录选项

当您作为用户将统一资源定位符（URL）输入 Web 浏览器时，该 URL 看起来类似于以下内容：

```
http://www.threeroomco.com/products/fb50.html
```

> **注意** 组件可能比这里显示的多或少，但此示例代表了简单 Web 页面 URL 的典型形式。

URL 包含有关使用协议（http）、要联系的计算机（www.threeroomco.com）以及要从该计算机检索的文件（products/fb50.html）的信息。最后一个组件指定为目录和文件名，但您可能不希望给予随机客户端访问计算机上所有文件的权限。因此，通常定义一个或多个用于存放 Web 页面的目录，并定义相对于该目录的 URL。在上面的示例中，products 目录是 Web 服务器文档根目录的子目录，而不是计算机的根目录。您可以使用服务器目录选项设置此选项以及其他几个影响 Apache 如何处理各种类型文档访问请求的选项。这些包括：

- **DocumentRoot**：此指令设置文档根目录，大多数文档都从中读取。默认值为“/usr/local/www/data/”（引号是必需的）。如果您愿意，可以更改此值，例如，如果您在另一个分区上有更多磁盘空间。

- **UserDir**：如果您的 Web 服务器托管由普通用户拥有的文件（即他们的个人 Web 页面），Apache 可以在服务器的主要文档根目录之外的其他地方查找这些文件。您可以使用 UserDir 指令指定查找用户文件的位置，该指令设置用户主目录内用于此类文件的子目录名称。例如，如果 www.threeroomco.com 的 httpd.conf 文件包含 `UserDir public_html`（默认文件也是如此），并且客户端请求 `http://www.threeroomco.com/~amy/mypage.html`，则 Apache 返回 amy 主目录中的 `public_html/mypage.html` 文件（可能是 `/home/amy/public_html/mypage.html`）。URL 中的波浪号（~）是标准指示符，表示该页面是用户的主页，而不是组织的主页。

- **Directory**：此指令开始一个指令块，因此出现在尖括号中。后面跟着目录名称（相对于计算机的根目录），其内容出现在其中。因此，该行可能是 `<Directory />` 或 `<Directory /usr/local/www/data/>`。实际上，这两个值都出现在默认配置文件中，第一个用于限制对用户目录的访问（原则上可以在任何位置），第二个用于定义对主要服务器目录的访问。如果您更改 DocumentRoot 指令，请务必将第二个路径更改为与之匹配。目录指令块以读取为 `</Directory>` 的行结束。

