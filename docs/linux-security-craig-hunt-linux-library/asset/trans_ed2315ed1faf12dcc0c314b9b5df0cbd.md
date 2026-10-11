
**图 2.5** 使用 *linuxconf* 设置用户账户过期参数

![](img/3258bbaf790525f8c4eb25fabff7844a_62_0.png)

**禁用通过 NFS 挂载的 root 访问权限。** 请特别关注 */etc/exports* 文件，在这里您声明希望通过网络文件系统（NFS）共享的本地文件系统。在大多数 Linux 发行版中，NFS 服务器默认将用户 ID 0（root）映射到一个非特权用户，例如 nobody。然而，这种行为可以通过 NFS 服务器的 */etc/exports* 文件中的 **no_root_squash** 选项进行覆盖。务必避免使用此选项。它会使得您的整个 NFS 服务器完全暴露在客户端上的某个 root 用户之下。

如果您已经配置了 Linux 客户端以自动挂载远程 NFS 共享，请参阅 Reaz Zadok 所著的《Linux NFS 和 Automounter 管理》（Sybase，2001年）。

**将 root 用户的使用限制在绝对必要的情况下。** 您应该克制住登录 root 账户以执行管理命令的冲动，并保持登录状态以执行其他用户级命令。您以 root 身份登录的时间越长，暴露在诸如木马和会话劫持等漏洞下的时间就越长。

**使用具有描述性的 root 提示符。** 有时您自己就是自己最大的敌人。当您的 X 显示上有多个活动终端时，能够一眼分辨出哪些是 root 终端至关重要。这有助于您避免错误地在 root 窗口中执行用户级命令。确保 root 提示符足够独特，并且包含一个 root 专用字符，例如井号（#）。

**为 root 账户使用最小化的 PATH。** 针对 root 账户的一种常见攻击方式是，将常用实用工具的木马版本放置在包含在 root $PATH 中的目录里。这是一种非常隐蔽的攻击，保护它的唯一方法是确保您了解 $PATH 变量的内容以及包含在变量中的目录的内容。为了最大程度地减少运行木马的可能性，请避免在 $PATH 中包含任何除 root 以外用户可写的目录。

**使用专用系统账户。** 一个只需要关闭系统的操作人员不需要完整的 root 权限。这正是默认 Linux 账户（如 operator 和 shutdown）的目的所在。此外，我建议您安装并使用 sudo，关于它的详细说明将在本章稍后的“sudo 实用工具”部分中介绍。

**使用组成员资格。** 作为一名 Linux 管理员，您经常被要求使文件或目录可供协作完成单一任务的多个用户读取和写入。虽然简单地使这些资源对所有人可写很容易，但不要这样做。花点时间添加一个新组，使每个用户成为该组的成员，并使资源仅对该组成员可访问。将权限开放的文件视为等待被利用的漏洞。

**将 root 登录限制在系统控制台。** 为了监控谁正在以 root 身份登录，请配置 /etc/security 文件，仅允许从控制台直接进行 root 访问。此操作强制授权的 root 用户使用 su 或 sudo 来获取 root 权限，从而您可以轻松记录这些事件。标准的 Linux 默认设置是仅允许从八个虚拟系统控制台（键盘上的功能键）进行 root 登录：

```
[root]# more /etc/security
tty1 tty2 tty3 tty4 tty5 tty6 tty7 tty8
```

除了记录优势外，如果 root 密码被泄露，这也设置了一道额外的障碍。入侵者必须首先获得普通用户账户（或物理控制台）的访问权限，才能利用他们的发现。

采用良好的用户账户实践对于确保系统安全至关重要，但通过选择糟糕的密码，用户可以破坏您为保护其账户所做的所有工作。下一节提供了一些关于选择强密码并强制使用它们的实用建议。

# 良好的密码

虽然更强的身份验证模式变得越来越普遍，但用户名和密码仍然是 Linux 服务器最常用的身份验证方法。关于密码安全的重要性已有大量讨论和著述，因此我将简要地讨论此话题。有一些非常简单的规则可以遵循，它们可以使您的密码政策大大加强：

