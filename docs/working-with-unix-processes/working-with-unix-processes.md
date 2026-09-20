# Unix 进程实战










# 致谢

非常感谢几位读过书籍初稿的优秀朋友们，他们帮助我理解如何营销这部作品，在我需要的时候推了我一把，并且在过程中给予了极大的帮助：Sam Storry, Jesse Kaunisviita 和 Marc-André Cournoyer。

我必须向我的妻子和女儿表达深深的谢意，她们不仅支持了让这本书成为可能的不规律日程，而且总是在那里提供第二意见。没有你们的爱和支持，我无法完成这一切。你们让一切变得值得。







# 第2章

## 导论

本节将提供书中用到的一些关键概念的背景知识。强烈建议你在进入更具实质内容的章节之前阅读这一部分。

## 为什么要关注？

Unix 编程模型自1970年以来一直以某种形式存在。那时，Unix 在贝尔实验室被著名发明，同时也诞生了C语言语言或框架。在 Unix 诞生后的几十年里，它因可靠性、安全性和稳定性一直是人们首选的操作系统。

Unix 编程概念和技术并非一时之风，它们不是最新的流行编程语言。这些技术超越了编程语言。无论你是使用 C、C++、Python、JavaScript、Haskell 还是[在此处插入你喜欢的语言]进行编程，这些技术都非常有用。

这些内容已经存在了几十年，几乎没有变化。在过去的 40 年里，聪明的程序员一直在使用 Unix 编程通过多种编程语言解决棘手问题，在未来的 40 年里他们将继续这样做。

## 掌握力量！

我现在就要警告你，书中描述的概念和技术可以带给你巨大的力量。拥有了这种力量，你可以创建新的软件，理解已经存在的复杂软件，甚至利用这些知识将你的职业提升到新水平。

只需记住，能力越大，责任越大。继续读下去，我会告诉你获得力量并避开陷阱所需要的所有知识。

## 概述

本书并不是为了作为参考手册来阅读的。它更像是一份指南。为了获得最大的收益，你应该按顺序阅读，因为每一章都建立在前章的基础上。一旦你完成，如果需要复习，可以使用章节标题查找信息。

本书包含了许多代码示例。我强烈建议你通过亲自在 Ruby 解释器中实际运行它们来跟随学习。亲自操作代码并进行微调将有助于加深对概念的理解。

一旦读完本书并运行了示例，我确定你将会想要尝试一个更深入的真实世界项目。到那时，请查看附带的 Spyglass 项目。

Spyglass 是专门为本书创建的一个 Web 服务器。它的设计目的是教授 Unix 编程概念。它将你在这里学到的概念展示了真实世界项目是如何使用它们的。查看本书的最后一章以获得更深入的介绍。

## 系统调用

理解系统调用首先需要对 Unix 系统的组件进行快速解释，特别是用户态（userland）与内核（kernel）。

你 Unix 系统的内核位于计算机的硬件之上。它是任何需要与硬件进行交互的中间人。这包括从文件系统读/写、通过网络发送数据、分配内存或通过扬声器播放音频等。由于其强大性，程序不允许直接访问内核。任何通信都是通过系统调用完成。

系统调用接口连接了内核和用户态。它定义了程序与计算机硬件之间允许的交互。

用户态是你所有程序运行的地方。在用户态程序中，你可以做很多事情而无需使用任何系统调用：进行数学运算、字符串操作、使用逻辑语句控制流。但我甚至可以说，如果你想让你的程序做任何有趣的事情，你就需要通过系统调用涉及内核。

如果你是一个 C 语言程序员，这些内容对你来说可能是本常的。系统调用是 C 编程的核心。

但我预计你和我一样，没有任何 C 语言编程经验。你是在高级语言中学习编程的。当你学习如何向文件系统写入数据时，并没有告诉你是哪些系统调用实现了这一点。

这里的结论是，系统调用允许你的用户空间程序通过内核间接与你的计算机硬件进行交互。在学习这些章节的过程中，我们将查看常见的系统调用。

## 术语，wtf(2)

学习 Unix 编程的障碍之一在于哪里找到正确的文档。想听听惊喜吗？所有内容都可以 Unix 手动页（manpages）获取，如果你现在正在使用基于 Unix 的计算机，它已经在你的计算机上了了！

如果你以前从未用过 manpages，可以从在终端调用 `man man` 命令开始。

完美，对吧？好吧，差不多吧。系统调用 API 的 manpages 在两种情况下是极好的资源：

- 你是一个想要如何调用给定系统调用的 C 语言程序员，或
- 你正在寻找给定系统调用的目的

我假设我们在这里不是 C 语言程序员，所以 #1 没用，但 #2 非常有用。

你将在本文中看到类似这样的引用：`select(2)`。这段文字告诉你你可以在哪里找到给定系统调用的 manpage。你可能知道或不知道，但 Unix 手动页有很多章节。

以下是 FreeBSD 和 Linux 系统 manpages 最常用的章节：

- 第 1 节：通用命令
- 第 2 节：系统调用
- 第 3 节：C 库函数
- 第 4 节：特殊文件

因此，第 1 节用于通用命令（又称 shell 命令）。如果我想让你参考 `find` 命令的手动页，我会这样写：`find(1)`。这告诉你在 manpages 的第 1 节中有 `find` 的手动页。

如果我想引用 `getpid` 系统调用的手动页，我会这样写：`getpid(2)`。这告诉你在 manpages 的第 2 节中有 `getpid` 的手动页。

> 为什么 manpages 需要多个章节？因为一个命令可能出现在多个章节，即既可以是 shell 命令也可以是系统调用。

以 `stat(1)` 和 `stat(2)` 为例。为了访问 manpages 的其他章节，你可以在命令行这样指定：

```
$ man 2 getpid
$ man 3 malloc
$ man 1 find
```

这种术语不是为本书发明的，它是引用 manpages 时通用的惯例¹。所以现在学习它并习惯它是好主意。

# 第3章
## 进程拥有 ID

运行在你的系统上的每个进程都有一个唯一的进程标识符，此处称为 pid。

pid 并没有关于进程本身的任何信息，它仅仅是一个顺序数字标签。这就是内核看待你的进程的方式：作为一个数字。

这里是我们在 Ruby 程序中检查当前 pid 的。启动 irb 并尝试这个：

```ruby
# 这一行将打印当前 ruby 进程的 pid。这可能是一个
# irb 进程、一个 rake 进程、一个 rails 服务器，或一个普通的 ruby 脚本。
puts Process.pid
```

pid 是进程的一种简单、通用的表示。由于它与进程内容的任何方面无关，因此可以从任何编程语言并使用简单工具来理解。我们将在下面看到如何使用 pid 跟踪进程详情。

## 交叉引用

为了获得全景，我们可以使用 ps(1) 将我们的 pid 与内核看到的进行交叉引用。保持你的 irb 会话开启，在终端运行以下命令：



```
$ ps -p <pid-of-irb-process>
```

该命令应该显示一个名为 'irb' 的进程，其 pid 与 irb 会话中打印的 pid 匹配。

## 现实世界

仅仅知道 pid 本身并没有什么用。那么它在什么使用呢？

在现实世界中，发现 pid 的常见地方是日志文件。当你有多个进程记录到同一个文件时，必须能够区分出哪行日志来自哪个进程。在每行中包含 pid 就能解决这个问题。

包含 pid 还允许你通过使用 `top(1)` 或 `lsof(1)` 等命令与操作系统进行信息交叉比对。以下是 Spyglass 服务器启动的一些示例输出。每行的第一个方括号表示该日志行所在进程的 pid。

```
[58550] [Spyglass::Server] Listening on port 4545
[58550] [Spyglass::Lookout] Received incoming connection
[58557] [Spyglass::Master] Loaded the app
[58557] [Spyglass::Master] Spawned 4 workers. Babysitting now...
[58558] [Spyglass::Worker] Received connection
```

## 系统调用

Ruby 的 `Process.pid` 映射到 `getpid(2)`。

还有一个全局变量 `$$` 持有当前 pid 的值。Ruby 从其他语言那里继承了这种行为（perl 和 bash 都支持 `$$`），不过输入 `Process.pid` 比 `$$` 更明确意图，不容易让没见过 `$$` 的人感到困惑。

## 进程拥有父进程

系统中运行的每个进程都有一个父进程。每个进程都知道其父进程标识符（此处称为 'ppid'）。

大多数情况下，给定进程的父进程是调用它的进程。例如，如果你是一个启动了 Terminal.app 并进入终端提示符的用户，那么终端提示符的父进程就是 Terminal.app。如果你接着从终端提示符调用 `ls(1)`，那么 `ls` 进程的父进程将是终端提示符。由于内核只处理 pid，这里有一种获取当前 pid 的方法。在 Ruby 中这样做：

```ruby
## 注意获取当前 pid
puts Process.ppid
```

## 交叉引用

在终端提示符中运行以下命令：

```bash
$ ps -p <pid-of-irb-process>
```

该命令应该显示一个名为 'bash' 的进程，其 pid 与 irb 会话中打印的 pid 匹配。

## 现实世界

在现实世界中，ppid 有很多用途。在检测守护进程时，它可以很重要，这一点将在后面的章节中介绍。

## 系统调用

Ruby 的 `Process.ppid` 映射到 `getppid(2)`。

# 第 5 章

进程拥有文件描述符

与 pid 代表进程的方式一样，文件描述符代表打开的文件。

