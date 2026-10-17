
`servername` 可以是任何东西；我们将使用“AUP-ws”作为我们的服务器。`length` 是文档的字节长度，以便客户端知道要读取多少。这样，连接可以保持打开状态，因为客户端不需要 EOF 来告诉它停止读取。`type` 是所谓的 MIME（多用途互联网邮件扩展）类型，我们只关心其中的两种：“`text/html`” 和 “`image/jpeg`”。（还有几十种。）头部之后是文档，其形式与服务器文件系统中存在的方式完全一致。

## 8.4.3 SSI Web 浏览器

这是一个名为 `minibr` 的简单 Web 浏览器。与早期的示例一样，它可以获取 HTML；然而，它不知道如何解释标签以显示漂亮的屏幕，因此它只是将所有内容转储到标准输出：

```c
int main(void)
{
    char url[100], s[500], *path = "", *p;

    SSI *ssip;

    int fd;

    ssize_t nread;

    while (true) {
        printf("URL: ");

        if (fgets(url, sizeof(url), stdin) == NULL)
            break;

        if ((p = strchr(url, '\n')) != NULL)
            *p = '\0';

        if ((p = strchr(url, '/')) != NULL) {
            path = p + 1;
            *p = '\0';
        }

        snprintf(s, sizeof(s), "/%s:80", url);

        ec_null( ssi = ssi_open(s, false) )
        ec_negl( fd = ssi_get_server_fd(ssi) )
        snprintf(s, sizeof(s), "GET /%s HTTP/1.0\r\n\r\n", path);

        ec_negl( writeall(fd, s, strlen(s)) )

        while (true) {
            switch (nread = read(fd, s, sizeof(s))) {
                case 0:
                    printf("EOF\n");
                    break;
                case -1: EC_FAIL
                default:
                    ec_negl( writeall(STDOUT_FILENO, s, nread) )
                    continue;
            }
            break;
        }

        ec_false( ssi_close(ssi) )
        ec_false( !ferror(stdin) )
        exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
```

在调用 `fgets` 之后紧接着的代码将输入的 URL 拆分为主机名和路径（在第 8.2.5 节中有解释）。主机名前面加上斜杠，后面附加端口 80，然后传递给 `ssi_open`。路径被格式化到 HTTP GET 请求中，该请求在连接建立后发送到 Web 服务器。

下面是一个 `minibr` 会话的示例，其中获取的每个页面都大大简化了：

```
URL: www.basepath.com

HTTP/1.1 200 OK

Date: Sat, 19 Jul 2003 19:01:41 GMT

Server: Apache/1.3.27 (Unix) FrontPage/5.0.2.2510 mod_jk/1.1.0

Last-Modified: Thu, 15 May 2003 19:56:49 GMT

Etag: "61744-191-3ec3f101"

Accept-Ranges: bytes

Content-Length: 401

Connection: close

Content-Type: text/html

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML//EN">

<html>

<head>

...

URL: 216.109.125.70

HTTP/1.1 200 OK

Date: Sat, 19 Jul 2003 19:02:49 GMT

P3P: policyref="http://p3p.yahoo.com/w3c/p3p.xml", CP="CAO DSP COR CUR ADM

...

Cache-Control: private

Connection: close

Content-Type: text/html

</html>

<head>

<title>Yahoo!</title>

...
```

## 8.4.4 SSI Web 服务器

到目前为止，我们一直在展示客户端——现在是服务器的时候了。我们简单的 Web 服务器查找来自客户端的 GET 请求，从中提取路径，并根据第 8.4.2 节的描述，将响应加上请求的文件写入客户端的文件描述符。

它首先定义了一些用于它可能提供的 HTTP 响应的宏以及一些用于“未找到”错误的 HTML：

