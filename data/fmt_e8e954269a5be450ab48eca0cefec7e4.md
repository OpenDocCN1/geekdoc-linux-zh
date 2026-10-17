
将 SSH 访问限制为仅允许该权限的账户。例如，你可以创建一个名为 `"sshlogin"` 的组，并将该组名作为值关联到 `/etc/ssh/sshd_config` 文件中的 `AllowGroups` 变量。

`AllowGroups sshlogin`

然后将你允许的 SSH 用户添加到 `"sshlogin"` 组，并重启 SSH 服务。

```bash
sudo adduser username sshlogin
```

```bash
sudo systemctl restart sshd.service
```

## 外部用户数据库认证

大多数企业网络要求对所有系统资源进行集中认证和访问控制。如果你配置了服务器通过外部数据库验证用户身份，请务必在外部和本地同时禁用用户账户。这样可以确保无法进行本地回退认证。

## AppArmor

AppArmor 是一个基于名称的强制性访问控制的 Linux 安全模块实现。AppArmor 将单个程序限制在一组列出的文件、端口和特定的能力范围内。

AppArmor 默认安装并加载。它使用应用程序的配置文件来确定应用程序所需的文件和权限。某些软件包将安装它们自己的配置文件，可以在 `apparmor-profiles` 软件包中找到额外的配置文件。

在终端提示符中安装 `apparmor-profiles` 软件包：

```bash
sudo apt install apparmor-profiles
```

AppArmor 有两种执行模式：

- 投诉/学习（Complaining/Learning）：允许并记录违反策略的行为。适用于测试和开发新配置。
- 强制/限制（Enforced/Confined）：限制配置策略并记录违规行为。

## 使用 AppArmor

可选的 `apparmor-utils` 软件包包含了命令行工具，你可以使用这些工具更改 AppArmor 的执行模式、配置状态、创建新配置等。

- `apparmor_status` 用于查看 AppArmor 配置文件的当前状态。
```bash
sudo apparmor_status
```

- `aa-complain` 将配置放入投诉模式。
```bash
sudo aa-complain /path/to/bin
```

- `aa-enforce` 将配置放入强制模式。
```bash
sudo aa-enforce /path/to/bin
```

- `/etc/apparmor.d` 目录是 AppArmor 配置文件所在的位置。它可以操作所有配置文件的模式。

输入以下命令将所有配置放入投诉模式：
```bash
sudo aa-complain /etc/apparmor.d/*
```

将所有配置放入强制模式：
```bash
sudo aa-enforce /etc/apparmor.d/*
```

- `apparmor_parser` 用于将配置加载到内核中。它还可以用于修改配置后使用 `-r` 选项重新加载当前配置以使更改生效。重新加载配置：
```bash
sudo apparmor_parser -r /etc/apparmor.d/profile.name
```

- `systemctl` 可重新加载所有配置：
```bash
sudo systemctl reload apparmor.service
```

- `/etc/apparmor.d/disable` 目录可以配合 `apparmor_parser -R` 选项禁用配置。
```bash
sudo ln -s /etc/apparmor.d/profile_name /etc/apparmor.d/disable/
sudo apparmor_parser -R /etc/apparmor.d/profile_name
```

要重新启用已禁用的配置，请删除 `/etc/apparmor.d/disable/` 中配置的符号链接。然后使用 `-a` 选项加载配置。
```bash
sudo rm /etc/apparmor.d/disable/.name
cat /etc/apparmor.d/profile_name | sudo apparmor_parser -a
```

- 可以通过以下命令禁用 AppArmor 并卸载内核模块：`systemctl stop apparmor.service`

- 重新启用 AppArmor：`systemctl enable apparmor.service`

### 注意

修改配置后，需要将 `profile.name` 替换为想要配置的名称。

## 配置文件

AppArmor 配置文件是位于 `/etc/apparmor.d/` 的简单文本文件。文件名根据可执行文件的完整路径命名。例如对于 `/bin/ping` 命令。

配置文件中使用了两种类型的规则：

- 路径项（Path entries）：详细说明应用程序可以访问。
- 能力项（Capability entries）：确定进程允许使用的权限。

作为一个示例，查看 `/etc/apparmor.d/bin.ping`：

```
#include <tunables/global>

/bin/ping flags=(complain) {

#include <abstractions/base>

#include <abstractions/consoles>

#include <abstractions/nameservice>

capability net_raw,

capability setuid,

network inet raw,

/bin/ping mixer,

/etc/modules.conf r,

}
```
