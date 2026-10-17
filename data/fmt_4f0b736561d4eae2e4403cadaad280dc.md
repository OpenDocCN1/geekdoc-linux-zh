
# 第 5 章：网络编程

## 标记消息边界

由于 TCP 不提供分离消息的方法，你必须在自己的网络程序中手动完成这一操作。在网络流中，界定消息有两种常用方法：

- 使用消息大小
- 使用消息结束标记

接下来的章节将描述这些方法。

## 使用消息大小

第一种方法使用消息大小来识别消息边界。如果接收主机在消息到达之前知道其大小，它就知道如何处理入站数据。使用消息大小进行数据传输有两种方式：

- 使每条消息的大小相同
- 为每条消息标记其消息大小

通过让每条消息的长度相同，你确切知道 `recv()` 函数应该通过函数调用提供的缓冲区从输入缓冲区中抓取多少数据。列表 5-7 中的 `betterserver.c` 程序通过限制 `recv()` 函数作用的字节数，修复了 `badserver.c` 程序。

### 列表 5-7：修复糟糕的 TCP 服务器问题

```c
/*
 * 专业的 Linux 编程 - 一个更好的 TCP 服务器
 */

#include <stdio.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int main(int argc, char *argv[])
{
    int i, s, fd, len;
    struct sockaddr_in my_addr;
    struct sockaddr_in remote_addr;
    int sin_size;
    char buf[BUFSIZ];

    memset(&my_addr, 0, sizeof(my_addr));
    my_addr.sin_family = AF_INET;
    my_addr.sin_addr.s_addr = INADDR_ANY;
    my_addr.sin_port = htons(8000);

    if ((s = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("socket");
        return 1;
    }

    if (bind(s, (struct sockaddr *)&my_addr, sizeof(struct sockaddr)) < 0) {
        perror("bind");
        return 1;
    }

    listen(s, 5);

    sin_size = sizeof(struct sockaddr_in);
    if ((fd = accept(s, (struct sockaddr *)&remote_addr, &sin_size)) < 0) {
        perror("accept");
        return 1;
    }

    printf("accepted client %s\n", inet_ntoa(remote_addr.sin_addr));
    len = send(fd, "Welcome to my server\n", 21, 0);

    for (i = 0; i < 5; i++) {
        len = recv(fd, buf, 13, 0);
        buf[len] = '\0';
        printf("%s\n", buf);
    }

    close(fd);
    close(s);
    return 0;
}
```

注意，`for` 循环内的 `recv()` 函数现在限制了 `recv()` 函数读取的字节数：

```c
len = recv(fd, buf, 13, 0)
```

由于客户端发送的每条消息都是 13 字节，这保证了单个 `recv()` 函数调用处理的数据不会超过一条消息。当使用 `badclient` 程序发送数据时，编译并运行 `betterserver.c` 程序产生以下结果：

```
$ ./betterserver
accepted client 10.0.1.37
test message
test message2
test message3
test message4
test message5
$
```

无论我运行程序多少次，得到的都是相同的结果。现在服务器可以干净地将消息相互隔离开。在应用程序中，发送相同大小的消息并不总是高效的。消息通常是多种消息的混合。选择一个过大的公共消息大小会导致跨网络发送大量的填充数据。为了解决这个问题，程序员通常使用可变消息大小，并在实际消息之前将消息大小发送到远程设备。接收主机必须先读取消息大小，并循环直到接收到完整消息。一旦接收了消息的所有字节，程序就可以重置以接受另一条消息。

## 连接到网络资源

libCurl 库提供了许多不同的函数来处理网络连接。主要函数由一个 `CURL` 对象句柄处理。`CURL` 对象用于跟踪连接、处理用于建立连接的参数，并提供连接返回的数据。

在执行任何函数之前，必须使用 `curl_easy_init()` 初始化 Curl 库：

```c
CURL *curl;
curl = curl_easy_init();
if (!curl) {
    perror("curl");
    return 1;
}
```

如果初始化成功，`CURL` 对象将包含一个新的句柄，可用于连接到网络资源。连接的参数使用 `curl_easy_setopt()` 函数定义。该函数的格式为：

```c
curl_easy_setopt(curl, opt, value)
```

`curl` 参数是一个已初始化的 `CURL` 对象。`opt` 参数是需要定义的连接选项，`value` 参数是该选项的定义值。有许多选项可以修改网络连接。下表显示了一些常用的选项。

