

> 注意：您也可以将 Apache 配置为仅作为代理和/或缓存服务器运行。`httpd.conf` 文件中已经包含了默认的代理和缓存服务器指令。`ProxyRequests` 指令用于开启代理功能。可以使用 `CacheRoot` 指令指定缓存目录，使用 `CacheSize` 指令设置缓存大小（默认值为 500KB），并使用 `CacheMaxExpire` 指令设置未修改文档的时间限制来配置缓存。

## 目录级配置：.htaccess 和 <Directory>

Apache 最灵活的方面之一是配置单个目录的能力。使用 **Directory** 指令，您可以定义一组仅适用于特定目录的指令。此类指令可以放置在 **httpd.conf** 或 **access.conf** 配置文件中。您还可以使用特定目录内的 **.htaccess** 文件来存放配置指令。这些指令随后仅应用于该目录。“.htaccess” 这个名称实际上是通过 **AccessFileName** 指令设置的。如果您愿意，可以更改此名称。

```apache
AccessFileName .htaccess
```

Directory 块以 **<Directory** _路径名_**>** 指令开始，其中 _路径名_ 是要配置的目录。结束指令使用相同的 **< >** 符号，但在单词 “Directory” 之前加了一个斜杠：**</Directory>**。放置在此块内的指令仅应用于指定的目录。以下示例仅拒绝来自 **www.myvids.com** 的请求访问 **mypics** 目录。

```apache
<Directory /var/www/html/mypics>
   Order Deny,Allow
   Deny from www.myvids.com
</Directory>
```

使用 **Options** 指令，您可以启用目录中的某些功能，例如使用符号链接、自动索引、执行 CGI 脚本以及内容协商。默认值为 **All** 选项，该选项开启了除内容协商（**Multiviews**）之外的所有功能。以下示例启用了自动索引（**Indexes**）、符号链接（**FollowSymLinks**）和内容协商（**Multiviews**）。

```apache
Options Indexes FollowSymLinks Multiviews
```

在主要配置文件中或通过上级目录指令所做的配置会被下级目录继承。保存在 **.htaccess** 文件和 Directory 块中的特定目录指令可以允许覆盖这些配置。这种能力可以通过 **AllowOverride** 指令进行控制。使用 **all** 参数，**.htaccess** 文件可以覆盖任何先前的配置。**none** 参数禁止覆盖，实际上禁用了 **.htaccess** 文件。您可以进一步控制特定指令组的覆盖权限。**AuthConfig** 允许使用授权指令，**FileInfo** 用于类型指令，**Indexes** 用于索引指令，**Limit** 用于访问控制指令，而 **Options** 用于选项指令。

```apache
AllowOverride all
```

## 访问控制

通过访问控制指令，如 **allow** 和 **deny**，您可以控制远程用户和主机对您网站的访问。后跟主机名列表的 **allow** 指令将访问限制为仅这些主机。带主机名列表的 **deny** 指令拒绝这些系统的访问。参数 **all** 将该指令应用于所有主机。**order** 指令指定访问控制指令的应用顺序。其他访问控制指令，如 **require**，可以建立认证控制，要求用户登录。访问控制指令可以全局使用以控制对整个站点的访问，也可以放置在 **Directory** 指令中以控制对单个指令的访问。在以下示例中，允许所有用户访问：

```apache
order allow,deny
allow from all
```

## URL 路径名

某些指令可以修改或补全用于访问您站点的 URL 路径名段。URL 的路径名段指定了您站点上的特定目录或网页。指令允许您别名或重定向路径名，以及选择默认网页。使用 **Alias** 指令，您可以让用户访问位于系统其他部分、其他文件系统或其他网站上的资源。别名可以使用 Internet 上站点的 URL，而不是系统中目录的路径名。使用 **Redirect** 指令，您可以将用户重定向到另一个站点。

```apache
Alias /mytrain /home/dylan/trainproj
Redirect /mycars http://www.myautos.com/mycars
```

