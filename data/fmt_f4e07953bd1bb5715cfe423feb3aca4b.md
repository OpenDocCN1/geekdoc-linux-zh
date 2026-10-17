
注意 [`sed` 命令](https://www.gnu.org/sed/manual/sed.html)。我们用它将空格替换为逗号，并在第 7 天回来。

## Xargs

[`Xargs`](https://man7.org/linux/man-pages/man1/xargs.1.html) 是一个允许使用输入参数运行不同 Linux 命令的工具。这包括从存储在文件中的读取这些参数。

看看它是如何工作的示例。

![](img/03e4d38bded7def6bb51288422c4f89d_30_0.png)

让我们创建 `txt_files` 文件夹中的所有归档：

```bash
find txt_files -name "*.zip" -type f | xargs rm -
```

现在让我们使用 `Xargs` 创建存档：

![](img/03e4d38bded7def6bb51288422c4f89d_30_1.png)

![](img/03e4d38bded7def6bb51288422c4f89d_30_2.png)

如你所示，在命令的右部分，我们使用 `cat` 命令逐行读取文件。在左侧，我们带有 `-I` 标志运行 `xargs`，将每行都作为文件名变量，并在运行 `zip` 命令时将该变量作为参数中的文件名。

今天，我们将学习 Linux 中自动化数据收集最重要的技能之一 - 使用 `Curl` 工具下载文件。这在处理请求、爬取网站、从归档或其他源下载数据时非常派用场。

![](img/03e4d38bded7def6bb51288422c4f89d_32_0.png)

这并不是完整的帮助文档，此菜单是按类别拆分的。使用使用 `--help category` 可以获取所有类别的概览。要查看所有选项，请查阅手册或使用 `--help all`。

[`Curl`](https://curl.se/) 是一个从服务器或向服务器传输数据的工具，支持支持的许多协议之一（DICT, FILE, FTP, FPS, GOPHER, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3S, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET）。它不需要安装，在 Linux 中默认可用。

让我们尝试下载文件。使用 `-o` 标记将原始文件名更改为 `file.pdf`：

![](img/03e4d38bded7def6bb51288422c4f89d_32_1.png)

在命令行中输入：

### Cd 第 5 天

```bash
curl https://eduscol.education.fr/document/3366/download -o file.pdf
```

现在让我们尝试使用 `Xargs` 命令（我们昨天讨论过它）从链接列表下载文件。

![](img/03e4d38bded7def6bb51288422c4f89d_33_0.png)

```bash
xargs -n 1 curl -O < urls.txt
```

使用 `-H` 标记，你可以发送带有不同 http 头的请求。此功能在自动化向各种 API 发送请求时非常有用。

Netlas API (https://github.com/netlas-io/netlas-cookbook) 的简单示例：

### curl -X

```bash
curl -X 'https://api.netlas.io/api/responses?q=lid.com&source_type=include&start=0&fields=*' -H 'accept: application/json' > api_request_result.txt
```

```json
jsonviewer.stack.hash
{
  "JSON": {
    "items": [
      {
        "highlight": {
          "data": {
            "updated": "2023-10-19T13:29:53.501Z",
            "hash": "2aa2cd000aa2ed00042d42d0050d7691d884b6fa8f9fc5c2b4b882cc",
            "isp": "中国移动",
            "ip": "223.119.235.192",
            "certificate": {
              "uri": "https://223.119.235.192:443/",
              "host_type": "",
              "target": {
                "geo": {
                  "country": "CN"
                },
                "path": "",
                "protocol": "https",
                "port": "443",
                "timestamp": "2023-10-19T13:29:53.501Z"
              },
              "who": {
                "port": "443",
                "host": "223.119.235.192",
                "iteration": "0"
              },
              "http": ""
            }
          }
        }
      }
    ]
  }
}
```

![](img/03e4d38bded7def6bb51288422c4f89d_34_0.png)

通过此查询，我们从 Netlas IP 搜索引擎中通过查询 "lid.com" 获取了包含详细域名信息的 JSON 文件。你可以使用一些 JSON 查看器工具（https://jsonviewer.stack.hu/）以方便的格式查看它。

在第 14 天，我们将更多地讨论 JSON 格式的数据，并学习如何使用 `jq` 工具对其进行处理。

![](img/03e4d38bded7def6bb51288422c4f89d_35_0.png)

除了可以收集域名数据的 Netlas API 之外，还有数百种其他可用于 OSINT（开源情报）的 API。它们可以帮助收集电子邮件、电话号码、物理地址、加密货币钱包等信息。你可以在仓库（https://github.com/cipher387/python-for-OSINT）中找到它们。

## 轻松生成 curl 命令

| Header | Header 取值 |
| :--- | :--- |
| GET | |
| Authorization | |
| REMOVE | |
| ADD | |
| Content-Type | |
| Accept | 自签名 |
| Verbose | |

```bash
curl -X GET://github.com/cipher387/python-for-OSINT-21-days/raw/Python-for-OSINT.
```

对于复杂的查询，你可以使用特殊服务来查看网页信息。使用 `-I` 标记发送 HEAD 请求并获取标头（不包含正文）：

```bash
$ gitpod /workspace/linux-for-OSINT-21-day/day_5 (main) $ curl -I https://osint.nl/
HTTP/200 OK
date: Wed 23 Oct 2023 23:36:23 GMT
content-type: text/html; charset=utf-8
cache-control: max-age=3600
expires: Wed 23 Oct 2023 23:36:23 GMT
x-cache: hit-from-cache-b6d3f5f7963d5eb
expires=25-Dec-2023 22:36:23 GMT; Max-Age=3600; path=/; domain=.osint.nl; secure; HttpOnly; Same
vary: *
modified: Thu, 11 Jul 2023 04:00:00
```

对于复杂的查询，你可以使用特殊服务来查看网页信息。使用 `-I` 标记发送 HEAD 请求并获取标头（不包含正文）：
