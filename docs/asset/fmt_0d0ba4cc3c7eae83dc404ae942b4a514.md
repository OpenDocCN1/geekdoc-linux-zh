
# sestatus -v less

SELinux status: disabled

输出显示当前系统未强制 SELinux。如果 SELinux 被设置为 permissive（宽容模式），输出将类似于下所示：

| SELinux 状态: | enabled |
| :--- | :--- |
| SELinux 挂载: | `/selinux` |
| 当前模式: | enforcing |
| 配置文件中的模式: | enforcing |
| 策略版本: | 24 |
| 配置文件中的策略: | targeted |

进程上下文:
当前上下文: `user_u:system_r:unconfined_t:SystemLow-SystemHigh`
初始化上下文: `user_u:system_r:init_t`
`/sbin/gettty` `user_u:system_r:getty_t`
`/usr/sbin/sshd` `user_u:system_r:unconfined_t:SystemLow-SystemHigh`

文件上下文:
控制终端: `user_u:object_r:devpts_t`
`/etc/passwd` `user_u:object_r:reict_t`
`/etc/shadow` `user_u:object_r:shadow_t`
`/bin/bash` `user_u:system_r:rhell_exec_t`
`/bin/login` `user_u:system_r:rlogin_exec_t`
`/bin/sh` `user_u:system_r:bin_t` *
`system_u:object_r:shell_exec_t` `user_u:object_r:gettty_exec_t`
`/sbin/gettty` `user_u:object_r:init_exec_t`
`/sbin/init` `user_u:object_r:gettty_t`
`/sbin/sshd` `user_u:object_r:sshd_exec_t`
`/lib/libc.so.6` `user_u:object_r:rlib_t` -> `system_u:object_r:ld_so_t`
`/lib/ld-linux.so.2` `user_u:object_r:rlib_t` -> `system_u:object_r:ld_so_t`

按 Page 键翻页输出。除了显示 SELinux 已启用并运行在强制模式外，此输出还显示了进程上下文和文件上下文：

要从图形界面查看并更改 SELinux 设置，可以打开 SELinux 管理窗口。从 GNOME 桌面，选择 System ➜ SELinux Management。在那个窗口中，你可以将 SELinux 设置为 Disabled（禁用）、Enforcing（强制）或 Permissive（宽容）。你还可以设置要使用的 SELinux 策略（默认是 targeted）。

## 460 第三部分：管理 Fedora 和 RHEL

更改策略类型或将 SELinux 服务从关闭开启，都需要你对整个文件系统进行重新标记（relabel）。更改策略绝不应轻率为。如果你决定通过 SELinux 管理窗口更改策略，该更改同样需要对文件系统进行重新标记。通过此窗口更改策略，文件系统将在下次重启计算机时被重新标记（或者你可以勾选复选框防止下次重启时对文件系统进行重新标记）。

> 注意：重新标记文件系统可能是一项长期且耗时的活动。再次记住，更改策略是对你操作系统的一项重大更改。文件系统中的节点越多，下次重启计算机时重新标记文件系统所需的时间越长。

你可以使用 `id` 命令配合 `-Z` 选项检查你当前操作的安全上下文。以下示例显示你的用户是 root 用户，你的角色是 `system_r` 角色，类型是 `unconfined_t`。

```bash
# id -Z
unconfined:unconfined_r:unconfined_t:s0-c0:1023
```
