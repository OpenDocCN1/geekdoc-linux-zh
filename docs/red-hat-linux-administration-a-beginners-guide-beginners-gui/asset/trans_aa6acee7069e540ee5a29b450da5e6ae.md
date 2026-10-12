
例如，如果你是以自己的身份登录并希望切换到 root 用户，请输入以下命令：

```
[michael@workbox michael]$ su
```

如果你是以 **root** 身份登录并希望切换到用户 **rwhite**，请输入以下命令：

```
[root@workbox michael]# su rwhite
```

可选的连字符（-）参数会告诉 **su** 切换身份并运行该用户的登录脚本。例如，如果你是以 **root** 身份登录并希望切换到用户 **rwhite** 并使用他的所有登录和 shell 配置，请输入以下命令：

```
[root@workbox michael]$ su - rwhite
```

本模块涵盖的一些命令只能由 **root** 用户使用。然而，以 **root** 身份登录进行所有操作是一种不良实践。你应该只**root** 需要时才使用。像 **su** 这样的命令让你更容易临时成为 **root** 以完成必要任务，并在完成后退出。

### 关键技能 6.2 使用 BASH Shell

在模块 5 中，你了解到用户密码条目中的一个参数是该用户的*登录 shell*，即用户登录工作站时运行的第一个程序。shell 类似于 Windows 程序管理器，区别在于所使用的 shell 程序当然是任意的。

*shell* 只是一个提供系统接口的程序。UNIX 系统中最初的通用 shell 是 Bourne shell，通常简称为*sh*。Bourne Again Shell（BASH）是一个基于原始 Bourne shell 的自由软件 shell，但增加了一些增强功能。它是一个仅支持命令行的接口，包含少量内置命令，能够启动其他程序，并能够控制从它启动的程序（作业控制）。可以将其想象成增强了功能的 command.com 或 cmd。

存在多种 shell，大多数具有类似的功能但实现方式不同。为了便于比较，你可以将各种 shell 想象成 web 浏览器；在不同的浏览器中，基本功能都是相同的——显示网络内容。在这种情况下，每个人都声称他们的 shell 比其他的好，但这其实主要取决于个人偏好。

在本节中，你将了解 BASH 的一些内置命令。BASH 的完整参考手册本身就足以写成一本书，因此在本模块中，我们将重点关注对系统管理员日常操作影响最大的命令。不过，我建议你最终深入学习 BASH 的操作。关于此主题的优秀书籍不计其数。

## 作业控制

在 BASH 环境中工作时，你可以从同一个提示符启动多个程序。每个程序都是一个作业。每当启动一个作业时，它会接管终端。（这是对早期使用实际哑终端（如 VT-100 和 Wyse-50）与机器交互时代的回顾。）在今天的机器上，终端要么是你启动机器时看到的纯文本接口，要么是运行 BASH 的 X Window System 创建的窗口。（X 中的终端接口称为伪 tty，简称为 pty。）如果某个作业控制终端，它可以发出控制代码，使纯文本接口（例如 pine 邮件阅读器）更加美观。程序完成后，它将完全控制权交还给 BASH，并重新显示用户提示符。

然而，并非所有程序都需要这种终端控制。有些程序，包括通过 X Window System 与用户交互的程序，可以被指示放弃终端控制，并允许 BASH 显示用户提示符，即使被调用的程序仍在运行。在下面的示例中，Mozilla 接受了这样的指令，由 & 后缀表示：

```
[michael@workbox michael]$ mozilla &
```

按下 ENTER 键后，BASH 会立即显示提示符。这称为将任务置于后台。记得 4.0 版本之前的 Windows NT 的人会记得，使用“开始”命令时也需要做类似的事情。

如果一个程序已经在运行并控制终端，你可以按 CTRL-Z 使该程序放弃控制权。这将完全停止正在运行的作业并将控制权返回 BASH，以便你可以输入新命令。

在任何时候，你都可以输入以下命令来了解 BASH 正在跟踪多少个作业：

```
[michael@workbox michael]$ jobs
```

列出的运行程序将处于两种状态之一：运行中或已停止。如果某个作业已停止，你可以让它在后台运行，从而允许你保留对终端的控制。或者，已停止的作业可以在前台运行，这将把终端控制权交还给该程序。

要在后台运行作业，请输入：

```
[michael@workbox michael]$ bg number
```

其中*number*是你想要置于后台的作业编号。如果省略编号，则假设是最近的作业。要在前台运行作业，请输入：

```
[michael@workbox michael]$ fg number
```

其中**number**是你想要置于前台的作业编号。同样，省略编号将指向前一个最近停止的作业。

> **注意** 你无法（有效地）将需要通过与终端窗口交互才能完成任务的后台化。

## 环境变量

每个运行中的 shell 实例都有其自己的“环境”——赋予其特定外观、感觉，在某些情况下甚至行为的设置。这些设置通常由*环境变量*控制。一些环境变量对 shell 有特殊含义，但没有什么阻止你定义自己的变量并将其用于自己的需求。正是通过环境变量的使用，大多数 shell 脚本才能做有趣的事情，并记住用户输入的结果以及程序的输出。如果你已经熟悉 Windows NT/2000/.NET Server 中环境变量的概念，你会发现你知道的许多内容也适用于 Linux；唯一的区别在于它们是如何设置、查看和移除的。

### 显示环境变量

要列出所有环境变量，请使用 **printenv** 命令。例如：

```bash
[michael@workbox michael]$ printenv
```

要显示特定的环境变量，请将变量作为 **printenv** 的参数指定。例如，这是查看环境变量 OSTYPE 的命令：

```bash
[michael@workbox michael]$ printenv OSTYPE
```

### 设置环境变量

要设置环境变量，请使用以下格式：

```bash
[michael@workbox michael]$ variable=value
```

其中*variable*是变量名，*value*是你想要赋予变量的值。例如，这是设置环境变量 FOO 为 BAR 的命令：

```bash
[michael@workbox michael]$ FOO=BAR
```

值设置后，使用 **export** 命令来最终确定它。**export** 命令的格式如下：

```bash
[michael@workbox michael]$ export variable
```

其中*variable*是变量名。在设置 FOO 的示例中，你会输入此命令：

```bash
[michael@workbox michael]$ export FOO
```

使用 **BASH**，你可以将设置环境变量的步骤与 **export** 命令结合，如下所示：

```bash
[michael@workbox michael]$ export FOO=BAR
```

如果要设置的环境变量值包含空格，请用引号包围变量。使用前面的示例，要将 FOO 设置为“Welcome to the BAR of FOO.”，你会输入：

```bash
[michael@workbox michael]$ export FOO="Welcome to the BAR of FOO."
```

### 取消设置环境变量

要移除环境变量，请使用 **unset** 命令：

```bash
[michael@workbox michael]$ unset variable
```

其中*variable*是你想要移除的变量名。例如，这是移除环境变量 FOO 的命令：

```bash
[root@tedford]# unset FOO
```

> 本节假设你使用的是 **BASH**。还有许多其他 shell 可供选择；最流行的替代方案是 **C-Shell** (csh) 及其兄弟 **Turbo C Shell** (tcsh)，它们使用不同的机制来获取和设置环境变量。有关更多信息，请阅读你偏好的 shell 的手册页[请参见本模块后面“man 命令”部分]。我在这里记录 **BASH** 是因为它是所有新 Linux 账户的默认 shell。

