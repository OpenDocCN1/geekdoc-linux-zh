

取消勾选表示 `The account is enabled` 的复选框。点击窗口底部的 `Accept` 按钮，即可完成设置。

该账户已被禁用，后续可以使用类似的方法重新启用。

### 3.1.10 启用用户账户

默认情况下，所有新建的用户账户都是启用状态。如果需要启用某个账户，可以使用 `linuxconf` 进行操作。

- 打开 `Config => Users accounts => Normal => User accounts`。勾选 `The account is enabled` 复选框。

### 3.1.11 删除用户账户

> **请注意**
> 虽然提供了保留与该账户关联文件的选项，但任何被删除的文件都将永久丢失且实际上无法恢复。使用此选项时请务必小心！

要删除账户：

- 打开 `Config => Users accounts => User accounts`。
- 在 `User accounts` 屏幕（参见图 3–3，`Users Accounts Screen`）上选择要删除的账户。
- 在 `User information` 屏幕底部，选择 `Del` 以删除该账户。

随后，`Linuxconf` 将提示您一系列选项。

**图 3–7** 删除账户屏幕

![](img/eda1471ab4ce718c791c97a85559a478_88_0.png)

默认选项是归档该账户的数据。归档选项具有以下效果：

1. 将用户从用户账户列表中移除；
2. 将用户主目录中包含的所有内容归档（使用 tar 和 gzip 压缩），并将生成的文件存储在 `default_home_directory/oldaccounts` 目录中。对于名为 `useraccount` 的账户，文件名类似于：
   `useraccount-2000-01-10-497.tar.gz`
   日期表示账户被删除的时间，紧随其后的数字是实际执行删除操作的进程 ID。`oldaccounts` 目录创建于与所有用户目录相同的位置，并会在首次使用此选项删除用户账户时自动创建。
3. 不属于用户主目录但由该用户拥有的文件将保留。这些文件的所有者是已删除账户的用户 ID (UID)。如果您创建一个新的账户并明确指定已删除账户的 UID，新账户将成为这些剩余文件的所有者。

在 *Deleting account* <accountname> 屏幕（参见图 3−7，*Deleting Account Screen*）上选择 **Delete the account's data** 将会：

1. 将用户从用户账户列表中移除；
2. 移除用户的主目录及其所有内容。

**请注意**

不属于用户主目录但由该用户拥有的文件将保留在系统中。这些文件的所有者仍将是已删除账户的用户 ID (UID)。如果您创建一个新的账户并明确指定已删除账户的 UID，新账户将成为这些“孤儿”文件的所有者。

在 *Deleting account* <accountname> 屏幕（参见图 3−7，*Deleting Account Screen*）上选择 **Leave the account's data in place** 将会：

1. 将用户从用户账户列表中移除；
2. 保留用户的主目录（包含所有文件）不变。

**请注意**

由已删除账户的用户 ID (UID) 拥有的文件和目录将保留在系统中。如果您创建一个新的账户并明确指定已删除账户的 UID，新账户将成为这些“孤儿”文件的所有者。

### 3.1.12 组

所有用户都属于一个或多个组。正如每个文件都有特定的所有者一样，每个文件也属于特定的组。该组可能是文件所有者特有的，也可能是所有用户共享的组。读取、写入或执行文件的权限可以分配给组；这与所有者的权限是分开的。例如，文件的所有者可以写入文档，而组的其他成员可能只能读取该文档。

#### 创建组

要创建一个新组：

- 打开 Config => Users accounts => Normal => Group definition。

根据 Control => Filters 中的设置，您可能会看到一个筛选屏幕。提供筛选条件，或选择 Accept 以绕过筛选。

图 3–8 用户组屏幕

![](img/eda1471ab4ce718c791c97a85559a478_90_0.png)

在 User groups 屏幕底部选择 Add。

**图 3-9 组规格屏幕**

![](img/eda1471ab4ce718c791c97a85559a478_91_0.png)

输入组名。您还可以指定组成员，这可以在 **Alternate members** 字段中完成。用户列表应以空格分隔，意味着每个用户名与其下一个用户名之间必须有一个空格。留空 **Group name** 字段，以便系统为您的新组分配一个 **Group ID (GID)**。完成后，选择 **Accept**，组将被创建。

