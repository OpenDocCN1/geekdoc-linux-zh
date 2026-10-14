
```
[me@linuxbox ~]$ sudo -l
User may run the following commands on this host:
(ALL) ALL
```

## UBUNTU 与 SUDO

普通用户经常遇到的问题之一是如何执行需要超级用户权限的某些任务。这些任务包括安装和更新软件、编辑系统配置文件以及访问设备。在 Windows 世界，这通常通过赋予用户管理员权限来实现。这允许用户执行这些任务。然而，这也使得由用户执行的程序具有相同的能力。这在大多数情况下是理想的，但也允许恶意软件（如病毒）肆无忌惮地运行。

在 Unix 世界中，普通用户和管理员之间一直存在着较大的划分，这归于 Unix 的多用户传统。Unix 的方法是在需要时才授予超级用户权限。为了这一点，通常使用 `su` 和 `sudo` 命令。

直到几年前，Linux 发行版依赖 `sudo` 来实现此目的。`sudo` 不需要配置，而拥有 root 账户在 Unix 中是传统的。这引入了一个问题：用户倾向于在不需要的情况下以 root 运行。事实上，有些用户完全以 root 身份运行系统，因为这样可以消除所有烦人的“拒绝访问”消息。这就是你降低 Linux 系统安全性到 Windows 系统水平的方法。这不是一个好主意。

当 Ubuntu 创建时，它的创建者采取了不同的任务。默认情况下，Ubuntu 禁用 root 登录（通过不对该账户设置密码），而是使用 `sudo` 授予超级用户权限。初始用户账户通过 `sudo` 获得完全的超级用户权限，并向后续账户授予类似的权限。

| 参数 | 结果 |
| :--- | :--- |
| admins | 将组所有者更改为组管理员。文件所有者不变。 |
| bob | 将文件所有者从当前所有者更改为用户 `bob`，并将所有者更改为用户 `bob` 的登录组。 |

假设有两个用户：`jan`，拥有超级用户权限，而 `tony` 则没有。`jan` 想要将一个文件从她的家目录复制到 `tony` 的家目录。因为 `jan` 想要能够编辑该文件，所以 `jan` 将复制的文件的所有权更改为 `tony`。

```
$janet@linuxbox ~$ sudo cp myfile.txt "tony"
$janet@linuxbox ~$ sudo -l ~/tony/myfile.txt
-rw-r-- 1 root root 2018-03-20 14:30 /home/tony/myfile.txt
$janet@linuxbox ~$ sudo chown "tony"
$janet@linuxbox ~$ sudo -l ~/tony/myfile.txt
-rw-r-- 1 tony tony 2018-03-20 14:30 /home/tony/myfile.txt
```

在这里，我们使用 `sudo` 将文件从她的家目录复制到 `tony` 的家目录。接下来，`janet` 更改了 root 下文件的所有权（这是使用 `sudo` 的结果）。通过第一个参数末尾的冒号，`jan` 还将文件的组所有权更改为 `tony` 的登录组，这恰好是 `tony` 组。

注意，在第一次使用 `sudo` 后，`janet` 没有被提示密码。这是因为在大多数配置中，`sudo` 在其计时器超时之前都是“信任”该用户的。

## chgrp: 更改组所有权

在 Unix 版本中，`chown` 命令只更改文件所有权，不更改组所有权。为了实现这一目的，使用了单独的命令 `chgrp`。它的工作方式与 `chown` 相同，只是功能更有限。

## 练习我们的权限

现在我们已经学习了权限是如何工作的，是时候展示一下它了。我们将演示一个常见问题的解决方案——设置共享目录。假设我们有两个名为 `bill` 和 `karen` 的用户。他们都有音乐收藏，并想建立一个共享目录，并在其中存储 Ogg Vorbis 或 MP3 格式的音乐文件。用户 `bill` 通过 `sudo` 拥有超级用户权限。

首先需要发生的是创建一个包含 `bill` 和 `karen` 为成员的组。使用图形化管理工具，`bill` 创建了一个名为 `music` 的组，并将用户 `bill` 和 `karen` 添加其中，如图 9-2 所示。

### 图 9-2: 创建新组

