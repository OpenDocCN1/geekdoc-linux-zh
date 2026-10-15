
有关特定特定笔记本电脑的更多信息，请访问 Linux 笔记本电脑主页 http://linux-laptop.net。另一个良好的信息源是 Mobilix 主页 http://tuxmobil.org/。SUSE LINUX 支持数据库包含了几篇关于在移动设备上使用 SUSE LINUX 的文章。访问 http://portal.suse.sdb/en/index.html 并搜索 laptop。

## 7.2 SCPM — 系统配置方案管理

某些情况需要修改计算机的系统配置。这对于在不同地点运行的移动计算机来说通常如此。如果临时使用比通常不同的硬件组件运行桌面系统，SCPM 将派上用场。无论如何，恢复原始系统配置应该是简单的，且系统配置的修改是可以重现的。

到目前，这个问题仅针对 PCMCIA 硬件提供了解决方案，即各种配置可以存储在不同的配置文件中。随着 SCPM（系统配置方案管理）的发展，这种方法得到了进一步完善，消除了对 PCMCIA 硬件的限制。通过 SCPM，系统配置的任何部分都可以保自定义配置文件。这就像是对系统进行快照，并在任何时间恢复它。

SCPM 的主要应用是笔记本电脑的网络配置。不同的网络配置通常需要其他设备的设置，例如电子邮件或代理。然后其他元素，如家里和办公室不同的打印机、为会议准备的 X 服务器配置、路上的特殊节能设置，或者海外机构不同的时区。

增加此工具的使用会导致不断发现新需求。欢迎随时与我们联系并分享你的想法和创意，SCPM 基于灵活的框架，旨在允许基于服务器的方案管理。通过我们的网页前端 http://www.suse.de/feedback/ 反馈愿望、灵感和错误描述。

### 7.2.1 术语和概念

以下是 SCPM 文档和 YaST 模块中使用的一些术语。

- 系统配置是指计算机的完整配置。它涵盖了所有基本设置，如分区使用、网络设置、时区选择和键盘映射。
- 配置方案（也称为配置文件）是一个已保存并可以随时恢复的状态。
- 活动配置是指最后选择的配置。这并不意味着当前的系统配置完全对应此配置，因为配置可以随时自定义。
- SCPM 语境下的资源是指对系统配置做出贡献的元素。它可以是一个文件或软链接，包括其元数据（如用户权限或访问时间）。它也可以是一个在该配置中运行但在另一个配置中禁用的系统服务。
- 每个资源都属于某个资源组。这些组包含了逻辑上相关的所有资源——大多数组同时包含一个服务及其配置文件。组合由 SCPM 管理的资源非常容易，因为这不需要了解目标服务的配置文件的知识。SCPM 附带了一组预配置的资源组，应该足够满足大多数场景。

### 7.2.2 YaST 模块与额外文档

YaST 模块（软件包 `yast2-profile-manager`）是 SCPM 的图形化前端，提供了命令行界面的替代方案。由于这两个界面的功能基本相同，且命令行界面的知识在许多情况下非常有用，因此本文将介绍命令行界面。在适当的地方，会提到 YaST 前端与命令行工具之间的差异。

请参阅 SCPM 页面以获取最新文档。您可以使用 Konqueror（执行命令 `konqueror info:scpm`）或 emacs 等工具阅读这些内容。在控制台上，请使用 `info` 或 `pinfo`。技术信息可以在 `/usr/share/doc/package/scpm` 提供。不带任何参数运行 `scpm` 将返回命令选项摘要。

### 7.2.3 配置 SCPM

SCPM 在使用前必须先激活。默认情况下，SCPM 处理网络和打印机设置以及 XFree86 配置。如果你需要管理特殊服务或配置文件，请激活资源组。要列出定义的资源组，请使用 `scpm list-groups`。要仅查看已激活的组，请使用 `scpm list-groups -a`。在命令行中以 root 身份执行这些命令。使用 `scpm activate-group NAME` 或 `scpm deactivate-group NAME` 激活或禁用某个组。将 `NAME` 替换为相应的组名。所有资源组都可以通过 YaST 描述管理器进行配置。