## 一切皆文件

Unix 哲学的一部分是：“一切皆文件”。这意味着设备被视为文件，套接字和管道被视为文件，文件也被视为文件。当我从泛义上谈论文件时，我会使用 'resource' 这个词（包括设备、管道、套接字等），而当我指代经典定义的文件时，我会使用 'file' 这个词（文件系统上的文件）。

## 描述符表示资源

每当运行进程打开一个资源时，它会被分配一个文件描述符数字。文件描述符在不相关的进程之间是不共享的，它们随着它们绑定的进程而生灭，正当进程退出时，任何打开的资源都会关闭。文件描述符共享有特殊的语义，稍后会介绍。

在 Ruby 中，打开的资源由 IO 类表示。任何 IO 对象都可以有一个关联的文件描述符数字。使用 IO#fileno 来访问它。

```ruby
passwd = File.open('/etc/passwd')
puts passwd.fileno
```

输出：

```
3
```

进程打开的任何资源都有一个标识它的唯一数字。这就是内核跟踪进程使用的任何资源的方式。

当我们打开多个资源会发生什么？

```ruby
passwd = File.open('/etc/passwd')
puts passwd.fileno

hosts = File.open('/etc/hosts')
puts hosts.fileno

## 关闭 passwd 文件。释放其文件描述符供下一个打开的资源使用。
passwd.close

null = File.open('/dev/null')
puts null.fileno
```

输出：

```
3
4
3
```

这个示例有两个关键收获：

- 文件描述符数字被分配为最小未使用的值。我们打开的第一个文件 `passwd` 得到了 3。
- 一旦关闭资源，其文件描述符就会再次可用。文件描述符有特殊的语义，尝试读取关闭的流将抛出异常。

```ruby
passwd = File.open('/etc/passwd')
puts passwd.fileno
passwd.close
puts passwd.fileno
```

输出：

```
3
IOError: closed stream (3)
```

## 标准流

每个 Unix 进程带有三个打开的资源。这些是标准输入 (STDIN)、标准输出 (STDOUT) 和标准错误 (STDERR)。

这些标准资源存在有一个我们理所当然的重要原因。STDIN 提供了一种从键盘设备或管道读取输入的通用方法，STDOUT 和 STDERR 提供了向显示器等输出内容的通用方法。这是 Unix 的创新之一。在 STDIN 存在之前，你的程序必须包含想要支持的所有键盘的键盘驱动程序。

```ruby
puts STDIN.fileno
puts STDOUT.fileno
puts STDERR.fileno
```

输出：

```
0
1
2
```

那前 3 个文件描述符数字就是去了那里。

## 现实世界

文件描述符是使用套接字等的网络编程的核心，也是任何文件系统操作的核心。因此，它们被每个运行的进程使用，并且是你使用计算机可以做的大部分有趣事情的核心。你将在后续章节或附带的 Spyglass 项目中看到更多使用它们的示例。

## 系统调用

IO 类上的许多方法映射到同名的系统调用。这些包括 open(2)、close(2)、read(2)、write(2)、pipe(2)、fsync(2)、stat(2) 等。

# 第 6 章
进程资源限制

在上一节中，我们查看了打开资源由文件描述符表示的事实。你可能注意到当资源不被关闭时，文件描述符数字会继续增加。这引发了一个问题：一个进程可以有多少个文件描述符？

答案取决于你的系统配置，但重点是内核对进程施加了一些资源限制。

## 查找限制

我们将继续讨论文件描述符。使用 Ruby 我们可以直接查询允许的文件描述符数量：

```ruby
Process.getrlimit(:NOFILE)
```

在我的机器上，这段代码片段输出：

```
[2560, 9223372036854775807]
```





我们使用了名为 `Process.getrlimit` 的方法，并通过符号 `:NOFILE` 请求最大打开文件数。它返回了一个包含两个元素的数组（Array）。

数组中的第一个元素是文件描述符数量的*软限制*（soft limit），数组中的第二个元素是文件描述符数量的*硬限制*（hard limit）。

## 软限制 vs 硬限制

它们之间有什么区别？很高兴你问了这个问题。*软限制并不是真正的限制*。这意味着，如果你超过了软限制（在本例中，是一次性打开了超过 2560 个资源），系统*会抛出*异常，但如果你愿意，你可以随时更改它。

> 注意，我系统中文件描述符数量的硬限制是一个大得离谱的整数。打开这么多资源是可能的吗？可能不会，我确信在一次性打开这么多资源之前，你就会遇到硬件限制。

> 在我的系统上，那个数字实际上代表了无穷大。它体现在常量 `Process::RLIMIT_INFINITY` 中。你可以尝试比较这两个值以确认。因此，在我的系统上，一旦我根据需要调高软限制，我就可以实际上打开我所需要的任何资源。

因此，任何进程都能更改其软限制，但硬限制呢？通常这只能由超级用户完成。然而，只要你的进程拥有所需的权限，它也可以调高硬限制。如果你对在系统级更改限制感兴趣，可以先从查看 sysctl(8) 开始。

## 调高软限制

让我们调高当前进程的软限制：

```
Process.setrlimit(:NOFILE, 4096)
p Process.getrlimit(:NOFILE)
```

输出为：

```
[4096, 4096]
```

我们可以看到，我们为打开的文件数设置了新限制，并且在再次请求该限制时，硬限制和软限制都被设置为了新值 4096。

我们可以选择性向 `Process.setrlimit` 传递第三个参数，以指定一个新的硬限制，前提是我们有权限这样做。请注意，降低硬限制（正如我们在上一个代码段中所做的样）是不可逆的：一旦它下降，就无法回升。

以下示例是将系统资源的软限制提高到与硬限制（即最大允许值）相等的常用方法。

```
Process.setrlimit(:NOFILE, Process.getrlimit(:NOFILE)[1])
```

## 超过限制

注意，超过软限制将抛出 `Errno::EMFILE` 异常：

```
# 将最大打开文件数设置为3。我们知道这
# 将达到上限，因为标准流占用了
# 前三个文件描述符。
Process.setrlimit(:NOFILE, 3)

File.open('/dev/null')
```

输出为：

```
Errno::EMFILE: Too many open files - /dev/null
```

## 其他资源

你可以使用相同的方法来检查和修改其他系统资源的限制。一些常见的资源包括：

```ruby
# 当前用户允许的# 最大并发进程数。
Process.getrlimit(:NPROC)

# 可以创建的最大文件大小。
Process.getrlimit(:FSSIZE)

## 进程栈段的最大大小。
Process.getrlimit(:STACK)
```

请查看 `Process.getrlimit` 的文档以获取可用选项的列表。

## 在现实世界中

对于大多数程序来说，修改系统资源限制并不是一个常见的需求。然而，对于某些特殊工具，这可能非常重要。

一个用例是任何需要处理成千上万并发网络连接的进程。例如 `httpperf(1)` HTTP 性能工具。类似 `httpperf --hog --server --num-conn 5000` 的命令会要求 `httpperf(1)` 创建 5000 个并发连接。显然，这在我系统中会由于软限制而产生问题，因此 `httpperf(1)` 在正确进行测试之前需要调高其软限制。

限制系统资源的另一个现实世界用例是你执行第三方代码时且...



[content]

# 第 9 章

## 进程具有名称

Unix 进程通信其状态的固有方式非常少。

程序员们一直在回避这个问题，并发明了日志文件（logfiles）等工具。日志文件允许进程通过写入文件系统来通信关于状态的任何信息，但这种操作是在文件系统层面的，而不是进程固有的。

同样，进程可以使用网络打开 socket 并与其他进程进行通信。但同样，这在与进程本身不同的层面运行，因为它依赖于网络。

有两种机制可以在进程本身层级运行并用于通信信息。其中一个是进程名称，另一个是退出状态码（exit codes）。

## 命名进程

系统上的每个进程都有一个名称。例如，当你启动一个 irb 会话时，该进程被命名为 'irb'。进程名称的妙之处在于，它们可以在运行时更改，并作为一种通信手段。

在 Ruby 中，你可以通过 `$PROGRAM_NAME` 变量访问当前进程的名称。同样，你也可以给该全局变量赋值来更改当前进程的名称。

作为一个有趣的练习，你可以启动一个 irb 会话，打印 pid，并更改名称。然后你可以使用 `ps` 工具查看系统上反映的更改。遗憾的是，这个全局变量（及其默认值 0）是 Ruby 为此功能提供的唯一机制。没有其他方法可以更改当前进程的名称。

```ruby
10.downto(1) do |num|
  $PROGRAM_NAME = "Process: #{num}"
  puts $PROGRAM_NAME
end
```

输出：

```
Process: 10
Process: 9
Process: 8
Process: 7
Process: 6
Process: 5
Process: 4
Process: 3
Process: 2
Process: 1
```

## 在现实世界中

要查看在实际项目中如何使用此点的示例，请阅读附录中的《进程如何管理》。

# 第 10 章

## 进程具有退出状态码

当一个进程结束时，它有最后一个机会在世界上留下印记：那就是它的退出状态码。每个进程退出时的代码（0-255）表示它是成功退出还是带错误退出。传统上，退出状态码为 0 的进程被认为是成功的。任何其他退出状态码都表示错误。尽管传统上它们被用来表示错误，但它们实际上只是一个通信通道。你需要做的就是处理退出状态码，以便你的程序能与 Unix 工具良好地协作。

