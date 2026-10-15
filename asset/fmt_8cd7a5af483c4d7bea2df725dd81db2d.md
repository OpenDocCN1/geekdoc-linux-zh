
# 第 8 章：SSH Agent 认证

使用用户的 SSH 密钥进行认证是对多因素认证的一种拙劣模仿。它证明了用户拥有密钥文件以及用于解密该密钥的短语。当然，密钥文件并不是物理实体。它可以在机器之间复制和移动。但它比单纯的明文密码稍微好一点。对于真正的双因素认证，你需要像 `Google Authenticator`（第 9 章）这样的工具，或者投资安全令牌。另一方面，SSH agent 认证让你避免在服务器上输入密码。

第 8 章：[`Pam_ssh_agent_auth`](https://sourceforge.net/projects/pamsshagentauth/) 的工作方式与基于密钥的 SSH 认证相同。模块获取用户的 `authorized_keys` 文件，并询问用户的 SSH agent 它是否具有匹配的私钥。如果 SSH agent 拥有该私钥，模块将返回 `PAM_SUCCESS`。`Pam_ssh_agent_auth` 设计用于认证 `sudo(1)`，这就是我们使用它的方式。

许多组织有正当理由不使用 SSH agent，或者有理由不以这种方式认证程序。破解用户的 SSH 客户端可能会导致服务器被破解。这在许多环境中是一个合理的反对意见。但 `pam_ssh_agent_auth` 是较简单的附加 PAM 模块之一，因此它是开始探索的好地方。

## `Pam_ssh_agent_auth` 与 PAM

那么，如何使用这个东西呢？找到你系统中 `sudo(1)` 的 PAM 配置。在大多数 Linux 系统中，它位于 `/etc/pam.d/sudo`，而 FreeBSD 会将其存放在 `/usr/local/etc/pam.d/sudo`。

现在是困难的部分：决定你想要如何使用该模块。你是否希望 SSH agent 认证就足够获取 sudo 权限？将该模块置于身份验证策略的最上方，并使用 `sufficient`（足够）控制。

你想同时要求 SSH agent 和密码吗？将 `pam_ssh_agent_auth` 放在最终的 `pam_deny.so` 之前的任何地方，并使用 `required`（强制）控制。

现在让我们来看一种稍微复杂的多因素身份验证方法。

# 第 9 章：一次性密码：Google 验证器 (Google Authenticator)

一次性密码仅有效一次的密码。我们有很多一次性密码的实现，从万物中的一次性密码 (OPIE) 到 RSA 令牌。基于时间的一次性密码系统（或 TOTP）使用系统时钟共享密钥根据需要计算有效的密码。最为人知的 TOTP 实现是 Google 验证器。

`Google Authenticator` 不需要访问 Google。它之所以被称为 *Google Authenticator* 是因为 Google 提供了软件，而不是因为它以任何方式挂接到 Google 的系统中。`Google Authenticator` 在没有连接互联网的机器上也能正常工作。

`Google Authenticator` 通过客户端应用和 Google 验证器 PAM 模块将你的智能手机、平板电脑或 Chrome 浏览器转换为身份令牌。当你尝试使用 Google 验证器访问服务时，PAM 模块会计算出一个六位数字密码作为临时的一次性密码。服务器提示你输入此密码。你的设备使用相同的方法计算出该主机当前的正确密码。将你设备提供的密码输入应用程序中。如果两个设备的计算结果相同，则密码匹配，你即可获得访问权限。

`Google Authenticator` 比使用 SSH agent 更好的多因素身份验证方法，但它并不完美。任何平板电脑、手机或 Chrome 浏览器都可以变成身份令牌。如果坏人捕获了你的任何设备，或者偷取了用于配置客户端应用的共享密钥，他们就拥有了你的身份令牌。但至少设备是物理对象，而不是入侵者可以轻易复制的文件¹¹¹⁷

每个使用 GA 的主机都有独立的 GA 配置和唯一的共享密钥。每个用户必须登录到她应该访问的每个主机并配置她的 GA 访问。`Google Authenticator` 本身最适合只有少数服务器和少量账户的环境。你不会希望一个拥有数千个账户的主机使用普通的 `Google Authenticator`，除非你投入员工时间来管理身份验证。正如稍后我们将讨论，可以在主机之间共享 GA 配置，但这会改变 GA 的安全性，并需要额外的脚本和配置。我们将从简单的情况开始，在单台主机上设置 GA。

在开始使用 `Google Authenticator` 之前，请检查主机的时钟和时区。`Google Authenticator` 在时钟与世界其他同步的服务器上效果最好。系统时钟经常偏离真实时间，特别是在虚拟机上。使用 `ntpd(8)` 或其他计时服务同步服务器的时间。如果 GA 莫名失败，双检一切的时钟和时区。

仅在身份验证策略中使用 `Google Authenticator`。它不为账户、会话或密码类型提供任何服务。

> ¹⁷ 除非你将共享密钥备份在入侵者可以窃取的地方。不要这样做。

`Google Authenticator` 几乎在处处可用；它没有像 `pam_ssh_agent_auth` 那样的环境要求。然而，我鼓励你在将其应用于所有系统身份验证之前仔细考虑。当服务器时间“醉酒”并剧烈偏移时会发生什么？如果你要求在控制台登录 GA，解决问题将进入单用户模式，可能需要通过重启。你有足够的冗余来处理这种情况？此外，`Google Authenticator` 内置了登录速率限制。如果你对 SSH 和 sudo 都要求 GA，你将直接撞上那个速率限制。

仔细考虑你部署决策的影响。

## 安装 Google 验证器

`Google Authenticator` 客户端很简单。从设备的应用商店获取你的应用，或者为桌面安装 Authenticator Chrome 扩展程序。

任何想要使用 `Google Authenticator` 的服务器都必须安装 `Google Authenticator` PAM 模块。FreeBSD 有 `pam_google_authenticator` 包，但大多数用户也会想要安装 `libqprencode` 包。Debian 包含了 `libpam-google-authenticator` 包，但很少是最新版本。CentOS 没有官方包，尽管在编写本文时 EPEL 已经包含了 CentOS 6 及更早版本的包。要在当前版本的 CentOS 上使用 `Google Authenticator`，或在 Debian 上使用 `Google Authenticator`，你可能必须从源码安装。

从 https://github.com/google/google-authenticator 获取当前的源码，可以使用 `git(1)` 或通过下载并解压 zip 文件。`libpam` 目录包含 `Google Authenticator` PAM 模块。进入该目录编译并安装库。

```
# ./bootstrap.sh
# ./configure
# make
# make install
```

你现在已经有了可用 `Google Authenticator` PAM 模块。

## Google 验证器用户功能

许多 GA 教程告诉用户运行 `google-authenticator` 并回答 yes。用户做出的糟糕决定可能会毁掉他们的一天。为你的用户提供关于如何配置的非常严格的

## 密码类型

GA 支持两种类型的密码：基于时间和基于计数器的。

基于时间的方法结合共享密钥和当前时间来创建一个临时的一次性密码。这些密码的有效期仅为 30 秒（或）。基于时间的一次性密码在 RFC 6238 中记录。

基于计数器的密码计算出一系列密码，每个密码只能使用一次。基于计数器的密码基于 RFC 4226。

这两种方法都需要服务器和设备之间的同步。基于时间的密码要求设备时钟与服务器时钟一致。基于计数器的密码要求用户避免误触数百个密码。虽然我可以构想出某些基于计数器的密码合理的情况，但在现实中我建议使用基于时间的。

## 文件管理

`Google Authenticator` 使用 `$HOME/.google_authenticator` 文件管理用户的身份验证设置和当前身份验证状态。（管理员可以更改文件位置，正如稍后我们将讨论的。）

即使速率限制也发生在该文件中。
