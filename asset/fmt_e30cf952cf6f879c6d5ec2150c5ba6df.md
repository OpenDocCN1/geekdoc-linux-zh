
你可以使用 `chmod` 命令来更改文件访问权限。`chmod` 命令的语法如下：

```
chmod [OPTION] .. MODE[,MODE] .. FILE
```

为了理解 `chmod` 命令的意义，请考虑以下示例：某机构的团队成员 Himanshu 向他的团队负责人 Poonam 抱怨，他无法执行一个名为 `program.c` 的程序。Poonam 需要检查该程序文件的权限。Poonam 可以使用以下命令来查看 `program.c` 程序的文件的权限：

```bash
$ ls -l program.c
```

上一个命令的输出为：

```
-rw-rw--r-- 1 root tech 50 Oct 22 21:01 program.c
```

上一个输出显示了文件的默认权限。Poonam 可以使用以下命令更改 `program.c` 文件的权限：

```bash
$ chmod u+x program.c
```

在上一个命令中，

- 'u' 表示文件所有者
- '+' 表示要赋予权限
- 'x' 表示执行权限
- 'program.c' 代表文件名

现在，文件 `program.c` 的文件访问权限将会发生变化。

```bash
$ ls -l program.c
```

上一个命令显示了以下输出：

```
-rwxr-xr-x -- 1 root tech 50 Oct 22 21:01 program.c
```

移除组所有者读权限的命令为：

```bash
$ chmod g-r program.c
```

在上一个命令中，'g' 表示组所有者，'-' 表示要移除该权限。

权限将显示为：

```bash
$ ls -l program.c
-rw-r--r-- 1 root tech 50 Oct 22 21:01 program.c
```

移除赋予其他用户的读权限的命令为：

```bash
$ chmod o-r program.c
```

在上一个命令中，'o' 表示其他用户。

权限将显示为：

```bash
$ ls -l program.c
-rw-w--r 1 root tech 50 Oct 22 21:01 program.c
```

Linux 还允许文件所有者更改该文件对所有类别类用户的权限。

移除所有用户执行权限的命令为：

```bash
$ chmod a-x program.c
```

在上一个命令中，'a' 表示所有用户。

文件 `program.c` 的文件访问权限将显示为：

```bash
$ ls -l program.c
-rw-w------ 1 root tech 50 Oct 22 21:01 program.c
```

## 更改文件所有权

你可以使用 `chmod` 命令来更改文件和目录的所有权。`chown` 也可以用于更改文件的组所有权。`chown` 命令的语法如下：

```
chown [options] owner[.group] <file/s>
chown [options] .group <file/s>
chown [options] -reference=file <file/s>
```

例如，以下命令更改了 `/home/Java_proj` 目录下所有文件的所有权：

```bash
# chown sumit /home/Java_proj/*
```

上一个命令将 `/home/Java_proj` 目录下所有文件的所有权分配给用户 `sumit`。

下表列出了配合 `chown` 命令使用的选项：

### 表 10-9 `chown` 命令使用的选项

| 选项 | 功能 |
| :--- | :--- |
| -R | 允许你递归更改特定目录下文件和目录的所有权。 |
| -f | 允许你抑制错误消息。例如，如果你指定的文件名不存在，带有 -f 选项的 `chown` 命令将不会显示任何错误消息。 |
| -V | 允许你显示所有处理文件的状态。 |
| -C | 允许仅在所有权更改时显示处理文件的状态。 |

> 在 Linux 中，只有超级用户（super user）可以更改文件的所有权。

## 练习

从命令行管理用户和组账户

Bluemoom Computers 的系统管理员 Prabhakar 被分配任务为新招募的开发者创建用户账户。此外，Prabhakar 需要为已离公司的 Shilpa 和 Manoj 创建用户账户。

此外，Prabhakar 需要根据分配给开发者的项目为开发者创建一个组账户。同一项目的开发者应该是同一个组的成员。在创建用户和组后，Prabhakar 需要为所有同组的开发者授予文件权限。

帮助 Prabhakar 完成上述任务。

为了解决上述问题，Prabhakar 需要执行以下任务：

