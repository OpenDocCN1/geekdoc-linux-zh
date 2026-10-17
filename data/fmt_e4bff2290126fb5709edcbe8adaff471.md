
# Unpack source directory `scgi-1.12` from tarball

```bash
tar xfz scgi-1.12.tar.gz

cd scgi-1.12

# Build the Python part
python setup.py build

# Install Python module; we'll need root privileges
sudo python setup.py install

# Now build and install the Apache module
cd apache2

sudo make install

# Enable the SCGI module in Apache. This may fail,
# depending on your Apache version, but no matter.
sudo a2enmod scgi

# Make Apache's new configuration take effect
sudo /etc/init.d/apache2 force-reload
```

1: `libapache2-mod-scgi`

你也可以手动安装这两个组件中的任意一个。Apache 模块需要 C 编译器以及 Apache 的 `apxs` 脚本。一些发行版将 `apxs` 保留在单独的开发包中，而不是作为常规 Apache 包的一部分进行安装。

假设你现在已经拥有了这些组件，接下来请下载源代码包 `scgi-1.12.tar.gz`，并运行清单 1 中所示的命令。

# 测试运行

现在，让我们确保一切正常。Python 包是一个包含一些类的模块，通常，你会编写应用程序作为导入该模块的程序。但是，为了调试目的，你也可以将其作为独立应用程序运行。当它接收到来自 Web 服务器的请求时，它仅将请求的详细信息作为测试页面打印出来。这是第一次测试的完美选择——无需编写代码！

在你的系统上找到 `scgi_server.py` 模块。它应该安装在 `/usr/lib/python2.4/site-packages/scgi`（在你的系统上，2.4 可能是 2.3 或 2.5）。然后，运行该模块：

```bash
cd /usr/lib/python2.4/site-packages/scgi

python scgi_server.py
```

这会在系统上的 TCP 端口上监听来自 Web 服务器的请求，默认使用端口 `4000`。你可以通过将期望的端口号作为命令行参数传递来使其监听不同的端口，例如

```bash
python /usr/lib/python2.4/site-packages/scgi/scgi_server.py 63080
```

该模块将持续运行，直到你终止它，因此请在一个单独的 shell 中启动它。请记住，你不需要以 `root` 用户身份甚至不需要以 Web 服务器的身份运行 SCGI 服务器。

既然 SCGI 应用程序正在等待请求，请在你的网站上选择一个位置将其委托给该应用程序。假设你希望它响应此服务器上所有对 `"/scgistest"` 的请求。编写一个 Apache 配置片段，如清单 2 所示，并将其写入 `/etc/apache2/conf.d` 中的新文件。

# 清单 2. Apache 配置片段

```apache
# Load the SCGI module. This is really only needed
# if you installed manually and the "a2enmod scgi"
# command failed.

LoadModule scgi_module /usr/lib/apache2/modules/mod_scgi.so

<Location "/scgistest">
    # Enable SCGI
    SCGIHandler On

    # Other properties for /scgistest, such as access control
    # ...
</Location>

# Hostname and port number where SCGI server for /scgistest is running.
# Port 4000 on localhost (127.0.0.1) is the default.

SCGIMount /scgistest 127.0.0.1:4000
```

# 清单 3. `scgi_server.py` 返回请求详细信息。

```text
SERVER_SOFTWARE: 'Apache'
SCRIPT_NAME: '/scgistest'
REQUEST_METHOD: 'GET'
SERVER_PROTOCOL: 'HTTP/1.1'
QUERY_STRING: ''
CONTENT_LENGTH: '0'
HTTP_ACCEPT_CHARSET: 'UTF-8,*'
HTTP_USER_AGENT: 'Mozilla/5.0'
SERVER_NAME: 'testserver.example.org'
REMOTE_ADDR: '10.99.11.99'
SERVER_PORT: '80'
SERVER_ADDR: '192.0.34.166'
DOCUMENT_ROOT: '/srv/www/'
SERVER_ADMIN: 'webmaster@example.org'
HTTP_HOST: 'testserver.example.org'
REQUEST_URI: '/scgistest'
HTTP_ACCEPT: 'text/html,text/plain,*/*;q=0.5'
REMOTE_PORT: '47088'
HTTP_ACCEPT_LANGUAGE: 'en'
SCGI: '1'
HTTP_ACCEPT_ENCODING: 'gzip,deflate'
```

SCGI 服务器实际上不需要与 Web 服务器运行在同一台机器上，正如这里所见。只需确保 SCGI 服务器的端口被正确防火墙保护，以便只有你的 Web 服务器才能访问它！这样，你的应用程序就可以确信所有 CGI 参数都首先经过了 Web 服务器的验证。如果攻击者可以直接连接到你的 SCGI 应用程序，你就无法信任这些信息。例如，CGI 参数 `AUTHENTICATED_USER` 告诉你的应用程序请求来自某个特定的已登录用户。只有当你从配置正确的 Web 服务器那里听到这一信息时，你才能相信它。

# 深入理解

`SCGI 允许你的程序只启动一次，并可以继续处理请求，直到它愿意为止。`

使 Apache 重新加载其配置，使用 `sudo /etc/init.d/apache2 reload`。现在，你的服务器应该提供一个新的位置，`scgiset`，当你访问它时，它会简单地打印出你的请求的 CGI 参数。通过浏览器查看来验证这一点。如果你的服务器地址是 `example.org`，请将浏览器指向 `http://example.org/scgiset`。你应该会看到类似于清单 3 的页面。

如果你看到的不是这样，请查看你运行模块所在的 shell。它可能在那里打印了一些有用的错误消息。或者，如果 SCGI 服务器完全没有反应，请求可能根本没有到达它；请检查 Apache 错误日志。

一旦你运行起来，恭喜——最糟糕的部分已经过去了。停止你的 SCGI 服务器进程，以免干扰我们接下来要做的事情。

# 编写应用程序

现在，让我们用 Python 编写一个简单的 SCGI 应用程序——一个打印时间的程序。

我们导入 SCGI Python 模块，然后编写我们的应用程序作为通过 Web 服务器传入的 SCGI 请求的处理程序。该处理程序采用一个类，我们从 `SCGIHandler` 派生该类。叫我缺乏想象力也好，但我已将示例处理程序类称为 `TimeHandler`。我们稍后会填入实际代码，但先从这个骨架开始：

```python
#!/usr/bin/python
import scgi
import scgi.scgi_server

class TimeHandler(scgi.scgi_server.SCGIHandler):
    pass    # (no code here yet)

# Main program: create an SCGIServer object to
# listen on port 4000.  We tell the SCGIServer the
# handler class that implements our application.

server = scgi.scgi_server.SCGIServer(
    handler_class=TimeHandler,
    port=4000
)

# Tell our SCGIServer to start servicing requests.
# This loops forever.

server.serve()
```
