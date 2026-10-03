
```
account    required       pam_unix.so
account    sufficient     pam_localuser.so
account    sufficient     pam_usertype.so system
account    [default=success=ok user_unknown=ignore] pam_ss.so
account    required       pam_permit.so
password   requisite       pam_cracklib.so try_first_pass retry=3
```

上述列表中添加的 `pam_cracklib` 条目使用了 `retry` 关键字。以下是 cracklib 可用的关键字：

```
debug
导致模块向 syslog 写入信息。
authtok_type=XXX
```

- 默认使用 `New UNIX password:` 和 `Retype UNIX password:` 来请求密码。
- 将 XXX 替换为其他单词以代替 UNIX。

## 第五部分：学习 Linux 安全技术

```
retry=N
```

- 默认值 = 1
- 在返回错误之前，最多向用户提示 N 次。

```
difok=N
```

- 默认值 = 5
- 新密码中必须不能出现在旧密码中的字符数量。
- 异常 1：如果新密码中有一半的字符不同，则接受新密码。
- 异常 2：参见 `difignore`。

```
difignore=N
```

- 默认值 = 23
- 在设置 `difok` 之前忽略的密码字符数量。

```
minlen=N
```

- 默认值 = 9
- 新密码可接受的最小长度。
- 查看 `dcredit`, `ucredit`, `lcredit` 了解它们的设置如何影响 `minlen`。

```
dcredit=N
```

- 默认值 = 1
- 如果 (N >= 0)：新密码包含数字的最大额度。如果你拥少于 N 个数字，则每个数字都计 +1 以满足当前的 `minlen` 值。
- 如果 (N < 0)：新密码必须满足的最小数字数量。

```
ucredit=N
```

- 默认值 = 1
- 如果 (N >= 0)：新密码包含大写字母的最大额度。如果你少于 N 个大写字母，则每个字母都计 +1 以满足当前的 `minlen` 值。
- 如果 (N < 0)：新密码必须满足的最小大写字母数量。

```
lcredit=N
```

- 默认值 = 1
- 如果 (N >= 0)：新密码包含小写字母的最大额度。如果你少于 N 个小写字母，则每个字母都计 +1 以满足当前的 `minlen` 值。
- 如果 (N < 0)：新密码必须满足的最小小写字母数量。

```
credit=N
```

- 默认值 = 1
- 如果 (N >= 0)：新密码包含其他字符的最大额度。如果你少于 N 个其他字符，则每个字符都计 +1 以满足当前的 `minlen` 值。
- 如果 (N < 0)：新密码必须满足的最小其他字符数量。

```
minclass=N
```

- 默认值 = 0
- 新密码需要满足四类字符中的任意 N 类。这四类是数字、大写字母、小写字母和其他字符。

```
maxrepeat=N
```

- 默认值 = 0
- 拒绝包含超过 N 个相同连续字符的密码。

`reject_username`

检查新密码中是否包含正序或反序形式的用户名用户名。如果找到，则拒绝该新密码。

`try_first_pass`

尝试从之前的 PAM 模块获取密码。如果不起作用，则提示用户输入密码。

`use_authtok`

此参数用于强制模块不向用户提示新密码。相反，新密码将由之前堆栈中的密码模块提供。

`dictpath=/path`

cracklib 字典的路径。

`maxsequence=N`

- 默认值 = 0（意味着此检查已禁用）
- 将 N 设置为 0 以外的任何数字会导致

## 练习

使用这些练习来测试你对使用加密工具和 PAM 的知识。这些任务假设你正在运行 Fedora 或 Red Hat Enterprise Linux（RHEL）系统（尽管某些任务在其他 Linux 系统上同样适用）。如果你遇到困难，任务的解决方案可以在附录 B 中（尽管在 Linux 中，通常有多种方法可以完成任务）。

