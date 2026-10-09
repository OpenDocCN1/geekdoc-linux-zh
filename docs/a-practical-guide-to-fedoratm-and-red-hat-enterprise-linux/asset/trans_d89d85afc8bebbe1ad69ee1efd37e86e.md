

## 管理 **root** 密码

在大量系统中管理 **root** 密码是一项挑战。如果不写下来（并安全地存储它们），记住每个系统的密码是困难的，而且检索密码又很耗时。跟踪哪些用户知道哪些 **root** 密码是不可能做到的。使用 `sudo`，即使是获取完整的 **root** shell 访问权限，也会使在大量系统上获取 **root** 权限以及跟踪谁可以在每个系统上获取 **root** 权限这些任务变得更加简单。

## sudo 的安全性

一些用户质疑 `sudo` 是否比 `su` 安全性低。由于两者都依赖于密码，因此它们拥有相同的优缺点。如果密码泄露，系统就会失守。然而，如果某个被 `sudo` 允许执行某项任务的用户密码泄露，整个系统可能并不一定会面临风险。因此，如果使用得当，`sudo` 权限结构的更细粒度 *可以* 使其成为比 `su` 更安全的工具。此外，当使用 `sudo` 调用单个命令时，与用户使用 `su` 打开一个 **root** shell 相比，用户不太会被引诱去继续以 **root** 权限进行操作。

使用 `sudo` 并不总是设置系统时最安全、最好的方式。在仅供单个用户使用的系统上，使用 `sudo` 与谨慎地使用 `su` 和 **root** 密码之间并没有太大区别。相反，在具有多个用户的系统上，特别是具有集中管理的系统网络上，`sudo` 可以被设置为比 `su` 更安全。

## 使用 sudo

添加或修改用户时，你可以通过让用户成为 `wheel` 组的成员来指定该用户为管理员。在“用户”窗口中指定账户类型为管理员（见图 4-17，第 112 页）时，该用户将成为 `wheel` 组的成员。基于 `/etc/sudoers` 文件中的以下行，`wheel` 组的成员可以使用 `sudo` 获得 **root** 权限：

```bash
%wheel  ALL=(ALL)  ALL
```

要使某用户成为 `wheel` 组的成员，在使用 **root** 权限工作时，运行带有 `-a` 和 `-G` `wheel` 选项的 `usermod`，以将该用户添加到 `wheel` 组。在下述示例中，用用户名替换 `sam`。

```bash
# usermod -a -G wheel sam
# grep wheel /etc/group
wheel:x:10:root,sam
```

`grep` 命令显示 Sam 是 `wheel` 组的成员。有关组的更多信息，请参见第 506 页的 `/etc/group`。

默认情况下，第一次运行 `sudo` 时会要求输入你的密码（而不是 **root** 密码）。此时，`sudo` 会*设置*你的时间戳。提供密码后，基于你的时间戳，`sudo` 在五分钟（默认）内不会再提示输入密码。

### 执行单个命令

在下述示例中，Sam 以非特权用户（即他自己）的身份工作，尝试设置系统时钟。**date** 实用程序显示一条错误消息，随后显示 Sam 输入日期的展开版本。当他使用 **sudo** 运行 **date** 来设置系统时钟时，**sudo** 会提示他输入密码，命令随后成功执行。

```bash
$ date 12121500
  date: cannot set date: Operation not permitted
  Thu Dec 12 15:00:00 PST 2013

$ sudo date 12121500
  [sudo] password for sam:
  Thu Dec 12 15:00:00 PST 2013
```

接下来，Sam 使用 **sudo** 卸载文件系统。由于他在前一个 **sudo** 命令的五分钟内给出了这个命令，因此他无需提供密码：

```bash
$ sudo umount /music
  $
```

现在，Sam 使用 `-l` 选项检查 **sudo** 允许他运行哪些命令。由于 sudoers 文件按照前一页“管理员与 **wheel** 组”中的说明进行设置，他允许以任意用户身份运行任何命令。

```bash
$ sudo -l
  ...
  User sam may run the following commands on this host:
    (ALL) ALL
```

### 授予 root 权限以编辑文件

使用 `-e` 选项，或将其作为 **sudoedit** 调用时，**sudo** 会以 **root** 权限编辑由其参数指定的文件。默认情况下，**sudo** 使用 **vi** 编辑器；有关如何指定不同编辑器的说明，请参见第 432 页。

任何能够以 **root** 权限运行命令的用户都可以使用 `-e` 选项。若要授予其他用户以 **root** 权限编辑任何文件的权限，请在 **sudoers** 文件中指定该用户可以执行 **sudoedit** 命令。更多信息请参见第 433 页的“用户权限规范”。

以这种方式调用编辑器会在用户的环境中运行编辑器，从而维护最小权限的概念。**sudo** 实用程序首先将待编辑文件复制到一个属于用户的临时文件中。如果文件不存在，**sudo** 会创建一个属于用户的新文件。一旦用户完成文件编辑，**sudo** 会将其复制回原位置（保持原有的权限）。

### 生成 Root Shell

