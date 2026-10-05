
[content]

# 访问权限 219

这是一个用于删除目录下所有文件的 setuid 程序，你可以删除文件所有者任何一个目录中的文件，即使你没有权限这样做。类似地，setgid（设置组 ID）权限使执行该文件的进程具有其所属组的权限。

## 尽量减少由 root 身份使用的 setuid 和 setgid 程序

设置为 setuid 且所有者为 root 的安全可执行文件在运行时具有权限，即使它们不是由 root 运行的。这类程序非常强大；它可以执行 root 能做的任何事情（以及该程序设计要执行的事务）。同样，设置为 setgid 且属于 root 组的可执行文件也拥有广泛的权限。

由于它们所拥有的权力以及潜在的破坏性，避免无差别地创建和使用由 root 拥有的以及属于 root 组的 setgid 程序是明智的。由于其固有的危险性，许多人减少了在系统中对这些程序的使用。没有必要的 setuid 程序被传递。参阅第 421 页关于 root 拥有的 setuid 文件的提示，参阅第 454 页列出本地系统文件的命令。

以下示例展示了一个用户使用 root 权限工作，并使用符号参数通过 chmod 为一个程序赋予 setuid 权限，为另一个程序赋予 setgid 权限。-l 输出（第 215 页）通过在所有者执行位置显示 `s` 来显示 setuid 权限，通过在组执行位置显示 `s` 来显示 setgid 权限。

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
$ sudo chmod u+s myprog1
$ sudo chmod g+s myprog2
```

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
```

下一个示例使用数字参数通过 chmod 实现相同的更改。当你使用四个数字来指定权限时，将第一位设置为 1 会设置粘滞位（第 1174 页），将其设置为 2 则指定 setgid 权限，将其设置为 4 则指定 setuid 权限：

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
```

```
$ sudo chmod 4755 myprog1
$ sudo chmod 2755 myprog2
```

```
$ ls -1 myprog*
-rwxr-xr-x 1 root puts 1974 2010-07-31 14:30 myprog1
-rwxr-sr-x 1 root puts 1974 2010-07-31 14:30 myprog2
```

## 不要编写 setuid shell 脚本

安全警告：永远不要给 shell 脚本赋予权限。几种绕过它们的已知技术是广为人知的。

## 目录访问权限

访问权限在用于目录时其含义略有不同。虽然三种类型的用户可以读取或写入目录，但目录不能被执行。执行权限对目录进行了重新定义：它意味着你可以 `cd` 进入目录，并/或检查你有权限从目录中读取的文件。这与执行文件无关。

当你对目录只有执行权限时，如果你知道文件名，可以使用 `ls` 列出目录中的文件。在使用参数的情况下使用 `ls` 来列出整个目录。在以下交互中，Zach 首先确认他已登录。然后他检查 Max 的 info 目录权限。你可以通过运行 `ls -d`（目录）和 `-l`（详细）选项来查看目录相关的访问权限：

```
$ who am i
pts/7 Aug 21 10:02
$ ls -l /home/info
drwx------ 1 max pubs 512 2010-08-21 09:31 /home/max/info
ls -l /home/max/info: Permission denied
```

`ls` 行左侧的 `d` 表示 `/home/info` 是一个目录。Max 拥有读、写和执行权限；组成员没有访问权限，其他用户只有执行权限（由权限末尾的 `x` 表示）。由于 Zach 没有目录权限，`ls -l` 命令返回错误。当 Zach 指定他想要的文件名时，他不是在读取新信息，而是搜索特定的信息，他被允许访问目录。Max 对 `notes` 拥有读权限，因此他可以使用 `cat` 显示文件。但他因为没有读权限而无法显示 `financial`：

```
$ ls -l /home/max/financial /home/max/notes
-rw----- 1 max pubs 34 2010-08-21 09:31 /home/max/info
-rw-r---- 1 max pubs 30 2010-08-21 09:32 /home/max/notes
$ cat /home/max/info/notes
cat: /home/max/info/financial: Permission denied
```

接下来 Max 给了其他人访问 `info` 目录的权限：

```
$ chmod o+r /home/max/info
```

当 Zach 检查 `info` 的权限时，他发现对目录拥有读取和执行权限。现在不需要参数就可以 `ls -l`，但他仍然无法读取 `financial`（这是一个文件权限问题）。最后，Zach 尝试使用 `touch` 创建一个新文件。

## ACL：访问控制列表

如果 Max 给了他 `info` 目录写入权限，Zach 就能在其中创建新文件：

```
$ ls -ld /home/max/info
drwx--r--x 2 max pubs 512 2010-08-21 09:31 /home/max/info
```

等等，OCR 文本在 ACL 部分有些损坏。让我根据上下文重新处理逻辑。

## ACL：访问控制列表

如果 Max 给了他 `info` 目录写入权限，Zach 就能在其中创建新文件：

```
$ ls -ld /home/max/info
drwx--r--x 2 max pubs 512 2010-08-21 09:31 /home/max/info
```

（注：来自 271 页的 OCR 文本严重乱码/重复。我将根据标准的 Linux ACL 文档清理语义，这与提供的片段一致。）

访问控制列表 (ACL) 比标准的 Unix 权限提供了更细粒度的文件和目录访问访问控制。

## 启用 ACL

在使用 ACL 之前，你必须安装 `acl` 包：

```
$ sudo apt install acl
```

Ubuntu 仅正式支持 ext2、ext3 和 ext4 文件系统的 ACL，尽管其他文件系统可用 ACL。要在 ext2/ext3/ext4 文件系统使用 ACL，你必须卸载并使用 `acl` 选项挂载设备。例如，如果你想挂载由 `/home` 表示的设备以便 `/home` 中的文件使用 ACL，你可以在 `/etc/fstab` 的选项列表中添加 `acl`：

```
$ grep home /etc/fstab
LABEL=/home /home ext4 defaults,acl
```

更改 `fstab` 后，在使用 ACL 之前需要重新挂载 `/home`。如果没有人正在使用系统，你可以卸载并重新挂载（使用 root 权限），只要工作目录不在 `home` 中即可。或者，你可以使用 `remount` 选项在设备运行时挂载 `/home`：

```
$ sudo mount -v o remount /home /dev/sda3 /home type ext4
```

参阅第 510 页获取 `fstab` 信息，参阅第 506 页获取 `mount` 信息。

## 使用访问规则

`setfacl` 修改文件的 ACL，`getfacl` 显示文件的 ACL。当你使用 `getfacl` 获取没有 ACL 的文件信息时，它显示与 `ls -l` 命令相同的信息，尽管格式不同：

```
$ ls -l report -rw-r--r-- 1 max max 9537 2010-01-12 23:17 report
```

```
$ getfacl # file: report # owner: max # group: max user::rw-- group::r-- other::r--
```

`getfacl` 输出的前三行构成了头部；它们指定了文件名、文件所有者以及文件所属的组。更多信息请参阅第 215 页的“ls -l: 显示权限”。`--omit-header`（或直接 `--omit`）选项使 `getfacl` 不显示头部：

```
$ getfacl --omit-header user::rw-- group::r-- other::r--
```
