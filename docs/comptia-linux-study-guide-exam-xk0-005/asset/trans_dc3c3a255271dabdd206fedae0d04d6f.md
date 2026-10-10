

user::rw-
group::r--
mask::r--
other::---

Linux 还允许你在目录上设置默认 ACL，该 ACL 会被目录中创建的任何文件自动继承。这个特性称为 *继承*。
要在目录上创建默认 ACL，请以 *d:* 开头，后跟正常的规则定义。示例如下：
$ sudo setfacl -m d::sales:rw /shared/sales
此示例为 /shared/sales 目录中的 *sales* 组分配了读和写权限。现在，该文件夹中创建的所有文件都将自动获得 sales 组的读和写权限。

## 基于上下文的权限

原始权限方法和高级 ACL 方法这两种向文件和目录分配权限的方式都称为 *自主访问控制* (DAC) 方法。权限的设置由文件或目录所有者自行决定。管理员无法阻止用户在其目录中的所有文件上授予其他用户完全权限。

为了对 Linux 系统进行完整保护，最好使用某种 *强制访问控制* (MAC) 方法。MAC 方法允许系统管理员根据 Linux 系统中对象的上下文来定义安全策略，从而覆盖由文件和目录所有者设置的权限。MAC 方法为管理员提供了规则，不仅限制用户对文件和目录的访问，还限制在系统上运行的应用程序的访问。

> **注意**
> 在安全文献中，你也可能会看到 *基于角色的访问控制* (RBAC) 这个术语。RBAC 方法是 MAC 的一个子类别，它根据用户和进程在 Linux 系统中扮演的角色来设置安全权限。

- 目前 Linux 中有两种流行的 MAC 实现：
  - Red Hat 基于的系统使用 SELinux
  - Ubuntu 系统使用 AppArmor

接下来的章节将详细介绍如何在你的 Linux 环境中使用 SELinux 和 AppArmor。

### 使用 SELinux

*Security-Enhanced Linux (SELinux)* 应用程序是美国国家安全局 (NSA) 的一个项目，自版本 2.6.x 起已集成到 Linux 内核中。它现在是 Red Hat 基于的 Linux 发行版（如 Fedora、Rocky 和 CentOS）的标准组成部分，也是 Debian 基于的发行版的可选安装项。

SELinux 通过允许你设置策略规则来控制 Linux 系统上各种类型对象之间的访问，从而实施 MAC 安全，这些对象包括用户、文件、目录、内存、网络端口和进程。每次用户或进程尝试访问 Linux 系统上的对象时，SELinux 都会拦截该尝试并根据定义的策略规则进行评估。

### 启用 SELinux

`/etc/selinux/config` 文件控制 SELinux 的基本操作。你需要指定两个主要设置：

SELINUX：此设置决定 SELinux 的运行模式。将其设置为 `enforcing` 可启用系统上的策略规则并阻止任何未经授权的访问。将其设置为 `permissive` 时，SELinux 监控策略规则并记录任何策略违规行为，但不强制执行它们。`disabled` 设置值会完全禁用 SELinux 对系统上活动的监控。

SELINUXTYPE：此设置决定强制执行哪些策略规则。`targeted` 设置是默认设置，仅强制执行网络守护进程的策略规则。`minimum` 设置仅强制执行指定进程的策略规则。`mls` 设置使用多层安全，提供遵循 Bell-LaPadula 安全控制模型的先进策略，该模型是大多数要求高安全级别的美国政府环境和军事环境所强制执行的。它使用绝密、非机密和公开等安全分类。`strict` 设置对守护进程强制执行所有策略规则，但已不再推荐用于此目的。

要更改 SELinux 的状态，你也可以从命令行使用 `setenforce` 实用工具。但是，你只能使用该工具在 enforcing 和 permissive 模式之间切换 SELinux。要禁用 SELinux，你必须在 SELinux 配置文件中做出更改。要查看 SELinux 的当前模式，请使用 `getenforce` 实用工具：

```
$ sudo getenforce
Enforcing
$
```

如需更详细的 SELinux 状态列表，请使用 `sestatus` 实用工具：

