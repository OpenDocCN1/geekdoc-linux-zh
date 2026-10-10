
### 大多数实用程序不保留 ACLs

**注意** 当使用 `-p`（保留）或 `-a`（归档）选项时，`cp` 在复制文件时保留 ACLs。`mv` 实用程序也保留 ACLs。当你使用 `cp` 配合 `-p` 或 `-a` 选项且无法复制 ACLs，或者 `mv` 无法保留 ACLs 时，实用程序会执行操作并发出错误消息：

```
$ mv report /tmp
mv: preserving permissions for '/tmp/report': Operation not supported
```

其他实用程序，如 `tar`、`cpio` 和 `dump`，不支持 ACLs。你可以使用带有 `-a` 选项的 `cp` 来复制目录层级结构，包括 ACLs。

你永远无法将 ACLs 复制到不支持 ACLs 的文件系统，或未开启 ACL 支持的文件系统。

### 启用 ACLs

在使用 ACLs 之前，你必须安装 `acl` 软件包：

```
$ sudo aptitude install acl
```

Ubuntu Linux 仅正式支持在 `ext2`、`ext3` 和 `ext4` 文件系统上使用 ACLs，尽管其他文件系统也提供非正式的 ACL 支持。要在 `ext2/ext3/ext4` 文件系统上使用 ACLs，你必须使用 `acl` 选项挂载设备（默认是 `no_acl`）。例如，如果你想挂载由 `/home` 表示的设备，以便在 `/home` 中的文件上使用 ACLs，你可以在 `/etc/fstab` 中的选项列表中添加 `acl`：

```
$ grep home /etc/fstab
LABEL=/home			/home			 ext4	 defaults,acl	 1 2
```

`remount` 选项 修改 `fstab` 后，在使用 ACLs 之前，你需要重新挂载 `/home`。如果没有其他人使用系统，你可以卸载并重新挂载它（以 `root` 权限运行），只要工作目录不在 `/home` 层级中即可。或者，你可以使用 `remount` 选项在设备被使用时重新挂载 `/home`：

```
$ sudo mount -v -o remount /home
/dev/sda3 on /home type ext4 (rw,acl)
```

有关 `fstab` 的信息，请参阅第 510 页；有关 `mount` 的信息，请参阅第 506 页。

### 使用访问规则

`setfacl` 实用程序修改文件的 ACL，`getfacl` 显示文件的 ACL。当你使用 `getfacl` 获取没有 ACL 的文件的信息时，它会显示与 `ls -l` 命令相同的信息，只是格式不同：

```
$ ls -l report
-rw-r--r-- 1 max max 9537 2010-01-12 23:17 report

$ getfacl report
# file: report
# owner: max
# group: max
user::rw-
group::r--
other::r--
```

`getfacl` 输出的前三行组成页眉；它们指定文件名、文件所有者以及文件所属的组。更多信息请参阅第 215 页的“`ls -l`: 显示权限”。`--omit-header`（或仅 `-o`）选项使 `getfacl` 不显示页眉：

```
$ getfacl --omit-header report
user::rw-
group::r--
other::r--
```

在以 `user` 开头的行中，中间没有名称的两个冒号（`::`）表示该行指定文件所有者的权限。类似地，`group` 行中的两个冒号表示该行指定文件所属组的权限。跟随 `other` 的两个冒号是为了保持一致性：`other` 不能关联任何名称。

`setfacl --modify`（或 `-m`）选项使用以下格式向文件的 ACL 中添加或修改一个或多个规则：

```
setfacl --modify ugo:name:permissions file-list
```

其中 `ugo` 可以是 `u`、`g` 或 `o`，分别表示命令为用户、组或其他所有用户设置文件权限；`name` 是正在设置权限的用户或组的名称；`permissions` 是采用符号或绝对格式的权限；`file-list` 是要应用权限的文件列表。当你为其他用户（`o`）指定权限时，必须省略 `name`。符号权限使用字母表示文件权限（`rwx`、`r-x` 等），而绝对权限使用八进制数。虽然 `chmod` 使用三组权限或三个八进制数（分别用于所有者、组和其他用户），但 `setfacl` 使用一组权限或一个八进制数来表示授予由 `ugo` 和 `name` 表示的用户或组的权限。有关文件权限的符号和绝对表示的更多信息，请参阅第 216 页关于 `chmod` 的讨论。

例如，以下两个命令都在 `report` 文件的 ACL 中添加了一条规则，授予 `Sam` 对该文件的读和写权限：

```
$ setfacl --modify u:sam:rw- report
```

或者

```
$ setfacl --modify u:sam:6 report
$ getfacl report
# file: report
# owner: max
# group: max
user::rw-
user:sam:rw-
group::r--
mask::rw-
other::r--
```

包含 `user:sam:rw-` 的行表明名为 `sam` 的用户对该文件具有读和写访问权限（`rw-`）。关于如何读取访问权限的解释，请参阅第 215 页。有关以 `mask` 开头的行的描述，请参阅以下可选章节。

当文件拥有 ACL 时，`ls -l` 在权限后显示加号（+），即使 ACL 为空：