1. 使用 `gpg` 工具和对称密钥加密文件。
2. 使用 `gpg` 工具生成公钥密钥环。
3. 列出你生成的密钥环。
4. 使用 `gpg` 工具加密文件并添加你的数字签名。
5. 访问 Fedora 下载页面：https://fedoraproject.org。选择其中一个 Fedora 发行版进行下载。下载完成后，验证你的镜像。
6. `su` 命令是否有 PAM 配置文件？如果是，请在屏幕上显示该配置文件，并列出它使用的 PAM 上下文（contexts）。
7. 在屏幕上列出你系统中的各种 PAM 模块。
8. 在你的系统中找到 PAM 的“other”配置文件。它是否存在？它是否强制了“隐式拒绝”（Implicit Deny）？
9. 找到 PAM limits 配置文件。它是否有设置可以防止系统发生进程炸弹（fork bomb）？
10. 使用 `authselect` 命令检查你的系统是否启用了 authselect，列出可用的配置（profiles），并查看当前是哪个配置。

# 第 25 章：使用 SELinux 增强 Linux 安全性

## 本章内容

- 学习 SELinux 的优势
- 学习 SELinux 的原理
- 设置 SELinux
- 解决 SELinux 问题
- 获取有关 SELinux 的额外信息

对于最高安全级别的服务器，基础的 Linux 安全是不够的。默认情况下运行在 Linux 系统上的进程使用文件和目录的标准权限来允许或拒绝对这些项目的访问。更安全的方法是允许访问服务所需的特定文件、目录、端口、系统调用、进程和网络套接字，并拒绝其他一切。这正是安全增强 Linux（SELinux）所做的。

Linux 由美国国家安全局（NSA）联合其他安全研究机构（如安全计算公司 SCC）共同开发，SELinux 于 2000 年发布到开源社区，并在 Red Hat 将其 Linux 发行版包含 SELinux 后变得流行。现在，许多组织都在使用 SELinux，且它广泛可用。

## 理解 SELinux 的优势

SELinux 是部署在 Linux 之上的安全增强功能。它提供了额外的安全措施，默认包含包含，并在 Red Hat Linux (RHEL) 和 Fedora 中被设置为强制模式（enforcing mode）。SELinux 可用于 Ubuntu 系统，但默认未安装。对于 Ubuntu，在强制性访问控制方面，App Armor 比 SELinux 更常用于安全防护。

SELinux 通过对主体和对象（即进程和资源）基于角色的访问控制（RBACs）提供了比 Linux 系统改进的安全性。“传统的”Linux 安全使用裁量性访问控制（DAC）。

使用 DAC 时，进程可以访问任何向其开放访问权限的文件、目录、设备或其他资源。使用 RBAC 时，进程根据分配的角色，仅能访问其被显式允许访问的资源。SELinux 实现 RBAC 的方式为进程分配一个 SELinux 策略。该策略按如下方式限制访问：

- 仅允许进程访问带有标签（labels）的资源
- 将潜在的不安全特性（如写入目录）作为布尔值（Booleans）提供，可以开启或关闭

具有 SELinux 策略的服务（如 Web 服务器）在安装时通常会在特定目录和文件设置 SELinux 标签。这使得运行的服务器进程只能从特定目录中读写文件。如果你想在进程想要访问的文件和目录上添加 SELinux 标签。

SELinux 并不是 DAC 的替代品。相反，它是一个额外的安全层。

- 先检查 DAC 规则，如果允许访问，然后检查 SELinux 策略。
- 如果 DAC 拒绝访问，则不检查 SELinux 策略。

如果用户尝试执行一个他们没有访问权限（rw-）的文件，“传统的”DAC 控制将拒绝访问。因此，SELinux 策略甚至不会被检查。

> SELinux 是 Red Hat 发行版的默认安全增强功能，而 AppArmor 则是 Ubuntu 的默认安全增强功能。你可以使用命令 `sudo apt-get install policy-selinux` 在 Ubuntu 上安装 SELinux。然而，截至本文编写，Ubuntu 的 SELinux wiki 页面建议不要使用 Ubuntu 的 SELinux 策略（https://wiki.ubuntu.com/SELinux）。如果你想了解更多关于 AppArmor 的信息，请访问 https://ubuntu.com/community/AppArmor。

尽管“传统的”Linux 控制仍然有效，但使用 SELinux 仍有许多优势。以下是 SELinux 的某些优势：

