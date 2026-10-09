
## 安装 VirtualBox 增强功能

![](img/d05aeb75f1c36187913c3b410abf92b1_18_0.png)

在终端中，输入以下命令并按下回车键。

```
cd /media/cdrom/
```

现在，键入以下命令并按下回车键。

```
sudo sh VBoxLinuxAdditions.run
```

系统现在会要求输入 Kali 的 sudo 密码，请从键盘上键入 “kali”。你输入的密码不会显示在屏幕上，但你必须自信地从键盘上键入 “kali” 并按下回车键。

将会出现几个命令处理过程，如果系统询问 “是或否”，请键入 “y” 并按下回车键。

VirtualBox Linux 增强功能现在已成功安装到你的 Kali Linux 机器上。

现在，重启你的 Kali Linux，你可以在终端中输入命令 “reboot” 或使用 Kali 中的电源图标来实现。

![](img/d05aeb75f1c36187913c3b410abf92b1_19_0.png)

现在，分别输入用户名和密码 “kali” 和 “kali”，如前所述。

Kali 现已设置完成，可以使用了。你可能已经注意到我们之前使用了一些像 “cd”、“sh”、“sudo” 这样的命令。这些是在终端中执行任务时附加的基本命令。让我们在下一节中讨论一些命令。

## Linux 命令

我们将讨论在 Kali Linux 中入门所需的一些基本命令。

### 1. cd

此命令用于在终端中更改目录。它用于目录的路径，例如，将当前目录更改到桌面目录，我们会使用
`cd Desktop/`

![](img/d05aeb75f1c36187913c3b410abf92b1_20_0.png)

若要返回上一级目录，请使用命令
`cd ..`

![](img/d05aeb75f1c36187913c3b410abf92b1_21_0.png)

### 2. pwd

此命令用于打印终端正在运行的工作目录。你只需键入 pwd 并按下回车键即可。

![](img/d05aeb75f1c36187913c3b410abf92b1_22_0.png)

默认情况下，当我们使用终端图标打开终端时，它会打开在 “/home/kali” 目录中。因此，写入 pwd 会输出 “/home/kali”。

尝试将目录更改为 “Desktop/” 并打印工作目录。

### 3. ls

此命令用于列出当前工作目录内的文件夹和文件。此命令可以单独使用。键入 “ls” 并按下回车键，它会输出目录中你正在运行的终端内的文件夹和文件。

![](img/d05aeb75f1c36187913c3b410abf92b1_23_0.png)

因为，我们当前在目录 “/home/kali/” 中运行终端，其中包含 Desktop、Documents 及其他文件夹。

尝试使用 “cd” 命令进入其他目录并打印工作目录。

你还可以键入

```
cd /
```

这将活动目录更改为系统文件所在的主目录。

有几种方法可以做到这一点，

首先，

![](img/d05aeb75f1c36187913c3b410abf92b1_23_1.png)

其次，

![](img/d05aeb75f1c36187913c3b410abf92b1_24_0.png)

你可以查看输出结果。有多个文件夹，如 bin、dev、home 等。

“home” 文件夹包含重要的用户文件夹，即 “kali”

你可以通过键入 “cd /home/kali/” 返回 kali 目录。这将工作目录更改为你启动终端时打开的默认目录。

如果你想了解 “/” 文件夹包含的每个文件夹，请查看此链接 https://www.linux.com/training-tutorials/linux-filesystem-explained/ 。

### 4. clear

这是一个简单命令，清除终端上显示的所有内容。终端内部可能会有一些杂乱无章的内容，可能需要你关闭并重新打开终端，但键入 clear 命令只会清除文本内容。

### 5. sudo

这是 Kali 终端中最重要的命令。此命令为你提供 root 权限，或者我们可以说你已经获得了超级用户访问权限。如果你曾经尝试让你的安卓设备获取 root（越狱）权限（尽管不建议这样做），你可能听说过超级用户（SU box）。

