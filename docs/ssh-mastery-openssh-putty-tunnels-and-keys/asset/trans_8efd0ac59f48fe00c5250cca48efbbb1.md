
伪造服务器。通过在 known_hosts 中用 @revoked 标记一个密钥，你告诉 ssh 不要接受该密钥并生成一个令人恐惧的警告。

```
$ ssh gluttony
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@ WARNING: REVOKED HOST KEY DETECTED! @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
The ECDSA host key for gluttony.mwl.io is marked as revoked.
This could mean that a stolen key is being used to
impersonate this host.
ECDSA host key for gluttony.mwl.io was revoked and you have requested strict checking.
Host key verification failed.
```

请注意，没有“无论如何接受此密钥”的选项。被撤销的密钥是完全不可信任的。将密钥保留在 known_hosts 中但将其标记为已撤销，会给用户明确的警告，表明他们遇到了一个受损的系统。

标记必须位于行的开头，在主机名之前。

## 主机名

主机名是 SSH 识别 SSH 服务器的方式。如果你使用短主机名连接到服务器，ssh 会记录它用于联系服务器的完整主机名。这意味着如果我输入 ssh wrath，ssh 会将主机名记录为 wrath.mwl.io，因为那是我的系统解析器提供给 ssh(1) 的名称。该机器可能还有其他主机名或别名，并且可能也以其 IP 地址为人所知。一个真正权威的 known_hosts 文件必须为这些名称中的每一个包含密钥。

好消息是，你不必为这些不同的名称包含多行大部分重复的行。known_hosts 文件接受单个条目中的多个主机名，只要它们用逗号分隔即可。

```
gluttony.mwl.io,mail.mwl.io,203.0.113.213 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTIbmlzdHAyN...
```

一些系统管理员会更改其 SSH 服务运行的 TCP 端口。这对安全来说不是特别有用，但有助于减缓更原始的蠕虫并减少日志噪音。这些主机名在 known_hosts 中以方括号出现，后跟冒号和端口号。

```
[lust.mwl.io]:2222 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTIbmlzdHAyNTYAAAAIbmlzdHAyNT...
```

第 5 章介绍了通过哈希主机名来隐藏它们，防止偶然的入侵者从 known_hosts 中提取服务器信息。在单行上列出多个主机名简化了 known_hosts 的集中管理，但与哈希主机名冲突。如果你想哈希主机名，你必须在单独的行上列出每个主机名。主机 avarice.mwl.io、mail.mwl.io 和 198.51.100.12 需要三个 known_hosts 条目，并且每个条目都会单独进行哈希。如果你在分发之前要对 known_hosts 条目进行哈希，我建议以明文维护你的主文件。

接受多个 IP 地址连接的主机理论上需要为每个地址提供一个 known_hosts 条目。如果你通常不连接到所有这些地址，那就不用费心了。我有一台拥有数十个 IP 地址的服务器，但我只通过 SSH 连接到其中一个地址，因此该服务器只有一个 *known_hosts* IP 条目。如果你有这样的服务器，将 sshd 锁定为仅监听一个地址可能会简化管理。

## 密钥类型

密钥类型是用于生成此主机密钥的算法。现代的 *known_hosts* 可以包含六种不同的密钥类型：*ssh-dss*（DSA 密钥）、*ssh-rsa*（RSA 密钥）、*ecdsa-sha2-nistp256*、*ecdsa-sha2-nistp384* 和 *ecdsa-sha2-nistp512*（ECDSA 密钥），以及 *ssh-ed25519*（ED 25519 密钥）。在空格中出现的任何其他内容都很奇怪，需要调查。

## 密钥

公钥是一个长长的乱码字母数字字符串。它通常以一系列大写 A 开头，并且经常（但不总是）以等号（=）结尾。密钥占据了该行的绝大部分。

## 注释

注释是自由格式文本。你可以根据需要使用注释。它在自动维护的 *known_hosts* 文件中通常为空，但在集中管理中你会发现它很有用。

## 创建 known_hosts

生成 *known_hosts* 的简便方法是使用 ssh-keyscan(1)。

```
$ ssh-keyscan wrath > wrath.known_hosts
```

这为你提供了一个开始的 *known_hosts* 文件。现在你需要将这些密钥与你在第 4 章中生成的指纹进行验证。这是一项非常适合交给一个你讨厌的细致、尽责的跟班的工作。

我鼓励你自动化收集 *known_hosts* 条目。你如何做到这一点完全取决于你组织偏好的工具。理想情况下，你会在机器首次部署时运行 ssh-keyscan，在任何入侵者有机会破坏它之前，并立即更新你的 *known_hosts*。

如果你想简化 *known_hosts*，你可以减少 SSH 服务器提供的密钥数量。你可以声明网络中的所有主机只提供 ED25519 密钥，从而消除所有其他密钥类型的 *known_hosts* 条目。*sshd_config* 中的 HostKeyAlgorithms 关键字让你可以设置 sshd 用于主机识别的算法。

```
HostKeyAlgorithms ssh-ed25519, ssh-rsa
```

你将使用确切的方法完全取决于你熟悉的工具和已有的自动化。如果可能，请重新利用你现有的工具。

如果你编写了一个用于收集、验证和构建 *known_hosts* 文件的好工具，请将其公开。

