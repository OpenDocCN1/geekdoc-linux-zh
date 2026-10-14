

以下是 `/etc/passwd` 文件的示例：

```text
at:x:25:25:Batch jobs daemon:/var/spool/atjobs:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
ftp:x:40:49:FTP account:/srv/ftp:/bin/bash
games:x:12:100:Games account:/var/games:/bin/bash
gdm:x:50:15:Gnome Display Manager daemon:/var/lib/gdm:/bin/bash
haldaemon:x:101:102:User for haldaemon:/var/run/hal:/bin/false
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
...
geeko:x:1000:100:Geeko Chameleon:/home/geeko:/bin/bash
```

`/etc/passwd` 文件中的每一行代表一个用户，并包含图 9-9 所示的信息（以冒号分隔）。

![](img/9129877170834ca9d5fdac5319bf5f12_297_0.png)

请注意每行中字段的以下内容：

- *用户名*—这是用户登录系统时输入的名称（登录名）。
- *密码*—此字段中的 x 表示密码存储在 `/etc/shadow` 文件中。
- *UID*—根据 Linux 标准，保留了三个数字范围：
  - 0 用于 root
  - 1–99 用于系统本身
  - 100–499 用于特殊系统用户（如服务和程序）
  - 1000+ 用于普通用户
- *GID*—组编号。根据 Linux 标准，保留了两个数字范围：
  - 0–99 用于特殊系统组，包括 root（如服务和程序）
  - 100+ 用于普通组
- *注释字段*—通常在此处存储用户的全名。房间号或电话号码等信息也可以存储在此处。

- *主目录*—用户的个人目录通常位于 /home 目录下，并与用户（登录）名相同。
- *登录 Shell*—用户成功登录后启动的 shell。在 Linux 中，这通常是 /bin/bash（Bourne Again shell）。shell 必须列在 /etc/shells 文件中。

![](img/9129877170834ca9d5fdac5319bf5f12_298_0.png)

有关此文件的更多信息，请输入 man 5 passwd。

shell 必须列在 /etc/shells 文件中。

## /etc/shadow

/etc/shadow 文件存储加密的用户密码和密码过期信息。大多数 Linux 系统使用 shadow 密码。
该文件只能由 root 用户更改，并可由 root 用户和 shadow 组成员读取。以下是 /etc/shadow 文件的示例：

```
at:!:13181:0:99999:7:::
bin:*:13181::::::
daemon:*:13181::::::
ftp:*:13181::::::
games:*:13181::::::
gdm:!:13181:0:99999:7:::
lp:*:13181::::::
root:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181:0:99999:7:-1::
xay0u3:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181::::::
sshd:!:13181:0:99999:7:::
ucp:*:13181::::::
wwwrun:+:13181::::::
geeko:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181:0:99999:7:-1::
```

/etc/shadow 文件中的每一行属于一个用户，并包含图 9-10 所示的字段。

![](img/9129877170834ca9d5fdac5319bf5f12_298_1.png)

Figure 9-10

图 9-10 显示了用户 geeko 的条目，其中包含加密密码。明文密码是 novel1。

加密密码使用 Blowfish 算法编码。加密词由字母、数字和一些特殊字符组成。如果在 Password 字段中出现无效字符（如“*”或“!”），则该用户具有无效密码。

许多用户，如 wwwrun（Apache Web 服务器）或 bin，在 Password 字段中有星号（“*”）。这意味着这些用户无法登录系统，但对于特殊应用程序是必需的。

如果 Password 字段为空，则用户可以在不输入密码的情况下登录系统。Linux 系统中应始终设置密码。

每行末尾的信息决定了一些限制：

- *上次更改*—上次密码更改日期。该数字代表自 1970 年 1 月 1 日以来的天数。
- *下次可更改*—用户可以在更改密码之前密码的最小使用期限。
- *下次必须更改*—用户可以在密码过期前使用同一密码的天数。
- *警告*—密码过期前用户获得警告的天数。输入 −1 以禁用警告。
- *限制*—密码过期后用户仍可登录的天数。输入 −1 表示无限访问。（当然，这没有意义。）
- *锁定*—账户过期的日期。日期必须采用 YYYY-MM-DD 格式。如果账户永不过期，请将字段留空。

## /etc/group