```
$ sudo sestatus
SELinux status: enabled
SELinuxfs mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: targeted
Current mode: enforcing
Mode from config file: enforcing
Policy MLS status: enabled
Policy deny_unknown status: allowed
Memory protection checking actual (secure)
Max kernel policy version: 33
$
```

启用 SELinux 后，它开始强制执行定义在一组策略中的对象访问规则。接下来的章节将解释 SELinux 策略的工作原理。

## 理解安全上下文

SELinux 使用 *安全上下文* 为系统上的每个对象标记。安全上下文定义了 SELinux 应用于该对象的策略。安全上下文的格式如下：
*user:role:type:level*

*user* 和 *role* 属性仅在多层安全模式中使用，可能会变得相当复杂。运行在默认目标安全模式下的系统仅使用 *type* 属性来设置对象安全类型并基于此控制访问。*level* 属性设置安全敏感度级别和许可级别。它在目标安全模式下是可选的，主要用于高安全环境。

要查看分配给对象的安全上下文，请在常见的 Linux 命令（如 id、ls、ps 和 netstat）中添加 -Z 选项。例如，要查看你的用户安全上下文，请使用以下命令：
$ id -Z
unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
$

unconfined_u 用户安全上下文表示该用户账户未分配到特定的安全策略；同样，角色为 unconfined_r，类型为 unconfined_t。s0-s0:c0.c1023 级别安全上下文意味着该对象的安全级别和许可级别也已设置。

要查看文件的安全上下文，请使用以下命令：
$ ls -Z test1.txt
unconfined_u:object_r:user_home_t:s0 test1.txt

再次说明，user 属性为 unconfined_u，但此时 type 属性设置为 user_home_t。你可以在安全策略中使用此属性来设置每个账户 $HOME 目录中文件的访问权限。

要检查分配给进程的安全上下文，请使用以下命令：
$ ps -aZ | grep sshd

```
system_u:system_r:sshd_t:s0-s0:c0.c1023 ? Ss 0:00
/usr/sbin/sshd [...]
$
```

sshd 应用程序所需的进程被设置为 system_u 用户安全上下文和 system_r 角色安全上下文。这表明该进程与系统相关。该进程的类型安全上下文有所不同，这意味着可以通过单独的策略进行控制。

> **注意**
> 在 SELinux 文档和文献中，安全上下文通常被称为标签。SELinux 在首次启用时必须为系统上的每个对象分配标签，这可能是一个漫长的过程。

semanage 实用工具允许你查看和设置系统上用户账户的安全上下文。对于文件和目录，Linux 系统在创建时会根据父目录的安全上下文设置它们的安全上下文。你可以使用 chcon 或 restorecon 实用工具来更改分配给文件的默认安全上下文。

chcon 的格式如下：

```
chcon -u newuser -r newrole -t newtype filename
```

newuser、newrole 和 newtype 值定义了你希望分配给指定文件的新用户、角色和类型安全上下文。

restorecon 实用工具将文件或目录的安全上下文恢复为策略中定义的默认设置。你可以使用 -R 选项递归恢复指定目录下所有文件的安全上下文。

> **警告**
> runcon 实用工具允许你使用指定的安全上下文启动应用程序，但请务必小心。如果应用程序在没有访问任何必需配置或日志文件的情况下启动，可能会发生奇怪的事情，而且通常都会发生。

## 使用策略

SELinux 基于策略控制对系统对象的访问。在目标安全模式下，每个策略定义了特定类型安全上下文中的对象可以访问另一个类型安全上下文中的哪些对象。这称为类型执行。

例如，标记为 sshd_t 类型安全上下文的应用程序仅被允许访问标记为 rpm_t 类型安全上下文中的文件。这将应用程序的访问限制为系统中的某些文件。

SELinux 在 /etc/selinux 目录结构中以文本文件形式维护策略。例如，目标安全模式下的所有策略都位于 /etc/selinux/targeted 目录下。

创建自己的策略可能有点复杂。幸运的是，SELinux 包含策略组，称为模块，你可以将它们作为标准 RPM 软件包安装。使用 semodule 实用工具来列出、安装和删除系统中的策略模块。