```c
#define HEADER\
    "HTTP/1.0 %s\r\n"\
    "Server: AUP-ws\r\n"\
    "Content-Length: %ld\r\n"

#define CONTENT_TEXT\
    "Content-Type: text/html\r\n\r\n"

#define CONTENT_JPEG\
    "Content-Type: image/jpeg\r\n\r\n"

#define HTML_NOTFOUND\
    "<!DOCTYPE html PUBLIC \"-//IETF//DTD HTML 2.0//EN\">\n"\
    "<html><head><title>Error 404</title>\n"\
    "<head><body>\n"\
    "<h2>AUP-ws server can't find document.</h2>\n"\
    "</body></html>\r\n"
```

请注意，`HEADER` 包含格式化代码，在实际被函数 `send_header` 使用时，这些代码会被状态码和内容长度替换：

```c
static void send_header(SSI *ssip, const char *msg, off_t len,
            const char *path, int fd)
{
    char buf[1000], *dot;
    snprintf(buf, sizeof(buf), HEADER, msg, (long)len);

    ec_negl( writeall(fd, buf, strlen(buf)) )
    dot = strchr(path, '.');
    if (dot != NULL && (strcasecmp(dot, ".jpg") == 0 ||
            strcasecmp(dot, ".jpeg") == 0))
        ec_negl( writeall(fd, CONTENT_JPEG, strlen(CONTENT_JPEG)) )
    else
        ec_negl( writeall(fd, CONTENT_TEXT, strlen(CONTENT_TEXT)) )
    return;
    EC_CLEANUP_BGN
        EC_FLUSH("Error sending response (nonfatal)")
    EC_CLEANUP_END
}
```

该函数以 `msg` 为“`404 Not Found`”或“`200 OK`”之一被调用，正如我在第 8.4.2 节中解释的。`len` 参数是文档的长度，`path` 是其文件名，仅用于确定文件是 JPEG 还是 HTML。`send_header` 的调用者负责发送文件。

`send_header` 由处理 GET 请求的函数 `handle_request` 调用：

```c
#define DEFAULT_DOC "index.html"

#define WEB_ROOT "/aup/webroot/"

static bool handle_request(SSI *ssip, char *s, int fd)
{
    char *tkn, buf[1000], path[500];
    int ntkn;
    FILE *in;
    struct stat statbuf;
    size_t nread;

    for (ntkn = 1; (tkn = strtok(s, " ")) != NULL; ntkn++) {
        s = NULL;
        switch (ntkn) {
            case 1:
                if (strcasecmp(tkn, "Get") != 0) {
                    printf("Unknown request\n");
                    return false;
                }
                continue;
            case 2:
                break;
        }
        break;
    }
    snprintf(path, sizeof(path) - 1 - strlen(DEFAULT_DOC),
             "%s%s/", WEB_ROOT, tkn);
    if (stat(path, &stbuf) == 0 && S_ISDIR(stbuf.st_mode)) {
        if (path[strlen(path) - 1] != '/')
            strcat(path, "/");
        strcat(path, DEFAULT_DOC);
    }
    if (stat(path, &stbuf) == -1 ||
        (in = fopen(path, "rb")) == NULL) {
        send_header(ssip, "404 Not Found", strlen(HTML_NOTFOUND), "", fd);
        ec_neg1( writeall(fd, HTML_NOTFOUND, strlen(HTML_NOTFOUND)) )
        return false;
    }
    send_header(ssip, "200 OK", statbuf.st_size, path, fd);
    while ((nread = fread(buf, 1, sizeof(buf), in)) > 0)
        ec_neg1( writeall(fd, buf, nread) )
    ec_eof( fclose(in) )
    return true;

    EC_CLEANUP_BGN
        EC_FLUSH("Error sending response (nonfatal)")
        return false;
    EC_CLEANUP_END
}
```

该 `for` 循环只是一种方式来检查它确实是一个 GET 请求，并提取路径名称，该名称随后被视为 `WEB_ROOT` 的子目录，以确保不会向客户端提供本地系统上的任意路径。如果它是目录，则附加默认 HTML 文件 `index.html`；否则，假定它指定了一个 HTML 或 JPEG 文件。

