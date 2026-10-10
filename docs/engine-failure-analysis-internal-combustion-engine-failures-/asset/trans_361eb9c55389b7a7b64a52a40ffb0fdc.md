

## 文件类型

在详细目录列表（例如由 `ls -l` 生成的列表）中，你会看到以下文件类型符号，如“文件类型符号”表所示。

### 文件类型符号

| 符号 | 说明 |
| :--- | :--- |
| - | 普通文件 |
| * | 可执行文件（程序或脚本） |
| / | 目录 |
| = | 套接字 |
| p | FIFO（命名管道） |
| @ | 符号链接 |

## 日期和时间表达式

某些命令要求你指定日期或时间。你可以使用以下约定来描述日历日期、星期几和时间，如“日历日期”表所示。

### 日历日期

| 使用以下任一字符串 | 指定该日期 |
| :--- | :--- |
| 2002-09-21 | 2002年9月21日 |
| 9/21/02 | |
| 21 September 2002 | |
| 21 Sept 02 | |
| 21 Sep 02 | |
| Sep 21, 2002 | |
| 21-sep-02 | |
| 21sep02 | |

### 星期

| 使用以下任一字符串 | 指示 |
| :--- | :--- |
| monday, mon | 星期一 |
| tuesday, tue | 星期二 |
| wednesday, wed | 星期三 |
| thursday, thu | 星期四 |
| friday, fri | 星期五 |
| saturday, sat | 星期六 |

### 时间

| 使用以下任一字符串 | 指定该时间 |
| :--- | :--- |
| 20:02:00 | 下午 8:02 |
| 20:02 | 下午 8:02 |
| 8:02pm | 下午 8:02 |
| 20:02-0500 | 下午 8:02 美东标准时间 |

## 按字母排序的命令参考

本节详细说明了用于以下目的的命令：

-   查看和修改所有权、权限及其他文件属性（**chgrp, chmod, chown, mc, lsattr, stat, touch, umask, wc**）
-   复制、移动、重命名和删除文件（**cp, dd, mc, mv, rm, sfdeldelete, undelete**）
-   创建和维护硬链接及符号链接（**ln, mc, symlinks**）
-   创建和删除目录（**mc, mkdir, rmdir**）
-   创建特殊文件（**mkfifo, mknod**）

## chgrp

```text
chgrp [ option ] group file
```

更改指定文件的所有权至指定组。要指定组所有者，你可以提供组名称或ID号。此命令需要超级用户状态（参见第1章中的 su）。

另见 chown。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -c, --changes | 仅在发生更改时显示消息 |
| -f, --silent, --quiet | 隐藏消息 |
| -h, --no-dereference | 更改符号链接本身，而不是符号链接指向的文件 |
| --help | 显示可用选项 |
| -R, --recursive | 更改当前目录及其所有关联子目录中的所有权 |
| --reference=filename | 使用指定参考文件名的组 |
| -v, --verbose | 显示有关所有已处理文件的消息 |
| --version | 显示版本号 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| chgrp games puzzle | 将指定组 (games) 设置为 puzzle 的所有者。 |
| chgrp -R authors *.doc | 将指定组 (authors) 设置为当前目录及其所有关联目录中所有具有 .doc 扩展名的文件的组所有者。 |

## chmod

```text
chmod [ option ] mode filename
```

