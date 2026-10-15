
## TABLE 22-6 Access Control Directives (continued)

| Directive | Description |
| --- | --- |
| `<LimitExcept method method ... > ... </LimitExcept>` | `<LimitExcept>` 和 `</LimitExcept>` 指定一组访问控制指令，然后适用于未列在参数中的任何 HTTP 访问方法。 |
| `<Location URL> ... </Location>` | `<Location>` 指令提供按 URL 进行访问控制。与 `<Directory>` 指令类似。 |
| `<LocationMatch regex> ... </LocationMatch>` | 提供按 URL 进行访问控制，与 `<Location>` 相同，但使用正则表达式作为参数。 |
| `order ordering` | 控制 `allow` 和 `deny` 指令的评估顺序。 |
| `Satisfy directive` | 同时使用 `allow` 和 `require` 时的访问策略。参数可以是 `all` 或 `any`。 |
| `LimitRequestBody number` | 限制 HTTP 请求消息体的大小。 |

你可以通过将它们限制为某些 HTML 访问方法来进一步限定访问控制指令。HTML 访问方法是指浏览器与你的 Web 站点交互的方式。例如，浏览器可以从页面获取信息（`GET`）或通过它发送信息（`POST`）。你可以使用 `<Limit>` 指令控制此类访问方法。`Limit` 以要控制的访问方法列表作为参数。指令然后与 `</Limit>` 指令配对，以定义一个 `Limit` 块，在其中可以放置访问控制指令。这些指令仅适用于指定的访问方法。你可以将此类 `Limit` 块与 `Directory` 块一起放置，以为特定目录设置访问方法控制。以下 `/etc/config/httpd.conf` 文件中的 `Directory` 块控制你的 Web 站点主目录 `/var/www/html` 的访问方法。

```
# This should be changed to whatever you set DocumentRoot to.
<Directory /var/www/html>
    Options Indexes FollowSymlinks
    AllowOverride All
    <Limit GET>
        order allow,deny
        allow from all
    </Limit>
</Directory>
```

控制从上层目录继承到下层目录。如果你想严格按每个目录为你的整个 Web 站点控制访问，你可以使用以下条目。以下条目可用于拒绝所有用户的访问。然后，在各个目录中，你可以允许特定用户、组或主机访问。

```
<Directory /var/www/html>
Order Deny,Allow
Deny from All
</Directory>
```

## URL 路径名

某些指令可以修改或补全用于访问你的网站的 URL 的路径名段。URL 的路径名段指定了网站上的特定目录或网页。指令使你能够别名化或重定向路径名，以及选择默认网页。使用 `Alias` 指令，你可以让用户访问位于系统其他部分、其他文件系统或其它网站上的资源。别名可以使用互联网上站点的 URL，而不是系统上目录的路径名。使用 `Redirect` 指令，你可以将用户重定向到另一个站点。

```
Alias /mytrain /home/dylan/trainproj
Redirect /mycars http://www.myautos.com/mycars
```

如果 Apache 只被给出一个目录来访问，而不是特定的网页，它会查找该目录中的索引网页并显示它。默认网页的可能名称由 `DirectoryIndex` 指令列出。通常使用的名称是 `index.html`，但你可以添加其他名称。标准名称如下所示。当 Apache 只被给出一个网页目录来访问时，它会查找并显示其中的 `index.html` 网页。

```
DirectoryIndex index.html index.shtml index.cgi
```

Apache 还允许用户在用户主目录中的一个特殊子目录中维护网页，而不是在主网站目录中。使用 `~` 后跟用户名可以访问此目录。此目录的名称由 `UserDir` 指令指定。默认名称是 `public_html`，如下所示。站点 `turtle.mytrek.com/~dylan` 访问主机 `turtle.mytrek.com` 上的目录 `turtle.mytrek.com/home/dylan/public_html`。

```
UserDir public_html
```

## MIME 类型