- 它实现了 RBAC 访问控制模型。这是最强大的访问控制模型。
- 它对主体（例如用户和进程）使用最小权限访问。最小权限术语意味着每个主体都被赋予一组有限的权限，这些权限足以使其在任务中正常运行。通过实施最小权限，限制了用户或进程对对象可能造成的意外（或故意的）伤害。
- 它允许进程沙箱化。进程沙箱化的术语意味着每个进程都运行在自己的区域（沙箱）中。除非授予特殊权限，否则它无法访问其他进程或其文件。进程运行的区域都是领域（domains）。
- 它允许在实施之前对其功能进行测试。SELinux 具有许可模式（permissive mode），允许你查看 SELinux 对系统产生的影响。在许可模式下，SELinux 仍然会记录它认为的安全违规行为（称为 AVC 拒绝），但不会阻止其发生。

另一种查看 SELinux 优势的方法是检查如果 Linux 系统上未启用 SELinux 会发生什么。例如，回到 Web 服务器示例，你的 Web 服务器守护进程（httpd）正在监听一个端口。来自网络浏览器的简单请求访问主页。按照常规程序，应用了传统的 Linux 安全。在没有 SELinux 约束的情况下，httpd 可以执行以下操作：

- 根据所有者和组的读/写/执行权限访问任何文件或目录
- 执行不安全的活动，如允许文件上传或更改系统限制
- 监听允许传入请求的任何端口

在受 SELinux 约束的系统上，受到了严格控制。使用前面的示例，httpd 只能在 SELinux 允许的端口上监听。SELinux 防止 httpd 访问任何未设置正确安全上下文的文件，并拒绝 SELinux 未显式允许的不安全活动。从本质上说，SELinux 极大限制了恶意代码的访问并泛限制了 Linux 系统上的活动。

## 理解 SELinux 如何工作

SELinux 可以比作门口的守卫。在这个类比中，主体（用户）想要访问房间内部的对象（文件）。为了访问该对象，必须执行以下操作：

1. 主体必须向守卫出示证件。
2. 守卫查看证件和记录在大手册中的访问规则。
   a. 如果规则允许此特定的证件进入门，主体即可进入房间访问对象。
   b. 如果规则不允许此特定的证件访问对象，守卫拒绝进入。

SELinux 提供了基于角色的访问控制（RBAC）与强制类型（TE）或多级安全（MLS）的结合。在基于角色的访问控制中，对对象的访问基于主体在组织中分配的角色。因此，它基于主体的用户名或进程 ID。每个角色都被授予了访问权限。

### 理解类型强制 (Type Enforcement)

类型强制（TE）是实现 RBAC 模型的必要。类型强制通过以下方法确保系统安全：

- 将对象标记为特定的安全类型
- 将主体分配给特定的域和角色
- 提供允许某些域和角色访问某些对象类型的规则

该示例遵循了 `ls -l` 命令，展示了文件 `my_stuff` 的 DAC（自主访问控制）控制情况。输出显示了文件的所有者（johnd）和组（johnd），以及其权限分配情况。

如果你需要检查文件权限，请参阅第 4 章“在文件系统中穿行”。

```
$ ls -l my_stuff
-rw-rw-r-- 1 johnd johnd 0 Feb 12 06:57 my_stuff
```

该示例包含了 `ls -lZ` 和同一个文件 `my_stuff`，但与 DAC 控制不同的是，`-Z` 选项还显示了 SELinux 的 RBAC 控制。

```
$ ls -lZ my_stuff
-rw-rw-r-- .. johnd johnd unconfined_u:object_r:user_home_t:s0 ... my_stuff
```

`ls -Z` 示例显示了与文件相关的四个 SELinux 特有项：

- `user` (unconfined_u)
- `role` (object_r)
- `type` (user_home_t)
- `level` (s0)

这些 RBAC 项目（用户、角色、类型和级别）被用于 SELinux 访问控制，以确定适当的访问级别。它们统称为 SELinux 安全上下文。安全上下文（身份标识）有时也被称为安全标签。

这些安全上下文分配分配给主体（进程和用户）。每个安全上下文根据其被分配的对象或主体而获得一个通用名称：文件具有文件上下文，用户具有用户上下文，进程具有进程上下文（也称为域）。

