

要在 Admintool 中添加群组账户，请执行以下操作：

- 1. 打开终端窗口，输入 `admintool` 命令并按下回车键。或者，在 CDE 的应用管理器中，双击 `System_Admin` 文件夹中的 AdminTool 图标。AdminTool 窗口将出现。
- 2. 从“Browse”（浏览）菜单中选择 Groups（群组）命令，以查看 Groups 窗口。
- 3. 从“Edit”（编辑）菜单中选择 Add（添加）命令，以查看 AdminTool: Add Group 对话框。

![](img/256e02a6afce528d264a8d911fa0ff20_473_0.png)

- 4. 在 AdminTool: Add Group 对话框的字段中输入以下信息：
    - 在 Group Name（群组名称）字段中，输入群组账户名称。
    - 在 Group ID（群组 ID）字段中，输入 GID 编号。
    - 在 Members List（成员列表）字段中，输入用户账户名称（用逗号分隔，不要加空格）。
- 5. 单击 Apply（应用）按钮以创建群组账户，并继续创建其他群组账户。或者单击 OK（确定）按钮以创建群组账户并关闭 AdminTool: Add Group 对话框。Solaris 会将新群组的这些信息添加到 `/etc/group` 文件中。

如果你想使用 AdminTool 修改群组账户，你需要以 sysadmin（GID 14）身份登录。当你想要通过 Solaris 管理控制台访问 AdminTool 时，你必须是 root 用户。AdminTool: Groups 窗口“Edit”（编辑）菜单上的 Modify（修改）命令会打开 AdminTool: Modify Group 对话框，该对话框与前面显示的 Add Group 对话框基本相同。你也可以双击群组账户名称来打开 Modify Group 对话框。

AdminTool 中的最后一个基本群组账户操作是 Delete（删除）命令，这也需要 sysadmin 组（GID 14）登录。

要删除用户账户，请遵循以下步骤：

- 1. 在 Admin tool: Groups 窗口中单击群组账户名称以将其高亮显示。
- 2. 从“Edit”（编辑）菜单中选择 Delete（删除）命令。Admin tool: Warning 对话框将出现。

![](img/256e02a6afce528d264a8d911fa0ff20_474_0.png)

- 3. 单击 Delete（删除）按钮以删除该账户。或者单击 Cancel（取消）按钮以保持群组账户不变。

## 群组标识号

群组标识号（GID 编号）被 Solaris 用于识别群组账户。用户账户可以分配一个 GID，该分配赋予用户对群组账户可访问的文件、目录和进程的访问权限。/etc/passwd 文件将用户账户的主 GID 编号列为其第四个字段（参见本章前文的“passwd 文件”部分）。GID 编号存储在 /etc/group 文件中，如 11.12 图所示。群组文件存储群组记录；每个记录由行结束符分隔。你使用 groupadd、groupmod 和 groupdel 命令来添加、更改和删除用户账户。

许多管理员创建模拟组织结构（如会计部门 ACCT、信息技术部门 IT、人力资源部门 HR 等）的群组。这样做可以让特定类型的员工访问该类型其他员工拥有权限的所有资源，从而简化安全设计的许多方面。也创建群组以表达组织中用户的地理分布。创建群组的另一个原因是允许管理员修改系统文件或进程。最后，可能存在诸如设计或开发项目等特别项目，需要保护其主要文件。你可以通过创建诸如 DEV（开发人员）的群组并赋予其访问主要文件的权限，同时排除除 root 以外的所有人，来保护源代码。

你可以使用 groups 命令查看群组列表。当你使用命令 `groups <username>` 时，Solaris 返回该用户名所属的群组列表。Solaris 创建了一些默认的群组账户，类似于它创建的系统用户账户。表 11.2 列出了这些群组及其 GID 编号。

### 图 11.12

/etc/group 文件存储有关群组账户的信息。

![](img/256e02a6afce528d264a8d911fa0ff20_475_0.png)

### 表 11.2：系统 GID

