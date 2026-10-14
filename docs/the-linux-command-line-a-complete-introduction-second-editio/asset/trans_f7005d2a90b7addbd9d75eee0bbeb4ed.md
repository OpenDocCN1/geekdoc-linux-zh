

```
echo "Parent: child is finished. Continuing..."
echo "Parent: parent is done. Exiting."
```

这是第二个子脚本。

```
#!/bin/bash

# async-child: Asynchronous execution demo (child)

echo "Child: child is running..."
sleep 5
echo "Child: child is done. Exiting."
```

在这个示例中，我们看到子脚本很简单。真正的动作是由父脚本执行的。在父脚本中，子脚本被启动并放到后台。子脚本的进程 ID 通过将 pid 变量赋值为 $! shell 参数的值来记录，该参数始终包含最后放入后台的作业的进程 ID。

父脚本继续执行，然后使用子进程的 PID 执行 wait 命令。这会导致父脚本暂停，直到子脚本退出，此时父脚本结束。

执行时，父脚本和子脚本产生以下输出：

```
[me@linuxbox ~]$ async-parent
Parent: starting...
Parent: launching child script...
Parent: child (PID= 6741) launched.
Parent: continuing...
Child: child is running...
Parent: pausing to wait for child to finish...
Child: child is done. Exiting.
Parent: child is finished. Continuing...
Parent: parent is done. Exiting.
```

## 命名管道

在大多数类 Unix 系统中，可以创建一种特殊类型的文件，称为命名管道。命名管道用于在两个进程之间创建连接，并且可以像其他类型的文件一样使用。它们并不那么流行，但了解它们是很有用的。

有一种常见的编程架构称为客户端-服务器，它可以使用命名管道等通信方法，以及网络连接等其他类型的进程间通信。

最广泛使用的客户端-服务器系统类型，当然是 Web 浏览器与 Web 服务器的通信。Web 浏览器充当客户端，向服务器发出请求，服务器则向浏览器响应网页。

命名管道表现得像文件，但实际上形成了先进先出 FIFO 缓冲区。与普通 无名 管道一样，数据从一端进入，从另一端出来。使用命名管道，可以设置如下内容：

```
process1 > named_pipe
```

以及这样：

```
process2 < named_pipe
```

它将表现得像这样：

```
process1 | process2
```

## 设置命名管道

首先，我们必须创建一个命名管道。这是通过使用 mkfifo 命令完成的。

```
[me@linuxbox ~]$ mkfifo pipe1
[me@linuxbox ~]$ ls -l pipe1
prw-r--r-- 1 me me 0 2018-07-17 06:41 pipe1
```

在这里，我们使用 mkfifo 创建一个名为 pipe1 的命名管道。使用 ls 检查文件，我们看到属性字段中的第一个字母是 p，表示它是一个命名管道。

## 使用命名管道

为了演示命名管道的工作方式，我们需要两个终端窗口 或 两个虚拟控制台。在第一个终端中，我们输入一个简单命令并将其输出重定向到命名管道。

```
[me@linuxbox ~]$ ls -l > pipe1
```

按下 ENTER 后，命令似乎会挂起。这是因为目前还没有东西从管道的另一端接收数据。当这种情况发生时，称管道被阻塞。一旦我们在另一端附加一个进程并开始从管道读取输入，此状况就会清除。使用第二个终端窗口，我们输入此命令：

```
[me@linuxbox ~]$ cat < pipe1
```

从第一个终端窗口产生的目录列表会作为 cat 命令的输出出现在第二个终端中。第一个终端中的 ls 命令在不再被阻塞后成功完成。

## 总结

好吧，我们已经完成了我们的旅程。现在唯一要做的就是练习、练习、再练习。尽管我们在旅途中覆盖了很多内容，但就命令行而言，我们才刚刚触及表面。还有数千个命令行程序等待被发现和享受。开始在 /usr/bin 中挖掘，你就会看到了！

