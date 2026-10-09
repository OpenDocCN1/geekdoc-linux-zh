
## 表 10-2 图形化配置工具

| 工具 | 功能 |
| :--- | :--- |
| **authconfig** / **authconfig-tui** | **authconfig-tui** 实用程序显示伪图形化的身份验证配置窗口。“用户信息”列允许你配置用户帐户以缓存信息，并使用 LDAP、NIS、IPA 或 Winbind 支持。“身份验证”列允许你指定系统如何对用户进行身份验证，具体取决于你配置用户帐户的方式。对于纯文本（可脚本化）界面，请使用 **authconfig**。 |
| **firewall-config** | 显示防火墙配置窗口（第 900 页）。 |
| **system-config-bind** | 显示 BIND 配置 GUI 窗口（**system-config-bind** 软件包；第 867 页）。 |
| **system-config-httpd** | 显示 HTTP 服务器配置窗口（**system-config-httpd** 软件包）。 |
| **system-config-kickstart** | 显示 Kickstart 配置器窗口，允许你创建 Kickstart 脚本（**system-config-kickstart** 软件包；第 83 页）。 |
| **system-config-nfs** | 显示 NFS 服务器配置窗口（**system-config-nfs** 软件包；第 812 页）。 |
| **system-config-printer** | 显示打印设置窗口，允许你设置打印机并编辑打印机配置（第 558 页）。 |
| **system-config-rootpassword** | 显示根密码窗口，允许你更改 **root** 密码。使用 **root** 权限工作时，你也可以从命令行使用 **passwd**（第 137 页）来更改 **root** 密码（**system-config-rootpassword** 软件包）。 |
| **system-config-samba** | 显示 Samba 服务器配置窗口，可以帮助你配置 Samba（**system-config-samba** 软件包；第 837 页）。 |
| **system-config-selinux** | 显示 SELinux 管理窗口，用于控制 SELinux（**policycoreutils-gui** 软件包；第 475 页）。 |
| **system-config-services** | 显示服务配置窗口，允许你指定哪些守护程序（服务）在每个运行级别中运行（**system-config-services** 软件包；第 447 页）。 |
| **system-config-users** | 显示用户管理器窗口，允许你处理用户和组（第 598 页）。 |
| **system-switch-mail** | 显示 system-switch-mail 伪图形窗口，允许你在 sendmail（第 739 页）和 Postfix（第 742 页）MTA 之间进行选择，前提是系统中同时安装了这两个软件包（**system-switch-mail** 软件包）。 |

## SELinux

传统 Linux 安全机制，称为 DAC（自主访问控制），基于用户和组。ACL（第 198 页）实现了 DAC，并可以对哪些用户和进程可以访问文件以及如何访问它们进行细粒度控制。细粒度访问控制在服务器上尤为重要，因为它们通常包含需要 root 权限才能运行的程序。问题在于，在 DAC 下，文件所有者控制对该文件的权限，这并不总是理想的。

SELinux（安全增强型 Linux），由 NSA（美国国家安全局）开发，在 Linux 内核中实现了 MAC（强制访问控制）。由系统管理员控制的 MAC 执行限制用户或程序行为的安全策略。它定义了一个安全策略，控制某些或所有对象（如文件、设备、套接字和端口）以及某些或所有主体（如进程）。使用 SELinux，你可以遵循最小权限原则（第 423 页），仅授予进程执行功能所需的那些权限。用户被分配决定其主要功能的角色。SELinux 角色在概念上类似于组，但在 SELinux 中，用户必须主动在允许的角色之间切换。MAC 是限制来自用户错误、软件缺陷和恶意用户的安全威胁的重要工具。内核在检查 DAC 规则后检查 MAC 规则；两者均可拒绝访问。

### DAC 与 MAC：谁拥有最终决定权？

DAC（自主访问控制）和 MAC（强制访问控制）在控制访问方面都行之有效。区别在于，DAC 由拥有文件的用户控制，因此比由系统管理员控制的 MAC 更容易被滥用。内核在检查 DAC 规则后检查 MAC 规则；两者均可拒绝访问。