## 如何退出进程

在 Ruby 中有几种退出进程的方法，每种都有不同的目的。

退出进程简单的方法是使用 `Kernel#exit`。当你的脚本在没有显式退出语句的情况下结束时，也会发生这种情况。

```ruby
# 这将以成功状态 (0) 退出程序。
exit
```

```ruby
# 你可以向此方法传递一个自定义的退出状态码
exit 2
```

```ruby
## 当调用 Kernel#exit 时，在退出之前 Ruby 会调用任何由 at_exit 定义的块
at_exit { puts 'Last!' }
exit
```

将输出：

```
Last!
```

exit!

Kernel#exit! 与 Kernel#exit 几乎完全相同，但有两个关键区别。第一个是它默认设置一个不失败的状态码（1），第二个是它不会调用任何使用 at_exit 定义的块。

```ruby
# 这将以状态码 1 退出程序。
exit!
```

```ruby
# 你仍然可以传递一个退出状态码。
exit! 3
```

```ruby
## 这个块将永远不会被调用。
at_exit { puts 'Silence!' }
exit!
```

abort

Kernel#abort 提供了一种不失败退出进程的通用方法。Kernel#abort 会将当前进程的退出状态码设置为 1。

```ruby
# 将以状态码 1 退出。
abort
```

```ruby
# 你可以向 Kernel#abort 传递消息。此消息将在进程退出前打印到 STDERR。
abort "Something went horribly wrong."
```

```ruby
## 使用 Kernel#abort 时会调用 Kernel#at_exit 块。
at_exit { puts 'Last!' }
abort "Something went horribly wrong."
```

将输出：

## raise

结束进程的另一种方法是使用未处理的异常。这是你永远不希望在生产环境中发生的，但在开发和测试环境中几乎总是发生的。

注意，Kernel#raise 与之前的方法不同，它不会立即退出进程。它只是抛出一个异常，该异常可能会在栈上被捕获。如果异常在代码库的任何地方都没有被捕获，那么未处理的异常将导致进程退出。这种方式结束进程仍然会调用任何 at_exit 处理器，并将异常消息和回溯跟踪打印到 STDERR。

```ruby
## 与 abort 类似，未处理的异常会将退出状态码设置为 1。
raise 'hell'
```

## 进程可以 fork

### 使用 fork(2)，Luke

Fork（分叉）是 Unix 编程中最强大的概念之一。fork(2) 系统调用允许运行中的进程程序化地创建新进程。这个新进程是原始进程的精确副本。

到为止，我们讨论的是如何通过终端启动进程来创建进程。我们还提到了创建其他进程的低级操作系统进程：fork(2) 就是它们这样做的方法。

在 forking 时，发起 fork(2) 的进程被称为“父进程”，新创建的进程被称为“子进程”。

子进程继承父进程使用的所有内存的副本，以及属于父进程的任何打开的文件描述符。让我们花一点时间从前三章的角度回顾子进程。

由于子进程是一个全新的进程，它有它自己的 pid。

子进程继承父进程使用的所有内存的副本，以及属于父进程的任何打开的文件描述符。通过这种方式，两个进程可以共享文件、socket 等。子进程继承父进程在 fork 时所拥的所有内容的副本。通过这种方式，进程可以 fork 一个大型代码库，比如一个 Rails 应用，它占用了 500MB 的内存。然后这个进程可以 fork 2 个新进程。这些子进程中的每个实际上都有它们自己的 500MB 内存。这对于当你想要加载多个应用程序实例时非常完美。因为只需要一个进程加载应用，而且 forking 是快速的，这种方法比在单独实例中加载 3 次应用要快。

子进程可以自由修改它们的内存副本而不影响父进程在内存中的内容。请看下一章关于写时复制（copy-on-write）以及它在 forking 时如何影响内存的讨论。

让我们通过一个令人头脑的示例开始在 Ruby 中学习 fork：

```ruby
if fork
  puts "entered the if block"
else
  puts "entered the else block"
end
```

输出：

```
entered the if block
entered the else block
```

WTF！这里发生了什么？fork 方法的调用将曾经熟悉的结构颠倒了。这段代码竟然同时进入了 if 结构的 if 和 else 块！

这里发生的事情并不神秘。一次 fork 方法调用实际上返回了两次。记住 fork 创建了一个新进程。因此它在调用进程（父进程）中返回一次，在新创建的进程（子进程）中返回一次。

如果我们打印出来，最后一个示例就变得更加明显了。

```ruby
puts "parent process pid is #{Process.pid}"

if fork
  puts "entered the if block from #{Process.pid}"
else
  puts "entered the else block from #{Process.pid}"

end
```

输出：

```
parent process pid is 21268
entered the if block from 21268
entered the else block from 21282
```

[/content]



现在很清楚了，`if` 块中的代码是由父进程执行的，而 `else` 块中的代码是由子进程执行的。子进程在执行完 `else` 块中的代码后会退出，而父进程将继续运行。

同样，这里有一个节奏，这与 `fork` 方法的返回值有关。**在子进程中**，`fork` 返回 `nil`。由于 `nil` 为假（falsy），它会执行 `else` 块中的代码。

**在父进程中**，`fork` 返回新创建的子进程的 pid。由于整数是真值（truthy），它会执行 `if` 块中的代码。

这个概念通过简单打印 `fork` 调用的返回值可以很好地说明。

```
puts fork
```

输出

```
21423
nil
```

在这里，我们看到了两个不同的返回值。第一个返回的值是新创建的子进程的 pid；它来自父进程。第二个返回值是子进程返回的 `nil`。

## 多核编程？

从间接的角度来说，是的。通过创建新进程，意味着你的代码能够（但不保证）分布在多个 CPU 核心上。

假设一个拥有 4 个 CPU 的系统，如果你 fork 了 4 个新进程，那么每个进程都可以由一个独立的 CPU 处理，从而提供多核并发性。

然而，无法保证事情一定会并行发生。在繁忙的系统上，你的所有 4 个进程都可能由同一个 CPU 处理。

> fork(2) 创建一个新进程，它是旧进程的副本。所以如果一个进程正在使用 500MB 的主内存，当它进行 fork 时，现在你在主内存中有了 1GB。

再这样做十次，你就会迅速耗尽主内存。这通常被称为 fork 炸弹（fork bomb）。在提高并发性之前，请确保你了解后果。

## 使用块（Block）

在上面的示例中，我们通过 `if/else` 结构演示了 `fork`。在 Ruby 代码中，带块的 `fork` 也是可能的，而且更常见。

当你向 `fork` 方法传递一个块时，该块将在新的子进程中执行，而父进程将简单地跳过它。子进程在执行完块后就会退出。它不会继续沿用与父相同的代码路径。

```
fork do
  # 此处的代码只在子进程中执行
end

  # 此处的代码只在父进程中执行。
```

## 真实世界

通过简单打印 `fork` 调用的返回值可以很好地说明这个概念。

## 系统调用

## 第 12 章

## 孤儿进程

> fork(2) 创建一个新进程，它是旧进程的副本。所以如果一个进程正在使用 500MB 的主内存，当它进行 fork 时，现在你在主内存中有了 1GB。

再这样做十次，你就会迅速耗尽主内存。这通常被称为 fork 炸弹。在提高并发性之前，请确保你了解后果。





## 第 14 章
进程可以等待

在目前为止的 `fork(2)` 示例中，我们让父进程与子进程并行运行。在某些情况下，这会导致奇怪的结果，例如当父进程在子进程之前退出时。

那种场景实际上只适用于一种用例：**触发后不管**（fire and forget）。当你希望子进程异步处理某些事务，但父进程仍有自己的工作要做时，这种方法非常有用。

```ruby
message = 'Good Morning'
recipient = 'tree@mybackyard.com'

fork do
  # 在这个刻意的示例中，父进程派生了一个子进程来负责
  # 将数据发送到统计收集器。与此同时，父进程
  # 继续执行发送实际负载的工作。

  # 父进程不想被这项任务拖慢速度，
  # 即使任务因为某种原因失败也无所谓。
  StatsCollector.record message, recipient
end

## 将消息发送给接收者
```

## 照看（Babysitting）

对于大多数涉及 `fork(2)` 的其他用例，你可能需要某种方法来监控你的子进程。在 Ruby 中，一种技术是由 `Process.wait` 提供的。让我们重写上一个章节中那个产生孤儿进程的示例，使其运行得更没有意外。

```ruby
fork do
  5.times do
    sleep 1
    puts "I am an orphan!"
  end
end

Process.wait
abort "Parent process died..."
```

这一次的输出将看起来如下：

```
I am an orphan!
I am an orphan!
I am an orphan!
I am an orphan!
I am an orphan!
Parent process died...
```

不仅如此，在所有输出打印之前，控制权都不会返回给终端。

那么 `Process.wait` 做了什么？`Process.wait` 是一个阻塞调用，指令父进程等待其任一子进程退出后再继续。

### Process.wait 和它的表兄弟

我在上一步的陈述中提到了一个关键点：`Process.wait` 会阻塞，直到任何一个子进程退出。如果你有一个父进程正在照看多个子进程，并且你正在使用 `Process.wait`，你需要知道哪一个退出了。为了这一点，你可以使用返回值。

`Process.wait` 返回退出的子进程的 pid。来看一下。

