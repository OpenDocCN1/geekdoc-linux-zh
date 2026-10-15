
此示例发送了两个分别为 123 和 456 字节的块，最后是一个 0 长度块。0 长度块指示服务器客户端已发送所有数据。

> 注意：
你必须设置 `Content-Length` (`HTTP_FIELD_CONTENT_LENGTH`) 或 `Transfer-Encoding` (`HTTP_FIELD_TRANSFER_ENCODING`) 字段来指示发送到服务器的数据量。`Content-Length` 字段包含总字节数。在发送请求之前已知道数据大小时使用该字段。

# 错误处理

`Transfer-Encoding` 字段可以设置为 "chunked"，以告诉服务器你将发送分块数据。在发送请求之前不知道数据的总大小时，请使用此字段。

在发送分块数据时，必须发送一个零长度的 `httpUpdate()`。在发送带有 `Content-Length` 的数据时，一个零长度的 `httpWrite()` 是可选的。

当发生错误时，你的程序将从 `httpUpdate` 获取 `HTTP_ERROR` 状态，或者从服务器获取一个错误。

使用 `httpError()` 函数来检查 `HTTP_ERROR` 状态报告的条件。错误编号是系统错误，因此你可以使用 `strerror()` 函数获取错误的文本消息：

```c
http_t *http;

http_status_t status;

while ((status = httpUpdate(http)) == HTTP_CONTINUE);

...

if (status == HTTP_ERROR)
{
    printf("发生以下系统错误：n\t%s\n",
    strerror(httpError(http)));
}
```

对于 HTTP 状态码，使用 `httpStatus()` 函数获取该状态的标准消息：

```c
http_t *http;

http_status_t status;

...

while ((status = httpUpdate(http)) == HTTP_CONTINUE);

...

if (status != HTTP_OK && status == HTTP_ERROR)
{
    printf("发生以下 HTTP 错误：n\t%s\n",
    httpStatus(status));
}
```

# 身份验证处理

当服务器返回 401 状态码（`HTTP_UNAUTHORIZED`）时，你的程序应该向用户询问用户名和密码，然后带有身份信息重新提交你的请求。

对于 Basic 认证，用户名和密码格式为“username:password-word”并进行 base-64 编码。你可以使用 `httpEncode64()` 函数为服务器生成必要的身份信息：

```c
http_t *http;

http_status_t status;

char username[33];

char *password;

char userpass[66];

char encoded[255];

...

nhttpGet(http, "/");

while ((status = httpUpdate(http)) == HTTP_CONTINUE) {
    if (status == HTTP_UNAUTHORIZED) {
        printf("Username: ");
        gets(username);
        password = getpass("Password: ");
        sprintf(userpass, "%s:%s", username, password);
        strncpy(encoded, "Basic ", 6);
        httpEncode64(encoded + 6, userpass);
    }
}

httpFlush(http);

ClearFields(http);

httpSetField(http, HTTP_FIELD_AUTHORIZATION, encoded);

httpGet(http, "/");

while ((status = httpUpdate(http)) == HTTP_CONTINUE) {
}
```

当你从 `httpUpdate()` 获取 `HTTP_UNAUTHORIZED` 状态时，你需要请求用户名和密码。当你获得用户名和密码后

对于 Digest 认证，密码不会以明文传递。相反，将用户名、密码、域（realm）和其他信息结合，并计算字符串的 MD5 和。然后将 MD5 和与其他支持字段一起发送给服务器。

`httpMD5()` 和 `httpMD5Final()` 函数用于大多数类型的 Digest 认证。要计算 MD5 和，你首先从 `WWW-Authenticate` 字段中获取“realm”和“nonce”子字段：

```c
http_t *http;

char nonce[256];

char realm[256];
```
...
httpGetSubField(http, HTTP_FIELD_WWW_AUTHENTICATE, "realm", realm);
httpGetSubField(http, HTTP_FIELD_WWW_AUTHENTICATE, "nonce", nonce);
```

接下来，调用 `httpMD5()` 函数来计算初始密码和：

```c
char username[33];
char *password;
char encoded[33];