然后，`bill` 为音乐文件创建了目录。

```
[bill@linux] ~$ sudo mkdir /usr/local/share/Music
Password:
```

因为 `bill` 正在操作其家目录之外的文件，因此需要超级用户权限。目录创建后，它具有以下所有权和权限：

```
[bill@linux] ~$ ls -ld /usr/local/share/Music
drwxr-xr-x 2 root 4096 2018-03-21 18:05 /usr/local/share/Music
```

如我们所见，该目录由 `root` 所有，权限模式为 `755`。为了让这个目录可共享，`bill` 需要更改组所有权并允许组进行写入。

```
[bill@linux] ~$ sudo chown music /usr/local/share/Music
[bill@linux] ~$ chmod 775 /usr/local/share/Music
[bill@linux] ~$ ls -ld /usr/local/share/Music
drwxr-xr-x 2 root 4096 2018-03-21 18:05 /usr/local/share/Music
```

这意味着什么？这意味着我们有一个目录 `/usr/local/share/Music`，它由 `root` 所有，并允许 `music` 组读取和写。`music` 组的成员有 `bill` 和 `karen`；因此，`bill` 和 `karen` 可以在 `/usr/local/share/Music` 目录中创建文件。其他用户可以看到目录的内容，但不能在那里创建文件。

但我们仍然面临一个问题。按照当前的权限，在 Music 目录内创建的文件和目录将具有 `bill` 和 `karen` 的普通权限。

```
[bill@linux] ~$ /usr/local/share/Music/test_file
[bill@linux] ~$ ls -l /usr/local/share/Music
-rw-r-- 1 bill 2018-03-24 20:03 test_file
```

实际上有两个问题。首先，该系统的默认 `umask` 是 `0022`，它阻止组成员写入属于组内其他成员的文件。如果共享目录只包含文件，这就不会成为问题，因为此目录将存储音乐，而音乐通常按艺术家和专辑的层次结构组织，组成员需要能够在其他成员创建的目录内部创建文件和目录的能力。我们需要将 `bill` 和 `karen` 使用的 `umask` 更改为 `0002`。

其次，由成员创建的每个文件和目录将被设置为该用户的主组，而不是 `music` 组。这可以通过在目录上设置 `setgid` 来解决。

```
[bill@linuxbox ~] chmod g+s /usr/local/share/Music
[bill@linuxbox ~] ls -ld /usr/local/share/Music
drwx-r-x 2 root 4096 2018-03-21 18:05 /usr/local/share/Music
```

现在我们测试权限是否修复了 `umask` 为 `0002`、删除了之前的文件并创建了新目录。

```
[bill@linuxbox ~] umask 0002
[bill@linuxbox ~] rm /usr/local/share/Music/test_file
[bill@linuxbox ~] mkdir /usr/local/share/Music/test_dir
[bill@linuxbox ~] ls -l /usr/local/share/Music
drwx-r-x 2 root 4096 2018-03-21 18:05 Music
drwxrwxrwx 1 bill 2018-03-24 20:03 test_dir
```

现在文件和目录都已以正确的权限创建，允许组的所有成员在 Music 目录中创建文件和目录。剩余的一个问题是 `umask`。必要的设置仅持续到会话结束，必须重置。

## 更改你的密码

在我们学习了权限如何工作后，是时候展示一下它了。我们将演示一个常见问题的解决方案——设置共享目录。假设我们有两个名为 `bill` 和 `karen` 的用户。他们都有音乐收藏，并想建立一个共享目录，并在其中存储 Ogg Vorbis 或 MP3 格式的音乐文件。用户 `bill` 通过 `sudo` 拥有超级用户权限。

首先需要发生的是创建一个包含 `bill` 和 `karen` 为成员的组。使用图形化管理工具，`bill` 创建了一个名为 `music` 的组，并将用户 `bill` 和 `karen` 添加其中，如图 9-2 所示。

### 图 9-2: 创建新组

然后，`bill` 为音乐文件创建了目录。

```
[bill@linux] ~$ sudo mkdir /usr/local/share/Music
Password:
```

因为 `bill` 正在操作其家目录之外的文件，因此需要超级用户权限。目录创建后，它具有以下所有权和权限：
