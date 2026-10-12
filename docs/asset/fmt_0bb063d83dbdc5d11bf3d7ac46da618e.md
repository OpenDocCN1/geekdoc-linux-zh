
CentOS 是 Linux 中红帽 Linux 分支的代表。本书使用 CentOS 而不是官方的 Red Hat Linux，是因为 CentOS 是免费的，而且我很小气。CentOS 使用 Linux-PAM。许多 Linux 发行版都是基于 Red Hat Linux 构建的，它们的衍生版本应该能够使用 CentOS 的 PAM 配置。

此处涵盖的一些 PAM 模块位于 EPEL 仓库中。要使用这些模块，你需要启用该仓库、构建自己的包或进行其他安排。

CentOS 和相关的 Linux 发行版提供了一个配置 PAM 的命令行工具 `authconfig(8)`。

## Debian

Linux 的 Debian 分支的设计哲学与红帽 Linux 分支不同。它支持许多相同的软件，但管理界面几乎完全不同。Debian 使用 Linux-PAM。许多 Linux 发行版（如 Ubuntu 和 Kali Linux）基于 Debian 构建，可以使用 Debian 配置。

书中讨论的一些 PAM 模块位于实验仓库中。你需要启用该仓库或构建自己的包。

与 CentOS 类似，Debian 包含一个为你编写 PAM 配置文件的附加工具。与 CentOS 不同，Debian 使用 `pam-auth-update(8)`，这是一个 Debian 人员专门为 Debian 编写的。

## FreeBSD

FreeBSD 是我们的 OpenPAM 参考平台。支持 PAM 的 BSD 平台（如 Dragonfly 和 NetBSD）以及苹果的 OS X 使用 OpenPAM。在 FreeBSD 上有效的配置应该可以在 OS X 之外的任何 BSD 平台上运行。（OS X 使用的 PAM 模块与其他任何 OpenPAM 实现完全不同，使其在几乎所有情况下都是特例。）

少数 Linux 发行版使用 OpenPAM，或者允许轻松将其 PAM 实现替换为其他。你将像配置任何其他 PAM 实现一样配置这些操作系统，但你可能会发现某些 PAM 模块名称略有不同。如果你在使用带有 OpenPAM 的 Linux 发行并在寻找模块时感到困惑，请检查 CentOS 或 Debian 的示例以找到 Linux 社区给模块分配名称。

## 其他平台

PAM 可能不是一个单一的标准，但其配置的基础在各个实现中是通用的。管理 Solaris 派生版或 OS X 的系统管理员可以使用这里的指南创建自己的 PAM 配置。

关于附加 PAM 模块（如 Google Authenticator 或 SSH 代理认证）许多指南适用于适用于平台。配置密码质量检查器的细节在不同操作系统之间差异不大，即使该模块在策略中的放置位置有所不同。

## PAM 和 OpenSSH

OpenSSH 的服务器 `sshd(8)` 并不真正需要 PAM。SSH 认证的行业标准方法——密钥并不符合 PAM。SSH 服务器确实需要检查密码，这在过程的某处确实涉及到 PAM，但它是一个非常简单的检查。如果你使用单因素认证，简单的密码检查就足够了。

但如果你想实现复杂的基于 PAM 的认证，可以通过让 `sshd(8)` 链接到 PAM。将 `ssh_config` 中的 `UsePAM` 选项设置为 `yes`。这启用了基于 PAM 的账户检查、自动主目录创建等。然而，它不会触发基于 PAM 的认证。

SSH 守护进程处理键盘认证有两个选项。一个 `PasswordAuthentication` 是专门用于密码的；另一个 `ChallengeResponseAuthentication` 是一种更通用的认证机制。为了使用 PAM，你几乎肯定需要 `ChallengeResponseAuthentication`。

```
UsePAM yes

ChallengeResponseAuthentication yes

PasswordAuthentication no
```

控制和串口登录尝试使用 `login(8)` 程序，它有自己的 PAM 策略。SSH 服务器可以通过 `UseLogin` 选项将用户登录过程的一部分交给 `login(8)`。该选项通常为 `no`。`login(8)` 和 `sshd(8)` 策略之间的交互极其有趣或令人愤怒，取决于你是否是那个需要让它们运行的人。为了使用 PAM，最好让 SSH 服务器处理登录，而不是调用 `login(8)`。

```
Login no
```

此外，让 `sshd(8)` 咨询 PAM 进行认证。为此，你需要 `ssh_config` 中的 `AuthenticationMethods` 选项。`keyboard-interactive` 设置告诉 sshd 将认证传递给其他代理（如 PAM）。如果你激活了 PAM 并告诉 `sshd(8)` 使用键盘交互认证，你将获得基于 PAM 的认证以及账户管理。

