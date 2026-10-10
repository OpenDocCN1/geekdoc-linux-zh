
规则存储在策略 `src` 目录下各种子目录中的配置文件中。在该目录下，你会找到 `policy/modules` 子目录。它组织为多个目录：`admin`、`apps` 等其他，你会在其中找到 `.tc`、`.fc` 和 `.if` 配置文件。

| 目录和文件 | 描述 |
| :--- | :--- |
| `config/app` | 应用模块 |
| `policy/booleans` | 可调优功能 |
| `policy/flask` | Flask 强制 |
| `policy/mcs` | 多级安全 |
| `policy/doc` | 文档 |
| `policy/modules/admin` | 管理模块 |
| `policy/modules/apps` | 应用模块 |
| `policy/modules/kernel` | 内内核模块 |
| `policy/modules/services` | 服务模块 |
| `policy/modules/system` | 系统模块 |
| `policy/rolemap` | 角色映射 |
| `config/local.users` | 用户定义 |
| `policy/constraints` | 额外约束 |
| `policy/global` | 全局调优 |
| `policy/mls` | 多级安全 |

### 表 17-3 SELinux 策略配置文件

# 第四部分：安全

## 第 17 章：增强安全型的 Linux：SELinux 391

### 接口文件 (Interface Files)

文件接口允许允许工具生成模块。在这里你可以找到 `/usr/share/selinux` 中的对象和文件类型，带有 `.te` 和 `.fc` 文件。

### 类型文件 (Types Files)

目标策略（`targeted policy`）中，`modules` 目录持有对象类型。`.te` 文件不再包含在标准的 SELinux 安装中。相反，请下载并安装 `refpolicy` 包。

### 模块文件 (Module Files)

模块位于 `policy/modules` 下的多个子目录。在这里你会为每个模块找到三个文件：一个 `.te` 文件、一个 `.if` 文件以及定义上下文的 `.fc` 文件。

### 安全上下文文件 (Security Context Files)

不同文件的安全上下文在安全上下文文件中详细说明。`file_contexts` 文件持有不同组、目录和文件的安全上下文。每个配置文件都有 `.fc` 后缀。在 SELinux 策略源码中，每个模块将有自己的 `.fc` 文件，以及相应的 `.te` 和 `.if` 文件。

### 用户配置：角色 (User Configuration: Roles)

全局用户配置在策略目录下的用户文件中定义。在这里你可以找到用户定义以及标准用户（`user_u`）和管理员（`admin.u`）的角色。要添加你自己的用户，使用 `local.users`。严格和目标策略都使用通用 `user_u` SELinux 身份。要为用户设置特定的 SELinux 身份，你需要在 `local.users` 中定义该用户。

`rbac` 文件定义了可以转换的角色。例如，用户角色可以转换到系统管理员角色？目标策略有多个定义允许用户自由转换到管理员，反之亦然。严格策略没有此类定义。

角色转换受约束文件中的规则限制。在这里，对其他用户的更改受到控制，并且对对象安全上下文（标记）的更改受到限制。

### 策略模块工具

要创建并加载策略模块，你需要使用几个策略模块工具。首先，使用 `checkmodule` 命令从 `.te` 文件创建 `.mod` 文件。然后，`semodule` 软件包获取 `.mod` 文件和任何支持的 `.fc` 文件，生成模块策略包文件 `.pp`。最后，`semodule` 工具可以获取策略包文件并作为 SELinux 策略的一部分进行安装。

### 应用配置：appconfig

某些服务和应用程序具有感知能力，并会向 SELinux 请求默认的安全上下文和类型（请参阅接下来的章节“运行时安全上下文和类型：上下文”）。配置保存在 `policy/config/appconfig-` 目录下的文件中。`default_types` 文件存储策略默认值；`default_contexts` 存储默认安全上下文。`intric_context` 文件持有 `/etc/rc` 脚本的默认安全上下文。一个特殊的 `root_context` 文件持有 root 用户如何被访问。`removable_context` 持有可移除设备的安全上下文，而 `media` 列出媒体设备（如 CD-ROM）。运行时值也可以注册到 `policy contexts` 目录下的文件中，例如 `/etc/selinux/targeted/contexts`。

### 创建 SELinux 策略：make 和 checkpolicy

如果你想创建一个全新的策略，请使用 SELinux 引用策略源 `/etc/selinux/refpolicy`。如果你已经配置了策略，可以使用 `make policy` 和 `checkpolicy` 命令来创建它。`make policy` 命令为你的配置文件生成一个 `policy.conf` 文件，然后 `checkpolicy` 可以使用该文件生成策略二进制文件。策略二进制文件将在 `policy` 子目录中创建，并带有与新策略相符的数字扩展名，例如 `policy.20`。

你将生成一个新的策略文件 `policy.conf`。要实现这一点，请在策略 `src` 目录（即 `/etc/selinux/refpolicy/src/`）中输入以下命令：

```
make policy
```

然后你可以使用 `checkpolicy` 创建新策略。

与其在每次想要更改时都编译源码，你只需为你更改的区域编译一个模块。在之前的 SELinux 版本中，每次进行更改都必须重新构建整个策略。模块位于不同的目录。每个模块都从 `.te` 文件构建。`checkmodule` 命令用于从 `.te` 文件创建 `.mod` 文件，`semodule` 命令用于创建可加载的策略包 `.pp` 文件。正如 SELinux 文档所述，如果你只需要使用 `syslog` 修改配置，首先将使用以下命令通过 `syslog.te` 创建 `syslog.mod` 文件。`-M` 选项指定对 MLS 安全级别的支持。

```
checkmodule -M -m syslog.te -o syslog.mod
```

然后使用 `semanage_module` 从 `syslogd.mod` 文件创建 `syslogd.pp` 文件。`-f` 选项指定文件上下文。

```
semanage_module -m syslogd.mod -o syslogd.pp -f syslogd.fc
```

使用 `semodule` 和 `-i` 选项添加模块。你可以使用 `-l` 选项检查模块是否加载。

```
semodule -i syslogd.pp
```

对基础策略的更改是在 `policy.conf` 文件中进行的，它会被编译到基础 `.pp` 模块中。

为了执行配置，现在需要从 `SRPMS` 目录下载 `selinux-policy` 源码。用于配置 SELinux 的 `.te` 文件不再是 SELinux 二进制包的一部分。使用的文件将安装到 `/usr/src/redhat/redOS`。（确保你已经安装了 `rpm-build`；它默认不安装）。安装完成后，源码将位于 `/etc/selinux` 下的 `policy` 目录。使用源码文件的文档包含在另一个 SRPMS 文件中，名为 `selinux.doc`。

对于 `fixfiles`，你使用：

```
fixfiles relabel
```
