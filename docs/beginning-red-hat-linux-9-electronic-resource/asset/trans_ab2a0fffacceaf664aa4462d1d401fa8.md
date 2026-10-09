

# 创建、移动和删除文件与目录

在创建和删除方面，目录和文件处理方式不同，因此我们将分几个小节来解释。

## 创建和删除目录

我们分别使用 `mkdir`（make directory，创建目录）和 `rmdir`（remove directory，删除目录）来创建或删除目录。以下示例在当前工作目录下创建一个名为 `grapple` 的子目录：

```bash
$ mkdir grapple
```

也可以一次性创建整个目录层级结构。为此，我们使用 `-p` 选项。例如，该命令会创建目录 `4wds`（作为 `vehicles/cars` 目录的子目录），但如果 `vehicles` 和 `cars` 目录尚不存在，它*也会*创建这两个目录：

```bash
$ mkdir -p vehicles/cars/4wds
```

默认情况下，`rmdir` 命令只能删除空目录——即没有包含任何文件的目录。这是为了帮助我们避免删除那些我们不一定知道存在的文件而设计的：

```bash
$ rmdir grapple
```

若要递归删除目录及其内容（包括子目录），我们可以使用 `rm -r` 命令：

```bash
$ rm -r vehicles
```

## 创建和删除文件

创建文件的一种快速方法是使用 `touch` 命令。`touch` 命令的实际目的是更新现有文件的时间戳（其理念是，如果你“触碰”了文件，操作系统应该会更新时间戳）。这一操作的一个副作用是，如果你指定了一个尚不存在的文件路径，Linux 也会创建一个空文件：

```bash
$ touch tigers.txt
```

要删除文件，我们使用 `rm`（remove，删除）命令：

```bash
$ rm tigers.txt
```

## 移动文件和目录

要移动文件或目录，我们使用 `mv`（move，移动）命令。这需要两个参数——要移动的文件或目录，以及目标位置：

```bash
$ mv squidgy.txt squeezy.txt
```

这是一个“移动文件”的经典示例。在此例中，我们使用 `mv` 并不是将文件移动到不同的目录，而是简单地*更改*文件的*名称*。在 Linux 中，“移动”文件实际上意味着“更改其路径”。

同时也支持同时移动多个文件。例如，该命令将当前工作目录下的文件 `squeezy.txt` 和 `stodgy.txt` 移动到目录 `/etc/textures`：

```bash
mv squeezy.txt stodgy.txt /etc/textures
```

## 试一试：创建、移动和删除文件与目录

让我们通过一个简单的示例逐步操作：首先创建一个包含文件的目录，然后重命名该文件。实验结束后，我们将通过删除文件和目录来清理所有内容。

- 1. 将当前工作目录更改为你的家目录。例如，如果你使用用户名 `deepakt` 登录，则只需输入以下命令：

  ```bash
  $ cd
  ```

- 2. 为了检查上一步是否成功，使用 `pwd` 查看当前工作目录：

  ```bash
  $ pwd
  /home/deepakt
  ```

- 3. 现在创建一个名为 `test` 的子目录，并将其设为工作目录：

  ```bash
  $ mkdir test
  $ cd test
  ```

- 4. 现在创建一个名为 `nomme.txt` 的新文件：

  ```bash
  $ touch nomme.txt
  ```

- 5. 为了证明 `touch` 命令确实创建了新文件，你可以使用 `ls` 命令列出 `test` 目录的内容：

  ```bash
  $ ls -al
  total 4
  drwxr-xr-x      2 deepakt users          0 Jan 16 17:29 .
  drwxr-xr-x      3 deepakt users       4096 Jan 16 17:29 ..
  -rw-r--r--      1 deepakt users          0 Jan 16 17:29 nomme.txt
  ```

- 6. 现在使用 `mv` 更改文件名称，并再次使用 `ls` 检查更改：

  ```bash
  $ mv nomme.txt name.txt; ls -al
  total 4
  drwxr-xr-x      2 deepakt users          0 Jan 16 17:29 .
  drwxr-xr-x      3 deepakt users       4096 Jan 16 17:29 ..
  -rw-r--r--      1 deepakt users          0 Jan 16 17:29 name.txt
  ```

  > *注意，我们在 mv 命令后使用了分号 (;) 并输入了 ls 命令。*
  > **分号用于分隔同一行上的多个命令。**

- 7. 接下来，我们将开始清理工作。使用 `rm` 删除文件 `name.txt`，并使用 `ls` 进行检查：

  ```bash
  $ rm name.txt
  $ ls -al
  total 4
  drwxr-xr-x      2 deepakt users          0 Jan 16 17:29 .
  drwxr-xr-x      3 deepakt users       4096 Jan 16 17:29 ..
  ```