```
$ ls -l report
-rw-rw-+ 1 max max 9537 2010-01-12 23:17 report
```

## 可选：有效权限掩码

以 `mask` 开头的行指定了`有效权限掩码`。此掩码限制了授予 ACL 组和用户的有效权限。它不会影响文件的所有者或与文件关联的组。换句话说，它不会影响传统的 Linux 权限。然而，由于 `setfacl` 始终将有效权限掩码设置为文件 ACL 权限中限制最少的一组，因此除非您在为文件设置 ACL 后明确设置掩码，否则掩码不会起作用。您可以通过在 `setfacl` 命令中用 `mask` 替换 `ugo` 并且不指定 `名称` 来设置掩码。

以下示例将 `report` 文件的有效权限掩码设置为读取：

```
$ setfacl -m mask::r-- report
```

以下 `getfacl` 输出中的掩码行显示有效权限掩码被设置为读取 (r---)。显示 `Sam` 文件访问权限的行显示权限仍设置为读写。然而，该行右端的注释显示其有效权限为读取。

```
$ getfacl report
# file: report
# owner: max
# group: max
user::rw-
user:sam:rw-                              #effective:r--
group::r--
mask::r--
other::r--
```

如下一个示例所示，`setfacl` 可以修改 ACL 规则，并且一次可以设置多条 ACL 规则：

```
$ setfacl -m u:sam:r--,u:zach:rw- report

$ getfacl --omit-header report
user::rw-
user:sam:r--
user:zach:rw-
group::r--
mask::rw-
other::r--
```

`-x` 选项会移除某个用户或组的 ACL 规则。它不影响文件的所有者或与文件关联的组的权限。下一个示例展示了 `setfacl` 移除赋予 `Sam` 文件访问权限的规则：

```
$ setfacl -x u:sam report

$ getfacl --omit-header report
user::rw-
user:zach:rw-
group::r--
mask::rw-
other::r--
```

使用 `-x` 选项时，您不得指定 `权限`。相反，仅指定 `ugo` 和 `名称`。仅后跟文件名的 `-b` 选项会移除文件指定文件目录的所有 ACL 规则和 ACL 本身。

`setfacl` 和 `getfacl` 都有许多选项。使用 `--help` 选项显示选项的简要列表，或参阅 `man` 手册页以获取详细信息。

## 为目录设置默认规则

以下示例显示 `dir` 目录最初没有 ACL。`setfacl` 命令使用 `-d` (`默认`) 选项为 `dir` 的 ACL 添加两条默认规则。这些规则适用于 `dir` 目录中没有显式 ACL 的所有文件。这些规则赋予 `pubs` 组成员读取和执行权限，并赋予 `admin` 组成员读取、写入和执行权限。

```
$ ls -ld dir
drwx------ 2 max max 4096 2010-02-12 23:15 dir
$ getfacl dir
# file: dir
# owner: max
# group: max
user::rwx
group::---
other::---

$ setfacl -d -m g:pubs:rx,g:admin:rwx dir
```

以下 `ls` 命令显示 `dir` 目录现在拥有 ACL，如权限右侧的 + 所示。`getfacl` 显示的每条默认规则都以 `default:` 开头。前两条默认规则和最后一条默认规则指定了文件的所有者、与文件关联的组以及所有其他用户的权限。这三个规则指定传统的 Linux 权限，并优先于其他 ACL 规则。第三和第四条规则指定 `pubs` 和 `admin` 组的权限。接着是默认的有效权限掩码。

```
$ ls -ld dir
drwx------ 2 max max 4096 2010-02-12 23:15 dir
$ getfacl dir
# file: dir
# owner: max
# group: max
user::rwx
group::---
other::---
default:user::rwx
default:group::---
default:group:pubs:rx
default:group:admin:rwx
default:mask::rwx
default:other::---
```

请记住，默认规则适用于目录中未显式分配 ACL 的文件。您也可以为目录本身指定访问规则。当您在具有默认规则的 ACL 的目录中创建文件时，该文件的有效权限掩码将根据文件的权限创建。在某些情况下，掩码可能会覆盖默认 ACL 规则。

在下一个示例中，`touch` 在 `dir` 目录中创建了一个名为 `new` 的文件。`ls` 命令显示该文件拥有 ACL。基于 `umask` 的值（第 459 页），文件的所有者以及与文件关联的组对该文件拥有读取和写入权限。有效权限掩码设置为读取和写入，因此 `pubs` 的有效权限为读取，`admin` 的有效权限为读取和写入。两个组都没有执行权限。

```
$ cd dir
$ touch new
$ ls -l new
-rw-rw----+ 1 max max 0 2010-02-13 00:39 new
$ getfacl --omit new
user::rw-
group::---
group:pubs:r-x                    #effective:r--
group:admin:rw+                   #effective:rw-
mask::rw-
other::---
```

如果您将文件的传统权限更改为所有者和组的读取、写入和执行，有效权限掩码将更改为读取、写入和执行，并且默认规则指定的组将获得该文件的执行访问权限。

