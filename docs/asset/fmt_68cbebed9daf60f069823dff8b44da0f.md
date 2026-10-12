
左：配合使用命令在后台运行你的进程

# 教程进程

检查提供的服务器代码，你可以使用端口号 `1234` 与其他部分进行测试。一旦安装了让其运行的工具，你就可以离开了。使用 `syslog` 代理将能够从你的服务器发送日志到：

```
Jan 27 10:34:16 my-server-1 server[1234]: Connection from 172.168.1.1
```

记住 `Perl` 是一种解释型语言，每个人都知道。这是你的服务器进程源代码：

```c
// NEEDS TO BE IMPLEMENTED
```

```c
int fd = open(logfile, O_RDWR|O_CREATE, MODE);
if (fd < 0) {
    exit(0);
}
ftruncate(fd, 0);
sprintf("%s\n", getpid());
write(fd, buffer, strlen(buffer)+1);
close(fd);
```

```c
if (signal(SIGHUP, handle_sigup) == SIG_ERR) {
    syslog(LOG_INFO, "There was an error handling the SIGHUP!\n\n");
    return -1;
}
```

```c
if (signal(SIGUSR1, handle_sigusr1) == SIG_ERR) {
    syslog(LOG_INFO, "There was an error handling the SIGUSR1!\n\n");
    return -1;
}
```

```c
struct sockaddr_in client_address;
int port = 12345;
char line[MAXSIZE];
int sockfd;
socklen_t slen = 0;
sockfd = createudp(0);
syslog(LOG_INFO, "The UDP server is running!\n");
```

```c
while (1) {
    alen = sizeof(client_address);
    n = recvfrom(sockfd, line, MAXSIZE, 0, (struct sockaddr *)&client_address, &alen);
    syslog(LOG_INFO, "Got: %s, from %s\n", line, inet_ntoa(client_address.sin_addr));
    counter++;
}
return 0;
```

# 更多信号处理

服务器进程以特殊方式处理信号。`Apache` Web 服务器可以处理 `TERM`、`USR1`、`HUP` 和 `WINCH` 信号。`TERM` 信号允许 `Apache` 进程立即尝试杀死它所有的子进程，应该只在紧急情况下使用。然后父进程也会退出。`USR1` 信号导致 `Apache` 进程建议子进程：

```
// 如果锁文件已经存在，则退出
```

![](img/f4a034c4fbc20906a013558fa4e058a2_33_0.png)

```bash
mtsouk@mail:~$ ls -l /var/run/
total 36
drwxr-xr-x 2 root root      60 Dec 14 21:33 apache2
-rw-r-- 1 root root       5 Dec 14 21:33 atd.pid
```

# 教程

# Atom 编辑器

## 破解基于技术构建并受 Emacs 扩展性启发的 Atom 编辑器？是时候调查了...

![](img/f4a034c4fbc20906a013558fa4e058a2_35_0.png)

对于花费大量时间通过键盘输入文字的程序员、作家和系统管理员来说，文本编辑器是一件神圣的工具。快捷键已植入记忆中，而扩展性的力量——我们可能发现很难禁用。对于 `Emacs` 来说，`Alt-Control-Shift` 已经是本能；想要另一套快捷键更是一项严峻的任务，需要真正的动力。

`Atom` 在其短短的生命周期内，主要组件在不到两年前才开放，而 2010 年仅仅是去年。从那时起，`GitHub` `Atom` 发布了数百个包。

它使用 `JavaScript` 等技术构建，并采用最优雅的方式：`CoffeeScript`；使用 `Less` 处理器的扩展格式的 `CSS`；`HTML` 和 `Node.js`。与扩展或修改网页不同，它非常易于使用，无需任何修改，并且可以通过 `GUI` 更改设置。添加一个好的 `Fuzz: Find` 搜索以及针对一切的包，也许现在你想要更详细地了解让 `Atom` 如此吸引人的原因，特别是它的可破解性。

# 01 欢迎（针对 64 位）

你的包里有最新的 `Atom` 吗？如果你使用的是 64 位操作系统，你可能需要为自己进行编译，而且 `ARM` 支持——树莓派和 `Chromebook`——尚未完全准备好。值得注意的是，`Atom` 在所有 `Linux` 发行版上可能运行得并不完美，因此要考虑 `Atom` 是否适合你。你的第一个指令是必要的：

