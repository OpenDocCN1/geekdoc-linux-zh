

由于守护进程不能连接到终端，它们首先要执行的任务之一就是关闭所有打开的文件描述符（尤其是标准输入、标准输出和标准错误）。它们通常将工作目录设为文件系统的根目录。然后它们会采取额外的步骤来切断与任何 shell 或终端的关联，其中包括离开其进程组并注册其忽略所有传入信号的意图。进程组的概念将在第 8 章中讨论。信号将在本章后面介绍。

守护进程的名称通常以 'd' 结尾。这是在 ps -ef 命令的输出中识别守护进程的一种方法；查找以 "d" 结尾的名称，如 ftpd、httpd、lpd、sshd、syslogd 和 telnetd。守护进程将在第 8 章中得到全面介绍。

## 5.1.3 交互式用户程序

另一类程序是那些与用户终端不可分割地绑定的程序，因为它们会为自己的使用而定制终端。通过终端与用户交互的程序，例如文本编辑器（vi、nano 或 emacs）、分页器（more 和 less）、基于终端的管理工具如 top、游戏（snake、worm 和 chess），以及基于终端的邮件客户端（pine 和 mailx），都与终端紧密耦合，必须控制其设置和属性。它们不能使用标准输入和输出流来与用户通信，因为这些流缺乏终端所具有的控制类型。这类程序通常需要控制

- 字符是否回显，
- 缓冲的字符数，如果有的话，
- 屏幕上光标的移动，
- 某些按键是否应具有其默认含义或具有应用程序定义的含义，
- 输入是否应发生超时，
- 诸如 Ctrl-C 之类的信号应被忽略、排队还是立即处理。

我们已经看到了如何在命令级别使用 stty 以及在编程级别使用 tcgetattr() 和 tcsetattr() 函数来控制终端的状态。在这里，我们将探讨可以将终端置于的各种模式，以便创建交互式程序。

## 5.2 设计交互式用户程序

大多数交互式用户程序都是事件驱动或菜单驱动的，这意味着它们执行某个简短任务，然后等待用户输入以执行下一个任务。所有基于窗口的应用程序都是事件驱动的；它们处于空闲状态，通常在输入上被阻塞，同时等待窗口管理器向它们传递鼠标、键盘或其他事件。

下面我们将介绍设计和开发基于终端的交互式应用程序所需的步骤。我们将从理解问题开始，然后逐步使程序对用户输入做出更灵敏的响应。

## 5.2.2 一个简单的文本编辑器：`simplevi`

vi 文本编辑器是一段非常复杂的软件，但我们可以创建一个极其精简的版本并在过程中学到很多东西。我们将我们的编辑器命名为 simplevi。这个简单的编辑器将允许用户在文本文档的任何位置插入字符，但不会提供删除字符的手段。这只是对程序的一个小扩展。此外，它不会打开现有的文本文件，而是在每次调用时创建一个新文件。添加打开文件的功能并不会为程序的交互式设计提供太多新的见解，但会使程序变得更大。尽可能地，simplevi 实现的功能将与 vi 中的语义相同。

### 5.2.2.1 simplevi 的功能

simplevi 程序允许用户以类似于 vi 的方式创建文件。它只有插入命令，目前不支持删除。像 vi 一样，它始终处于三种可能模式中的一种：

- input mode
- command mode, and
- last_line mode

每种模式现在将简要描述。

**Command Mode** 初始模式是命令模式。在 command_mode 中可以输入以下按键/命令：

| Key | Semantics |
|---|---|
| `i` | changes to input mode. |
| `:` | changes to lastline mode. |
| `h`, backspace, or left-arrow key | moves left until the first character in the text line. If a line wraps, it follows the wrapped text backwards. |
| `l`, spacebar, or right-arrow key | moves right until the last character in the text line. If a line wraps, it follows the wrapped text backwards. |
| `k` or up-arrow key | moves to the text line above, to the same position relative to the start of the text line, unless that text line is shorter than the current one, in which case it is placed at the end of the text line. Scrolling takes place as necessary. |
| `j` or down-arrow key | moves to the next text line below, using the same rule as for the up arrow when deciding the horizontal position. Scrolling takes place as necessary. |
| `Ctrl-D` | Does nothing except display the message that it was pressed. |
| `Ctrl-C` | Does nothing except display the message that it was pressed. |
| `Ctrl-H` | Can be used to display a help screen, but at present just shows a one-line text message. |

