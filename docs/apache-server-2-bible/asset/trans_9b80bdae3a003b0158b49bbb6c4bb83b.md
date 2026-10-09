

默认行为（`all`）要求客户端通过地址访问限制，并输入有效的用户名和密码。使用 `any` 选项时，如果用户通过主机限制或输入有效的用户名和密码中的任意一项，客户端即被授予访问权限。此指令可用于通过使用密码来限制对某个区域的访问，同时允许来自特定 IP 地址池（即一组 IP 地址）的所有客户端在无需输入密码的情况下获得访问权限。

### ScriptInterpreterSource

`ScriptInterpreterSource` 指令允许你指定 Windows 如何查找脚本的解释器。通常，脚本解释器是通过脚本中找到的 `#!` 行来检测的。然而，将此指令设置为 `registry` 将强制 Windows 在注册表中查找脚本扩展名以找到其关联程序（即解释器）。

- 语法：`ScriptInterpreterSource Registry | Script`
- 默认设置：`ScriptInterpreterSource script`
- 上下文：目录，.htaccess

### MPM threaded 特定指令

这类似于 prefork MPM，但每个子进程不再只有一个线程，而是允许每个子进程拥有一定数量的线程。由于线程比进程更具资源效率，因此这种 MPM 非常易于扩展。子进程内的每个线程可以处理不同的请求。

通过监控其空闲线程数量来添加或删除进程。例如，如果一个进程的空闲线程少于最小数量，则会添加一个新进程。同样，当一个进程拥有最大数量的空闲线程时，它会被终止。

> 所有进程都在分配给 Apache 服务器的同一用户和组 ID 下运行。

### CoreDumpDirectory

`CoreDumpDirectory` 指令设置 Apache 在崩溃并转储核心文件（即服务器的内存映像）之前尝试切换到的目录。默认位置是由 `ServerRoot` 指令指定的目录。

- 语法：`CoreDumpDirectory directory_path`
- 默认设置：服务器根目录
- 上下文：服务器配置

### Group

**Group** 指令应与 *User* 指令配合使用。**Group** 确定独立服务器处理请求所在的组。若要使用此指令，独立服务器最初必须以 root 身份运行。**Group** 指令也可以被分配一个组号。**Group** 在你的 */etc/group* 文件中查找组名称及其对应的数值。

- 语法：`Group Unix-group`
- 默认设置：`Group #=-1`
- 上下文：服务器配置，虚拟主机

![](img/e11fcbd2818a3495ac70085e5d8d1c26_123_0.png)

我稍后提供的关于 *User* 指令的所有警告和建议也适用于此指令。请确保阅读本章稍后关于 *User* 指令的详细信息。

### Listen

默认情况下，Apache 响应附加到服务器机器的所有 IP 地址上的请求，但仅响应由 *Port* 指令指定的端口地址。*Listen* 指令可用于使这种情况更具可配置性。你可以使用 *Listen* 指令告诉 Apache 响应特定的 IP 地址、IP 地址和端口组合，或仅响应端口本身。

- 语法：`Listen [IP address:] port_number`
- 默认设置：无
- 上下文：服务器配置

虽然 *Listen* 可以代替 *BindAddress* 和 *Port* 使用，但如果你的 Apache 服务器生成指向自身的 URL，你可能仍需要使用 *Port* 指令。

可以使用多个 *Listen* 指令来指定要监听的多个地址和端口。服务器将响应来自列出的任何地址和端口的请求。例如，要使服务器接受端口 80 和端口 8080 上的连接，请使用：

```
Listen 80
Listen 8080
```

以下示例使 Apache 接受两个 IP 地址和端口号上的连接：

```
Listen 192.168.1.100:80
Listen 192.168.1.101:8080
```

### ListenBacklog

`ListenBacklog` 指令通过允许你设置待处理连接队列的最大长度，使你可以针对一种名为拒绝服务（DoS）的已知安全攻击采取防御措施。如果你检测到正在遭受 TCP SYN 泛洪（DoS）攻击，请增加此值；否则，你可以保持默认值不变。

- **语法：** `ListenBacklog backlog`
- **默认设置：** `ListenBacklog 511`
- **上下文：** 服务器配置

### LockFile

如果 Apache 是使用 `USE_FCNRL_SERIALIZED_ACCEPT` 或 `USE_FLOCK_SERIALIZED_ACCEPT` 选项编译的，则使用锁文件。你可以使用 `LockFile` 指令设置锁文件文件名的路径。请确保只有 Apache 服务器具有该文件的读写访问权限。

- **语法：** `LockFile filename`
- **默认设置：** `LockFile logs/accept.lock`
- **上下文：** 服务器配置

> 将锁文件存储在通过网络文件系统（NFS）挂载的分区上不是一个好主意，因为 NFS 在文件锁定和安全性方面众所周知存在问题。

### MaxClients

`MaxClients` 指令限制 Apache 可以同时处理的请求数量。由于 Apache 为每个请求使用一个子服务器，因此这也是可以同时存在的子服务器的有效限制。

- **语法：** `MaxClients number`
- **默认设置：** `MaxClients 256`
- **上下文：** 服务器配置

默认限制实际上是 Apache 源代码发行版中 `httpd.h` 文件中设置的硬性限制。对于大多数中等负荷的网站，此设置应该足够了。Apache 程序员在那里设置硬性限制有两个原因：他们不希望服务器通过填满某些内核表而使系统崩溃，并且这个最大限制使记分板文件足够小，以便轻松读取。当服务器达到最大请求数时，它会进入等待状态，直到可以处理这些传入请求为止。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_125_0.png)

如果你拥有高性能服务器系统并具备必要的带宽，你可以通过修改适当的 MPM 头文件（`mpm_defaults.h`）来重新编译服务器，以提高硬性限制。参见第 2 章中的表 2-3。

### MaxRequestsPerChild

Apache 启动一个子服务器进程来服务请求；然而，子服务器可以处理多个请求。子服务器可以处理的请求数量由 `MaxRequestsPerChild` 指令限制。

- **语法：** `MaxRequestsPerChild number`
- **默认设置：** `MaxRequestsPerChild 0`
- **上下文：** 服务器配置

在提供最大数量的请求服务后，子进程将终止。如果 `MaxRequestsPerChild` 为 0，则该进程永远不会过期。如果你怀疑操作系统（例如，Solaris）上存在一些库包含内存泄漏代码，你可能希望将此指令设置为非零值。这使你可以为子进程定义一个生命周期，从而减少进程消耗泄漏内存并缓慢耗尽所有可用内存的可能性。它还为你的系统提供了较小的平均负载数，因为随着 Web 服务器变得不太繁忙，与 Apache 相关的负载会减少。

### MaxSpareThreads

`MaxSpareThreads` 指令设置空闲线程的最大数量。线程化 MPM 在服务器范围内处理空闲线程，这意味着如果服务器中有太多空闲线程，它会开始终止子进程，直到空闲线程数量减少到此处指定的数量为止。

- **语法：** `MaxSpareThreads number`
- **默认设置：** `MaxSpareThreads 10`（对于 Perchild MPM）或 `500`（对于线程化 MPM）
- **上下文：** 服务器配置

perchild MPM 按每个子进程计算空闲线程，这意味着如果某个子进程中有太多空闲线程，线程将被销毁，直到每个子进程的线程数小于由 `MaxSpareThreads` 指令指定的数量为止。

### MinSpareThreads

`MinSpareThreads` 指令设置空闲线程的最小数量。线程化 MPM 在服务器范围内处理空闲线程，这意味着当空闲线程少于此处指定的数量时，Apache 会创建新的子进程，使总线程数至少达到这个数量。