| 选项 (Option) | 描述 (Description) |
| :--- | :--- |
| `CURLOPT_URL` | 指定要连接的 URL |
| `CURLOPT_USERPWD` | 指定用于连接的 用户名:密码对。 |
| `CURLOPT_PROXY` | 指定用于连接的代理服务器:端口。 |
| `CURLOPT_VERBOSE` | 指定详细模式是否开启 (1) 或关闭 (0)。 |
| `CURLOPT_HEADER` | 指定是否显示协议头信息 (1)。 |
| `CURLOPT_WRITEFUNCTION` | 指定指向接收数据的句柄指针。否则，接收到的数据将显示在标准输出上。 |
| `CURLOPT_WRITEDATA` | 传递给定义的函数的数据指针。 |
| `CURLOPT_READFUNCTION` | 指定指向发送数据的句柄指针。 |
| `CURLOPT_READDATA` | 传递给定义的读取函数的数据指针 |

定义连接参数后，使用 `curl_easy_perform()` 函数启动连接。该函数使用 `CURL` 对象指针作为参数，并返回带有结果数据的 `CURLcode` 对象。

完成 `CURL` 对象的操作后，使用 `curl_easy_cleanup()` 将其从内存中移除是明智的。

列表 5-8 中的 `getweb.c` 程序演示了一个基本的 libCurl 应用：

### 列表 5-8：使用 libCurl 库

```c
/*
 * Professional Linux Programming - 一个简单的 libCurl 程序
 */

#include <stdio.h>
#include <curl/curl.h>

int main(int argc, char *argv[])
{
    CURL *curl;
    CURLcode res;

    curl = curl_easy_init();
    if (!curl) {
        perror("curl");
        return 1;
    }

    curl_easy_setopt(curl, CURLOPT_URL, argv[1]);
    curl_easy_setopt(curl, CURLOPT_PROXY, "webproxy:8080");
    res = curl_easy_perform(curl);
    curl_easy_cleanup(curl);

    return 0;
}
```

该程序演示了使用 libCurl 进行网络编程是多么简单。仅需几行代码，该程序就使用 libCurl 库连接到远程网站并显示获取的网页。如果你的网络使用代理服务器进行连接，你需要更改 `CURLOPT_PROXY` 选项的值以匹配你的网络设置。如果你的网络不使用代理服务器，请删除该选项。

使用以下命令编译 C 程序：

```bash
$ cc -I /usr/local/include -o getweb getweb.c -lcurl
```

编译完成后，新程序会输出几页内容。你可以指定网站的全 URL（如 `http://curl.haxx.se`），或者只需指定你的网站地址（`curl.haxx.se`）。libCurl 库会尝试根据 URL 名称确定使用的默认协议。

如果连接成功，网页的 HTML 代码将显示在你的控制台上：

```
$ ./getweb http://www.google.com
<html><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Google</title>
<style>
body,td,a{font-family:arial,sans-serif}
h1{font-size:20px}
.q{color:red}
</style>
<script>
function topDig(e) {
  var elements=document.getElementsByName('more');
  for (var i=0;i<elements.length;i++) {
    var obj=elements[i];
    if (obj.style.display != "none") { obj.style.display="none"; }
  }
  return false;
}
function stopB(e) {
  if (window.event) { window.event.cancelBubble(); }
}
</script>
<span id="more" style="display:none;position:absolute;background:#f8f8f8;border:1px solid #ccc;margin:5px;padding:5px;width:16px;line-height:1.9;z-index:1000;"></span>
<form action="http://google.com/search" method="get">
<table width="255">
<td align="center">
<input type="hidden" hidden name="html" value="ISO-8859-1">
<input maxlength="2048" size="55" name="q" value="">
<input type="submit" value="Google Search">
<input type="submit" value="I'm Feeling Lucky!" name="btm1">
</td>
<td valign="top" nowrap width="255">
<font size="-2">&nbsp;&nbsp;&nbsp;<a href="/advancedsearch?hl=en">Advanced Search</a>)
<br>&nbsp;&nbsp;&nbsp;<a href="/language/tools/?hl=en">Language Tools</a>)
</font>
</td>
</table>
</form><br><br>
<font size="-1"><a href="/intl/en/ads/">Advertising&nbsp;&nbsp;&nbsp;Programs</a>) /<a href="/services/Business Solutions">Business Solutions</a> /<a href="/intl/en/about.html">About Google</a>)
</font>
<font size="2">&copy;2006 Google</font></p></p>
</html>
```
