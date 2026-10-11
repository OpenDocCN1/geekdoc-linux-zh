
在所示示例中，修改选项（`-m`）后面跟着字母 `u`，表示你正在为某个用户分配 ACL 权限。在冒号（`:`）之后，你指定用户名，然后是另一个冒号以及你想要分配的权限。与 `chmod` 命令一样，你可以为用户或组分配读取（`r`）、写入（`w`）和/或执行（`x`）权限（示例中给予了完整的 `rwx` 权限）。最后一个参数被替换为你正在修改的实际文件名。

## 第11章：管理用户账户

以下是用户使用 `setfacl` 命令为文件和其他用户及组添加权限的示例：

```
[may]$ ls touch /tmp/memo.txt
[may]$ ls -l /tmp/memo.txt
-rw-r--r 1 mary 0 Jan 21 09:27 /tmp/memo.txt
[may]$ setfacl -m ubill:rw /tmp/memo.txt
[may]$ setfacl -m g:sales:rw /tmp/memo.txt
```

在前面的示例中，mary 使用 `setfacl` 命令创建了一个备录文件，她为名为 bill 的用户修改（`-m`）权限，使其拥有该文件的读/写（`rw`）权限。然后，她修改了 sales 组的权限，使得该组的任何人都将拥有读/写权限。查看该文件的 `ls -l` 和 `setfacl` 输出：

```
[may]$ ls -l /tmp/memo.txt
-rw-r--+ 1 mary 0 Jan 21 09:27 /tmp/memo.txt
[may]$ setfacl /tmp/memo.txt
# file: tmp/memo.txt
# owner: mary
# group: mary
user:rw-
user:bill:rw-
group:rw-
group:sales:rw-
mask:rw--
other::r--
```

从 `ls -l` 的输出中，注意 `rw-rw--+` 输出中的加号（`+`）。加号表示该文件设置了 ACL，因此你知道需要运行 `getfacl` 命令来查看 ACL 是如何设置的。输出显示 mary 为所有者和组（与你在 `ls -l` 中看到的相同），普通用户权限（`rw-`）以及 ACL 用户 bill 的权限（`rw-`）。组权限和对 sales 组的权限也是如此。其他权限为 `r--`。

`mask` 行（位于上一个 `getfacl` 示例的末尾）需要特殊讨论。一旦你在文件上设置了 ACL，文件上的普通组权限就会设定 ACL 用户或组在文件上可以拥的最大权限掩码。因此，即使你为个人提供的 ACL 权限超过了组权限允许的范围，该个人的有效权限也不会超过组权限，如下例所示：

```
[may]$ chmod 644 /tmp/memo.txt
[may]$ setfacl /tmp/memo.txt
# file: tmp/memo.txt
# owner: mary
# group: mary
user:rw-
user:bill:rw- #effective:r--
```

```
group::rwx- #effective:r--
group::sales:rw- #effective:r--
mask::r--
other::r--
```

注意前面的示例中，尽管用户 bill 和 sales 组拥有 `rw--` 权限，但 bill 或 sales 组的任何人都无法更改文件，除非 mary 重新开启权限（例如通过输入 `chmod`）。

### 设置默认 ACL

在目录下设置默认 ACL 意味着在其创建的新文件和子目录将继承这些权限。要设置默认 ACL，请使用带有 `-d` 选项的 `setfacl` 命令。考虑以下示例：

```
[may]$ mkdir projects
[may]$ setfacl -d -m u:bill:rwx projects
[may]$ setfacl -d -m g:sales:rwx projects
```

当你在 `projects` 目录下创建一个新文件时，它将继承默认 ACL：

```
[may]$ touch projects/newfile.txt
[may]$ getfacl projects/newfile.txt
# file: projects/newfile.txt
# owner: mary
# group: mary
user::rwx
user:bill:rwx
group::rwx
group:sales:rwx
mask:rwx
other::r--
```

默认 ACL 只适用于目录中创建的新对象。要更改现有对象的权限，必须使用不带 `-d` 选项的 `setfacl` 命令。

### 启用 ACL