httpMD5(cupsUser(username), realm, password, encoded);
```

然后使用 `httpMD5Final()` 函数将密码和与“nonce”值、请求方法和资源路径结合：

```c
char resource[HTTP_MAX_URI];
...
httpMD5Final(nonce, "POST", resource, encoded);
```

`encoded` 变量中生成的字符串是 MD5 响应字符串，它将传递给服务器。该身份验证字符串还需要用户名、“realm”和“nonce”值来验证身份：

```c
char authstring[256];

sprintf(authstring, sizeof(authstring),
  "Digest username=\"s\", realm=\"s\", nonce=\"s\", "
  "response=\"s\"", username, realm, nonce, encoded);
```

要同时处理 Basic 和 Digest 认证，只需使用 `strncmp` 检查 `WWW-Authenticate` 字段的第一个单词：

```c
if (strncmp(httpGetField(http, HTTP_FIELD_WWW_AUTHENTICATE),
  "Basic", 5) == 0)
{
  /* 执行 Basic 认证 */
}
else
{
  /* 执行 Digest 认证 */
}
...
```

# 升级加密

当服务器返回 426 状态码（`HTTP_UPGRADE_REQUIRED`）时，你的程序应该切换到加密通信。实现此最简单的方法是使用描述的 `httpEncryption(http)` 函数：

```c
http_t *http;
http_status_t status;
```

# 代理服务器处理

当服务器返回 426 状态码（`HTTP_UPGRADE_REQUIRED`）时，你的程序应该切换到加密通信。实现此最简单的方法是使用下述的 `httpEncryption(http)` 函数：

```c
http_t *http;
http_status_t status;
```

当服务器返回 426 状态码（`HTTP_UPGRADE_REQUIRED`）时，你的程序应该切换到加密通信。实现此最简单的方法是使用描述的 `httpEncryption(http)` 函数：

通常，如果你使用代理，则需要设置 `Host` 字段为代理的名称。这看起来如下：

```c
http_t *http;
http_status_t status;
...
httpSetField(http, HTTP_FIELD_HOST, "proxy.com");
```

`httpUpdate()` 函数处理服务器的任何消息。`httpEncryption()` 函数在后续章节中描述。这看起来如下：

```c
http_t *http;
http_status_t status;
...
httpFlush(http);
httpGet(http, 80);
```

# 其他实用函数

除了处理问题外，CUPS 提供了一些方便函数。第一个是 `httpSeparate()`，它分离 URL：

```c
http_t *http;
http_status_t status;
...
while ((status = httpUpdate(http)) == HTTP_CONTINUE);
```

新版本的 CUPS 增加了 `httpSeparate()`，它允许你指定字符串的大小。每个输出以空字符结尾：

```c
char url[HTTP_MAX_URI];
char scheme[HTTP_MAX_URI];
char userpass[HTTP_MAX_URI];
char server[HTTP_MAX_URI];
int port;

httpSeparateLen(url, sizeof(scheme), userpass, sizeof(userpass), server, sizeof(server), &port);
```

> 注意：`httpSeparate()` 函数已过，将在未来的版本中移除。

# 实现简单的浏览器

现在你已经熟悉了 HTTP 函数，你有足够的信息来实现简单的文本浏览器。你将首先通过 `httpSeparate()` 获取网页的主机、端口和资源：

```c
char scheme[HTTP_MAX_URI];
char userpass[HTTP_MAX_URI];
char server[HTTP_MAX_URI];
int port;
char resource[HTTP_MAX_URI];

httpSeparate(argv[1], scheme, userpass, server, &port);
```

接下来，使用 `httpConnectEncrypt()` 连接到服务器：

```c
http_t *http;

if ((http = httpConnectEncrypt(server, port, encryption)) == NULL)
```

然后使用 `HttpGet()` 向服务器发送 GET 请求：

```c
http_status_t status;
...
httpGet(http, resource);
while ((status = httpUpdate(http)) == HTTP_CONTINUE);
```

如果状态是 `HTTP_UNAUTHORIZED`，请请求用户名和密码。如果是 `HTTP_UPGRADE_REQUIRED`，则升级到 TLS 加密。

最后，从服务器读取响应并将其发送到标准输出：

```c
char buffer[1024];
int bytes;
...
while ((bytes = httpRead(http, buffer, sizeof(buffer)) - 1) > 0)
{
  buffer[bytes] = '\0';
  puts(buffer, stdout);
}
```

# 列表 15.1 browse.c 源文件

```
/* 包含 CUPS 头文件 */
#include <cups/cups.h>

