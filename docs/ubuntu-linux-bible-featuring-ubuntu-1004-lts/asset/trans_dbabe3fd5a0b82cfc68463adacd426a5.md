

## 第 27 章：管理用户、组和认证

使用标准的 /etc/passwd 和 /etc/shadow 密码认证，该文件包含以下 PAM 规则：

```
password [success=1 default-ignore] pam_unix.so obscure sha512
password requisite pam_deny.so
password required pam_permit.so
```

这调用了 pam_unix.so 模块来检查 /etc/passwd 中是否存在有效用户，并将该用户的密码与 /etc/shadow 文件中找到的加密密码条目进行测试。`obscure` 参数指定在更改密码时将执行某些检查，例如验证新密码是否为旧密码的回文或循环位移版本、新密码在大小写上是否与旧密码不同，以及新密码是否与旧密码“相似”（我个人从未查看过代码来确定如何判断相似性，但其规则似乎相当晦涩）。`sha512` 指定了将用于加密密码的加密算法。PAM 必须成功，但仅凭本身不足以允许用户登录。如果此规则成功，则文件中的其他规则将不再被调用。如果第一条规则失败，第二条规则将立即返回失败以阻止认证。第三条规则如果在密码栈上已存在正值返回则保持不变，但按理不应存在。

- 15. 调用带有 `open` 参数的 pam_selinux.so 模块，为登录会话打开一个新的 SELinux 上文。

## 备注

在 /etc/pam.d/common-password 文件中列出了其他密码检查和密码强度 PAM，但它们被注释掉了。你可能不想取消这些注释，除非注释掉原始的 `pam_unix.so` 条目；例如，你可能想利用 `pam_cracklib.so` 模块执行的字典检查，这些检查虽然很烦人，但能确保密码不会是字典中常见的词汇。

一旦 `/etc/pam.d/login` 文件（以及它包含的文件）中指定的所有 PAM 都成功完成，登录过程将继续，创建用户的登录会话，并执行用户登录配置文件中的任何其他启动操作。

上所述，PAM 认证过程可能非常复杂，且容易导致头痛。尽管这很痛苦，但安全是任何系统管理员最重要的责任之一。你几乎不会在家庭 Linux 系统上乱动 PAM 配置文件，但在企业或学术环境中使用 Ubuntu 时，你可能需要修改它们（并且一定要理解它们）。如果说有什么可以慰藉的话，想想如果没有 PAM 提供的灵活性，实现所有这些功能的代码将会是多么复杂。

## 各种 PAM 的配置文件

/etc/pam.d 中的文本格式文件控制着与每个感知认证的应用程序或服务相关的 PAM。正如在上一节探索 `/etc/pam.d/login` 文件时所提到的，其中一些 PAM 使用可选的配置文件来进一步细化其行为。单个 PAM 的配置文件位于 `/etc/security` 目录。虽然这些文件必须存在，但它们不需要包含任何有用信息——它们的存在是为了以防你想利用它们提供的高级配置选项。以下是 Ubuntu 系统上找到的该目录下的文件列表：

- access.conf：为登录提供细粒度的访问控制，并被 `pam_access.so` 模块使用。
- group.conf：提供基于会话的组 Membership控制，并被 `pam_group.so` 模块使用。
- limits.conf：提供一种设置系统资源限制的逐用户机制；被 `pam_limits.so` 模块使用。
- namespace.conf：定义如果使用 `pam_namespace.so` 模块支持 SELinux 多级安全（MLS）策略将将多实例化（polyinstantiated）的目录。多实例化目录通常是系统目录和用户目录。多实例化和命名空间意味着查看共享资源的用户将根据用户名、角色、安全级别等看到不同的内容。
- namespace.init：包含一个 shell 脚本，如果使用 `pam_namespace.so` 模块支持 SELinux 多级安全（MLS）策略将执行该脚本。Ubuntu 系统提供的此默认脚本确保在创建新用户账户时，`/etc/skel` 的内容会被复制到多实例化目录。
- passwd：包含各种用户最近使用过的密码列表，以防止重复使用密码。此文件本身并不是 PAM 配置文件，但会被 `pam_cracklib.so` 等 PAM 使用。只有当 `/etc/pam.d/common-password` 配置行带有 `remember=N` 选项时，此文件才会被使用，其中 N 是你希望系统为每个用户记住之前的密码哈希数量。
- pam_env.conf：提供一种设置环境变量值的机制；被 `pam_env.so` 模块使用。
- time.conf：提供一种对系统服务和应用程序实施通用或用户特定限制的机制；被 `pam_time.so` 模块使用。

如果你安装了其他认证系统及其相关的 PAM，与其他 PAM 相关的配置文件也可能安装在 `/etc/security` 中。本节仅列出了标准 Ubuntu 安装提供的默认配置文件。

## 如果 PAM 配置文件缺失了怎么办？

PAM 为各种应用程序提供了一种非常强大的认证机制，并确保只有正确的用户从正确的设备运行它们。因此，很容易看出，正确配置特定应用程序的 PAM 非常重要。但如果某个应用程序使用了 PAM，而你忘记创建它的 PAM 配置文件，或者该文件由于某种意外删除了怎么办？为了涵盖这些情况，Linux-PAM 库为任何没有自己配置文件的应用程序和服务提供了一个默认配置文件。这就是 `/etc/pam.d/other` 文件，它在标准 Ubuntu 系统上具有以下有效条目：

```
@include common-auth
@include common-account
@include common-password
@include common-session
```

这些文件的每个内容在本章之前讨论过，即“示例：登录过程使用的 PAM”章节。在 Ubuntu 系统上，`/etc/pam.d/other` PAM 配置文件默认提供了一组合理的默认值，用于验证随机程序至少是由能够成功登录并向系统认证身份的人执行的，并保证为该用户创建各种日志条目。

## 提示

由于 PAM 配置文件配置不当通常意味着系统配置错误，或者意味着有人在没有深思熟的情况下导入了感知 PAM 的二进制文件，你可以通过更改 `/etc/pam.d/other` 文件来禁用访问并实施极端的偏执安全策略，将其改为以下条目：

```
auth required pam_deny.so
auth required pam_warn.so
account required pam_deny.so
account required pam_warn.so
password required pam_deny.so
password required pam_warn.so
session required pam_deny.so
session required pam_warn.so
```

由于同一模块类型的后续 `required` 条目都会被执行，因此每个模块类型条目首先执行 `pam_deny.so` PAM（拒绝对请求服务的访问），然后执行 `pam_warn.so` PAM（向系统日志输入警告信息）。这些日志条目将帮助你识别问题，如果一个挑剔的用户还没有搜索并询问为什么他们无法再次运行他们导入的某个晦涩二进制文件的话。■

## 自定义 sudo 命令

正如第 4 章中“执行特权操作”节介绍的那样，Ubuntu 不使用传统的 root 账户来执行特权操作，而是需要 admin 组成员的用户通过指定自己的密码来执行所有特权操作。在这些系统上禁用 root 账户（及其传统伙伴 sudo 命令）的原因在 Ubuntu 官方文档中有讨论：https://help.ubuntu.com/community/RootSudo。为了节省你查询 Web 的时间，这是

