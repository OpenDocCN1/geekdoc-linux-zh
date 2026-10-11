

使用 `-x` 选项时，你不能指定 `permissions`。相反，只需指定 `ugo` 和 `name`。仅跟随文件名的 `-b` 选项会移除你指定的文件或目录中的所有 ACL 规则以及 ACL 本身。

`setfacl` 和 `getfacl` 都有许多选项。使用 `--help` 选项可显示选项的简要列表，或参阅 man 页面以获取详细信息。

## 为目录设置默认规则

以下示例显示 `dir` 目录最初没有 ACL。`setfacl` 命令使用 `-d` 选项为 `dir` 的 ACL 添加两个默认规则。这些规则适用于 `dir` 目录中所有未明确设置 ACL 的文件。这些规则授予 `pubs` 组成员读取和执行权限，并授予 `admin` 组成员读取、写入和执行权限。

```bash
$ ls -ld dir
drwx------ 2 max max 4096 Feb 12 23:15 dir
$ getfacl dir
# file: dir
# owner: max
# group: max
user::rwx
group::---
other::---

$ setfacl -d -m g:pubs:r-x,g:admin:rw dir
```

以下 `ls` 命令显示 `dir` 目录现在有一个 ACL，如权限右侧的 + 所示。`getfacl` 显示的每个默认规则都以 `default:` 开头。前两个默认规则和最后一个默认规则指定文件所有者、文件所属组以及其他所有用户的权限。这三个规则指定了传统的 Linux 权限，并且优先于其他 ACL 规则。第三和第四个规则指定了 `pubs` 和 `admin` 组的权限。接下来是默认的有效权利掩码。

```bash
$ ls -ld dir
drwx------ + 2 max max 4096 Feb 12 23:15 dir
$ getfacl dir
# file: dir
# owner: max
# group: max
user::rwx
group::---
other::---
default:user::rwx
default:group::---
default:group:pubs:r-x
default:group:admin:rw
default:mask::rwx
default:other::---
```

请记住，默认规则适用于保存在目录中但未明确分配 ACL 的文件。你还可以为目录本身指定访问规则。

当你在具有默认规则的 ACL 的目录中创建文件时，该文件的有效权利掩码是根据该文件的权限创建的。在某些情况下，掩码可能会覆盖默认 ACL 规则。

在下一个示例中，`touch` 在 **dir** 目录中创建了一个名为 **new** 的文件。`ls` 命令显示该文件有一个 ACL。根据 `umask` 的值（第 440 页），文件所有者和文件所属组对该文件都具有读取和写入权限。有效权利掩码设置为读取和写入，因此 `pubs` 的有效权限是读取，而 **admin** 的有效权限是读取和写入。两个组都没有执行权限。

```bash
$ cd dir
$ touch new
$ ls -1 new
$ getfacl --omit new
user::rw-
group::---
group:pubs:r-x               #effective:r-
group:admin:rwx               #effective:rw-
mask::rw-
other::---
```

如果你将文件的传统权限更改为对所有者和组的读取、写入和执行，有效权利掩码将更改为读取、写入和执行，并且由默认规则指定的组将获得对文件的执行访问权限。

```bash
$ chmod 770 new
$ ls -1 new
-rwxrwx---- 1 max max 0 Feb 13 00:39 new
$ getfacl --omit new
user::rwx
group::---
group:pubs:r-x
group:admin:rw-
mask:rwx
other::---
```

## 链接

链接是指向文件的指针。每次你使用 `vim`、`touch`、`cp` 或任何其他方式创建文件时，你实际上是在目录中放置一个指针。该指针将文件名与磁盘上的位置关联起来。当你在命令中指定文件名时，你间接指向了磁盘上保存你想要信息的位置。

![](img/f28adb66a7398a382f0505e0ba74a872_253_0.png)

图 6-13 使用链接对文件进行交叉分类

当两个人或更多人在同一个项目上工作并需要共享某些信息时，共享文件会很有用。通过为文件创建额外的链接，你可以让其他用户轻松访问你的某个文件。

要与另一个用户共享文件，首先授予该用户读取和写入文件的权限（第 204 页）。你可能还需要更改文件父目录的访问权限，以赋予该用户读取、写入或执行权限（第 206 页）。一旦适当设置了权限，用户就可以创建指向该文件的链接，以便你们每个人都可以从各自的目录层次结构中访问该文件。

