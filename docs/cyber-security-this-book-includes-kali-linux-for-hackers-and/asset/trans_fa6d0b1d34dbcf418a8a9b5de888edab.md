
## Level 1 题目

登录名：level18
密码：newworld
学习内容：外部命令与管道符的执行。

本阶段所需掌握的核心知识是了解如何利用那些执行外部命令的程序。如果该程序的有效用户 ID（EUID）高于你的，这将带来严重的安全隐患。为了进行演示，让我们参考 level0 的例子。我将创建一个虚拟的 level1，并使用一些虚拟文件作为测试。

```text
Login: level18
[level1 @ level1] $ find -user level2 -group level1 2> /dev/null
/usr/bin/list
[level1 @ level1] $ cd /usr/bin
[level1 @ level1 bin] $ ./list
Enter a file: /usr/bin/list
-rwxr-xr-x  level2 level1 876 Jun 23 13:12 /usr/bin/list
```

让我们仔细看看刚才的操作。我们本应登录到 HackersLab 系统，然后查找拥有 level2 UID 和 Level1 GID 的文件（如果你仍然不明白为什么要这样搜索，请重读 level0）。我们找到了文件 `/usr/bin/list`。我尝试运行它并成功了。它要求我输入任意文件，并告知我同样的信息，正如我们之前使用的那样，只是为了看看会发生什么（实际上可以是任何文件）。随后，list 程序返回了关于我提供的文件的信息。问题就出在这里。从内部执行 list 的命令实际上是 `ls -l`，用于显示文件信息。它在系统上执行了以下操作：

```text
[level1 @ level1] $ ls -la /usr/bin/list
-rwxr-xr-x  level2 level1 876 Jun 23 13:12 /usr/bin/list
```

但它是以高于我们的权限执行的（忘了你的创造性用户和 ID 是 level2 吗???）。既然它外部执行 ls，我们该如何添加另一个命令呢？最简单的方法是使用管道符（`|`），我们在命令章节中见过它。它允许你输入另一个待执行的命令。但我们要在哪里做呢？让我们再次运行 list：

```text
[level1 @ level1 bin] $ ./list
Enter a file: /usr/bin/list
```

这里就是秘密所在。除了仅仅输入文件的 PATH，我们能否在前面加上管道符和某些命令？就像这样：

`Enter a file: /usr/bin/list | pass`

就是这样！如果我们的理论正确，它将运行 `ls`，列出我们的程序 `/usr/bin/list`，然后立即运行提供密码的程序。现在完成：

```text
[level1 @ level1 bin] $ ./list
Enter a file: /usr/bin/list | pass
-rwxr-xr-x  level2 level1 876 Jun 23 13:12 /usr/bin/list
The password for level2 is ...
```

准备就绪！我们获得了新的密码。现在让我们进入真实的 walkthrough。

### 分步操作
- 登录到 HackersLab 并使用 level1 密码登录。
- 首先要做（已经成了经典套路）是输入命令 `find / -user level2 -group level1 2>/dev/null` 来查找目标文件。
- 我们找到了两个文件：`/proc/20840` 和 `/usr/bin/amos`。
- 但等等……Amos 是一位先知的名字（叮叮，叮叮……我们发现为什么这个提示级别是这样的了）。
- 让我们检查一下 amos 文件，然后：

通过查看来自管理员的信息，我们发现再次拥有执行该文件的组权限（`x`）。我们成功运行了它，无需在前面加“./”（斜杠），这意味着它在 PATH 中。在我们的学习会话模拟中这是如何发生的？程序要求我们输入任意文件的 PATH。我们输入了当前正在运行的文件（如前所述，可以是任何文件）。它通知我们该文件是可执行的。

回到本阶段的问题，我们看到 Matthew 必须使用 file 命令来生成 amos 程序。那么，程序是否在外部运行文件归档？是的？让我们试一试！是的！！示例在外部运行了文件。让我们尝试运行它，并制作一个管道来尝试获取你的权限。所以让我们以我们学习的方式进行：我们输入 `/usr/bin/amos` 的信息，`|`（管道符）以及 `pass` 命令。因此，程序将处理文件 `/usr/bin/amos|pass`。结果如何？level2 的密码。又赢了一个阶段。

## Level 2 题目

Kevin，一位 BBS 程序员，希望在你的主页上添加一个警报，以便你的成员每次登录时都能看到你的帖子。不幸的是，该消息有多页，且他的成员无法阅读。结果，他日夜挠头，试图找到一个解决方案。最后，他考虑使用 more 命令来解决这个问题。然而，由于安全问题，这种方法是有风险的。