- 8. 现在返回父目录（即将你的用户家目录设为工作目录）：

  ```bash
  $ cd ..
  $ pwd
  /home/deepak
  ```

- 9. 最后，删除我们在开始时创建的 `test` 目录：

  ```bash
  $ rmdir test
  ```

## 文件系统命令摘要

以下是用于在文件系统中操作的常用命令快速摘要：

- **cd**：改变目录。不带参数时，该命令将当前工作目录更改为用户的家目录。当提供目录名称作为参数时，它将当前工作目录更改为该目录。
- **pwd**：打印当前工作目录。
- **mkdir**：创建新目录。根据该命令的参数创建一个或多个目录。当指定层级结构时，`-p` 选项会在缺失时创建中间目录。
- **rmdir**：删除空目录。
- **cat**：连接文件的内容。可以与 `>` 运算符一起用于创建文件，或与 `>>` 运算符一起用于向文件追加内容（详见后文关于 I/O 重定向的章节）。
- **rm**：删除文件。`-i` 选项提示用户确认是否继续删除。`-f` 选项是静默删除选项。它尝试在没有确认的情况下删除文件；如果删除失败，它不会报告错误。
- **mv**：将一个或多个作为参数提供的文件或目录移动到另一个目录。
- **ls**：列出作为一个或多个参数提供的目录内容。`-l` 选项列出文件的详细信息。`--color` 选项使用颜色编码列出文件，描述文件类型。`-t` 选项列出文件和目录的时间戳。`-R` 选项递归列出目录的内容。

下一章还将讨论几个重要的 `ls` 选项。

- **touch**：修改作为参数提供的文件或目录的时间戳。如果指定的参数不存在，`touch` 会在当前目录中创建一个名为该名称的空文件。

# 进程管理命令

Unix（因此也是 Linux）具有进程的概念，进程本质上是在操作系统基础设施上运行的任务。每次调用命令时，该调用都会生成一个或多个**进程**。进程属于用户，通常彼此隔离。通常情况下，系统普通用户关注进程的唯一时刻是当进程拒绝响应时；这通常被称为**程序挂起**。

## 列出进程

要列出由特定 shell 或其父 shell 生成的当前进程，我们可以使用 `ps`（processes spawned，生成的进程）命令：

```bash
$ ps
PID   TTY              TIME CMD
5355 pts/0           00:00:00 bash
5381 pts/0           00:00:00 ps
```

要列出系统中的*所有*进程，我们可以使用带有 `-A` 选项的 `ps` 命令：

```bash
$ ps -A
  PID TTY              TIME CMD
    1 ?                00:00:04 init
    2 ?                00:00:00 keventd
    3 ?                00:00:03 kaptmd
    4 ?                00:00:00 ksoftirqd_CPU0
    5 ?                00:00:03 kswapd
    6 ?                00:00:00 bdflush
    7 ?                00:00:00 kupdated
    8 ?                00:00:00 mdrecoveryd
  ...
```

> *注意，此选项区分大小写（大多数 Linux 命令也是如此）。*

## 获取完整命令行

我们知道进程代表已执行的命令。但是 `ps` 没有告诉我们的（至少不是很容易地）是进程被调用时的完整命令行是什么。有时，我们需要知道传递给了命令哪些参数以及调用了哪些选项。要查看进程的完整命令行及其所有者的名称，我们可以使用带有 `-auxww` 选项的 `ps` 命令：

```bash
$ ps -auxww

USER   PID %CPU %MEM   VSZ   RSS TTY          STAT START TIME COMMAND
root      1  0.0   0.2 1336   428 ?          S  Jan15  0:04 init

root    449  0.0   0.3 2056   756 ?          S  Jan15  0:00 /sbin/dhclient -q -lf /var/lib/dhcp/dhclient-eth0.leases -pf /var/run/dhclient-eth0.pid -cf /etc/dhclient-eth0.conf eth0
root    619  0.0   0.2 1328   412 ?          S  Jan15  0:00 /usr/sbin/apmd -p 10 -w 5 -W -P /etc/sysconfig/apm-scripts/apmscript
ident   657  0.0   0.3 27032  708 ?          S  Jan15  0:00 identd
root    671  0.0   0.4 3276   860 ?          S  Jan15  0:00 /usr/sbin/sshd
root    685  0.0   0.3 2096   752 ?          S  Jan15  0:00 xinetd -stayalive -reuse -pidfile /var/run/xinetd.pid
deepak  5270  0.0   3.1 16436 5952 ?          S  12:03  0:04 /usr/bin/gnome-session
deepak  5313  0.0   0.3 2900   724 ?          S  12:03  0:00 /usr/bin/ssh-agent /etc/X11/xinit/Xclients
```

