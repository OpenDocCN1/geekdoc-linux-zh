
### 步骤 2：可执行程序的名称

可执行程序的名称为`webserver2`，包含它及关联代码（如`index.html`文件等）的目录为`/home/bob/webserver2`。

### 步骤 3：创建服务文件

你用文本编辑器创建的文件应命名为`webserver2.service`并保存在`/etc/systemd/system`。`[Service]`下的`ExecStart=`指令应该是：

```
ExecStart=/home/bob/webserver2 8081 /home/bob/webserver2
```

### 步骤 4：使用命令管理服务的生命周期

使用以下命令启动服务：

```
$ systemctl start webserver2.service
```

使用以下命令查看服务状态：

```
$ systemctl status webserver2.service
```

使用以下命令停止服务：

```
$ systemctl stop webserver2.service
```

### 步骤 5：配置服务的开机自启属性

为了确保服务在系统每次后续重启后自动启动，请使用以下命令：

```
$ systemctl enable webserver2.service
```

防止服务在系统每次后续重启后启动，请使用以下命令：

```
$ systemctl disable webserver2.service
```

### 步骤 6：连接服务器并查看 Web 页面

要连接到服务器并查看你放在`/home/bob/webserver2`中的 Web 页面，请将浏览器指向启动服务的 IP 地址、端口和文件位置：

```
192.168.0.6:8080/home/bob/webserver2/index.html
```

## 练习 18.18

是否可以多次运行你在`18.5.2`节中编译并执行的`webserver2`，使其每个实例都监听 Linux 系统上的不同端口？是否可以在你的 Linux 系统上从这些多个基于`webserver2`的`systemd`服务中运行不同的 Web 页面，每个服务监听不同的端口并提供不同的 Web 页面？请描述这些场景各自的工作原理。将其与书籍网站`W21`章节中所示的文件锁守护进程进行比较。

## 总结

本章为普通用户结合了`systemd`的基础参考和教程。从这个角度来看，我们说明了`systemd`是如何从上而下构建的。我们定义了基础的单元（`unit`）和目标（`target`）。然后，我们通过许多示例引入了最重要的命令`systemctl`。最后，我们提供了应用这些命令的扩展和典型用例。我们使用一个基础 Web 服务器作为`systemd`管理服务的示例。我们使用许多基于文本的命令涵盖了以下`systemd`主题：

- 系统启动、初始化和关机
- 单元和单元文件，重点介绍服务单元文件
- 目标单元文件及其用途和用法
- 系统服务管理基础和`systemctl`命令
- 其他重要的用户命令，例如`journalctl`命令
- 从零开始创建、添加和控制新的`systemd`服务

此外，我们将`systemd`定义为结合了 Linux 初始化程序和服务的管理器，它还包含并实现了许多其他重要的系统控制程序和工具。

我们建议系统不仅是一个初始化程序和服务管理器，而且是一个“超级内核”，它将 Linux 内核本身作为子程序。Linux 内核在特定的抽象层上，为`systemd`维护计算机硬件和软件组件的稳定状态。扩展`systemd`抽象则监控内核为优化稳定状态下的运行所做的一切，无论是启动、进程控制和`IPC`、硬件服务、网络操作、关机以及许多其他设施。

我们通过一些扩展示例展示了普通用户如何添加和控制新的`systemd`服务，以此结束本章。

## 问题与思考

1. 请尽可能完整回答以下问题：
    a. `systemd`单元是一个单元，还是它可以是一个目标？
    b. `systemd`目标是一个目标，还是它可以是一个单元？
    
    这个问题旨在让你思考图`18.1`所示的`systemd`概念组织，以及单元和目标的细节。

2. 如何验证你的系统启动时达到了图`18.2`所示的里程碑，顺序为`local-fs-target`、`sysinit.target`、`basic.target`、`multi-user-target`和`graphical.target`？这里的假设是你正进入 Linux 桌面环境，但你也可以基于使用`CLI`纯文本`systemd`命令集进行验证。

3. 使用什么`systemctl`命令可以将你的 Linux 系统从最终目标状态`graphical.target`切换到`multi-user.target`，并将最终状态改回`graphical.target`？在你的 Linux 系统上测试这些操作。

4. 取一个对你有用的`Bash`脚本文件，将其转换为由`systemd`控制的服务，该服务在适当的时间间隔执行。将脚本文件放置在系统的家目录中并设置权限。使用适当的`systemctl`命令启动、停止、重启和编辑服务的操作。

5. 在检查了`18.5`节中提供的守护进程示例的命令和执行逻辑后，与书籍网站`W21`章节第`13`节中名为`test_server`的`C`代码中创建守护进程的系统调用进行比较（总结在图`W21.3`中）。你发现了什么？`W21`章节`test_server`中的哪些系统调用未出现在示例中，反之亦然？

6. 修改`18.5`节中提供的守护进程`server2`示例，使用`sd_journal-send` `systemd`函数向日志写入你可能需要的其他感兴趣的字段。

7. 对比`/var/log`中的信息和日志与`journal`的内容（排除存在的`/var/log`目录）。准备一份报告，说明你注意到的显著相似之处，特别是在日志的搜索和保留方面。

8. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术对示例`webserver2`程序进行你任意的修改。

9. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

10. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

11. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

12. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

13. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

14. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

15. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

16. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

17. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

18. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

19. 在你的 Linux 系统上从本书的`GitHub`下载、编译并执行`webserver2`程序代码。然后，使用示例`webserver2`程序中的技术，对示例`webserver2`程序进行你任意的修改。

### 第 1 部分

编写一个对你有用的`Bash`脚本文件，将其转换为由`systemd`控制的服务，该服务在适当的时间间隔执行。将脚本文件放置在系统的家目录中并设置权限。使用适当的`systemctl`命令启动、停止、重启和编辑服务的操作。

### 第 2 部分