```
apt-get install atom
```

你发行版的等效命令，你就可以开始运行了。`Atom` 的开发速度很快。即使在写这篇文章期间，`Atom` 也已经从 `1.3` 增长到 `1.4`，你今天应该使用 `1.5`。我们的教程适用于这些任何一个版本。

第一次运行 `Atom` 会显示一个分屏窗口（你可以通过帮助菜单访问它；左侧被分为两个窗格。左侧窗格链接到文档打开，右侧窗格提供了打开项目（带模块）或直接进行自定义的选项。这是开发者的一种意图声明。

# Richard Midland

一个 `Unix` 全能手总有一种简单的方法来自己完成他想要的事情：仅仅了解命令行并不难。

# 资源

| 项目 | 链接 |
|---|---|
| `Atom` | `atom.io` |

# Atom 飞行手册

`atom.io/docs`

`Atom` 为 Web 技术构建的，但它的包使其变得非常多功能

![](img/f4a034c4fbc20906a013558fa4e058a2_35_1.png)

# ATOM

一个适用于 21 世纪的可破解文本编辑器

- `Atom` 文档和 `API` 参考
- `GitHub` `issues` 页面，可以在那里找到所有 `GitHub` 创建的包

注意：为了帮助改进 `Atom`，我们在 `GitHub` 上跟踪问题。如果你在 `Atom` 或其包中发现 `bug`，请在 `GitHub` 上报告。

![](img/f4a034c4fbc20906a013558fa4e058a2_36_0.png)

# 02 键盘优先

学习一些快捷键来使用 `Ctrl+Shift+P` - 称为命令面板（`Command Palette`），并记住它显示了所有内容的快捷键，搜索窗口拆分为更多窗格，打开 `GitHub` `issues`，并让你通过输入来找到所有命令，而不是遍历菜单。

`Atom` 也是一个 `GUI`，但一切都可以被纳入控制范围。除了通过命令面板为所有命令定义快捷键外，你还可以安装类似 `Eclipse` 或 `VS` 的模式，使用键盘在之间切换而不会丢失记忆。

使用其中一个快捷键：`Ctrl+Shift+O` 来打开你正在工作的项目（仅限代码文件或文本文件）。这允许 `Atom` 为每个项目创建一个新窗口（这是默认行为），并带有树形视图（`Tree View`）——你可以通过 `Ctrl+T` 将其关闭。

# 03 使用窗格

使用 `Atom` 编辑器，你可以将窗口拆分为多个窗格。上面的截图向我们展示两个垂直窗格，右侧窗格可以通过命令面板拆分为二。拆分窗格的快捷键是 `Ctrl+K`，使用 `Ctrl+方向键` 在它们之间移动。你也可以安装一个使用 `Ctrl+K` 杀死某行的包，你可能可能想要修改或替换 `Atom` 的“向右拆分”（`Split Right`）命令。

每个窗格都有你已经熟悉的选项 - 它们包含大量的 `Chromium`。例如，你可以看到左侧的文件树形视图（或截图右侧的工具栏）并展开/折叠任何 `Atom` 插件。

顺便提一下，窗格和缓冲区（后者是 `Atom` 内存中文件的内容）的任务——

# 04 Web 环境

`Atom` 的 `CoffeeScript` (`CSS`/`HTML`) 编译很容易编辑，以及我们轻松构建的 `GUI` 菜单集，它们直接对应于 `CSS` 设置。这是一个 `CSS` 布局模块，非常容易样式并提供了一个完全控制的环境。就像 `Electron` 一样，它让你自由使用所有的 Web 工具——开发这样一个项目最棒的部分是：

当你启动 `Atom` 时，它会在右侧窗格，你点击“自定义样式”（`Custom Styling`），然后“打开样式表”（`Open Stylesheet`）——你现在正在编辑（空的）`styles.css`。

> 要避免：
>
> `Atom` 的 `CoffeeScript` (`CSS`/`HTML`) 编译很容易编辑，以及我们轻松构建的 `GUI` 菜单集，它们直接对应于 `CSS` 设置。这是一个 `CSS` 布局模块，非常容易样式并提供了一个完全控制的环境。就像 `Electron` 一样，它让你自由使用所有的 Web 工具——开发这样一个项目最棒的部分是：
