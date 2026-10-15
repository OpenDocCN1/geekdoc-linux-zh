
```
root:x:0:root
bin:x:1:root,daemon
daemon:x:2:root,daemon
sys:x:3:root,daemon
adm:x:4:root,daemon
tty:x:5:root,daemon
disk:x:6:root,lp
mem:x:7:root,lp
wheel:x:8:root
mail:x:9:mail
news:x:10:news
uucp:x:11:uucp
man:x:12:man
games:x:13:games
gopher:x:14:gopher
dip:x:15:dip
ftp:x:16:ftp
lock:x:17:lock
nbody:x:18:nbody
users:x:19:users
ddbus:x:81:dbbus
floppy:x:20:floppy
vcsa:x:69:vcsa
nscd:x:28:nscd
rpm:x:37:rpm
haldaemon:x:68:haldaemon
netdump:x:34:netdump
utmp:x:22:utmp
slocate:x:21:slocate
sshd:x:74:sshd
rpc:x:32:rpc
rpcuser:x:29:rpcuser
nfsnody:x:6534:nfsnody
mailnull:x:47:mailnull
msmssp:x:51:msmssp
npcap:x:77:npcap
apache:x:48:apache
squid:x:23:squid
webalizer:x:67:webalizer
xfs:x:43:xfs
tnp:x:38:tnp
gdm:x:42:gdm
mrhinkle:x:500:mrhinkle,mark
mark:x:501:mark,mrhinkle
```

你可以看到，`/etc/passwd` 文件中列出的所有用户都有唯一的名称和数字，这些是他们的用户 ID (UID)。在 `/etc/group` 中，他们有一个名称和数字表示他们的组 ID (GID)。在图 6.3 中，你可以看到通过图形化 YaST 工具添加的用户。

![](img/72e1c6125676a623b5032cfdab8d797c_160_0.png)

图 6.3 Novell Linux 桌面使用 YaST 添加用户并将其分配到组。

# 使用 Linux 桌面

一旦你理解了用户和组，就可以查看它们如何关联文件和目录。你可以使用 `ls` 命令查找目录中文件的权限设置情况。如果你查看图 6.4，将看到目录中所有文件的列表。注意文件有两列，包含用户和组。

```
[root@www example ~] ls
file1 file2 file3 file4
[root@www example ~]# ls -al
total 8
drwxr-xr-x 2 mrhinkle 4096 Aug 18 04:44
drwxr-xr-x 5 mrhinkle 4096 Aug 18 04:44
-rw-r--r-- 1 mrhinkle 0 Aug 18 04:44 file1
-rw-r--r-- 1 mrhinkle 0 Aug 18 04:44 file2
-rw-r--r-- 1 mrhinkle 0 Aug 18 04:44 file3
-rw-r--r-- 1 mrhinkle 0 Aug 18 04:44 file4
```

图 6.4 使用 `ls` 命令列出的目录文件。

这里显示的信息可以如图 6.5 所示进行分析。第一列显示类型，这是一个目录。第二列显示链接数。第三、四列显示所有者和组。第五列显示文件大小，时间戳显示创建时间，最后一列是文件名。

![](img/72e1c6125676a623b5032cfdab8d797c_161_0.png)

图 6.5 详细列表的每一列。

注意权限使用 r、w、x 字母表示。这些表示文件拥有的权限类型：读 (r)、写 (w) 和执行 (x)。这些字母写出来时的格式如下：

```
- rwxrwx
```

第一组三个表示文件所有者可以进行的更改，第二个组表示文件所属组可以进行的操作，最后的一组（有时被称为“世界/其他”）表示任何用户对文件可以的操作。此代码示例表示该文件不受限制，用户、组和世界都拥有完全权限。我们将查看一个 Web 服务器的常见设置，允许任何人执行或读取文件，但不能写入。

```
- rwr- xr-x
```

