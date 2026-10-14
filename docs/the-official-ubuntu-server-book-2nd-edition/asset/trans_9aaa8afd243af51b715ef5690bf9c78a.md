

第一项将是一个 # 符号，表示该行为注释，或者是 deb 或 deb-src。这指定了仓库是源代码包仓库还是二进制包仓库。第二项是位置，采用 URI 形式。第三项是发行版的名称，或者更准确地说，是发行版版本。在之前的示例中，该发行版版本是 lucid，它指的是 Ubuntu 的 Lucid Lynx 版本。剩余的参数是组件列表。核心 Ubuntu 仓库中提供的组件在下一节中详细介绍。

一个示例有助于说明添加仓库的过程。如果我想安装 Bazaar 的最新发布版本，我需要从默认的 Ubuntu 仓库之外获取，因为默认仓库仅根据 Ubuntu 发布周期进行更新。幸运的是，Bazaar 开发者提供了自己的“个人包仓库”——这是我在本章结尾会再次提及的内容。在他们的网站上，他们提供了我可以直接放入 sources.list 的 deb 和 deb-src 行：

```
deb http://ppa.launchpad.net/bzr/ubuntu lucid main
deb-src http://ppa.launchpad.net/bzr/ubuntu lucid main
```

如果我执行更新，我首先会收到一个错误，声称我没有正确的加密密钥来验证仓库中的软件包是否确实来自 Bazaar 开发者：

```
W: GPG error: http://ppa.launchpad.net lucid Release: The following
signatures couldn't be verified because the public key is not
available: NO_PUBKEY FE8956A73C5EE1C9
```

我可以轻松地通过从可信来源（如 PPA 提供商的网站）下载密钥并将其保存到文件中（示例中称为 /tmp/keyfile），验证其正确性，然后使用如下命令将其添加到包管理器的密钥数据库中

```
apt-key add - < /tmp/key
OK
```

apt-key 手册页提供了有关如何使用此有用的命令管理仓库密钥的更多详细信息。

## Ubuntu 默认仓库

你所需的大多数软件包都已为 Ubuntu 打包。这是因为，利用 Debian 的工作，Ubuntu 提供了对绝大多数最受欢迎的自由软件的访问，这些软件作为其自己的仓库中的软件包提供。

这些数万个软件包被划分为一系列不同的部分或组件。你可以通过在 sources.list 的组件列表中包含它们来打开或关闭这些组件。由于这对你将获得的软件支持水平有重要影响，因此了解这些不同的组件是值得的，以便你可以决定从哪些区域获取软件。Ubuntu 服务器上可用的组件包括 main、restricted、universe 和 multiverse。以下描述改编自 Ubuntu 网站上的组件描述。

- **Main**
  主发行版组件包含可自由重新分发的自由软件，并由 Ubuntu 团队完全支持。其中包括最受欢迎和最可靠的开源应用程序，其中许多在安装 Ubuntu 时默认已安装。main 中的软件包括 Ubuntu 开发者、社区和用户认为重要且 Ubuntu 安全和发行团队愿意支持的手选应用程序列表。当你从 main 组件安装软件时，可以保证该软件将附带安全更新和技术支持。

- **Restricted**
  restricted 组件保留给使用非常广泛且由 Ubuntu 团队支持的软件，即使它不是在完全自由的许可证下提供的。请注意，由于 Ubuntu 团队无法修复软件，只能将问题报告转发给实际作者，因此 Ubuntu 可能无法为此软件提供完整支持。

- **Universe**
  在 universe 中可以找到几乎所有开源软件以及在各种较不开放的许可证下提供的软件，所有这些软件都是从各种公共源自动构建的。所有这些软件都是针对构成 main 的库并使用其中的工具编译的，因此它应该能与 main 中的软件一起安装并正常工作，但*它不提供安全修复和支持的保证*。

- **Multiverse**
  multiverse 组件包含非自由软件，这意味着该软件的许可要求不符合“main”组件的许可政策。验证你使用该软件的权利并遵守版权持有者的许可条款的责任在于你。此软件不受支持，通常无法修复或更新。自行承担风险使用。

## 使用其他仓库

正如我在几节之前添加 Bazaar 仓库时所看到的，用户仍有时希望使用超出 Ubuntu 提供的各种外部仓库。例如，用户可能希望从 Ubuntu 开发版本安装特定应用程序或库的新版本，但可能不想将所有软件包升级到最新版本。

Ubuntu 中准官方的“backports”仓库是一个有用的资源。它包含从 Ubuntu 开发版本回溯移植到可在 Ubuntu 稳定版本上干净安装的软件版本。你可以通过手动使用 dpkg 一次安装一个 DEB 软件包来添加 backports，也可以通过在 sources.list 中添加一行额外内容来添加。有关这两种方法的详细信息可以在 Ubuntu 网站 https://help.ubuntu.com/community/UbuntuBackports 上找到。

许多用户选择 à la carte 方法的原因——即手动下载软件包并使用 dpkg 安装它们的方法——而不是直接添加仓库，是因为

