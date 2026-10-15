
`% mkdir NEWDIR`

`% ls -ld NEWDIR`

`dr-xr-xr-x 2 author 24 Nov 5 10:54 NEWDIR3/`

5. 如果你尝试创建一个已经使用过的名称的目录会发生什么？

```
% mkdir NEWDIR
mkdir NEWDIR: File exists
```

6. 要在当前位置之外创建目录，请在新目录名前前加上位置：

```
% mkdir /tmp/test
% ls -l /tmp
-rwx------ 1 zhongqi 22724 4 Nov 5 21:33 /tmp/a.out*
-rw------ 1 julia 95594 4 Nov 5 23:10 /tmp/active.10122
-dr-xr-r-- 1 beast 572 Nov 5 05:59 /tmp/anon
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_125_0.png)

| 权限 | 所有者 | 大小 | 日期 | 时间 | 名称 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| -rw---- | root | 0 | Nov 5 | 10:30 | /tmp/bar.report |
| -rw---- | qsc | 0 | Nov 5 | 10:18 | /tmp/lh0138 |
| -rwx--- | steen | 24853 | Nov 5 | 10:40 | /tmp/mbox.steen |
| -rwx--- | techman | 371 | Nov 5 | 10:45 | /tmp/mbox.techman |
| -rw-r--r-- | root | 99738 | Nov 5 | 10:58 | /tmp/quotas |
| -rwx------ | zhongqi | 163579 | 4 | Nov 5 | /tmp/a.out* |
| drwx------x | author | 24 | Nov 5 | 10:53 | NEWDIR2/ |
| dr-xr-xr-x | author | 24 | Nov 5 | 10:54 | NEWDIR3/ |

*(注：此处表格最后两行根据上下文逻辑进行了微调以对齐格式，但内容严格遵循原文 `ls` 命令的输出)*

由于 `rm` 命令具有危险性：你将发现 UNIX 中没有“remove”删除命令，并学习如何规避程序中潜藏的可能危险。

### 使用 `rm` 命令的危险最小化

118

第 6 小

## 总结

你可以使用 `cp` 命令将原始文件复制为新文件或复制到特定目录（格式为 `original-file new-file-or-directory`），你也可以将一组文件复制到一个目录（`cp list-of-files new-directory`）。尝试使用 `mkdir` 创建目录并将文件复制到新位置。在此过程中，使用 `ls` 确认原始文件没有被删除。

# 任务 6.3：移动文件到新位置 mv

## 描述

`cp` 会保留原始文件，这相当于对我从办公桌上拿起的一张纸进行某种电子化的复印；而 `mv` 的功能更像传统的办公桌：纸张从一个位置移动到另一个位置。`mv` 不会为你正在复制的文件创建多个副本，而是将它们物理地从一个目录移动到另一个。

1. 你使用 `mv` 的方式几乎与 `cp` 相同：
```
% ls -l login.copy
-rw-- 1 taylor 1858 Nov 5 12:08 login.copy
% mv login.copy new.login
% ls -l login.copy new.login
login.copy not found
-rw-- 1 taylor 1858 Nov 5 12:08 login.login
```

2. 同样，你也可以移动一组文件，使用 `mv` 的方式几乎与 `cp` 相同：
```
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
```

3. 因为你可以使用 `mv` 来重命名文件或目录，所以你可以移动目录 `NEWDIR`。但是，你不能使用 `mv` 移动该目录，因为你正处于它内部：

```
% mv -- new.dot
mv :: rename: Invalid argument
```

4. `mv` 和 `cp` 都是可能存在危险的。请仔细考虑以下示例，并在你的电脑上尝试 `mv`：

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

## 任务 6.4：通过 mv 重命名文件

## 总结

DOS 和 Macintosh 系统都有重命名文件的简单方法。在 DOS 中，你可以使用 `RENAME` 来完成任务。在 Mac 上，你可以选择名称图标并输入新的文件名。

## 描述

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_129_1.png)

UNIX 没有相应的选项。要重命名文件，你使用 `mv` 命令，它本质上是将旧名称移动到新名称。这有点令人困惑，但确实有效。

## 操作

1. 用你自己的名称重命名文件 `cshrc.copy`。这是一个例子：
```
% ls -l cshrc.copy
-rw---- 1 taylor 1178 Nov 5 13:00 cshrc.copy
% mv cshrc.copy dave
% ls -l dave
-rw---- 1 taylor 1178 Nov 5 13:00 dave
```

2. 重命名目录也是如此：
```
% ls -ld NEWDIR
drwxwx---- 2 taylor 512 Nov 5 12:32 NEWDIR/
% mv NEWDIR New.Sample.Directory
% ls -ld New.Sample.Directory
```