注意在上一个示例中用连字符替换了权限。你也可以用数字表示权限。你可以使用三数字表示法，它是每个三个领域权限的总和。例如，以下列表显示了权限的数值：

- 读—r—4
- 写—w—2
- 执行—x—1
- 无—0

一个组成员和其他人可读、可执行，但所有者可读、写、执行的文件，其权限看起来如下：

```
755
```

数字权限比整个格式更短。以下示例显示了一些额外的权限：

- rwxr-xr-x (755)—所有者拥有读、写和执行权限；组和其他人只有读取和执行权限。
- -rw------- (600)—仅所有者具有读取和写入权限。文件无法执行可能是出于安全考虑；例如，这种设置可能用于某些脚本，如果不小心执行，可能会导致范围广泛且毁灭性的系统更改。
- rw-r--r-- (644)—只有所有者具有读取和写入权限；用户组和其他用户只能读取文件。
- rwx------ (700)—只有所有者可以访问该文件，且拥有所有权限。
- rwx-x--x (711)—所有者具有读取、写入和执行权限；用户组和其他用户只有执行权限。
- -rw-rw-rw- (666)—每个人都可以对文件进行读取和写入。在应用此权限时要小心，因为这实际上允许任何人访问、修改或删除该文件。
- rwxrwxrwx (777)—每个人都可以读取、写入和执行。这在实际上消除了对文件上的所有限制，因此请务必确定你确实想允许任何人运行或修改此文件。

一旦你理解了权限，就可以继续学习如何使用 `chmod` 命令对文件权限进行更改。

# 更改所有者和权限

如果你有一些数据且并不经常写入，例如某些像演示文稿的归档副本，你可以将文件的权限更改为只读，这样文件被覆盖或删除的难度就会增加，虽然并非不可能。你可以使用 `chmod` 命令来实现此。`chmod` 用于设置文件的权限。其语法通常为 `chmod [permissions] file`，其中 `[permissions]` 是所有者、组以及所有其他用户的权限。对于你想要确保只读的文件，在示例中你可以将该数字设置为 444，其中 4 表示只读。在接下来的示例中，文件是 `example.txt`，是使用 `vi` 编辑器创建的。一旦创建了文件，你可以使用 `chmod` 将文件设置为只读，这样就不会覆盖那里的数据了。注意，如果你尝试删除该文件，会收到警告。这并不是万无一失的方法，你可以对 `rm -d` 回答 `y`，文件就会被删除，但警告可以帮助用户在编辑或删除之前仔细考虑。

```bash
mrhinkle@linux:~$ example.txt
mrhinkle@linux:~$ chmod 444 example.txt
mrhinkle@linux:~$ rm example.txt
rm: write-protected regular file `example.txt`? n
```

作为一个预防性步骤，你可能希望将文件的所有者更改另一个仅具有只读属性的用户。例如，以 mrhinkle 身份登录的用户如果文件不是所有人可写或组可写，那么他无法删除由 mark 用户拥有的文件。

你可能甚至想创建一个归档用户。然后使用 `chown` 命令将所有者“更改”为 archive。请记住，要执行此操作，你必须拥有该文件的权限，因此作为 root 用户来操作很容易完成。其语法如下：

```bash
root@linux:-> chown mark example.txt
```

在示例中，`example.txt` 的所有权被更改为用户 mark。如果你想将文件所有权从一个用户转移到另一个用户，你可能需要以 root 用户身份登录，然后使用 `chown` 将文件所有权从一个所有者更改为另一个。当员工离开公司，你想移动并更改其文件的所有权到另一个用户的 `/home` 目录时，这可能是必要的。确保你记得更改所有权，即使你将文件移动到另一个目录，它们也不一定属于其所在目录的所有者。普通用户可能永远不会深入研究文件权限的细节，但系统管理员或 IT 支持人员可能需要经常使用这种做法。现在你已经对所有权有了基本的概述，可以开始查看用户是如何执行进程的。

# 进程
