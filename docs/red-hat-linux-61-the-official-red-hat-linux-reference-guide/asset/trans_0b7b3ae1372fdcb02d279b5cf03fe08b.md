

## 10.52. ReadmeName

ReadmeName 指定文件名，如果该文件存在于目录，会被追加到生成的目录列表末尾。Web 服务器首先尝试将该文件作为 HTML 文档包含，然后尝试作为纯文本包含。默认情况下，ReadmeName 设置为 README.html。

## 10.53. HeaderName

HeaderName 指定文件名，如果该文件存在于目录，会被插入到服务器目录列表的开头。与 ReadmeName 类似，服务器会尝试将其作为 HTML 文档包含，或者以纯文本形式包含。

## 10.54. IndexIgnore

IndexIgnore 列出文件扩展名、部分文件名、通配符表达式或完整文件名。Web 服务器不会在服务器生成的目录列表中包含任何匹配这些参数之一的文件。

## 10.55. AddEncoding

AddEncoding 指定应指定特定编码类型的文件扩展名。AddEncoding 还可以用于指令浏览器在下载时解压缩某些文件。

## 10.56. AddLanguage

AddLanguage 将文件名扩展名与特定语言关联。该指令对于 Apache HTTP 服务器非常有用，它可以根据客户端 Web 浏览器的语言设置提供多语言的内容。

## 10.57. LanguagePriority

Language-Priority 设置客户端 Web 浏览器语言偏好不同语言的优先级。

## 10.58. AddType

使用 AddType 指令来映射 MIME 类型和文件扩展名对。例如，使用 PHP 时，使用 AddType 指令让 Web 服务器识别 PHP 扩展名（.php4, .php3, .php）为 PHP MIME 类型。以下指令允许 Apache HTTP 服务器识别 AddType text/html。

```
AddType text/html .html
AddHandler server-parsed .shtml
```

## 10.59. AddHandler

AddHandler 将文件扩展名映射到特定的处理器。例如，cgi-script 处理器可以匹配扩展cgi 扩展名，从而自动将以 .cgi 结尾的文件视为 CGI 脚本。以下是 .cgi 扩展名的示例 AddHandler 指令。

```
ErrorHandler cgi-script .cgi
```

此指令允许 cgi-bin 之外的 CGIs 在服务器上的任何目录中运行，只要该目录容器内开启了 ExecCGI 选项。有关设置目录的 ExecCGI 选项的更多信息，请参阅第 10.5.24 节 Directory。

除了 cgi 脚本，AddHandler 指令还用于处理服务器解析的 HTML 和图像映射文件。

## Chapter 10. Apache HTTP Server

## 10.5.60. Action

Action 指定 MIME 类型和 CGI 脚本对，每当请求某种媒体类型的文件时，都会执行特定的 CGI 脚本。

## 10.5.61. ErrorDocument

ErrorDocument 将 HTTP 响应码与发送回客户端的消息或 URL 关联。默认情况下，当发生错误时，Web 服务器输出一个简单且通常晦涩的消息。ErrorDocument 指导 Web 服务器输出自定义消息或将客户端重定向到本地或外部 URL。

> **重要**

为了确保有效，消息必须包含在一对双引号 "" 中。

## 10.5.62. BrowserMatch

BrowserMatch 允许服务器根据 User-Agent HTTP 头部字段（用于识别客户端浏览器类型）定义环境变量并采取适当的操作。默认情况下，Web 服务器使用 BrowserMatch 拒绝具有已知问题的浏览器的连接，并对已知这些操作存在问题的浏览器禁用保持连接（keepalives）和 HTTP 头部。

## 10.5.63. Location

<Location> 和 </Location> 标签创建一个容器，可以在其中指定基于 URL 的访问控制。

例如，要允许从服务器域名连接的人查看状态报告，请使用以下指令：

```
<Location /server-status>
SetHandler server-status
Order deny,allow Deny from all
Allow from <.example.com>
</Location>
```

将 <.example.com> 替换为服务器的二级域名。

要为来自域名内部的请求提供服务器配置报告（包括已安装的模块和配置指令），使用以下指令：

```
<Location /server-info>
SetHandler server-info
Order deny,allow
Deny from all
Allow from <.example.com>
</Location>
```

再次，将 <example.com> 替换为服务器的二级域名。

## 10.5.64. ProxyRequests

要配置 Apache HTTP Server 作为代理服务器运行，请删除 <IfModule mod_proxy.c> 行开头的注释标记以启用 mod_proxy 模块，并将 ProxyRequests 指令设置为 On。

## 10.5.65. ProxyVia

<Proxy > </Proxy> 标签创建一个容器，包含了一组仅适用于代理服务器的配置指令。许多指令也适用于目录，并可以在 <Proxy> 标签内使用。

## 10.5.66. ProxyVia

ProxyVia 命令控制在通过代理服务器的请求或响应中是否发送 HTTP 头部。如果将 ProxyVia 设置为 On，则 Via: 头部会发送主机名；设置为 Full，则显示主机名和 Apache HTTP 服务器版本；设置为 Off，则原样传递任何 Via: 行；设置为 Block，则会删除这些行。

## 10.5.67. Cache Directives

默认 Apache HTTP Server 配置提供了一些缓存指令。在大多数情况下，取消行首哈希标记 [#] 的注释就足够了。然而，这里有一些与缓存相关的最重要的指令：

- CacheRoot 指定缓存文件的目录名称。默认 CacheRoot 为 /var/httpd/proxy/。
- CacheSize 指定缓存可以使用的空间（单位为 KB）。默认 CacheSize 为 5 KB。
- CacheInterval 指定缓存文件被删除前必须经过的小时。默认 CacheInterval 为 4 小时。
- CacheMaxExpires 指定文档保留的时间（无需从原始服务器重新加载）。默认为 24 小时。
- CacheLastModified 指定为未从其原始服务器获取过期的文档创建一个过期日期。默认 CacheLastModifiedFactor 为 0.1。
- CacheDefaultExpires 指定使用不支持过期的协议收到的文档的过期时间。默认为 1 小时。
- NoCache 指定不缓存的主机列表。

## Chapter 10. Apache HTTP Server

## 10.5.68. NameVirtualHost

NameVirtualHost 指令将 IP 地址和端口号关联到任何基于名的主机。基于名的托管允许一个 Apache HTTP Server 在不使用多个 IP 地址的情况下提供不同的域名。

基于名的虚拟主机仅适用于非安全 HTTP 连接。如果使用虚拟主机，请使用基于 IP 地址的虚拟主机。

要启用基于名的虚拟主机，请取消 NameVirtualHost 指令并添加 IP 地址。为每个虚拟主机添加 VirtualHost 容器。

## 10.5.69. VirtualHost

<VirtualHost> 和 </VirtualHost> 标签创建一个概述虚拟主机特征的容器。<VirtualHost> 容器接受配置指令。

httpd.conf 提供了一组注释的 VirtualHost 容器，说明了每个虚拟主机所需的最小配置指令。请参阅第 10.8 节 Virtual Hosts 获取更多关于虚拟主机的信息。

## 10.5.70. SSL Configuration Directives

/etc/httpd/conf.d/ssl.conf 文件中的 SSL 指令可以配置 SSL 和 TLS 安全 Web 通信。

## 10.5.71. SetEnvIf

SetEnvIf 在传入安全连接的头部上设置环境变量。在提供的 /etc/httpd/conf.d/ssl.conf 文件中，它用于禁用 HTTP 保持连接并允许 SSL 在没有客户端浏览器关闭警告的情况下关闭连接。此设置对于某些不关闭 SSL 连接的浏览器是必要的。

