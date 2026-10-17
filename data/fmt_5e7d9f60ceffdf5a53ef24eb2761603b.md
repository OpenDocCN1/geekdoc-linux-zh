
annobin (if gcc or clang) is needed by (installed) redhat-rpm-config-99-1.el9noarch

(gcc-plugin-annobin if gcc) is needed by (installed) redhat-rpm-config-99-1.el9noarch

`[root@server1 Packages#]`

## 依赖关系与 dnf 命令
图 4-4

这些包存在依赖关系。

`[root@server1 Packages#] rpm -ivh gcc-11.3.1-21.el9.x86_64.rpm glibc-devel-2.34-40.el9.x86_64.rpm annobin-10.73-3.el9.x86_64.rpm gcc-plugin-annobin-11.3.1-2.el9.x86_64.rpm`

error: Failed dependencies:

glibc-headers >= 2.34-40.el9 is needed by glibc-devel-2.34-40.el9.x86_64

kernel-headers >= 3.2 is needed by glibc-devel-2.34-40.el9

libcrypt-devel(x86-64) >= 4.0 is needed by glibc-devel-2.34-40.el9

`[root@server1 Packages#]`

图 4-5

还有更多的依赖关系。

5. 输入 `rpm -ivh`，然后输入图 4-3 中列出的包。为了此目的使用命令补全非常方便；例如，如果你输入：

```bash
# rpm -ivh glibc-devel
```

`glibc-devel-`。你可以双击键查看以这些额外字母开头的可用包并再次按键完成包名。

6. 经过一番努力，你将得到与图 4-4 所示类似的命令和结果。这实际上取决于每个包的当前版本级别，以及本地系统中已安装的内容。

7. 下一步尝试将缺失的依赖包含待安装包列表中。当我们尝试这一步时，会导致图 4-5 所示的命令和结果。

## 第4 章 软件管理

在 yum 之前，RHEL 在更新过程中包含了依赖关系解决。在 RHEL 4 中，这是通过 update 完成的。Red Hat 从 RHEL 5 开始引入 yum。从 RHEL 8 开始，yum 是 dnf 的符号链接，dnf 是下一代包管理器，它支持所有的 yum 命令选项以及更多功能。

使用 dnf，要安装图 4-4 列出的软件包，你只需要运行以下命令：

```bash
# dnf install gcc
```

如果系统提示，接受安装额外依赖包的请求，所有提到的依赖项将自动安装。（使用 `-y` 选项也可以执行相同的功能。）如果连接的存储库中有可用更新，将安装每个软件包的最新版本。dnf 命令将在本章稍后的部分进行详细介绍。

但是，如果你运行的是 RHEL 9 且没有连接到红帽订阅管理（Red Hat Subscription Management），则什么都不会发生。稍后，你将看到如何操作。

RHEL 有许多第三方仓库可供选择。它们包含了红帽不支持的热门应用程序。例如，本书的一位作者使用外部仓库来安装与他的笔记本网卡相关的软件包。

尽管这些仓库的所有者与红帽开发人员密切合作，但有报告显示，从一个仓库所需的依赖项在其他仓库中不可用，导致了另一种形式的“依赖地狱”。然而，最流行的第三方仓库是非常优秀的；我们在使用这些仓库时从未遇到过依赖地狱。

> 红帽不包含来自第三方仓库的经过验证且流行的软件包主要有两个原因。某些软件包没有以开源许可发布，另一些则是红帽简单选择不支持的软件包。

![](img/9c00a73030da5bd310455c3e10fece4d_180_0.png)

### 红帽订阅管理

可靠的依赖关系取决于 dnf 的正确配置。你不仅需要知道如何配置 dnf 通过互联网连接到存储库，还需要如何配置 dnf 连接到局域网。

RHCSA 目标要求候选人能够“从红帽网络安装和更新软件软件包”。如前提到的，红帽已被红帽订阅管理取代，但考试目标继续使用其旧名称来指代该服务。访问红帽订阅管理可以通过互联网或本地的红帽 Satellite 服务器提供。

## 依赖关系与 dnf 命令

可能红帽 Satellite（或 Spacewalk Katello 等替代方案）的主要优势在于可以在网络上的本地系统上存储软件包。一旦从客户端配置了适当的连接，Satellite 服务器就可以按照任何时间表运行远程命令。如果你在管理整个系统群，红帽 Satellite 支持组配置。如果有 10 个系统被配置为 RHEL Web 服务器，你可以将这些系统配置为一个组组。然后，你可以调度单个命令以远程应用于所有系统。有关红帽 Satellite 的更多信息，请参阅最新版本的文档，该文档可从 https://access.redhat.com/products/ 获得。然而，这超出了 RHCSA 考试的范围。

如果你已经像第 1 章中安装的那样参加了红帽开发者计划，那么你有权使用红帽开发者订阅。练习 4-2 解释了如何将你的系统连接到 RHSM。

## 练习 4-2

### 将系统订阅到红帽订阅管理

1. 如果你还没有这样做，请加入红帽开发者计划并在 https://developers.redhat.com 注册。如果你没有账户，请创建一个新的。
2. 将浏览器指向 https://access.redhat.com/management/subscriptions/。你应该在库存中看到“个人版红帽开发者订阅”（Red Hat Developer Subscription for Individuals）。此订阅允许你注册 RHEL 系统并从 RHSM 下载更新。
3. 登录到第 1 章中安装的 server1.example.com。运行以下命令向 RHSM 注册你的系统。系统将提示输入红帽用户名和密码。如果系统已经注册，请使用 `force` 命令重新注册机器。
4. 将系统订阅到红帽产品。在以下命令中，`--auto` 选项会寻找最合适的订阅（如果没有其他订阅，将是红帽订阅）：
5. 或者，列出所有可用订阅。注意 pool ID。
```bash
# subscription-manager register
# subscription-manager attach --auto
# subscription-manager list --available
```
然后，使用从中获取的 pool ID 附加系统：
```bash
# subscription-manager attach --pool=2c94b80c497b018823f74eb
```

6. 运行当前设置。运行以下命令列出附加到系统的订阅：
```bash
# subscription-manager list
```
命令输出应类似于：
```text
--------------------------------+
Installed Product Status
--------------------------------+
Product Name:    Red Hat Enterprise Linux for x86_64
Product ID:      479
Version:        9.2
Arch:           x86_64
Status:         Subscribed
Status Details:  
Starts:         05/11/2023
Ends:           05/10/2024
```

7. 显示所有存储库：
```bash
# subscription-manager repos
```

8. 显示当前启用的存储库：
```bash
# subscription-manager repos --list-enabled
```
命令输出应类似于：
```text
--------------------------------+
Available Repositories in /etc/yum.repos.d/redhat
--------------------------------+
Repo ID:   rhel-9-x86_64-baseos-repos
Repo Name: Red Hat Enterprise Linux 9 for x86_64 BaseOS (RPMs)
Repo URL:  https://cdn.redhat.com/content/dist/hel9/release/x86_64/baseos/os
Enabled:  1
Repo ID:   rhel-9-x86_64-appstream-repos
Repo Name: Red Hat Enterprise Linux 9 for x86_64 AppStream (RPMs)
```
