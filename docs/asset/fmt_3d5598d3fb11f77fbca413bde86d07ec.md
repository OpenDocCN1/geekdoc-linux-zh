
RPM 的一个方便功能是，它可以防止你移除其他包所需要的包。例如，如果我们尝试移除 `kernel-headers` 包（回想一下 `gcc` 包依赖它），我们将看到以下内容：

### 第3 章：软件管理

```
[root@fedora-serverA ~]# rpm -e kernel-headers
error: Failed dependencies:
  kernel-headers is needed by (installed) glibc-headers-2.8-3.i386
  kernel-headers >= 2.2.1 is needed by (installed) glibc-headers-2.8-3.i386
```

> 注意 记住 `glibc-dev*` 包依赖另一个包，即 `glibc-headers`。

## 使用 RPM 可以做的其他事情

除了基本的安装和卸载外，RPM 还有许多其他可以的操作。在本节中，我们将介绍其中的一些。

### 验证软件包

RPM 的一个有用选项是验证软件包的功能。其原理是 RPM 查看数据库中的软件包信息（假设这些信息是正确的），然后将其与系统上的二进制文件和文件进行对比。在当今这个被黑客攻击是一个现实可能的世界上，这可以立即告诉你是否有人对你的系统做过什么。

### 软件包校验

RPM 的另一个功能是软件包可以进行数字签名。这提供了一种内置的身份验证机制，允许用户确定拥有的软件包确实是由预期（信任）的一打包的，并且该软件包在传输传输过程中没有被篡改。

你有时可能需要验证为什么在之前尝试安装软件包时看到某些警告（例如此信息：“Warning: lynx-2.*.rpm: Header V3 DSA Signature: NOKEY, key ID 4f2a6fd2”）。为了防止此警告信息，你应该将 Fedora 的数字密钥导入系统密钥类型中。

```
[root@fedora-serverA ~] # rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-fedora
```

你可能还需要将其他供应商的密钥导入密钥环。为了额外确信即使是你拥有的本地密钥也不是伪品，你可以直接从供应商的网站导入密钥。例如，要从 Fedora 项目站点导入密钥，你将输入

```bash
[root@fedora-serverA]# rpm import http://download.fedora.redhat.com/pub/fedora/linux/releases/9/Fedora/i386/RPM-GPG-KEY-fedora
```

### Yum

Yum 是 Linux 系统上软件管理较新的方法之一。它基本上是 RPM 的一个封装程序，并带有极大的增强。它已经存在了一段时间，但由于 Linux 供应商决定专注于其（利润更丰厚的）商业产品，Yum 变得更加广泛地使用并更加突出。Yum 改变并增强了基于 RPM 的系统的传统软件包管理方法。作为开源软件存储库的热门网站必须稍作调整以适应“Yum 化”的存储库。根据 Yum 的网页介绍：

- “Yum 是 RPM 系统的自动更新程序和软件包安装器/删除程序。它会自动计算依赖关系，并确定安装软件包时应该发生哪些操作。它更容易管理了一组机器，而无需手动使用 RPM 更新每台机器。”

这个总结还是有些保守了。Yum 提供的功能远多于此。某些新的发行版严重依赖 Yum 提供的功能。

在支持的系统上使用 Yum 非常简单。你通常只需要一个配置文件（`/etc/yum.conf`）。其他配置文件可能存储在 `/etc/yum.repos.d/` 目录下，指向启用了 Yum 的（Yum 化）软件存储库。幸运的是，几个 Linux 发行版在出厂时已经安装并预配置了 Yum。Fedora 就是其中之一。

在 Fedora 系统（或任何其他类 Red Hat 发行版）上使用 Yum——在命令行安装 `gcc` 软件包，你将输入

```bash
[root@fedora-serverA]# yum install gcc
```

Yum 会自动处理该软件包可能需要的任何依赖关系，并为你安装该软件包。（第一次运行时，它将建立其缓存。）Yum 会帮你洗碗（实际效果可能因人而异）。Yum 还具有极其强大的搜索功能，可以帮助你找到某个软件包，即使你不知道它的正确名称。你只需要知道名称的一部分。例如，如果你想搜索所有包含“headers”单词的软件包，可以尝试如下 Yum 选项：

