
```
UPDATE Filters set type = 9 LIMIT 1 OFFSET 1
UPDATE Filters destname = "snmp_monitor" LIMIT 1 OFFSET 1
UPDATE Filters set regex = "User set alert on zone ([-1-5]), (.*) LIMIT 1 OFFSET 1;
UPDATE Filters set rewrite = "ladTestAlarm TrapZoneId i %1$s TrapZoneName s '%2$s$s'" LIMIT 1 OFFSET 1;
```

```sql
UPDATE Filters Set destype = 9 LIMIT 1 OFFSET 2;
UPDATE Filters Set destname = "snmp_monitor" LIMIT 1 OFFSET 2;
UPDATE Filters Set regex = "Alarm set on zone [(1-5]), (*)" LIMIT 1 OFFSET 2;
UPDATE Filters Set rewrite = "ladAlarm ladTrapZoneId 1 %%%$s\nladTrapZoneName = '%%2$s'" LIMIT 1 OFFSET 2;
```

`SnmpDest`表中的值应为网络用户提供访问配置接收陷阱（traps）的权限，因此您需要从一个或多个 UI 使用这些值。`Laddie`界面允许您指定`Laddie` SNMP 陷阱的位置。在本例中，我们使用 SQL 手动设置了这些值。假设目标位于名为`snmp_host`的网络主机上。

```sql
UPDATE SnmpDest SET destname = "snmp_monitor" LIMIT 1;
UPDATE SnmpDest SET dest = "snmp host" LIMIT 1;
UPDATE SnmpDest SET community = "public", port = 162 LIMIT 1;
UPDATE SnmpDest SET version = 2 LIMIT 1;
```

您可以通过在其中一个网络主机上运行`snmptrapd`来测试此配置。详情请参见第 13 章。

# 总结

传统的日志记录通过将事件的报告（日志消息）放入磁盘上的一个或多个文件中来处理事件。更好的方法是逐个检查每个事件，然后决定如何妥善处理。让您的设备感知事件并对这些事件做出响应，是您可以为客户做的最好的事情之一。

在早的章节中，我们向您展示了如何使用`PostgreSQL`协议和 API 来控制设备的状态和控制。但控制和状态只是解决方案的一半——在本章中，我们介绍了事件处理，这是成功设备设计的另一半部分。

# 8 设计网页界面

![](img/ab18faa434b6e1e10df0a92984bf70fc_128_0.png)

网页浏览器已成为配置网络设备的首选用户界面，特别是对于来自`Linksys`和`Netgear`等公司的家庭路由器。

网页界面流行的推动动力是它们易于使用且不需要专门的客户端软件。客户现在期望能够访问其设备的网页界面，因此领先的家庭网络设备制造商提供这些界面并不意外。

这是系列几个专门用于用户界面（UI）设计的章节中的第一章。本章涵盖了通用的网页 UI，特别是`Laddie`网页 UI 的开发。在后续章节中，我们将查看`Laddie`的其他 UI：第 9 章的 CLI 界面、第 10 章的前面板 LCD 界面、第 11 章的帧接口以及第 12 章的红外遥控界面。所有这些 UI 都通过协议与后端守护进程通信。

本章涵盖了以下主题：

- 网页技术概述
- 为您的设备网页界面建立需求
- 选择 Web 服务器
- 设计界面的外观和感受
- 我们的实现亮点
- 经验总结与未来改进

## 网页基础

网页浏览器使用超文本传输协议（HTTP）与 Web 服务器通信，HTTP 是一种客户端-服务器协议。通信由网页浏览器（客户端）通过统一资源定位符（URL）请求网页时发起，例如，`http://www.google.com`。当 Web 服务器接收到此请求时，它会检查请求的页面是否可用，可用则将页面发送给网页浏览器。由于 HTTP 协议是基于文本的，我们可以使用：

```
GET / HTTP/1.0
```

一旦会话连接，输入以下内容：

`GET`创建的空行会导致 Web 服务器响应（GET 请求）。返回的页面是以 HTML 格式格式的；显然，如果您在浏览器中打开它，页面看起来会有不同，因为浏览器会解释标记并以人类可读的方式呈现它。注意，页面的中间部分已被省略号替换以减小其尺寸。