```ruby
### 我们创建了 3 个子进程。
3.times do
  fork do
    # 每个进程睡眠一个小于 5 秒的随机数。
    sleep rand(5)
  end
end
3.times do
  # 我们等待每个子进程退出，并打印返回的 pid。
  puts Process.wait
end
```

### 与 Process.wait2 通信

等一下！`Process.wait` 还有一个表兄弟叫 `Process.wait2`！

为什么名字会混淆？一旦你知道 `Process.wait` 返回 1 个值（pid），而 `Process.wait2` 返回 2 个值（pid, status），一切就说通了。

这个状态可以通过退出码作为进程之间的通信手段。在关于“退出码”的章节中，我们提到过可以使用退出码为其他进程编码信息。`Process.wait2` 让你直接访问这些信息。

从 `Process.wait2` 返回的状态是 `Process::Status` 的一个实例。它附带了许多有用信息，用于确定进程究竟是如何退出的。

```ruby
### 我们创建了 5 个子进程。
5.times do
  fork do
    # 每个进程生成一个随机数。如果是偶数，它们以
    # 111 退出码退出，否则使用 112 退出码。
    if rand(5).even?
      exit 111
    else
      exit 112
    end
  end
end
5.times do
  # 我们等待每个子进程退出。
  pid, status = Process.wait2

  # 如果子进程以 111 退出码退出
  # 我们就知道它们遇到了偶数。
  if status.exitstatus == 111
    puts "#{pid} encountered an even number!"
  else
    puts "#{pid} encountered an odd number!"
  end
end
```

无需通过文件系统或网络即可进行进程通信！

### 等待特定的子进程

等一下！`Process.wait` 的表兄弟还有两个表兄弟：`Process.waitpid` 和 `Process.waitpid2`。

你可能猜得出它们是做什么的。它们的功能与 `Process.wait` 和 `Process.wait2` 相同，区别在于，它们不是等待*任何*子进程退出，而是只等待由 pid 指定的特定子进程退出。

```ruby
favourite = fork do
  exit 77
end
middle_child = fork do
  abort "I want to be waited on!"
end
npid, status = Process.waitpid2 favourite
puts status.exitstatus
```

虽然 `Process.wait` 和 `Process.waitpid` 似乎提供了不同的行为，但不要被骗了！它们实际上是相同的别名。两者都接受相同的参数且行为相同。

你可以向 `Process.wait` 传递一个 pid 以让它等待特定的子进程，也可以将 `-1` 作为 pid 传递给 `Process.waitpid` 让它等待任何子进程。

`Process.wait` 和 `Process.waitpid2` 也是如此。

就像 `Process.pid` 与 `$$` 一样，我认为这点很重要……

### 竞态条件

当你观察这些简单示例时，你可能会开始担心竞态条件。如果父进程处理每个子进程退出的速度很慢怎么办？

## 在现实世界中

查看子进程的理念是一个常见 Unix 模式的核心。这种模式有时被称为照看进程（babysitting processes）、主/工作进程模式（master/worker）或预派生（preforking）。

这种模式的核心概念是：你有一个进程它派生了几个子进程以实现并发，并花时间照看它们：确保它们有响应，在其中任何一个进程退出时做出反应等。

例如，Unicorn Web 服务器就采用了这种模式。你告诉它你希望它启动多少个工作进程。

### 僵尸进程

在上一个章节的开始，我们看了一个示例，它使用子进程以触发后不管的方式异步处理任务。我们需要重新审视这个示例，并确保我们妥善清理该子进程，否则它会变成僵尸进程！

### 等待(wait2)的人会有好报

在上一个章节中，我展示了内核会缓存已退出的子进程的状态信息。因此，即使你在子进程退出很久之后才调用 `Process.wait`，它的状态仍然可用。我确定你已经闻到了问题所在……

内核会保留退出子进程的状态，直到父进程使用 `Process.wait` 请求该状态。如果父进程从不请求状态，内核就永远无法回收这些状态信息。创建触发后不管的子进程而不收集其状态信息是对内核资源的资源的浪费。




```ruby
message = 'Good Morning'
recipient = 'tree@mybackyard.com'

pid = fork do
# 在这个人为示例中，父进程派生了一个子进程来
# 负责将数据发送到统计收集器。同时，父进程
# 继续执行发送实际负载的工作。

# 父进程不想被这项任务拖慢速度，
# 即使由于某些原因导致失败也没有关系。
StatsCollector.record message, recipient
end
# 这一行确保了执行统计收集的进程
# 不变成僵进程。
Process.detach(pid)
```

`Process.detach` 是做什么的？它只是启动了一个新线程，该线程唯一的工作是等待指定的 `pid` 的子进程退出。这确保了内核不会挂起在我们需要的任何状态信息上。

## # 僵进程看起来是什么样的？

```ruby
## 创建一个 1 秒后退出的子进程。
pid = fork { sleep 1 }
## 打印它的 pid。
puts pid
# 让父进程无限睡眠，以便我们可以检查
# 子进程的状态。
sleep
```

在终端中运行以下命令，使用上一个代码段打印的 `pid`，将打印该僵进程的状态。状态应该显示 'z' 或 'Z+'，意味着该进程是一个僵进程。

```bash
ps -ho pid,state -p [僵进程的 pid]
```

## 在现实世界中

注意，任何没有被等待状态的死亡进程都是僵进程。因此，每个在父进程仍然活跃时死亡的子进程都会变成僵进程，即使只是很短。一旦父进程从僵进程那里收集了状态，它就会实际上消失，不再消耗内核资源。

以“发后不管”的方式派生（fork）子进程且从不收集其状态是非常少见的。如果需要在后台卸载工作，更常见的做法是使用专门的后台队列系统来完成。

尽管如此，有一个名为 `spawn`¹ 的 Rubygem 提供了完全相同。除了提供了进程或线程的通用 API 之外，它还确保了“发后不管”的进程被正确地分离（detached）。

## # 系统调用

`Process.detach` 没有系统调用，因为它在 Ruby 中简单地实现为线程和 `Process.wait`。Rubinius² 的实现极其简单。

> ¹https://github.com/tra/spawn
²https://github.com/rubinius/rubinius/blob/c6e8e33b37601d4a082dcbbd60a5867607471/kernel/common/process.rb#L377-395

## 进程可以接收信号

在最后一章中，我们看了 `Process.wait`。它为父进程监控子进程提供了一种很好的方法。然而，它是一个阻塞调用：在子进程死亡之前，它不会返回。

忙碌的父进程怎么办？并不是每个父进程都有整天等孩子的奢侈。忙碌父进程有一个解决方案！这就是我们对 Unix 信号的介绍。

## 捕获 SIGCHLD

让我们从上一章中取一个简单的示例并为忙碌的父进程重写它。

```ruby
child_processes = 3
dead_processes = 0
## 我们派生了 3 个子进程。
child_processes.times do
    fork do
        # 它们睡眠 3 秒。
        sleep 3
    end
end

## 我们的父进程将忙于进行一些复杂的数学计算。
## 但仍然想知道其中一个孩子何时退出。

# 通过捕获 :CHLD 信号，我们的进程会在其中一个孩子
# 退出时收到内核通知。
trap(:CHLD) do
    # 由于 Process.wait 会为我们排队任何数据，我们在这里
    # 请求这些数据，因为我们知道其中一个子进程已经退出了。

    puts Process.wait
    dead_processes += 1
    # 我们显式地在所有子进程都到位后退出。
    exit if dead_processes == child_processes
end

## 运行它。
loop do
    (Math.sqrt(rand(44)) ** 8).floor
    sleep 1
end
```


- 1. 在第一个 ruby 会话中执行以下代码：

```ruby
puts Process.pid
sleep # so that we have time to send it a signal
```

- 2. 在第二个 ruby 会话中发出以下命令，以通过信号杀死第一个会话：

```ruby
Process.kill(:INT, <pid of first session>)
```

因此，第二个进程向第一个进程发送了 "INT" 信号，导致其退出。"INT" 是 "INTERRUPT"中断）的缩写。

当进程接收到此信号时，系统的默认行为是它应该中断当前正在的操作并立即退出。

## 概览

下表显示了 Unix 系统上常见的支持的信号。每个 Unix 进程都能响应这些信号，并且任何信号都可以发送给任何进程。

在命名信号时，名称中的 SIG 部分是可选的。表格中的 Action（动作）列描述了每个信号的默认动作：

- Term: 意味着进程将立即终止
- Core: 意味着进程将立即终止并生成核心转储（堆栈追踪）
- Ign: 意味着进程将忽略该信号
- Stop: 意味着进程将停止（即暂停）
- Cont: 意味着进程将恢复（即取消暂停）

| Signal | Value | Action | Comment |
| --- | --- | --- | --- |
| SIGHUP | 1 | Term | 控制终端检测到挂断或控制进程死亡 |
| SIGINT | 2 | Term | 键盘中断 |
| SIGQUIT | 3 | Core | 键盘退出 |
| SIGILL | 4 | Core | 非法指令 |
| SIGABRT | 6 | Core | 终止信号(3) |
| SIGFPE | 8 | Core | 浮点数异常 |
| SIGKILL | 9 | Term | 杀死信号 |
| SIGSEV | 11 | Core | 无效内存引用 |
| SIGPIPE | 13 | Term | 管道破：向没有读者的管道写入 |
| SIGALRM | 14 | Term | 来自 alarm(2) 的定时器信号 |
| SIGTERM | 15 | Term | 终止信号 |
| SIGUSR1 | 30,10,16 | Term | 用户自定义信号 1 |
| SIGUSR2 | 31,12,17 | Term | 用户自定义信号 2 |
| SIGCHLD | 20,17,18 | Ign | 子进程停止或终止 |
| SIGCONT | 19,18,25 | Cont | 如果进程继续 |
| SIGSTOP | 17,19,23 | Stop | 停止进程 |
| SIGTSTP | 18,20,24 | Stop | 在 tty 输入的停止 |
| SIGTIN | 21,21,26 | Stop | 后台进程的 tty 输入 |
| SIGTOU | 22,22,27 | Stop | 后台进程的 tty 输出 |

