
## 链接文件

![](img/c27875544958897d817484d558c208c8_176_0.png)

### 图 4-1 硬链接文件的结构

硬链接文件可以在图 4-1 中看到。你可以无限次地为文件创建硬链接；但是，硬链接文件必须位于同一个文件系统上。

要创建硬链接，你必须使用 **ln (link)** 命令并指定两个参数：要创建硬链接的现有文件和将作为现有文件的硬链接创建的目标文件。每个参数可以是文件的绝对路径或相对路径。以根用户主目录的以下内容为例：

```
[root@server1 ~]# ls -l
total 520
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-x 1 root root 519964 Apr 7 09:59 file1
-rw-r--xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

假设你想要为 file1 创建一个硬链接，并将新的硬链接命名为 file2，如图 4-1 所示。为了实现这一点，你需要在命令提示符处输入命令 **ln file1 file2**；名为 file2 的文件将被创建，并与 file1 硬链接。要在创建后查看硬链接的文件名，你可以使用 `ls -l` 命令：

```
[root@server1 ~]# ln file1 file2
[root@server1 ~]# ls -l
total 1032
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-x 1 root root 519964 Apr 7 09:59 file1
-rw-r--xr-x 2 root root 519964 Apr 7 09:59 file2
-rw-r--xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

从上面的长列表中可以看出，file1 和 file2 共享同一个 inode 和数据段，因为它们具有相同的大小、权限、所有权、修改日期等。还要注意，file1 的链接数（权限组后面的数字）在上面的输出中从 1 增加到了 2。链接数为 1 表示只有一个 inode 由文件共享。如果一个文件与另一个文件硬链接，则共享两个 inode，因此其链接数为 2。类似地，一个文件如果与另外三个文件硬链接，则共享四个 inode，因此其链接数为 4。

尽管硬链接共享同一个 inode 和数据段，但删除一个硬链接文件并不会删除其他所有硬链接文件；它只是移除一个文件名引用。删除硬链接可以通过移除其中一个文件来实现，这会导致链接数降低。

要查看硬链接文件的 inode 编号以验证它们是否相同，除了其他选项外，你还可以使用 `ls` 命令的 `-i` 选项。inode 编号位于目录列表中每一行的左侧，如下面的输出所示：

```
[root@server1 ~]# ls -li
total 1032
37595 drwx------ 3 root root 4096 Apr 8 07:12 Desktop
1204 -rwxr-xr-x 2 root root 519964 Apr 7 09:59 file1
1204 -rwxr-xr-x 2 root root 519964 Apr 7 09:59 file2
17440 -rwxr-xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_177_0.png)

> 目录文件通常不会被硬链接，因为结果将包含两个内容相同的目录。然而，在某些情况下，root 用户可以使用 `ln` 命令的 `-F` 或 `-d` 选项来硬链接目录。通常只有那些经常添加文件且需要保持相同文件内容的目录才会被硬链接。例如，在 Fedora 20 中，`/etc/init.d` 目录被符号链接到 `/etc/rc.d/init.d` 目录。

符号链接（如图 4-2 所示）与硬链接不同，因为它们不与其目标文件共享相同的 inode 和数据块；一个是另一个的指针，因此两个文件具有不同的大小。符号链接文件中的数据块仅包含目标文件的路径名。当用户编辑符号链接文件时，实际上是在编辑目标文件。因此，如果目标文件被删除，符号链接将不起作用，因为它指向一个不存在的文件。

![](img/c27875544958897d817484d558c208c8_177_1.png)

> 符号链接有时被称为“软链接”或“symlinks”。

要创建符号链接，你需要使用 `ln` 命令的 `-s` 选项。要创建一个指向 file3 的名为 file4 的符号链接，如图 4-2 所示，你可以在命令提示符处输入 `ln -s file3 file4`。与硬链接一样，指定的参数可以是绝对路径或相对路径。

![](img/c27875544958897d817484d558c208c8_177_2.png)

### 图 4-2 符号链接文件的结构

要在创建后查看符号链接的文件名，你可以使用 `ls -l` 命令，如下面的示例所示：

```
[root@server1 ~]# ls -l file3 file4
[root@server1 ~]# ls -l
total 1032
drwx------   3 root  root     4096 Apr  8 07:12 Desktop
-rwxr-xr-x   2 root  root    519964 Apr  7 09:59 file1
-rwxr-xr-x   2 root  root    519964 Apr  7 09:59 file2
-rwxr-xr-x   1 root  root      1244 Apr 27 18:17 file3
lrwxrwxrwx   1 root  root        5 Apr 27 19:05 file4 -> file3
[root@server1 ~]# _
```

从上面的输出中可以看出，file4 不共享相同的 inode，因为其权限、大小和修改日期与 file3 不同。此外，符号链接比硬链接更容易识别；文件类型字符（在权限之前）是 `l`，表示这是一个符号链接，并且文件名使用箭头指向目标。`ls -F` 命令还通过附加一个 `@` 符号来指示符号链接，如下面的输出所示：

```
[root@server1 ~]# ls -F
Desktop/  file1*  file2*  file3*  file4@
[root@server1 ~]# _
```

硬链接和符号链接之间的另一个区别在于，符号链接不需要与其目标位于同一个文件系统上。相反，它们指向目标文件名，并且不需要相同的 inode，如下面的输出所示：

```
[root@server1 ~]# ls -li
37595 drwx------   3 root  root     4096 Apr  8 07:12 Desktop
1204  -rwxr-xr-x   2 root  root    519964 Apr  7 09:59 file1
1204  -rwxr-xr-x   2 root  root    519964 Apr  7 09:59 file2
17440 -rwxr-xr-x   1 root  root      1244 Apr 27 18:17 file3
19926 lrwxrwxrwx   1 root  root        5 Apr 27 19:05 file4 -> file3
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_178_0.png)

