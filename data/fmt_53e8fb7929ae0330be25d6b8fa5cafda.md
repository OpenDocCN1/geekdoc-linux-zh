
# 挂载与文件系统管理

挂载是将附加文件系统附加到计算机当前可访问文件系统的过程。文件系统是一个目录层次结构，也称为目录树，用于组织计算机或存储媒体上的文件。在 Linux 中，目录从根目录开始，它包含了系统中所有其他目录和文件。根目录由正斜杠（`/`）标识。

现在，当你需要访问 Linux 中的文件系统时，你首先需要挂载它。挂载文件系统意味着使其在 Linux 目录树的某个点变得可访问。这个点就是挂载点。注意，当你挂载文件系统时，它可以位于硬盘分区、光驱、软盘或 USB 存储设备上。你只需要知道与特定存储设备相关的设备名称，以及你想要挂载它的目录即可。

## 配置 `/etc/fstab` 文件

当新安装 Linux 系统时，在安装期间创建的所有磁盘分区都配置为在每次系统启动时自动挂载。然而，如果在安装后向系统附加额外的驱动器，会发生什么呢？简单的答案是什么都不会发生，因为系统没有配置自动挂载这些驱动器。为此，你需要配置 `/etc/fstab` 文件。该文件用于控制系统启动时挂载的文件系统。`/etc/fstab` 文件包含以下格式的细节：

| device | /mount-point | ftype | options | dumpfreq | passno |
| :--- | :--- | :--- | :--- | :--- | :--- |

上述格式包含以下字段：

- `device`：指设备或文件名
- `/mount-point`：指在挂载文件系统时使用的现有目录（如 `/boot`）
- `ftype`：指指定设备上指定的文件系统类型
- `options`：指用逗号分隔的选项列表，用于控制挂载行为
- `dumpfreq`：指一个数字（0 或 1），指定是否应该对文件系统进行备份
- `passno`：指检查文件系统的顺序

## 挂载文件系统

`mount` 命令用于将位于设备上的文件系统附加到目录树上。`mount` 命令的标准格式如下：

```
mount -t type dir
```

如果你只提供目录或设备，如下所示：

```
mount /dir
```

那么，`mount` 命令会在 `/etc/fstab` 文件中查找相应的挂载点项，并尝试挂载该文件。

让我们考虑以下命令，我们正将一个设备挂载到特定的文件夹：

```
$ mount -t mdsos /dev/fd0 /mnt/floppy
```

在上一个命令中，假设 Linux 拥有 `/mnt/floppy` 文件夹。我们挂载了一个 mdsos 文件系统，由 `-t`（类型）选项指定，并将设备映射到 `/mnt/floppy` 点。同样，你可以如下挂载光驱：

```
$ mount -t iso9660 /dev/cdrom /mnt/cdrom
```

## 卸载文件系统

`umount` 命令用于从文件层次结构中分离一个或多个文件系统。只需通过提供挂载目录来指定文件系统。考虑以下示例：

```
$ umount /mnt/floppy
$ umount /mnt/cdrom
```

此外，你可以使用 `man` 命令获取有关 `mount` 和 `umount` 命令的更多信息。

# 3.5 备份

备份是复制数据以便在丢失时恢复。在 Linux 中有几种类型的备份：

- **全备**：备份系统上的所有数据。
- **增量备份**：仅备份上次备份以来更改的数据。
- **差异备份**：备份自上次全备以来更改的数据。

Linux 中常用的备份工具有：

- `tar`
- `cpio`
- `dump` 和 `restore`

让我们逐一讨论这些工具。

## Tar 工具

Tar 代表“Tape Archive”（磁带存档），是一个 UNIX 命令，用于从多个文件创建一个“存档”的单个文件。需要注意的是，tar 归档包中的文件通常没有经过压缩；它们只是被合并在一个文件中。

以下是执行文件备份的命令语法：

```
tar -cvf <destination> <source>
```

例如：

```
tar -cvf /backup/home.back /home
```

在上一个示例中，`c` 选项创建备份文件，`v` 选项提供运行的详细信息，`f` 选项指定备份文件的名称和位置。

## CPIO 工具

`cpio` 命令是一个传统的 Linux 工具，可用于文件系统的备份。使用 `cpio` 命令的语法如下：

```
cpio flags [options]
```

创建 cpio 文件的语法如下：

```
find (source file name) | cpio (options) > (target file name)
```

例如：

```
find file1 | cpio -o file1_back.cpio
```

以下语法用于提取 cpio 文件：

```
cat <source file name> | cpio (options)
```

例如：

```
cat file1_back.cpio | cpio -idvm
```

## Dump 和 Restore

`dump` 和 `restore` 命令是 dump 包中的两个不同的程序。以下是 `dump` 命令的语法，用于在另一个目录中对目录进行备份：

```
dump <dump levels> <options> <destination name> <source name>
```

例如：

```
dump -0 -f /home_dumps/mydumps /home
```

图 1 显示了上一个命令的输出：