当浏览器访问网站上的网页时，它通常会访问许多不同类型的对象，包括 HTML 文件、图片或声音文件以及脚本文件。为了正确显示这些对象，浏览器必须知道它们是什么类型的对象。JPEG 图片文件与简单文本文件的处理方式不同。服务器以 MIME 类型的形式提供此类型信息（参见第 13 章）。MIME 类型与通过 Internet 邮件程序（如 Pine）发送附件文件时使用的类型相同。每种类型的对象都与给定的 MIME 类型相关联。提供 MIME 类型后，浏览器可以正确处理和显示该对象。

MIME 协议将特定类型与具有给定扩展名的文件关联。例如，具有 `.jpg` 扩展名的文件将具有 MIME 类型 `image/jpeg`。`TypesConfig` 指令保存 `mime.types` 文件的位置，该文件列出了所有 MIME 类型及其关联的文件扩展名。`DefaultType` 是任何无法确定类型的文件的默认 MIME 类型。`AddType` 使你能够在不编辑 MIME 文件的情况下修改 `mime.type` 类型列表。

```
TypesConfig /etc/mime.types
DefaultType text/plain
```

其他类型指令用于指定对某些文档采取的操作。`AddEncoding` 允许浏览器即时解压缩压缩文件。`AddHandler` 将文件扩展名映射到操作，而 `AddLanguage` 使你能够指定文档的语言。以下示例将带有 `.gz` 扩展名的文件名标记为 gzip 编码文件，并将带有 `.fr` 扩展名的文件标记为法语文件：

```
AddEncoding x-gzip gz
AddLanguage fr .fr
```

Web 服务器可以显示和执行许多不同类型的文件和程序。然而，并非所有 Web 浏览器都能显示所有这些文件。旧浏览器限制最大。某些浏览器，如 Lynx，甚至不设计用于显示简单图形。为了允许 Web 浏览器显示页面，服务器会与其协商以确定它可以处理的文件类型。为了启用此类协商，你需要启用 `Multiviews` 选项。

```
Option multiviews
```

## CGI 文件

通用网关接口（CGI）文件是可以由访问你的网站的 Web 浏览器执行的程序。CGI 文件通常由执行程序作为其显示内容一部分的网页启动。传统上，CGI 程序被放置在名为 `cgi-bin` 的目录中，并且只有在位于此类特殊目录中时才能执行。通常，每个网站只有一个 `cgi-bin` 目录。发行版通常会在默认 Web 服务器目录中设置一个 `cgi-bin` 目录（Red Hat 上为 `/var/www/cgi-bin`）。在这里，你放置可在你的网站上执行的任何 CGI 程序。`ScriptAlias` 指令为你的 `cgi-bin` 目录指定一个别名。任何网页或浏览器都可以使用该别名引用此目录。

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
```

如果你想执行位于网站任何位置的 CGI 程序，你可以指定具有 `.cgi` 扩展名的文件被视为可执行的 CGI 程序。你可以使用 `AddHandler` 指令来做到这一点（参见表 22-7）。该指令将某些处理器应用于给定类型的文件。执行此操作的处理器指令包含在随 Apache 源代码文件提供的默认 `httpd.conf` 文件中，尽管被注释掉了。你可以删除注释符号（`#`）以启用它。

```
AddHandler cgi-script cgi
```

| Directive | Description |
| --- | --- |
| `Action action-type cgi-script` | 添加一个操作，当请求触发 `action-type` 时激活 `cgi-script`。 |
| `AddHandler handler-name extension extension ...` | 将文件扩展名 `extension` 映射到处理器 `handler-name`。 |
| `RemoveHandler extension extension ...` | 移除给定扩展名文件的管理器关联。这允许子目录中的 `.htaccess` 文件撤销从父目录或服务器配置文件继承的任何关联。 |
| `Script method cgi-script` | 添加一个操作，当使用 `method` 方法（可以是 `GET`、`POST`、`PUT` 或 `DELETE` 之一）请求文件时激活 `cgi-script`。 |
