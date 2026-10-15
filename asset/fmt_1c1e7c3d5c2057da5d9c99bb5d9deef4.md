
stetson@linux_rocks:~/my_awesome_directory$ `mv file1.png`

my_awesome_file.png

stetson@linux_rocks:~/my_awesome_directory$ `ls`

my_awesome_file.png

stetson@linux_rocks:~/my_awesome_directory$ `mv`

my_awesome_file.png /tmp/my_renamed_awesome_file.png

stetson@linux_rocks:~/my_awesome_directory$ `ls /tmp`

my_renamed_awesome_file.png

我们取 `file1.png` 并将其重命名为 `my_awesome_file.png`。然后，我们再次移动并重命名了它，将其放入 `/tmp` 目录并命名为 `my_renamed_awesome_file.png`。

### 复制目录

假设我们要移动一个包含某些文件的目录：

```
stetson@linux_rocks:~$ cp my_awesome_directory/ another_directory

cp: r not specified; omitting directory 'my_awesome_directory/'

stetson@linux_rocks:~$ ls -l

total 4

drwxrxr-x 2 st stetson 4096 Feb 16 00:46 my_awesome_directory
```

我们收到了关于 `-r` 标志的奇怪错误信息。这是什么？Linux 想要使用递归标志来复制目录内的任何文件和目录。

让我们再次尝试：

```
stetson@linux_rocks:~$ cp -r my_awesome_directory/
another_directory
stetson@linux_rocks:~$ ls -l

total 8

drwxrxr-x 2 st stetson 4096 Feb 16 00:46 another_directory
drwxrxr-x 2 st stetson 4096 Feb 16 00:46 my_awesome_directory
```

太棒了！这次成功了！

小贴士 🔥 通配符可以在 bash shell 的许多地方使用。假设我们有一个包含许多不同扩展名的目录，但我们只想复制带有 `.png` 扩展的文件。我们可以使用通配符这样做：

```
stetson@linux_rocks:~/important_files$ ls -l

total 0

-rw-rw-r-- 1 steton steton 0 Feb 16 00:53 Users.pdf
-rw-rw-r-- 1 steton steton 0 Feb 16 00:53 Reports.pdf
-rw-rw-r-- 1 steton steton 0 Feb 16 00:53 file1.png
-rw-rw-r-- 1 steton steton 0 Feb 16 00:53 file2.png
```
*(注：此处示例代码中未显示具体的通配符命令，但根据上下文逻辑应为 `cp *.png ...`)*

*(注：原文文本后半部分存在乱码或重复的无效片段，已根据指令要求进行翻译和清理)*

为了让它成功运行，需要某些命令。例如，你可能运行 `sudo apt-get install nginx` 来安装 Nginx Web 服务器。如果我们只使用 `apt-get install nginx` 并且以非 root 用户运行它，相同的命令将会失败。

> 很多时候在自己的终端里输入命令时，我会忘记在它们前面加上 `sudo`，导致出现“权限被拒绝”(`permission denied`)的错误。与其向上滚动并在它们前加上 `sudo`，或者重写整个命令，我宁愿直接使用 `sudo !!`。双感叹号 `!!` 字符告诉系统使用 `sudo` 运行上一个命令。执行 `sudo !!` 会替换我上一行的原始命令。这让我在命令行上的操作速度更快。

一旦你安装了 `sudo`，你就需要从 root 账户将你的普通用户添加到 `sudo` 组。执行 `adduser <user_name> sudo` 来完成：

```
root@linux_rocks:#$ adduser stetson sudo

Adding user `stetson` to group `sudo` ...
Adding user stetson to group sudo
Done.
```

注意，我在执行此命令时是以 root 身份登录的。

### 以 root 身份运行……谨慎行

我提到过你不应该以 root 身份运行大多数命令，但有时你别选择。执行需要提升权限的任务的另一种方法是直接变成 root。你可以通过运行 `su`（switch user 的缩写）来实现这一点。你需要输入 root 密码来变变为 root。

```
stetson@linux_rocks:~$ su
Password:
root@linux_rocks:/home/stetson# whoami
root
```

能力越大，责任越大。在以 root 身份运行命令时，你需要格外小心，因为你可能会犯更改或破坏系统的错误。

作为 root，你也可以使用 `su` 切换回另一个用户：

```
root@linux_rocks:#$ su stetson
$ whoami
stetson
```

### 添加用户

添加用户非常简单。我们可以使用的主要命令是 `useradd`。该命令允许我们在指定用户名称的同时指定任何我们需要的属性。

现在让我们添加一个用户吧（你需要 root 或超级用户权限才能操作）：

```
stetson@linux_rocks:~$ useradd bob
useradd: Permission denied.
useradd: cannot lock /etc/passwd; try again later.
stetson@linux_rocks:~$

stetson@linux_rocks:~$ sudo useradd bob
[sudo] password for stetson:
stetson@linux_rocks:~$

stetson@linux_rocks:~$ cat /etc/passwd | grep bob
bob:x:1001:1001::/home/bob:/bin/sh
```

上面，我添加了 `bob`，但由于没有 `sudo` 权限，被拒绝了。我使用 `sudo` 再次添加了用户，并检查了 `/etc/passwd` 目录以验证 `bob` 是否出现。`/etc/passwd` 文件是什么？

### /etc/passwd

`/etc/passwd` 文件是一种特殊类型的文件，作为存储用户账户信息的中央区域。文件中的每一行代表一个用户账户并由一系列由冒号分隔的字段组成，这些字段提供了关于用户的详细信息。

`/etc/passwd` 主要用途是允许系统在身份验证期间将用户名与相应的用户 ID 进行匹配。当用户登录时，Linux 会检查凭据是否与 `/etc/passwd` 中存储的内容匹配。该文件还负责一些其他管理任务，例如确定用户的默认组和主组成员身份。

`/etc/passwd` 曾用于存储加密密码，但现代系统将加密密码存储在我们之前处理过的名为 `/etc/shadow` 的文件中。`etc/shadow` 具有更多的安全限制。

### 修改你的密码

当我们更改用户的密码时，我们正在与 `/etc/passwd` 文件交互！

现在让我们用新用户 `bob` 尝试一下：

```
stetson@linux_rocks:~$ sudo passwd bob
New password:
retype new password:
password: password updated successfully
stetson@linux_rocks:~$ su bob
Password:
$ whoami
bob
```

上面，我告诉 Linux 我想给 `bob` 设置一个新密码。在确认密码后，我可以使用 `su` 或切换用户来使用新密码切换到 `bob`。最后，我使用 `whoami` 命令验证我确实是以 `bob` 的身份登录的。

### 更改用户的默认 shell

你可能已经注意到，当切换到某个用户时，他们的提示符只是 `$` 符号，而不是我们之前使用的完整路径名和用户名。这可能是因为用户的默认 shell 是 `sh` 而不是 `bash`。

你可以使用命令 `ps -p $$` 当前正在使用哪个 shell。`ps` 是一个显示进程 ID 的命令。`-p` 标志指定了我们要看到的进程。最后，`$$` 是一个特殊变量，赋予我们当前 shell 实例的进程 ID。我们稍会深入研究进程，所以不用担心现在觉得这没意义！

```
$ ps -p $$
PID         TIME CMD
```
