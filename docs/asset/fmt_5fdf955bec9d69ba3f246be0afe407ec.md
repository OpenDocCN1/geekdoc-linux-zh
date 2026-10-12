
`resp = time.time() + "\r\n"`

`self.wfile.write(resp.encode('latin-1'))`

如果你正在编写一个只处理数据包并始终向客户端响应的处理器，它可以继承 `DatagramRequestHandler` 而不是 `BaseRequestHandler`。它与 `StreamRequestHandler` 共享相同的文件接口。例如：

```python
try:
    from socketserver import DatagramRequestHandler # Python 3
except ImportError:
    from _SocketServer import DatagramRequestHandler # Python 2
```

```python
class TimeServer(DatagramRequestHandler):
    def handle(self):
        resp = time.time() + "\r\n"
        self.wfile.write(resp.encode('latin-1'))
```

在这种情况下，所有写入 `self.wfile` 的数据会在 `handle()` 方法返回后收集成一个数据包。

## 服务器 (Servers)

要使用处理器，必须将其接入服务器对象中。有四种基本的服务器：

- `TCServer(address, handler)`：使用 IPv4 支持 TCP 协议的服务器。`address` 是（主机, 端口）形式的元组。`handler` 是定义的 `BaseRequestHandler` 类子类的实例。
- `UDPServer(address, handler)`：使用 IPv4 支持 Internet UDP 协议的服务器。`address` 和 `handler` 与 `TCPServer()` 相同。
- `UnixStreamServer(address, handler)`：使用 UNIX 域套接字实现流式协议。继承 `TCServer`。
- `DatagramServer(address, handler)`：使用 UNIX 域套接字实现数据报协议。继承 `UDPServer`。

所有四类服务器实例都具有以下基本方法：

- `s.fileno()`：返回服务器套接字的整数文件描述符。该方法的set使得服务器实例可以合法地用于轮询操作（如 `select()` 函数）。
- `s.serve_forever()`：处理无限数量的请求。

`s.shutdown()`

停止 `server_forever()` 循环。以下属性提供了关于运行服务器配置的一些基本信息：

### s.RequestHandlerClass

传递给服务器构造函数的用户提供的请求处理类。

### s.server_address

服务器监听的地址，例如元组 `('127.0.0.1', 80)`。

### s.socket

用于处理入入请求的套接字对象。以下是一个将 `TimeHandler` 作为 TCP 服务器运行的示例：

```python
from Server import TCPServer
```

```
serv = TCPServer('',10000,TimeHandler)
serv.server_forever()
```

以下是将处理程序作为 UDP 服务器运行的示例：

```python
from Server import UDPServer
```

```
serv = UDPServer('',10000,TimeHandler)
serv.server_forever()
```

`SocketServer` 模块的一个关键点是处理器与服务器是解耦的。一旦你写了一个处理器，就可以将其插入许多不同类型的服务器中，而无需更改其实现。

## 定义自定义服务器

服务器通常需要特殊配置，以适应不同的网络地址族、超时、并发和其他功能。这种自定义是通过继承自上一节中描述的四种服务器之一来实现的。可以定义以下类属性来定制底层网络套接字的基本设置：

### Server.address_family

服务器套接字使用的地址族。默认值是 `socket.AF_INET`。如果你想使用 IPv6，请使用 `socket.AF_INET6`。

### Server.allow_reuse_address

一个布尔标志，指示套接字是否应该重用地址。当你想要在程序终止后立即在相同端口上重新启动服务器时，此设置非常有用（否则，你将必须等待几分钟）。默认值为 `False`。

### Server.request_queue_size

传递给套接字 `listen()` 方法的请求队列的大小。默认值是 `5`。

### Server.socket_type

服务器使用的套接字类型，例如 `socket.SOCK_STREAM` 或 `socket.SOCK_DGRAM`。

### Server.timeout

服务器等待新请求的超时时间（秒）。超时时，服务器会调用 `handle_timeout()` 方法（下文描述）并返回等待。此超时不用于设置套接字超时。然而，如果设置了套接字超时，则将使用该值而非此值。

以下是如何创建一个允许重用端口服务器的示例：

```python
from SocketServer import TCPServer
```

```python
class TimeServer(TCPServer):
    allow_reuse_address = True
serv = TimeServer(('', 10000, TimeHandler))
serv.server_forever(0)
```

如果有，在继承自服务器的类中扩展以下方法是最实用的。如果你在自己的服务器中定义了这些任何方法，请确保调用了父类中的该方法。

### Server.activate()

在服务器上执行 `listen()` 操作的方法。服务器套接字引用为 `self.socket`。

### Server.bind()

在服务器上执行 `bind()` 操作的方法。

### Server.handle_error(request, client_address)

处理处理过程中发生的未捕获异常的方法。在发生最后一个异常后，使用 `sys.exc_info()` 或 `traceback` 模块中的函数。

### Server.timeout()

当服务器超时时调用的方法。通过完善此方法并调整超时设置，你可以将其他处理集成到服务器事件循环中。

### Server.verify_request(request, client_address)

如果你想在任何进一步处理之前验证连接，请重新定义此方法。如果你想实现防火墙或执行其他类型的验证，则定义此方法。

最后，通过使用混合类（mixin classes）可以使用额外的服务器功能。这就是通过线程或进程分生（fork）添加并发的方法。为此定义了以下类：

## ForkingMixIn

一种为服务器添加 UNIX 分生（forking）功能的混合类，允许它服务多个客户端。类变量 `max_children` 控制子进程的最大数量，`timeout` 变量决定了尝试收集僵尸进程之间的时间。实例变量 `active_children` 跟踪正在运行的活动进程数量。

## ThreadingMixIn

一种混合类修改服务器，使其能够通过线程服务多个客户端。对可以创建的线程数量没有限制。默认情况下，除非类 `daemon_threads` 被设置为 `True`，否则线程是非守护的。

要为服务器添加功能，你使用使用继承，并将混合类列在第一个。例如，这是一个分生服务器：

```python
from TCPServer, ForkingMixIn
```

```
class TimeServer(ForkingMixIn, TCPServer):
  reuse_address = True
  max_children = 10
serv = TimeServer(('',10000,TimeHandler))
serv.serve_forever()
```

由于并发服务器相对常见，`SocketServer` 为此定义了以下服务器：

- ForkingUDPServer(address, handler)
- ForkingTCPServer(address, handler)
- ThreadingUDPServer(address, handler)
- ThreadingTCPServer(address, handler)

这些类实际上只是根据混合类定义的。例如，这是一个分生服务器：

```
from ForkingMixIn, TCPServer
serv = ForkingTCPServer('', 10000)
```

# 492 第 21 章 网络编程与套接字
