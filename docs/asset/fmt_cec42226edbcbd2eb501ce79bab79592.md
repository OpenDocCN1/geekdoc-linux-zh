
当 SELinux 拒绝访问文件或应用程序时，内核会发布 AVC 通知。很多情况下，只需通过重命名文件的安全上下文来允许访问即可解决问题。使用 `chcon` 命令更改文件的安全上下文。在此重命名中，需要为 Samba 服务器授予 `/var/lib/samba` 目录下的 `log.richard3` 文件的权限。SELinux 故障排除器本身不会采取行动，而是会建议可能的措施。在示例中，用户仅执行了以下 `chcon` 命令：

```bash
chcon -R -t samba_share_t log.richard3
```

更复杂的问题（尤其是未知问题）可能需要您使用审计日志中的 AVC 消息创建一个新的策略模块。要做到这一点，您可以使用 `audit2allow` 命令。内核将获取 AVC 消息并生成用于允许 SELinux 访问的命令。审计日志为 `/var/log/audit/audit.log`。此日志被输出到 `audit2allow`，然后该命令使用 `-M` 选项创建一个策略模块。

```bash
cat /var/log/audit/audit.log | audit2allow -M local
```

然后，您将使用 `semodule` 命令加载该模块。

如果您想先编辑允许的条目，可以使用以下命令创建本地模块的 .te 文件（`local.te`），然后您可以对其进行编辑：

```bash
audit2allow -m /var/log/audit/audit.log > local.te
```

一旦编辑了 .te 文件，您就可以使用 `checkmodule` 编译它，然后使用 `semodule_package` 创建策略模块 `local.pp`。随后，您可以使用 `semodule` 安装它。您首先用 `checkmodule` 创建 .mod 文件，然后用 `semodule_package` 创建 .pp 文件。

```bash
checkmodule -m -o local.mod.te
semodule_package -o local.pp -m local.mod
semodule -i local.pp
```

在此示例中，策略模块仅被命名为 `local`。如果您以后想用 `audit2allow` 创建新模块，您应该使用不同的名称，或者直接使用 `-option` 选项将输出追加到 .te 文件中。

## 基于角色的访问控制

基于角色的方法侧重于控制用户。用户被分配特定的角色，这些角色定义了他们可以使用哪些资源。在标准系统中，文件权限（例如针对组的）可以控制用户对文件和目录的访问。通过角色，权限变得更加灵活和精细化。某些用户对服务的访问权限可以高于其他用户。

## SELinux 用户

用户将保留标准系统中可用的权限。此外，SELinux 可以为给定的用户设置自身的控制策略，为该用户定义一个角色。SELinux 创建的通用安全身份：

```
system_u 用于系统进程的用户
user_u 允许普通用户使用服务
root 用于 root 用户
```

## 策略文件

策略在策略文件中实现。这些是根据源文件编译而成的二进制文件。对于一个预配置的策略文件，策略二进制文件位于 `/etc/selinux` 配置目录下的策略子目录中，即 `/etc/selinux/targeted`。例如，targeted 策略的策略文件为：

`/etc/selinux/targeted/policy/policy.20`

包含接口文件的 targeted 开发文件安装在 `/usr/share/selinux/targeted`。

你可以使用开发文件创建自己的策略模块，然后加载它们。

## SELinux 配置

通用 SELinux 服务器设置的配置在 `/etc/selinux/config` 目录下进行。目前只有两个设置需要完成：状态和策略。将 `SELINUX` 变量设置为相应的状态（例如 `enforcing` 强制或 `permissive` 允许），并将 `SELINUXTYPE` 变量设置为你想要的策略类型。这些对应于 Securitylevel-config 中 SELinux 的禁用和启用设置，以及如 `targeted` 这样的策略。示例配置文件如下：

```
# 此文件控制系统上 SELinux 的状态。
# SELINUX= 可以取以下三个值之一：
# enforcing - 强制 SELinux 安全策略。
# permissive - SELinux 打印警告而非强制。
# disabled - 完全禁用 SELinux。
SELINUX=permissive
# SELINUXTYPE= 正在使用的策略类型。可能的值有：
# targeted - 仅保护目标网络守护进程。
# strict - 全 SELinux 保护。
SELINUXTYPE=targeted
```

## 第 12 章：SELinux 243

## SELinux 策略规则

策略规则可以由类型（类型强制）或 rbac（基于角色的访问控制）语句组成，以及安全级别（多级安全）。类型语句可以是类型定义或属性的声明，也可以是转换、更改或断言规则。rbac 语句可以是角色声明或允许规则。安全级别指定了一个与许可访问级别相对应的数字。策略配置可能非常困难，包含大量复杂的规则。由于由于原因，许多规则是通过文件中的 M4 宏实现的，这些文件反过来生成相应的规则（Sendmail 以类似的方式使用 M4 宏）。你可以在 SELinux 参考策略源码包中找到这些规则，你需要下载并安装它。参考策略包是 `selinux-policy`，位于 Fedora 的 RPMS 源码仓库中。请参阅后续关于 SELinux 配置文件的章节。

