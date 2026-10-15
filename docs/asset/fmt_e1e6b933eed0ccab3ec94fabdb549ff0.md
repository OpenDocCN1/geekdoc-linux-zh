
除非为文件夹设置了执行权限，否则用户将无法执行以下任何操作：

- 查看文件夹中的文件列表（有注意事项——见后文）；
- 在文件夹中创建、修改或删除文件；
- 通过 `Nautilus` 双击其图标进入文件夹，或使用 `cd` 命令。

如果用户尝试执行上述任何操作，而未设置执行权限，她将看到“Permission Denied”错误消息。

与文件一样，执行权限可以为文件夹所有者、分配给它的组以及其他用户设置。

## 读/写权限

尽管执行权限控制对文件夹的访问，但读取和写入权限可以单独设置。然而，如果未同时设置执行权限，两者均无任何意义。

**读权限：** 通过设置文件夹的读权限，可以控制谁可以查看其中的文件/文件夹列表。如果用户尝试查看文件列表，而读权限未设置，他将看到“Permission denied”错误。

**写权限：** 通过设置写权限，可以控制谁可以在文件夹内创建、删除或重命名文件/文件夹。如果文件夹的写权限未设置，且用户尝试创建、删除或重命名文件/文件夹，他将看到一个错误。

与文件一样，可以为文件夹所有者、分配给它的组以及其他用户分别设置读和写权限。

## 更深入的说明

- 查看文件夹中的文件列表（有注意事项——见后文）；
- 在文件夹中创建、修改或删除文件；
- 通过 `Nautilus` 双击其图标进入文件夹，或使用 `cd` 命令。

如果用户尝试执行上述任何操作，而未设置执行权限，她将看到“Permission Denied”错误消息。

与文件一样，执行权限可以为文件夹所有者、分配给它的组以及其他用户设置。

## 读/写权限

尽管执行权限控制对文件夹的访问，但读取和写入权限可以单独设置。然而，如果未同时设置执行权限，两者均无任何意义。

**读权限：** 通过设置文件夹的读权限，可以控制谁可以查看其中的文件/文件夹列表。如果用户尝试查看文件列表，而读权限未设置，他将看到“Permission denied”错误。

**写权限：** 通过设置写权限，可以控制谁可以在文件夹内创建、删除或重命名文件/文件夹。如果文件夹的写权限未设置，且用户尝试创建、删除或重命名文件/文件夹，他将看到一个错误。

与文件一样，可以为文件夹所有者、分配给它的组以及其他用户分别设置读和写权限。

## 文件夹权限的更深入说明

说用户在未设置执行权限的情况下无法查看文件夹的列表并不完全正确。如果文件夹的读权限已设置，但执行权限未设置，用户仍可使用 `ls` 命令查看简短的文件列表，但长列表命令选项（即 `ls -l myfolder`）将无法工作。其原因与 Linux 在技术层面的工作方式有关。

> 注意 在 `Nautilus` 文件浏览窗口中，如果读权限已设置，但执行权限未设置，用户将能够访问该文件夹，但它看起来会是空的。

如果以上内容让你头疼，不用担心。对于大多数用户而言，文件夹权限可归结为以下日常规则：

只读：要将用户限制为仅查看文件夹中的文件列表，请确保已设置读和执行权限，但未设置写权限；

写权限：要允许用户在文件夹中创建或删除文件，请确保已设置读、写和执行权限（注意：文件夹可以设置为“仅写”，如果读权限未同时设置——用户可以在其中保存文件，但无法查看文件列表）；

拒绝访问：要完全拒绝用户访问文件夹，请取消所有权限——读、写和执行。

任何其他文件夹权限组合都可能导致混淆。

## 权限的显示方式

在命令行文件列表中，权限由 `r` 表示读，`w` 表示写，`x` 表示执行。对于所有文件和文件夹，权限都按一行列出：首先是所有者，然后是组，最后是其他用户。参见图 5-1 的注释示例。

权限、所有权和组分配可以通过使用 `ls` 命令的 `-l` 命令选项来查看。尝试列出你 `/home` 文件夹中文件和文件夹的权限：

- `ls -l ~`

这是我在测试系统上看到的内容：

```
total 28
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Desktop
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Documents
drwxrwxrwx 1 keir keir 26 2008-10-24 09:51 Examples -> /usr/share/example-content
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Music
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Pictures
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Public
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Templates
drwxr-xr-x 2 keir keir 4096 2008-10-24 10:07 Videos
```

让我们更仔细地看看列表中的第一个——Desktop 文件夹。权限、所有权和组分配列在行的开头，读法如下：

```
drwxr-xr-x 2 keir keir
```

开头的 `d` 仅表示这是一个目录——文件夹的另一个名称。如果那里出现连字符，则我们处理的是

![](img/48d064407ff591f0b5365c2d2919ee6e_99_0.png)

Figure 5-1. File/folder permissions.

with a file. There are a handful of other letters that can appear here, but the main one you’ll encounter is `l`, which indicates a link.

Following this are the three sets of permissions, listed one after the other: `rwxr-xr-x`. After that is a link number, which isn’t relevant to this discussion and can be ignored. Then the owner’s username is listed (in this case, `keir`), and then the group the file is assigned to (the group is also called `keir`).

> NOTE Under Ubuntu each user is assigned to their own personal group, that is named after their username. This policy effectively means that group permissions are irrelevant for personal files unless you were specifically to add another user to your personal group. However, it’s still important you understand the concept of groups and how it applies to file/folder permissions.

Here are the permissions separated out into sets of three relating to owner, group and others:

- Owner: `rwx`
- Group: `r-x`
- Others: `r-x`

The owner has read (`r`), write (`w`), and execute (`x`) permissions. In other words, he can do anything—he has full permissions. He can view a file listing of the Desktop folder, and write new files there. He can switch to the folder by typing `cd Desktop`, or by browsing to it with `Nautilus`.

Members of the group `keir` have read and execute permissions, so they can view a file listing of the folder, and also switch into it. However, they can’t write any files there, or delete them, because there’s a hyphen where the `w` would normally appear. Quite simply, a hyphen in place of a permission means “no permission”.
