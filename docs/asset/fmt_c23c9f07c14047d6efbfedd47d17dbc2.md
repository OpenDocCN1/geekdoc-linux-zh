
| HP-UX | `useradd`<br>`smh` | `/etc/default/useradd`<br>`/etc/default/security` | GUI 工具，也称为 `sam` |

| AIX | `useradd`<br>`mkuser`<br>`chuser`<br>`rmuser`<br>SMIT | `/etc/security/user`<br>`/etc/security/login.cfg`<br>`/etc/security/mkuser.default` | 由 `useradd` 调用<br>由 `usermod` 调用<br>由 `userdel` 调用<br>GUI 工具 |

a. 在较旧的 AIX 系统中，此文件位于 `/usr/lib/security`。

### Ubuntu 上的 useradd

Ubuntu 提供了两种添加用户的方式：`adduser` 和 `useradd`。`adduser` 是 `useradd` 的一个 Perl 包装器，使用起来更方便一些（会创建主目录、复制启动文件等）。

`adduser` 的配置位于 `/etc/adduser.conf`，其中包括如下选项：

- 定位主目录的规则：按组、按用户名等。
- 新主目录的权限设置
- 系统用户和普通用户的 UID 和 GID 范围
- 为每个用户创建独立组的选项
- 磁盘配额（遗憾的是仅支持布尔值）
- 基于正则表达式的用户名和组名匹配

其他典型的 `useradd` 参数，例如密码规则，会作为参数传递给执行常规密码认证的 PAM 模块。（有关 PAM（即可插拔认证模块）的讨论，请参见第 908 页。）`adduser` 有一个孪生命令 `addgroup`，还有近亲 `deluser` 和 `delgroup`。

### SUSE 上的 useradd

![](img/14d78e3cecac4581d37024baf1e94cca_241_0.png)

SUSE 的 `useradd` 默认不会创建新用户的主目录，也不会复制启动文件。你必须使用 `-m` 选项才能获得这些便利功能。（启动文件来自 `/etc/skel`。）`useradd` 也不会为新用户创建邮件假脱机文件。

SUSE 的 `useradd` 也不会创建用户专属组；`passwd` 文件中的默认 GID 由 `/etc/default/useradd` 中的 `GROUP` 变量设置。新用户还会被添加到 `GROUPS` 变量指定的组中。默认情况下，这些组是 video 和 dialout，它们允许访问系统帧缓冲区和拨号 IP 软件 `pppd`。

为了弥补这些不足，SUSE 的 `useradd` 会调用 `/usr/sbin/useradd.local`，这是一个 `bash` 脚本，你可以向其中添加任何你希望的自定义设置。

SUSE 上的 `/etc/login.defs` 文件控制以下类型的问题：

- 如果用户的主目录不存在，是否允许登录
- 对登录失败尝试的容忍程度（延迟和锁定）
- “每日消息”和 `ttype`（终端类型）文件的位置
- 对使用 `chsh` 和 `chfn` 的限制
- 密码时效
- 系统及用户的 UID 和 GID 范围
- 构成有效用户名和组名的规则
- 用户的 `umasks`（默认为 022）
- 依附于 `useradd` 和 `userdel` 命令的本地脚本

`login.defs` 的手册页和文件本身的注释都很好地描述了各种参数及其含义。

### Red Hat 上的 useradd

![](img/14d78e3cecac4581d37024baf1e94cca_241_1.png)

Red Hat Enterprise Linux 上的 `useradd` 程序从 `/etc/login.defs` 获取其配置参数，该文件涵盖密码时效控制、加密算法、邮件假脱机文件以及 UID/GID 范围等问题。文件中的注释很好地解释了各种参数。

`useradd -D` 显示 `useradd` 为新登录所使用的默认值。 这些默认值设置在文件 `/etc/default/useradd` 中。 在 Red Hat 上，新用户会被放置在其自己的独立组中。 `passwd` 文件条目使用 "x" 作为密码占位符，而 `shadow` 文件使用 "!"，该代码会禁用登录并要求系统管理员为新用户设置密码。 MD5 加密是默认的。 新用户的主目录会从 `/etc/skel` 填充启动文件。

### Solaris 上的 useradd

在 Solaris 上，与登录和密码相关的某些默认参数存储在 `/etc/default/login` 和 `/etc/default/passwd` 中；其他参数则内置于 `useradd` 命令本身。 `useradd -D` 显示多个参数的默认值。 使用附加标志，它可以用于重置其中一些默认值。

`default/login` 和 `default/passwd` 文件的格式与 Linux 的 `login.defs` 文件类似，即空白行和以 # 开头的行会被忽略，并且每一行非注释行都会为变量分配一个值。 然而，其语法是

```
NAME=value
```

而不是

```
NAME <white-space> value
```

`/etc/default/passwd` 文件控制以下内容：

- 最小密码长度
- 密码老化
- 所需的密码复杂度
- 检查可破解的密码

`/etc/default/login` 控制诸如以下问题：

- 时区
- 用户可创建文件的大小限制
- root 是否只能在控制台上登录
- 是否每个用户都需要密码
- 失败登录尝试的处理
- 用户的初始搜索路径
- 用户的默认 umask（默认为 022）
- 是否通过 syslog 记录 root 和失败登录

文件 `/etc/security/policy.conf` 和 `/etc/security/crypt.conf` 确定可用于密码的加密算法。

### HP-UX 上的 useradd

默认情况下，HP-UX 的 `useradd` 命令不会创建主目录或将用户放入独立组。 然而，使用 `-m` 选项，`useradd` 会创建主目录并从 `/etc/skel` 用启动文件填充它们。

`useradd` 的配置参数设置在文件 `/etc/default/useradd` 和 `/etc/default/security` 中，其中 `useradd` 文件采用 Linux 风格的 `NAME <white-space> value` 格式，而 `security` 使用 Solaris `NAME=value` 风格。 哎呀，HP，拿定主意吧！ 语法应可从每个文件中的其他条目清楚看出，但如果使用错误的形式，你尝试设置的变量将被静默忽略。 不会生成语法错误消息。

`/etc/default/useradd` 文件控制诸如以下选项：

- 默认组和 shell
- 主目录树的根
- 账户过期
- 是否创建主目录
- 是否允许重复 UID

文件 `/etc/default/security` 包含额外的配置参数，其中一些与用户管理相关：

- 是否允许在缺少主目录的情况下登录
- 是否允许空密码
- 最小密码长度
- 失败登录尝试的处理
- 非活跃账户的处理
- 新用户的默认 umask（默认 027）

此文件中的变量名称很长且选择得当，可以准确解释每个变量控制的内容。

### AIX 上的 useradd

AIX 的 `useradd` 实际上只是其原生 AIX 等价物 `mkuser` 的 `ksh` 包装器。 同样，`usermod` 调用 `chuser`，而 `userdel` 调用 `rmuser`。 这些命令的手册页在其原始名称和符合世界其他地区规范的名称下都存在。

配置文件控制登录和密码的众多方面，并保存在 `/etc/security` 目录中。 有三个相关文件：`login.cfg`、`user` 和 `mkuser.default`。 前两个使用 * 作为注释字符；第三个没有注释。 这些文件按以下形式的段落组织：

```
label:
    attribute = value
    next-attribute = value

next-label:
    attribute = value
```

例如，在 `/etc/security/user` 文件中，标签是用户名（或单词 default）； 可能的属性显示在下一页的表 7.5 中。

### 表 7.5 /etc/security/user 中的用户账户选项（AIX）

| 选项 | 类型 | 含义 |

|---|---|---|

| account_locked | Boolean | 如果为 true 则阻止登录 |