使用 `scpm enable` 激活 SCPM。首次执行时，SCPM 会初始化，这需要几秒钟。可以随时使用 `scpm disable` 禁用 SCPM，以防止意外切换配置。随后的激活将直接恢复初始化。

### 7.2.4 创建和管理配置

在 SCPM 激活后，已经存在一个名为 `default` 的配置。使用 `scpm list` 获取所有可用配置的列表。这个仅存在的配置也是激活配置，可以通过 `scpm active` 进行验证。`default` 配置文件是一个基础配置，其他配置均基于此派生。因此，所有在所有配置中应相同的设置都应先进行。这些修改随后通过 `scpm reload` 存储在激活配置中。`default` 配置可以被使用、重命名或删除。

添加新配置有两种可能。如果新配置（此处命名为 `work`）应基于 `default` 配置，则使用 `scpm copy default work` 创建它。命令 `scpm switch work` 会切换到新配置，并对其进行修改。有时为了特殊目的修改了系统配置，这些修改应该保留在新配置中。命令 `scpm add work` 通过将当前系统配置保存到配置 `work` 中并将其标记为激活状态，来创建一个新配置。运行 `scpm reload` 将更改保存到 `work` 配置中。

使用命令 `scpm rename x y` 和 `scpm delete x` 重命名或删除配置。例如，将 `work` 重命名为 `project`：执行 `scpm rename work project`。使用 `scpm delete project` 删除 `project`。激活的配置无法删除。

YaST 模块仅提供“添加”（Add）按钮。点击该按钮会打开一个对话框，在其中选择复制现有配置还是保存当前系统配置。使用“编辑”（Edit）进行重命名。

### 7.2.5 切换配置方案

`scpm switch` 命令切换到另一个配置（在此例中为 `work`）。切换到激活的配置以保存修改后的系统配置设置。或者，使用 `scpm reload` 来实现此操作。

在切换配置时，SCPM 首先检查激活配置中哪些资源被修改过。然后它查询每个资源的修改是应该添加到激活配置中还是丢弃。如果你倾向于使用独立的资源列表（在 SCPM 的旧版本中），请带有 `-r` 参数使用 `switch` 命令：`scpm switch -r work`。

SCPM 将当前系统配置与要切换到的配置进行比较。在此阶段，SCPM 会评估哪些系统服务由于相互依赖需要停止或重启，或者为了反映配置的变化。这类似于部分系统重启，仅涉及系统的一小部分，而其他部分继续运行保持不变。

只有在此时，系统服务才会停止，所有修改的资源（例如配置文件）会被写入，并重启系统服务。

### 7.2.6 高级配置设置

你可以为每个配置输入描述，该描述会在 `scpm list` 时显示。对于激活的配置，使用 `scpm set description "text"` 设置。对于未激活的配置，提供配置名称，例如 `scpm set description "text" work`。有时可能需要执行一些额外的操作，这些操作未由 SCPM 提供，但在切换配置时执行。这些操作在配置切换的以下阶段执行：

- 停止服务前的 prestop
- 停止服务后的 poststop
- 启动服务前的 prestart
- 启动服务后的 poststart

从配置切换到配置如下：

1. 执行 `work` 的 prestop。
2. 服务停止。
3. 执行 `work` 的 poststop。
4. 系统配置已更改。
5. 执行 `home` 的 restart。
6. 服务启动。
7. 执行 `home` 的 poststart。

通过 `scpm set prestop <filename>`、`scpm set poststop <filename>`、`scpm set restart <filename>` 或 `scpm set poststart <filename>` 关联这些操作。脚本必须对 root 可执行。如果脚本不可执行，SCPM 在尝试运行它时报错。

### 7.2.7 启动时选择配置

可以在启动过程中通过提供 `PROFILE=<name>` 来选择配置。在启动加载程序配置（`/boot/grub.lst`）中，标题反映了名称。例如：

示例 7.1：`/boot/grub.lst`

```
entry "work" {
    kernel /vmlinuz
    initrd /initrd
    args root=/dev/sda
}
entry "home" {
    kernel /vmlinuz
    initrd /initrd
    args root=/dev/sda
}
entry "road" {
    kernel /vmlinuz
    initrd /initrd
    args root=/dev/sda
}
```
