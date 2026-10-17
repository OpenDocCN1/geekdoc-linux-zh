
`http://www.server.com/cgi/ls?tmp+proc`

- 服务器创建子进程，并将`stdin`（标准输入）、`stdout`（标准输出）和`stderr`（标准错误输出）重定向到客户端通道。

- 接下来，服务器使用`exec()`系统调用来调用该程序。

通过简单的事实可以看出多任务处理的强大之处：没有多任务处理，就无法有效地运行外部程序。`exec()`系统调用有五种变体：

- `exec1()`可变参数列表，第一个参数是带有完全限定路径的命令。后续的所有参数都是命令行参数，从第零个参数（`arg[0]`）开始。列表以零或`NULL`结尾。

```c
/* For example: */
if ( exec1("/bin/ls", "/bin/ls", "-aF", "/etc", NULL) != 0 )
    perror("exec1 failed"); exit(-1);    /* actually the "if" is redundant -
                                           exec does not
                                           return unless it failed */
```

- `execl()`类似于`exec1()`。

## 注意

`exec1()`系统调用看起来可能有多余之处；为什么第一个和第二个参数是相同的命令？第一个参数是实际执行的命令名称，第二个是第零个命令行参数（类似于 C 程序中`main()`里的`arg[0]`）。不要忘记包含名称——一些外部命令会检查名称以确定使用何种行为。另外，不要忘记最后一个`NULL`或零；它表示参数列表的结束。

- `execp()`类似于`exec1()`，但命令会在执行路径中进行搜索。

```c
/* For example: Find the program 'ls' in execution path */
if ( execp("ls", "ls", "-aF", "/etc", NULL) != 0 )
    perror("execp failed"); exit(-1);
```

- `execle()`类似于`execl()`，但最后一个参数是一个表示环境的字符串数组。记得用`NULL`或零结束参数列表。

```c
/* For example: */
char *env[] = { "PATH=/bin:/usr/bin", "USER=gonzo", NULL };
if ( execle("/bin/ls", "/bin/ls", "-aF", "/etc", NULL, env) != 0 )
    perror("execle failed"); exit(-1);
```

- `execv()`有两个参数。第一个是命令的完全限定路径。第二个是命令行参数数组。数组的最后一个条目是零或`NULL`。

```c
/* For example: */
char *args[] = { "/bin/ls", "-aF", "/etc", NULL };
if ( execv(args[0], args) != 0 )
    perror("execv failed"); exit(-1);
```

- `execvp()`类似于`execv()`，但命令会在执行路径中进行搜索。

```c
/* For example: */
char *args[] = { "ls", "-aF", "/etc", NULL };
if ( execvp(args[0], args) != 0 )
    perror("execvp failed"); exit(-1);
```

如果成功，`exec()`系统调用不会返回到你的程序。操作系统会用外部程序替换任务上下文，因此你甚至不需要`if`语句；在`exec()`之后执行的任何语句都意味着它失败了。

要在套接字服务器中使用此系统调用，请用以下内容替换主要的客户端等待循环：

```c
/*----------------------------------------------------*/
/* Code fragment for accepting client connections and */
/* calling an external program ("ls -al /etc"). */
/*----------------------------------------------------*/
...
while (1)
{
    int client, addr_size = sizeof(addr);
    client = accept(sd, &addr, &addr_size);
    printf("Connected: %s:%d\n", inet_ntoa(addr.sin_addr),
           tohs(addr.sin_port));

    if ( fork() )
        close(client);
    else
    {
        close(sd); /* Client doesn’t need access to the socket */
        dup2(client, 0); /* Replace stdin */
        dup2(client, 1); /* Replace stdout */
        dup2(client, 2); /* Replace stderr */
        execl("/bin/ls", "/bin/ls", "-al", "/etc", 0);
        perror("Exec failed!"); /* something went awry */
    }
}
...
```

请参阅网站上的`ls-server.c`以获取完整列表。

### `fork()`与`vfork()`之间的区别

在其他 UNIX 版本中，你可能希望使用`vfork()`系统调用。由于进程不共享其数据，子进程必须获取父进程数据空间的快照。如果你只是在`fork()`之后调用`exec()`，那么这种复制是时间和空间的浪费。为了解决这个问题，一些 UNIX 版本引入了`vfork()`系统调用以抑制复制。然而，Linux 使用写时复制程序（只有当子进程或父进程修改页面时才复制父进程的页面）。`exec`-子进程不会修改数据页面，因此系统不会复制任何数据页面。因此，Linux 不需要`vfork()`系统调用。它将`vfork()`系统调用映射到了`fork()`。

正常父子进程创建之间的两个主要区别是 I/O 重定向和`exec*()`调用。你需要重定向所有标准通道，包括`stderr`，以便为外部程序提供其正确工作所需的所有 I/O。

你可以在线程和进程中使用`exec()`系统调用。随着可用工具的增加，这变得非常有用。线程有一个注意事项；由于它们无法在不影响任何同级线程 I/O 的情况下重定向标准 I/O，因此调用`exec()`的线程与同级线程共享相同的 I/O。

### 在线程中使用`exec()`调用

这里有一个有趣的问题：如果线程调用`exec()`会发生什么？外部程序无法替换调用者而不影响同级线程。Linux 内核采用的策略是调用不共享数据，但现有的文件通道保持共享。因此，当外部程序终止时，它会关闭`stdin`和`stdout`文件句柄。这会影响同级线程。建议：如果你想`exec()`外部程序，最好使用`fork()`代替。

## 总结：分配进程负载

多任务处理为你的程序提供了增加可访问性和灵活性所需的额外动力。你可以使用线程和进程来加速客户端并提升服务器。通过任务管理和通信，你可以简化编程并提高可靠性。

本章向你介绍了多任务处理的主题以及不同类型的任务——进程和线程。你还学习了如何使用像 Pthreads 或`fork()`这样的高级工具，或像`__clone()`这样的低级工具来创建它们。

创建任务后，你可以使用同步来控制线程交互。同步进一步帮助你串行化（或协调）对争用数据的访问。串行化确保数据完整性。

每个任务都可以通过管道或其他 I/O 以及信号来接收消息，以处理异步事件。管道允许你将信息定向到子进程，从而为父进程卸载任务。它们还允许你重定向标准 I/O 以简化交互。信号捕获事件，有助于使你的程序更加健壮。

下一章扩展 I/O 的概念，并提供多任务处理的替代方案。

# 第 8 章. 选择何时等待 I/O

### 本章内容

- I/O 阻塞：为什么？
- 何时阻塞？
- I/O 阻塞的替代方案
- 比较不同的 I/O 编程交互
- 轮询 I/O
- 异步 I/O
