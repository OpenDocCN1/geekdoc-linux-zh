
172.16.0.1 - [01/Jul/1999:13:09:46 -0700] "GET /head.gif"
  -HTTP/1.0" 200 17446

172.16.0.1 - [01/Jul/1999:13:09:57 -0700] "GET /logback.gif"
  -HTTP/1.0" 404 204

172.16.0.1 - [01/Jul/1999:13:09:57 -0700] "GET /logback.gif"
  -HTTP/1.0" 404 204

172.16.0.1 - [01/Jul/1999:13:10:04 -0700] "POST /"
  -HTTP/1.0" 405 228

172.16.0.1 - [01/Jul/1999:13:10:04 -0700] "POST /"
  -HTTP/1.0" 405 228

172.16.0.1 - [01/Jul/1999:13:10:06 -0700] "GET /logback.gif"
  -HTTP/1.0" 404 204

172.16.0.1 - [01/Jul/1999:13:10:06 -0700] "GET /logback.gif"
  -HTTP/1.0" 404 204

## Linux 网络安全
第四部分

表 19.2 提供了 HTTP 代码的快速参考。

| 代码 | 描述 |
| :--- | :--- |
| 200 | 200 代码表示一切顺利；传输成功。 |
| 201 | 201 代码表示 POST 执行成功。 |
| 202 | 202 代码表示服务器已接受客户端的命令。 |
| 203 | 203 代码表示服务器部分满足了客户端请求。 |
| 204 | 204 代码表示客户端请求已处理，但服务器没有返回任何数据。 |
| 300 | 300 代码表示客户端请求的数据最近移动过。 |
| 301 | 301 代码表示服务器在备用 URL 找到了客户端请求的数据。 |
| 302 | 302 代码表示服务器为客户端请求的数据提供了一个备用位置。 |
| 303 | 303 代码表示由于服务器无法修改请求的数据，存在问题。 |
| 400 | 400 代码表示客户端请求格式错误，因此未处理。 |
| 401 | 401 代码表示客户端尝试访问未授权的数据。 |
| 402 | 402 代码表示已协商支付方案。 |
| 403 | 403 代码表示访问被禁止（最常见的代码表示未找到文档）。 |
| 500 | 500 代码表示服务器无法恢复的内部服务器错误（当客户端调用缺陷脚本时的常见错误）。 |
| 501 | 501 代码表示客户端请求服务器无法执行（或不支持）的操作。 |
| 502 | 502 代码表示服务器过载。 |
| 503 | 503 代码表示 `httpd` 等待另一个网关服务返回数据，但外部服务挂起或崩溃。 |

### error_log：错误消息日志

`error_log` 默认存储以下字段：

- 日期和时间
- 报告类型 (`error`)
- 错误原因
- 服务
- 采取的操作（有时）

以下显示了一些示例输出：

```
[root@linux apache]# more error_log

[Thu Jul 1 12:03:01 1999] [notice] Apache/1.3.1 (Unix) configured
-- resuming normal operations

[Thu Jul 1 13:09:46 1999] [error] File not exist:
-- /home/http/html/logback.gif

[Thu Jul 1 13:09:57 1999] [error] File not exist:
-- /home/http/html/logback.gif

[Thu Jul 1 13:10:06 1999] [error] File not exist:
-- /home/http/html/logback.gif

[Thu Jul 1 13:33:30 1999] [notice] httpd caught SIGTERM,
-- shutting down

[Thu Jul 1 13:35:04 1999] [notice] Apache/1.3.1 (Unix) configured
-- resuming normal operations

[Thu Jul 1 13:51:39 1999] [notice] httpd caught SIGTERM,
-- shutting down

[Thu Jul 1 21:23:28 1999] [notice] Apache/1.3.1 (Unix) configured
-- resuming normal operations
```

## 自定义 httpd 日志

Apache 允许通过 `LogFormat` 指令自定义你的日志。默认值为：
`LogFormat "%h %l %u %r" %s %b"`

这意味着默认 Apache 记录

- 远程主机地址
- 远程主机（仅当客户端运行 `ident` 时可用）
- 远程用户（不可用）
- 时间（例如 Thu Jul 1 13:10:06 1999）
- 客户端的第一行请求
- 状态
- 字节数

表 19.3 总结了 `LogFormat` 指令。

### 表 19.3 httpd LogFormat 指令

| 指令 | 功能 |
| :--- | :--- |
| `%{env_variable}` | `%e` 指令将定义指定的环境变量。 |
| `%b` | `%b` 指令记录总字节数（不包括标头）。 |
| `%f` | `%f` 指令记录请求的文件。 |
| `%h` | `%h` 指令记录远程主机地址。 |
| `%l` | `%l` 指令记录客户端用户的日志名（用户名）（如果他们运行 `ident`）。 |
| `%P` | `%P` 指令记录满足客户端请求的进程 PID。 |
| `%p` | `%p` 指令记录服务器响应的端口。 |
| `%r` | `%r` 指令记录客户端请求的第一行。 |
| `%s` | `%s` 指令记录请求的状态。 |
| `%t` | `%t` 指令记录请求的时间。 |
| `%T` | `%T` 指令记录满足客户端请求所需。 |
| `%u` | `%u` 指令记录远程用户（使用身份验证）。 |
| `%U` | `%U` 指令记录客户端最初请求的 URL。 |
| `%v` | `%v` 指令记录虚拟主机的主机名。 |

# 日志与审计追踪
第 19 章

## 注意

如果你的 Linux 系统非常老旧，你将在 `/var/adm` 中找到消息。

系统和内核消息按照它们接收的顺序出现：

```bash
[root@linux6 log~# more messages

Jul 12 12:02:50 linux6 syslog 1.3-3: restart.
Jul 12 12:02:50 linux6 kernel: klogd 1.3-3, source = /proc/kmsg.
Jul 12 12:02:50 linux6 kernel: Loaded 4122 symbols from /boot/System.map-2.0.35.
Jul 12 12:02:50 linux6 kernel: Symbols match kernel 2.0.35.
Jul 12 12:02:50 linux6 kernel: Loaded 95 symbols from 16 modules.
Jul 12 12:02:50 linux6 kernel: VFS: Mounted root (ext2 filesystem) readonly.
Jul 12 12:02:50 linux6 kernel: lo0: 0x03bc, (polling)
Jul 12 12:02:50 linux6 kernel: CSIP code 1998 Regents of the University of California
Jul 12 12:02:50 linux6 kernel: SLIP: version 0.8.4-NEW-MODULAR (dynamic channels, max=256).
Jul 12 12:02:50 linux6 kernel: PPP: version 2.2.0 (dynamic channel) allocation
Jul 12 12:02:50 linux6 kernel: PPP Dynamic allocation code copyright 1995 Caldera, Inc.
Jul 12 12:02:50 linux6 kernel: PPP line registered.
Jul 12 12:02:50 linux6 kernel: IPX 0.34 for NET3.0 Swansea Computer Society Copyright (c) 1995 Caldera, Inc.
Jul 12 12:02:50 linux6 kernel: sysctl: ip forwarding off
```