# 第 0 章：引言

将其设置为 `publickey` 意味着 sshd 要求公钥认证。用逗号将两者结合意味着 sshd 要求同时满足这两者，而用空格将它们分开则意味着 sshd 提供了认证选项供选择。

大多数想在 `sshd(8)` 中启用 PAM 的人都希望守护进程拒绝所有没有公钥的身份验证请求，然后让 PAM 有机会许可或否决连接。这将产生如下所示的 `AuthenticationMethods` 条目。

```
AuthenticationMethods publickey,keyboard-interactive
```

或者，你可能希望允许使用公钥认证的用户登录，然后回退到 PAM 进行一次性密码或其他其他强身份验证。在方法之间加一个空格。

```
AuthenticationMethods publickey keyboard-interactive
```

即使有这些选项，并不是所有的 PAM 模块都能与 sshd 配合。将 `pam_ssh_agent_auth`（第 8 章）接入 sshd 听起来可能很有趣，但只会让你烦恼。

## PAM、LDAP 和 Kerberos

每当系统管理员考虑认证时，集中认证的话题就会出现。这些讨论大多数都将围绕轻量级目录访问协议 (LDAP) 和 Kerberos 的各种排列组合展开。这会对你有帮助吗？

是的……也不。

部署 LDAP 的困难与 PAM 几乎没有关系。配置 LDAP 认证之所以困难，是因为 LDAP 的格式极其灵活。你可以使用任意数量的 LDAP 架构（schemas）或创建自己的。在 LDAP 部署早期做出的决策将产生你将永远受其影响的影响。更糟糕的是，我们每个参考平台上的 LDAP 模块之间的差异，意味着每个平台都需要唯一的配置。

Kerberos 比 LDAP 没那么灵活，但它有非常特定的要求和更高的开销。

本书将帮助你理解你的 PAM 配置如何影响这些集中认证方法。它将帮助你在部署时从 PAM 中提取调试信息。但它不会帮助你决定如何设计你的 LDAP 架构。

## 本书概览

本书由两个大部分组成。前六章将引导你了解 PAM 是如何工作的。

第 0 章是本引言。

第 1 章“PAM 组件”讨论了 PAM 的组成部分。你将学习 PAM 配置文件和语句、控制语句、PAM 模块以及常用标志。我们还将探索 PAM 策略是如何运作的，以及 PAM 如何决定允许或拒绝请求。

第 2 章“常用模块”涵盖了每个人都需要理解的模块，例如用于传统 Unix 认证的模块、允许 root 访问服务、审计等。

第 3 章“PAM 项、代码和函数”深入探讨了某些 PAM 内部机制。系统管理员不需要为 PAM PAM，但在这些代码出现时需要识别它们。理解 PAM 项（items）和返回代码对于管理 PAM 至关重要。

第 4 章“Linux-PAM 扩展和子栈”讨论了 Linux-PAM 对 PAM 配置的扩展，例如根据特定的 PAM 响应做出决策。

第 5 章“流行的 Linux-PAM 模块”详细介绍了通常在 Linux-PAM 系统中部署的模块。PAM 中的 Linux 配置功能是其他系统放置在其他地方的。

第 6 章“PAM 调试”展示了如何在你的 PAM 配置中找到问题。

通过这六章，你可以完成本质的配置任务和调试。书的其余部分将介绍特定的模块。通过极其简易的互联网搜索就能发现数百个 PAM 模块，但本书只涵盖了少数几个。其中一些广泛可用且非常有用，例如 `pam_exec`（第 7 章）。有些很流行，如 `pam_ssh_agent_auth`（第 8 章）和 Google Authenticator（第 9 章）。有些可以让我说明关于 PAM 的重要点。`pam_ssh` 模块（第 10 章）不仅说明了一个实用的功能，还作为操作系统部署 PAM 模块时令人愤怒的差异案例。

这留下了数百个 PAM 模块。许多 PAM 模块对于需要它们的人来说至关重要，但只有少数读者需要任何特定的模块。本书让你对 PAM 有足够的理解，让你确信能力为使用该模块编写正确的规则，从而释放你宝贵的脑力去理解模块本身以及该模块如何融入策略中。

第 7 章“任意文件和随机程序”讨论了基于文本列表的访问。你还学习了作为 PAM 的一部分运行外部程序。

第 8 章“SSH Agent 认证”涵盖了在登录系统后使用你的 SSH agent 对服务进行身份验证。