/*
 * 'main' - 获取并显示 页面。
 */

int /* O 输出状态 */
main(int argc, /* I 命令行参数个数 */
     char *argv[]) /* I 命令行参数 *
{
    http_t *http;
    http_status_t status;
    char *scheme[HTTP_MAX_URI];
    char *userpass[HTTP_MAX_URI];
    char *server[HTTP_MAX_URI];
    int port;
    char *resource[HTTP_MAX_URI];
    http_encryption_t encryption;
    char *username[33];
    char *password;
    char *encoded[255];
    int bytes;
    char *buffer[1024];

/* 检查命令行。 */
if (argc != 2)
{
    puts("Usage: browse <URL>");
    return (1);
}

/* 将 URL 拆分为它的各个组件。 */
httpSeparate(argv[1], scheme, userpass, server, &port, resource);
```

```c
/* Determine我们是否需要使用 SSL。 */
if (strcmp(scheme, "https") == 0)
  encryption = HTTP_ENCRYPT_ALWAYS;
else
  encryption = HTTP_ENCRYPT_IF_REQUESTED;
```

```c
/* 连接到服务器。 */
if ((http = httpConnectEncrypt(server, port, encryption)) == NULL)
{
  perror(server);
  return (1);
}
```

```c
/* 编码 userpass 字符串。 */
if (userpass[0])
{
  strcpy(encoded, "Basic ");
  httpEncode64(encoded + 6, userpass);
}
else
  encoded[0] = '\0';
```

```c
/*发送 GET 请求，必要时重试... */
do
{
  /* 设置 HTTP 字段并发送请求。 */
  httpClearFields(http);
  httpSetField(http, HTTP_FIELD_AUTHORIZATION, encoded);
  httpGet(http, resource);
```

```c
/* 等待服务器的响应。 */
while ((status = httpUpdate(http)) == HTTP_CONTINUE)
```

```c
/* 根据需要进行身份验证或加密。 */
if (status == HTTP_UNAUTHORIZED)
{
  /* 获取用户名和密码。 */
  printf("Username: ");

break;

/* 编码用户名和密码 */
  sprintf("%s:%s", username, password);
  strncpy(encoded, "Basic ");
  httpEncode64(encoded + 6, userpass);

  /* 刷新错误消息。 */
  httpflush(http);
} else if (status == HTTP_UPGRADE_REQUIRED)
{
    /* 刷新错误消息。 */
    httpFlush(http);

    /* 升级到加密 */
    httpEncryption(http, HTTP_ENCRYPT_REQUIRED);
}
while (status == HTTP_UPGRADE_REQUIRED ||
       status == HTTP_UNAUTHORIZED);

/* 现在显示系统错误或来自服务器的数据。 */
if (status == HTTP_ERROR)
{
    printf("A system error occurred:\n\t%s\n",
           strerror(httpError(http)));
}
else
{
    while ((bytes = httpRead(http, buffer, sizeof(buffer) - 1)) > 0)
    {
        buffer[bytes] = '\0';
        fputs(buffer, stdout);
    }
}

/* 关闭服务器连接并删除 HTTP 对象。 */
httpClose(http);

/* 无错误返回 */
return (0);
}
```

# IPP 函数

CUPS IPP 接口比 HTTP 接口更简单。CUPS IPP 接口不需要处理许多状态或特殊的协议问题，例如身份验证。

# IPP 对象结构

每个 IPP 请求或响应都由 `ipp_t` "对象" 结构表示，该结构包含 `ipp_state` 头部和属性的链表。表 15.5 显示了 `ipp_t` 结构的成员。

## 表 15.5 ipp_t 结构

| 名称 | 类型 | 描述 |

|---|---|---|

| state | ipp_state_t | IPP 对象的当前状态 |

| request | ipp_request_t | IPP 请求或响应头部 |

| attrs | ipp_attribute_t * | 对象中的第一个属性 |

| last | ipp_attribute_t * | 对象中的最后一个属性 |

| current | ipp_attribute_t * | 对象中的当前属性 |

| curtag | ipp_tag_t | 当前的组标签 |

# IPP 对象状态

`state` 成员提供了对象的当前状态，用于读取和写入对象。表 15.6 列出了这些状态。

## 表 15.6 IPP 对象状态

| 名称 | 描述 |

|---|---|