#### 删除组

要删除一个组：

- 打开 **Config => Users accounts => Normal => Group definitions**。
- 根据 **Control => Features** 中的筛选设置，您可能会看到一个筛选屏幕。您可以使用筛选功能通过指定前缀来缩小组的选择范围。
- 无论是否使用前缀，请在屏幕底部选择 **Accept**。
- 在 **User groups** 屏幕（参见图 3-8，*User Groups Screen*）上选择要删除的组。

您将被带到 **Group specification** 屏幕（参见图 3–9，*Group Specification Screen*）。

选择 `Del` 以删除该组。随后 `Linuxconf` 将提示您确认删除。选择 **yes** 以删除该组。

该组的文件仍将保留，且其各自的所有者仍对它们拥有完全控制权。组名将被替换为已删除组的 ID。可以使用 `chgrp` 命令将文件分配给新组。在 shell 提示符下输入 `info chgrp` 或 `man chgrp` 可以获取有关 `chgrp` 的更多信息。如果创建了新组并指定了已删除组的 ID，那么新组将能够访问已删除组的文件。不用担心，`linuxconf` 不会像回收旧用户 ID 那样回收旧组号，因此这不会意外发生。

#### 修改组成员资格

有两种方法可以修改进属某个组的用户列表。您可以更新每个用户账户本身，或者您可以更新组定义。通常，更新每个组定义是最快的方法。如果您计划为每个用户更改的信息不仅仅是组信息，那么更新每个用户账户可能更简单。

我们首先详细介绍组定义方法。

- 在 shell 提示符下输入 `linuxconf` 来启动 `linuxconf`。
- 打开 **Config => Users accounts => Normal => Group definitions**。
- 根据 **Control => Features** 中的筛选设置，您可能会看到筛选屏幕。使用筛选功能缩小列表，或直接选择 **Accept** 以绕过筛选。
- 选择您要修改的组。这将打开 *Group specification* 屏幕（参见图 3–9，*Group Specification Screen*）。
- 在 **Alternate members** 字段中添加或移除每个用户。确保所有用户名都由空格字符分隔。
- 选择位于屏幕底部的 **Accept**。

这将自动更新每个用户账户，组会显示在 Supplementary groups 字段中（如果已添加）或消失（如果已移除）。也可以通过修改每个单独的用户账户来添加和移除组。

- 在 shell 提示符下输入 `linuxconf` 来启动 `linuxconf`。
- 打开 **Config => Users accounts => Normal => User accounts**。
- 根据 **Control => Features** 中的设置，您可能会看到筛选屏幕。使用筛选功能缩小列表，或选择 **Accept** 以绕过筛选。
- 在 **User accounts** 屏幕（参见图 3-3，*Users Accounts Screen*）上，选择您希望更新的用户。您将被带到 **User information** 屏幕。
- 在 **Supplementary groups** 字段中添加或移除所需的组。每个组之间应由空格字符分隔。
- 一旦完成所有更改，选择屏幕底部的 `Accept`。

这将自动更新组定义。对每个用户重复此过程。

### 3.1.13 文件系统

文件系统由文件和目录组成，所有这些都从一个根目录开始。根目录可以包含任意数量的文件和其他目录，每个目录依次遵循相同的结构。典型的文件系统看起来像一棵倒置的树，目录作为分支，文件作为叶子。文件系统驻留在诸如软盘驱动器、硬盘和 CD-ROM 等大容量存储设备上。

例如，DOS 和 Windows 机器上的软盘驱动器通常由 `A:\` 表示。这既描述了该设备（`A:`），也描述了该设备上的根目录（`\`）。在同一系统中，主硬盘通常被称为 `C` 盘，因为第一个硬盘的设备规范是 `C:`。要指定 C 盘上的根目录，您需要使用 `C:\`。在此配置下，有两个文件系统——一个在 `A:` 上，另一个在 `C:` 上。为了指定 DOS/Windows 文件系统上的任何文件，您必须明确