```
HTTP/1.1 200 OK
Cache-Control: private
Content-Type: text/html
Set-Cookie: expires=Sun, 17 Jan-2038 09:14:07 GMT; path=/
Server: Apache/2.1
Date: 26 Aug 2006 17:04:48 GMT
<head>
<meta http-equiv="content-type" content="text/html">
...
<a href="/en/about.html">About Google</a>
<p><font size="-2">&copy;2006 Google</font></p>
</body>
</html>
```

## DNS 和 TCP

网络协议`DNS`（域名系统）和`TCP`（传输控制协议）使得这种客户端-服务器的交换成为可能。给定 URL（例如`http://www.google.com`），客户端使用`DNS`确定服务器的 IP 地址。`HTTP`使用`TCP`实现客户端和服务器之间无错误的数据传输。

这些协议由互联网工程任务组（IETF）定义，IETF 是权威的互联网标准机构。有关 IETF 的更多信息，请参见`http://www.ietf.org`；有关 TCP/IP 的更多信息，请参阅 Charles M. Koenig 2005 年 Starch Press 出版的*The TCP/IP Guide*。

## Web 服务器

Web 服务器查找并返回给定 URL 的网页。该页面可能存在于文件系统或内存中，也可能在请求时动态生成。

## CGI

通用网关接口（CGI）出现作为 Web 服务器与专门定制程序通信的一种，该程序将代表 Web 服务器生成网页。在 Unix 世界中，早期的 CGI 程序是用`bash`、`Perl`和`C`等语言编写的。今天，像`PHP`这样的特定脚本语言更为常见。此外，像`Apache`等现代 Web 服务器可以配置为在 Apache Web 服务器相同的进程中运行 PHP 脚本，从而避免 CGI 通信机制。

## JavaScript

`JavaScript`已被接受为网页的客户端编程语言。`JavaScript`代码嵌入在 HTML 页面中，网页中的标签告诉浏览器何时执行`JavaScript`函数。

`JavaScript`的主要优势之一是它提供了更响应响应用户体验。`JavaScript`的缺点之一是并非所有浏览器都支持它，某些浏览器并不一定以标准方式支持它。

## 演进中的技术

随着客户端和服务器端的发展，HTML 协议经历了多次修订，并扩展到包含`XHTML`、`CSS`、`XML`和`XPath`。

底线是网页技术仍在演进。这种演进为追求网页互操作性和生命力的开发者带来了挑战。因此，作为 Web 开发者，为变化做计划是明智的。

## 建立需求

在为`Laddie`报警设备开发网页 UI 之前，我们建立了以下需求来指导我们的设计：

- 网页界面应该是易于使用的。
- 网页界面应该支持各种浏览器，包括文本浏览器。
- 网页应根据设备状态自动更新。
- 网页应遵守互联网标准，避免专用功能。
- 实现应与各种 Web 服务器兼容，以便有更好的时替换设备 Web 服务器。
- 实现应该是简单的，以便于维护。

## 选择 Web 服务器

构建设备时应使用何种 Web 服务器？在本节中，我们将回顾几种适用于 Linux 设备的 Web 服务器。

### 选择

Web 服务器有多种不同的类型。许多支持 CGI 接口，允许 Web 服务器产生任意进程来代表 Web 服务器生成网页内容。

- `Apache` Web 服务器可以编译`PHP`解释器，以便`PHP`脚本在`Apache`内部解释。这种方法减少了进程间通信并提高了响应速度。
- `lighttpd` Web 服务器支持`FastCGI`机制，产生多个`PHP`解释器并在`PHP`网页请求之间进行负载均衡。更多信息请参见`http://www.fastcgi.com`。
- `GoAhead` Web 服务器允许将 Web 服务器和所有网页打包到一个可执行文件中，从而 Web 服务器可以在没有文件系统的情况下运行。
- `Lynx` `WRT54G`无线路由器的 Web 服务器完全用`C`编写，并为每个网页手工编写函数。
- `TUX` Web 服务器运行在 Linux 内核中。
