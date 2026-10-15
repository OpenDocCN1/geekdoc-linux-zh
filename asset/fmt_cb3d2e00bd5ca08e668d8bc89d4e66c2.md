
```
File Edit View Search Terminal help
[root]# tail -f /var/log/messages
May 13 22:29:31 system: pam_unix_auth[26735]: WARNING: unable to log in
May 13 22:29:31 system: session-manager[26881]: init: pamget session version 1.8
May 13 22:29:31 system: pam_pluid[26735]: pid: File open, overwritten.
May 13 22:29:31 system: pam_pluid[26735]: ALSA wake up on new
data to the device, but there was actually nothing to write
May 13 22:29:31 system: pam_pluid[26735]: Likely this is a bug in
the ALSA driver (snd_hcs171): Report this issue to the ALSA developers.
May 13 22:29:31 system: pam_pluid[26735]: We were woken up with POLL
SET - however subsequent snd_pcm_read[26735] or value_call[26735] returned 8 or another value <
min
May 13 22:29:31 system: pam_pluid[26735]: rejected message, 2 ruled types:
t"method return", "sd-1.12" - io-pid 26735: kernel/usb/bluetooth
("iface-guest-user-device: requested reply function
[1.57] - 26738: bluetooth-application)
May 13 22:29:31 system: pam_pluid[26735]: ALSA wake up to read new
data from the device, but there was actually nothing to read
May 13 22:29:31 system: pam_pluid[26735]: Likely this is a bug in
the ALSA driver (snd_hcs171): Report this issue to the ALSA developer.
May 13 22:29:31 system: pam_pluid[26735]: We were woken up with POLL
SET - however subsequent snd_pcm_read[26735] returned 8 or another value <
min
```

### 创建空文件

在文件系统上创建文件是非常用的。这是检查文件是否可写的一种有用测试。`touch` 命令可以帮助你完成这一操作。例如，使用 `touch somefile` 可以在当前目录下创建一个名为 `somefile` 的零字节文件。

`touch` 的目的是创建空文件。它的主要目的是打开一个文件，以便将显示的最后访问时间和修改时间更新为当前日期和时间。例如，`touch *` 将将当前目录下所有文件的时间戳设置为当前时间。当 `touch` 使用不存在的文件名作为参数时，它将创建该空文件。

![](img/3a7e027360b64bc83d5cf9a2db902251_78_0.png)

### 现实世界场景

#### 使用命令行释放 Linux 的威力

使用管道（pipes）和重定向（redirects）以高效方式组合 Linux 命令可以为管理员节省时间。想象你需要为服务器上所有现有用户创建一个列表。因为这些用户定义在 `/etc/passwd` 文件中，如果你能从文件中提取它们，这就会很容易实现。起点是 `cat /etc/passwd`，它将 `/etc/passwd` 的所有内容转储到屏幕。接着将其管道到 `cut -d -f 1` 以仅过滤用户。如果你需要，可以对其进行排序，创建一个指向 `sort` 命令的管道。在接下来的章节中，你将学习如何使用这些命令以及如何使用管道将它们连接起来。

管道构造中常用的另一个非常有用的命令是 `grep`。该命令用作过滤器，只显示你想看到的信息而不显示其他任何内容。例如，假设你想检查用户数据库 `/etc/passwd` 中是否存在一个名为 `linda` 的用户。一种解决方案是使用 `cat` 或 `less` 等查看器打开文件并浏览文件内容以检查你正在查找的字符串是否存在。然而，那工作量太大了。一个简单得的方法是将文件内容管道给过滤器 `grep`，它将选择出所有包含作为 `grep` 参数的字符串的行。该命令将是 `cat /etc/passwd | linda`。

在练习 2.2 中，我将向你展示如何一起使用 `grep` 和管道。

## 练习 2.2

### 在管道中使用 grep

在此过程中，你将再次使用 `ps aux` 命令显示系统上所有进程的列表，但这次你将通过 `grep` 工具传递命令的输出，它会选择你正在寻找的信息。

1. 输入 `ps aux` 显示你计算机上运行的所有进程列表。如你所见，找到你所需的精确信息并不容易。
2. 现在运行 `ps aux | grep blue` 来仅选择包含文本 `blue` 的行。你会发现只有这些行被显示出来。
3. 在此练习中，你将学习如何过滤输出。

### 重定向

管道用于将一个命令的输出发送另一个命令，而重定向用于将命令的输出发送文件。重定向有两种类型：输出重定向（`>`）和追加重定向（`>>`）。

输出重定向运算符 `>` 将覆盖文件内容（如果不存在则创建一个新文件）。例如，`ls > files.txt` 将文件列表保存到 `files.txt`。追加重定向运算符 `>>` 将输出添加到现有文件的末尾。例如，`date >> files.txt` 将当前日期添加到 `files.txt`。

## 练习 2.3

### 将输出重定向到文件

在此练习中，你将学习如何将命令的输出重定向到文件。

1. 从控制台输入 `ps > output.txt`。这将所有运行进程列表保存到名为 `output.txt` 的文件中。
2. 现在使用 `cat output.txt` 查看文件内容。
3. 要向文件中添加更多信息，请使用 `>>` 运算符。例如，`date >> output.txt`。这将当前日期添加到文件中。

# 第二章 在命令行上寻找路径

除了重定向输出，反向也是可能的，即输入重定向（`<`）。这允许你将文件内容输入命令，而不是手动输入。例如，`sort < list.txt` 将告诉 `sort` 命令从 `list.txt` 读取行并排序。

## 练习 2.4

### 使用标准输入重定向

在此练习中，你将学习如何使用输入重定向来自动化任务。

1. 从控制台输入 `mail root`。这打开命令行邮件程序向用户 `root` 发送消息。
2. 当 `mail` 提示主题时，输入 `Test message` 作为主题文本，并按回车。
3. `mail` 命令显示一个空白行，你在其中输入消息正文。在此练习中，你不需要输入正文，并且你想立即关闭输入。为此，输入一个 `.`（点）并按回车。邮件消息现在已发送给用户 `root`。
4. 现在你正在使用命令行选项通过 `mail -s test message` 命令指定主题。`mail` 命令立即返回一个空白行，你再次输入一个 `.`（点）来告诉邮件客户端你已完成。
5. 在第三次尝试中，你通过一个命令输入所有内容，这对于想在自动化 shell 脚本中使用此类命令非常有用。输入此：`mail -s test message < file`。如你所见，当重定向标准输入时，点会立即传递给 `mail` 命令，你不需要做任何其他操作即可发送消息。

## 练习 2.4（继续）

```
mail Edit view search Terminal Help
[root@hostname]## mail root
Subject: test message

EOT
Mail message body; hope that's ok
You have new mail in /var/spool/mail/
[root@hostname]## mail -s test message root

EOT
Mail message body; hope that's ok
[root@hostname]## mail -s test message root <
Mail message body; hope that's ok
[root@hostname]## -
```
