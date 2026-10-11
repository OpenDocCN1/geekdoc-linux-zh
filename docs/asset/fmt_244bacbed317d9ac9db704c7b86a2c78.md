
你可以修改这些系统事件配置文件来实现你组织特定的安全需求。例如，可以修改 `system-auth-ac` 文件来处理某些密码限制。

> 警告：错误地修改 PAM 系统事件配置文件可能会导致你被锁在自己的系统之外。在修改生产服务器之前，请务必在虚拟或测试环境中对其进行测试。

这些 PAM 系统事件配置文件的运行方式与 PAM 感知应用程序配置文件完全相同。它们具有相同的格式，使用相同的语法，并调用 PAM 模块。然而，其中许多文件是符号链接（参见第 4 章“文件系统中的移动”）。因此，在对这些配置文件进行更改时，需要额外的步骤。具体的实现方法将在本章稍后介绍。

# 第五部分：学习 Linux 安全技术

尽管 Linux 已经预装了许多 PAM 感知应用程序、各种配置文件和 PAM 模块，但你不能只希望 PAM 自动处理一切。管理 PAM 需要某些特定的管理步骤。

## 在你的 Linux 系统上管理 PAM

在 Linux 系统上管理 PAM 的任务通常绝非简单。你需要验证 PAM 是否已正确实现，并根据你组织的特定安全需求进行调整。

此外，PAM 的功能远超前述描述的身份验证步骤。PAM 可以限制资源、限制访问时间、强制良好的密码选择等。

## 管理 PAM 感知应用程序配置文件

你应该检查 PAM 感知应用程序和工具的 PAM 配置文件，以确保它们的身份验证过程与你组织所需的身份验证过程一致。你的访问控制矩阵（参见第 22 章“理解基础 Linux 安全”）以及本章提供的信息将帮助你对 PAM 配置文件进行审计。

每个 PAM 感知应用程序都有自己的 PAM 配置文件。每个配置文件定义了使用哪些特定的 PAM 模块进行身份验证。如果不存在配置文件，可能会为该应用程序创建一个安全漏洞。这可能被用于恶意意图。作为安全措施，PAM 自带了一个名为“other”的配置文件。如果一个 PAM 感知应用程序没有 PAM 配置文件，它将默认使用“other” PAM 配置文件。

你可以使用 `ls` 命令验证你的 Linux 系统是否存在 `/etc/pam.d/other` 配置文件。示例显示该系统上存在 `/etc/pam.d/other` PAM 配置文件。

```
$ ls /etc/pam.d/other

/etc/pam.d/other
```

PAM `/etc/pam.d/other` 应该拒绝所有访问，这在安全领域被称为“隐式拒绝”（Implicit Deny）。在计算机安全访问控制中，隐式拒绝意味着如果不明确满足某些标准，则必须拒绝访问。在这种情况下，如果 PAM 感知应用程序没有配置文件，则对其的所有访问都将被拒绝。以下是 `/etc/pam.d/other` 文件的内容：

```
$ cat /etc/pam.d/other

#PAM-1.0

auth required      pam_deny.so

account required    pam_deny.so

password required   pam_deny.so

session required    pam_deny.so
```

注意，所有的 PAM 上下文（`auth`、`account`、`password` 和 `session`）都已列出。每个上下文都使用了 `required` 控制标志和 `pam_deny.so` 模块。`pam_deny.so` 模块用于拒绝访问。

即使有了“other”配置文件，如果 PAM 感知应用程序缺少 PAM 配置文件，也必须创建一个。请将此项加入你的 PAM 审计清单。你还应该检查 Linux 系统上的 PAM "other" 配置文件，以确保它执行了隐式拒绝。

## 管理 PAM 系统事件配置文件

与 PAM 感知应用程序和工具配置文件类似，你的 PAM 系统事件配置文件也需要根据组织的访问控制矩阵进行审计。然而，对这些文件进行任何必要的修改都需要你采取额外步骤。