链接对于拥有大型目录层次结构的单个用户也很有用。你可以创建链接来对目录层次结构中的文件进行交叉分类，为不同的任务使用不同的分类。例如，如果你拥有第 189 页图 6-2 中描绘的文件布局，名为 to_do 的文件可能出现在 correspond 目录的每个子目录中——即 personal、memos 和 business。如果你发现很难跟踪所有需要做的事情，你可以在 correspond 目录中创建一个名为 to_do 的独立目录。然后，你可以将每个子目录的待办事项列表链接到该目录。例如，你可以将 memos 目录中名为 to_do 的文件链接到 to_do 目录中名为 memos 的文件。这组链接如图 6-13 所示。

虽然这听起来可能很复杂，但这种技术可以让你将所有待办事项列表方便地集中在一处。当你忙于写信、写备忘录或处理个人事务时，相关的列表在任务相关目录中很容易访问。

### 关于硬链接的讨论

> **提示** 存在两种链接：硬链接和符号（软）链接。硬链接较旧，正在变得过时。硬链接部分被标记为可选；你可以跳过它，尽管它讨论了 inode 并让你了解文件系统的结构。

## 硬链接

指向文件的硬链接看起来就像另一个文件。如果该文件与链接目标文件出现在同一目录中，链接必须具有不同的文件名，因为同一目录中的两个文件不能具有相同的名称。你只能在持有该文件的文件系统内部创建指向该文件的硬链接。

### ln：创建硬链接

`ln`（link）实用工具（不使用 `-s` 或 `--symlink` 选项）使用以下语法为现有文件创建硬链接：

```bash
ln existing-file new-link
```

下一条命令通过创建一个名为 `/home/alex/letter` 的新链接，指向 Jenny 主目录中名为 `draft` 的现有文件，从而创建图 6-14 中所示的链接：

```bash
$ pwd
/home/jenny
$ ln draft /home/alex/letter
```

新链接出现在 `/home/alex` 目录中，文件名为 `letter`。实际上，Alex 可能需要更改目录和文件权限，以便 Jenny 能够访问该文件。尽管 `/home/alex/letter` 出现在 Alex 的目录中，但 Jenny 是该文件的所有者，因为是她创建了该文件。

`ln` 实用工具为现有文件创建额外的指针，但不会创建文件的另一个副本。因为只有一个文件，文件状态信息——如访问权限、所有者和文件最后修改时间——对所有链接都是相同的；只有文件名不同。例如，当 Jenny 修改 `/home/jenny/draft` 时，Alex 会在 `/home/alex/letter` 中看到更改。

![](img/f28adb66a7398a382f0505e0ba74a872_254_0.png)

图 6-14 指向同一文件的两个链接：`/home/alex/letter` 和 `/home/jenny/draft`

### cp 与 ln 的区别

以下命令验证 `ln` 不会创建文件的额外副本。创建一个文件，使用 `ln` 为该文件创建额外的链接，通过一个链接更改文件内容，并通过另一个链接验证更改：

```bash
$ cat file_a
This is file A.
$ ln file_a file_b
$ cat file_b
This is file A.
$ vim file_b
...
$ cat file_b
This is file B after the change.
$ cat file_a
This is file B after the change.
```

如果你尝试使用 `cp` 代替 `ln` 进行相同的实验，并更改文件的一个*副本*，这两个实用工具之间的区别将变得更加清晰。一旦更改了文件的*副本*，这两个文件就不同了：

```bash
$ cat file_c
This is file C.
$ cp file_c file_d
$ cat file_d
This is file C.
$ vim file_d
...
$ cat file_d
This is file D after the change.
$ cat file_c
This is file C.
```

#### ls 和链接计数

你可以使用带有 `-l` 选项的 `ls`，后接要比较的文件名，以确认指向同一文件的两个链接具有相同的状态信息，而未链接的文件具有不同的状态信息。在以下示例中，链接字段中的 `2`（紧挨在 *alex* 左侧）表示 *file_a* 和 *file_b* 有两个链接：

```bash
$ ls -l file_a file_b file_c file_d
-rw-r--r-- 2 alex pubs 33 May 24 10:52 file_a
-rw-r--r-- 1 alex pubs 33 May 24 10:52 file_b
-rw-r--r-- 1 alex pubs 16 May 24 10:55 file_c
-rw-r--r-- 1 alex pubs 33 May 24 10:57 file_d
```

尽管在这个示例中很容易猜测哪些文件相互链接，但 `ls` 并没有明确告诉你。

#### ls 和 inode

使用带有 `-i` 选项的 `ls` 来确定哪些文件是链接，以免产生疑问。`-i` 选项列出每个文件的 *inode*（第 1087 页）编号。inode 是文件的控制结构。如果两个文件名具有相同的 inode 编号，它们共享相同的控制结构，并且是同一文件的链接。反之，当两个文件名具有不同的 inode 编号时，它们是不同的文件。以下示例

