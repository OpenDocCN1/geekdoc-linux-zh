

`/mnt` 目录，按照 Unix 惯例，是放置临时挂载点（例如 CD-ROM 驱动器、远程网络驱动器和软盘驱动器）的位置。如果需要挂载文件系统，可以使用 `mount` 命令并遵循以下语法：

```
mount -t file_system_type device_to_mount directory_to_mount_to
```

例如，如果你想将 CD-ROM 挂载到 `/mnt/cdrom` 目录，可以输入：

```
$ mount -t iso9660 /dev/cdrom /mnt/cdrom
```

这假设你的 CD-ROM 设备名为 `/dev/cdrom`，并且你希望将其挂载到 `/mnt/cdrom`。有关更具体的信息，请参阅 mount 手册页，或在命令行中输入 `mount -h` 以获取帮助信息。挂载完成后，你可以使用 `cd` 命令通过刚刚创建的挂载点访问新可用的文件系统。

## 卸载文件系统

要从系统中卸载（移除）文件系统，请使用 `umount` 命令，并指定挂载点或设备。例如，要卸载 cdrom，请使用以下命令：

```
$ umount /dev/cdrom
```

`mount` 命令使你可以访问文件系统，但在大多数现代 Unix 系统中，自动挂载功能使此过程对用户不可见，且无需干预。

## 用户和组配额

用户和组配额提供了机制，用于将单个用户或特定组内所有用户使用的空间限制在管理员定义的数值范围内。配额围绕两个限制进行运作，当空间量或磁盘块数量开始接近管理员定义的限值时，允许用户采取某些操作：

-   **软限制** – 如果用户超过定义的限制，将有一个宽限期，允许用户释放部分空间。
-   **硬限制** – 当达到硬限制时，无论宽限期如何，都无法再分配更多的文件或块。

有许多用于管理配额的命令：

| 命令 | 描述 |
| :--- | :--- |
| quota | 显示用户或组的磁盘使用量和限制。 |
| edquota | 这是一个配额编辑器。可以使用此命令编辑用户或组的配额。 |
| quota check | 扫描文件系统的磁盘使用情况，创建、检查和修复配额文件。 |
| setquota | 这也是一个命令行配额编辑器。 |
| quotaon | 向系统发出通知，应在一个或多个文件系统中启用磁盘配额。 |
| quotaoff | 向系统发出通知，应在一个或多个文件系统中禁用磁盘配额。 |
| repquota | 打印指定文件系统的磁盘使用量和配额摘要。 |

# 第十九章：UNIX 用户管理

Unix 系统上有三种类型的账户：

-   **Root 账户** – 也称为超级用户，对系统具有完全且不受限制的控制权。超级用户可以运行任何命令而不受限制。应假设此用户是系统管理员。
-   **系统账户** – 系统账户是系统特定组件运行所需的账户，例如邮件账户和 sshd 账户。这些账户通常用于系统中的某些特定功能，对其进行的任何修改都可能对系统产生不利影响。
-   **用户账户** – 用户账户为用户和用户组提供对系统的交互式访问权限。普通用户通常被分配到这些账户，并且通常对关键系统文件和目录具有有限的访问权限。

UNIX 支持*组账户*的概念，它在逻辑上将多个账户组合在一起。每个账户都必须是某个组账户的一部分。Unix 组在处理文件权限和进程管理方面起着重要作用。

## 管理用户和组

主要有三个用户管理文件：

-   */etc/passwd:* – 保存用户账户和密码信息。此文件持有 Unix 系统上关于账户的大多数信息。
-   */etc/shadow:* – 保存对应账户的加密密码。并非所有系统都支持此文件。
-   */etc/group:* – 包含每个账户的组信息。
-   */etc/gshadow:* – 包含安全的组账户信息。

使用 `cat` 命令检查上述所有文件。

大多数 Unix 系统上可用于创建和管理账户和组的命令：

| 命令 | 描述 |
| :--- | :--- |
| **useradd** | 向系统添加账户。 |
| **usermod** | 修改账户属性。 |
| **userdel** | 从系统中删除账户。 |
| **groupadd** | 向系统添加组。 |
| **groupmod** | 修改组属性。 |
| **groupdel** | 从系统中移除组。 |

## 创建组

在创建任何账户之前，你需要先创建组，否则你将不得不使用系统中现有的组。你可以在 /etc/groups 文件中找到所有组。所有默认组都是系统账户特定的组，不建议将它们用于普通账户。使用以下语法创建新的组账户：

```
groupadd [-g gid [-o]] [-r] [-f] groupname
```

以下是参数的详细说明：

| 选项 | 描述 |
| :--- | :--- |
| **-g GID** | 组 ID 的数值。 |
| **-o** | 此选项允许添加具有非唯一 GID 的组 |
| **-r** | 此标志指示 groupadd 添加一个系统账户 |
| **-f** | 此选项导致如果指定组已存在则仅以成功状态退出。如果使用 -g 且指定的 GID 已存在，则会选择其他（唯一）的 GID |
| **groupname** | 要创建的实际组名称。 |

如果你不指定任何参数，系统将使用默认值。以下示例将使用默认值创建一个 developers 组，这对于大多数管理员来说是可接受的。

```
$ groupadd developers
```

## 修改组

要修改组，请使用 `groupmod` 语法：

```
$ groupmod -n new_modified_group_name old_group_name
```

要将 developers_2 组名更改为 developer，请键入：

```
$ groupmod -n developer developer_2
```

以下是如何将 financial 的 GID 更改为 545：

```
$ groupmod -g 545 developer
```

## 删除组

要删除现有组，你只需要 `groupdel` 命令和组名。要删除 developer 组，命令如下：

```
$ groupdel developer
```

这仅移除组本身，而不会移除与该组关联的文件。这些文件仍可由其所有者访问。

## 创建账户

让我们看看如何在你的 Unix 系统上创建新账户。使用以下语法创建用户账户：

```
useradd -d homeDir -g groupName -m -s shell -u userid accountname
```

可用参数：

| 选项 | 描述 |
| :--- | :--- |
| -d homeDir | 指定账户的主目录。 |
| -g groupname | 为此账户指定一个组账户。 |
| -m | 如果主目录不存在，则创建它。 |
| -s shell | 指定此账户的默认 shell。 |
| -u userid | 你可以为此账户指定用户 ID。 |
| accountname | 要创建的实际账户名称 |

如果你不指定参数，系统将使用默认值。`useradd` 命令会修改 /etc/passwd、/etc/shadow 和 /etc/group 文件，并创建一个主目录。以下是一个示例，它将创建一个名为 mcmohd 的账户，将其主目录设置为 /home/mcmohd，组设置为 developers。该用户将被分配 Korn Shell。

```
$ useradd -d /home/mcmohd -g developers -s /bin/ksh mcmohd
```

在发出上述命令之前，请确保你已使用 `groupadd` 命令创建了 developers 组。一旦账户创建完成，你可以使用 passwd 命令设置其密码，如下所示：

```
$ passwd mcmohd20
Changing password for user mcmohd20.
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
```

当你键入 `passwd accountname` 时，如果你是超级用户，它会给你更改密码的选项；否则，你只能使用相同但不指定账户名称的命令更改你自己的密码。

## 修改账户

`usermod` 命令使你可以修改现有账户

