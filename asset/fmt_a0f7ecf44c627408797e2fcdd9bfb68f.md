
角色声明决定了可以访问对象的规则。角色声明可以是角色声明、支配关系或允许。安全级策略配置可能很困难，需要使用大量复杂的规则。由于原因，许多规则以 M4 宏的形式实现在生成相应规则的文件中（`SendCommand` 以类似的方式使用 M4 宏）。你将在位于 SELinux 参考策略源码包的文件中找到这些规则，你需要下载并安装它。参考策略包是 `selinux-policy`，位于 Fedora 的 RPMMS 源仓库中。请参阅后续关于 SELinux 配置文件的章节。

# 第四部分：安全

## 文件上下文

文件上下文将特定文件与安全上下文关联。首先列出文件，使用正则表达式。然后指定角色、类型和安全级。以下为 `/etc` 目录创建所有文件的安全上下文。

```
（此处上下文省略）
```

文件上下文位于 `/etc/selinux/targeted/contexts/file_contexts` 中。

## 用户角色

用户角色定义了角色可以承担什么。角色以关键字 `user` 开始，后跟用户名、关键字 `roles`，最后是它可以使用的角色。你将在 SELinux 参考策略源码文件中找到这些规则。以下是 `system-u` 角色的定义：

```
user system_u roles system_r;
```

如果用户有多个角色，它们列在括号中。以下是目标策略中标准用户的定义，允许用户承担系统管理角色：

```
user user_u roles { user_r sysadm_r system_r };
```

严格策略仅列出了 `user_r` 角色。

```
user user_u roles { user_r };
```

## 访问向量规则：allow

访问向量规则允许定义对象和进程权限。`allow` 关键字后是对象或进程，然后是所使用的权限。以下 `amanda_t` 域中的进程搜索 Amanda 配置目录（任何类型为 `amanda_config_t` 的目录）：

```
allow amanda_t amanda_config_t:dir search;
```

以下示例允许 Amanda 读取用户主目录下的文件：

```
allow amanda_t user_home_type:file getattr read ;
```

下一个示例允许 Amanda 在 amanda 目录中读取、搜索和写入文件：

```
allow amanda_t amanda_data_t:dir read search write ;
```

### 第 17 章：增强型 Linux 安全：SELinux 387

## 角色允许规则 (Role Allow Rules)

角色也可以允许规则。虽然它们可以用于域和对象，但它们通常用于控制角色转换，指定一个角色是否可以转换为另一个角色。这些规则列在 rbac 配置文件中。以下条允许用户转换到系统管理员角色：

```
allow user_r sysadm_r;
```

## 转换和向量规则宏 (Transition and Vector Rule Macros)

类型规则设置了用于创建对象的类型。转换规则还需要相应的访问向量规则来启用对象或进程的权限。与其创建单独的规则，可以使用宏来生成所需的规则。以下示例使用 `file_type_auto_trans` 设置了主目录中用户文件的转换和访问规则：

```
file_type_auto_trans (privhome, user_home_dir, user_home_t);
```

下一个示例设置了创建进程的进程转换和访问规则：

```
domain_auto_trans (inetd_t, amanda_inetd_exec_t, amanda_t);
```

## 约束规则 (Constraint Rules)

为了确保更高的安全性，可以对进程转换进行进一步的限制。这些限制是通过约束文件中的约束定义实现的。约束规则通常应用于转换操作，例如要求在进程转换过程中用户身份保持不变，或者进程 1 处于具有 `privilege` 属性的域，而进程 2 处于具有 `userdomain` 属性的域。字符 `u`、`t` 和 `r` 分别代表用户、类型和角色。

```
const process transition
( u == u2 or ( t1 == pivuser and t2 == userdomain )
```

## SELinux 策略配置文件

配置文件通常使用 `.te` 和 `.fc` 文件进行更改。如果你正在添加一个位于 `/usr/share/selinux` 的模块，则模块头文件中将缺少这些文件。你需要为它创建 `.te` 和 `.fc` 文件。然后你可以像下一节描述的那样创建一个模块并加载它。

## 第四部分：安全

如果你想创建或修改你的策略，将按照后续章节的描述下载并安装 SELinux 参考策略的源码文件。参考策略代码包含了完整的 `.te` 和 `.fc` 配置文件。

## 编译 SELinux 模块

不需要在每次更改时都编译源码，你只需要为你更改区域编译一个模块。`modules` 目录存放不同的模块。每个模块都由相应的 `.te` 文件构建。`checkmodule` 命令用于从 `.te` 文件创建 `.mod` 文件，`semanage_module` 命令用于创建可加载的 `.mod` 文件以及 `.fc` 文件上下文。如 SELinux 文档所述，如果你只需要更改 syslog 的配置，-M 选项指定使用 `syslog.te` 支持 `syslog.mod` 文件。

```
checkmodule -M syslog.te -o syslog.mod
```

然后使用 `semanage_module` 命令从 syslog `.mod` 文件创建 `syslog.pp` 文件。-f 选项指定策略文件内容。

```
semanage_module -m syslog.mod -o syslog.pp -f syslog.fc
```

要将其添加到模块，你需要使用 `semodule` 和 -i 选项。你可以使用 -1 选项检查模块是否已加载。

```
semodule -i syslog.pp
```

对基础策略的更改是在 `policy.conf` 文件进行的，它会被编译成 `base.pp` 模块。

## 使用 SELinux 源码配置

要执行配置，你必须从 SRPMS 目录（源码）下载并安装 `selinux-policy` 源码。用于配置 SELinux 的 `.te` 文件不再是 SRPMS 二进制包的一部分。

一旦下载了 SRPMS 文件，你需要在终端中使用带有 -i 选项的 `rpm` 命令安装源码。

```
rpm -i selinux-policy-2.3.18-10.noarch.rpms
```

源码的压缩包（tgz 文件）以及策略配置文件将安装到 `/usr/src/redhat/SOURCES`。请确保你已经安装了 `rpm-build`；它默认不安装。使用源码文件的文档出现在另一个源码 SRPMS 文件中，称为 `selinux-doc`。

你可以通过 `rpmbuild` 操作将文件提取到 `/usr/src/redHAT/` 下的 `refpolicy` 目录。在该目录下，你会找到 `policy/modules` 子目录。它组织为多个目录：admin、apps 等其他，你会在其中找到 `.tc`、fc 和 `.if` 配置文件。

```
rpmbuild -bp security-policy.spec
```

### 第 17 章：增强型 Linux 安全：SELinux 389

然后你切换到 `/usr/src/redhat/BUILD/serif-policy` 目录并运行以下命令将 SELinux 源码安装到 `/etc/selinux/serefpolicy/src`：

```
make install-src
```
