
在所有已注册的文件描述符上进行轮询。`*timeout*` 是可选的超时时间，以毫秒为单位。返回一个元组列表 (`*fd, event*`)，其中 `*fd*` 是文件描述符，`*event*` 是表示事件的位掩码。位掩码字段与常量 `POLLIN`、`POLLOUT` 等对应。例如，要检查 `POLLIN` 事件，只需使用 `*event &* POLLIN` 测试值即可。如果返回空列表，则意味着超时且没有发生任何事件。

# 高级模块特性

`*select()*` 和 `*poll()*` 函数是该模块定义的通用性最强的函数。在 Linux 系统上，select 模块提供了边缘和水平轮询 (`*epoll*`) 接口的接口，该接口可以提供显著更好的性能。在 BSD 系统上，提供了对内核队列和事件对象的访问。编程接口可以在 http://docs.python.org/library/select 中 `*select*` 的在线文档中找到。

# 高级异步 I/O 示例

select 模块有时用于实现基于任务或协程的服务器——这种技术可以在不使用线程或进程的情况下实现并发。下面的高级示例通过实现一个基于 I/O 的协程任务调度器来阐述这一概念。预警一下——这是书中最高级的示例，需要一些研究才能理解。你可能还想参考我的 PyCON'09 教程“协程与并发奇妙课程”（http://www.dabeaz.com/coroutines）作为额外的参考材料。

```python
import select

import types

import collections
```

## 表示正在运行任务的对象
```python
class Task(object):
    def __init__(self,target):
        self.target = target  # 一个协程
        self.sendval = None   # 恢复时发送的值
        self.stack = []      # 调用栈
    def run(self):
        try:
            result = self.target.send(self.sendval)
            if isinstance(result,SystemCall):
                return
            if isinstance(result,types.GeneratorType):
                self.stack.append(self.target)
                self.sendval = None
                self.target = result
            else:
                if not self.stack:
                    return
                self.sendval = result
                self.target = self.stack.pop()
        except StopIteration:
            if not self.stack:
                raise
            self.sendval = None
            self.target = self.stack.pop()
```

## 表示“系统调用”的对象
```python
class SystemCall(object):
    def handle(self,sched,task):
        pass
```

## 调度器对象
```python
class Scheduler(object):
    def __init__(self):
        self.task_queue = collections.deque()
        self.read_waiting = {}
        self.write_waiting = {}
        self.numtasks = 0

    # 创建新任务
    def new(self,target):
        newtask = Task(target)
        self.schedule(newtask)
        self.numtasks += 1

    # 将任务放入队列
    def schedule(self,task):
        self.task_queue.append(task)

    # 任务等待文件描述符读取
    def readwait(self,fd):
        self.read_waiting[fd] = task

    # 任务等待文件描述符写入
    def writewait(self,fd):
        self.write_waiting[fd] = task

    # 主调度循环
    def mainloop(self,count=-1,timeout=None):
        while self.numtasks:
            # 检查 I/O
            if count > 0:
                # (此处逻辑根据上下文推断，原文中代码部分似乎有逻辑断层或不完整，此处按结构翻译)
                pass
            # ... (后续逻辑省略)
        pass
```

## 第 21 章 网络编程与套字

- 如果任何任务退出（`StopIteration`），它就会被丢弃。如果一个任务产出（yield），它会被重新放回任务队列，以便再次运行。这一过程将持续进行，直到没有更多任务或所有任务都处于阻塞状态，等待更多的 I/O 事件。作为一种选项，`mainloop()` 接受一个 `count` 参数，可以在指定数量的 I/O 轮询操作后返回。如果需要将调度器集成到另一个事件循环中，这可能会非常有用。

- 调度器最微妙的方面可能过于在 `mainloop()` 方法中对 `SystemCall` 实例的处理。如果一个任务产出了一个 `SystemCall` 实例，调度器会调用其 `handle()` 方法，并将相关的 `Scheduler` 和 `Task` 对象作为参数传递。系统调用的目的是执行与任务或调度器本身相关的某种内部操作。`ReadWait()`、`WriteWait()` 和 `NewTask()` 类就是此类调用的示例。例如，`ReadWait()` 接收一个任务并调用调度器调用的 `read()` 方法，调度器将其放入适当的区域。在这里，对象之间再次存在关键的解耦。任务产出 `SystemCall` 对象来请求服务，而不是直接与调度器交互。相反，`SystemCall` 对象对任务和调度器执行操作，但并不绑定到任何特定的调度器或任务实现。因此，从理论上，你可以编写一个完全不同的调度器实现（可能使用线程），将其插入此框架中并仍然能够工作。

下面是一个使用 I/O 任务调度器实现的计时服务器示例。它将阐明之前列表中描述的许多概念：

```python
from socket, AF_INET, SOCK_STREAM

def time_server(address):

    import time

    s = socket(AF_INET, SOCK_STREAM)

    s.bind(address)

    s.listen(5)

    while True:

        yield ReadWait(s)

        conn, addr = s.accept()

        print("Connection from %s" % str(addr))

        yield WriteWait(conn)

        resp = time.time() + "\r\n"

        conn.send(resp.encode('latin-1'))

        conn.close()

sched = Scheduler() # Server on port 10000

sched.new(time_server(('',11000'))) # Server on port 11000

sched.run()
```

在这个示例中，两个服务器正在并发运行——每个服务器都在不同的端口号上（使用 telnet 连接并测试）。`ReadWait()` 和 `WriteWait()` 语句会导致运行中的协程挂起，直到在关联套字上可以进行 I/O 操作。当这些语句返回时，代码将立即执行 I/O 操作，如 `accept()` 或 `send()`。

使用 `ReadWait` 和 `WriteWait` 看起来可能相当底层。幸运的是，我们的设计允许这些操作隐藏在库函数和方法之后——只要它们是协程。考虑以下封装了套字对象并模拟其接口的类：

```python
class CoSocket(object):
    def __init__(self, sock):
```
