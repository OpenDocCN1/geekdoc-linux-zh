

## Linux 安全模块

为了解决此问题，Linux 安全模块（LSM）应运而生。在启用 LSM 的系统中，进程（Subject）仅能访问策略中定义的文件（Objects）。此策略由系统管理员设置并由操作系统内核强制执行；文件访问不再由用户自行决定。

根据内核文档，LSM 内核补丁提供了一个支持安全模块的通用内核框架。具体来说，LSM 框架主要专注于支持访问控制模块，尽管未来的开发可能会解决其他安全需求，例如审计。该框架本身并不提供任何额外的安全性；它仅仅是提供支持安全模块的基础设施。

最著名的基于 LSM 的 Linux 工具是 Security Enhanced Linux（SELinux，用于 RHEL）和 AppArmor（用于 SLES）。使用这些工具，你可以以高粒度定义哪个进程可以以何种权限访问哪个文件。这些规则由内核强制执行，并且独立于进程的 UID 和文件系统中设置的权限。

要定义这些策略，你必须对相关应用程序及其工作方式有透彻的理解。

这种访问控制也被称为强制访问控制（MAC）。

## 强制访问控制

与自由访问控制（Discretionary Access Control）相反，在自由访问控制中，用户决定授予其创建的对象何种权限；而在强制访问控制中，权限是根据策略由管理员设置的。

以下内容将描述：

- SELinux
- AppArmor

## SELinux

SELinux 中的强制访问控制可以通过两种方式实现：*类型强制（Type Enforcement, TE）* 和 *基于角色的访问控制（Role Based Access Control, RBAC）*。要了解有关这些的更多信息，我们推荐访问美国国家安全局的网站 <http://www.nsa.gov/selinux/>。NSA 发起了 SELinux 项目。

在 RHEL 系统上，SELinux 的主要配置文件存储在目录 `/etc/selinux/` 中。

SELinux 通常由 init 进程在启动时激活。可以通过输入启动参数 `selinux=0` 或将 `/etc/selinux/config` 中的 SELINUX 参数设置为 `disabled` 来禁用启动时的激活。

有两种类型的 SELinux 策略：*targeted*（仅保护特定的网络守护进程）和 *strict*（完整的 SELinux 保护）。内核中同一时间只能激活一种类型的策略。激活 SELinux 时使用哪种策略由文件 `/etc/selinux/config` 中的参数 **SELINUXTYPE** 定义。

策略是使用 m4 宏语言创建的。源代码保存在 `/etc/selinux/<POLICY-NAME>/src/policy/` 中，而二进制文件可以在 `/etc/selinux/<POLICY-NAME>/policy/` 中找到。

策略由 Security-Server 管理，Security-Server 是 SELinux 的核心组件。来自 Security-Server 的消息存储在 /var/log/messages 中。

使用命令 **ls -Z** 可以查看用于某个文件的安全上下文。将 **-Z** 选项与 **ps** 命令结合使用可以显示运行中进程的安全上下文。

命令 **setenforce** 用于将 SELinux 从“开启”切换到“仅警告”以及反向操作。**system-config-securitylevel** 是一个允许更改 SELinux 配置参数的工具。命令 **selinuxenabed** 可用于检查运行中系统上 SELinux 的状态。返回代码 0 表示 SELinux 已启用。

## AppArmor

AppArmor 内核模块（apparmor 和 aamatch_pctre）挂钩到内核的 Linux 安全模块框架中。

**/etc/apparmor.d/** 中的**配置文件（Profiles）**用于配置哪个应用程序可以访问和执行哪些文件。

AppArmor 必须在受其控制的启动之前激活。在 AppArmor 激活时已经运行的应用程序不受 AppArmor 控制，即使为它们创建了配置文件。因此，AppArmor 由 **/etc/init.d/boot.apparmor** 在启动过程的早期被激活。

在 SUSE Linux Enterprise Server 10 的默认安装中，AppArmor 正在使用 Novell 提供的一组配置文件积极保护多个服务。使用提供的 YaST 模块或命令行工具，你可以轻松地将这些配置调整以满足你的需求，并为你想要保护的额外应用程序创建新的配置文件。

作为一个一般规则，你应该限制授予特权的程序，即，访问使用者不具备权限的资源的程序：

- 网络代理——具有开放网络端口的程序
- Cron 作业
- Web 应用程序