在接下来的内容中，你将学习如何通过 PAM 在你的 Linux 系统上设置安全需求，例如账户登录限制。许多特殊情况要求你修改 PAM 系统事件配置文件，如 `/etc/pam.d/system-auth.ac`。

修改某些 PAM 系统事件文件的风险在于工具可能会重写这些文件。幸运的是，使用 `grep` 可以快速发现哪些配置文件存在此问题。

```bash
# grep "authconfig" /etc/pam.d/*

/etc/pam.d/fingerprint-auth# User changes will be destroyed the next time authconfig runs.

/etc/pam.d/fingerprint-auth-ac# User changes will be destroyed the next time authconfig runs.

...

/etc/pam.d/system-auth# User changes will be destroyed the next time authconfig runs.

/etc/pam.d/system-auth-ac# User changes will be destroyed the next time authconfig runs.
```

PAM 事件配置文件使用了符号链接（参见第 4 章“文件系统中的移动”）。例如，你可以看到 `system-auth` 实际上是一个指向 `system-auth-ac` 的符号链接。文件中的第一个字符 `l` 表示该文件是链接的。

```bash
# 1 -system-auth
lrwxrwxrwxx 1 root root 14 Feb 28 01:56
system-auth -> system-auth-ac
```

注意：并不是每个 Linux 发行版（如 Ubuntu）都有重写配置文件的 `authconfig` 工具。要检查你的发行版是否具有该工具，请在命令行输入 `which authconfig`。

在某些 Linux 发行版中，`pam-auth-config` 与 `authconfig` 类似，具有重写配置文件的能力。如果在命令行输入了 `pam-auth-config --force` 命令，就会发生这种情况。如果安装了该工具，请阅读 `man pam-auth-config` 页面。

`authconfig` 工具不使用也不修改符号链接。因此，你可以创建一个本地的 PAM 事件配置文件，并将符号链接指向它。这允许你实现必要的安全修改，并避免配置文件被 `authconfig` 工具重写。基本步骤如下，包括针对 `system-auth-ac` 执行这些步骤的示例：

1. 将当前的 PAM 事件配置文件复制到新文件，添加新文件名，如 "local"。
   `# cp system-auth-ac system-auth-local`
2. 对新配置文件进行所需的更改。
   `# vi system-auth-local`
3. 删除旧的符号链接文件。
   `# ls -system-auth`
   `lrwxrwxrwxx 1 root root 14 Feb 28 01:56`
   `system-auth -> system-auth-ac`
   `# rm -i system-auth`
   `rm: remove symbolic link 'system-auth'?`
4. 创建指向新配置文件的符号链接。
   `# ln -s system-auth-local system-auth`
   `# ls -system-auth`
   `lrwxrwxrwxx 1 root root 17 Feb 28 01:37`
   `system-auth -> system-auth-local`

## 第 23 章：理解高级 Linux 安全

在完成这些更改后，你可以对“本地”PAM 系统事件配置文件进行任何必要的修改，而无需担心 `authconfig` 可能会覆盖这些文件。

## 使用 PAM 实现资源限制

资源管理不仅是一项系统管理任务，它也是一项安全管理任务。设置资源限制有助于你避免 Linux 系统上出现不利问题。通过限制单个用户可以创建的进程数量，可以防止诸如炸弹（fork bombs）等问题。炸弹是指进程以递归方式一个接一个地产生，直到资源被耗尽为止。炸弹可能是恶意的，也可能是意外的——例如由程序开发不当引起。

PAM `limits` 模块使用特殊的配置文件来设置资源限制：`/etc/security/limits.conf`。默认情况下，该文件中没有设置任何资源限制。因此，你需要检查该文件并设置符合组织需求的资源限制。

> 注意
> PAM 配置文件位于 `/etc/pam.d` 目录和 `/etc/security` 目录。

以下代码段显示了 `/etc/security/limits.conf` 文件。该文件有详尽的文档说明。你应该通读该文件的内容，以获取的格式描述和可以设置的限制示例。
