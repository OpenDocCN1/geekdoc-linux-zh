

# 34 第一部分 Linux 入门步骤

原始 csh 的许多功能（例如命令行编辑和历史记录机制）都包含在 tcsh 以及其他 shell 中。虽然你可以在大多数 Linux 系统上同时运行 csh 和 tcsh，但这两个命令都指向同一个可执行文件。换句话说，启动 csh 实际上是在兼容模式下运行 tcsh shell。

## 使用 ash

ash 是 Berkeley UNIX shell 的轻量级版本。它不包含 sh shell 的许多基本功能，并且缺少命令历史记录等功能。Kenneth Almquist 创建了 ash。

对于资源较少的嵌入式系统，ash 是一个很好的 shell。ash shell 的大小约为 bash 的六分之一（ash 约为 100k，而 bash 为 680k）。由于如今内存价格便宜，许多嵌入式和小型 Linux 系统都有足够的空间包含完整的 shell。

## 使用 ksh

ksh 由 David Korn 在 AT&T 贝尔实验室创建，是 sh shell 的前身。它已成为 UNIX 系统中默认且最常用的 shell。ksh 的开源版本最初存在许多基于 rpm 的系统中（如 Fedora 和 Red Hat Enterprise Linux）。David Korn 将原始的 ksh 作为开源发布，因此你可以作为 Linux 系统中软件的一部分找到它。

## 使用 zsh

zsh shell 是另一个 sh shell 的克隆。它符合 POSIX 标准，但包含一些不同的功能，例如拼写检查和命令编辑。Mac OS 使用 zsh 作为默认 shell，尽管默认使用的是 bash。

## 探索 shell

一旦你在 Linux 中访问了 shell，就可以从输入简单命令开始。稍后的“在 Linux 中使用 shell”部分将提供更多关于选项、参数和环境变量的详细信息。目前，以下章节将帮助你进行探索。

## 从 shell 运行命令

如果你不喜欢默认的 shell，只需输入你想要尝试的 shell 名称即可。要永久更改 shell，请使用 usermod 命令。例如，要将名为 chris 的用户的 shell 改为 csh，请输入：

```bash
usermod -s /bin/csh chris
```

## 检查登录会话

当你登录 Linux 系统时，Linux 将你视为具有特定的身份，包括你的用户名、组名、用户 ID (uid) 和组 ID (gid)。Linux 还会跟踪你登录的时间、空闲时长以及登录的位置。要查找你的身份，请按如下方式使用 id 命令：

```bash
$ id
uid=501(chris) gid=105(sales) groups=105(sales),4(adm),7(lpd)
```

在此示例中，用户名是 chris (uid=501)。chris 的主组是 sales (gid=105)。用户 chris 还属于其他组 adm (4) 和 lpd (7)。这些名称和数字代表了 chris 访问资源的权限。

你可以使用 who 命令查看有关当前登录会话的信息。-u 选项添加了关于空闲时间和进程的信息，并会打印一个表头：

```bash
$ who -u
NAME TIME IDLE PID COMMENT
chris tty Jan 13 20:57 .
```

who 的输出显示用户已登录到 tty (which) ，登录会话于 1 月 13 日 20:57 开始。空闲时间显示了 shell 打开后多久没有输入任何命令（点号 `.` 表示表示当前处于激活状态）。PID 显示用户的进程 ID。COMMENT 显示用户登录的远程计算机名称，或者如果你使用终端 窗口（如 :0），则显示本地名称。

## 检查目录和权限

每个 shell 都关联着 Linux 文件系统中的一个位置，称为当前目录或工作目录。每个用户都有一个标识为用户主目录的目录。当你首次登录 Linux 时，你从主目录作为当前目录开始。

当你想要打开或保存文件时，你的 shell 使用当前目录作为参考点。保存文件时只需提供文件名，它将被放置在当前目录（相对路径）。或者，你可以通过文件与当前目录的关系（相对路径）来识别文件，也可以忽略当前目录并通过完整的目录层次结构（绝对路径）来识别文件。文件系统的结构和用法在本章稍后详细描述。

要查找当前所在的目录，输入 pwd 命令：

```bash
$pwd
/usr/bin
```

在此示例中，当前工作目录是 /usr/bin。要查找你的主目录名称，使用 echo 命令后接 $HOME 变量：

```bash
$ echo $HOME
/home/chris
```

这里的主目录是 /home/chris。要返回主目录，只需输入切换目录 (cd) 命令。（虽然在 cd 后加上目录名会将当前目录更改为你选择的目录，但在不带目录名的情况下输入 cd 将带你回到主目录）：

```bash
$ cd
```

> **注意：** 代替输入 $HOME，可以使用波浪号 (~) 来引用你的主目录。因此，要返回主目录，你只需输入：`cd ~`

要列出主目录的内容，可以使用主目录的完整路径，或者使用不带目录名的 ls 命令。使用 -a 选项允许你看到隐藏文件（点文件）以及所有其他文件。使用 -l 选项，你可以看到每个文件的详细长列表。（你可以在单个横杠后组合多个单字母选项，例如，-la）。

```bash
$ ls -la /home
total 16
drwxr-xr-x 2 chris sales 4096 Jan 13 20:57 .
drwxr-xr-x 4 root root 4096 Jan 13 20:00 ..
-rw-r--r-- 1 chris chris 920 Jan 13 20:57 .bash_history
-rw-r--r-- 1 chris chris 1200 Jan 13 20:57 .bash_profile
-rw-r--r-- 1 chris chris 800 Jan 13 20:57 .bashrc
-rw-r--r-- 1 chris chris 1500 Jan 13 20:57 .bashlogout
```