```bash
[root@fedora-serverA]# yum search headers
```

这将返回一个长长的匹配列表。然后你可以查看列表并选择你需要的软件包。

> 注意：默认情况下，Yum 尝试访问位于互联网上某处的存储库。因此，你的系统在默认状态下需要能够访问互联网才能使用 Yum。你可以在本地文件系统或本地局域网（LAN）上创建自己的本地软件存储库并将其 Yum 化。只需将发行媒体（DVD/CD）的所有内容复制到某处，并针对目录位置运行 `yum-arch` 命令即可。

## UBUNTU 中的软件管理

正如我们之前提到的，Ubuntu 等类 Debian 发行版的软件管理是使用 DPMS 及其所有相关工具（如 APT 和 `dpkg`）完成的。在本节中，我们将查看如何在 Debian 类发行版上执行基本的软件管理任务。

### 查询信息

在你的 Ubuntu 服务器上，列出所有已安装软件的等效命令是

```bash
yyang@ubuntu-server:~$ dpkg -l
```

获取已安装软件包基础信息的命令是

```bash
yyang@ubuntu-server:~$ dpkg -l bash
```

获取关于 `bash` 软件包更详细信息的命令是

```bash
yyang@ubuntu-server:~$ dpkg --print-avail bash
```

要查看 `bash` 软件包随附的文件列表，请输入

```bash
yyang@ubuntu-server:~$ dpkg-query -L bash
```

`dpkg` 的查询功能非常强大。你可以使用 DPMS 查询有关软件包的特定信息。例如，要查找已安装 `bash` 软件包的大小，你可以输入

```bash
yyang@ubuntu-server:~$ dpkg-query -W --showformat='${Package} ${Installed-Size}\n' bash
```

### 在 Ubuntu 中安装软件

在 Ubuntu 系统上安装软件有多种方法。你可以使用 `dpkg` 直接安装 `.deb`（读作 dot deb）文件，你也可以选择使用 `apt-get` 安装 Ubuntu Ubuntu 存储库或本地（CD/DVD-ROM、文件系统等）中可用的任何软件。

> 注意：在系统上安装和卸载软件被视为管理或特权功能。这就是为什么任何需要超级权限的命令前面都有 `sudo` 命令。`sudo` 命令可用于在特权用户（或另一个用户）的上下文中执行命令。另一方面，查询软件数据库不被视为特权功能。你可以使用 `dpkg` 安装 `.deb` 软件包 `lynx_2.8.6-2ubuntu2_i386.deb`

```bash
yang@ubuntu-server:~$ sudo dpkg --install lynx_2.8.6-2ubuntu2_i386.deb
```

使用 `apt-get` 安装软件简单一点，因为 APT 通常会为你处理任何依赖问题。唯一的注意事项是 `sources.list` 文件（`/etc/apt/sources.list`）中配置的存储库必须通过互联网或本地可访问。安装软件的另一个优势是只需要知道名称的一部分，不需要知道确切版本。使用 `apt-get` 安装软件：

```bash
yang@ubuntu-server:~$ apt-get install 
```

### 在 Ubuntu 中移除软件

在 Ubuntu 中使用 `dpkg` 卸载软件非常简单

```bash
yyang@ubuntu-server:~$ dpkg --remove
```

你也可以通过 `apt-get` 的 `remove` 选项移除软件

```bash
yyang@ubuntu-server:~$ apt-get remove
```

使用 APT 卸载软件的一种不太常用的方法是在软件包名称前加上减号。APT 可以轻松地从系统中完全移除软件及其配置文件。这允许你通过消除自定义配置从头开始。假设我们要从系统中完全移除 `lynx` ，我们将使用

```bash
yyang@ubuntu-server:~$ sudo apt-get --purge lynx
```

## 编译与安装 GNU 软件

开源软件的一个主要优势是你可以获得源代码。如果开发者选择停止维护该软件，你可以继续开发（如果你懂的话）。如果你发现问题，可以自己修复它。否则，你将掌握局面的主动权，而不是受控于你无法控制的商业开发者的摆布。但拥有源代码意味着你将能够编译它；否则，你拥有的仅仅是一堆无法运行的文本文件。
