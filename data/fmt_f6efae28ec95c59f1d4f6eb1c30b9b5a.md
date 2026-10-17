
对于表格字段，我们需要小心命名，因为 HTML 规范要求表单中的所有字段必须具有唯一的名称。在 HTML 中为此类字段命名的常用方法是在列名后附加行号。例如，我们在 `Name` 后面附加行号 1（使用下划线作为分隔符），从而为区域 1 的 `Name` 列得到 `Name_1`。

生成此网页的 PHP 代码可以在本书的配套 CD 中找到，文件位于 `/opt/laddie/htdocs/web/cgi-bin/setup_alarm.php`。查看 `displayForm` 函数，它是示例中处理网页更新的 PHP 代码。

## 页面布局与菜单系统

在本节中，我们将描述 Laddie 的网页布局和菜单系统。这个简单的方案由两个 PHP 文件处理。第一个文件 `layout.php` 将 Laddie 的两级菜单系统定义为二维数组（参见本书配套 CD 中 `/opt/laddie/htdocs/web/cgi-bin/layout.php` 中的全局变量 `menu_system`），并定义了函数 `display()`。该函数用于刷新页面。第二个文件 `alarmstyle.css` 控制颜色、字体和缩进（见图 8-11）。

| 设置 (Setup) | 状态 (Status) | 报告 (Reports) | 帮助 (Help) |

|---|---|---|---|

| 网络 SNMP 报警 | 区域名称 (Zone Name) | 状态 (State) | 锁类型 (Latch Type) |

| 1 | 车库门 (Garage Door) | 已启用 (Enabled) | 非锁定 (NonLatching) |

| 2 | 电机检测器 (Motor Detector) | 已启用 (Enabled) | 锁定 (Latching) |

| 3 | 大门 (Front Door) | 已启用 (Enabled) | 锁定 (Latching) |

| 4 | 厨房窗 (Kitchen Window) | 已启用 (Enabled) | 锁定 (Latching) |

| 5 | 冰箱 (Refrigerator) | 已启用 (Enabled) | 锁定 (Latching) |

图 8-11：设计 Web 界面

## 使用 Ajax 进行异步更新

考虑图 8-9 所示的状态页面。网页如何响应报警状态的变化？

理想情况下，网页应该自动更新，而不是要求用户反复点击浏览器的“刷新”按钮。这种方法是以固定频率轮询服务器，例如使用如下 `Refresh` HTML meta 标签：

```
<META HTTP-EQUIV="Refresh" CONTENT="URL=refreshed-page.html">
```

另一种方法是使用 Ajax，使得网页仅在服务器上发生状态变化时进行更新。Ajax 的缺点是它要求在 浏览器中启用 JavaScript；如果用户禁用了 JavaScript，更新机制就会失效。另一方面，当使用 Ajax 时，网页会迅速响应服务器状态的变化并进行更新。

在第 117 页的“通过 Ajax 提高响应性”章节中，我们描述了典型的 Ajax 交换工作原理。然而，请注意，这种交换是由客户端发起的而不是服务器。我们需要一种方法来修改 Ajax，让浏览器对服务器的状态变化做出响应。

事实证明我们可以修改 Ajax 交换，使得系统的行为就像是 Web 服务器发起的交换一样。技巧在于双重处理：首先，将 `mouseover` 事件替换为 `onload` 事件，以便在网页加载后立即发送 `XMLHttpRequest`。其次，修改 Web 服务器脚本，使其阻塞等待事件。通过实现这种修改后的 Ajax 交换，每当服务器上发生特定事件时，网页就会进行更新。经验丰富的 Ajax 程序员会注意到，还有另一种机制可以实现类似的结果，特别是在 http://www.ajaxpatterns.org 中记录的 HTTP Streaming 模式（以及相关的书籍 Michael Haemhoff 编写的、O'Reilly 2006 年出版的 *Ajax Design Patterns*）。我们的方法和 HTTP Streaming 模式都有使用长连接 TCP 的缺点，这对于并发连接数有限的 Web 服务器来说可能是一个问题。然而，对于我们的方法，我们可以控制请求等待服务器事件的时间，从而限制并发连接的数量。

