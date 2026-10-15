
| - | 普通文件 |

## 表5.1 ls 文件类型指示符

权限字符串中的接下来九个字母被分成三组，每组三个，分别表示所有者、组和其他所有人，如图5.1所示。

![](img/036fe100817eada43c999b050270081b_91_0.png)

**图5.1** 解释文件权限。

要理解权限对计算机系统究竟意味着什么，请记住 Unix 将一切都视为文件。如果你安装一个应用程序，它和其他所有东西一样，只有一个例外：系统知道应用程序是可执行的。一封写给你的

Mum 是一个普通文件，但如果你告诉 Unix 它是可执行的，系统会愉快地尝试将其作为程序运行（然后失败）。

文件存在三种主要类型的权限：读、写和执行。读权限使用户能够使用各种程序查看文件的内容，但他们不能更改、修改或删除任何信息。他们可以将文件复制到自己有写权限的目录中，然后编辑新版本。

写权限是下一步。具有文件写访问权限的用户可以向文件添加信息。如果你对文件同时具有写权限和读权限，你就可以编辑文件：读权限使你能够查看内容，写权限使你能够更改内容。仅有写权限时，你可以向文件添加信息，但你无法在任何时候查看文件的内容。坦白说，Unix 中仅写权限是不常见的，但你可能会在日志文件上看到它，日志文件是跟踪系统活动的 files。

到目前为止，你已经了解到你可以拥有只读权限、读写权限和仅写权限的文件。第三种访问权限是执行，由 `ls` 在权限字符串的第三个位置用 `x` 表示。你可以设置任何文件为可执行；shell 脚本、Perl、Ruby 和其他解释型语言都是被执行的文本文件。例如，这里是我自己的 `bin` 目录中的一些程序——以及 shell 脚本——它们是可执行的：

Click here to view code image

```
% ls -l bin
 total 57
-rwx-- 1 taylor 1507 Aug 17 13:27 bounce.msg
-rwxrwx- 1 taylor 32916 Oct 10 19:09 calc
-rwx-- 1 taylor 18567 Sep 14 22:14 fixit
-rw--- 1 taylor 334 Oct 1 09:53 punt
-rwx-- 1 taylor 3424 Sep 10 22:27 rumor.mill.sh
```

1. 尝试列出你系统上 `/etc` 目录中的文件，看看你能否识别哪些是可执行文件或程序，哪些是目录，哪些是符号链接（以权限字符串的第一个字符为 `l` 表示；它们是指向其他文件的文件，或指向其他目录的目录），哪些是普通文件。

2. 执行权限与读或写权限略有不同。任何具有执行权限的文件都可以像程序一样对待。你在命令行输入文件名，如果该目录在你的 `PATH` 中，该文件将被执行：

Click here to view code image

```
% pwd
/home/taylor
% echo $PATH
/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local:/usr/local/bin:
% ls -l bin/say.hi
-rwxrwx- 1 taylor 9 Oct 11 13:32 bin/say.hi
% say.hi
hi
```

你现在可以看到搜索路径的重要性。没有搜索路径，系统将无法找到任何命令，你将只剩下几乎无法使用的系统。你也可以看到检查可执行权限状态的目的。我要稍微跳 ahead 一点来向你展示 `chmod`（change mode/permission）程序的一种用途，这样你就可以看到如果我使用 `-x` 标志从 `say.hi` 程序中移除执行权限会发生什么：

Click here to view code image

```
% chmod -x bin/say.hi
% ls -l bin/say.hi
-rw-rw-- 1 taylor 9 Oct 11 13:32 bin/say.hi
% say.hi
/home/taylor/bin/say.hi: Permission denied.
```

这次 Unix 在我的搜索路径中搜索，找到了与我请求的程序名称匹配的文件，然后确定它不可执行。由此产生的错误消息是 `Permission denied`。

3. 现在尝试在你的计算机系统上输入 `say.hi`。你会得到不同的错误消息，`Command not found`，这告诉你 Unix 检查了搜索路径中的所有目录，但在哪里都找不到匹配项。

4. 检查你的 `PATH` 并找到一个你可以添加文件的目录。你可能在你的 `HOME` 目录中有 `bin` 目录（例如，我在搜索路径中有 `/home/taylor/bin`）。如果没有，使用 `mkdir bin` 创建一个。这是一个使用 `touch` 命令添加文件的好地方：

Click here to view code image

```
% echo $PATH
/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local:/usr/local/bin:
% touch bin/my.new.cmd
% ls -l bin
-rw-rw-- 1 taylor 0 Oct 11 15:07 my.new.cmd
```

5. 现在尝试通过直接输入其名称来实际执行该命令：

Click here to view code image

```
% my.new.cmd
/home/taylor/bin/my.new.cmd: Permission denied.
```

### Note

如果你使用的是 C shell（而不是 bash）作为你的命令解释器，就像在 FreeBSD 上可能的情况，它可能找不到你刚刚创建的新命令。这是因为，为了加快速度，它会保留一个内部表，记录不同命令在你的搜索路径中的位置。你需要强制程序重建其表，你可以用简单的命令 `rehash` 来做到这一点。如果你输入文件名时没有得到 `permission denied` 错误，而是看到 `Command not found`，请输入 `rehash` 再试一次。

6. 最后，使用 `chmod` 为文件添加执行权限，再次尝试执行它：

Click here to view code image

```
% chmod +x bin/my.new.cmd
```

```
% ls -l bin/my.new.cmd
-rwxr-x-- 1 taylor      0 Oct 11 15:07 bin/my.new.cmd
% my.new.cmd
%
```

Voilà! 你已经创建了你的第一个 Unix 命令，这是一项成就，即使它什么也没做。你现在可以看到搜索路径以及 Unix 哲学中应用程序与普通文件相同，只是权限不同，这种特性在你学习如何自定义环境时是无价的。

执行权限使用户能够像运行程序一样运行文件。执行权限独立于其他被授予或被拒绝的权限，因此完全可以拥有一个具有读和执行权限但没有写权限的程序。毕竟，你不希望其他人修改程序本身。你也可以拥有仅具有执行权限的程序。这意味着用户可以运行应用程序，但他们无法检查其工作原理或复制它。复制当然需要能够读取文件内容。

### Note

尽管实际具有仅执行权限的程序工作正常，但一类特殊的程序称为 shell 脚本会失败。Shell 脚本充当 Unix 命令行宏设施，使你能够轻松地将一系列命令保存在文件中，然后作为单个程序运行。然而，要工作，shell 必须能够读取文件并执行它，因此 shell 脚本始终需要同时具有读和执行权限。

在三种不同的权限：读、写和执行上，显然有相当多的排列组合。实际上，其中少数几种最常见，如表 5.2 所列。

| Permission | Meaning |
|---|---|
| --- | No access is allowed |
| r-- | Read-only access |
| r-x | Read and execute access, for programs and shell scripts |
| rw- | Read and write access, for files |
| rwx | All access allowed, for programs |

## TABLE 5.2 The Most Common File Permissions

这些权限应用于目录时含义不同，但 `---` 始终表示没有人可以访问相关文件。

对以下几个示例的解释应该会有所帮助：

Click here to view code image

```
-rw--- 1 taylor    3843 Oct 10 16:22 iecc.list
-rw-rw-r 1 taylor  280232 Oct 10 16:22 mailing.lists
-rw-rw- 1 taylor   1031 Oct  7 15:44 newlists
-rwxr-x- 1 taylor    64 Oct  9 09:31 the.script
```