## 类型和角色声明

类型声明以关键字 `type` 开头，后跟跟类型名称（标识符）以及任何可选的属性或别名。类型名称将带有 `_t` 后缀。包含了针对文件等对象的标准类型定义。以下是任何文件的默认类型，具有属性 `file_type` 和 `sysadfile`：

```
type file_t, file_type, sysadfile;
```

root 拥有它自己的类型声明。

```
type root_t, file_type,
```

`boot` 等特殊目录也有它们自己的类型。

```
type boot_t, sysadfile;
```

针对 Amanda 服务器等特定目标设置了更专门的规则。以下示例是 `amanda_t` 对象的通用类型定义，这些对象是 Amanda 备份服务器使用的，列在 targeted 策略的 `src/program/amanda.te` 文件中。

```
type amanda_t, domain, privlog, amanda, nscd_client_domain
```

角色声明决定了访问特定类型对象的规则。这些规则以关键字 `role` 开头，随后是角色以及与角色相关的对象。在此示例中，具有系统角色（`system_r`）的用户或进程可以访问 amanda 对象（`amanda_t`）。

```
role system_r types amanda_t;
```

可执行文件提供了更具体的类型声明，例如针对 Amanda 服务器的（`amanda_exec_t`）。这把 Amanda 可执行文件定义为系统管理控制的可执行文件。

```
type amanda_exec_t, file_type, sysadfile, exec_type;
```

关联的配置文件通常有自己的规则。

```
type amanda_config_t, file_type, sysadfile;
```

在 targeted 策略中，创建了一个通用的无限制类型（unconfined），用户和系统角色可以访问它，从而对系统拥有完全不受限制的访问。更具体的规则将限制对 Web 服务器等特定目标的访问。

```
type unconfined_t, domain, privuser, privhome, privrole, pivowner, admin,
auth_write, fs_domain, pivim;
role system_r types unconfined_t;
role user_r types unconfined_t;
role sysadm_r types unconfined_t;
```

为用户主目录中创建的文件也设置了类型。

```
（注：此处原文未提供具体代码块内容，根据上下文逻辑可推断或省略）
```

## SELinux 策略配置文件

配置文件通常使用 `.te` 和 `.fc` 文件进行更改。这些文件在 `/usr/share/selinux` 的模块头文件中缺失的。如果你正在添加一个模块，将需要为其创建 `.te` 和 `.fc` 文件。你可以在下一节中创建一个模块并添加它。如果你想创建或修改自己的策略，需要按照后文的描述下载并安装 SELinux 参考策略的源码文件。参考策略代码包含了全套 `.te` 和 `.fc` 配置文件。

## 编译 SELinux 模块

你不需要在每次想要更改时编译整个源码，只需针对你更改的区域编译一个模块。`modules` 目录包含了不同的模块。每个模块都由相应的 `.te` 文件构建，并使用 `semanage` 模块从 `.te` 创建可加载的 `.pp` 模块文件，以及创建一个 `.fc` 文件上下文。与 SELinux 文档一样，如果你需要更改 `rsyslog` 的配置，首先可以使用以下命令使用 `rsyslogd.te` 创建一个 `rsyslog.mod` 文件。`-M` 选项支持 MLS 安全级别的策略。

```
checkmodule -M -m rsyslogd.te -o rsyslogd.pp
```

然后使用 `semanage` 模块从 `rsyslogd.mod` 文件创建 `rsyslogd.pp` 文件。`-f` 选项指定文件上下文。

```
semanage -m rsyslogd.mod -o rsyslogd.pp
```

使用 `semodule` 和 `-i` 选项添加模块。你可以通过 `-i` 选项检查模块是否已加载。

```
semodule -i rsyslogd.pp
```

对基础策略的更改通过 `policy.conf` 文件进行，它会被编译到 `base.pp` 模块中。

## 使用 SELinux 源码配置

要执行你自己的配置，必须从 `SRPMS` 目录（源码）下载并安装 `selinux-policy` 源码文件。用于配置 SE 策略的 `.te` 文件已不再是 SELinux 二进制包的一部分。

一旦下载了 SRPMS 文件，你需要在终端窗口中使用带有 `-i` 选项的 `rpm` 命令来安装源码。

```
rpm -i selinux-policy-2.3.18-10.noarch.rpms
```

源码的压缩包（`.tgz` 文件）以及各种策略配置文件将安装到 `/usr/src/redhat/SOURCES`。（确保你已经安装了 `rpm-build`，它默认没有安装）。使用源码文件的文档位于另一个名为 `selinux-doc` 的 SRPMS 文件中。

你可以使用 `rpmbuild` 操作将文件提取到 `/usr/src/redhat/BUILD` 中的 `serefpolicy` 目录。在该目录下，你会找到一个 `policy/modules` 子目录。在那里，通过 `admin` 和 `apps` 等几个目录组织，你可以找到 `.te`、`.fc` 和 `.if` 配置文件。

```
rpmbuild -bp security-policy.spec
```

然后切换到 `/usr/src/redhat/BUILD/seref-policy` 目录并运行命令将 SELinux 源码安装到 `/etc/selinux/seref-policy/src`。

