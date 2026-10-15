
# 第五部分：学习 Linux 安全技术

> ### 注意
> 在对生产 Linux 系统进行更改之前，请为 `system-auth-local` 创建备份并在测试环境中测试你的更改。错误的修改可能会导致所有人（包括 root 用户）被锁定在系统之外。

在前面的代码的第一条 auth 上文行 `pam_tally2.so` 中，注意增加了两个选项：`deny=3` 和 `quiet`。`deny=3` 选项允许用户仅尝试登录三次，账户就会被锁定。

`quiet` 选项在账户被锁定时不会告诉账户已锁定。它只会向用户保持“密码错误”的消息。如果你正受到攻击，让用户不知道账户发生了什么情况是有帮助的。恶意攻击者不会知道账户已被锁定，并认为他刚刚……

## 学习 Linux 安全技术

还有几个网站可以为你提供关于 PAM 的额外信息：

- Linux-PAM 官方网站：http://linux-pam.org
- Linux-PAM 系统管理员指南：http://linux-pam.org/Linux-PAM-html/Linux-PAM_SAG.html
- PAM 模块参考：http://linux-pam.org/Linux-PAM-html/sag-module-reference.html

### 总结

在学习 Linux 的过程中，加密工具和 PAM 都应该小心处理。在将任何修改应用于生产机器之前，请务必在测试 Linux 系统或虚拟化 Linux 系统上进行测试。

在将这些高级的加密和 PAM 工具添加到组织的安全生命周期的“实施”阶段之前，请审查你所提供的各种选项。一旦确定了组织需要这些高级工具的哪些功能，就将它们添加到你的实施阶段。

下一章将介绍 SELinux。虽然加密和 PAM 是可以在 Linux 系统上使用的工具，但 SELinux 是一个整个安全增强层。

### 练习

使用这些练习来测试你对加密工具和 PAM 的了解。这些任务假设你正在运行 Fedora 或红帽企业级 Linux 系统（尽管某些任务在其他 Linux 系统上也可以运行）。如果你遇到困难，任务的解决方案位于附录 B（尽管在 Linux 中，通常有多种方法可以完成任务）。

1. 使用 `gpg` 工具和对称密钥加密文件。
2. 使用 `gpg` 工具生成密钥环。
3. 列出你生成的密钥环。
4. 使用 `gpg` 工具加密文件并添加你的数字签名。
5. 访问 Linux Mint 主页 www.linuxmint.com。从下载页面中选择一个 Linux Mint 发行版进行下载。下载完成后，使用适当的消息摘要来确保下载的文件没有损坏。
6. 使用 `su` 命令确定 `su` 命令的完整文件路径。接下来，确定你 Linux 系统上的 `su` 命令是否感知 PAM。
7. `su` 命令是否有 PAM 配置文件？如果是，在屏幕上显示该配置文件并列出它使用的哪些 PAM 上下文（PAM contexts）。
8. 将你系统上的各种 PAM 模块列在屏幕上。
9. 在你的系统中找到 PAM 的 "other" 配置文件。它是否存在？它是否强制执行“隐式拒绝”（Implicit Deny）？
10. 在你的系统中找到 PAM limits 配置文件。它是否有设置可以防止你的系统发生派生炸（fork bomb）？

# 使用 SELinux 增强 Linux 安全

## 本章内容

- 学习 SELinux 的优势
- 学习 SELinux 如何工作
- 设置 SELinux
- 修复 SELinux 问题
- 获取有关 SELinux 的额外信息

安全增强 Linux（SELinux）是由美国国家安全局（NSA）与其他研究机构（如 Secure Computing Corporation, SCC）共同开发的。SELinux 于 2000 年发布到开源社区，并在红帽开始将 SELinux 作为默认包实现后变得流行。现在，SELinux 被许多组织使用并已广泛可用。

## 理解 SELinux 的优势

SELinux 是一个部署在 Linux 之上的安全增强模块。它提供了额外的安全措施，并默认包含在 RHEL 和 Fedora 中。

SELinux 通过对主体和对象（即进程和资源）实施实施基于角色的访问控制（RBAC），在 Linux 系统上提供了改进安全性。“传统的”Linux 安全使用的是裁量访问控制（DAC）。

