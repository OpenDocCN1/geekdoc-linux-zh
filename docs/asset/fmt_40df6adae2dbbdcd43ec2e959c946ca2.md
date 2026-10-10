
`pi@rpi $ sudo apt update`

`pi@rpi $ sudo apt install nginx`

`pi@rpi $ sudo reboot`

> 注意：在某些 Nginx 服务器上，你必须编辑 `/etc/nginx/sites-available/default` 配置文件，并使用 `#` 字符注释掉 `"listen []:80 default_server;"` 条目。如果你在 Pi 上安装了 Apache，则在安装 Nginx 之前必须停止它；例如，使用 `sudo service apache2 stop`。

Nginx Web 服务器默认运行在端口 `80` 上。端口号是一个可以与 IP 地址结合以为通信会话提供端点的标识符。它被有效地用于识别客户端所需的软件服务。例如，你可以使用网络统计 `netstat` 命令查找 RPi 的 IP 地址以及 RPi 上正在监听端口的服务列表：

```
pi@rpi $ sudo hostname -I

192.168.1.116

pi@rpi $ sudo netstat -tlpn

Active Connections (only servers)

Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name

tcp 0 0 0.0.0.0:80 0.0.0.0:* LISTEN 2299/nginx

tcp 0 0 0.0.0.0:22 0.0.0.0:* LISTEN 2253/ssh
```

因此，当接收到端口 `80` 的网络请求时，它会被重定向到 Nginx Web 服务器应用程序。不安全 Web 流量的常用端口为 `80`；当你在 Web浏览器中输入 URL 时，就会假设此端口。你还可以看到端口 `22` 的流量被重定向到安全外壳 `SSH` 服务器。你可以使用以下命令测试 Nginx 服务器的配置：

```
pi@rpi ~ $ sudo nginx -t

nginx: configuration file /etc/nginx/nginx.conf syntax is ok

nginx: configuration file /etc/nginx/nginx.conf test is successful
```

在执行服务器重启之前，你还可以获取有关对服务器配置更改的信息，如下：

```
pi@rpi ~ $ sudo service nginx configtest

[ ] Testing nginx configuration...

pi@rpi ~ $ sudo service nginx restart

[ ] Restarting nginx: nginx.
```

这两项测试在识别配置问题方面特别有用。

# 配置 Nginx Web 服务器

Nginx 可以使用 `/etc/nginx/` 中的文件进行配置，其中核心配置文件如下：

- `nginx.conf` 是服务器的主配置文件。
- `sites-available` 目录包含任何虚拟站点的配置文件，`sites-enabled` 目录应该包含指向 `sites-available` 目录配置文件的符号链接，以激活站点。大多数配置更改都是在 `sites-available` 目录的默认文件条目上进行的。

除了配置文件外，Nginx 的功能可以进一步扩展（例如通过使用 Python 支持），并可以使用以下命令识别当前编译到 Nginx 中的模块：

```
pi@rpi ~ $ nginx -v

nginx version: nginx/1.6.2

TLS SNI support enabled ...
```

# 创建 Web 页面和 Web 脚本

要为 RPi Web 服务器创建一个简单的 Web 页面，你可以使用 `nano` 编辑器和基础 HTML 语法，如下：

```
pi@rpi /var/www/html $ sudo nano index.html

pi@rpi /var/www/html $ more index.html

<HTML><TITLE>Raspberry Pi First Page</TITLE>

<body><h1>Raspberry Pi test page.</h1></body></html>
```

现在当你使用 Web浏览器连接到 Web 服务器时，你将看到如图 12-3 所示的输出。你可以使用 Pi 的本地 IP 地址，或 mDNS 名称（例如 `raspberrypi.local`）。(img/8d9725dcf071daded8acede3920e981_517_0.png) 图 12-3：来自 Nginx 的第一个 Web 页面

Web 页面是展示静态 Web 内容理想选择，通过使用 Notepad++ 等编辑器，你可以快速为个人 Web 服务器构建 HTML 内容。然后你可以使用路由器的端口转发将你的静态 Web 内容分享给世界。

还可以为 RPi 开发更高级的 Web 内容，使其与物理环境衔接，例如读取数据或驱动电机。实现此点的一种相对直接的方法是使用通用网关接口 `CGI` 脚本。与 Apache 不同，Nginx 默认不支持简单的 CGI。要安装它们，请使用以下步骤：

1. 安装 `fcgiwrap` 和示例配置文件：
```
pi@rpi $ sudo apt install fcgiwrap

pi@rpi $ sudo cp /usr/share/doc/fcgiwrap/nginx/default /etc/nginx/sites-available/
```

2. 在 `default` 文件中添加以下行（注意分号）：
```
server {

    listen 80;

    include /etc/nginx/sites-available/default;

};
```

3. 重启服务器：
```
pi@rpi $ sudo service nginx restart
```

4. 在 `sites-enabled` 目录中创建符号链接：
```
pi@rpi $ sudo ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled/
```

5. 脚本必须是可执行的，并且可以如下进行测试：
```
pi@rpi $ mkdir /var/www/html/cgi-bin

pi@rpi $ touch /var/www/html/cgi-bin/test.cgi

pi@rpi $ chmod a+x /var/www/html/cgi-bin/test.cgi
```

6. 使用 `nano /var/www/html/cgi-bin/test.cgi` 写入内容：
```bash
#!/bin/bash

echo "Content-type: text/html"

echo ""

echo "<html><head>"

echo '<meta charset="UTF-8">'

echo "<title>Raspberry Pi</title></head>"

echo "<body><h1>Raspberry Pi</h1><p>"

hostname

uptime

echo "</p></body></html>"
```

脚本非常冗长，但你可以看到可以在内部调用系统命令（例如 `hostname` 和 `uptime`）。当在终端中测试脚本时，它显示 HTML 源码。但当你使用 Web浏览器查看它时，HTML 会被正确渲染。

(img/8d9725dcf071daded8acede3920e981_518_0.png) 图 12-4：简单的 CGI 脚本

除了 Linux 系统命令，你还可以执行用 C/C++ 编写的程序。为了演示此功能，可以将 AM2301/2302 `DHT` 总线传感器连接到 RPi，如图 6-1 所示。列表 64 中的 `dht.cpp` 程序经过适配以输出温度和湿度值。这个新的可执行文件可以复制到 `/usr/local/bin` 目录，使其“永久”安装在 RPi 上：

```
pi@rpi $ cd /usr/local/bin

pi@rpi $ sudo chown root:root dht

pi@rpi $ sudo chmod ugo+x dht

pi@rpi $ ls -l dht

-rwxr-xr-x 1 root root 9336 Oct 11 15:36
```

CGI 脚本可以修改为直接从传感器输出温度，如下 `/var/www/html/cgi-bin/temperature.cgi`：

```bash
#!/bin/bash

echo "Content-type: text/html"

echo ""

echo "<html><head>"

echo '<meta charset="UTF-8">'

echo "<title>Pi Weather Sensor</title></head>"

echo "<body><h1>Pi Weather Sensor</h1><p>"