信号 SIGKILL 和 SIGSTOP 无法被捕获、阻塞或忽略。

这个表看起来可能有些突其来，但它让你对向进程发送信号时预期的结果有一个大致的了解。你可以看到，默认情况下，这些信号会终止进程。

注意的是 SIGUSR1 和 SIGUSR2 信号很有趣。这些信号的动作专门设计用于由你的进程定义。我们很快就会看到，我们可以自由地重新定义任何喜欢的信号动作，但这两个信号是供你使用的。

## 重新定义信号

让我们回到那两个 ruby 会话并玩点有趣的。

- 1. 在第一个 ruby 会话中，使用以下代码重新定义 INT 信号的行为：

```ruby
puts Process.pid
trap(:INT) { print "Na na na, you can't get me" }
sleep # so that we have time to send it a signal
```

现在，我们的进程在接收到 INT 信号时不会退出。

- 2. 在第二个 ruby 会话中发出以下命令，注意第一个进程正在嘲笑我们！

```ruby
Process.kill(:INT, <pid of first session>)
```

- 3. 你可以尝试使用 Ctrl-C 来杀死第一个会话，并发现它的响应是一样的！

- 4. 但如表所示，有些信号是无法重新定义的。SIGKILL 会让你看到谁才是老大。

```ruby
Process.kill(:KILL, <pid of first session>)
```

## 忽略信号

- 1. 在第一个 `ruby` 会话中使用以下代码：

```ruby
puts Process.pid
trap(:INT, "IGNORE")
sleep # so that we have time to send it a signal
```

- 2. 在第二个 `ruby` 会话中发出以下命令，注意第一个进程不受影响。

```ruby
Process.kill(:INT, <pid of first session>)
```

第一个 `ruby` 会话不受影响。

## 信号处理器是全局的

信号是一个非常强大的工具，非常适合某些情况。但最好记住，**捕获信号有点像使用全局变量**，你可能会覆盖某些代码依赖的内容。而且与全局变量不同，信号处理器无法进行命名空间划分。

所以，在你所有的开源库中添加信号处理器之前，请务必阅读下一节 :)





# 第 17 章
进程可以进行通信

到目前为止，我们查看了共享内存和共享开放资源的相关进程。但在多个进程之间如何传递信息呢？

这是一个名为“进程间通信”（Inter-process communication，简称 IPC）的整个领域。实现 IPC 有许多不同的方法，但我将介绍两种常用的实用方法：管道（pipes）和套接字对（socket pairs）。

## 我们的第一个管道

管道是一个单向的数据流。换句话说，你可以打开一个管道，一个进程可以“占用”其中一端，另一个进程可以“占用”另一端。然后数据就可以沿着管道传递，但只能向一个方向。因此，如果一个进程“占用”了读取者而非写入者的位置，它将无法向管道写入数据。反之亦然。

在引入多个进程之前，让我们先看看如何创建一个管道以及我们从中得到什么：

```ruby
reader, writer = IO.pipe => [#<IO:fd 5>, <IO:fd 6>]
```

IO.pipe 返回一个包含两个元素的数组，这两个元素都是 IO 对象。Ruby 极其强大的 IO 类是 `File`、`TCPSocket`、`UDPSocket` 等类的父类。因此，所有这些资源都有共同的接口。

IO.pipe 返回的 IO 对象可以被视为匿名文件。你基本上可以像构建 `File` 一样对待它们。你可以调用 `#read`、`#write`、`#close` 等。但该对象不会响应 `#path` 方法，且在文件系统中没有位置。

在暂不引入多个进程的情况下，让我们演示使用管道进行通信：

```ruby
reader, writer = IO.pipe
writer.write("Into the pipe I go...")
writer.close
puts reader.read
```

输出

```
Into the pipe I go...
```

非常简单对吧？注意到我在向管道写入数据后必须关闭写入者了吗？这是因为当读取者调用 `IO#read` 时，它将继续读取数据，直到看到 EOF（即文件结束标记符）。这告诉读取者将不再有更多数据可供读取。

只要写入者仍打开状态，读取者就可能看到更多数据，因此它会一直等待。通过在读取之前关闭写入者，可以在管道上放置一个 EOF，这样读取者在获取初始数据后就会停止。如果你跳过关闭写入者的步骤，读取者将阻塞并无限读取下去。

1. http://libreflist.com/browser/usp.ruby/2011/9/17/the-ruby-io-class/
2. http://en.wikipedia.org/wiki/End-of-file

## 管道仅单向

```ruby
reader, writer = IO.pipe
reader.write("Trying to get the reader to write something")
```

输出

```
>> reader.write("Trying to get the reader to write something")
IOError: not opened for writing
  from (irb):2:in `'write'
  from (irb):2
```

IO.pipe 返回的 IO 对象只能用于单向通信。因此，读取者只能读取，写入者只能写入。

让我们把进程引入进来。

## 共享管道

在关于 fork（派生）的章节中，我描述了当进程派生子进程时开放资源是如何共享或复制的。管道被视为一种资源，它们有自己的文件描述符等，因此它们会与子进程共享。

这里有一个使用管道在父进程和子进程之间进行通信的简单示例。子进程通过向管道写入数据向父进程指示它已完成了一次迭代：

```ruby
reader, writer = IO.pipe

fork do
  reader.close

  10.times do
    # 重负载操作
    writer.puts "Another one bites the dust"
  end
end

writer.close
while message = reader.gets
  $stdout.puts message
end
```

输出 Another one bites the dust 十次。

注意到，像上面一样，管道未使用的端被关闭了，以防干扰 EOF 的发送。当涉及到两个进程时，考虑 EOF 实际上还有多一层。由于文件描述符被复制了，现在有 4 个实例在运行。由于只有其中 2 个将用于通信，另外 2 个实例必须关闭。这就是为什么有额外的关闭操作。

由于管道的两端是 IO 对象，我们可以在它们上调用任何 IO 方法，而不仅仅是 `#read` 和 `#write`。在这个示例中，我使用 `#puts` 和 `#gets` 来读取和写入以换行符分隔的字符串。我实际上在这里使用这些方法是为了简化管道的一个方面：管道持有数据流。

## 流 vs 消息

当我说“流”（stream）时，我的意思是向管道写入和读取数据时，没有开始和结束的概念。在处理 IO 流（如管道或 TCP 套接字）时，你将数据写入流中，并跟上某些特定特定的分隔符。例如，HTTP 使用一系列换行符来分隔头部和正文。

然后当从该 IO 流中读取数据时，你一次读取一个块，遇到分隔符时停止。这就是为什么我在上一个示例中使用了 `#puts` 和 `#gets`：它为我使用了换行符作为分隔符。

正如你可能猜到的，使用消息（messages）而不是流进行通信是可能的。我们无法通过管道做到，但可以通过 Unix 套接字做到。在不涉及过过多细节的情况下，Unix 套接字是一种只能在同一台物理机器上通信的套接字。因此，它比 TCP 套接字快得多，非常适合 IPC。

这里有一个创建一个 Unix 套接字对的示例，它们通过消息通信：

```ruby
require 'socket'
Socket.pair(:UNIX, :DGRAM, 0) => [#<Socket:fd 15>, #<Socket:fd 16>]
```

这创建了一对 Unix 套接字，它们已经连接在一起。这些套接字使用数据报（datagrams）而不是流。通过这种方式，你向一个套接字写入完整消息，从另一个套接字读取完整消息。不需要分隔符。

这是一个稍微复杂的管道示例，其中子进程等待父进程告诉它要做什么，然后在完成完成后向父进程报告：

```ruby
require 'socket'

child_socket, parent_socket = Socket.pair(UNIX, DGRAM, 0)
maxlen = 1000

fork do
  parent_socket.close

  4.times do
    instruction = child_socket.recv(maxlen)
    child_socket.send("#{instruction} accomplished!", 0)
  end
child_socket.close

2.times do
  parent_socket.send("Heavy lifting", 0)
end
2.times do
  parent_socket.send("Feather lifting", 0)
end

4.times do
  $stdout.puts parent_socket.recv(maxlen)
end
```

输出

```
Heavy lifting accomplished!
Heavy lifting accomplished!
Feather lifting accomplished!
Feather lifting accomplished!
```

因此，虽然管道提供单向通信，但套接字对提供了双向通信。父套接字可以同时读取和写入子套接字，反之亦然。

## 远程 IPC？

IPC 指运行在同一机器上的进程之间的通信。如果你对从一台机器扩展到许多机器并进行类似于 IPC 操作感兴趣，有一些东西可以研究。第一种方案只需通过 TCP 套接字进行通信。对于非复杂的系统，这种方案比其他方案需要更多的代码。其他可能的解决方案是 RPC ³（远程过程调用）、像 ZeroMQ ⁴ 这样的消息系统或通用的分布式系统⁵。

