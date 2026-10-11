
![](/f850b93901bbb4c267df1b99fb6de52_162_0.png)

图 8-16: 从 KDE 开始菜单启动 KDE System Guard

KDE System Guard 像 GNOME 系统监器一样提供了系统进程及其状态的定期更新。与 GNOME 系统监器不同，无法从图形应用程序修改刷新间隔（尽管有一个刷新按钮）。与 GNOME 系统监器不同，无法指定发送到进程的信号。唯一的选项是杀死（使用 `TERM` 信号）。KDE System Guard 界面如图 8-17 所示。

# SUSE Linux GNU: 安装与配置 - KDE Guard

![](/f850b93901bbb4c267df1b99fb6de52_163_0.png)

动手！

## B-2： GUI 工具

### 问题解答

- 1 如何启动 GNOME 系统监器？

进入开始菜单。选择程序、系统、系统监器。

- 2 描述使用 KDE System Guard 杀死进程的步骤。

如有，点击刷新按钮获取当前显示。选择要杀死的进程。点击杀死按钮。

- 3 描述使用 GNOME 系统监器杀死进程的步骤。

在目标进程上点击右键。选择 Kill nicely 发送 `TERM` 信号，选择 Kill now 发送 `SIGKILL` 信号，或选择 select> 选择特定信号。

- 4 描述使用 Konqueror 更改权限掩码的步骤。

5 在 Nautilus 程序上点击鼠标右键并选择 Renice。当弹出窗口出现时，将滑块移动到 -5。发生了什么？

错误信息“Only root can set a negative priority.”（只有 root 可以设置负优先级。）

6 尝试杀死进程（右键点击进程并选择“Kill nicely (SIGTERM)”）。发生了什么？

进程被杀掉了。

为什么？

因为是你启动了该进程，所以不需要特殊权限即可杀死它。

# 第 9 单元

基础系统管理

单元时长：90 分钟

完成本单元，你将学会如何：

- A 从命令行（shell）和图形界面（GUI）创建并管理用户账户及组。
- B 从命令行和图形界面（GUI）管理打印机。
- C 挂载和使用可移动介质。
- D 监控重要的系统资源，如磁盘空间和网络。

# 主题 A：创建和管理用户账户和组

## 解释

在创建和管理用户账户和组时，你有多个选项。可以使用命令行（shell）工具和 GUI 工具来创建和管理用户账户和组。你也可以直接编辑控制用户账户和组的配置文件。

## 用户账户

为了访问系统和系统资源，你必须登录用户账户。每个 Linux 系统都至少有一个登录账户：`root`。在笔记本电脑或桌面工作站等单用户系统上，使用 `root` 进行所有用户访问是很有诱惑力的。这是一个非常糟糕的主意。作为 `root` 用户，不小心损坏系统实在太容易了。

每个账户在主配置文件 `/etc/passwd` 中至少有一条条目。在现代 Linux 发行版中，默认安装了 shadow 工具包，这会创建一个第二个配置文件 `/etc/shadow`。

无论是使用 GUI 工具、shell 实用程序还是直接编辑配置文件，创建用户账户都需要创建一组最少数量的用户属性。

## 理解 Linux 配置文件

在 Linux 上运行的每个程序都可以通过编辑文本文件来完成配置。这种灵活性允许管理员使用文本编辑器（如 `vi`、`pico` 或 `emacs`）远程更改系统的配置。如果你熟悉 Windows 环境，配置文件大致对应于 Windows 系统注册表，但它们更容易理解、访问和编辑。

在 Linux 中修改配置文件的过程如下：

- 使用文本编辑器打开配置文件。
- 对配置文件进行相应的修改。
- 保存并退出文件。
- 重启守护进程以读取更改后的配置文件并加载新配置。

虽然这些步骤非常简单，但复杂之处在于知道需要修改哪些配置文件、理解配置文件各项项的语法和含义，以及知道哪些守护进程需要重启。