- SELinux 可以处于三种模式（状态）之一：
  - **强制/激活**—默认状态，在此状态下执行 SELinux 安全策略。用户或程序只能执行安全策略所允许的操作。
  - **宽容/警告**—诊断状态，在此状态下 SELinux 向日志发送警告消息，但不执行安全策略。你可以使用该日志来构建符合你要求的安全策略。
  - **禁用**—SELinux 不执行安全策略，也不发出警告，因为未加载策略。

在宽容或强制状态下运行 SELinux 据估计会使系统性能下降 0 到 7 个百分点，具体取决于调优和用法。如果你不确定是否要使用 SELinux，选择宽容状态可以让你稍后轻松切换到禁用或强制状态。

策略：SELinux 实现以下策略之一：

- **Targeted**—仅对某些（特定）进程应用 SELinux MAC 控制（默认）。
- **MLS**—服务器的多级安全保护。
- **Minimum**—仅保护虚拟机。

本节讨论 targeted 策略。在此策略下，没有指定策略的守护程序和系统进程由传统 Linux DAC 控制。

### SELinux 是否导致了问题？

**提示：** 如果服务器或其他系统软件在设置后无法工作，不正确的 SELinux 配置可能是问题的原因。许多服务包含与 SELinux 安全使用相关的说明（例如 smb.conf），或者在 selinux-policy-devel 软件包中有 man 页面（例如，安装该软件包后，执行命令 `man 8 httpd_selinux`）。如果你怀疑需要调整 SELinux 策略，也可以检查 /var/log/audit/audit.log。

### 更多信息

- Web NSA: www.nsa.gov/research/selinux/docs.shtml
- Fedora SELinux Wiki: fedoraproject.org/wiki/SELinux
- SELinux 项目: selinuxproject.org
- SELinux HOWTO: wiki.centos.org/HowTos/SELinux
- 关于禁用 SELinux 的警告: stopdisablingselinux.com
- Fedora SELinux 邮件列表: admin.fedoraproject.org/mailman/listinfo/selinux

### 关闭 SELinux

**提示：** 禁用 SELinux 有两种方法。你可以修改 /etc/selinux/config 文件以包含 SELINUX=disabled 行并重新启动系统，或者你可以使用 system-config-selinux（如第 475 页所述）。但是，请参阅 stopdisablingselinux.com。

如果你将来可能会想要启用 SELinux，将 SELinux 设置为宽容模式比禁用它是更好的选择。这种策略允许你在决定使用它时更快地开启 SELinux。

## config: SELinux 配置文件

`/etc/selinux/config` 文件（在 `/etc/sysconfig/selinux` 处有一个链接）控制本地系统上 SELinux 的状态。虽然你可以修改此文件，但使用 `system-config-selinux`（下一页）可能更直观。在以下示例中，策略设置为 targeted，但由于 SELinux 被禁用，该设置没有影响：

```
$ cat /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=disabled
# SELINUXTYPE= can take one of these two values:
#     targeted - Targeted processes are protected.
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

要将 SELinux 设置为强制模式，请将包含 **SELINUX** 赋值的行更改为 `SELINUX=enforcing`。同样，你可以通过设置 `SELINUXTYPE` 来更改策略。更改在系统重启时生效。

### 如果你将来会使用 SELinux

> 如果你将来会使用 SELinux 但当前不使用，请在安装 Linux 时将其打开，并在将策略设置为你最终将使用的策略的情况下以宽容状态运行它。宽容状态将所需的扩展信息写入 inode，但它不会阻止你在系统上执行任何操作。

如果在禁用后重新启用 SELinux，当系统重启时，SELinux 必须向文件系统中的文件添加扩展属性。此过程在大型文件系统中可能需要很长时间。如果你永远不使用 SELinux，请禁用它。

## getenforce, setenforce, 和 sestatus: 使用 SELinux

`getenforce` 和 `setenforce` 实用程序报告并临时设置 SELinux 状态。`sestatus` 实用程序显示本地系统上 SELinux 的摘要：

```
# getenforce
Enforcing

# setenforce permissive

# sestatus
SELinux status:              enabled
SELinux fs mount:            /sys/fs/selinux
SELinux root directory:      /etc/selinux
Loaded policy name:          targeted
Current mode:                permissive
```

