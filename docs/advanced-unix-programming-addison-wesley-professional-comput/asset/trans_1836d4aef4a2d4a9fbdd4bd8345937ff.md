

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

BC_CLEANUP_BGN
    EC_FLUSH("Error sending response (nonfatal)")
    return false;
EC_CLEANUP_END
}

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

该函数建立连接，然后进入一个循环，在其中等待就绪的文件描述符，读取命令，并将其交给 `handle_request`。如果客户端终止或只是关闭了连接（某些客户端会不时这样做），可能会收到 EOF。在这种情况下，必须调用 `ssi_close_fd` 以告知 `ssi_wait_server` 不再考虑该文件描述符，如 8.1.3 节中所述。这个 Web 服务器确实有效，你可以从任何浏览器访问它，而不仅仅是上一节中那个简单的浏览器。例如，图 8.3 显示了通过 URL http://suse2:8000 进行访问的情况：

![](img/41b4c8f6d6a5c349eee321a301703d97_572_0.png)

服务器（称为 suse2，因为它运行 SuSE Linux）上 `/aup/webrroot/index.html` 中的 HTML 内容为：

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
        struct sockaddr_un *sunp = (struct sockaddr_un *)sa;

        if (strlen(name) >= sizeof(sunp->sun_path)) {
            errno = ENAMETOOLONG;
            EC_FAIL
        }
        strcpy(sunp->sun_path, name);
        sunp->sun_family = AF_UNIX;
        *len = sizeof(*sunp);
    }
    else {
        struct addrinfo hint;
        char nodename[SSI_NAME_SIZE], *servicename;

        memset(&hint, 0, sizeof(hint));
        hint.ai_family = domain;
        hint.ai_socktype = SOCK_STREAM;
        if (will_bind)
            hint.ai_flags = AI_PASSIVE;
        strcpy(nodename, name);
        servicename = strchr(nodename, ':');
        if (servicename == NULL) {
            errno = EINVAL;
            EC_FAIL
        }
        *servicename = '\0';
        servicename++;
        ec_ai(getaddrinfo(nodename, servicename, &hint, &infop) )
        memcpy(&sa, infop->ai_addr, infop->ai_addrlen);
        *len = infop->ai_addrlen;
        freeaddrinfo(infop);
    }
    return true;
    EC_CLEANUP_BGN
    if (infop != NULL)
        freeaddrinfo(infop);
    return false;
    EC_CLEANUP_END
}
```

我有意保持 `make_sockaddr` 独立于 `SSI` 结构，以便你希望将其提取出来并在自己的应用程序中使用。

接下来是两个函数，由 `ssi_open` 和 `ssi_close` 用于维护文件描述符的高水位标记，正如我们在第 8.1.3 节中所做的那样：

```c
static void set_fd_hwm(SSI *ssip, int fd)
{
    if (fd > ssip->ssi_fd_hwm)
        ssip->ssi_fd_hwm = fd;
}
static void reset_fd_hwm(SSI *ssip, int fd)
{
    if (fd == ssip->ssi_fd_hwm)
        ssip->ssi_fd_hwm--;
}
```

现在我们已经准备好处理 `ssi_open`，它没有做任何我们尚未见过的事情：

```c
SSI *ssi_open(const char *name_server, bool server)
{
    SSI *ssip = NULL;
    struct sockaddr_storage sa;
    socklen_t sa_len;
    ec_null( ssip = calloc(1, sizeof(SSI)) )
    ssip->ssi_server = server;
    if (strncmp(name_server, "/", 2) == 0) {
        ssip->ssi_domain = AF_INET;
        name_server += 2;
    }
    else {
        ssip->ssi_domain = AF_UNIX;
        if (!ssip->ssi_server)
            (void)unlink(name_server);
    }
    if (strlen(name_server) >= sizeof(ssip->ssi_name_server)) {
        errno = ENAMETOOLONG;
        EC_FAIL
    }
    strncpy(ssip->ssi_name_server, name_server);
    ec_false(make_sockaddr((struct sockaddr *)&sa, &sa_len,
        ssip->ssi_name_server, ssip->ssi_domain, ssip->ssi_server))
    ec_neg1(ssip->ssi_fd = socket(ssip->ssi_domain, SOCK_STREAM, 0))
    set_fd_hwm(ssip, ssip->ssi_fd);
    if (ssip->ssi_domain == AF_INET) {
        int socket_option_value = 1;

        ec_neg1(setsockopt(ssip->ssi_fd, SOL_SOCKET, SO_REUSEADDR,
            &socket_option_value, sizeof(socket_option_value)))
    }
    if (ssip->ssi_server) {
        FD_ZERO(&ssip->ssi_fd_set);
        ec_neg1(bind(ssip->ssi_fd, (struct sockaddr *)&sa, sa_len))
        ec_neg1(listen(ssip->ssi_fd, SOMAXCONN))
        FD_SET(ssip->ssi_fd, &ssip->ssi_fd_set);
    }
    else
        ec_neg1(connect(ssip->ssi_fd, (struct sockaddr *)&sa, sa_len))
    return ssip;

    EC_CLEANUP_BGN
    free(ssip);
    return NULL;
    EC_CLEANUP_END
}
```

套接字选项 SO_REUSEADDR 在第 8.3 节中有解释。

关闭一个 SSI 很简单：

```c
bool ssi_close(SSI *ssip)
{
    if (ssip->ssi_server) {
        int fd;

        for (fd = 0; fd <= ssip->ssi_fd_hwm; fd++)
            if (FD_ISSET(fd, &ssip->ssi_fd_set))
                (void)close(fd);
        if (ssip->ssi_domain == AF_UNIX)
            (void)unlink(ssip->ssi_name_server);
    }
    else
        (void)close(ssip->ssi_fd);
    free(ssip);
    return true;
}
```

接下来是 `ssi_wait_server`，它只是对第 8.1.3 节中代码的重新整理，不同之处在于它返回一个就绪的文件描述符（即除服务器套接字以外的），而不是自己使用该文件描述符：

```c
int ssi_wait_server(SSI *ssip)
{
    if (ssip->ssi_server) {
        fd_set fd_set_read;
        int fd, clientfd;
        struct sockaddr_un from;
        socklen_t from_len = sizeof(from);

        while (true) {
            fd_set_read = ssip->ssi_fd_set;
            ec_neg1(select(ssip->ssi_fd_hwm + 1, &fd_set_read, NULL, NULL,
                NULL));
            for (fd = 0; fd <= ssip->ssi_fd_hwm; fd++)
                if (FD_ISSET(fd, &fd_set_read)) {
                    if (fd == ssip->ssi_fd) {
                        ec_neg1(clientfd = accept(ssip->ssi_fd,
                            (struct sockaddr *) &from, &from_len));
                        FD_SET(clientfd, &ssip->ssi_fd_set);
                        set_fd_hwm(ssip, clientfd);
                        continue;
                    }
                }
                else
                    return fd;
        }
    }
}
```