当你有几个需要使用 **root** 权限运行的命令时，生成一个 **root** shell，输入命令（而无需在每个命令前键入 **sudo**），然后退出 shell 可能更容易。这种技术会破坏 **sudo** 内置的一些安全措施，因此请谨慎使用，并记得尽快返回到非 root shell。有关最小权限的注意事项，请参见第 423 页。使用 `sudo -i` 选项（第 432 页）生成 root shell：

```bash
$ pwd
/home/sam
$ sudo -i
# id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys) ...
# pwd
/root
# exit
logout
$
```

在此示例中，`sudo` 生成一个 root shell，并显示 `#` 提示符，以提醒 Sam 他正以 root 权限运行。`id` 实用程序显示运行该 shell 的用户的实际 UID。`exit` 命令（也可以使用 CTRL-0）终止 root shell，将 Sam 恢复到他的正常状态以及他先前的 shell 和提示符。

前述示例中的 `pwd` 内置命令展示了由 `-i` 选项创建的环境修改的一个方面。此选项生成一个 root 登录 shell（其环境与用户以 root 身份登录时所拥有的环境相同），并执行 root 的启动文件（第 329 页）。在发出 `sudo -i` 命令之前，`pwd` 内置命令显示 `/home/sam` 为 Sam 的工作目录；命令之后，它显示 `/root`（root 的主目录）为工作目录。使用 `--option`（第 432 页）生成 root shell 而不修改环境。在没有选项的情况下调用 `sudo` 时，它在一个未修改的环境中运行你指定的命令。为了演示此功能，下述示例在没有选项的情况下调用 `sudo` 来运行 `pwd`。以这种方式运行的命令的工作目录不会改变。

```bash
$ pwd
/home/sam
$ sudo pwd
/home/sam
```

下述命令失败，因为虽然 `sudo` 生成的 shell 以 root 权限执行了 `ls`，但用户运行的非特权 shell 重定向了输出。用户的 shell 没有权限写入 `/root`。

```bash
$ sudo ls > /root/ls.sam
-bash: /root/ls.sam: Permission denied
```

有几种方法可以绕过这个问题。最简单的方法是将整个命令行传递给在 `sudo` 下运行的 shell：

```bash
$ sudo bash -c "ls > /root/ls.sam"
```

`bash -c` 选项生成一个 shell，该 shell 执行选项后的字符串，然后终止。`sudo` 实用程序以 root 权限运行生成的 shell。你必须对该字符串加引号，以防止非特权 shell 解释特殊字符。你也可以使用 `sudo -i` 生成一个 root shell，执行命令，然后退出特权 shell。（参见前一节。）

**可选** 处理由 **sudo** 运行的命令输出重定向问题的另一种方法是使用 **tee**（第 162 页）：

```bash
$ ls | sudo tee /root/ls.sam
```

此命令行将 **ls** 的标准输出通过 **sudo** 传递给 **tee**，后者将其标准输入复制到由其参数指定的文件和标准输出。如果你不想显示输出，可以让非特权 shell 将输出重定向到 **/dev/null**（第 503 页）。下一个示例使用此技术来消除显示的输出，并使用 **tee** 的 **-a** 选项追加到文件而不是覆盖它：

```bash
$ ls | sudo tee -a /root/ls.sam > /dev/null
```

## 选项

你可以使用命令行选项来控制 **sudo** 如何运行命令。以下是 **sudo** 命令行的语法：

```bash
sudo [options] command
```

其中 **options** 是一个或多个选项，**command** 是你想要执行的命令。如果没有 **-u** 选项，**sudo** 将以 **root** 权限运行 **command**。以下是一些更常见的 **options**；完整的列表请参见 **sudo man** 页。

- **-b**（background）在后台运行 **command**。
- **-e**（**edit**）使用此选项时，**command** 是文件名而不是命令。此选项导致 **sudo** 使用由 **SUDO_EDITOR**、**VISUAL** 或 **EDITOR** 环境变量指定的编辑器，以 **root** 权限编辑名为 **command** 的文件。默认使用 **vi** 编辑器。或者，你可以使用 **sudoedit** 实用程序而不带任何选项。使用这种技术，编辑器不以 **root** 权限运行。请参见第 430 页的技巧。
- **-i**（**initial login environment**）生成在 /etc/passwd 中为 **root**（或由 **-u** 指定的其他用户）指定的 shell，运行 **root**（或其他用户）的启动文件，有一些例外（例如，TERM 不会改变）。有关示例，请参见第 426 页的“生成一个 **root** Shell”。
- **-k**（**kill**）重置运行该命令的用户的时间戳（第 429 页），这意味着该用户下次运行 **sudo** 时必须输入她的密码。
- **-l**（**list commands**）列出运行 **sudo** 的用户在本地系统上被允许运行的命令。不接受 **command**。
- **-s**（**shell**）如在 /etc/passwd 文件中指定，生成一个新的 **root**（或由 **-u** 指定的其他用户）shell。类似于 **-i**，但不改变环境。不接受 **command**。
- **-u user** 以 **user** 的权限运行 **command**。如果没有此选项，**sudo** 将以 **root** 权限运行 **command**。

