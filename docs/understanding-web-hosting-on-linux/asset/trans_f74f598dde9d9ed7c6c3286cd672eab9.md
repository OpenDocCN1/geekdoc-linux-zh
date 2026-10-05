
# Linux 与互联网 • 163

![](img/069cd06404ac5e90171e6d857bf3ad28_178_0.png)

图 11.1：TCP/IP 网络的各种组件。

## 协议

理解“协议”（protocol）这个术语非常重要，因为大多数人对他们在浏览器中输入的 URL 含义存在误解。以 "http://www.mydomain.com" 这个 URL 为例。大多数人错误地认为它正在监听 (80) 端口，并且 URL 中的 "www" 代表“全球范围网”（Worldwide Web）。事实上，它确实是这个意思，但仅在名称上如此。实际上，“www” 仅仅是 "mydomain.com" 域名下的一个主机。该 URL 完全可以很容易地改为 "http://myserver.mydomain.com"，且一切运行依然正常。使用 "www" 作为标准主机名是为了让人们能够对公司网站的位置做出假设。遵循这一标准，想要查找更多关于 IBM 产品信息的人会访问 http://ibm.com。实际上，URL 中的 "http://" 部分才表示你想使用超文本传输协议（Hypertext Transfer Protocol）进行通信。

简单来说，协议是一种为了完成给定任务而约定的语言。在 Web 服务器的情况下，你的浏览器会连接到它正在监听的端口，一旦连接，就会指定特定的命令来检索单个文件。Web 服务器将返回请求的文件或一条表示未找到的错误消息。此时，连接断开，交换完成。

浏览器将对发送给它的页面进行格式化并将其显示给你。网页中嵌入的图像会对 Web 服务器产生后续影响，例如点击任何链接。每个连接都是一个独立的事务，以服务器的响应结束。你可以通过简单地连接到计算机的 Web 服务器来验证这一点。确保你的 Web 服务器正在运行（/sbin/service httpd status）。然后，从命令行输入以下内容：

```
telnet localhost 80
```

这使用客户端连接到你计算机的 HTTP 端口。一旦收到消息 `Escape character is ' '`，Web 服务器就准备好接受你的请求。输入 GET /HTTP/1.0 并按两次回车。你将收到 Web 服务器已接收你请求的通知，以及一条指示成功或失败的消息。在这种情况下，你应该收到消息 HTTP/1.1 200 Ok，随后是一些头头部信息和网页。通过输入 GET /form HTTP/1.0 并按两次回车来对比错误。该事务的编辑版本显示图 11.2 中。

```
Trying 127.0.0.1...
Connected to localhost (127.0.0.1).
Escape character is 'A'.
GET /HTTP/1.0

HTTP/1.1 200 OK
Date: Thu, 04 Dec 2001 02:08:16 GMT
Server: Apache/1.3.19 (UNIX) (Red-Hat/Linux) mod_jk
Last-Modified: Thu, 29 Mar 2001 17:53:01 GMT
ETag: "147d-b4a-3ac367d"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<HTML>
<HEAD>
<TITLE>Test Page for the Apache Web Server on Red Hat Linux</TITLE>
</HEAD>
<!-- Background white, links blue (unvisited), navy (visited), red (active) ->
<BODY COLOR="#FFFFFF">

<P>
You are free to use the image below on an Apache-powered web server.
Thanks for using Apache!
</P>

<P ALIGN="CENTER">
<A HREF="http://www.apache.org/"><IMG SRC="icons/apache_pb.gif" ALT="[Powered by Apache]"></A>
</P>

<P>
You are free to use the image below on a Red Hat Linux-powered web server.
Thanks for using Red Hat Linux!
</P>

<P ALIGN="center">
<A HREF="http://www.redhat.com/"><IMG SRC="poweredby.gif" ALT="[Powered by Red Hat Linux]"></A>
</P>

<BODY>
</HTML>
Connection closed by foreign host.
```

图 11.2：Apache 对无效请求的响应。

除了 HTTP 之外，你偶尔会看到形式为 "ftp://ftp.domain.com" 的 URL。尽管现代浏览器可以与 FTP 通信，但早期的计算机用户非常熟悉一个很奇妙地被称为 ftp 的 FTP 客户端。你可以通过在命令行执行 `ftp` 命令来体验 FTP。在 `ftp` 提示符处，输入一个问号并按回车。你将看到文件传输协议（File Transfer Protocol）包含的命令列表。如果你不想自己操作，可以随时查看图 11.3，我们已经为你完成了大部分繁重工作。

```
ftp ?
Commands may be abbreviated.

! cr mdir proxy send
$ delete mget sendport site
account debug mkdir put size
append dir mls status
```
