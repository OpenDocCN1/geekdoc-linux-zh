
## 理解和配置 SELinux

你也可以在启动时的 GRUB 提示符上设置当前的 SELinux 模式。更多细节请参见“理解和故障排除启动”。在 GRUB 提示符上，使用 `selinux=0` 禁用 SELinux，如果希望开启则使用 `selinux=1`。通常希望 SELinux 始终开启。然而，某些产品无法与 SELinux 工作。如果你有软件特别提到与 SELinux 不兼容，你必须关闭 SELinux。如果你怀疑 SELinux 阻止了服务的按预期运行，请将其关闭。相反，请按照本章“故障排除 SELinux”部分的分析日志文件。然而，测试服务器在关闭状态下运行是有用的。设置为 Permissive，练习 8.2 提供了用用的示例。

### 练习 8.2：在 SELinux 模式之间切换

在此练习中，你将安装 Apache Web 服务器并配置被 SELinux 拒绝的行为。你将 SELinux 设置为 Permissive 模式，这显示默认行为被接受。你将更改 `/etc/sysconfig/selinux` 文件将 SELinux 设置为禁用。随后，你创建一个空文件，将 SELinux 设为 Enforcing 并重启服务器。你会注意到重启后启动了重新标记程序，这需要很长时间完成。

- 1. 使用 `yum install httpd` 安装 Apache Web 服务器。如果 yum 说已安装，没关系；继续练习即可。
- 2. 安装完成后，使用 `service httpd` 验证你的 Apache 服务器确实启动。验证后，再次使用 `service httpd` 停止它。
- 3. 使用编辑器打开 `/etc/httpd/conf/httpd.conf` 文件，找到 `Listen 80` 的行。将其更改为 `Listen 81`。这尝试在 80 端口启动 Apache Web 服务器。现在再次使用 `service httpd` 启动 Apache 服务器。你会收到“Permission denied”（拒绝访问）的消息。
- 4. 输入 `setenforce Permissive`，并尝试启动 Apache 服务器。你会发现它是可以的。打开 `httpd.conf` 文件，将默认端口改回 80。
- 5. 使用编辑器打开 `/etc/sysconfig/selinux` 文件，将 `SELINUX` 参数更改为 `disabled`。重启服务器。
- 6. 重启后，以 root 身份登录并使用 `touch` 在家目录下创建一个新文件。
- 7. 使用 `ls -Z` 检查为该文件设置的上下文。你会发现该文件没有设置。
- 8. 再次修改 `/etc/sysconfig/selinux` 文件，将 SELINUX 设置回 `enabled`。重启服务器。当显示 Red Hat 图标时，按 Esc 键显示启动信息。你会看到此消息：Warning -- SELinux targeted policy label is required。几分钟后，此消息将消失且重新标记完成。这正是为什么你通常应该尝试完全避免禁用 SELinux 模式的原因。

## 使用 SELinux 上下文类型

你已经学习了 `-Z` 选项如何用于许多命令（包括 `ls`、`ps` 和 `netstat`），显示当前的上下文类型。在本节中，你将学习如何为新文件和目录设置上下文。

如果文件在特定目录内创建，它默认继承父目录的上下文。你在练习 8.1 中观察到了这一点。然而，如果文件从一个位置移动到另一个位置，它将保留旧位置的上下文，因为 SELinux 上下文存储在文件系统的扩展属性中。要设置文件的上下文类型，可以使用 `fcontext` 命令。通过此命令，你将新的上下文类型写入策略，但它不会立即更改实际上下文。要应用策略中的上下文类型，随后需要运行 `restorecon` 命令。

> `fcontext` 命令未安装。要使用它，请确保服务器上安装了 `policycoreutils` 和 `policycoreutils-python` 包。或者，如果你不想记住这些包的名字，可以使用 `yum provides semanage`。

## 第 8 章 · 理解与配置 SELinux