## 撤销主机密钥

如果你有理由怀疑服务器的密钥已被泄露，请撤销它。在你的 *known_hosts* 中找到服务器的所有主机密钥条目。在所有条目前添加字符串 @revoked。为服务器生成新的主机密钥并重启 *sshd*，然后将新的主机密钥添加到你的 *known_hosts*。现在你可以将更新后的 *known_hosts* 分发给你的客户端，并且在（不太可能）用户尝试使用被撤销密钥的情况下，用户会收到警告。

被撤销密钥的有效性完全取决于向客户端分发 *known_hosts*。

## 分发主机密钥

只要 SSH 服务器的主机密钥被添加、移动或更改，用户就会看到有关主机密钥的警告。分发 *known_hosts* 的全部目的就是防止用户看到不必要的警告。领先于你的用户。¹ 只要你部署或移除服务器，或必须为服务器提供新密钥，就更新你的 *known_hosts*。如果你延迟更新 *known_hosts*，用户会学会忽略警告。

维护集中式 *known_hosts* 文件最糟糕的部分是将文件复制到所有服务器和工作站。你很忙。如果更新花费很长时间或大量精力，你就无法跟上。你确实需要像 Ansible、Puppet 或其众多竞争对手之一这样的集中系统。Active Directory 对于向 Windows 系统分发主机密钥效果很好。如果你从未使用过自动化，我推荐 Ansible。一旦你为现有系统准备了完整的 *known_hosts*，更新该文件并将其推送到所有系统只需一两分钟，就能为你的用户和支持团队节省数小时的工作。

## 分发 known_hosts

所有 OpenSSH 客户端都会检查 */etc/ssh/ssh_known_hosts* 以获取主机密钥。将你的 *known_hosts* 复制到每个服务器和工作站的此位置。下次有人在这些机器上使用 ssh(1) 时，正确的密钥已经在位。

OpenSSH 会在每个用户的个人 *known_hosts* 文件中检查主机密钥，此外还会检查系统的 */etc/ssh/ssh_known_hosts*。客户端将使用与服务器提供的密钥匹配的任何条目。当你首次部署集中式 *known_hosts* 时，每个用户可能已有现有的个人 *known_hosts*。你不希望用户个人缓存中的任何过时或无效条目干扰后续的密钥更改或撤销。不要直接删除每个人的 *known_hosts*；它们可能包含你不控制的服务器的已验证主机密钥。相反，在首次部署时，将每个用户的个人 *known_hosts* 移动到像 *known_hosts.personal* 这样的位置。

务必告诉你的用户发生了什么。最好提前通知。
一旦你建立了维护 *known_hosts* 的系统，你会在 SSH 中找到自动化的其他用途。请记住 */etc/ssh/ssh_config* 为 ssh(1) 设置系统范围的默认值。如果你有需要特殊设置的组织标准，你可以在全局配置中输入它们，从而节省用户编辑自己的配置或记住命令行参数的精力。如果你的组织在非标准端口上运行 SSH，在 */etc/ssh/ssh_config* 中设置 Port 关键字实际上可能会赢得用户的良好 karma。个人配置文件会覆盖系统范围的设置，因此如果用户真的想自找麻烦，他们仍然可以射伤自己的脚。

## 分发 PuTTY 主机密钥

PuTTY 将其主机密钥保存在 Windows 注册表中。复制密钥不如将文件移动到所有工作站那么容易，但可以简化。PuTTY 团队有一个 Python 脚本可以将 *known_hosts* 转换为 PuTTY 的注册表键，`hk2reg.py`。你不会在正常的 PuTTY 安装中找到 `hk2reg.py`，但它包含在源代码中。你可以从 PuTTY 网站下载 PuTTY 源代码，或从 PuTTY GitHub at https://github.com/github/putty 的“contrib”目录获取。

运行 `hk2reg.py` 并给它一个参数，你的原始 *known_hosts*。

```
$ hk2reg.py pristine-known_hosts > putty.reg
```

通过 Active Directory、登录脚本或让用户双击它，在客户端上安装此注册表文件。²

请记住 PuTTY 将密钥存储在每个单独用户的注册表中。没有系统范围的 PuTTY 注册表树。按用户而非按机器分发密钥。

如果你为多种平台维护 *known_hosts*，我建议以下分发主机密钥的工作流程：首先收集你的主机密钥。为你的 OpenSSH 客户端创建一个 *known_hosts* 文件。触发脚本自动将新的 *known_hosts* 分发到每个 OpenSSH 系统。在此期间，使用 `hk2reg.py` 创建你的 Windows 注册表。最后，将新的注册表文件排队通过 Active Directory 分发。下次人们登录时，他们应该拥有所有新密钥。

## DNS 中的主机密钥

OpenSSH 支持在域名系统中检查主机密钥指纹。（PuTTY 不支持。）这消除了将文件推送到服务器的需要，但传统的 DNS 服务并不安全。如果你想通过 DNS 安全地分发服务器的公钥指纹，你绝对必须拥有 DNS 安全扩展（DNSSEC）。如果你还没有 DNSSEC，现在就去配置它，然后再回来这里。你可能会发现我的书 *DNSSEC Mastery* (Tilted
