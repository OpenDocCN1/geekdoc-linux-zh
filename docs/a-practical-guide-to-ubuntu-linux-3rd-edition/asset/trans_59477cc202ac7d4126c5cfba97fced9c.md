
## 可选：有效权限掩码

以 **mask** 开头的行指定了*有效权限掩码*。此掩码限制了授予 ACL 组和用户的有效权限。它不会影响文件的所有者或与文件关联的组。换句话说，它不会影响传统的 Linux 权限。然而，由于 **setfacl** 始终将有效权限掩码设置为文件 ACL 权限中限制最少的一组，因此除非您在为文件设置 ACL 后明确设置掩码，否则掩码不会起作用。您可以通过在 **setfacl** 命令中用 **mask** 替换 **ugo** 并且不指定 *名称* 来设置掩码。

以下示例将 **report** 文件的有效权限掩码设置为读取：

```
$ setfacl -m mask::r-- report
```

以下 **getfacl** 输出中的掩码行显示有效权限掩码被设置为读取 (r---)。显示 Sam 文件访问权限的行显示权限仍设置为读写。然而，该行右端的注释显示其有效权限为读取。

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

如下一个示例所示，**setfacl** 可以修改 ACL 规则，并且一次可以设置多条 ACL 规则：

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

-x 选项会移除某个用户或组的 ACL 规则。它不影响文件的所有者或与文件关联的组的权限。下一个示例展示了 **setfacl** 移除赋予 Sam 文件访问权限的规则：

```
$ setfacl -x u:sam report

$ getfacl --omit-header report
user::rw-
user:zach:rw-
group::r--
mask::rw-
other::r--
```

使用 *-x* 选项时，您不得指定 *权限*。相反，仅指定 *ugo* 和 *名称*。仅后跟文件名的 *-b* 选项会移除文件指定文件目录的所有 ACL 规则和 ACL 本身。

*setfacl* 和 *getfacl* 都有许多选项。使用 *--help* 选项显示选项的简要列表，或参阅 *man* 手册页以获取详细信息。

## 为目录设置默认规则

以下示例显示 *dir* 目录最初没有 ACL。*setfacl* 命令使用 *-d* (*默认*) 选项为 *dir* 的 ACL 添加两条默认规则。这些规则适用于 *dir* 目录中没有显式 ACL 的所有文件。这些规则赋予 *pubs* 组成员读取和执行权限，并赋予 *admin* 组成员读取、写入和执行权限。

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

以下 *ls* 命令显示 *dir* 目录现在拥有 ACL，如权限右侧的 + 所示。*getfacl* 显示的每条默认规则都以 *default:* 开头。前两条默认规则和最后一条默认规则指定了文件的所有者、与文件关联的组以及所有其他用户的权限。这三个规则指定传统的 Linux 权限，并优先于其他 ACL 规则。第三和第四条规则指定 *pubs* 和 *admin* 组的权限。接着是默认的有效权限掩码。

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

在下一个示例中，**touch** 在 **dir** 目录中创建了一个名为 **new** 的文件。**ls** 命令显示该文件拥有 ACL。基于 **umask** 的值（第 459 页），文件的所有者以及与文件关联的组对该文件拥有读取和写入权限。有效权限掩码设置为读取和写入，因此 **pubs** 的有效权限为读取，**admin** 的有效权限为读取和写入。两个组都没有执行权限。

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

*链接* 是指向文件的指针。每次使用 **vim**、**touch**、**cp** 或通过其他方式创建文件时，您实际上是在目录中放入一个指针。该指针将文件名与磁盘上的某个位置关联起来。当您在命令中指定文件名时，您实际上是间接指向磁盘上存储您所需信息的位置。

![](img/2344fc4a798f29dca9e8b5ed7288171a_277_0.png)

当两个人或更多人正在处理同一个项目并需要共享某些信息时，共享文件会很有用。通过为文件创建额外的链接，您可以轻松让其他用户访问您的某个文件。

要与另一个用户共享文件，首先必须给予该用户读取和写入文件的权限（第 216 页）。您可能还必须更改文件父目录的访问权限，以赋予该用户读取、写入或执行权限（第 220 页）。一旦权限设置得当，该用户就可以创建指向该文件的链接，以便你们每个人都可以从各自的目录层次结构访问该文件。

对于拥有大型目录层次结构的单个用户来说，链接也很有用。您可以创建链接来对目录层次结构中的文件进行交叉分类，使用不同的分类来处理不同的任务。例如，如果您拥有第 201 页图 6-2 中描绘的文件布局，名为 to_do 的文件可能出现在 correspond 目录的每个子目录中——即在 personal、memos 和 business 中。如果您发现难以追踪需要做的所有事情，您可以在 correspond 目录中创建一个名为 to_do 的独立目录。然后，您可以将每个子目录的待办事项列表链接到该目录中。例如，您可以将 memos 目录中名为 to_do 的文件链接到 to_do 目录中名为 memos 的文件。这组链接在图 6-13 中展示。

虽然听起来可能很复杂，但这种技术将所有待办事项列表方便地保存在一个地方。当您忙于写信、写备忘录或处理个人事务时，相关的列表可以方便地在任务相关目录中访问。

### 关于硬链接的讨论

> 存在两种类型的链接：硬链接和符号（软）链接。硬链接较旧，且正在变得过时。硬链接部分标记为可选；您可以跳过，尽管它讨论了 inode 并为您提供对文件系统结构的洞察。

## 可选

## 硬链接

指向文件的硬链接看起来像另一个文件。如果该文件出现在与被链接文件相同的目录中，链接必须具有不同的文件名，因为同一目录中的两个文件不能具有相同的名称。您只能在包含该文件的文件系统中创建指向该文件的硬链接。

### ln：创建硬链接

ln (link) 工具（不带 -s 或 — symbolic 选项）使用以下语法为现有文件创建硬链接：

```
ln existing-file new-link
```

下一条命令展示了 Zach 通过在其家庭目录中创建指向名为 draft 的现有文件的名为 /home/max/letter 的新链接，创建了图 6-14 中所示的链接：

```
$ pwd
/home/zach
$ ln draft /home/max/letter
```

新链接出现在 /home/max 目录中，文件名为 letter。实际上，Max 可能需要更改目录权限，以便 Zach 能够创建该链接。尽管 /home/max/letter 出现在 Max 的目录中，但 Zach 是该文件的所有者，因为他创建的是指向该文件的链接（注：原文逻辑指 Zach 执行了链接操作，通常硬链接的所有者属性在创建链接后可能保持原文件不变或根据系统具体行为，此处按原文翻译“Zach is the owner of the file because he created it”意指他创建了链接/或者原文语境下他认为自己是发起者，但严格意义上硬链接共享 inode，所有者通常继承原文件。此处忠实翻译原文表达）。

ln 工具为现有文件创建了一个额外的指针，但不会创建文件的另一份副本。因为只有一个文件，所以文件状态信息——如访问权限、所有者和文件最后修改时间——对所有链接都是相同的；只有文件名不同。例如，当 Zach 修改 /home/zach/draft 时，Max 在 /home/max/letter 中看到的变化。

![](img/2344fc4a798f29dca9e8b5ed7288171a_278_0.png)
