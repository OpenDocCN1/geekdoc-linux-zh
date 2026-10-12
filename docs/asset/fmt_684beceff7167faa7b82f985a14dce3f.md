
第 204 行尝试与 MS SQL Server 的远程 socket 建立 TCP 连接。如果连接失败，则变量被设置为 10。这会导致下一次 `user` 检查返回 `undefined`，从而结束检查。如果连接成功，则将用户名和密码值传递给 `make_login_pkt` 以创建身份验证数据包，然后在第 214 行发送。来自 `pkt_lang` 变量的本地信息将在第 215 行通过单独的数据包发送。

第 217 行接收返回数据并存储在变量中，然后关闭 socket。

```
if(strlen(r) > 10 &&
ord(r[8]) == 0xE3)
{
report = string(report, 'Account ', username, ' has password ', password, '');
found = found + 1;
}
```

为了确定用户名和密码组合是否成功，脚本检查返回数据是否大于 10 字节以及第八个字节是否等于 `0xE3`。如果匹配，则向报告中添加一行，并增加发现的账户数量。

```
if(found)
{
report = string("The following accounts were found on the SQL Server:\n", report);
report += string("\An attacker can use these accounts to read or modify\n");
234 report += "*data on your SQL server. In addition, the attacker may\n");
235 report += "*to launch programs on the target system\n");
236 security_check(port, data:report);
}
```

如果有任何成功的用户名和密码组合，就会为发现的账户添加一个头，并通过 `security_check` 函数将报告提交给 Nessus 引擎。总而言，该 NASL 脚本是为高风险漏洞创建可靠检查的极佳示例。显然，由于不存在内置的 SQL 库，在该脚本上花费了大量精力。作者必须嗅探网络流量，理解身份验证序列，确定用户名和密码字段的位置。

# Nessus 编程 • 第9章 529

```perl
52 port = get_http_port(default:80);
53
54 if(get_port_state(port))exit(0);
55 sig = get_kb_item("http/hmap/" + port + "/description");
56 if (sig & "IIS") < sig) exit(0);
```

第 49 行和 50 行的包含语句指示 Nessus 引擎将指定的 `http_func.inc` 和 `http_keepalive.inc` 函数对脚本可用。第 52 行通过 `get_http_port` 从知识库（Knowledge Base）获取所有可用的 HTTP 端口，并在 54 行检测端口状态。`sig` 变量用于存储知识库中的端口描述，并在第 56 行对 `sig` 进行扫描。如果未在 Microsoft IIS 中找到字符串 IIS，或者该漏洞仅存在于 Microsoft IIS 上，则脚本将退出。

```perl
59 function check(req)
60 {
61 req = http_get(item:req, port:port);
62 r = http_keepalive_send_recv(port:port, data:req);
63 if (r == NULL) exit(0);
64
65 if("HTTP/1.1 500 Server Error" < r &&
66 "(The remote procedure call failed.") < r ||
67 "<html<head><title>Error</title>" > r)
68 {
69 security_hole(port:port);
70 return(1);
71 }
72 return(0);
73 }
```

在遇到检查代码的主体之前，作者定义了一个名为 `check` 的函数。`check` 函数接收一个字符串 `req`，作为第 61 行 `http_get` 函数的项参数。结果是一个格式化的 HTTP GET 请求，并存储回 `req` 变量中。完全格式化的请求通过 `http_keepalive_send_recv` 发送，如果存储在 `r` 中的结果为空，则脚本退出。否则，脚本将检查多个条件以确定是否存在安全漏洞。第 65 行到 67 行嵌入脚本的逻辑本质上执行以下操作：

如果请求导致服务器错误（由结果字符串 `HTTP/1.1 500 Server Error` 识别），则假设服务器存在漏洞。

或者，如果请求导致服务器返回的结果包含字符串 `The remote procedure call failed` 或者代码段读取为 `<html><head>Error</title>`，则服务器也被认为存在漏洞。

如果识别出漏洞，则 `check` 函数返回 1；如果未识别出漏洞，则返回 0。

```perl
75 dir[0] = "/scripts/";
76 dir[1] = "/cgi-bin/";
78 dir[2] = "/"
```

第 75 行、76 行和 77 行设置了目录数组的值，该数组包含了脚本尝试访问 `.plx` 文件的不同路径。使用这些路径是因为只有特定目录被标记为由处理程序处理或执行。只有通过这些目录，脚本才能正确触发 `.pl` 漏洞。

```perl
79 for(d=0; d<dir[d]; d=d+1) {
80
81 url = string(dir[d], crap(660, ".plx")); #by default perlIS.dll handles
82 if(check(req(url))) exit(0);
83
84 url = string(dir[d], crap(660, ".plx"));
85 if(check(req(url))) exit(0);
}
```

第 79 行的 `for` 循环遍历每个潜在目录，每个目录都与一个 660 字节、带有 `.plx` 扩展的文件拼接。在第 82 行调用 `check` 函数来确定漏洞状态。如果发现服务器存在漏洞（意味着满足第 65 行到 67 行嵌入的要求），则执行脚本。如果未发现服务器存在漏洞，则以 `.pl` 扩展名访问相同的文件名。同样适用于相同的逻辑。否则，循环继续并检查剩余的目录和文件，直到没有更多组合。

## Microsoft IIS 跨站脚本漏洞

由于跨站脚本（XSS）的简单性，可以为它们编写简单的检查。以下是整体的逻辑检查：

- 提供详细的作者、致谢和修订信息。
- 构建描述。
- 确定端口可用。
- 确定服务器是否存在漏洞。
- 使用构造构造的数据尝试利用漏洞。

# 第 9 章 · 为 Nessus 编码

仔细观察请求字符串，我们看到 `shml.dll` 文件位于 `_rti_bin` 中。在指定 `shml.dll` 文件之后，紧随其的是扩展字符串数据，这些数据包含了 XSS 攻击。额外的字符串信息实际上是一行完整的 JavaScript 代码，它将显示一个带有文档域名信息的告警框。如果 `shml.dll` 文件没有对额外数据进行充分的解析，那么它将按照提供的内容原样返回。当浏览器尝试解释来自 `shml.dll` 的结果时，它将处理 JavaScript 代码；然而，在我们的检查中，我们并不尝试处理该代码。验证仅需注意到原始代码没有以任何方式从原始形式被修改或解析。这样我们就知道，如果结果被合法浏览器解释，它将会被处理。

请注意，这一行是从通过网站提供的脚本中修改的。问题在于应该检查该版本，网站上列出的版本是 `shml.exe` 而不是它。我们已经在脚本中修复了这个错误。

```
61 res = http_keepalive_send_recv(port:data:req);
62 if (res == NULL) exit(0);
63 if (ereg(pattern:"HTTP/. 404 *.*", string:res)) exit(0);
```

HTTP GET 请求在第 61 行发送，如果存储在 `res` 中的结果不包含值，则脚本假设没有漏洞并退出。如果调用 `ere` 正则表达式匹配函数搜索 "HTTP/."，此模式尝试定位响应中任何以 "HTTP/" 开头、随后跟任何任意内容直到数字 `404` 之后再次跟随任意内容的行。有效来说，该表达式尝试确定 Web 服务器是否返回了 404 错误，这表示 `shml.dll` 文件未找到。如果找不到文件，脚本将正常退出并假设没有漏洞。
