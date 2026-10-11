
你想运行为特定 `shell` 环境创建的 `shell` 脚本，你需要运行为这些脚本而创建的 `shell`，以便你可以测试或使用这些脚本。

# 第二部分：成为 Linux 高级用户

`screen`。在这种情况下，`/etc/passwd` 就是参数。通常，你可以在命令行上放置任意数量的参数，仅限于命令行允许的字符总数。

有时，参数会与某个选项 `option` 相关。在这种情况下，参数可能会紧跟在选项之后。对于单字母选项，参数通常跟在空格后面。对于完整单词选项，参数通常跟在等号 `=` 后面。以下是一些示例：

```
$ ls --hide=Desktop
Documents Music Public Videos
Downloads Pictures Gvfs Templates
```

在上一个示例中，`--hide` 选项告诉 `ls` 在列出目录内容时不显示名为 `Desktop` 的文件或目录。注意等号紧跟在选项之后（没有空格），然后是参数（同样没有空格）。

这里是一个后跟参数的单字母选项示例：

```
$ tar -cvf backup.tar /home/chris
```

在所示的 `tar` 示例中，选项表示创建 `c` 一个名为 `backup.tar` 的文件 `f`，其中包含 `/home/chris` 目录及其子目录的所有内容，并在执行备份时显示详细信息 `v`。由于 `backup.tar` 是 `f` 选项的参数，因此 `backup.tar` 必须紧跟在选项之后。

这里是你可以尝试的几个命令，以及它们在不同选项下的不同行为：

```
$ ls -2
Desktop Documents Music Public Templates Videos
$ ls -a
Desktop Desktop gnome2_private .lessht Public
Documents gnome .local Templates
.bash_history Downloads gnupg mozilla Videos
.bash_logout emacs gstreamer-01 Music xession-errors
.bash_profile .esd_auth gtk-bookmarks Pictures zshrc
.bashrc .fsync.log gvfs Pictures
$ uname
Linux
$ uname -a
linux myhost.example.com 2.62-131.137.1.e16.x86_64 #1 SMP Sep 29
10:24:25 EDT 2011 x86_64 x86_64 GNU/Linux
$ date
Sun Dec 4 09:08:38 EST 2011
$ date +'%Y-%d/%m/%Y'
$ date +'%A, %B d, %Y'
Sunday, December 04, 2011
```

## 第 3 章：使用 Shell

`ls` 命令本身会显示当前目录下的所有文件和目录。通过添加 `-a`，你还可以看到目录中的隐藏文件（那些以点开头的文件）。`uname` 命令显示你正在运行的系统类型 `Linux`。当你添加 `-a` 时，还可以查看主机名、内核发布版本和内核版本。

`date` 命令有特殊的选项类型。本身，`date` 仅如上所示打印当前的日期和时间。但 `date` 命令支持一个特殊的 `+` 格式选项，允许你以不同的格式显示日期。输入 `--help` 查看你可以使用的不同格式指示符。

尝试 `id` 和 `who` 命令来感受你的 Linux 环境，如下文所述。

当你登录到 Linux 系统时，Linux 将你视为具有一个特定的身份，其中包括你的用户名、组名、用户 ID `uid` 和组 ID `gid`。Linux 还会跟踪你的登录会话：它知道你何时登录、空闲了多久以及在哪里登录。

要查找有关你身份的信息，请如下所示使用 `id` 命令：

```
$ id
uid=501(chris) gid=501(chris) groups=105(sales),7(lp)
```

在这个示例中，`chris` 由数字用户 ID `uid` 501 表示。`chris` 的主组也是 `chris`，其组 ID `gid` 为 50。Fedora 和 Red Hat Enterprise Linux 用户的主组名与其用户名相同是正常现象。用户 `chris` 还属于名为 `sales` `gid` 105 和 `lp` `7` 的其他组。这些名称和数字代表了 `chris` 访问计算机资源的权限。

> 注意
>
> Linux 发行版启用了安全增强 Linux `SELinux`，例如 Fedora 和 RHEL，它们会在 `id` 的末尾显示信息。输出可能类似于所示：
>
> `context=unconfined:unconfined:unconfined_t:s0:c0.c1023`
