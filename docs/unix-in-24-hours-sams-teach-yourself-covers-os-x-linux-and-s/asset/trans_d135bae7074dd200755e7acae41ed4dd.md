

## Note

好消息是，你可以设置 Unix 使其不会覆盖文件。坏消息是，出于某种原因，许多系统默认并不启用此行为。如果你的系统配置合理，当你尝试前面两种危险示例中的任一种时，系统的响应是 remove login.copy?. 你可以按 Y 键替换旧文件，或按 Enter 键改变主意。如果你的系统无法以这种方式响应，你可以对 cp 和 mv 都使用 -i 标志来避免此问题。稍后，你将学习如何通过 shell 别名永久修复此问题。

mv 和 cp 合在一起是 Unix 文件组织的动态二人组。这些命令使你能够将所需的信息放在所需的位置，如果需要的话，还会留下副本。

## Task 6.4: Renaming Files with mv

Windows 和 Macintosh 系统都有简单的方法重命名文件。在 Mac 上，你可以选中文件图标下的名称并输入新文件名。在 Windows 上，你右键单击图标并从弹出菜单中选择重命名。

Unix 没有这些选项。要重命名文件，你使用 mv 命令，其本质是将旧名称移动到新名称。有点违反直觉，但它有效。

- 1. 将文件 profile.copy 重命名为你自己的名字。以下是示例：

Click here to view code image

```
% ls -l profile.copy
-rw--- 1 taylor 1178 Nov 5 13:00 profile.copy
% mv profile.copy dave
% ls -l dave
-rw--- 1 taylor 1178 Nov 5 13:00 dave
```

- 2. 也可以重命名目录：

Click here to view code image

```
% mv New.Sample.Directory dave
mv: New.Sample.Directory: rename: Not a directory
```

反向操作则能正常工作，因为文件按预期被移动到目录中。这就是使用 mv 命令重命名文件的微妙之处。

- 4. 如果你为新目录指定一个属于现有目录的名称，某些版本的 mv 会很乐意覆盖现有目录并按要求命名新目录：

Click here to view code image

```
% mkdir testdir
% mv New.Sample.Directory testdir
```

能够重命名文件是为你构建一个有用的 Unix 虚拟文件柜的另一个重要部分。然而其中涉及一些重大危险，因此请谨慎行事，并且始终将 ls 与 cp 和 mv 结合使用，以确保在操作过程中不会覆盖或替换现有文件。

## Task 6.5: Removing Directories with rmdir

现在你可以用 mkdir 命令创建目录，是时候学习如何使用 rmdir 命令删除目录了。

- 1. 使用 rmdir，你可以删除任何你拥有适当权限的目录：

```
% mkdir test
% ls -l test
total 0
% rmdir test
```

请注意，ls 的输出显示 test 目录中没有任何文件。

- 2. 默认情况下，rmdir 命令只删除空目录：

Click here to view code image

```
% mkdir test
% touch test/sample.file
% ls -l test
total 0
-rw-rw-- 1 taylor 0 Nov 5 14:00 sample.file
% rmdir test
rmdir: test: Directory not empty
```

要删除目录，你必须先使用 rm 命令删除其中的所有文件。在此示例中，test 仍包含文件。请注意，某些版本的 rmdir 提供 -p 标志，它将递归地从右到左删除所有目录和子目录，直到遇到非空目录为止。其他版本包含 -f 标志，它将允许你强制删除指定目录中包含的任何文件或子目录。正如你所想象的，rmdir -f / 可能毁掉你的系统，所以要小心！

- 3. 权限也很重要。考虑当我尝试删除我没有权限触碰的目录时会发生什么：

Click here to view code image

```
% rmdir /tmp
rmdir: /tmp: Permission denied
% ls -l /tmp
drwxrwxrwt 81 root 15872 Nov  5 14:07 /tmp
```

父目录的权限，而不是你试图删除的目录，才是重要的考虑因素。

一旦删除目录，就无法恢复，因此请小心并仔细思考你的操作。好消息是，由于使用 rmdir 你无法删除包含任何内容的目录（前面示例中尝试删除 /tmp 失败的第二个原因），因此你相对安全，不会犯下重大错误。然而，你在使用下一个命令 rm 时并不安全，因为它会删除任何东西。

## Task 6.6: Removing Files Using rm

rm 命令可能是 Unix 中最危险的命令。缺乏任何归档或恢复功能，rm 命令会永久删除文件。这就像把文件扔进碎纸机而不是扔进垃圾桶。

## Caution

在某些 Unix 系统中，包括 Solaris，有一个名为 shred 的命令，它删除文件并覆盖磁盘上文件信息先前存储的位置。它比 rm 更无情，如果使用的话应极其谨慎。

- 1. 使用 rm 删除文件很容易。以下是示例：

Click here to view code image

```
% ls -l login.copy
-rw--- 1 taylor 1178 Nov  5 13:00 login.copy
% rm login.copy
% ls -l login.copy
login.copy not found
```

如果你决定删除了错误的文件并且实际上想保留 login.copy 文件，为时已晚。你只能自认倒霉。

## Note

如果你在命令行上工作，Unix 中没有“回收站”或“废纸篓”可以从中恢复意外删除的文件。请小心！

- 2. 你可以通过向 rm 命令指定每个文件，一次删除多个文件：

Click here to view code image

```
% ls -F
Archives/      PubAccessLists.Z  new.login
InfoWorld/     bin/              rumors.26Oct.Z
```
