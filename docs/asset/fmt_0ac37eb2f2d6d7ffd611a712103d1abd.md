
`telnet localhost 80`

```
trying 127.0.0.1...

Connected to localhost.

Escape character is '^'.

HEAD /HTTP/1.0

HTTP/1.1 200 OK

Date: Wed, 06 Dec 2000 19:59:03 GMT

Server: Apache/1.3.14 (Unix) mod_perl/1.24_01

Content-Length: 85

Connection: close

Content-Type: text/html
```

```
Connection closed by foreign host.
```

使用的 HTTP 请求是 `HEAD /HTTP/1.0`。该请求仅索 Web 服务器文档树根目录 `/` 的头部信息。使用的协议是 HTTP 1.0 版本。

HTTP 协议的最新版本是 1.1 版本。在用 `telnet` 手动连接时，1.0 版本更容易使用，因此我们在大多数示例将使用 1.0 版本。

# 第 12 章：Web 服务器与动态内容

此头部告诉我们关于所连接的机器的以下信息：

- 服务器是 Apache 版本 1.3.14。
- 服务器运行在 UNIX 上。（UNIX 版本是 Linux，但在此头部中未显示。）
- 服务器是用 mod_perl 版本 1.24_01 构建的。

## 从头部中获取信息

| 流行度 | 4 |
| 简单性 | 10 |
| 影响 | 4 |
| 风险等级 | 6 |

黑客可以根据 Web 发出的头部获取关于机器的信息。黑客可以利用这些信息来利用该特定版本的 Web 服务器软件。例如，假设在 mod_perl 版本 1.24_01 中发现了一个漏洞。黑客就可以开始扫描站点，检查它们的头部，直到找到一个使用 mod_perl 版本 1.24_01 的站点。然后他就可以开始攻击。

## 修改默认头部

许多 Web 服务器允许你修改打印在头部中的信息。例如，你可以让头部显示如下：

```
HTTP/1.1 200 OK

Date: Wed, 06 Dec 2000 19:59:03 GMT

Server: KoolWeb/3.7.1

Content-Length: 85

Connection: close

Content-Type: text/html
```

这个修改后的头部没有提供关于运行此 Web 服务器的机器的任何有用且准确的信息。寻找 mod_perl 版本 1.24_01 的黑客可能会忽略这个。修改 Apache 以显示此头部，编辑 `src/include/httpd.h`：

```
#define SERVER "Apache"

#define REVISION "1.3.14"
```

然后按照通常方式编译并安装。在启动服务器之前，在 `httpd.conf` 添加以下指令：

```
ServerTokens Min
```

> 注意 对于非 Apache Web 服务器更改头部，请参考你的 Web 服务器文档。

# 骇客入侵：Linux 安全秘密与解决方案

## 必要时升级旧软件

当黑客攻击运行旧版本有漏洞软件的机器时，最佳应对措施是确保你运行最新版本。我们无法强调这一点的重要性。

## 访问敏感数据

流行度： 4
简单性： 7
影响： 5
风险等级： 5

你有一些想要提供给特定人的敏感信息，HTTP 用户身份验证限制了对 Web 服务器特定目录的访问。浏览器通过一个输入用户名和密码的对话框来实现验证。密码用星号表示。

此用户名/密码组合由浏览器进行 base64 编码并发送到服务器。注意的是，密码是以编码的形式在网络上传输的。

这里是浏览器在头部发送的身份验证信息的示例。`Authorization` 字段用于传递编码的用户名/密码：

```
machine1 telnet 127.0.0.1...

Connected to localhost.

Escape character is '^'.

GET /protected/directory HTTP/1.0

Authorization: Basic c2VjmV00k1BbUdvZA==
```

# 第 12 章：Web 服务器与动态内容

## 使用 IP 限制保护 Web 数据

许多 Web 服务器（包括 Apache）可以根据请求者的 IP 限制目录访问。如果你知道允许访问你数据的用户的 IP 地址，Apache 可以配置为仅允许这些 IP 地址。如果不是你选择的 IP 发起请求，将被拒绝访问。

配置 Apache 根据 IP 地址限制访问的一种方法是在 `.htaccess` 中放入以下内容：

```
Order Deny, Allow

Deny from All

Allow from 192.168.1.100

Allow from 192.168.1.101
```

Apache 的配置将在本章稍后详细讨论。

## 嗅探 HTTP 身份验证用户名/密码

| 流行度 | 4 |
| 简单性 | 6 |
| 影响 | 6 |
| 风险等级 | 5 |

黑客正在嗅探你的网络并看到了传输的以下 HTTP 身份验证用户名/密码：

```
GET /protected/directory HTTP/1.0\r\nAuthorization: Basic c2VjmV00k1BbUdvZA==
```

# 破解 Linux 揭秘：Linux 安全秘密与解决方案

他知道正在被请求的文档 (`/protected/directory`)，他也知道包含加密用户名/密码的 base64 字符串。

由于身份验证字符串是明文传输的，黑客可以运行以下 Perl 命令来解密用户名/密码：

```perl
hacker_machine$ perl -MIME:Base64 -le \
> 'print decode_base64 "c2VjmVok1BbudVZA=="'
```
secret:IamGod
```

显示的输出为用户名:密码。黑客现在可以访问这些数据了。

> 注意：如第 9 章节“密码破解”所述，切勿在 HTTP 身份验证登录时对使用相同的密码。如果两个密码都相同，黑客现在就可以以你的身份登录到这台机器。

### 使用安全的 HTTP 连接

为了最大限地减少黑客从 HTTP 请求中嗅探用户名/密码的概率，请使用安全套接层（SSL）。SSL 不仅在数据传输到网站之前对其加密，还能对从网站接收的数据进行解密。因此，所有数据都以加密形式在网络上发送。

这是一个使用 tunnel 连接监听 SSL 端口 443 的网站的示例。请注意，在传输任何数据之前，都会建立一个安全连接，随后的所有数据都经过加密。因此，如果有任何敏感信息（如身份验证用户名/密码）或任何敏感数据（如信用卡号），对于在网络监听的黑客来说都是不可读取的。

```
machine1$ tunnel -f -d7 -c -r www.example.com:443
LOG[28843:1024]: Using 'example.com,443' as tcp service name
LOG[28843:1024]: Snagged 64 random bytes from /home/jdoe/.rnd
LOG[28843:1024]: Wrote 1024 new random bytes to /home/jdoe/.rnd
LOG[28843:1024]: STATUS claims sufficient entropy for the PRNG
LOG[28843:1024]: PRNG seeded successfully
LOG[28843:1024]: tunnel 3.1 on 1686-pc-linux-gnu PTHREAD+LIBWBRAP
LOG[28843:1024]: ...example.com,443 started
LOG[28843:1024]: ...example.com connecting 123.45.266.7:443
LOG[28843:1024]: Remote host connected
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: before/connect initialization
LOG[28843:1024]: SSLv3 write client hello A
LOG[28843:1024]: SSLv3 read server hello A
LOG[28843:1024]: SSLv3 read server certificate A
LOG[28843:1024]: SSLv3 write client key exchange A
```

## 第 12 章：Web 服务器与动态内容
