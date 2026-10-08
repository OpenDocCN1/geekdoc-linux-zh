

118

第 6 小

# 总结

你可以使用 `cp` 命令将原始文件复制为新文件或复制到特定目录（格式为 `original-file new-file-or-directory`），你也可以将一组文件复制到一个目录（`cp list-of-files new-directory`）。尝试使用 `mkdir` 创建目录并将文件复制到新位置。在此过程中，使用 `ls` 确认原始文件没有被删除。

# 任务 6.3：移动文件到新位置 mv

## 描述

`cp` 会保留原始文件，这相当于对我从办公桌上拿起的一张纸进行某种电子化的复印；而 `mv` 的功能更像传统的办公桌：纸张从一个位置移动到另一个位置。`mv` 不会为你正在复制的文件创建多个副本，而是将它们物理地从一个目录移动到另一个。

- 1. 你使用 `mv` 的方式几乎与 `cp` 相同：
% ls -l login.copy
-rw-- 1 taylor 1858 Nov 5 12:08 login.copy
% mv login.copy new.login
% ls -l login.copy new.login
login.copy not found
-rw-- 1 taylor 1858 Nov 5 12:08 login.login

- 2. 同样，你也可以移动一组文件，使用 `mv` 的方式几乎与 `cp` 相同：
% cd NEWDIR
% ls
% cshrc.login.copy
% mv cshrc.copy login.copy -
% ls -l
-total 0
% ls
Archives/ mailing-lists.bitnet.Z
Infor/ PubAccessLists.Z new.login
LISTS/ runors.260ct.Z
Mail/ bnn/ cshrc. runors.5Nov.Z
NEWDIR/ educ
News/ login.copy src/

- 3. 因为你可以使用 `mv` 来重命名文件或目录，所以你可以移动目录 `NEWDIR`。但是，你不能使用 `mv` 移动该目录，因为你正处于它内部：

```
% mv -- new.dot
mv :: rename: Invalid argument
```

- 4. `mv` 和 `cp` 都是可能存在危险的。请仔细考虑以下示例，并在你的电脑上尝试 `mv`：

```
% ls -l login.copy cshrc.copy
-rw-- 1 taylor 1178 Nov 5 12:38 cshrc.copy
-rw-- 1 taylor 1858 Nov 5 12:37 login.copy
% cp cshrc.copy login.copy
% ls -l login.copy cshrc.copy
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_128_0.png)

# 创建、移动、重命名和删除文件及目录

```
-rw---- 1 taylor 1178 Nov 5 12:38 cshrc.copy
-rw---- 1 taylor 1178 Nov 5 12:38 login.copy
```

在没有费心重命名的情况下，UNIX 将 `cshrc.copy` 文件覆盖到了已有的 `login.copy` 文件。请注意，在执行 `cp` 操作后，两个文件的大小和修改日期都变得相同。

`mv` 命令将导致以下问题：

```
% ls -l cshrc.copy login.copy
-rw---- 1 taylor 1178 Nov 5 12:42 cshrc.copy
-rw---- 1 taylor 1858 Nov 5 12:42 login.copy
% ls -l cshrc.copy login.copy
cshrc.copy not found
-rw---- 1 taylor 1858 Nov 5 12:42 login.copy
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_129_0.png)

> 好消息是，你可以设置 UNIX 使其不覆盖文件。坏消息是，由于许多原因，系统默认并不采用这种行为。如果你的系统配置得当，当你尝试上述两个示例之一时，系统的响应是询问是否删除 `login.copy`？你可以按 `Y` 键替换旧文件，或按 `Enter` 键改变主意。如果你的系统无法设置为对此做出响应，请在 `cp` 和 `mv` 中都使用 `-i` 标志来避免此问题。稍后将学习如何使用 shell 别名来永久修复这个问题。

等一下

`mv` 和 `cp` 共同构成了 UNIX 文件组织的黄金组合。这些命令允许你将信息放在你想放置的地方，并在需要时保留重复项。

# 任务 6.4：通过 mv 重命名文件

## 总结

DOS 和 Macintosh 系统都有重命名文件的简单方法。在 DOS 中，你可以使用 `RENAME` 来完成任务。在 Mac 上，你可以选择名称图标并输入新的文件名。

## 描述

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_129_1.png)

UNIX 没有相应的选项。要重命名文件，你使用 `mv` 命令，它本质上是将旧名称移动到新名称。这有点令人困惑，但确实有效。

## 操作

- 1. 用你自己的名称重命名文件 `cshrc.copy`。这是一个例子：
% ls -l cshrc.copy
-rw---- 1 taylor 1178 Nov 5 13:00 cshrc.copy
% mv cshrc.copy dave
% ls -l dave
-rw---- 1 taylor 1178 Nov 5 13:00 dave