与硬链接不同，符号链接通常指向目录，以简化文件系统树的导航。此外，指向目录的符号链接通常用于与其他 UNIX 和 Linux 系统保持兼容性。例如，在 Fedora 20 中，出于此原因，`/usr/tmp` 目录被符号链接到 `/var/tmp` 目录。

## 文件和目录权限

请记住，所有用户都必须使用用户名和密码登录才能访问 Linux 系统。登录后，用户通过其用户名和所属组进行识别；对所有资源的访问取决于用户名和所属组是否具有所需的权限。因此，为了以安全的方式操作 Linux 系统并防止未经授权的访问敏感文件、目录和命令的用户，对所有权和权限的牢固理解是必要的。

## 文件和目录所有权

当用户创建一个文件或目录时，该用户的姓名和**主组**分别成为该文件的所有者和组所有者。这会影响权限结构，正如你在下一节中看到的那样；但它也决定了谁有能力修改文件和目录的权限和所有权。在 Linux 系统上，只有两个用户可以修改文件或目录的权限或更改其所有权：文件/目录的所有者和 root 用户。

要查看你当前的用户名，你可以使用 `whoami` 命令。要查看你的组成员身份和主组，你可以使用 `groups` 命令。作为 root 用户登录时这两个命令的示例如下面的输出所示：

```
[root@server1 ~]# whoami
root
[root@server1 ~]# groups
root bin daemon sys adm disk wheel
[root@server1 ~]#
```

从上面的输出中可以看出，root 用户是七个组的成员，但 root 用户的主组也称为“root”，因为它是 `groups` 命令输出中提到的第一个组。

![](img/c27875544958897d817484d558c208c8_179_0.png)

如果 root 用户创建一个文件，所有者是“root”，组所有者也是“root”。要快速创建一个空文件，你可以使用 `touch` 命令：

```
[root@server1 ~]# touch file1
[root@server1 ~]# ls -l
total 4
drwx------   3 root    root   4096 Apr  8 07:12 Desktop
-rw-r--r--   1 root    root      0 Apr 29 15:40 file1
[root@server1 ~]#
```

从上面的输出中可以看出，file1 的所有者是“root”，组所有者是“root”组。要更改文件或目录的所有权，你可以使用 `chown` (change owner) 命令，该命令至少需要两个参数：新所有者和要更改的文件或目录。两个参数都可以是绝对路径或相对路径，你还可以使用 `chown` 命令的 `-R` 选项递归地更改目录树中的权限。要将 file1 的所有权更改为用户 user1，并将 Desktop 目录及其所有内容的所有权也更改为 user1，你可以输入以下命令：

```
[root@server1 ~]# chown user1 file1
[root@server1 ~]# chown -R user1 Desktop
[root@server1 ~]# ls -l
total 4
drwx------   3 user1   root   4096 Apr  8 07:12 Desktop
-rw-r--r--   1 user1   root      0 Apr 29 15:40 file1
```