³ http://en.wikipedia.org/wiki/Remote_procedure_call
⁴ http://www.zermq.org/
⁵ http://en.wikipedia.org/wiki/Distributed_computing

管道和套接字对都是进程间通信非常有用的抽象。它们快速且简单。通常用于替代使用共享数据库或日志文件这种粗暴的方法。





## 守护进程 (Daemon Processes)

守护进程是在后台运行的进程，而不是在终端用户的控制下运行的进程。守护进程的常见示例如 Web 服务器或数据库服务器，它们会一直在后台运行，以处理请求。

守护进程也是你操作系统的核心。有很多进程在后台不断运行，保持你的系统正常运行。这些是诸如 GUI 系统上的窗口服务器、打印服务或音频服务，这样你的扬声器就能随时准备好播放那个恼人的“叮”的通知音。

## 第一个进程 (The First Process)

有一个特定的守护进程对你的操作系统具有特殊意义。我们在上一个章节中讨论过，每个进程都有一个父进程。这对于所有进程都真实吗？系统上的第一个进程呢？

这是一个经典的“谁创造了创造者”的问题，但它有一个简单的答案。当内核启动（bootstrap）时，它会产生一个名为 `init` 的进程。该进程的 ppid 为 0，是“所有进程的祖父”。它是第一个进程，且没有祖先。它的 pid 是 1。

## 创建你的第一个守护进程

我们需要准备什么呢？并不多。任何进程都可以变成守护进程。

让我们看看 rack 项目¹ 的例子。Rack 带有一个 `rackup` 命令，用于使用不同的支持 rack 的 Web 服务器提供服务。Web 服务器是一个永远不会结束的进程示例；只要你的应用程序处于激活状态，你就一个服务器来监听连接。

`rackup` 命令包含一个选项，可以将服务器守护化并在后台运行。让我们来看看它是如何做什么的。

> ¹http://github.com/rack/rack

## 深入研究 Rack (Diving into Rack)

```ruby
def daemonize_app
  if RUBY_VERSION < "1.9"
    exit if fork
    Process.setsid
    exit if fork
    Dir.chdir "/"
    STDIN.reopen "/dev/null", "a"
    STDOUT.reopen "/dev/null", "a"
    STDERR.reopen "/dev/null", "a"
  else
    Process.daemon
  end
end
```

这里有很多操作。我们先跳到 `else` 块。Ruby 1.9.x 带有一个名为 `Process.daemon` 的方法，它可以让当前进程守护化！太方便了！

但你不想知道它在底层是如何工作的吗？我知道你想！事实是，如果你查看 `Process.daemon` 的 MRI 源码并翻阅 C 代码，它最终执行的操作与上面 `if` 块中 Rack 所做的完全相同。

所以让我们继续用它作为例子。我们将逐行分析代码。

> 2.https://github.com/ruby/ruby/blob/c852d76f4a68e2820ofoc3f68c68789e79c86/process.c#L4817-4860

## 逐步实现进程守护化

```ruby
exit if fork
```

这一行代码智能地利用了 `fork` 方法的返回值。回想分支（forking）章节，`fork` 返回两次：一次在父进程中，一次在子进程中。在父进程中，它返回子进程的 pid，在子进程中则返回 `nil`。

一如既往，返回值对于父进程是真（truth-y），对于子进程是假（false-y）。这意味着父进程将退出，正如我们所知，孤儿子进程会正常继续。

> 如果一个进程是孤儿，那么当你请求 `Process.ppid` 时会发生什么？
这就是对 `init` 进程知识变得相关的地方。孤儿进程的 ppid 始终为 1。这是内核可以确保始终活跃的唯一进程。

在创建守护进程时，第一步是至关重要的，因为会导致调用此进程的终端退出。由于我们所知，孤儿子进程会正常继续。

这第一步在创建守护进程时是强制性的，因为它导致了调用此进程的终端退出。由于父进程的退出，孤儿子进程会正常运行。由于由于所所，，由于.id会会退出退出，让进程脱离终端。

```ruby
Process.setsid
```

调用 `Process.setsid` 做了以下三件事：

1. 进程成为新会话的 leader
2. 进程成为新会话组的 leader
3. 进程没有控制终端

为了准确理解这三点的影响，我们需要深入了解进程组和会话组。

## 进程组 (Process Groups)

进程组和会话组是作业作业的。进程组和会话组是关于终端的控制。进程组和会话组是关于终端的控制。进程组和会话组是关于终端的控制。进程组和会话组是关于终端的控制。进程组和会话组是关于终端的控制。

进程组和会话组是关于终端的控制。尝试以下代码片段：

```ruby
puts Process.pid
puts Process.pgid

fork {
  puts Process.pid
  puts Process.pgid
}
```

你可以看到，尽管这些进程属于同一个会话，但一个 Ctrl-C 会杀死它们所有的。这些命令属于同一个会话。每个 shell 的调用都会获得自己的进程组。一个调用可以是单个命令，也可以是通过管道连接的一系列命令。

就像上面的示例，会话组可能连接到终端。它也可能没有连接到任何终端，例如守护进程。

```bash
git log | grep | less
```

在这种情况下，每个命令都会获得自己的进程组，因为每个都可能创建子进程。即使这些命令属于同一个会话，一个 Ctrl-C 会杀死它们所有的。

由于每个子进程都可能创建子进程，每个会话组都是一个进程组。会话的 leader。

```ruby
puts Process.pid
puts Process.pgid
```

你可以看到，尽管这些进程属于同一个会话，但一个 Ctrl-C 会杀死它们所有的。这些命令属于同一个会话。每个 shell 的调用都会获得自己的进程组。一个调用可以是单个命令，也可以是通过管道连接的一系列命令。




会话领导，这可以保证该进程永远不会拥有控制终端。终端只能分配给会话领导。

这一系列操作确保了我们的进程现在完全脱离了控制终端，并将一直运行完成。

```
Dir.chdir "/"
```

这会将当前工作目录更改为系统的根目录。并不是严格必要的，但这是一个额外步骤，用于确保守护进程在执行期间当前工作目录不会消失。

这避免了守护进程启动时的目录因任何原因被删除或卸载的问题。

```
STDIN.reopen "/dev/null"
STDOUT.reopen "/dev/null", "a"
STDERR.reopen "/dev/null", "a"
```

这会将所有标准流都重定向到 `/dev/null`，即被忽略。由于守护进程不再连接到会话终端，这些流已经没有用了。你不能简单地关闭它们，因为某些程序期望它们始终可用。将它们重定向到 `/dev/null` 可以确保它们对程序仍然可用，但不会产生任何影响。

## 在现实世界中

提到，`rackup` 命令带有一个用于将进程守护化的命令行选项。任何流行的 Ruby Web 服务器也是如此。

如果你想深入研究守护进程的内部机制，你应该查看 `daemons` rubygem 1。

如果你想创建一个守护进程，你应该问自己一个基本问题：这个进程需要永久运行吗？

如果答案是否定的，那么你可能想查看 cron 任务或后台作业系统。如果答案是定的，那么你可能有一个很好的守护进程候选者。

## 系统调用

Ruby 的 `Process.setsid` 映射到 `setsid(2)`，`Process.getpgid` 映射到 `getpgid(2)`。本章提到的其他系统调用在之前的章节中详细介绍过。

## 产生终端进程

Ruby 程序中一种常见的交互是从程序中“调用 shell”（shelling out）以在终端中运行命令。当我编写 Ruby 脚本来为自己将一些常用组合在一起时，这种情况经常发生。在 Ruby 中，有几种方法可以产生进程来运行终端命令。

在查看不同的“调用 shell”方式之前，让我们看看它们在底层共同使用的机制。

### fork + exec

下面描述的所有方法都是同一个主题的变体：`fork(2) + exec(2)`。

我们在之前的章节中仔细查看了 `fork(2)`，但这是我们第一次查看 `exec(2)`。它非常简单，`exec(2)` 允许用不同的进程替换当前进程。

换句话说：`exec(2)` 允许你将当前进程转换为任何其他进程。你可以获取一个 Ruby 进程并将其转换为 Python 进程，或者 `ls(1)` 进程，或者另一个 Ruby 进程。

`exec(2)` 会转换进程且永不返回。一旦你将 Ruby 进程转换为其他东西，你就永远无法回来了了。

```
exec 'ls', '--help'
```

`fork + exec` 组合在产生新进程时非常常见。`exec(2)` 是将当前进程转换为另一个进程非常强大且高效的方法；唯一的缺点是你的当前进程消失了。这就是 `fork(2)` 派上用场的地方。

你可以使用 `fork(2)` 创建一个新进程，然后使用 `exec(2)` 将其转换为你喜欢的任何东西。漂亮！当前进程仍然像以前一样运行，而你能够产生任何需要的其他进程。

如果你的程序依赖于 `exec(2)` old的输出，你可以使用之前章节中学到的工具来处理它。`Process.wait` 将确保你的程序等待子进程完成它正在做的事情，以便你获得返回的结果。

记住，`exec(2)`（默认情况下）不会关闭任何已打开的文件描述符，也不会进行任何内存清理。你可以在某些情况下利用这一点。你的优势。在其他情况下，它可能会导致资源使用问题。