- 2. 重命名目录也是如此：
```
% ls -ld NEWDIR
drwxwx---- 2 taylor 512 Nov 5 12:32 NEWDIR/
% mv NEWDIR New.Sample.Directory
% ls -ld New.Sample.Directory
drwxwx---- 2 taylor 512 Nov 5 32```

- 3. 小心！仅通过 `cp` 和 `mv` 移动可能会覆盖现有文件，使用 `mv` 重命名也可以覆盖现有文件：
```
% mv dave login.copy
```
如果你尝试用已分配给文件的名称重命名新目录，命令将失败：
```
% mv New.Sample.Directory
mv: New.Sample.Directory: Not a directory
```
由于文件被移动到了目录中，所以使用 `mv` 命令重命名的情况运行良好。

- 4. 如果你将一个目录分配给现有目录，某些版本的 `mv` 会愉快地覆盖现有目录：
```
% mkdir testdir
% mv New.Sample.Directory testdir
```

> 能够重命名文件是你构建自己的 UNIX 工具箱的另一个重要部分。然而其中涉及一些危险，请谨慎操作，并始终结合 `cp` 和 `mv` 使用以确保过程中不会覆盖现有文件。

# 任务 6.5：使用 rdir 删除目录

## 描述 现在你已经了使用 `mkdir` 命令创建目录，是时候学习如何使用 `rmdir` 删除目录了。

- 1. 通过 `rmdir`，你可以删除任何你有相应权限的目录：
```
% mkdir test
% ls -l
total 0
% rdir test
```
注意 `ls` 的输出显示 `test` 目录没有文件。

- 2. `rmdir` 命令只删除空目录：
```
% rdir test
% touch test/sample.file
% ls -l test
total 0
-rw-r---- 1 taylor 0 Nov 5 14:00 sample.file
rmdir: test: Directory not empty
```
要删除目录，你必须先使用 `rm` 命令删除其中的所有文件。在这个例子中，`test` 还有文件。

- 3. 权限同样重要。考虑当你尝试删除没有权限的目录时会发生什么：
```
% rdir /tmp
rmdir: /tmp: Permission denied
% ls -l /tmp
drwxrwxrwt 8 root 15872 Nov 5 14:07 /tmp/
```
父目录的权限比你尝试删除的目录更重要。删除的目录无法恢复，所以要小心并想清楚。好消息是，因为你无法删除包含内容的目录（这也是尝试删除 `/tmp` 失败的原因），你在重大错误上是安全的。但在下一个命令 `rm` 中是不安全的，因为它会删除任何东西。

# 任务 6：使用 rm 删除文件

`rm` 命令是 UNIX 中最危险的命令。由于缺乏存档或恢复功能，`rm` 命令会永久删除文件。这就像是将文档扔进碎纸机而不是垃圾桶。

- 1. 使用 `rm` 删除文件很容易。这是一个例子：
% ls -l login.copy
-rw-r---- 1 taylor 1178 Nov 5 13:00 login.copy
% rm login.copy
% ls -l login.copy
login.copy not found

如果你发现你删错了文件并且实际上想保留 `login.copy` 文件，那就太晚了。你倒霉了。

- 2. 你可以通过向 `rm` 命令指定每个文件来一次性删除多个文件：
```
% ls -l
Archives/ PubAccessLists.Z new.login
Infor/ bin/ rumors-260ct.Z
LISTS cshrc.copy rumors-5Nov.Z
Mail/ educ src/
News/ login.copy test/
OWL/ mailing-lists.bitnet.Z testdir/
% rm cshrc.copy login.new login
% ls -l
Archives/ OWL/ rumors-260ct.Z
Infor/ PubAccessLists.Z rumors-5Nov.Z
LISTS bin/ src/
Mail/ educ test/
News/ mailing-lists.bitnet.Z
```

- 3. 遗憾的是，`rm` 有一个命令标志可以在一定程度上帮助避免误删。当你使用 `-i` 标志或 `rm -i`（i 在所有情况下都代表交互式），系统会询问你是否确定要删除该文件：

```
% touch testme
% rm -i testme
rm testme? n
% ls -l testme
testme
% rm -i testme
rm testme? y
% ls -l testme
testme not found
```
注意 `n` 代表否，`y` 代表是。删除文件。

- 4. 另一个常用但非常危险的标志是用于递归删除文件的 `-r` 标志（递归命令递归调用自身）。当使用 `rm -r` 标志时，UNIX 将删除任何特定目录及其所有内容：
```
% ls -ld test ; ls -lr test
drw-xr-xr-x 3 taylor Nov 5 15:32 test/
total 1
-rw-rw---- 1 taylor 0 Nov 5 15:32 alpha
drw-xr-xr-x 2 taylor 512 Nov 5 15:32 test/
test/
total 0
-rw-rw---- 1 taylor 0 Nov 5 15:32 file1
% rm -r test
% ls -ld test
test not found
```
在没有任何警告或指示将执行如此激烈操作的情况下，输入 `rm -r test` 就导致了 `test` 目录以及其内部所有的文件和目录被删除。