如果 Apache 仅被给予一个目录进行访问，而不是特定的网页，它会查找该目录中的索引网页并显示它。默认网页的可能名称由 **DirectoryIndex** 指令列出。通常使用的名称是 **index.html**，但您可以添加其他名称。这里显示了标准名称。当 Apache 仅被给予一个 Web 目录进行访问时，它会查找并显示其中位于的 **index.html** 网页。

```apache
DirectoryIndex index.html index.shtml index.cgi
```

Apache 还允许用户维护位于主用户目录中特定子目录里的网页，而不是主要网站目录。使用 ~ 后跟用户名可访问此目录。此目录的名称通过 **UserDir** 指令指定。默认名称为 **public_html**，如下所示。站点 **turtle.mytrek.com/~dylan** 访问主机 **turtle.mytrek.com** 上的目录 **turtle.mytrek.com/home/dylan/public_html**。

```apache
UserDir public_html
```

如果您想让人们使用完整的路径名，则使用路径名引用。例如，对于用户 **dylan**，**/usr/www** 将转换为 URL 引用 **/usr/www/dylan**，HTML 文件将位于此处；**/home/*/www** 将转换为 **/home/dylan/www**，即用户 **dylan** 主目录中的 www 目录。

```apache
UserDir /usr/www
UserDir /home/*/www
```

在标准配置文件中，UserDir 访问默认是被注释掉的。通常有像 **root** 这样的用户需要拒绝访问。使用 disable 和 enable 选项，您可以允许特定用户访问，同时禁用其他用户的访问，如下所示：

```apache
UserDir disable root
UserDir disabled
UserDir enabled dylan chris justin
```

## MIME 类型

当浏览器访问网站上的网页时，它通常访问许多不同类型的对象，包括 HTML 文件、图片或声音文件以及脚本文件。为了正确显示这些对象，浏览器必须得到它们是什么类型对象的某种指示。JPEG 图片文件的处理方式与简单文本文件不同。服务器以 MIME 类型的形式提供此类型信息（参见第 13 章）。MIME 类型与通过 Internet 邮件程序（如 Pine）发送附件时使用的类型相同。每种类型的对象都关联给定的 MIME 类型。提供 MIME 类型后，浏览器可以正确处理和显示该对象。

MIME 协议将特定类型与具有给定扩展名的文件相关联。例如，扩展名为 .jpg 的文件将具有 MIME 类型 image/jpeg。**TypesConfig** 指令保存 **mime.types** 文件的位置，该文件列出了所有 MIME 类型及其关联的文件扩展名。**DefaultType** 是任何无法确定类型的文件的默认 MIME 类型。**AddType** 允许您在不编辑 MIME 文件的情况下修改 mime.types 列表。

```apache
TypesConfig /etc/mime.types
DefaultType text/plain
```

其他类型指令用于指定在特定文档上执行的操作。**AddEncoding** 允许浏览器即时解压压缩文件。**AddHandler** 将文件扩展名映射到操作，而 **AddLanguage** 允许您指定文档的语言。以下示例将扩展名为 .gz 的文件名标记为 gzip 编码文件，将扩展名为 .fr 的文件标记为法语文件：

```apache
AddEncoding x-gzip gz
AddLanguage fr .fr
```

Web 服务器可以显示和执行许多不同类型的文件和程序。然而，并非所有 Web 浏览器都能显示所有这些文件。旧版浏览器的限制最多。一些浏览器，如 Lynx，甚至没有设计用于显示简单的图形。为了让 Web 浏览器显示页面，服务器会与其进行协商以确定它可以处理的文件类型。为了启用这种协商，您需要启用 **multiviews** 选项。

```apache
Options multiviews
```

## CGI 文件

通用网关接口（CGI）文件是可以由访问您站点的 Web 浏览器执行的程序。CGI 文件通常由执行该程序作为其显示内容一部分的网页发起。传统上，CGI 程序被放置在一个名为 **cgi-bin** 的目录中，并且只有当它们驻留在这样一个特殊目录中时才能被执行。