```
$ chmod 770 new
$ ls -l new
-rwxrwx---+ 1 max max 0 2010-02-13 00:39 new
$ getfacl --omit new
user::rwx
group::r-x
group:pubs:r-x
group:admin:rwx
mask::rwx
other::---
```

## 链接

`链接` 是指向文件的指针。每次使用 `vim`、`touch`、`cp` 或通过其他方式创建文件时，您实际上是在目录中放入一个指针。该指针将文件名与磁盘上的某个位置关联起来。当您在命令中指定文件名时，您实际上是间接指向磁盘上存储您所需信息的位置。

![](img/2344fc4a798f29dca9e8b5ed7288171a_277_0.png)

当两个人或更多人正在处理同一个项目并需要共享某些信息时，共享文件会很有用。通过为文件创建额外的链接，您可以轻松让其他用户访问您的某个文件。

要与另一个用户共享文件，首先必须给予该用户读取和写入文件的权限（第 216 页）。您可能还必须更改文件父目录的访问权限，以赋予该用户读取、写入或执行权限（第 220 页）。一旦权限设置得当，该用户就可以创建指向该文件的链接，以便你们每个人都可以从各自的目录层次结构访问该文件。

对于拥有大型目录层次结构的单个用户来说，链接也很有用。您可以创建链接来对目录层次结构中的文件进行交叉分类，使用不同的分类来处理不同的任务。例如，如果您拥有第 201 页图 6-2 中描绘的文件布局，名为 `to_do` 的文件可能出现在 `correspond` 目录的每个子目录中——即在 `personal`、`memos` 和 `business` 中。如果您发现难以追踪需要做的所有事情，您可以在 `correspond` 目录中创建一个名为 `to_do` 的独立目录。然后，您可以将每个子目录的待办事项列表链接到该目录中。例如，您可以将 `memos` 目录中名为 `to_do` 的文件链接到 `to_do` 目录中名为 `memos` 的文件。这组链接在图 6-13 中展示。

虽然听起来可能很复杂，但这种技术将所有待办事项列表方便地保存在一个地方。当您忙于写信、写备忘录或处理个人事务时，相关的列表可以方便地在任务相关目录中访问。

### 关于硬链接的讨论

> 存在两种类型的链接：硬链接和符号（软）链接。硬链接较旧，且正在变得过时。硬链接部分标记为可选；您可以跳过，尽管它讨论了 inode 并为您提供对文件系统结构的洞察。

## 可选

## 硬链接

指向文件的硬链接看起来像另一个文件。如果该文件出现在与被链接文件相同的目录中，链接必须具有不同的文件名，因为同一目录中的两个文件不能具有相同的名称。您只能在包含该文件的文件系统中创建指向该文件的硬链接。

### ln：创建硬链接

`ln` (link) 工具（不带 `-s` 或 `— symbolic` 选项）使用以下语法为现有文件创建硬链接：

```
ln existing-file new-link
```

下一条命令展示了 `Zach` 通过在其家庭目录中创建指向名为 `draft` 的现有文件的名为 `/home/max/letter` 的新链接，创建了图 6-14 中所示的链接：

```
$ pwd
/home/zach
$ ln draft /home/max/letter
```

新链接出现在 `/home/max` 目录中，文件名为 `letter`。实际上，`Max` 可能需要更改目录权限，以便 `Zach` 能够创建该链接。尽管 `/home/max/letter` 出现在 `Max` 的目录中，但 `Zach` 是该文件的所有者，因为他创建的是指向该文件的链接（注：原文逻辑指 `Zach` 执行了链接操作，通常硬链接的所有者属性在创建链接后可能保持原文件不变或根据系统具体行为，此处按原文翻译“Zach is the owner of the file because he created it”意指他创建了链接/或者原文语境下他认为自己是发起者，但严格意义上硬链接共享 inode，所有者通常继承原文件。此处忠实翻译原文表达）。

`ln` 工具为现有文件创建了一个额外的指针，但不会创建文件的另一份副本。因为只有一个文件，所以文件状态信息——如访问权限、所有者和文件最后修改时间——对所有链接都是相同的；只有文件名不同。例如，当 `Zach` 修改 `/home/zach/draft` 时，`Max` 在 `/home/max/letter` 中看到的变化。

![](img/2344fc4a798f29dca9e8b5ed7288171a_278_0.png)

# cp 与 ln 的对比

以下命令可验证 `ln` 不会对文件进行额外复制。创建一个文件，使用 `ln` 为该文件创建一个额外的链接，通过其中一个链接修改文件内容，然后通过另一个链接验证该修改：

```
$ cat file_a
This is file A.
$ ln file_a file_b
$ cat file_b
This is file A.
$ vim.tiny file_b
....
$ cat file_b
This is file B after the change.
$ cat file_a
This is file B after the change.
```

如果尝试使用 `cp` 代替 `ln` 进行相同的实验，并修改文件的副本，这两种工具之间的区别将更加明显。一旦修改了文件的副本，这两个文件就会变得不同：

```
$ cat file_c
This is file C.
$ cp file_c file_d
$ cat file_d
This is file C.
$ vim.tiny file_d
....
$ cat file_d
This is file D after the change.
$ cat file_c
This is file C.
```

# ls 与链接计数