允许访问的规则被称为允许规则或策略规则。策略规则是 SELinux 用于授予或拒绝对特定系统类型访问权限的过程。回到 SELinux 与守卫（guard）的比较中，SELinux 充当守卫的角色，在允许或拒绝对对象的访问之前，必须查看主体的安全上下文（身份标识）并审查策略规则（访问规则手册）。因此，类型强制确保只有某些“类型”的主体可以访问某些“类型”的对象。

### 理解多级安全 (Multi-Level Security)

在 SELinux 中，默认策略类型称为目标策略（targeted policy），它主要控制 Linux 系统上的网络服务（如 Web 服务器和文件服务器）如何被访问。目标策略对系统中有效用户账户的限制较少。对于更严格的策略，你可以选择多级安全（MLS）。MLS 使用类型强制以及安全许可（security clearances）这一额外功能。它还提供了多分类安全（MCS），为对象提供了分级级别。

> 提示
>
> 多级安全的名称可能会引起混淆。多分类安全（MCS）有时被称为多级许可安全，由于 MLS 提供了 MCS，所以它有时被称为 MLS/MCS。

多级安全执行 Bell-LaPadula 强制性访问模型。Bell-LaPadula 模型由美国政府开发，旨在提供信息机密性。该模型的实现是通过根据角色的安全许可和对象的分级级别来授予对象访问权限。

安全许可是授予允许访问机密对象的属性。分级是授予对象的属性，用于防止安全许可属性过低的主体访问。你可能听说过“秘密（secret）”分级级别。虚构书籍和电影角色詹姆斯·邦德拥有特级安全许可，这使他能够访问特级机密信息。这是 Bell-LaPadula 模型的经典示例。

RBAC 与类型强制或多级安全的结合，使得 SELinux 能够提供如此强大的安全增强。SELinux 还为其使用提供了不同的运行模式。

### 实现 SELinux 安全模型

基于角色的访问控制模型、类型强制、多级安全以及 Bell-LaPadura 模型都是非常有趣的话题。SELinux 通过四个 SELinux 策略组件组合来实现这些模型：

- 运行模式
- 安全上下文
- 策略类型
- 安全规则包

尽管我们已经接触了这些设计元素，但接下来的内容将让你对它们深入理解。在开始修改系统上的 SELinux 配置之前，需要这种理解。

### 理解 SELinux 运行模式

SELinux 带有三种运行模式：禁用（disabled）、许可（permissive）和强制（enforcing）。每种模式都为 Linux 系统安全提供了不同的益处。

#### 使用禁用模式 (disabled)

在禁用模式下，SELinux 被关闭。取而代之的是默认访问控制方法自主访问控制（DAC）。这种模式适用于不需要增强安全的情况。

如果可能，红帽建议将 SELinux 设置为许可模式而不是直接禁用它。在某些情况下，禁用 SELinux 是恰当的。

如果你运行的应用程序（从你的角度来看）工作正常，但产生了大量的 SELinux AVC 拒绝消息（即使在许可模式下也是如此），你可能会导致日志文件填满，甚至使系统无法使用。更好的方法是对你需要访问的文件设置安全上下文。尽管如此，禁用 SELinux 是更快的解决办法。

然而，在禁用 SELinux 之前，请考虑你以后可能想在该系统上启用它。如果你决定在稍后将其设置为强制或许可模式。

#### 使用许可模式 (permissive)

在许可模式下，SELinux 已开启，但不会执行安全规则。许可模式用于：

- 审计 SELinux
- 测试新应用程序以查看 SELinux 的情况
- 测试新策略规则以查看 SELinux

#### 使用强制模式 (enforcing)

名称已说明了一切。在强制模式下，SELinux 已开启，并且所有的安全规则都被执行。

### 理解 SELinux 安全上下文

如前所述，安全上下文用于分类对象（如文件）和主体（如用户）。安全上下文由四个属性组成：用户、角色、类型和级别。

**用户** 用户属性是将 Linux 用户名映射到 SELinux 名称。这不同于用户名，它特指用户。SELinux 用户名以 u 结尾，以便在输出中识别。普通无限制用户在默认策略中具有 `unconfined_u` 属性。
