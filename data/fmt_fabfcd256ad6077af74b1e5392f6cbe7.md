
上述代码需要远程服务器的 IP 地址，因为我们使用了 `yahoo.com` 的 IP 地址 (`97.158.253.26`) 作为示例。

# 3. 编写连接代码

它需要 `socket` 和 `sockaddr` 结构。如下：

```c
#include <stdio.h>
#include <sys/socket.h>
#include <arpa/inet.h>
int main(int argc) {
    int socket_desc;
    struct sockaddr_in server;
    // 创建 socket
    socket_desc = socket(AF_INET, SOCK_STREAM, 0);
    server.sin_addr.s_addr = inet_addr("97.158.253.26");
    server.sin_family = AF_INET;
    server.sin_port = htons(80);
    // 连接到服务器
    if (connect(socket_desc, (struct sockaddr *)&server, sizeof(server)) < 0) {
        printf("连接失败");
        return 1;
    }
    printf("已连接");
}
```

# 发送数据

创建一个发送数据的函数。它需要 `socket` 描述符、数据及其大小。发送到 `yahoo.com` 的代码：

```c
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
int main(int argc, char *argv[])
{
    int socket_desc;
    struct sockaddr_in server;
    char *message;
    // 创建 socket
    socket_desc = socket(AF_INET, SOCK_STREAM, 0);
    if (socket_desc == -1) {
        printf("创建 socket 失败");
    }
    server.sin_addr.s_addr = inet_addr("97.158.253.26");
    server.sin_family = AF_INET;
    server.sin_port = htons(80);
    // 连接到服务器
    if (connect(socket_desc, (struct sockaddr *)&server, sizeof(server)) < 0) {
        puts("连接错误");
        return 1;
    }
    puts("已连接\n");
    // 发送数据
    message = "GET / HTTP/1.1\r\n\r\n";
    if (send(socket_desc, message, strlen(message), 0) < 0) {
        puts("发送失败");
        return 1;
    }
    printf("数据已发送\n");
    return 0;
}
```

在上述代码中，建立了到 IP 地址的连接，然后向其发送字符串。消息实际上是获取网站主页的 HTTP 命令。

# 接收回复

创建 `recv` 函数在 `socket` 上接收数据，如下所示：

```c
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
int main(int argc, char *argv[])
{
    int socket_desc;
    struct sockaddr_in server;
    char *message, server_reply[2000];
    // 创建 socket
    socket_desc = socket(AF_INET, SOCK_STREAM, 0);
    if (socket_desc == -1) {
        printf("创建 socket 失败");
    }
    server.sin_addr.s_addr = inet_addr("97.158.253.26");
    server.sin_family = AF_INET;
    server.sin_port = htons(80);
    // 连接到远程服务器
    if (connect(socket_desc, (struct sockaddr *)&server, sizeof(server)) < 0) {
        puts("连接错误");
        return 1;
    }
    puts("已连接");
    // ... recv 逻辑在此处 ...
}
```

```php
puts("connect error");
return 1;
}
puts("Connected\n");
//Send some data
message = "GET /HTTP/1.1\r\n\n";
if (send(socket_desc, message, strlen(message), 0) < 0) {
    puts("Send failed\n");
    return 1;
}
puts("Data sent\n");
//Receive a reply from the server
if (recv(socket_desc, server_reply, 2000, 0) < 0) {
    puts("recv failed\n");
}
puts("Reply received\n");
puts(server_reply);
return 0;
```

上述代码的输出如下：

Connected
Data Send
Reply/ received
HTTP/1.1 302 Found
Location: http://www.yahoo.com/
Cache-Control: private
Content-Type: text/html; charset=UTF-8
Set-Cookie: 
PRE1F4EdDMD6b2Fb219;expires=TM-1323644706;U=1323644706;s=z6hDC9cZfGEowv_o;expires=Sun, 22-Dec-2013 12:51:46 GMT;path=/;domain=.yahoo.com
Date: Fri, 23 Dec 2011 12:51:46 GMT
Server: gws
Content-Length: 221
X-SS-Protection: 1; mode=block
X-Frame-Options: SAMEORIGIN
<<html>
<meta http-equiv="content-type" content="text/html;charset=utf-8">
<title>302 Moved</title>
</head>
<body>
<h1>302 Moved /</h1>
The document has been moved
<a href="http://www.yahoo.com/">here</a></a>></a>.
</body>
</html>

# 关闭套接字 (Close the Socket)

创建一个关闭套接字的函数。为此你需要包含 `unistd.h` 头文件。使用以下代码：

```
close(socket_desc);
```