Kali 中有一些工具需要 root 权限才能工作，否则它们会输出 “bash, command not found” 或 “请运行此命令时拥有 root 权限”。为了给这些工具提供 root 权限，我们必须在其后附加 “sudo”。之后你还需要输入密码 “kali”，正如我们在安装 VirtualBox 增强功能工具时所做的那样。我们将在下一个命令中更多地讨论 sudo。

### 6. ifconfig

此命令用于显示在 Kali 内部运行的活动网络适配器。尝试输入以下命令并按下回车键。

`ifconfig`

你可能会收到 “bash, command not found” 的错误。这是因为 “ifconfig” 命令至少需要 root 权限一次。尝试输入命令

`sudo ifconfig`

这将显示一些 IP 地址和 MAC 地址。这些 IP 和 MAC 地址在无线攻击和执行远程执行攻击（如 MSF venom、beef 等）中非常关键。如果你想执行无线攻击或破解无线路由器密码，你可以阅读我们在 Kali 中关于无线攻击的最终指南。

既然我们拥有了 root 访问权限，那么每次输入需要 sudo 或 root 访问的命令时，我们是否都需要输入 sudo 呢？

答案是：不需要！

你可以切换到 root 模式，并在每条命令前不写 sudo 的情况下输入任意数量的 root 命令。可以通过键入命令来实现

```
sudo su
```

这将使你进入 root 权限目录，即 root 目录。

![](img/d05aeb75f1c36187913c3b410abf92b1_26_0.png)

现在，你可以在每次输入 sudo 之前运行任意数量的 root 命令。要退出 root 模式，请输入

```
exit
```

并按下回车键。这将返回到普通用户模式。

### 7. touch

此命令用于在活动目录中创建一个文件。
让我们创建一个名为 “newfile” 的文件。为此，请输入命令

```
cd Desktop/
(将活动目录更改为 Desktop)
touch newfile
```

这将在桌面上创建一个名为 newfile 的空文件。
双击该文件，看看它是否是空的。目前它肯定是空的。

![](img/d05aeb75f1c36187913c3b410abf92b1_27_0.png)

### 8. nano

此命令用于使用终端编辑器编辑文件。这与文本编辑器不完全相同，但当编辑无法使用普通文本编辑器编辑的 root 级别文件时，它是一个方便的命令。
输入命令
`nano newfile`
这将打开一个终端编辑器。在那里输入 “Hello World” 文本。

![](img/d05aeb75f1c36187913c3b410abf92b1_28_0.png)

输入这些内容后，使用键盘按下 “Ctrl O”，然后按下 “Enter” 键。最后按下 “Ctrl X”。这些按键组合将把你带出终端编辑器，同时保存你输入的内容。

“nano” 命令也可以直接用于创建文件，而不需要使用 “touch” 命令。

若要使用 nano 命令创建文件，请输入

```
nano anotherfile
```

这将创建一个名为 “anotherfile” 的新文件，但你需要输入一些内容并保存该文件，该文件才会出现在活动目录中。

输入 “Hello There”，按下 “Ctrl O”，然后按 “Enter Key”，再按 “Ctrl X”。这将保存文件，并且该文件将出现在活动目录中。

以下是我们使用上述方法创建的两个文件。

![](img/d05aeb75f1c36187913c3b410abf92b1_29_0.png)

尝试双击桌面上的这些文件，看看每个文件是否包含我们写入的文本。

### 9. echo

此命令用于将任何文本或代码输入到指定文件中。其工作原理与 nano 终端编辑器相同。

让我们创建一个新文件名为 “file1”，并使用 “echo” 命令将文本 “Have a Great Day” 插入到 “file1” 中。

```
(kali@kali)-[~/Desktop]
$ touch file1

(kali@kali)-[~/Desktop]
$ echo Have a Great Day > file1

(kali@kali)-[~/Desktop]
$ 
```

这将创建一个名为 “file1” 的文件，并将 “Have a Great Day” 插入其中。

### 10. cat

此命令用于在终端中显示文件内容。

到目前为止，我们已创建了 3 个文件。

让我们使用此命令显示每个文件的内容。

为此，请输入以下命令，并在每条命令后按下回车键。

```
cat newfile
cat anotherfile
cat file1
```

