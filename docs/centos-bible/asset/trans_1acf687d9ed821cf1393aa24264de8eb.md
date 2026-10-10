
用法（按 **P** 键）。以下输出展示了 top 运行时的一个示例，其中信息按内存使用量排序。所示系统正在运行 GNOME 桌面环境，OpenOffice.org Writer、Firefox 网页浏览器以及其他几个应用程序处于活动状态。请注意，空闲内存量非常低。要在 CentOS 桌面系统上获得良好的性能，一旦开始运行许多大型应用程序，256 MB 可能是不够的。

```
top - 16:11:41 up 10:27,   2 users,   load average: 1.60,  0.51,  0.18
Tasks: 107 total,   2 running, 103 sleeping,   0 stopped,   2 zombie
Cpu(s): 16.6%us,  6.5%sy,  0.0%ni,  0.0%id, 76.9%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:  252424k total,  249224k used,   3200k free,    2360k buffers
Swap: 1020088k total,  14240k used, 1005848k free,   86820k cached

  PID USER     PR  NI VIRT  RES  SHR S %CPU %MEM     TIME+ COMMAND
 4242 timothy  18   0 163m  37m  25m R 19.9 15.0   0:05.86 writer-b
 4217 timothy  15   0 137m  31m  17m S  0.0 12.9   0:07.27 firefox-b
 4244 timothy  15   0 39148 18m  7684 S  0.0  7.6   0:04.94 beagled-hel
 4138 timothy  15   0  101m  14m 9.8m S  0.0  5.9   0:06.87 baobab
```

# 在笔记本电脑上监控电源使用情况

要有效地使用笔记本电脑，您需要能够监控和管理笔记本的电源使用情况。使用 CentOS 提供的工具，您可以配置您的笔记本电脑以：

-   监控电池电量
-   在电池电量低时通知您。
-   在电池充满时通知您。
-   显示笔记本电脑是否已插电
-   挂起当前会话。

CentOS 提供 ACPI 设施来处理电源管理。ACPI 还可以进行热控制、主板配置以及更改电源状态。

许多旧笔记本电脑的 BIOS 中不包含对 ACPI 的支持，而一些新笔记本电脑可能需要 ACPI。要检查您的 CentOS 系统是否支持 ACPI，您可以在重启后使用 dmesg 命令。例如，输入：

```
# dmesg | less
```

翻页查看输出，寻找以 ACPI 开头的行。在一台 ACPI 无法正常工作的计算机上，我看到了信息“ACPI: System description tables not found.”（ACPI：未找到系统描述表）。

以下过程是在一台使用 ACPI 来管理电源事件的笔记本电脑上执行的。它描述了如何使用桌面上的 GNOME 电源管理器小工具来监控电池。

## 第三部分 管理

> **注意**
> 如果似乎 ACPI 正在干扰您的笔记本电脑正常运行，您可以在启动计算机时将其关闭。在 GRUB 引导屏幕的内核行末尾或 `/boot/grub/grub.conf` 文件中的内核行末尾添加 `acpi=off` 即可关闭 ACPI。

### 使用 acpi_listen 监控 ACPI 事件

如果您的系统正在运行 ACPI，您可以使用 `acpi_listen` 命令监控 ACPI 事件。作为 root 用户，在终端窗口中输入以下内容：

```
# acpi_listen
ac_adapter AC 00000080 00000000
processor CPU 00000080 00000000
processor CPU 00000081 00000000
battery BAT0 00000080 00000001
ac_adapter AC 00000080 00000001
processor CPU 00000080 00000000
processor CPU 00000081 00000000
battery BAT0 00000080 00000001
button/lid LID 00000080 00000001
button/lid LID 00000080 00000000
```

上述消息出现在交流电源断开、电源重新连接、笔记本电脑盖子关闭以及盖子再次打开时。

## 使用 Security Enhanced Linux

Security Enhanced Linux（SELinux）是一种安全模型，它有可能对 Linux 系统的每个组件（进程、文件、目录、用户、设备等）进行隔离和加固。与传统 Linux 和 UNIX 系统那种“要么拥有 root 权限，要么没有”的全有或全无的安全方法不同，SELinux 在授予计算机组件运行和修改权限方面允许更细粒度的控制。借助 SELinux，您可以极大地限制某人破解 Linux 系统某一部分所造成的损害。

安装 CentOS 时，您有机会启用或禁用 SELinux。如果启用，默认使用 targeted 策略。Targeted 策略侧重于具有漏洞守护进程的服务中心，以及这些服务可以访问的资源。

Targeted 策略限制了对以下服务攻击可能对您整个服务器造成的影响：Apache（Web 服务器）、Samba（Windows 文件和打印共享）、FTP（文件传输协议）、NFS（网络文件系统）以及其他。当前的 targeted 策略集合是实用的，并为已经相当安全的功能提供了进一步的边界。在大多数情况下，您可以无需修改即可使用此策略集合。