在描述这种修改后的 Ajax 交换的细节之前，让我们回顾一下整体。图 8-12 显示了用户请求新网页的序列，包括首次页面更新和随后的部分页面更新。从计时来看，事件 ➀ 到 ⑧ 在用户请求网页后接连发生。此时，网页已加载了最新的警报 状态。当某些警报状态在事件 ⑨ 发生变化时，它会触发事件 ⑩ 到 ⑮，此时网页将用新的警报状态进行刷新。后一个序列会一直重复，直到用户离开网页。

### 浏览器发送第一个 HTTP 请求

从事件 ➀ 到 ⑦ 的序列是标准的 HTML 请求响应交换。在步骤 ⓗ 中，用户请求网页，服务器通过发送网页进行响应，在步骤 ⑿ 中，服务器显示该页面。无论网页是否包含 JavaScript，所有 Web 请求都会执行这些步骤。通过 ����� 的剩余序列更有趣，我们将详细描述这一序列。

![](img/a28f80056348678270f2ea0cfefd7891_150_0.png)

### 浏览器发送第二个 HTTP 请求

在客户端，当网页的 `currentStatus` 在事件 ⑦ 处首次加载时，事件 ® 会立即被触发。具体来说，`GetCurrentStatus()` 函数被调用。通过启动本书的附带 CD 并使用浏览器访问 http://192.168.1.11，查看区域状态（Zone Status）页的 HTML 源码。

Laddie 设备的默认 IP 地址为 192.168.1.11（默认掩码为 255.255.0.0）。当你将此设备插入计算机并重启时，你可以在另一台电脑的任何 浏览器上使用 URL http://192.168.1.11 连接到 Web。如果默认 IP 地址与网络上的现有节点冲突，你可以按照以下步骤更改 Laddie 的 IP 地址：退出帧缓冲区界面（按 `Q` 退出），然后在提示符处输入 `root` 作为用户并按 ENTER 密码（没有密码）。在命令提示符处输入 `linux`。从 `linux` 可以导航到网络设置（Network Setup）页面并修改网络接口的 IP 地址。一旦你使用 `linux` 更改了 IP 地址，就可以在另一台电脑的浏览器中重新输入 URL（带有你的新 IP 地址）。

如果你查看此网页的源码，将看到以下行：

```
<body onload="GetCurrentStatus()">
```

`GetCurrentStatus()` 函数在事件 ⑨ 处通过 `url_for_status.php` 发起一个 `XMLHttpRequest`。你将在本书附带 CD 的 `/opt/laddie/web/cgi-bin/status.php` 文件中看到以下代码：

```javascript
function GetCurrentStatus() {
  // 使用 ms= 部分使 url 唯一，以防止 IE 检索
  // 缓存副本。
  url = "wait_for_status.php?disp_id=" + curr_id + "&ms=" + new Date(Date.getTime());
}
```

```javascript
if (window.XMLHttpRequest) {
  // Firefox/Netscape XMLHttpRequest 分支
  req_status = new XMLHttpRequest();
  if (req_status) {
    req_status.abort();
    req_status.onreadystatechange = GotStatus;
    req_status.open("GET", url, true);
    // lighthttp 必需的 Header
    req_status.requestHeader("Accept", "*/*");
    req_status.send(null);
  }
...
```

这段代码段指示浏览器发送一个 URL 为 `wait_for_status.php` 的 HTTP GET 请求。它还指示浏览器在收到服务器的响应时调用回调函数 `GotStatus()`。

### 服务器阻塞等待警报状态变化

在服务器端，脚本 `wait_for_status.php` 被调用。该脚本在事件 ⑧ 处对端口 4444 执行阻塞读取。每当在事件 ⑨ 处发生警报状态变化时，日志守护进程向端口 4444 写入消息（事件 ⑿）。写入 线程的内容并不重要；重要的是消息解阻塞了 ⑧ 处的 线程。
