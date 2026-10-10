
| 八进制值 | 权限 | 含义 |
| --- | --- | --- |
| 3 | -wx | 写和执行 |
| 4 | r-- | 只读 |
| 5 | r-x | 读和执行 |
| 6 | rw- | 读和写 |
| 7 | rwx | 读、写和执行 |

必须按照正确的顺序指定所有者、组和其他人的三个八进制值，如清单 15.4 所示。

### 清单 15.4：使用八进制模式分配权限

```bash
$ chmod 664 research.txt
$ ls -l
total 12
-rw-r-- 1 Christine marketing 1521 Jan 19 15:38 customers.txt
-rw-rw-- 1 Christine sales 479 Jan 19 15:37 research.txt
-rwxrwx-- 1 Christine sales 696 Jan 19 15:37 salesdata.txt
$ 
```

八进制模式 664 将所有者和组的权限设置为读写（6），但将其他人的权限设置为只读（4）。你可以从 `ls` 输出中查看结果。这是一种方便的方式，可以在单个命令中为文件或目录设置所有权限。

### 探索特殊权限

Linux 使用三个特殊权限位来控制文件和目录的高级行为。

Set User ID (SUID) 位用于可执行文件。它告诉 Linux 内核以文件所有者的权限运行程序，而不是以实际运行该文件的用户账户的权限。此功能最常用于必须作为 root 用户账户运行的服务器应用程序，以便能够访问系统上的所有文件，即使启动进程的用户是标准用户。

SUID 位通过用字母 s 替代文件所有者的执行权限字母来表示：`rwsr-xr-x`。假设系统运行该文件需要执行权限。如果在一个对所有者没有执行权限的文件上设置了 SUID 位，则用大写字母 S 表示。

要为文件设置 SUID 位，在符号模式下将 s 添加到所有者权限中，或在八进制模式下在八进制模式设置的开头包含 4：

```bash
# chmod u+s myapp
# chmod 4750 myapp
```

Set Group ID (SGID，也称为 GUID) 位在文件和目录中的工作方式不同。对于文件，它告诉 Linux 以文件的组权限运行程序文件。它在组执行位位置中由 s 表示：`rwxrwSr--`。

对于目录，SGID 位帮助我们创建一个多个用户可以共享文件的环境。当目录设置了 SGID 位时，用户在该目录中创建的任何文件都会被分配为该目录的组，而不是该用户的组。这样，该组中的所有用户都可以拥有与共享目录中所有文件相同的权限。

要设置 SGID 位，在符号模式下将 s 添加到组权限中，或在八进制模式下在八进制模式设置的开头包含 2：

```bash
# chmod g+s /sales
# chmod 2660 /sales
```

最后，sticky bit 用于保护文件不被非所有者删除，即使他们属于对文件具有写权限的组。sticky bit 用 t 表示其他人执行位位置：`rwxrw-r-t`。

sticky bit 经常用于由他人共享的目录。组成员对目录中包含的数据文件具有读和写权限，但只有文件所有者才能从共享目录中删除文件。

要设置 sticky bit，在符号模式下将 t 添加到**其他**权限中，或在八进制模式下在八进制模式设置的开头包含 1：

```bash
# chmod o+t /sales
# chmod 1777 /sales
```

### 管理默认权限

当用户创建新文件或目录时，Linux 系统会为其分配默认的所有者、组和权限。默认所有者，顾名思义，是创建该文件的用户。默认组是所有者的主组。

用户掩码功能定义了 Linux 分配给文件或目录的默认权限。用户掩码是一个八进制值，代表要从文件的八进制模式 666 权限或目录的八进制模式 777 权限中移除的位。

用户掩码值通过 `umask` 命令设置。你可以通过在命令行上单独输入该命令来查看当前的 umask 设置：

```bash
$ umask
0022
$
```

`umask` 命令的输出显示四个八进制值。第一个八进制值代表分配给你创建的文件和目录的 SUID (4)、GUID (2) 和 sticky (1) 位的掩码。接下来三个八进制值分别对应所有者、组和其他人的权限设置的掩码。

掩码是应用于文件或目录权限位的按位掩码。掩码中设置的任何位都会从文件或目录的权限中移除。如果某个位未设置，则掩码不会更改该设置。表 15.2 演示了在你的 Linux 系统上创建文件和目录时，umask 值在实际中是如何工作的。

### 表 15.2 文件和目录常见 umask 值的结果

