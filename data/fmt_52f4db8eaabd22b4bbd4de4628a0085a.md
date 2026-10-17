
- Libvirt 网络过滤器
    - `http://bit.ly/libvirt`
- Web Security Dojo 3.0
    - `http://bit.ly/WebDojo`

本教程已在 Debian Jessie 64位系统上经过测试。

我们都熟悉关于信息访问（或 ATAWAD）的“三个任意”概念：随时随地、任何设备。虚拟桌面基础架构（VDI）正是这种承诺的一种体现：如今，拥有一个完整的计算机教室并在每一台机器上部署独立的镜像似乎已毫无意义。毕竟，我们生活在云时代。VDI 应运而生。当然，这并不是我们能为 VDI 技术找到的唯一用途。渗透测试、恶意软件分析和取证也是众所周知的场景，在这些场景中，VDI 中间件可以扭转局势！RAVADA VDI 就是一个这样现成可用的 VDI 框架。其后端的设计和实现旨在允许通过 REST API 向框架添加未来的虚拟化程序。这一点非常棒，因为你不必担心 KVM 某日会过时：RAVADA VDI 肯定会支持未来流行的虚拟化程序。部署此框架将帮助你设计和管理渗透测试训练场景，在这些场景中，你可以测试任何疯狂、非常规的概念验证（PoCs），而不会损坏任何单一系统。

截至本文撰写之时，RAVADA VDI 仅支持 KVM 虚拟化程序，这意味着你需要为内核加载适当的模块。因此，如果你有基于 Intel 的处理器，请运行（作为 root）：`modprobe kvm-intel`。对于基于 AMD 的处理器，请运行：`modprobe kvm-amd`。

从最终用户的角度来看，唯一的要求是一个 web 浏览器和一个支持 SPICE 协议的远程查看器（例如，`apt-get install virt-viewer`）。

## 嵌套 KVM

你可以在具有嵌套 KVM 功能的计算机上设置该框架。这样你可以在部署之前先尝试 RAVADA VDI。你可以使用 libvirt 及其 `vir-manager` 工具创建一个新的虚拟机，然后在该虚拟机上安装 RAVADA VDI。首先确保你的处理器支持嵌套 KVM：`cat /sys/module/kvm_intel/parameters/nested`。如果输出为 'Y' 或 '1'，则说明可以使用。如果你没有嵌套 KVM 功能，不要惊慌：你仍然有机会拥有它：卸载 kvm 模块，然后使用 `nested=1` 参数重新加载它：

```
modprobe kvm-intel nested=1
```

## 在 Debian 上安装和使用 RAVADA VDI

如果你想在 Debian Jessie 上使用此 VDI 中间件，你需要先进行一些更改（参见资源）。请注意，RAVADA VDI 尚未在 6 月 17 日发布的 Debian Stretch 上进行测试。

克隆该存储库并开始研究其内部结构。代码是用 Perl 5 和 AngularJS 编写的。RAVADA VDI 背后的开发团队实施了一系列测试，以确保在发布新版本之前一切正常。你需要做的第一件事是克隆它：

```
git clone https://github.com/UPC/ravada.git
```

现在根据文档安装其先决条件。在 `ravada` 目录中，运行：`perl Makefile.PL`，然后以 root 身份执行所有测试：`make test`。RAVADA VDI 可以从其源代码或使用 DEB 包进行安装。要生成该包，`deb` 目录中有一个 Perl 脚本；请尝试使用：`deb/debianize.pl`。

## 夺旗

说到渗透测试，培训是强制性的。那里已经有大量准备好的虚拟机和在线系统，供你测试技能而不违反法律。当然，这很好，但为什么不想得更大一些呢？通过使用 VDI 中间件，你可以设置一个环境，让每一个渗透测试学员使用各自独立的 VDI 针对共享的虚拟机执行不同的测试和攻击。该想法是在 RAVADA VDI 中创建一个新虚拟机，学员将使用所有必要的工具，然后将其设为公共。这样，每个经过身份验证的用户都可以通过 SPICE 协议（参见资源）连接到它。

得益于 QCOW2 格式，一旦你创建了新虚拟机并将其作为基础镜像，每个用户的额外实例占用的磁盘空间将比原始虚拟机少得多。截至撰写时，RAVADA VDI 尚未在 GUI 中实现添加新 VDI XML 定义或 ISO 镜像的选项，但情况并不糟糕！接下来，你将准备你的 VDI 框架以容纳 Kali Linux（这将成为你学员的虚拟桌面）。