![](img/889a483c5a60e0806e42b73b2662a855_88_0.png)

> 图 1：使用 dump 命令

`restore` 命令用于恢复和查看 dump 文件。以下是 `restore` 命令的语法：

```
restore <options> <file name>
```

例如：

```
restore -if mydumps
```

## 压缩工具

压缩工具也用于执行备份。Linux 中有多种压缩工具。其中一些主要的工具如下：

- **gzip**：指 GNU zip 压缩程序，它使用 GNU zip 压缩 tar 归档。通常情况下，它会创建一个以 `.gz` 扩展名的文件。`gzip` 命令的语法如下：

```
gzip user_tar_file.tar
```

- **bzip2**：指 Julian Seward 在 1997 年以 BSD 许可证发布的工具。该工具提供了比 gzip 更好的压缩率，但它需要更多的处理器时间。它会创建一个以 `.bz2` 扩展名的文件。使用 `bzip2` 工具的语法如下：

```
bzip2 user_tar_file.tar
```

使用以下语法可以解压由 `bzip2` 压缩的文件，并提取当前目录中提取内容：

```
bunzip2 user_file.bz2
```

- **tar**：指一个通常创建归档文件的工具，但你可以使用 gzip 或 bzip2 来压缩该归档文件。为此，你使用 `z` 或 `j` 选项，如下所示：

```
tar -zcvf pics.tar.gz *.png *.opt
tar -jcvf data.bz2 *.doc
```

在上述命令中，`-z` 选项用于 gzip 压缩，`-j` 选项用于 bzip2 压缩。

- **zipinfo**：指一个用于查找 zip 归档文件详细信息（例如 winzip）的工具。使用 `zipinfo` 命令的语法如下：

```
zipinfo zip_file.zip
```

- **zipgrep**：指一个运行 `grep` 命令在 zip 文件中查找文件（例如 winzip）的工具，而无需先手动解压文件。使用 `zipgrep` 命令的语法如下：

```
zipgrep pattern zip_file.zip
```

- **bzip2recover**：指一个用于从损坏的 bzip2 归档中恢复文件的工具。它简单地提取所有工作数据块并对它们进行完整性测试。

- **bzme**：指一个使用 bzip2 将 zip 文件或 gzipped 文件转换为压缩文件的工具。使用 `bzme` 命令的语法如下：

```
bzme filename
```

# 3.6 处理用户账户

在 Linux 中创建新用户账户非常简单。为此，你只需要在命令行中运行 `useradd` 命令。例如，要创建一个名为 Mahendra 的用户，你可以按照如下方式运行 `useradd` 命令：

```
# useradd Mahendra
```

这会在 `/etc/passwd` 文件中添加新条目。默认情况下，该文件存储了与用户账户相关的所有信息。

用户 Mahendra 没有默认密码。为了给它创建一个密码，你只需要在命令行中输入 `passwd` 命令，如下所示：

```
# passwd Mahendra
```

这将提示你输入密码。输入密码并按回车。系统会要求你确认密码。再次输入密码并按回车。你需要正确输入两次相同的密码才能成功创建账户。

## 修改现有用户信息

对现有用户信息进行修改意味着更改用户的密码、用户主目录、用户账户过期日期、用户标识 (UID) 和组标识 (GID)。让我们在接下来的章节中学习如何在 Linux 中执行所有这些任务。

### 更改用户主目录

更改用户主目录的语法如下：

```
# usermod -d <homedir> <username>
```

例如，如果你想将 Mahendra 的主目录从 `/home/Mahendra` 更改到 `/home/mahen`，请运行以下命令：

```
# usermod -d /home/mahen Mahendra
```

要更改 Mahendra 的主目录并将其目录 (`/home/Mahendra`) 中包含的信息也移动到新位置 (`/home/mahen`)，请运行以下命令：

```
# usermod -d -m /home/mahen Mahendra
```

此命令将 Mahendra 当前目录 (`/home/Mahendra`) 中的所有文件移动到新的主目录 (`/home/mahen`)。

### 更改 UIDs 和 GIDs

在 Linux 中，每个用户都有一个 UID 和一个 GID。用户的 UID 是用于在 Linux 系统中标识用户的整数值，而 GID（一个整数值）代表用户所属的特定组。如果你想更改用户的 UID，请使用以下语法：

```
# usermod -u <UID> <username>
```

例如，以下命令将 Mahendra 的 UID 更改为 555：

```
# usermod -u 555 Mahendra
```

要更改用户的 GID，请使用以下语法：

```
# usermod -g <GID> <username>
```

例如，以下命令将 Mahendra 的 GID 更改为 555：

```
# usermod -g 555 mahendra
```

### 描述 `/etc/passwd` 文件

`/etc/passwd` 文件存储了登录计算机时所需的用户账户信息。这些信息包括用户 ID、组 ID、用户主目录等。该文件还包含所有用户的列表。

