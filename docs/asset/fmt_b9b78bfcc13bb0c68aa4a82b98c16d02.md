
# SELinux：管理操作

你可以在 SELinux 系统上执行若干任务，而无需重新编译整个配置。根据需要更改文件和目录的安全上下文。例如，当你添加新的文件系统时，你需要用适当的安全上下文对其进行标记。此外，当你添加用户时，可能需要系统对某个用户给予特殊关注。为了检测和修复问题，你可以使用 `setroubleshoot`。

## 使用安全上下文：`fixfiles`, `setfiles`, `restorecon` 和 `chcon`

有多种工具可以更改对象的安全上下文。`fixfiles relabel` 命令可以设置安全上下文，并可以使用 `check` 选项查看应该更改的内容。`fixfiles` 工具是一个使用 `setfiles` 和 `restorecon` 执行实际更改的脚本。

`restorecon` 命令将恢复文件和目录的安全上下文，但 `setfiles` 是设置安全上下文的基础工具。它可以应用于单个文件或目录。它在首次安装策略时用于标记文件标记。

通过 `chcon`，你可以更改单个文件和目录的权限，就像 `chmod` 处理普通权限一样。

## 添加新用户

如果新新用户需要特殊访问权限，通常可以使用通用的 SELinux 用户 `user_u` 身份。然而，如果你需要允许用户承担在其他情况下受限的角色（例如严格策略中的系统管理员角色），你需要相应地配置该用户。要做到这一点，你需要将用户添加到策略 `users` 目录下的 `local.users` 文件，例如 `/etc/selinux/targeted/policy/local.users`。注意，这与 `src` 目录中的 `local.users` 文件不同，后者会被直接编译到策略中。用户的语法为：

```
user username roles { rolelist };
```

以下示例将 `sysadm` 角色添加到 `george` 用户：

```
user george roles { user_r sysadm_r };
```

一旦添加了角色，你就必须重新加载策略。

```
reload
```

你还可以使用 `seuser` 命令管理用户。要查看当前活跃用户，你可以使用 `seuser` 命令和 `show users` 选项列出它们。

```
# seuser show users
system_u: system_r

user_u: user_r sysadm_r system_r

root:user_r sysadm_r system_r
```

`seuser` 命令可以添加、删除、更改和重命名上下文以管理用户。`add` 和 `change` 选项允许你指定要添加到用户的角色。

## 运行时安全上下文和类型：上下文

某些服务和应用程序具有感知能力，并会向 SELinux 请求默认的安全上下文和类型（请参阅接下来的章节“运行时安全上下文和类型：上下文”）。配置保存在 `policy/config/appconfig-` 目录下的文件中。`default_types` 文件存储策略默认值；`default_contexts` 存储默认安全上下文。`intric_context` 文件持有 `/etc/rc` 脚本的默认安全上下文。一个特殊的 `root_context` 文件持有 root 用户如何被访问。`removable_context` 持有可移除设备的安全上下文，而 `media` 列出媒体设备（如 CD-ROM）。运行时值也可以注册到 `policy contexts` 目录下的文件中，例如 `/etc/selinux/targeted/contexts`。

`default_types` 文件定义了类型。该文件包含角色/类型项，当转换到新角色时将使用此处指定的默认类型。例如，`sysadm_r` 角色的默认类型是 `sysadm_t`。

```
sysadm_r:sysadm_t

user_r:user_t
```

特别重要的是 `initrc_context` 文件，它设置了 `etc` 目录下运行脚本的上下文。在目标策略中，这些对所有用户开放。

```
user_u:system_r:unconfined_t
```

在严格策略中，这些仅限于系统用户。

```
system_u:system_r:initrc_t
```

`removable_context` 持有可移除设备的安全上下文，而 `media` 列出媒体设备（如 CD-ROM）。可移除设备的默认上下文是 `removable_context`。其内容所示：

```
system_u:object_r:removable_t
```

文件和目录的默认安全上下文位于 `contexts/files` 目录。`file_contexts` 目录列出了策略设置的所有文件和目录的默认安全上下文。`context.homedirs` 设置用户家目录文件以及根目录的上下文，包括 `.mozilla .conf` 等配置文件。`media` 文件为媒体设备（如 CD-ROM 和磁盘）设置默认上下文。

```
cdrom system_u:object_r:removable_device_t

floppy system_u:object_r:removable_device_t

disk system_u:object_r:fixed_disk_device_t
```

### users

可能还需要为特定用户（如 root 用户）设置默认安全上下文。在 `suers` 中，你会找到一个角色文件，列出了 root 用户可以承担的角色、类型和安全级别，例如以下 `su` 操作的示例：

```
sysadm_r:sysadm_su_t sysadm_r:sysadm_t staff_r:staff_t user_r:user_t
```