![](img/fb76008333fb7aef815b136f9f1afe5f_40_0.png)

**上图** 厌倦了在命令行中输入冗长烦人的命令吗？别担心！GUI 来了！

> RAVADA VDI 后端的设计和实现旨在允许未来的虚拟化程序添加到该框架中

## 创建渗透测试机器

下载 Kali Linux 64位（参见资源）并将其保存到 RAVADA VDI 服务器的 `/var/lib/libvirt/images`。计算其 SHA256，并确保其与项目网站上的相匹配。然后，你需要执行一条 INSERT SQL 语句以更新 MySQL 数据库服务器中的 `iso_images` 表。INSERT 语句非常简单：表中的每个字段都比较直观。将 `file_re` 字段的值设置为 ISO 的名称，将 `md5_*` 字段填充为 NULL，不要忘记设置 `sha256` 为对应的哈希值。最后，`sha256_url` 应指向 `https://codimage.kali.org/current/SHA256SUMS`。

第二步是为新虚拟机准备两个 XML 文件。第一个将保存所有机器定义 – 处理器数量、网络接口、USB 通道等等。第二个是卷定义。从其他任何虚拟机复制这两个文件并重命名：`cd /var/lib/ravada/xml/; cp jessie-amd64.xml kali-amd64.xml; cp jessie-volume.xml kali-volume.xml`。使用你喜欢的 ASCII 编辑器编辑 `kali-amd64.xml`，并确保相应更改磁盘和 CD-ROM 虚拟磁盘定义：

```
<source file='/var/lib/libvirt/images/kali64.img'/>
<source file='/var/lib/libvirt/images/kali-2017.1-amd64.iso'/>
```

接下来，打开你的 RAVADA VDI Web 界面并导航到 Admin Tools > Machines，然后单击 New Machine。确保你在下拉列表中选择了 'Kali Linux' ISO 镜像。一旦你对虚拟机设置满意，请单击 Create。现在等待一会儿，直到机器创建完成。你可以使用 ‘Start’ 按钮启动机器，并单击 ‘View’ 连接它。继续进行 Kali 的正常安装，并添加你认为学员需要的任何额外包或工具。一旦你认为该机器已准备好部署，请勾选 Base 和 Public 复选框：从现在开始，任何已注册的 RAVADA VDI 用户都能使用各自独立的 Kali Linux VDI 实例，独立于其他实例运行。

RAVADA VDI 支持两种不同的身份验证机制。第一种是 LDAP；你可以将你的 RAVADA VDI 绑定到现有的 LDAP 服务器。如果你没有 LDAP...

## 开源 VDI 解决方案

除了 RAVADA VDI 之外，还有一堆免费（其中一些是开源的）VDI 项目。它们中的大多数基于 KVM (`http://bit.ly/VDI-KVM`)。RAVADA VDI 致力于不依附于任何特定的虚拟化程序；截至本文撰写之时，它仅支持 KVM，但其他虚拟化程序也在路线图之上（例如 LXDI）。所以如果你想帮助那些人，请不要害羞。

### 渗透测试

![](img/fb76008333fb7aef815b136f9f1afe5f_41_0.png)

**取证与恶意软件分析**

使用 `Q2le`

同样非常适合取证追踪。RAVADA `vcl2` 支持 QCOW2 磁盘映像，可以从命令行直接挂载这些映像，而无需启动虚拟机。此外，得益于 `libguestfs`，你不仅能挂载 QCOW2 映像，还能做更多事情。这对于取证和动态恶意软件分析非常有用（前提是虚拟机完全隔离。切记！）。

即使网络上的服务器出现问题，你仍然可以使用数据库认证方法创建新用户：用户将存储在 `users` 表中。`password` 字段将存储用户的密码，并使用 SHA-1 进行哈希处理；截至本文撰写时，该框架尚不支持盐值（salt）。要向你的 RAVADA VDI 服务器添加几个使用数据库认证的用户（`lud01` 和 `lud2`），请执行以下命令：`rwd_back --add-user lud01`；对 `lud2` 执行相同操作。使用 web 浏览器导航至 VDI Web GUI，并分别以 `lud01` 和 `lud2` 身份登录；你将能够在浏览器中访问 Kali 虚拟桌面；你可以对自己的虚拟桌面为所欲为，而不会影响其他用户。你会注意到连接并未受 TLS 通道保护；默认情况下，GUI 不提供任何设置加密的手段（目前尚未实现）。

## 从 OVA 到目标易受攻击服务器