```
/.* 所有文件 system-u:object_r:default_t:s0
/..* 普通文件 system-u:object_r:etc_runtime_t:s0
/.autofsc 普通文件 system-u:object_r:etc_runtime_t:s0
/.autorelabel 普通文件 system-u:object_r:etc_runtime_t:s0
/.journal 所有文件 <None>
/.suspended 普通文件 system-u:object_r:etc_runtime_t:s0
/atquota\?\.(user|group) 普通文件 system-u:object_r:quota_db_t:s0
/afs 目录 system-u:object_r:mnt_t:s0
/bin 目录 system-u:object_r:bin_t:s0
/bin/.* 所有文件 system-u:object_r:bin_t:s0
```

有两种方法可以找出你的服务提供了哪些可用的上下文设置：

- 安装服务并查看所使用的默认上下文设置。
- 查阅特定服务的 man 手（帮助文档）。许多服务都有以 _selinux 结尾的 man 手，其中包含了查找正确上下文设置所需的所有信息。

找到特定的上下文设置后，你只需要应用它。要实现这一点，使用 `semanage fcontext -t` 作为第一个参数，随后是你想应用上下文设置的目录或文件名称。为了将上下文应用到你目标目录中已存在的所有内容，你需要在目录名称后添加正则表达式 `(.*?)`。这意味着在优化的情况下，匹配项后将跟任意字符。

![](img/3a7e027360b64bc83d5cf9a2db902251_265_0.png)

> 如果你觉得很难记住 `semanage fcontext` 命令的语法，请查看 man 手。你会在 man 手末尾找到一个示例列表，展示如何使用该命令。

你永远无法记住所有可用的类型上下文。默认就有超过 3000 个！你可以使用 `seinfo -t` 命令获取这些内容的概述。在练习 8.3 中，你将学习如何为服务器应用文件上下文。

## 练习 8.3

### 应用文件上下文

在此练习中，你将使用 `semanage fcontext` 和 `restorecon` 应用文件上下文。你会发现第一次尝试时，使用非默认文档根的 Web 服务器无法工作。更改 SELinux 上下文后，它就能正常运行。

- 1. 使用 `yum install policycoreutils policycoreutils-python` 确保已安装包含 `semanage` 和 `restorecon` 的包。
- 2. 使用 `mkdir /web`，然后通过 `cd /web` 激活该目录。
- 3. 使用编辑器创建 `/web/index.html`，包含“welcome to my website”。
- 4. 使用编辑器打开 `/etc/httpd/conf/httpd.conf`，并将 `DocumentRoot` 行改为 `DocumentRoot "/web"`。
- 5. 使用 `service httpd start` 启动 Apache 服务器。
- 6. 使用 `links localhost` 打开本地 Web 服务器会话。你会收到“Connection refused”（拒绝连接）的消息。按回车键然后按 q 退出 links。
- 7. 使用 `ls -Z /var/www` 查找默认 DocumentRoot 的当前类型，它应该是 `httpd_sys_content_t`。
- 8. 使用 `semanage fcontext -a -t httpd_sys_content_t '/web/(.*)?' ` 并按回车。
- 9. 现在使用 `restorecon -Z` 应用新的上下文。
- 10. 使用 `ls -Z /web` 显示 `/web` 目录中文件的上下文。你能看到哪里出问题了吗？
- 11. 使用 `restorecon -R /web` 将新上下文递归应用到 `/web` 目录。类型上下文已正确设置。
- 12. 使用 `service httpd restart` 重启 Web 服务器。你应该能够访问 `/web` 目录的上下文。
- 13. 使用编辑器打开 `/etc/httpd/conf/httpd.conf` 文件，确保 DocumentRoot 设置为 `/var/www/html`。

#### 配置 SELinux 策略

编写策略是专家的工作，本身就值得写一本书。更改策略行为的一种方法是使用布尔值（Booleans）。布尔值是你用来更改策略设置的开关。要找出你可用的布尔值，有以下三种方案：

