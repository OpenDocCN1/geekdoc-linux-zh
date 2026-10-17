
- `disabled`（禁用）—— SELinux 关闭，仅执行标准的 Linux 权限（正如在不包含 SELinux 的系统上一直开启一样）。

Fedora 和 RHEL 包含了它们交付的目标策略的编译后策略文件。例如，在当前的 Fedora 版本中，`/etc/selinux/targeted/policy/policy.23` 是该策略激活时使用的编译策略集。

## SELinux 中的工具

SELinux 提供的工具允许你操作和更改 SELinux 中的策略设置。这些工具中的许多项在当前版本的 Fedora 中包含在 `selinux-policy`、`selinux-policoreutils` 和 `setroubleshoot-server` 软件包中。工具包括：

- SELinux 故障器 (SELinux Troubleshooter) —— 当 SELinux 检测到违反 SELinux 策略的内容时，桌面面板会启动一个图标。点击该图标显示排除器窗口，查看问题的描述和潜在的修复。你也可以通过选择应用程序 -> 系统工具 -> SELinux 故障器直接启动排除器。
- SELinux 策略生成工具 (SELinux Policy Generation Tool) —— 用于生成自定义 SELinux 策略框架的图形化工具。应用程序开发人员或系统管理员可以使用此工具限制用户或应用程序，使其仅访问它们所需的资源。
- SELinux 管理窗口 —— 打开 SELinux 管理窗口（选择系统 -> 管理）来更改 SELinux 的状态（启用、禁用或强制）。你还可以针对用户、文件和目录、模块以及网络端口修改 SELinux 设置。
- SELinux 命令 —— 一系列命令行工具可用于修改 SELinux 策略。这些策略可以开启或关闭（SELinux 属性）。要获取有关 SELinux 如何处理特定守护进程的信息，请参考各种 SELinux 策略手册页（`file_selinux`、`http_selinux`、`kerberos_selinux`、`named_selinux`、`nfs_selinux`、`nis_selinux`、`vsync_selinux` 和 `ybind_selinux`）。

## 在 Fedora 和 RHEL 中使用 SELinux

如果你使用 SELinux 策略（默认提供的），你可以像以前一样管理 SELinux。以下步骤描述了使用 SELinux 需要的软件软件包，并引导你从默认策略开始。如果你需要更多信息，请参考以下：

- Red Hat Enterprise Linux 4 SELinux 指南 —— 描述了如何在 Red Hat Enterprise 4 中使用、管理和排错 SELinux。虽然某些特定的策略设置与最新的 Fedora 有所不同，但它是理解 SELinux 在 RHEL 和 Fedora 系统中工作的极佳指南。你可以在此处找到此文档：

```
http://www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/selinux-guide/
```

- SELinux 文档 —— `selinux-doc` 页面提供的大多数来自国家安全局（NSA）的标准类型文档。在 Fedora 或 RHEL 系统的 `/usr/share/doc/selinux-doc` 目录下查找这些文件，使用你的网络浏览器或 PDF 查看器。

## 第 10 章：理解系统管理

### 获取 SELinux

虽然 SELinux 已启用，但它并不一定会被强制执行。`/etc/selinux/config` 文件决定了 SELinux 的状态。如果你倾向于使用 SELinux，可以在 SELinux 管理窗口中更改状态。SELinux 在 Fedora 和 RHEL 中默认启用。（注：此处后续部分文字由于原文重复，翻译时已按要求去重）。

### SELinux 状态检查

安装 SELinux 后，你可以通过 `/etc/selinux/config` 文件检查 SELinux 是否开启。要检查 SELinux 是否启用，输入以下命令：

| `sestatus -v` | `less` |

| SELinux status: | `disabled` |

输出显示当前系统未强制执行 SELinux。如果 SELinux 被设置为宽容（permissive），输出将如下所示：

| SELinux status: | `enabled` |

 SELinux mount: | `/selinux` |

 Current mode: | `enforcing` |

 Mode from config file: | `enforcing` |

 Policy version: | `22` |

 Policy from config file: | `targeted` |

## 第 10 章：理解系统管理 465

进程上下文：

| 当前上下文: | `user_u:system_r:unconfined_t:SystemLow-SystemHigh` |

| 初始文上下文: | `system_u:system_r:init_t` |

| `/sbin/mingetty` | `system_u:system_r:getty_t` |

| `/usr/sbin/sshd` | `system_u:system_r:unconfined_t:SystemLow-SystemHigh` |

文件上下文：

| 控制术语: | `user_u:object_r:devpts_t` |

| `/etc/passwd` | `system_u:object_r:etc_t` |

| `/etc/shadow` | `system_u:object_r:shadow_t` |

| `/bin/bash` | `system_u:object_r:shell_exec_t` |

| `/bin/login` | `system_u:object_r:login_exec_t` |

| `/bin/sh` | `system_u:object_r:bin_t` |

| `system_u:object_r:shell_exec_t` | `user_u:object_r:getty_exec_t` |

| `/sbin/agetty` | `system_u:object_r:init_exec_t` |

| `/sbin/init` | `system_u:object_r:getty_exec_t` |

| `/sbin/mingetty` | |

| `/usr/sbin/sshd` | `system_u:object_r:sshd_exec_t` |

| `/lib/Libc.so.6` | `system_u:object_r:lib_t -> system_u:object_r:lib_t` |

| `/lib/ld-linux.so.2` | `system_u:object_r:lib_t` |

按空格键翻页审计日志。除了 SELinux 已启用并运行在许可模式（permissive mode）外，此输出显示了已设置的进程上下文和文件上下文。

要在图形界面查看并更改 SELinux 设置，可以打开 SELinux 管理窗口。在 GNOME 桌面中，选择“管理（Administration） -> SELinux 管理”。在该窗口中，你可以设置 SELinux 是禁用（Disabled）、启用（Enabled）还是许可（Permissive）。你还可以将 SELinux 策略设置为目标类型（targeted，这是默认设置）。

更改策略类型或从关闭开启 SELinux 服务需要对整个文件系统进行重新标记（relabel）。更改策略绝不能轻率为。如果你决定通过 SELinux 管理更改策略，该更改也需要对文件系统进行重新标记。通过这种方式更改策略，文件系统将在下次重启计算机时自动重新标记（或者你可以勾选框以防止在下次重启时重新标记文件系统）。

> 注意：重新标记文件系统是一项漫长且耗时的活动。再次记住，更改策略是对你操作系统的重大变更。文件系统中的节点越多，下次重启计算机时重新标记文件系统所需就越长。

你可以使用带有 `-z` 选项的 `id` 命令检查你运行的安全上下文。以下示例显示你的当前上下文是 root 用户，你的角色是 `system_r` 角色，类型是 `unconfined_t`。

## 第三部分：管理 Fedora 和 RHEL

```
# id -Z
unconfined:unconfined_r:unconfined_t:s0-s0:c0.1023
```

SELinux 能够产生大量的错误信息。默认情况下，这些消息被定向到 `/var/log/messages` 文件。由于该文件包含许多服务的消息，你可以使用 `seAudit` 窗口（在终端窗口输入 `seaudit`）来查看与 SELinux 严格相关的消息。

## 更多关于 SELinux

要深入研究 SELinux，有很多技术报告、FAQ 和组件文档。以下是你可以检查的几个：

- SELinux FAQ (`fedora.redhat.com/docs/selinux-faq`) —— 该网站提供了针对 Fedora 中 SELinux 实现的信息。