> 在 AppArmor 文档的某些部分，你会找到 AppArmor 的前身名称，Subdomain。

可以使用命令 rcaparmor start 和 stop 分别开启和关闭 AppArmor 保护。单个应用程序可以使用同名命令在 enforce（AppArmor 限制应用程序可以做什么）和 complain（仅创建日志条目）模式之间切换。

## 目标 2 创建和管理 AppArmor 配置文件

SUSE Linux Enterprise Server 10 附带了针对各种应用程序（如 named, ntpd, nscd 等）的 AppArmor 配置文件。

配置文件包含在 */etc/apparmor.d/* 中。配置文件的文件名代表应用程序的文件名（包括路径），其中“/”被替换为“:”。/usr/sbin/squid 的配置文件将包含在 /etc/apparmor.d/usr.sbin.squid 中。

一个配置文件可以使用 **#include** 语句包含其他文件。目录 */etc/apparmor/abstractions/* 包含几个旨在根据由 AppArmor 保护的程序类型而被包含在配置文件中的文件。有针对所有程序都应可读或可写的文件（base）、与名称服务相关的文件（如 */etc/passwd*）（nameservice）、与控制台操作相关的文件（console）等的抽象定义。

配置文件是纯文本文件，因此可以使用任何文本编辑器创建和修改它们。然而，命令行工具以及 YaST 模块大大简化了创建配置文件的过程。

除了 */etc/apparmor.d/* 中的活动配置文件外，在 */etc/apparmor/profiles/extras/* 中已经预先准备了几个配置文件，你可以根据你的需求进行定制，并将它们复制到 */etc/apparmor.d/* 中以激活它们。

为了成功管理 AppArmor，你需要：

- 理解配置文件和规则
- 使用 YaST 管理 AppArmor 配置文件
- 使用命令行工具管理 AppArmor 配置文件

### 理解配置文件和规则

Novell AppArmor 配置文件包含两种类型的 AppArmor 规则：路径条目和权限条目。路径条目指定进程可以在文件系统中访问什么。默认情况下，AppArmor 限制授予进程的权限（参见 man apparmor）。权限条目用于指定授予进程的特定 POSIX 权限（man 7 capabilities），覆盖默认限制。

其他包含 AppArmor 规则的文件可以通过 **#include** 语句引入。

作为例子，让我们看一下 /sbin/klogd（内核日志守护进程）的配置文件（/etc/apparmor.d/sbin.klogd）：

```python
# Profile for /sbin/klogd

#include <tunables/global>

/sbin/klogd {
#include <abstractions/base>

capability sys_admin,

/boot/System.map*     r,
/proc/kmsg           r,
/sbin/klogd          rmx,
/var/log/boot.msg    rwl,
/run/klogd.pid       rwl,
}
```

注释（如第 1 行所示）以 # 号开始。

**#include**（如第 3 行和第 6 行所示）不被解释为注释，而是用于从其他文件中包含规则。如上所示，路径是相对于 /etc/apparmor.d/ 的。

/etc/apparmor.d/tunables/global（第 3 行）用于包含应在每个配置文件中可用的定义。默认情况下，它仅包含 /etc/apparmor.d/tunables/home，其中定义了变量 @{HOMEDIRS} 和 @{HOME}。这些变量在许多配置文件中被使用。

目录 /etc/apparmor.d/abstractions/ 包含按常见应用程序任务分组的通用规则文件。这些包括，例如，所有应用程序所需的文件访问（base）、认证机制访问（authentication）、图形环境（kde, gnome）、名称解析（nameservice）等。为了避免在多个配置文件中冗余指定，它们在单点定义并包含在需要它们的配置文件中。

上述示例中的第 5 行给出了由 AppArmor 限制的程序的路径。规则以及任何包含项都跟随在大括号 {} 内。

第 8 行为此程序启用 sys_admin 权限。其他所需的权限将列在以 capability 开头的单独行中。

剩余的行列出文件和目录，以及授予的访问权限。

在列出文件和目录的行中，可以使用以下通配符：

- `*` 替代任意数量的字符，但不包括 /。
- `**` 替代任意数量的字符，包括 /。使用 `**` 来包含子目录。
- `?` 替代任意单个字符，但不包括 /。
- `[abc]` 替代 a, b 或 c。
- `[a-d]` 替代 a, b, c 或 d。
- `{ab,cd}` 替代 ab 或 cd。

