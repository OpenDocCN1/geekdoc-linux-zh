
## 检查 Apache 是否已安装

`rpm -q apache`

```
apache-1.3.12-21
```

If the output shows an apache package name, you have the Apache software installed on your system.

1. 输入以下命令检查 Apache Web 服务器是否已安装：

`rpm -q apache`

```
apache-1.3.12-21
```

如果输出显示 `apache` 软件包名称，则表示您的系统已安装 Apache 软件。

## 检查 httpd 进程是否正在运行

2. Type the following command to check whether the `httpd` process (the name of the Apache Web server program is `httpd`) is running:

```
ps ax | grep httpd
```

The output should show a number of `httpd` processes. It is common to run several Web server processes — one parent and several child processes — so that several HTTP requests can be handled efficiently by assigning each request to an `httpd` process.

2. 输入以下命令检查 `httpd` 进程（Apache Web 服务器程序的名称为 `httpd`）是否正在运行：

```
ps ax | grep httpd
```

输出应显示多个 `httpd` 进程。通常运行多个 Web 服务器进程——一个父进程和多个子进程——以便通过将每个请求分配给一个 `httpd` 进程来高效处理多个 HTTP 请求。

## 使用 telnet 和 HTTP HEAD 命令查询 Web 服务器

3. Use the `telnet` program on your Linux system and employ the HTTP HEAD command to query the Web server as follows:

```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html
Connection closed by foreign host.
```

If you get a response such as the preceding, your system already has the Apache Web server installed and set up correctly. All you have to do is understand the configuration so that you can place the HTML documents in the proper directory.

3. 在 Linux 系统上使用 `telnet` 程序并按如下方式使用 HTTP HEAD 命令查询 Web 服务器：

```
telnet localhost 80
Trying 128.0.0.1...
Connected to localhost.
Escape character is '^]'.
HEAD / HTTP/1.0
... Press Enter once more to type a blank line
HTTP/1.1 200 OK
Date: Sat, 19 Aug 2000 23:57:14 GMT
Server: Apache/1.3.12 (Unix)  (Red Hat/Linux)
Last-Modified: Mon, 07 Aug 2000 10:21:07 GMT
ETag: "328fe-b4a-398e8d93"
Accept-Ranges: bytes
Content-Length: 2890
Connection: close
Content-Type: text/html
Connection closed by foreign host.
```
