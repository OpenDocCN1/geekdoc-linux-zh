

启动序列负责将 Linux 操作系统引导至对用户可用的状态，以便用户可以登录并开始使用系统执行任务。

## systemd

systemd 被称为 Linux 操作系统中所有进程的“母亲”。它负责启动 Linux 操作系统并将其引导至可用状态。在开发 systemd 服务之前，这一任务是由 init 服务执行的，但相比 init，systemd 拥有更多功能，例如初始化和管理系统服务、挂载文件系统等等。

systemd 的首要任务是挂载配置文件 /etc/fstab 中定义的所有文件系统。systemd 还可以访问存储在 /etc 目录中的其他所有配置文件。systemd 会将系统带入由存储在 /etc/systemd/system/default.target 文件中的定义状态或目标。如果是桌面环境，默认目标通常是 graphical.target；如果是 Linux 服务器，默认目标通常是 multi-user.target。

目标（Targets）和服务（Services）是 systemd 服务的单元。目标的配置文件定义了该特定目标的依赖项。systemd 会初始化这些依赖项。这些依赖项指的是基于已初始化的目标运行 Linux 操作系统所需的服务。当 systemd 加载完所有目标的依赖项后，可以说系统已启动并运行，或者系统正在该特定目标级别下运行。

启动序列有两个检查点：sysinit.target 和 basic.target。虽然 systemd 是并行启动服务的，但事实是某些服务需要在其他服务之前初始化。只有当特定检查点的所有服务和目标都成功初始化后，该检查点才算通过。

只有当其所有服务和目标都成功初始化后，才会到达 sysinit.target 检查点。sysinit.target 有多个依赖项，这些依赖项在 sysinit.target 内部并行初始化。

sysinit.target 首先启动所有达到 basic.target 所需的低级服务。然后 basic.target 会初始化一些额外的服务以到达下一个目标。

一旦成功到达这两个检查点，系统就可以移动到 **graphical.target** 或 **multi-user.target**。但请注意，即使 graphical.target 的依赖项尚未初始化，Linux 系统也可以先到达 multi-user.target。

如果默认目标设置为 multi-user.target，你将看到基于文本的登录提示符。该目标常用于安装了不带图形界面的 Linux 的服务器。如果你在个人桌面上安装了 Linux 并包含了 GNOME 桌面环境，默认目标将是 graphical.target。在这种情况下，你将看到一个图形界面用于登录 Linux 桌面。

至此，启动序列结束。你可以简单地在那基于文本的登录提示符或图形界面登录屏幕上输入你的用户名和密码，开始使用你的 Linux 系统。

每个现代的 Linux 操作系统都以 GRUB2 和 systemd 作为其核心组件。这两个组件协同工作以加载 Linux 内核、启动服务并使 Linux 系统对任何最终用户可用。

# 第十一章

## Shell 脚本简介

为 Linux 开发的开源编程语言被称为 Shell 脚本。简单来说，Shell 脚本是一系列单独的 Linux 命令组合在一起以自动执行。Shell 脚本可以包含单行或多行代码，这些代码存储在单个文件中，这样用户在需要执行特定任务时无需每次手动输入。

本章将向你介绍 Shell 脚本的基础知识，并简要讨论一些 Shell 脚本的高级概念。本章将作为你进入 Shell 脚本世界的垫脚石。

## 编写 Shell 脚本

你可以使用文本编辑器来编写 Shell 脚本。Linux 有一套内置的文本编辑器，如 nano、vi 和 vim。你可以使用其中任何一个开始编写 Shell 脚本。你需要确保的一件事是你创建的用于 Shell 脚本的文件是可执行的。你可以通过对文件名运行以下命令来使任何文件可执行。

```bash
$ chmod a+x filename.sh
```

然后，你只需将文件存储在一个 Linux 操作系统可以轻松访问的位置。

创建 Shell 脚本的步骤如下。

- 1. 使用你选择的文本编辑器创建一个新文件。将脚本文件保存为 .sh 扩展名。
- 2. 脚本文件的第一行应始终是 #!/bin/sh
- 3. 输入一些 Linux 命令。
- 4. 将文件保存为 filename.sh
- 5. 在 Linux shell 上使用以下命令执行你的脚本。

```bash
bash filename.sh
```

#! 被称为 shebang 运算符。它告诉脚本 Linux 系统解释器的位置。当你在 shell 脚本的第一行输入 #!/bin/sh 时，Linux 操作系统知道执行该脚本的解释器位于 /bin/sh

让我们创建一个简单的 shell 脚本。

```bash
#!/bin/sh
ls
```

将此脚本保存为 list.sh

你可以在 shell 上使用以下命令运行此脚本。

```bash
[student@desktop ~]$ bash list.sh
```

Documents Movies Books Pictures

此脚本的结果是 `ls` 函数，它列出了目录的内容。

## 为脚本添加注释

注释用于每种编程语言，shell 脚本也不例外。你可以使用以下语法为你的 shell 脚本添加注释。

```bash
#this is a comment
```

如果我们以上面的脚本为例，你可以这样添加注释。

```bash
#!/bin/sh
#this is my first script
```

## ls

你也可以在 shell 脚本中添加多行注释。你可以通过将注释放在 `:'` 和 `'` 之间来实现。

考虑下面的例子。

```bash
#!/bin/bash
:'
  This script calculates
  the square of 5.
'
((area=5*5))
echo $area
```

因此，`:'` 和 `'` 之间的字符串，即此脚本计算 5 的平方，在脚本中被注释掉了。

## Shell 变量

任何编程语言中的变量都用于以字符和数字形式存储数据。Shell 脚本也支持变量，这些变量存储的数据可以被 Linux shell 访问。

例如，下面的简单示例显示了一个存储一些数据然后打印它的变量。

```bash
variable ="Hello"
echo $variable
```

让我们看另一个使用变量的 shell 脚本示例。

```bash
#!/bin/sh
echo "what is your name?"
read name
echo "How do you do, $name?"
read remark
echo "I am $remark too!"
```

## 这个脚本是如何工作的？

当你运行这个脚本时，系统会打印问题，“what is your name?”

然后你会看到系统正在等待你的输入。如果你输入 Mark，字符串 Mark 就会被存储在变量 **name** 中。在下一行代码中，脚本使用提供的名字来问下一个问题，“How do you do Mark?” 其中变量 **name** 被替换为你之前输入的字符串。系统再次期望你输入这个答案。当你输入时，它会被存储在另一个名为 **remark** 的变量中。所以如果你的回答是“fine”，脚本将在下一行代码中用你的字符串替换变量 **remark**，并打印输出为“I am fine too!”

## 更多 Shell 脚本示例

### 你好世界

每个人学习新编程语言时输入的第一个程序通常是 Hello World。它是一个简单的程序，将打印输出“Hello World。”使用 nano 或 vim 等文本编辑器创建一个名为 helloworld.sh 的文件，并在其中输入以下代码。

```bash
#!/bin/bash

echo "Hello World"
```

保存文件并更改文件权限使其可执行。

```bash
$ chmod a+x hello-world.sh
```

现在运行以下其中一个命令来运行你的脚本。

```bash
$ bash hello-world.sh
```

