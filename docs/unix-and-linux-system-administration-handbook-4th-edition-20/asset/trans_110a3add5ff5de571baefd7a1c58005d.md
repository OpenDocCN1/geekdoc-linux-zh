
adduser 在 `/etc/adduser.conf` 中配置，其中包含此类选项：

- 查找主目录的规则：通过组、用户名等。
- 新主目录的权限设置
- 系统用户和普通用户的 UID 和 GID 范围
- 为每个用户创建独立用户组的选项
- 磁盘配额（遗憾的是，是布尔值）
- 基于正则表达式的用户名和组名匹配

其他典型的 adduser 参数（如密码规则）被设置为执行常规密码认证的 PAM 模块的参数。（有关 PAM——可插拔认证模块的讨论，请参见第 908 页。）adduser 有一个兄弟命令 `addgroup` 以及两个表兄弟 `deluser` 和 `delgroup`。

## SUSE 上的 useradd

SUSE 的 `adduser` 默认不会创建新用户的主目录或启动文件。你必须使用 `-m` 标志来请求这些便利。（启动文件来自 `/etc/skel`）。`adduser` 也不会为新用户创建轮廓文件。

SUSE 的 `adduser` 也不创建用户特定的组；`passwd` 文件中的默认 GID 是由 `/etc/default/useradd` 中的变量设置的。新用户还会被 `GROUPS` 变量指定的组。默认情况下，这些组是 `video` 和 `dialout`，它们允许访问系统的帧缓冲区和拨号 IP 服务器 `pppd`。

为了弥补这些缺陷，SUSE 的 `useradd` 调用 `/usr/sbin/useradd.local`，这是一个 bash 脚本，你可以在其中添加任何所需的自定义内容。

SUSE 的 `/etc/login.defs` 文件控制以下类型的问题：

- 如果用户主目录不存在是否允许登录
- 登录尝试失败的容忍度（延迟和锁定）
- “今日消息”（message of the day）和 ttytype（终端）文件的位置
- 对 `csh` 和 `chfin` 使用的限制
- 密码老化
- 系统和用户 UID 及 GID 的范围
- 形成有效用户名和组名的规则
- 用户的 umask（默认为 022）

寄附于 useradd 和 userdel 命令的本地脚本

`login.defs` 的主页以及文件本身中的注释在描述各种参数及其含义方面都做得很好。

## Red Hat 上的 useradd

Red Hat Linux 上的 `useradd` 程序从 `/etc/login.defs` 获取配置参数，该文件处理了密码老化控制、加密算法、邮件轮廓文件以及 UID/GID 范围等问题。文件中的注释很好地解释了各种参数。

![](img/579efec8c67772f31ecf34844bbb71a2_241_0.png)

![](img/579efec8c67772f31ecf34844bbb71a2_241_1.png)

## 第7章 添加新用户

`useradd -D` 显示 useradd 用于新登录的默认值。这些默认值设置在 `/etc/default/useradd` 文件。在 Red Hat 上，新用户被放置在自己的独立组中。`passwd` 文件使用 "x" 作为密码所有者，`shadow` 文件使用 "!"，这是一个禁用登录并要求管理员为新用户设置密码的代码。MD5 加密是默认设置。新用户的主目录将填充来自 `/etc/skel` 的启动文件。

## Solaris 上的 useradd

在 Solaris 上，某些与登录和密码相关的默认参数内置在 `/etc/default/login` 和 `/etc/default/passwd` 中；另一些内置于 `useradd` 命令本身。`useradd -D` 显示多个参数的默认值。通过额外的标志，可以使用它来重置某些默认值。

`default/login` 和 `default/passwd` 的格式与 Linux 的 `user.defs` 文件类似，会忽略空行和以 `#` 开头的行，但 `NAME=value` 语法为变量分配了非注释值。

`/etc/default/passwd` 文件控制以下内容：

- 最小密码长度
- 密码老化
- 要求的密码复杂度
- 检查易破解的密码

`/etc/default/login` 控制此类问题：

- 时区
- 用户可以创建的文件大小限制
- root 是否仅允许在控制台登录
- 每个用户是否都需要密码
- 登录尝试失败的处理
- 用户的初始搜索路径
- 用户的 umask（默认为 022）

## HP-UX 上的 useradd

默认情况下，HP-UX 的 `adduser` 不创建新用户的主目录或启动文件。你必须使用 `-m` 标志来请求这些便利。（启动文件来自 `/etc/skel`）。`adduser` 也不会为新用户创建轮廓文件。

... 

`/etc/security/login.cfg` 文件包含了控制错误登录的参数（在登录提示和密码提示之间插入的延迟、禁用账户前的错误登录次数、允许账户存在的时间、何时恢复账户等）。

遗憾的是，这仅仅是控制新用户登录的配置之一。`/etc/security/login.cfg` 文件包含了控制错误登录的参数（在登录提示和密码提示之间插入的延迟、禁用账户前的错误登录次数、允许账户存在的时间、何时恢复账户等）。
