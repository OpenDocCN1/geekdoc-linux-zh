

## 删除组 — 总览

要删除一个组：

- 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 打开 [Config] -> [Users accounts] -> [Normal] -> [Group definitions]。

如果您有超过 15 个组，您将获得一个筛选屏幕（见图 8-9）来通过指定前缀来缩小组的选择范围。

- 有或没有前缀，在屏幕底部选择 Accept。
- 在 User groups 屏幕（见图 8-10）中选择您要删除的组。
- 您将被呈现 Group specification 屏幕（见图 8-11）。
- 选择 Del 以删除该组。Linuxconf 然后会提示您确认删除。选择 yes 以删除该组。

该组的 files 将仍然保留，并且其各自的所有者仍将对其拥有完全控制权。组名将被替换为已删除组的 ID。文件可以通过使用 chgrp 命令分配给新组。有关 chgrp 的更多信息，可以在 shell 提示符下输入命令 info chgrp 或 man chgrp。 如果创建了一个新组并指定了已删除组的 ID，则该新组将有权访问已删除组的文件。 不用担心，Linuxconf 不会像旧用户 ID 那样回收旧组号，因此不会意外发生。

## 修改组成员身份

有两种方法可以修改属于一个组的用户的列表。您可以更新每个用户账户本身，也可以更新组定义。一般来说，最快的方法是更新每个组定义。如果您计划更改每个用户的不仅仅是组信息的信息，那么更新每个用户账户可能更容易。

## 修改组成员身份 — 快速参考

### 在 Groups 下

- 1 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 2 打开 [Config] -> [Users accounts] -> [Normal] -> [Group definitions]。
- 3 选择您要添加或删除用户的组。
- 4 在 Alternate members(opt) 字段中添加或删除新用户；确保所有用户名都用空格 " " 字符分隔。
- 5 选择 Accept。

### 在 Users 下

- 1 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 2 打开 [Config] -> [Users accounts] -> [Normal] -> [User accounts]。
- 3 选择您要添加或删除组的 user。相应地调整 Supplementary groups 字段；确保所有组名都用空格 " " 字符分隔。
- 4 选择 Accept。
- 5 对每个要添加的额外用户重复步骤 3 到 5。

## 修改组成员身份 — 总览

我们将首先详细介绍组定义方法。

- 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 打开 [Config] -> [Users accounts] -> [Normal] -> [Group definitions]。

如果您有超过 15 个组，您将获得一个筛选屏幕（见图 8-9）来通过指定前缀来缩小组的选择范围。

- 有或没有前缀，在屏幕底部选择 Accept。
- 选择您要修改的组。这将打开 Group specification 屏幕（见图 8-11）。
- 从 Alternate members 字段中添加或删除每个用户。确保所有用户名都用空格 " " 字符分隔。
- 完成此操作后选择 Accept，它位于屏幕底部。

这将自动更新每个用户账户，并在添加时在 Supplementary groups 字段中显示该组，或在删除时将其移除。添加和删除组也可以通过修改每个单独的用户账户来完成。

- 在 shell 提示符下输入 linuxconf 启动 Linuxconf。
- 打开 [Config] -> [Users accounts] -> [Normal] -> [User accounts]。

如果系统上有超过 15 个账户，Linuxconf 将为您提供一个筛选屏幕（见图 8-2）。

- 在 User accounts 屏幕（见图 8-3）中，选择您要更新的用户。您将被呈现 User information 屏幕（见图 8-6）。
- 从 Supplementary groups 字段中添加或删除所需的组。每个组应由空格 " " 字符分隔。
- 完成您想要的所有更改后，在屏幕底部选择 Accept。

这将自动更新组定义。对每个用户重复此过程。

## CD-ROMs、软盘、硬盘和文件系统 — 内部解析

文件系统由文件和目录组成，所有内容都从单个根目录开始。根目录可能包含任意数量的文件和其他目录，每个目录依次如此。平均文件系统通常看起来像一棵倒置的树，目录作为分支，文件作为叶子。文件系统驻留在磁盘驱动器、硬盘驱动器和 CD-ROM 等大容量存储设备上。

