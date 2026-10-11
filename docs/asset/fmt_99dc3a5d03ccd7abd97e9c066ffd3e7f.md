
# 注意

最佳方法是通过修改配置文件并重启从禁用（`disabled`）切换到强制模式。通过 `setenforce` 命令从禁用切换到强制可能会由于标签不正确导致系统挂起。

要禁用 SELinux，必须编辑 SELinux 配置文件。要保持当前的运行模式设置不变，必须编辑配置文件。更改 SELinux 运行模式的首选方法是修改配置文件然后重启系统。当从禁用切换到强制或允许模式时，SELinux 会在重启后自动重新标记文件系统。这意味着 SELinux 将更改具有错误安全上下文的文件，这可能会导致问题。重新标记过程可能需要很长时间，因为它会检查每个文件的上下文。在重启后进行重新标记期间，你会收到以下消息：

> 警告 -- 需要重新标记 SELinux 目标策略。重新标记可能需要长时间，取决于文件系统的大小和硬盘的速度。

修改 `/etc/selinux/config` 文件中的运行模式，将 `selinux=` 行更改为以下之一：

- `disabled`
- `enforcing`
- `permissive`

后续 SELinux 配置示例显示模式已设置为允许（`permissive`）。现在当系统重启时，模式将被更改。

## 第五部分：学习安全技术

```
# cat /etc/selinux/config
# 此文件控制系统中 SELinux 的状态。
# SELINUX= 取以下三个值之一：
- enforcing - SELinux 安全策略已执行。
- permissive - SELinux 打印警告而不是执行。
- disabled - SELinux 完全禁用。
SELINUX=permissive
```

主要的 SELinux 配置文件不仅包含运行模式设置，它还指定了策略类型，这将决定对象可以访问的内容。

### 设置 SELinux 策略类型

你选择的策略类型将决定 SELinux 执行 TE、MLS 还是基础包。默认策略类型设置为目标（`targeted`）。要更改默认策略类型，编辑 `/etc/selinux/config` 文件。将 `SELinuxTYPE=` 行更改为以下之一：

- `targeted`
- `mls`
- `minimum`

如果你将 SELinux 类型设置为 `mls` 或 `minimum`，你需要先安装相应的策略包。通过输入命令检查：`yum list selinux-policy-mls` 或 `yum list selinux-policy-minimum`。

> 注意
在 Ubuntu 上检查 SELinux 策略包使用命令 `sudo apt-cache`。

后续 SELinux 配置示例显示类型已设置为 `mls`，当系统重启时，策略类型将更改。

```
# cat /etc/selinux/config
# 此文件控制系统中 SELinux 的状态。
# SELINUXTYPE= 使用的类型。可能的值：
- targeted - 仅保护目标进程。
- strict - 完整的 SELinux 保护。
SELINUXTYPE=mls
```

# 第 24 章：使用 SELinux 增强 Linux 安全

> 注意
不要被 SELinux 配置文件中的过时注释误导。在较新的 Linux 发行版中，你无法将 `SELINUXTYPE` 设置 `strict`。如果你这样做，系统将在下次重启时挂起，你需要使用 `grub` 命令修复问题。`strict` 策略类型现在是目标类型的一部分。

## 管理 SELinux 安全上下文

SELinux 安全上下文允许 SELinux 对访问对象的实体执行策略。你的 Linux 系统已分配了安全上下文。

查看当前的 SELinux 文件和进程安全上下文，使用 `secon` 命令。表 24.1 列出了 `secon` 命令的选项。

| 选项 | 描述 |
| :--- | :--- |
| `-u` | 使用此选项显示安全上下文的用户。 |
| `-r` | 使用此选项显示安全上下文的角色。 |
| `-t` | 使用此选项显示安全上下文的类型。 |
| `-s` | 使用此选项显示安全上下文的敏感级别。 |
| `-c` | 使用此选项显示安全上下文的权限级别。 |
| `-m` | 使用此选项以 MLS 范围显示安全上下文的敏感性和权限级别。 |