本节旨在让您了解 SELinux 是什么。它描述了如何在 CentOS 中开启 SELinux。然后，它概述了 CentOS 的 targeted 策略是如何为您设置的，并描述了您可以如何修改 targeted SELinux 策略以个性化您的 SELinux 策略设置。

# 理解 Security Enhanced Linux

在传统 UNIX 和 Linux 系统中，当用户获得对计算机的 root 访问权限时，她就拥有了这台机器。*root* 用户（或接管为 *root* 用户的人）可以覆盖所有权、读/写/执行权限以及处理器调度优先级。同样，对 Web 服务器（*httpd* 守护进程）的攻击可能允许攻击者获得 apache 用户账户的全部权限，而不是将攻击限制在单个虚拟主机资源集上。

美国国家安全局（NSA）等机构认识到需要在安全环境中的操作系统能够根据保密性和数据完整性来分离信息。标准的安全模型使得 Linux 和 UNIX 系统无法用于高度安全的环境，在这些环境中，一次利用就导致整个操作系统崩溃的风险是不可接受的。NSA 推荐用于实现高度安全系统的机制被称为*强制访问控制*（MAC）。

SELinux 项目旨在为 Linux 内核提供 MAC 功能。通过实施规则规定所有操作系统组件可以做和不能做的事情，可以限制存在安全漏洞或被恶意接管的应用程序。换句话说，控制系统的某个组件并不允许黑客接管整个计算机。

尽管 SELinux 很复杂，但在最近的版本中，许多 bug 已经被解决，默认设置相当易于操作。我建议在一台正在测试的服务器上启用 SELinux，为有一天启用 SELinux 来保护您的互联网服务器做准备。

## SELinux 中的类型和角色

在 SELinux 中实施安全规则的机制被称为*策略*。任何实现 SELinux 的系统都会选择一个特定的策略（*strict*、*targeted* 等），该策略产生一套一致的规则，以满足系统所需的安全级别。

使用策略配置文件，SELinux 实现了两种不同的安全模型：*类型强制*（TE）和*基于角色的访问控制*（RBAC）。

-   **类型强制（TE）** — 在 TE 模型下，操作系统中的每个对象都绑定到一个称为*类型*的安全属性。每个进程都绑定到一个称为*域*的安全属性。这种方法允许对操作系统中的每个对象进行非常严格的控制。每个用户根据其被允许操作的域，被允许访问操作系统中的对象。

-   **基于角色的访问控制（RBAC）** — 使用 RBAC 模型，SELinux 允许每个用户在特定角色中操作。这些角色按层级排列，每个角色都通过类型强制提供特定的权限。

在传统 Linux 中，用户被分配特定的用户 ID（UID）和组 ID（GID），这赋予该用户对系统资源的某些访问权限。例如，根据用户是否拥有文件或目录，或者是否属于分配给该文件或目录的组，这赋予用户对文件或目录进行读取、写入或执行操作的某些权利。

在 SELinux 中，数据文件、目录或应用程序可以关联更多的属性。这些属性实际上可能比传统 Linux 安全机制提供的权限更多，允许访问该组件。同时，拥有该组件的访问权限并不一定意味着该用户能以超出安全策略允许的方式控制该组件。

## SELinux 中的用户

SELinux 用于定义用户在启用 SELinux 的系统中权利的模式，可以与现有的 Linux 用户模型共存，而不是取代它。启用 SELinux 后，Linux 用户仍然通过 /etc/passwd 文件中的定义来确定其账户。也被分配 SELinux 角色的用户被称为定义用户。

SELinux 中的特殊用户身份包括 system_u（分配给系统进程的用户身份）和 user_u（用于指示一般用户，特别是那些没有特定用户身份的用户，是否被允许使用相关功能的分配）。还有一个 root 身份，保留它是为了与现有的文件上下文保持兼容。这允许现有文件如果其用户身份为 root，则保持有效。

## SELinux 中的策略

如前所述，在 CentOS 中，您可以选择关闭 SELinux 或开启 SELinux。/etc/selinux/config 文件中设置的值决定了哪种类型的策略是开启的（默认仅提供 targeted 策略；但也可提供 strict 策略），以及 SELinux 是否处于：

-   **Enforcing（强制）** — 当前 SELinux 策略已开启，且其策略被强制执行。
-   **Permissive（宽容）** — 当前 SELinux 策略已开启，但未强制执行（因此您只会看到描述该策略将如何被强制执行的警告消息）。
-   **Disabled（禁用）** — SELinux 已关闭，因此仅强制执行标准 Linux 权限（就像在没有 SELinux 的系统上一直那样）。

CentOS 包含针对其提供的 targeted 策略的编译策略文件。例如，在当前的 CentOS 版本中，当该策略处于活动状态时，使用的编译策略集是 /etc/selinux/targeted/policy/policy.21。

## SELinux 中的工具

SELinux 提供的工具让您能够处理 SELinux 的策略设置并更改它们。这些工具中的许多包含在 selinux-policy、policycoreutils-gui 和 setroubleshootshot 软件包中。