```
hosts = File.open('/etc/hosts')
exec 'python', '-c', 'import os; print os.fdopen(#{hosts.fileno}).read()'
```

在这个示例中，我们启动了一个 Ruby 程序并打开了 `/etc/hosts` 文件。我们通过 `exec(2)` 启动了一个 python 进程，并告诉它 Ruby 打开 `/etc/hosts` 文件时接收的文件描述符。你可以看到 python 识别了这个文件描述符（因为它通过 `exec(2)` 共享了），并能够在无需重新打开文件的情况下读取它。

## exec 的参数

注意在上面的所有示例中，我向 `exec` 发送了一个参数数组，而不是作为字符串传递它们。两种参数形式之间存在细微的。

向 `exec` 传递字符串，它实际上会启动一个 shell 进程并将字符串传递给 shell 进行解释。传递数组，它将跳过 shell 并直接将数组设置为新进程。

**通常你想要避免传递字符串，除非你真的需要。尽可能传递数组。** 传递字符串并通过 shell 运行代码可能会引发安全疑虑。如果涉及用户输入，他们可能直接在 shell 中注入恶意命令，潜在地获得当前进程拥有的任何权限。在你想做类似下面的操作的情况下：

## Kernel#system

```
system('ls')
system('ls', '--help')
system('git log | tail -10')
```





`IO.popen` 最常用的用法是在纯 Ruby 中实现 Unix 管道。这正是 `popen` 中 'p' 的来源。在底层，它仍然在执行 `fork+exec`，但它同时也建立了一个管道与派生的进程进行通信。该管道作为块参数传递给 `IO.popen` 的块形式。

```
# 一个 IO 对象被传递到块中。在这种情况下，我们以写入模式打开流，
# 因此流被设置为派生进程的 STDIN。
# 如果我们以读取模式打开流（默认值）
# 流将被设置为派生进程的 STDOUT。
IO.popen('less', 'w') { |stream|
  stream.puts "some\data"
}
```

使用 `IO.popen` 时，你必须选择你可以访问哪种流。你无法同时访问它们。

## open3

Open3 允许同时访问派生进程的 STDIN、STDOUT 和 STDERR。

```
# 这是标准库的一部分可用。
require 'open3'

Open3.popen3('grep', 'data') { |stdin, stdout, stderr|
stdin.puts "some\ndata"
stdin.close
puts stdout.read
}

# Open3 会在可用时使用 Process.spawn。选项可以像这样
# 传递给 Process.spawn：
Open3.popen3('ls', '-uhh', :err => :out) { |stdin, stdout, stderr|
puts stdout.read
}
```

Open3 的作用就像是 `IO.popen` 的一个更灵活的版本，供你在需要的时候使用。

## 在现实世界中

所有这些方法在现实世界中都非常常见。由于它们的行为各不相同，你必须根据自己的需求选择其中一种。

所有这些方法的共同缺点是它们依赖于 `fork(2)`。这有什么问题呢？想象这样一个场景：你有一个占用数百 MB 内存的大型 Ruby 应用。你需要调用外部命令（shell out）。如果你使用上述任何方法，你将承担 `fork` 的开销。

即使你只是调用一个简单的 `ls(1)` 命令，内核仍然需要确保 Ruby 进程正在使用的所有内存对于该 `ls(1)` 进程可用。为什么？因为这就是 `fork(2)` 的 API。当你执行 `fork(2)` 时，进程内核并不知道你正准备通过 `exec(2)` 转换该进程。你可能是为了运行 Ruby 代码而进行 fork，在这种情况下，你需要所有内存都可用。

记住 `fork(2)`是有开销的，有时它可能会成为性能瓶颈。如果你需要频繁调用外部命令且不想承担 `fork(2)` 的开销怎么办？

有一些原生的 Unix 系统调用可以在不产生 `fork(2)` 开销的情况下派生进程。遗憾的是，Ruby 语言的核心库并没有对这些支持的支持。不过，有一个 Rubygem 为这些系统调用提供了 Ruby 接口。`posix-spawn` 项目提供了对 `posix_spawn(2)` 的访问，它在大多数 Unix 系统上都是可用的。

`posix-spawn` 模拟了 `Process.spawn` API。事实上，你传递给 `Process.spawn` 的大多数选项也可以传递给 `POSIX::spawn.spawn`。因此，你可以继续使用相同的 API，并重复 factor 的优势——更高效的进程派生。

在基础层面，`posix_spawn(2)` 是 `fork(2)` 的子集。回一下 `fork(2)` 产生的新子进程的显著特征：1. 它获得了父进程内存中所有内容的精确拷贝；2. 它获得了父进程已打开的所有描述符的拷贝。

`posix_spawn(2)` 保留了 #2 但没有保留 #1。这是两者最大的区别。因此，你可以预期新派生的进程可以访问父进程打开的任何描述符，但它不会共享任何内存。这就是为什么 `posix_spawn(2)` 比 `fork(2)` 更快、更高效。但请记住，这使其灵活性降低了。

> 2.http://github.com/rtomayko/posix-spawn

## 系统调用

Ruby 的 `Kernel#system` 映射到 `system(3)`，`Kernel#exec` 映射到 `execve(2)`，`IO.popen` 映射到 `popen(3)`，posix-spawn 使用 `posix_spawn(2)`。

## 结

在 Unix 中处理进程涉及两件事：抽象和通信。

## 抽象

内核对它的进程有一个极其抽象（且简单）的视角。作为程序员，我们习惯于将源代码视为程序之间的区别。

我们精通许多编程语言，并将每种语言用于不同的目的。我们不可能在带有垃圾回收的语言中编写出内存高效的代码，我们必须使用 C。但我们需要对象，让我们用 C++ 吧。以此类推。

但如果你问内核，它们看起来是一样的。最终，我们所有的代码都被编译成内核可以理解的简单内容。当它在那个层级工作时，所有进程都被同等对待。每个东西都会获得一个数字标识符，并获得访问内核资源的平等权限。

这些废话的意义何？使用 Unix 编程让你能够稍微调节一下这些旋钮。它让你能够完成那些在编程语言层面无法实现的事情。





```ruby
procline "Forked #{@child} at #{Time.now.to_i}"
```

procline 是 Resque 用于更新当前进程名称的内部方法。记得我们提到过，可以使用 $0 来更改当前进程的名称，但没有程序化的方法可以做到？

这就是 Resque 的解决方案。`procline` 设置当前进程的名称。

```ruby
Process.wait(@child)
```

如果你读过关于 `Process.wait` 的章节，那么这行代码对你来说应该很。

`child` 变量被赋值为 `fork` 调返回值。因此在父进程中，它将是子进程 PID。这行代码告诉父进程阻塞，直到子进程完成。

现在我们来看一下子进程中发生了什么。

```ruby
procline "Processing #{@job.queue} since #{Time.now.to_i}"
```

注意，`if` 和 `else` 块都调用了 `procline`。尽管这两行代码属于同一个逻辑结构，但它们是在两个不同的进程中执行的。由于进程名称是进程进程特定的，这两个调用将分别为父进程和子进程设置名称。

```ruby
perform(job, &block)
```

在这里，子进程中是 Resque 真正“执行”任务的地方。

```ruby
exit! unless @cant_fork
```

然后子进程退出。

## 为什么要费此精力？

正如本章第一段提到的，Resque 这样做并不是为了实现并发或提高速度。事实上，它为每个任务的处理增加了一个额外步骤，这使得整个过程变慢了。那么为什么要这么麻烦呢？为什么不直接一个接一个处理任务呢？

Resque 使用 `fork(2)` 来确保其工作进程的内存占用不会膨胀。让我们回顾一下 Resque 工作进程 fork 时发生了什么，以及它如何影响 Ruby 虚拟机。

你可能还记得 `fork(2)` 会创建一个原始进程的精确副本新进程。在这种情况下，原始进程已经加载了应用程序环境且没有其他内容。因此我们知道在 fork 之后，我们将有一个只加载了应用程序环境的新进程。

然后子进程将开始处理任务。这就是内存使用可能出现问题。后台任务可能需要将图像文件加载到主内存中处理，或者从数据库获取大量的 ActiveRecord 对象，或者任何需要使用大量主内存的操作。

一旦子进程完成任务，它就会退出，从而将其所有内存释放给操作系统进行清理。然后原始进程就可以恢复运行，此时再次只加载了应用程序环境。

所以，每当 Resque 执行一个任务时，你在内存使用方面都回到了一个干净的起点。这意味着在处理任务时，内存占用可能会飙升，但它应该总是回到那个良好的基准线。

## GC（垃圾回收）不就帮我们清理的吗？

嗯，是的，但它做得并不完美。它做得还可以。事实是，MRI 的 GC 很难释放它不再需要的内存。

当 Ruby 虚拟机启动时，内核会为它分配某块主内存。当它用完所有可用内存时，它需要向内核请求另一块主内存。

由于 Ruby GC 的许多问题（天真的方法、磁盘碎片化），虚拟机很少能将内存块释放回内核。因此，Ruby 进程的内存占用可能会随时间推移而增长，而不是缩小。现在 Resque 的方法开始变得合理起来了！

如果 Resque 工作进程简单地按可用顺序处理每个任务，它将无法维持那个良好的内存使用基准水平。一旦它处理一个需要大量主内存的任务，这些内存就会一直被工作进程占用，直到它退出。

即使随后的任务需要的内存少得多，Ruby 也很难将这些内存还给内核。因此，工作进程不可避免地随着时间推移而变大，永不缩小。