/etc/group 文件存储组信息。以下是 /etc/group 文件的示例。

```
at:!:25:
audio:x:17:
bin:x:1:daemon
cdrom:x:20:
console:x:21:
...
video:x:33:geeko
wheel:x:10:
www:x:8:
xok:x:41:
users:x:100:
```

文件中的每一行代表一个组记录，并包含组名、GID（组 ID）和组成员。例如，这是 /etc/group 文件中组 video 的条目：

```
video:x:33:geeko
```

第一个字段标识组（video）。第二个字段（x）是 Password 字段。第三个字段显示 GID（33），第四个字段将 geeko 标识为组 video 的成员。/etc/group 文件显示次要组成员身份，但不标识用户的首要组。

![](img/9129877170834ca9d5fdac5319bf5f12_300_0.png)

## 练习 9-1：使用 YaST 管理用户账户并从命令行获取用户和组信息

在本练习中，首先使用 YaST 用户管理模块创建并删除一个用户账户。请执行以下任务：

- 为用户 Tux Penguin 创建一个标记为 `tux` 的新账户，密码为 `novell`。
- 以新用户 `tux` 登录。
- 打开 `/etc/passwd` 文件并查找 `geeko` 和 `tux` 的条目。
- 以 `geeko` 登录并使用 YaST 删除 `tux` 的账户。

然后，从命令行获取一些用户和组的信息。请执行以下任务：

- 查找 `ftp`、`lp`、`nobody`、`root`、`www` 和 `users` 组的 GID（存储在 `/etc/groups` 中）。
- 查找 `ftp`、`lp`、`nobody`、`root`、`wwwrun` 和 `geeko` 用户的 UID（存储在 `/etc/passwd` 中）。
- 比较 `root` 和 `geeko` 用户的身份信息（使用 `id` 命令）。

![](img/9129877170834ca9d5fdac5319bf5f12_300_1.png)

## 完成此练习的详细步骤

- 第一部分：使用 YaST 创建新用户账户
- 第二部分：以新用户登录
- 第三部分：查看 passwd 文件
- 第四部分：以用户 geeko 登录并删除新用户账户
- 第五部分：从命令行获取用户和组信息

### 第一部分：使用 YaST 创建新用户账户

要使用 YaST 创建新用户账户，请执行以下操作：

- 1. 按以下方式启动 YaST：
  - a. 从 GNOME 桌面，选择 计算机 > 更多应用程序 > 系统 > YaST。
  - b. 在“需要密码”对话框中，输入密码 `n0v3ll`。
  - c. 选择 继续。
  YaST 控制中心出现。
- 2. 从 YaST 控制中心，选择 安全和用户 > 用户管理。
- 3. 通过选择 **添加** 添加新用户。
- 4. 输入以下信息：
  - *用户全名*—Tux Penguin
  - *用户名*—tux
  - *密码*—novell
  - *确认密码*—novell
- 5. 完成后，选择 **接受**。
- 6. 通过选择 **是** 确认密码警告。
- 7. 重复步骤 3 至 6 创建另一个用户，信息如下：
  - *用户全名*—Mary Novell
  - *用户名*—mary
  - *密码*—novell
  - *确认密码*—novell
- 8. 通过选择 **完成** 保存新设置。
- 9. 关闭 YaST 窗口。

### 第二部分：以新用户登录

要以新用户登录，请执行以下操作：

- 1. 从底部面板，通过选择 **计算机 > 注销** 注销。
- 2. 在注销对话框中，选择 **注销**。
  X Window 被重新启动，GUI 登录屏幕出现。
- 3. 在用户名字段中，输入 `tux`；然后按 **Enter**。
- 4. 在密码字段中，输入 `novell`；然后按 **Enter**。
- 5. 关闭或取消任何显示的对话框。

### 第三部分：查看 passwd 文件

要查看 passwd 文件，请执行以下操作：

- 1. 通过双击桌面上 tux 的主目录图标启动 Nautilus 文件管理器。
  tux 主目录的内容显示出来。
- 2. 浏览到 /home 目录。
  注意有 tux 和 geeko 用户的两个目录。
- 3. 浏览到 /etc 目录。
- 4. 通过双击打开 passwd 文件。
  注意文件末尾用户 tux 和 geeko 的条目。
- 5. 关闭所有窗口。