```
make install-src
```

规则存储在策略的 `src` 目录下各个子目录的配置文件中。在该目录下，你会找到一个 `policy/modules` 子目录。在那里，通过 `admin` 和 `apps` 等几个目录组织，你可以找到 `.te`、`.fc` 和 `.if` 配置文件。

你将拥有类型强制（type enforcement）和安全上下文的配置文件。类型强制文件具有 `.te` 扩展，而安全上下文具有 `.sc` 扩展。

反映了 SELinux 提供的细粒度控制，你对系统上的许多对象和进程拥有大量的配置文件。主要的配置文件和目录列在表 12-3 中，但有几个扩展到了子目录的详细列表。此处（此处为原文重复内容翻译：反映了 SELinux 提供的细粒度控制，你对系统上的许多对象和进程拥有大量的配置文件。主要的配置文件和目录列在表 12-3 中，但有几个扩展到了子目录的详细列表。）

*注：原文此处存在内容重复，已按要求处理。*

将 SELinux 源码安装到 /etc/selinux/seref-policy/src。

```
make install-src
```

规则存储在策略的 `src` 目录下各个子目录的配置文件中。在该目录下，你会找到一个 `policy/modules` 子目录。在那里，通过 `admin` 和 `apps` 等几个目录组织，你可以找到 `.te`、`.fc` 和 `.if` 配置文件。

你将拥有类型强制和安全上下文的配置文件。类型强制文件具有 `.te` 扩展，而安全上下文具有 `.sc` 扩展。

反映了 SELinux 提供的细粒度控制，你对系统上的许多对象和进程拥有大量的配置文件。主要的配置文件和目录列在表 12-3 中，但有几个扩展到了子目录的详细列表。

接口文件

接口文件允许管理工具生成模块。SE Linux 源码将包含相应的 `.te` 和 `.fc` 文件。

类型文件

在目标策略中，`modules` 目录包含了用于各种对象的 `.te` 文件。类型强制文件不再包含在 SELinux 默认安装中。

模块文件

模块位于 `policy/modules` 目录下的各个子目录。这里包含了特定的 `.te` 文件和 `.if` 文件。

安全上下文

不同文件的安全上下文在 `file_contexts` 中。`file_contexts` 文件包含了不同组、目录的安全上下文。具有 `.fc` 扩展。在 SELinux 源码中，每个模块都包含 `.mod` 文件以及 `.if` 文件。

应用配置

某些服务和应用程序具有安全感知，并从 SELinux 请求默认的安全上下文和类型。配置保留在 `policy/config/appconfig-` 目录下的文件类型中。

用户配置

全局用户配置定义在策略目录的 `users(u)` 和管理员中。这里是标准用户（user_u）和管理员（admin_u）的定义。要添加你自己的用户，使用 `local.users` 文件。这里是输入你自己的 SELinux 用户的示例。严格策略和目标策略都使用通用的 SELinux 身份。要为用户设置独立的 SELinux 身份，你需要在 `local.users` 文件中定义该用户。

## 目录与文件

## 说明

| 路径 | 说明 |

| :--- | :--- |

| assert.te | 向量断言 |

| config/appconfig- | 运行时配置文件 |

| policy/booleans.conf | 可调功能 |

| file_contexts | 文件和目录的安全上下文 |

| policy/flask | Flask 配置 |

| policy/mcs | 多类别安全 (MCS) 配置 |

| doc | 策略策略文档支持 |

| policy/modules | 安全模块 |

| policy/modules.conf | 模块列表及使用方法 |

| policy/modules/admin | 管理模块 |

| policy/modules/apps | 应用模块 |

| policy/modules/kernel | 内核模块 |

| policy/modules/services | 服务和服务器模块 |

| policy/modules/system | 系统模块 |

| policy/rolemap | 用户域类型和角色 |

| policy/users | 通用用户定义 |

| config/local.users | 定义您的 SELinux 用户 |

| policy/constraints | 针对角色转换和对象访问的额外约束 |

| policygentool | 生成策略的脚本 |

| policy/global_tunables | 定义用于自定义的策略可调项 |

| policy/mls | 多级安全 (MLS) 配置 |

> 表 12-3: SELinux 策略配置文件

## 创建 SELinux 策略：make 和 checkpolicy

如果您想创建一个新策略，请使用 SE Linux 引用策略源 `/etc/selinux/serefpolicy`。一旦配置了策略，您可以使用 `make policy` 和 `checkpolicy` 命令来创建它。`make policy` 命令会为您的配置文件生成一个 `policy.conf` 文件，然后 `checkpolicy` 可以使用该文件生成策略二进制文件。策略二进制文件将在 `policy` 子目录中创建，并带有表示策略版本的数字扩展名，例如 `policy.20`。

您必须生成一个新的策略 `policy.conf` 文件。要执行此操作，您需要在策略源目录中输入以下命令，该目录为 /etc/selinux/serefpolicy/src/`policy`。

```bash
make policy
```

## 第二部分：安全

然后，您可以使用 checkpolicy 来创建新策略。