| umask | 创建的文件 | 创建的目录 |
| :---- | :------------ | :------------------ |
| 000 | 666 (rw-rw-rw- ) | 777 (rwxrwxrwx) |
| 002 | 664 (rw-rw-r--) | 775 (rwxrwxr-x) |
| 022 | 644 (rw-r--r--) | 755 (rwxr-xr-x) |
| 027 | 640 (rw-r----) | 750 (rwxr-x--) |
| 077 | 600 (rw------) | 700 (rwx-----) |
| 277 | 400 (r-------) | 500 (r-x-----) |

你可以通过在 Linux 系统上创建新文件和目录来测试这一点：

```bash
$ mkdir test1
$ touch test2
$ ls -l
total 4
drwxr-xr-x 2 rich rich 4096 Jan 19 17:08 test1
-rw-r--r-- 1 rich rich 0 Jan 19 17:08 test2
$
```

如预期那样（注意目录条目的权限列表以 d 开头），umask 值 0022 为 test2 文件创建了默认文件权限 rw-r--r--，即八进制 644，为 test1 目录创建了 rwxr-xr-x，即八进制 755。

你可以通过从命令行使用 umask 命令来更改用户账户的默认 umask 设置：

```bash
$ umask 027
$ touch test3
$ ls -l test3
-rw-r----- rich rich 0 Jan 19 17:12 test3
$
```

新文件的默认权限已更改为匹配 umask 设置。

![](img/c0a399aca0d18f8822d714ad0a173123_513_0.png)

umask 值通常设置在 Linux 系统在登录时运行的脚本中，例如在 /etc/profile 文件中。如果你从命令行覆盖该设置，它仅在你的会话期间有效。你可以通过将其添加到 $HOME 目录中的 .bash_profile 文件来覆盖系统默认的 umask 设置。

### 访问控制列表

Linux 的基本权限方法有一个缺点，即它有些有限。你只能为文件或目录分配给单个组或用户账户的权限。在需要不同组人员对文件和目录拥有不同权限的复杂业务环境中，这种方法行不通。

Linux 开发人员发明了一种更高级的文件和目录安全方法，称为*访问控制列表* (ACL)。ACL 允许你指定多个用户或组的列表以及分配给它们的权限。就像基本安全方法一样，ACL 权限使用相同的读、写和执行权限位，但现在可以将它们分配给多个用户和组。

要在 Linux 中使用 ACL 功能，你使用 `setfacl` 和 `getfacl` 命令。`getfacl` 命令允许你查看分配给文件或目录的 ACL，如清单 15.5 所示。

### 清单 15.5：查看文件的 ACL

```bash
$ touch test
$ ls -l
total 0
-rw-r----- 1 rich rich 0 Jan 19 17:33 test
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
other::---
$
```

如果你只分配了基本安全权限给文件，这些权限仍然会出现在 `getfacl` 输出中，如清单 15.5 所示。

要为额外的用户或组分配权限，你使用 `setfacl` 命令：

```bash
setfacl [options] rule filenames
```

`setfacl` 命令允许你使用 `-m` 选项修改分配给文件或目录的权限，或使用 `-x` 选项移除特定权限。你用三种格式定义规则：

```text
u[ser]:uid:perms
g[roup]:gid:perms
o[ther]:perms
```

要为额外的用户账户分配权限，使用用户格式；为额外的组，使用组格式；为其他人，使用其他格式。对于 uid 或 gid 值，你可以使用数字用户标识号或组标识号，也可以使用名称。这是一个例子：

```bash
$ setfacl -m g:sales:rw test
$ ls -l
total 0
-rw-rw----+ 1 rich rich 0 Jan 19 17:33 test
$
```

此示例为 sales 组添加了 test 文件的读和写权限。注意 `setfacl` 命令没有输出。当你列出文件时，只显示标准的所有者、组和其他人的权限，但在权限列表中添加了加号 (+)。这表明该文件应用了额外的 ACL。要查看额外的 ACL，再次使用 `getfacl` 命令：

```bash
$ getfacl test
# file: test
# owner: rich
# group: rich
user::rw-
group::r--
group:sales:rw-
mask::rw-
other::---
$
```

`getfacl` 输出现在显示有两个组被分配了权限。默认文件组 (rich) 被分配了读权限，但现在 sales 组对该文件具有读和写权限。要移除权限，使用 `-x` 选项：

```bash
$ setfacl -x g:sales test
$ getfacl test
# file: test
# owner: rich
# group: rich
```