| GID | 描述 |
|---|---|
| 1–10 | 保留给守护进程和系统维护伪群组 |
| 0 | Root 用户或超级用户账户 |
| 1 | 用于 other 群组 |
| 2 | 用于 bin 群组 |
| 3 | 用于 sys 群组 |
| 4 | 用于 adm 群组 |
| 5 | 用于 uucp 群组（Unix 到 Unix 复制程序 [UUCP]） |
| 6 | 用于 mail 群组 |
| 7 | 用于 tty 群组 |
| 8 | 用于 lp 群组 |
| 9 | 用于 Unix 到 Unix 复制程序（UUCP）的用户名 nuucp |
| 11–99 | 保留给守护进程 |
| 12 | 用于 daemon 群组 |
| 14 | 用于 sysadmin 群组 |
| 71 | 用于行式打印机（lp）进程的用户名 lp |
| 60,001 | 保留给 nobody 群组，一个具有最小访问权限的账户 |
| 60,002 | 保留给 noaccess 群组（类似于 nobody） |
| 65,534 | 保留给 nogroup 群组 |

## 更改群组状态

有时你可能需要在会话期间更改你的群组状态，就像你可以更改你的用户账户状态一样。登录后，你的用户群组是在 /etc/passwd 文件中分配给该用户名 的默认群组。更改群组状态提供了一些与更改用户账户相同的优势：它允许你访问群组资源，或者让你测试 Solaris 对特定群组的运行方式。更改你的群组账户的命令是 newgrp（新群组）命令。

newgrp 命令的语法如下：

```
newgrp <groupname>
```

你必须是指定群组的成员才能更改到该群组。如果你不是该群组的成员，Solaris 将显示错误信息 newgrp: Sorry.

## 使用 AdminSuite 3 进行账户管理

你可以使用 AdminSuite 3 在网络中添、改、删用户和群组账户。该软件安装在服务器上，通常从该位置进行管理。此外，它还提供域管理并充当设置安全策略的控制台。在接下来的章节中，你将找到如何使用 AdminSuite 管理用户和群组账户的描述。

> **注意** 要获取 AdminSuite 3，请从 www.sun.com/bigadmin/content/adminPack 免费下载。它包含在 Solaris 8 管理包中。在该位置，你还可以下载 Solaris 管理控制台（SMC）。

要打开 AdminSuite 3，请遵循以下步骤：

- 1. 在 CDE 桌面上的应用管理器的 `System_Admin` 文件夹中，双击 Solaris 管理控制台（SMC）图标。SMC 登录对话框将出现（如图 11.13 所示）。

- 2. 输入你的用户名和密码，然后单击 Log In（登录）按钮以查看 Solaris 管理控制台窗口，如图 11.14 所示。Solaris 管理控制台窗口提供对账户信息、系统实用程序和网络实用程序及功能的访问。

### 图 11.13

Solaris 管理控制台登录对话框

![](img/256e02a6afce528d264a8d911fa0ff20_477_0.png)

### 图 11.14

Solaris 管理控制台窗口

![](img/256e02a6afce528d264a8d911fa0ff20_477_1.png)

- 3. 在任一窗格中单击 **Infrastructure**（基础架构）文件夹。图 11.15 显示了 Infrastructure 窗格的内容，其中包含 Admintool 和 AdminSuite 实用程序。

![](img/256e02a6afce528d264a8d911fa0ff20_478_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_478_1.png)

- 4. 双击 **AdminSuite** 文件夹，然后双击 AdminSuite 图标。AdminSuite 登录对话框将出现（见图 11.16）。

![](img/256e02a6afce528d264a8d911fa0ff20_478_2.png)

![](img/256e02a6afce528d264a8d911fa0ff20_478_3.png)

- 5. 在 AdminSuite 中，输入具有超级用户权限的用户账户的用户名和密码，然后单击 OK（确定）按钮。如图 11.17 所示的 AdminSuite 工具将出现。

### 图 11.17

**AdminSuite 工具** 打开到 *Users*（用户）窗口

![](img/256e02a6afce528d264a8d911fa0ff20_479_0.png)

- 6. 要关闭 AdminSuite 工具，双击标题栏控件（标题栏最左侧的图标），从“Window”（窗口）菜单中选择 Close（关闭）命令，或按 Alt+F4。

## 使用 AdminSuite 管理网络用户

使用 AdminSuite 3，你可以在网络中添加、修改和删除用户账户。使用 User Accounts（用户账户）窗口，你可以选择要修改的域，甚至可以添加或删除域。你还可以查看账户的属性，并在 AdminSuite 中分配属性。此外，你可以设置安全策略，并分配允许用户在 AdminSuite 内部对其他用户账户进行更改的超级用户权限。