将 filename 的权限设置更改为 mode。要指定 mode，你可以使用符号模式或数字模式。有关模式规范的更多信息，请参见“设置权限”部分。若要更改其他用户文件的权限，需要超级用户状态（参见第1章中的 su）。要查看文件的当前权限，请使用 stat。要更改所有权，请使用 chown。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -c, --changes | 仅在发生更改时显示消息 |
| -f, --silent, --quiet | 隐藏消息 |
| -v, --verbose | 显示有关所有已处理文件的消息 |
| -R, --recursive | 更改当前目录及其所有关联子目录中的权限 |
| --reference=filename | 使用指定参考文件名的模式 |
| --help | 显示可用选项 |
| --version | 显示版本号 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| chmod 755 welcome.html | 将指定文件 (welcome.html) 的权限设置为数字权限模式 0755。 |
| chmod u+x ballistic | 增加指定文件 (ballistic) 的权限，以便用户可以执行该文件。 |
| chmod o-w my-doctoral-thesis.doc | 减少指定文件 (my-doctoral-thesis.doc) 的权限，以便其他人无法写入该文件。 |
| chmod u=rw,go=r info.txt | 设置指定文件 (info.txt) 的权限，使文件所有者 (user) 可以读写，但组所有者和其他人仅限于读取该文件。 |
| chmod a=rw *.doc | 设置所有符合指定 shell 模式的文件（参见第4章）的权限，使所有用户都可以读写该文件。 |
| chmod -R u+rw * | 增加指定目录中所有文件的权限，必要时还包括其所有关联子目录中的文件，使用户同时具有读取和写入权限。 |
| chmod u+s ballistic | 为指定可执行文件 (ballistic) 添加设置用户ID特殊权限。 |
| chmod u-s ballistic | 从指定可执行文件 (ballistic) 中移除设置用户ID特殊权限。 |
| chmod o+t ballistic | 在交换设备上保存程序的副本，以便其加载速度更快。 |

## chown

```text
chown [ option | user [.group] ] file
```

将指定文件的所有权更改为指定用户。要更改组所有权，请在用户名后输入一个点号，然后输入组名称或ID，中间不要有空格。要指定所有者或组，你可以提供用户或组名称或ID号。此命令需要超级用户状态（参见第1章中的 su）。

另见 chgrp。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -c, --changes | 仅在发生更改时显示消息 |
| --dereference | 更改目标的所有权，而不是符号链接的所有权 |
| -f, --silent, --quiet | 隐藏消息 |
| -h, --no-dereference | 更改符号链接本身，而不是符号链接指向的文件 |
| --help | 显示可用选项 |
| -R, --recursive | 更改当前目录及其所有关联子目录中的所有权 |
| --reference=filename | 使用指定文件名的所有者和组 |
| -v, --verbose | 显示有关所有已处理文件的消息 |
| --version | 显示版本号 |

### 示例

| 此命令 | 执行以下操作 |
| :--- | :--- |
| chown suzanne autobiography.doc | 将指定用户 (suzanne) 设置为 autobiography.doc 的所有者。 |
| chown suzanne.authors essay1.doc | 将指定用户 (suzanne) 和指定组 (authors) 设置为 essay1.doc 的所有者。 |
| chown -R mike.games * | 将指定用户 (mike) 和指定组 (games) 设置为当前目录及其所有关联子目录中所有文件的所有者。 |

## cp

```text
cp [ option ] [ source ] [ destination ]
```

将一个源文件 (source) 复制到目标文件 (destination)，或将多个源文件复制到必须是一个现有目录的目标。当你复制多个文件时，可以使用 shell 模式来指定源（参见第4章中的“Shell 模式”部分）。另见 dd。

### 选项

| 使用此选项 | 执行此操作 |
| :--- | :--- |
| -a, --archive | 创建由 *source* 指定的文件的归档副本（等同于 `-dpR`）。 |
| -b, --backup | 为将被复制操作删除的现有目标文件制作备份副本。 |
| -d, --no-dereference | 将符号链接作为符号链接复制，而不是复制它们指向的文件。 |
| -f, --force | 删除现有目标文件，而不提示确认。 |
| --help | 显示可用选项。 |
| -i, --interactive | 在覆盖现有目标文件之前提示。 |
| -l, --link | 创建硬链接而不是目标文件。 |
| -p, --preserve | 如果可能，保留文件属性。 |
| -P path name, --parents=path name | 为每个目标文件将指定目录信息添加到目标目录，并在必要时创建所需的子目录。 |
| -r directory | 从当前目录及其所有关联子目录递归复制指定目录。此选项试图复制 FIFO 和特殊文件，以及常规文件。如有必要，此选项会在目标目录中创建子目录。 |