## 控制用户账户的配置文件

在不支持 shadow 密码的系统中，所有用户账户属性都存储在 `/etc/passwd` 文件中。在支持 shadow 密码的系统中，属性分在 `/etc/passwd` 和 `/etc/shadow` 之间。如上述，当前的 Linux 发行版默认安装了 shadow 支持。存储在这些文件中本质的用户账户属性包括：

## 基础系统管理

| 属性 |  |
|--- |--- |
| `username` | 唯一的字母数字标识符 |
| `password` | 字母数字密码 |
| `UID` | 标识用户的唯一整数 |
| `GID` | 标识用户账户所属组的唯一整数。一个用户可能属于多个组。 |
| `directory` | 默认登录目录。登录时并非强制要求。 |
| `shell` | 用户登录时启动的默认 shell |

`/etc/passwd`

`/etc/passwd` 文件的格式为：

```
username:password:UID:GID:GECOS:directory:shell
```

上表用户属性表描述了除一个外外的所有字段。`GECOS` 字段是一个描述字段。按照习惯，它通常包含用户的全名。

以下是一个新安装的 Red Hat 系统的 `/etc/passwd` 示例：

```
root:x:0:0:/root:/bin/bash
daemon:x:1:1::/bin/bin:x:2:2:daemon:/sbin
adm:x:3:4:/var/adm
lpd:x:4:7:/var/spool/lpd
sync:x:5:0:sync:/sbin/bin/sync
shutdown:x:6:11:shutdown:/sbin/bin/shutdown
halt:x:7:0:halt:/sbin/halt
mail:x:8:12:mail:/var/spool/mail
news:x:9:13:news:/var/spool/news
uucp:x:10:14:uucp:/var/spool/uucp
operator:x:11:0:operator:/usr/games
games:x:12:100:games:/usr/lib/gopher
gftp:x:14:30:FTP User:/home/ftp:
man:x:15:15:Manual Owner::/
madomordo:x:16:16:Majordo:::/bin/false
postgres:x:17:17:Postgres User:/home/postgres:/bin/bash
mysql:x:18:13:MySQL User:/var/lib/mysql:/bin/false
bind:x:19:19:DNS Server::/bin/false
httpd:x:55:54:HTTP Server::/bin/false
nobody:x:65534:65534:Nobody::/bin/false
johng:x:500:100:Johnny B Goode:/home/johng:/bin/bash
```

# SAIR Linux GNU: 安装与配置

## `/etc/shadow`

以下是一个新安装的 Red Hat 系统的 `/etc/passwd` 示例（注：原文此处可能笔误，实际应为 shadow 内容）：

```
root:hgoJby2yF:s:11386:0::7::
bin*:10547:0::7::
demon*:10547:0::7::
adm*:10547:0::7::
lp*:10547:0::7::
sync*:10547:0::7::
shutdown*:10547:0::7::
halt*:10547:0::7::
mail*:10547:0::7::
news*:10547:0::7::
uucp*:10547:0::7::
operator*:10547:0::7::
games*:10547:0::7::
gopher*:10547:0::7::
man*:10547:0::7::
madomordo*:10547:0::7::
postgres*:10547:0::7::
mysql*:10547:0::7::
bind*:10547:0::7::
httpd*:10547:0::7::
nobody*:10547:0::7::
johng:x:500:100:Johnny B Goode:/home/johng:/bin/bash
```

## 用户组

与其手动配置许多用户，通过组来管理安全更为简单。组允许系统管理员通过限制组访问来控制文件和目录。例如，在学校里，老师和管理员可以使用同一台计算机系统。而学生不应该访问这些记录。

将学生分配到一个组，老师分配到另一个组，可以保护敏感材料。

## 组文件

组通过存储在 `/etc/group` 文件中的信息组织。每行一个组项，每行由冒号分隔的四个字段：

```
group_name:password:GID:users
```

`users`字段是组内用户的逗号分隔列表。