示例的格式如下：

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/sbin:/sbin/nologin
bin:x:2:2:bin:/bin:/sbin/nologin
sys:x:3:3:sys:/root:/sbin/nologin
sync:x:4:4:sync:/dev:/bin/sync
games:x:5:5:games:/usr/games:/sbin/nologin
man:x:6:6:man:/var/cache/man:/sbin/nologin
lp:x:7:7:lp:/root:/sbin/nologin
mail:x:8:8:mail:/var/spool/mail:/sbin/nologin
uu:x:9:9:uu:/root/u:/sbin/nologin
proxy:x:13:13:proxy:/root:/sbin/nologin
backup:x:34:34:backup:/var/backups:/sbin/nologin
data:x:35:36:data:/dd:/sbin/nologin
list:x:38:38:list:/var/spool/list:/sbin/nologin
sync:x:42:42:sync:/lp:/sbin/nologin
irc:x:39:39:irc:/var/run/ircd:/sbin/nologin
gnp:x:41:41:gnp:/var/lib/gnp:/sbin/nologin
irc:x:48:48:irc:/var/run:/sbin/nologin
www-data:x:33:33:www-data:/var/www:/sbin/nologin
backup:x:34:34:backup:/var/backups:/sbin/nologin
nats:x:634:634:nats:/var/lib:/sbin/nologin
list-apt:x:100:100:list-apt:/var/lib/apt/:/sbin/nologin
nobody:x:999:999:nobody:/nonexistent:/sbin/nologin
user:x:1000:1000:user:/home/user:/bin/bash
```

前述命令会打印用户 deven 的终端名称、主目录、邮件状态和电话号码。

`chfn` 命令用于更改用户的 finger 信息（用户详细信息）。例如，要更改用户 deven 的 finger 信息，请输入以下命令：

```bash
# chfn deven
```

如果你没有指定想要更改的信息（无论是全名、电话号码还是目录），系统将针对用户的每个字段信息向你提问。在提示符处，你可以输入新信息，也可以直接按 `ENTER` 键以保持该字段不变，或者输入 'none' 使该字段留空。

### 删除用户

`userdel` 命令用于删除用户账户。例如，要删除用户 Mahendra，请输入以下命令：

```
# userdel Mahendra
```

如果你想同时删除该用户的家目录，可以在使用 `userdel` 时输入 `-r` 选项。

# 3.7 组与权限

Linux 允许你创建一个用户组，并赋予他们所需的权限。让我们来看一个例子，假设你有一个来自组织 IT 部门的用户组。他们经常在系统上使用电子表格应用程序。你可以创建一个名为 `finance` 的新组，并将其设置为电子表格的默认组。要创建一个组，运行以下 `groupadd` 命令：

```bash
# groupadd finance
```

现在，如果你需要创建一个名为 Mahendra 的电子表格用户，可以使用以下命令：

```bash
# useradd Mahendra -g finance
```

该命令为默认组 `finance` 创建了一个名为 `mahendra` 的用户。如果需要将现有用户放入 `IT` 组，可以使用以下命令：

```bash
# chgrp deven IT
```

前述命令将把 `IT` 组设置为 `deven` 的新默认组。如果你需要让一个特定用户同时属于多个组，请在 `useradd` 命令中使用 `-G` 选项，如下：

```bash
# useradd mahendra -G IT,finance
```

前述命令将用户 `mahendra` 添加为 `IT` 和 `finance` 组的成员。要查看现有组及其成员，运行以下命令：

```bash
# cat /etc/group
```

`/etc/group` 文件包含四个部分：组名、密码、组 ID 和用户。这些部分由冒号（`:`）分隔。通过查看此文件，你可以知道 Mahendra 属于哪些组。

## Linux 文件权限

Linux 通过在文件和目录上应用权限来控制未经授权的访问。在所有系统都互连的组织环境中，用户可能会访问敏感信息或读取私人电子邮件。为了避免这种情况的发生，每个文件和目录都有一个所有者或一个组，你需要获得其对应的权限（通常称为模式）。

在 Linux 中，你可以使用 `ls` 命令查看文件的权限列表。每个文件都有一组权限，用于控制哪些用户可以对该文件进行访问。文件的权限也被称为其访问模式。一个文件具有以下权限：

- `r` (-)：表示读取权限，即允许用户读取和复制特定文件。
- `w` (-)：表示写入权限，即允许用户修改特定文件。
- `x` (-)：表示执行权限，即仅允许用户执行特定文件。

你可以通过 `chmod` 命令更改你文件的权限（如果你是 `root` 用户，也可以更改其他用户文件的权限）。例如，你可以使用以下命令为用户提供写入权限：

```bash
chmod g+w [filename]
```

在前述命令中，`g` 代表文件的组，`w` 代表写入权限，`+` 表示权限已添加。

## 更改文件所有者或组

`chown` 命令用于更改文件的所有权，`chgrp` 命令用于更改组的所有权。使用 `chown` 命令的示例如下：

```bash
# chown deven file.txt
```

前述命令将 `file.txt` 的所有者更改为 `deven`。

# 3.8 管理软件包