- 1. 管理组
- 2. 管理用户账户
- 3. 创建项目目录并分配权限
- 4. 更改默认权限

### 管理组

要管理组，Prabhakar 可以使用以下命令创建一个名为 project 的新组：

```bash
# groupadd -g 1000 project
```

### 管理用户账户

Prabhakar 需要执行以下步骤：

- 删除现有用户：

```bash
# userdel -r shila
# userdel -r manoj
```

- 创建新用户：

```bash
# useradd -u 550 -c "Mahima" -g 1000 mahima
# 设置密码
# passwd mahima
```

### 创建项目目录并分配权限

要创建目录，Prabhakar 需要执行以下操作：

- 创建目录：

```bash
# mkdir /project
```

- 将所有权分配给组：

```bash
# chown project /project
```

### 更改默认权限

为了禁止所有者以外的用户进行写入和执行，Prabhakar 应该使用以下命令：

```bash
# chmod 770 /project
```

# Linux 中的存储管理

Linux 支持多种文件系统，如 ext2 和 ext3。它还允许使用磁盘配额（disk quotas）来管理磁盘。本章将介绍文件系统，并介绍了如何创建、挂载和卸载文件系统。解释了如何创建、激活和删除交换空间（swap space）。此外，本章解释了如何创建和删除分区。最后，本章包含一个从 Linux 访问 Windows 驱动器的练习。

## Linux 中的文件识别

文件系统是操作系统用于管理存储在分区上的文件的方法和数据结构的集合。文件系统定义了文件在分区上的组织方式。当你访问文件系统时，Linux 以文件排列的形式组织数据。

硬盘上可以存在多个文件系统。然而，文件系统的数量取决于分区的数量。一个分区只能包含一个文件系统。文件系统包含以下唯一属性：

- 超块（Superblock）：指定文件系统的特征，例如文件系统的大小。
- 节点（Inode）：包含文件信息，如文件在硬盘上的位置、文件所有者以及文件创建时间。
- 目录项（Directory Entry）：分配给文件的节点号及其名称。
- 数据块（Data Block）：存储文件数据。
- 间接块（Indirect Block）：代表动态创建的数据块。节点中始终存在若干数据块。如果你需要的数据块比节点中存在的多，则通过分配指向新数据块的的空间来动态创建数据块。这些动态创建的数据块被称为间接块。

Red Hat Linux 9 具有类似于 UNIX 的单层次目录结构。目录结构从根目录（/）开始。根目录下的所有文件和目录都由文件系统管理。

## Linux 中的存储管理

你可以在硬盘分区上创建两种类型的文件系统。特定类型文件系统的创建取决于数据是存储在本地还是从远程计算机访问。你可以创建的两种文件系统如下：

- 本地文件系统
- 网络文件系统

## 本地文件系统

文件系统有多种类型，取决于所使用的文件格式类型。文件格式是在硬盘上组织文件和目录的方法。各种文件系统的类型取决于存储数据时使用的格式：

- 第二级扩展 (`ext2`) 文件系统：支持最大为 256 个字符的文件名。`ext2` 文件系统的最大大小大于 4 TB。`ext2` 文件系统使用超级块（superblock）来存储文件系统的状态。文件系统的状态用于验证文件系统是否包含错误。
- 第级扩展 (`ext3`) 文件系统：Linux 的默认文件系统。`ext3` 文件系统是 `ext2` 文件系统的更新。`ext3` 文件系统提供了日志（journal）功能，这是 `ext2` 文件系统不具备的。日志文件系统会将数据存储多次，以便在系统崩溃时稍后恢复。尽管写入了多次数据，但 `ext3` 文件系统的吞吐量大于 `ext2` 文件系统，因为 `ext3` 文件系统中的日志功能有助于优化硬盘头的移动。`ext3` 文件系统支持最大 4 TB 的文件系统大小和最大 2 GB 的文件大小。
- 日志文件系统 (`JFS`)：提供日志功能以实现快速恢复文件系统。`JFS` 支持最小 16 MB 和最大 32 PB 的文件系统大小。

## 基于网络的文件系统