得益于 `fork(2)` 的威力，Resque 工作进程是可靠的，在处理一定数量的任务后不需要重启。

## 附录：Unicorn 如何收割工作进程

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 事实上的收割

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 事实上的收割

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 事实上的收割

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 事实上的收割

任何对 Ruby 语言中 Unix 编程的研究，如果不多次提到 Unicorn Web 服务器¹，都是不完全的。

## 这是怎么回事？

- ¹See http://www.unicorn-server.org/

```ruby
def reap_all
  begin
    wpid, status = Process.waitpid(-1, Process::WNOHANG)
    return unless wpid
    
    if status.success?
      logger.info "reaped worker #{wpid}"
    else
      logger.error "worker #{wpid} exited with status #{status}"
    end
    
    reap_all
  rescue Errno::ECHILD
  end
end
```



```ruby
wpid or return
```

这一行看起来可能有点奇怪，但它实际上是一个条件返回语句。如果 `wpid` 为 `nil`，那么我们最后一行返回了 `nil`。这意味着没有子进程退出并将其状态返回给我们。

如果是这样，那么此方法将返回，它的任务就完成了。

```ruby
if reexec_pid == wpid
  logger.error "reaped #{status.inspect} exec()-ed"
  self.reexec_pid = 0
  self.pid = pid.chomp('.oldbin') if pid
  proc_name = 'master'
```

我不想花很多时间来讨论这部分。'reexec' 相关内容与 Unicorn 的内部实现有关，特别是它是如何处理零停机重启的。也许我可以在未来的报告中介绍这个过程。

我想要引起你注意的是对 `proc_name` 的调用。这类似于 Resque 章节中的 `procline` 方法。Unicorn 也有一个更改当前进程显示名称的方法。这是与软件用户通信的一个至关重要的部分。

```ruby
else
  worker = WORKERS.delete(wpid) and worker.close rescue nil
```

Unicorn 在其 `WORKERS` 常量中存储了当前活跃的 worker 进程列表。`WORKERS` 是哈希，键是 worker 进程的 pid，值是 `Unicorn::Worker` 的实例。

因此，这一行从 Unicorn 的内部跟踪列表 `(WORKERS)` 中移除 worker 进程，并在 worker 实例上调用 `#close`，关闭其不再需要的心跳机制。

```ruby
m = "reaped #{status.inspect} worker=#{worker.nr} rescue 'unknown'"
```

这一行根据 `Process.waitpid2` 调用返回的 `status` 构建了日志消息。

该字符串是通过首先检查 `status` 变量构建的。它看起来像什么？类似于这样：

```
#<Process::Status: pid=32227, exited(0)>
# or
#<Process::Status: pid=32308, signaled(SIGINT=2)>
```

它包含了结束进程的 pid 以及其结束的方式。在第一行中，进程以退出代码 0 自退出。在第二行中，进程被信号杀死（在这种情况下是 `SIGINT`）。因此，这样的一行会被添加到 Unicorn 日志中。

日志行的第二部分 `worker.nr` 是 Unicorn 对 worker 的内部表示。

```ruby
status.success? ? logger.info(m) : logger.error(m)
```

这一行获取构建好的日志消息并发送给记录器。它使用 `status` 对象上的 `success?` 方法将此消息记录为 INFO 级别或 ERROR 级别。

`success?` 方法只在一种情况下返回 `true`，即进程以退出代码 0 退出。如果以不同的代码退出，它将返回 `false`。如果被信号杀死，它将返回 `nil`。

```ruby
rescue Errno::ECHILD
  break
```

这是此方法中顶层 `begin` 语句的一部分。如果抛出此异常，此方法的无限循环将执行 `break` 并返回。

如果当前进程没有子进程，`Process.waitpid2`（或任何类似的方法）将抛出 `Errno::ECHILD` 异常。如果在这种情况下发生这种情况，意味着此方法的任务完成了！所有子进程都已收割（reaped）。因此它返回。

## 结论

这段代码对你产生了兴趣，如果你想学习更多关于 Ruby 中的 Unix 编程，Unicorn 是一个很棒的资源。访问官网 http://unicorn.bogomips.org 去学习吧！

## 附录：预分服务器

我很高兴你读到了这里，因为这一章可能是整书中内容最丰富的内容。预分服务器将书中解释的许多概念整合成一种强大且高效的方法，来解决某些特定问题。

你很有可能用过 Phusion Passenger¹ 或 Unicorn²。这两者服务器，以及 Spyglass（本文包含的 Web 服务器）-



假设有10个互独立不共享套接字的进程，每个进程都必须绑定到一个唯一的端口。现在必须有一个基础设施运行在所有 Mongrel 进程之前。它必须知道每个 Mongrel 进程绑定到了哪个端口，并且必须确保每个 Mongrel 一时间只处理一个连接，并确保连接得到适当平衡。

再次，预Fork（preforking）在简单性和资源效率方面都胜出。

## 3. 高效的系统管理

这一点技术性较少，更多是是以人为本的。

作为一个预分派服务器的管理员，你通常只需要向主进程发送命令（通常是信号）。它将负责跟踪并向其工作进程中送消息。

在管理多个非预分派服务器实例时，系统管理员必须跟踪每个实例，分别对它们进行管理，并确保它们的命令得到执行。

## 预Fork服务器的基本示例

以下是预分派服务器的一个非常基础的代码。它可以使用多个进程并行响应请求，并利用内核进行负载均衡。如果需要更复杂的预分派服务器示例，我建议你查看 Spyglass 的源代码（下一章）或 Unicorn 的源代码。

```ruby
require 'socket'
## 打开一个套接字。
socket = TCPServer.open('0.0.0.0', 8080)

## 预加载应用代码。
## require 'config/environment'

## 将任何相关信号传递给子进程。
[:INT, :QUIT].each do |signal|
 Signal.trap(signal) {
  wpids.each { |wpid| Process.kill(signal, wpid) }
 }
}


## 用于跟踪子进程 pid。
 wpids = []

5.times {
 wpids << fork do
  loop {
   connection = socket.accept
   connection.puts 'Hello Readers!'
   connection.close
  }
  }

Process.waitall
```

你可以使用类似 `nc(1)` 或 `telnet(1)` 的工具来查看它的效果。

```bash
$ nc localhost 8080
$ telnet localhost 8080
```

注意，我在代码里偷偷加入了一个新东西吗？我们还没有见过过 `Process.waitall`，它出现在上面示例代码的最后一行。

`Process.waitall` 仅仅是 `Process.wait` 封装的一个便利方法。它运行一个循环等待所有子进程退出，并返回一个进程状态数组。当你实际上不想对进程状态信息做任何处理时，它非常有用，只需等待子进程退出。

## 附录：Spyglass

如果你想了解更多关于 Unix 进程的知识，那么下一个目标应该是包含的 Spyglass 项目。为什么？因为它是专门为了展示 Unix 编程概念而编写的。

> 如果你有这本书的副本但没有获得附带的代码项目，请给我发邮件，我会提供给你的：jesse@workingwithunixprocesses.com。

你读到的案例旨在展示相同的内容，但当你刚开始学习 Unix 编程时，它们有时会非常晦涩且难以阅读。Spyglass 的目的是弥补这一差距。

## Spyglass 的架构

Spyglass 是一个 Web 服务器。它向外部世界打开一个套接字并处理 Web 请求。Spyglass 解析 HTTP，符合 Rack 标准，并且非常棒。

以下关于如何启动 Spyglass 服务器以及它在接收到 HTTP 请求会发生什么的简要总结。

## 启动 Spyglass

```bash
$ spyglass
$ spyglass -p other_port
$ spyglass -h # 用于帮助
```

## 请求到达之前

启动后，控制权被移交给 `Spyglass::Lookout`。这个类**没有**预加载 Rack 应用，并且对 HTTP 一无所知，它只是在等待连接。在此时，Spyglass 极其轻量，它仅仅是一个打开的套接字。

## 连接建立

当 `Spyglass::Lookout` 通知连接已建立时，它会 fork 出 `Spyglass::Master` 来实际处理连接。`Spyglass::Lookout` 在 fork 主进程后使用 `Process::wait`，因此它在主进程退出之前一直保持空闲状态。

`Spyglass::Master` 负责预加载 Rack 应用以及 fork/监控工作进程。主进程本身对 HTTP 解析或请求处理一无所知。

真正的工作是在 `Spyglass::Worker` 中完成的。它使用预取章节中概述的方法接受连接，依靠内核进行负载均衡。一旦获得连接，它就会解析 HTTP 请求，调用 Rack 应用，并将响应写入客户端。

## 归于平静

只要有稳定的入流量，Spyglass 就会继续作为预取服务器工作。如果它的内部超时在没有收到更多入请求的情况下到期，那么主进程及其所有工作进程将退出。控制权返回给 `Spyglass::Lookout`，工作流再次开始。

## 开始上手

Spyglass 不是一个生产就绪的服务器，所以不要急于在你的项目中使用它！它是为了阅读而编写的代码库。它有大量的注释，并使用 rocco ¹ 生成了格式化文档。

此时最好的做法是在终端中进入随书提供的 `code` 目录，找到 Spyglass 代码库并运行 `rake read`。这将在浏览器中打开格式化文档供你尽情阅读。

现在去阅读代码吧！愿 `fork(2)` 与你同在！

