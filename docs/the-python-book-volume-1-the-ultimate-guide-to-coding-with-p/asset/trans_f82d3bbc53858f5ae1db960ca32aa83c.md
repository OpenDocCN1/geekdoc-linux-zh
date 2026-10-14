

## 使用 Python

### 05 回显函数

我们需要一个可以从客户端线程调用的函数，用于向每个客户端回显一条消息。这个函数非常简单。最重要的是，向套接字发送数据被放在一个 `try` 块中，这意味着如果操作失败，我们可以处理异常，而不是让程序崩溃。

```
def echo(self, data):
# Send a message to each socket in self.client_socket
print "echoing: {}".format(data)
for socket in self.client_sockets:
# Try and echo to all clients
try:
socket.sendall(data)
except socket.error:
print "Unable to send message"
```

### 06 完成 Server 类

Server 类的剩余部分由几个简单函数组成；一个用于从套接字集合中移除套接字（这不需要解释），另一个是我们在类的初始化器中讨论过的 `signal_handler` 函数。这个函数会停止监听新连接，并解除套接字与其监听端口的绑定。最后，我们向每个客户端发送一条消息，让他们知道我们正在退出。一旦 `signal_handler` 函数结束，信号将继续按预期关闭程序。

```
def remove_socket(self, socket):
```

### 07 客户端线程

用于处理每个客户端的类继承自 `Thread` 类。这意味着可以先创建该类，然后通过 `client_thread.start()` 启动它。此时，类的 `run` 函数中的代码将在后台运行，而 Server 类的主循环将继续接受新连接。

```
class ClientListener(threading.Thread):
def __init__(self, server, socket, address):
# Initialise the Thread base class
super(ClientListener, self).__init__()
# Store the values that have been passed to the constructor
self.server = server
self.address = address
self.socket = socket
self.listening = True
self.username = "No Username"
```

### 08 客户端线程的循环

在客户端线程中运行的循环与服务器中的循环非常相似。当 `self.listening` 为真时，它会持续监听数据，并将收到的任何数据传递给一个我们稍后将要编写的 `handle_msg` 函数。传给 `socket.recv` 函数的值是接收数据时使用的缓冲区大小。

```
def run(self):
# The thread's loop to receive and process messages
while self.listening:
data = ""
try:
data = self.socket.recv(1024)
except socket.error:
"Unable to receive data"
self.handle_msg(data)
time.sleep(0.1)
# The while loop has ended
print "Ending client thread for {}".format(self.address)
```

### 09 清理收尾

我们需要一个函数来清理线程。当客户端发送一个空字符串（表示它已停止监听套接字）或发送字符串 "QUIT" 时，我们将调用此函数。发生时，我们会向每个客户端回显该用户已退出。

```
def quit(self):
# Tidy up and end the thread
self.listening = False
self.socket.close()
self.server.remove_socket(self.socket)
self.server.echo("{} quit.".format(self.username))
```

### 10 处理消息

我们的客户端可以发送三种可能的消息：
- QUIT
- USERNAME user
- 要回显给所有客户端的任意字符串

如果套接字已被关闭，客户端还会发送一堆空消息，因此我们会在这种情况下结束它们的线程。除了正则表达式部分外，代码应该相当一目了然。如果有人发送 USERNAME 消息，服务器会告诉每个客户端有新用户加入。这是通过正则表达式来检测的。`^` 表示字符串的开头，`$` 表示结尾，包含 `$` 的括号会提取 `"USERNAME"` 之后的内容。

```
accept any more connections")
self.client_sockets.append(client_socket)
print "Starting client thread for {}".format(client_address)
client_thread = ClientListener(self, client_socket, client_address)
client_thread.start()
time.sleep(0.1)
```

```
# Remove the specified socket from the client_sockets list
self.client_sockets.remove(socket)
def signal_handler(self, signal, frame):
# Run when Ctrl+C is pressed
print "Tidying up"
# Stop listening for new connections
self.listener.close()
# Let each client know we are quitting
self.echo("QUIT")
```