如果路径不存在，则发送 404 头部，随后是一些 HTML。否则，发送 200 头部，随后是文件。注意，该文件可能是文本或二进制 JPEG 文件。

最后，这里是包含对 SSI 函数调用的主程序，用于执行连接客户端的实际工作：

```c
#define PORT ":8000"

int main(void)
{
    SSI *ssip = NULL;
    char msg[1600];
    ssize_t nrcv;
    int fd;
    char host[100] = "/";

    ec_neg1( gethostname(&host[2], sizeof(host) - 2 - strlen(PORT)) )

    strcat(host, PORT);

    printf("Connecting to host %s\n", host);

    ec_null( ssip = ssi_open(host, true) )

    printf("\t...connected\n");

    while (true) {
        ec_neg1( fd = ssi_wait_server(ssip) )
        switch (nrcv = read(fd, msg, sizeof(msg) - 1)) {
        case -1:
            printf("Read error (nonfatal)\n");
            /* fall through */
        case 0:
            ec_false( ssi_close_fd(ssip, fd) )
            continue;
        default:
            msg[nrcv] = '\0';
            (void)handle_request(ssip, msg, fd);
        }
    }

    ec_false( ssi_close(ssip) )
    printf("Done.\n");
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
    return EXIT_FAILURE;
    EC_CLEANUP_END
}
```

`ssi_open` 的服务器名称形成方式如下：

`//host:8000`

我们使用端口 8000，因为端口 80 已被系统中一个真正的 Web 服务器（Apache）占用，并且 1024 以下的端口仅限于超级用户访问。

该函数建立连接，然后进入一个循环，在其中等待就绪的文件描述符，读取命令，并将其交给 `handle_request`。如果客户端终止或只是关闭了连接（某些客户端会不时这样做），可能会收到 EOF。在这种情况下，必须调用 `ssi_close_fd` 以告知 `ssi_wait_server` 不再考虑该文件描述符，如 8.1.3 节中所述。这个 Web 服务器确实有效，你可以从任何浏览器访问它，而不仅仅是上一节中那个简单的浏览器。例如，图 8.3 显示了通过 URL `http://suse2:8000` 进行访问的情况：

![](img/41b4c8f6d6a5c349eee321a301703d97_572_0.png)

服务器（称为 `suse2`，因为它运行 SuSE Linux）上 `/aup/webrroot/index.html` 中的 HTML 内容为：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<html>
<head>
</head>
<body>
<h1>Marc's Bike</h1>
<p><img src="picture.jpg">
</body>
</html>
```

### 8.4.5 SSI 实现

我已经讨论了实现 SSI 函数涉及的所有问题，并在一个示例或另一个示例中展示了所有代码。你可能希望回顾第 8.1.3、8.2.2 和 8.2.6 节。

这是类型 SSI 的结构：

```c
#define SSI_NAME_SIZE 200

typedef struct {
    bool ssi_server;	/* server? (vs. client) */
    int ssi_domain;	/* AF_INET or AF_UNIX */
    int ssi_fd;	/* socket fd */
    char ssi_name_server[SSI_NAME_SIZE];	/* server name */
    fd_set ssi_fd_set;	/* set for server’s select */
    int ssi_fd_hwm;	/* high-water-mark for fds seen */
} SSI;
```

我们将在阅读代码过程中了解这些成员是如何使用的。

首先是一个方便的函数，可以生成 AF_UNIX 或 AF_INET 的套接字地址。`name` 参数对于 AF_INET 的形式为 `host:port`，对于 AF_UNIX 则只是一个普通的名称。`will_bind` 参数指示该套接字地址是用于 `bind` 还是 `connect`，如第 8.2.6 节中所述。

```c
bool make_sockaddr(struct sockaddr *sa, socklen_t *len, const char *name,
int domain, bool will_bind)
{
    struct addrinfo *infop = NULL;

    if (domain == AF_UNIX) {
```