提示：无须多言！

**登录名：level2**
**密码：DoItYourself**
**学习内容：Shell 与子 Shell**

系统的 Shell 不过就是执行输入的 Shell 解释器命令。它是一个文本模式屏幕，你可以通过系统命令与之交互。例如在 DOS 系统中，命令解释器是 `command.com` 文件。在 Windows NT 及兼容系统中，它是 `cmd.exe`。你可以在 NT 上通过进入 开始/运行 并输入 `cmd` 来证明这一点。将会打开一个命令屏幕。

为什么要用 Windows 作为例子？为什么 Linux 没有接近的不同之处。它有几种 shell 类型（sh, csh, ksh, bash2 ...），当在图形窗口管理器（如 GNOME 或 KDE）内运行时，会给你一个另一个小的文本模式窗口，即命令提示符老板。结束它很简单。只需关闭它即可。当你在窗口管理器内运行 shell 时，你将在后台运行。这是一个重要的概念，因为我们要稍后大量使用它。我还可以在一个 shell 内运行另一个 shell。这被称为子 shell。下面是一个例子：

```text
[my system] $ ls
....
rohtspasswd.old
[my system] $ /bin/sh
bash $
```

在上面的例子中，我在一个 shell（展示我拼写的系统）中，然后移动到另一个 shell，sh（或简单的 bash）。如果我输入 exit 命令，我会回到上一个 shell。这证明了 sh 是一个子 shell，因为它是在最初运行的 shell 内部运行的。

```text
bash $ exit
[my system] $
```

这也可以通过程序完成。许多在 shell 上运行的文本模式程序（如 pine, vi 和其他）允许你从内部运行子 shell。甚至像 more 这样的命令也允许。这将在本级别的实践部分中变得清晰。

### 分步操作
- 我们连接到 HackersLab 并尝试列出具有 level3 用户权限和 level2 组权限的文件。
- 我们找到了 alert 文件。大概是从本级别描述中之前创建的那个。
- 下一步：列出它。执行它。让我们做。

我们运行了 alert 文件，发现 Kevin 使用 more 命令在你的文件屏幕之间暂停。如果我们按下 Enter，Page Down 和其他一些键，文件将继续缓慢显示。相反，我们将执行以下操作：我们在 `--More--` 上写下命令 `! /bin/sh`。这意味着告诉系统：亲爱的 Linux，运行（`!`）bin 目录（`/bin/sh`）内的命令解释器 sh。我们跌入了 shell。因为谁正在运行 shell 是一个具有 level3 权限的程序，我们用 `whoami` 测试，发现已经是 level3 就绪了。运行 `pass`，就这样，我们到达 level3！

## Level 3 题目

登录名：level3
密码：hackerproof
学习内容：PATH 和 IFS HackersLab

Level 3 和 Level 4 几乎是一样的，在这两个级别中，你需要理解 PATH、IFS 和 export 的概念。这些级别在挑战的早期部分确实非常有趣且困难（你稍后会发现 level5 和 6 要容易得多）。虽然这本书侧重于如何破解 Linux 系统，但我将简要解释 PATH。学习这个术语使理解其他术语更容易。首先，让我们进入概念：

PATH 是目录的绝对路径，系统总是在这些目录中查找要运行的文件。例如，在系统根目录中输入命令 `ls`、`dir`、`date` 或任何其他命令，操作系统将按这些命令搜索 PATH 目录并执行它们。如果没有，它将返回错误。复杂吗？没那么复杂。

让我们看一个简单的例子。在上面的 DOS 例子中，我列出了名为 test director 的目录中的数据。我发现有一个名为 `app.exe` 的程序。然后我尝试从根目录运行 app。我收到一个错误，说命令未被识别（未找到）。因此，我修改了 PATH 并将其指向 app 所在的 test director。只需使用 `PATH = C:\directory\test`。我再次尝试运行 app，瞧！它正常运行了。当然，现在命令在系统搜索的 PATH 内部。

好的，但这与黑客挑战有什么关系？全部。想象一个 Windows 应用程序外部调用 `send NET.EXE`（控制 NetBIOS 协议的命令，可能连接到共享、发送消息、启用用户等）。如果我自己创建了另一个同名文件（`NET.EXE`），把它放在 test director 并设置 PATH，会发生什么？`NET` 将由个人程序正常调用，但我的 `NET`，可能是一个入侵程序，如后门（或木马）。

回到 Linux，那么想象 Steven 的程序只是写入日期。这很容易，只需在目录中创建一个伪造版本