- 使用你想要配置的服务 man 手。许多服务都有以 _selinux 结尾的 man 手，包含你所需的信息。
- 使用 `getboolean -a` 显示当前所有可用布尔值列表。使用 `grep` 过滤出特定于你想要配置的服务的布尔值。布尔值的名称很好地说明了用途。
- 使用 `semanage boolean -a` 显示所有布尔值列表。该命令的输出与 `getboolean -a` 类似，区别在于描述通常更长。

一旦找到了想要设置的布尔值，就可以使用 `setsebool`。在使用 `setsebool` 时，始终使用 `-P` 选项是非常重要的。

## 练习 8.4

配置 SELinux 策略

一旦找到了想要设置的布尔值，就可以使用 `setsebool`

## 练习 8.4

### 处理 SELinux 布尔值

在此练习中，你将学习如何处理 SELinux 布尔值。你会发现可用的布尔值：

- 使用你想要配置的服务 man 手。许多服务都有以 _selinux 结尾的 man 手，包含你所需的信息。
- 使用 `getboolean -a` 显示当前所有可用布尔值列表。使用 `grep` 过滤出特定于你想要配置的服务的布尔值。布尔值的名称很好地说明了用途。
- 使用 `semanage boolean -a` 显示所有布尔值列表。该命令的输出与 `getboolean -a` 类似，区别在于描述通常更长。

一旦找到了想要设置的布尔值，就可以使用 `setsebool`。在使用 `setsebool` 时，始终使用 `-P` 选项是非常重要的。这会将设置持久化到磁盘。

## 练习 8.4

### 处理 SELinux 布尔值

在此练习中，你将学习如何处理 SELinux 布尔值。你会发现可用的布尔值：

- 使用你想要配置的服务 man 手。许多服务都有以 _selinux 结尾的 man 手，包含你所需的信息。
- 使用 `getboolean -a` 显示当前所有可用布尔值列表。使用 `grep` 过滤出特定于你想要配置的服务的布尔值。布尔值的名称很好地说明了用途。
- 使用 `semanage boolean -a` 显示所有布尔值列表。该命令的输出与 `getboolean -a` 类似，区别在于描述通常更长。

一旦找到了想要设置的布尔值，就可以使用 `setsebool`。在使用 `setsebool` 时，始终使用 `-P` 选项是非常重要的。这会将设置持久化到磁盘。

## 处理 SELinux 模块

Red Hat Linux 的 SELinux 实现是模块化的。这意味着实现策略的并不是单一的，而是由较小的模块组成。引入 SELinux 模块的概念是为了让第三方能够与之兼容。要获取 SELinux 模块的概述，可以使用 `semodule -l`。管理员也可以启用或禁用模块。要禁用某个模块，使用 `semodule -d`。如果你想再次启用，使用 `semodule -e`。

## 使用 system-config-selinux 设置 SELinux

你已经读过一些命令行工具。如果你不喜欢命令行界面，还有一个名为 system-config-selinux 的图形工具。该工具位于 `policycoreutils-gui` 包中在启动它之前确保已安装。

`system-config-selinux` 工具方便地提供了你从命令行学习的大多数选项。但它有一个重要的缺点：你从 `system-config-selinux` 写入策略的任何内容都会立即写入。这意味着你不能连续点击几十个选项；选择一个选项后，策略立即更新，你必须等待。

## 排除 SELinux

正如你在本章前面提到的，许多管理员关闭 SELinux 是因为它阻止了他们做想做的事。然而，关闭 SELinux 会带来巨大的风险。更好的做法是保持开启，并在它阻止你执行特定任务时进行分析。如果 SELinux 是某些功能无法工作的原因，日志消息会发送到 `/var/log/audit/audit.log` 日志文件（前提是审计服务正在运行）。如果你看到空的 `/var/log/audit`，请检查审计服务是否运行 (`auditd`) 并已启用 (`chkconfig | grep audit`)。此外，你需要安装 `troubleshoot` 包才能在 audit.log 中看到任何内容。audit.log 文件中的消息不幸的是很难阅读的。8.4 显示了这种示例。

# 第 8 章 理解与配置 SELinux