要使用 ACL，文件系统必须带有 `acl` 选项时挂载。对于大多数现代文件系统（如 `ext4` 和 `xfs`），这是默认启用的。但对于较旧的文件系统，你可能需要在 `/etc/fstab` 文件中添加它。

要检查文件系统是否启用了 ACL，可以使用 `mount` 命令：

```
mount | grep acl
```

如果不存在 `acl` 选项，你可以使用 `acl` 选项重新挂载文件系统：

```
mount -o remount,acl /mount/point
```

一旦启用 ACL，你就可以使用 `setfacl` 和 `getfacl` 来管理细粒度权限。

## 第11章：用户账户管理

### 为协作添加目录

当你使用 `chmod` 命令在文件系统上创建权限时，通常会忽略一组特殊的三个位权限位。这些权限位可以为命令和目录设置特殊权限。本节的重点是设置可以帮助你创建用于协作的目录的位。

除了用户、组和其他和其他的读、写、执行位外，这些特殊的文件权限位可以使用 `chmod` 命令进行设置。例如，如果你运行 `chmod 775 /mnt/xyz`，隐含的权限是 `0775`。要更改权限，你可以将数字 `0` 替换为这三个位中的任何组合（`4`、`2` 和 `1`），或者使用数值代替（如果你需要提醒你权限的工作原理，请参阅第 4 章“在文件系统中移动”）。字母和数字如表 11.1 所示。

#### 11.1 创建和使用文件的命令

| 名称 | 数值值 | 字母值 |
|---|---|---|
| 设置用户 ID 位（Set UID） | 4 | u+s |
| 设置组 ID 位（Set GID） | 2 | g+s |
| 粘滞位（Sticky bit） | 1 | o+t |

我们感兴趣用于创建协作目录的位是设置组 ID（`2`）和粘滞位（`1`）。如果你对设置用户 ID 和设置组 ID 的其他用途感兴趣，请参考侧边栏“Set UID 和 Set GID 位命令”。

### 创建协作目录（设置 GID 位）

当 true 创建一个设置了 GID 的目录时，在该目录中创建的任何文件都会分配给目录本身所在的组。这种思想是让组内成员可以在其中共享文件，但仍然保护它们免受其他用户的干扰。以下是为我创建的 `sales` 组所有用户创建协作目录的步骤：

1. 创建一个用于协作的组：

```
# groupadd -g 301 sales
```

2. 将你想要共享文件的某些用户加入组（我使用了 mary）：

```
# usermod -aG sales mary
```

3. 创建协作目录：

```
# mkdir /mnt/salestools
```

# 第三部分：成为 Linux 系统管理员

### 使用 Set UID 和 Set GID 位命令

设置 UID 和设置 GID 位用于特殊的可执行文件，允许这些命令以与其他命令不同的方式运行。通常，当用户运行命令时，该命令以用户的权限运行。换句话说，如果你以 root 身份运行 `vi` 命令，那么 `vi` 命令的实例将具有读写用户可以读写的文件的权限。

带有设置 UID 或设置 GID 位命令则不同。是分配给命令的所有者组决定了命令访问计算机上资源的权限。因此，设置 UID 的命令将以 root 身份运行但没有权限，由 apache 拥有的设置 GID 命令将具有 apache 权限。

开启了设置位的应用程序示例包括 `su` 和 `newgrp` 命令。在这两种情况下，命令必须以 root 用户身份运行才能完成工作。然而，为了实际获得权限，用户必须提供密码。你可以通过通常第一位（u）显示的 `s` 来判断 su 是否为设置 UID 位的命令：

```
$ ls /bin/su
- rwsrxr-x. 1 root root 30092 Jan 30 07:11 su
```

4. 将 sales 组分配给目录：

```
# chmod sales /mnt/salestools
```

5. 将目录权限更改为 `2775`。这设置了组 GID 位（`2`）、用户的完全 `rwx`（`7`）、组的 `rwx`（`7`）以及其他人的 `r-x`（`5`）：

```
# chmod 2775 /mnt/salestools
```

6. 变成 mary 并运行 `su mary`。作为 mary，在共享目录中创建一个文件并查看权限。当你列出权限时，你会发现该目录设置了 GID 位，因为在必须有组执行权限的地方出现了一个小写的 `s`（`rwxrxr-x`）：