- **不要将系统设置得太快导致密码过期。** 如果密码过期周期太短，用户更有可能觉得他们会忘记密码，因此他们会把它写下来。此外，用户会使用循环、可预测的密码模式。在密码过期方面，少于三个月的任何时间间隔都应被视为太短。
- **不要让密码变得陈旧。** 相反，如果您允许用户一年使用同一个密码，它们暴露在安全风险中的时间就比安全允许的要长。四个月是一个很好的折衷，但六个月并不算不合理的过期周期。
- **避免短密码。** 强制用户选择至少六个字符长的密码。短于此长度的密码太容易被暴力破解攻击猜测，即使是随机字符也是如此。图 2.6 说明了如何使用如 Red Hat 的 linuxconf 等系统管理工具来强制实施密码长度最小值。请注意，除了强制实施六个字符的限制外，此页面还强制用户至少使用两个非字母数字字符。
- **破解您自己的密码。** 作为定期系统安全审计的一部分，使用密码猜测工具查找 */etc/passwd* 文件中的弱密码。直接联系有问题的用户，建议他们使用更长的密码，包含更多的非字母数字字符，以及混合大小写字符。第三章“系统监控和审计”会更详细地讨论这个话题，当正式介绍 crack 实用工具时。
- **删除未使用的账户。** 大多数 Linux 服务器不提供 UUCP、PPP、NNTP、Gopher 或 Postgres 服务，但大多数 Linux 发行版都附带这些账户。完全删除这些账户，以及您的环境中没有意义的任何其他账户。

![](img/3258bbaf790525f8c4eb25fabff7844a_65_0.png)

**避免空密码字段。** 即使 shell 高度受限，也永远不要设置没有密码的用户。获得系统中任何用户的访问权限就使入侵者完成了一半的目标。

最小化与用户密码相关风险的有效方法是配置对影子密码和组文件的支持。这是下一节的主题。

# 影子密码

最容易被忽视的系统漏洞之一是任何用户可以*破解*另一个用户密码的能力。使用互联网上唾手可得工具，这可以迅速轻松地做到。为了防止这一点，启用*影子密码*。影子密码将密码文件分为两个：包含实际密码字段条目占位符的 /etc/passwd 文件，以及包含加密密码的 /etc/shadow 文件。/etc/shadow 文件不需要除了 root 以外的任何人可读，这使得普通用户更难尝试破解另一个用户的密码（包括 root）。

大多数 Linux 发行版还支持*影子组*的概念，其中每个组的实际成员没有列在主要的 /etc/group 文件中，而是列在 /etc/gshadow 文件中，该文件与 /etc/shadow 文件一样，仅 root 可读。

> **提示** 某些 Linux 发行版默认未启用影子密码；如果您的发行版是其中之一，请立即启用此功能。

清单 2.1 展示了您应该如何查找 /etc/shadow 文件是否存在。如果它不存在，只需使用 pwconv 命令创建它。注意转换后 /etc/passwd 文件的变化：

# 清单 2.1 创建影子密码文件

```
[root]# ls -1 /etc/shadow
ls: /etc/shadow: No such file or directory
[root]# more /etc/passwd
root:PV/6t9I GetTjU:0:0:root:/root:/bin/bash
bin::1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm::3:4:adm:/var/adm:
lp::4:7:lp:/var/spool/lpd:
sync::5:0:sync:/sbin:/bin/sync
shutdown::6:0:shutdown:/sbin:/sbin/shutdown
halt::7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
operator::11:0:operator:/root:
ftp::14:50:FTP User:/home/ftp:
nobody:x:99:99:Nobody:/:
ramon:aa1g0.pAVxZuA:501:100:Ramon J.ontanon:/home/ramon:/bin/bash
[root]# pwconv
[root]# ls -1 /etc/shadow
- - - - - - - - - - - 1 root root 563 Sep 23 15:27 /etc/shadow
[root]# more /etc/passwd
root:x:0:0:root:/root/bin/bash
bin::1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm::3:4:adm:/var/adm:
lp::4:7:lp:/var/spool/lpd:
sync::5:0:sync:/sbin:/bin/sync
shutdown::6:0:shutdown:/sbin:/sbin/shutdown
halt::7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
operator::11:0:operator:/root:
ftp:x:14:50:FTP User:/home/ftp:
nobody:x:99:99:Nobody:/:
ramon::501:100:Ramon J.ontanone:/home/ramon:/bin/bash
[root]# more /etc/shadow
root:PV/6t9I GetTjU:11223:0:99999:7:::
bin::11223:0:99999:7:::
```