如果你在不指定参数的情况下使用 `secon` 命令，它将显示当前进程的安全上下文。要查看另一个进程的安全上下文，使用 `-p` 选项。后续示例显示了如何使用 `secon` 查看当前进程和 init 进程的安全上下文。

```
# secon -urt
user: unconfined_u
role: unconfined_u
# secon -urt -p
user: system_u
role: system_r
type: init_t
```

## 第五部分：学习安全技术

查看当前的 SELinux 文件和进程安全上下文，使用 `secon` 命令。表 24.1 列出了 `secon` 命令的选项。

| 选项 | 描述 |
| :--- | :--- |
| `-u` | 使用此选项显示安全上下文的用户。 |
| `-r` | 使用此选项显示安全上下文的角色。 |
| `-t` | 使用此选项显示安全上下文的类型。 |
| `-s` | 使用此选项显示安全上下文的敏感级别。 |
| `-c` | 使用此选项显示安全上下文的权限级别。 |
| `-m` | 使用此选项以 MLS 范围显示安全上下文的敏感性和权限级别。 |

查看当前的 SELinux 文件和进程安全上下文，使用 `secon` 命令。表 24.1 列出了 `secon` 命令的选项。查看文件的安全上下文，使用 `secon` 命令。

```
# secon -urt
user: unconfined_u
role: unconfined_u
# secon -urt -p
user: system_u
role: system_r
type: init_t
```

## 管理 SELinux 安全上下文

SELinux 安全上下文允许 SELinux 对访问对象的实体执行策略规则。你的 Linux 系统已分配了安全上下文。

# 第五部分：学习 Linux 安全技术

## 管理进程安全上下文

进程的定义是一个运行中的程序。当你在 Linux 系统上运行程序或启动服务时，每个程序都会被赋予一个进程 ID（参见第 6 章）。在启用了 SELinux 的系统中，进程还会被赋予一个安全上下文。

进程获取其安全上下文取决于启动它的进程。请记住 `init` 是所有进程的“母进程”（参见第 15 章）。因此，许多守护进程和进程是由 `init` 启动的。不是由 `init` 启动的进程会被分配一个新的安全上下文。例如，当 `init` 启动 `apache` 守护进程时，它会被分配一个（也称为域）`httpd_t` 上下文。分配的上下文是由专门为该守护进程编写的 SELinux 策略处理的。如果某个进程没有策略，则它会被分配一个默认类型 `unconfined_t`。

对于由用户（父进程）运行的程序或应用程序，新进程（子进程）会继承用户的安全上下文。当然，这只有在用户被允许运行该程序时才会发生。进程也可以运行程序。子进程继承其父进程的安全上下文。因此，子进程运行在相同的域中。

所以，进程的安全上下文在程序运行之前设置，并取决于是谁启动了它。你可以使用以下命令来更改运行程序时的安全上下文：

- `runoption` -- 运行你使用的程序，通过该程序来确定用户、角色和（也称为域）。
- `sandbox` -- 在在严格控制的域（也称为沙箱）中运行程序。

使用 `running` 可能会导致一些问题，因此请谨慎使用。然而 `sandbox` 提供了大量的保护。它允许在你的 Linux 系统上测试新程序时具有很高的灵活性。

## 管理 SELinux 策略规则包

策略规则是 SELinux 用于判断主体是否有权访问某个对象的规则。这些规则被分组为包（也称为模块），并与 SELinux 一起安装。查看系统中模块的简单方法是使用 `semodule -1` 命令。它将列出所有策略模块及其当前版本号。`semodule -1` 命令的示例在此：

```
# semodule -1
abrt 1.2.0
accountsd 1.0.0
acct 1.5.0
...
xserver 3.5.6
zabbix 1.3.1
zarafa 1.0.0
zebra 1.12.0
zoosremote 1.1.0
```