> 大多数 SELinux 文档指出 SELinux 使用了强制访问控制（MAC）模型。记住 RBAC 是 MAC 的精炼版本（见第 22 章“理解基础 Linux 安全性”）。因此，文档说 SELinux 使用 MAC 是正确的。

SELinux 并不是 DAC 的替代品。相反，它是一个额外的安全层。

- 使用 SELinux 时仍然使用 DAC 规则。
- 先检查 DAC 规则，如果允许，则会检查 SELinux 策略。
- 如果 DAC 拒绝访问，则不检查 SELinux 策略。

如果用户尝试执行一个没有执行权限（`(rw-)`）的文件，“传统的”DAC 控制将拒绝访问。因此，SELinux 策略甚至不会不会被检查。

> 注意
> SELinux 是红帽发行版的默认安全增强，而 AppArmor 是 Ubuntu 的默认增强。你可以使用命令 `sudo apt-get install selinux` 安装 SELinux 并重启。如果你想了解更多关于 AppArmor 的信息，请访问 https://help.ubuntu.com/community/AppArmor。

尽管“传统的”Linux 控制仍然有效，但使用 SELinux 具有以下几个优势。其优势包括：

- 实施 RBAC 访问控制模型——这被认为是最强大的访问控制模型。
- 对主体使用最小权限访问（例如，用户和进程）——最小权限术语意味着赋予每个主体一组有限的权限，这些权限仅足够允许主体执行其任务。通过最小权限，可以防止它们对可能影响的对象造成意外损害。
- 允许进程沙箱化——进程沙箱化意味着每个进程运行在自己的区域（sandbox）中。除非授予特殊权限，否则这些区域被称为域（domains）。
- 在实施前允许 SELinux 进行测试——SELinux 有一个允许模式（Permissive mode），允许你查看 SELinux 对系统的影响。

另一种检查 SELinux 优势的方法是查看 SELinux 未运行时会发生什么。例如，来自 Web 浏览器的请求进入以查看主页。在常规操作中，httpd 守护进程接收请求并应用传统的 Linux 安全。在不受 SELinux 限制的情况下，httpd 能够：

受 SELinux 限制的系统中，httpd 能够：

- 访问任何文件或目录，基于所有者和组的权限。
- 执行可能不安全的活动，例如上传文件或更改限制。
- 监听它喜欢的任何端口。

在 SELinux 限制的系统中，httpd 受到更严格的控制。使用前面的示例，httpd 只能监听 SELinux 允许它监听的端口。从本质上说，SELinux 极大限制了系统上的恶意代码和活动。

## 理解 SELinux 如何工作

SELinux 可以比作门卫：在这种情况下，主体（用户）想要访问房间内的对象（文件）。为了获得访问：

1. 用户必须向门卫展示证件。
2. 门卫查看证件以及存在大型手册中的访问规则。
- 如果访问规则允许此 ID 进入对象，主体可以进入房间访问对象。
- 如果访问规则不允许此 ID 进入对象，门卫拒绝进入。

SELinux 提供了基于角色的访问控制（RBAC）与类型强制（TE）或多级安全（MLS）的结合。在基于角色的访问控制（见第 22 章）中，对对象的访问基于主体在组织中分配的角色。因此，它不是基于主体的用户名或进程 ID。每个角色被

### 类型强制

类型强制（TE）对于实施 RBAC 模型是必要的。类型强制通过以下方式确保系统安全：

- 将对象标记为特定的安全类型
- 将主体分配到特定的域和角色
- 提供包含域和角色的规则来访问对象类型

示例使用 `ls -1` 命令显示 `my_stuff` 的 DAC 控制。文件列出了所有者和组，以及对读、写、执行的分配。如果你需要回顾文件权限，请参见第 4 章“在文件系统中移动”。

```
$ ls -1 my_stuff

-rw-rw-r-- 1 johndoe johndoe 0 Feb 12 06:57 my_stuff
```

后续示例使用 `ls -Z` 查看同一个文件 `my_stuff`，但不仅显示 DAC 控制，`-Z` 选项还显示 SELinux 安全 RBAC 控制。

```
$ ls -Z r-rw-- my_stuff

-rw-rw--. johndoe johndoe

unconfined u:object:user_home_t:s0 my_stuff
```
