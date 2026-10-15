
# 软件包管理与 Debian 包系统

因此，大多数系统升级和 ABI/API 更改都是通过发行版之间的大型升级脚本完成的。用户预计会一次性安装涉及重大过渡的每个软件包，并使用升级脚本正确安排顺序并适当处理依赖关系。虽然这些问题是有限的软件包管理系统的局限性，但它们大多是存在于软件包管理系统之外的問題。在没有软件包管理系统的情况下，经历 API 和 ABI 更改的共享库要么从未或很少被处理（对一致性和安全性都有危险影响），要么受同样的限制而没有软件包系统提供的警告。

受 Debian 项目创建的名为 `dselect` 的程序以及其备受称赞的高级打包工具 `APT`，最初名为 `deity`，主要在名为 `apt-get` 的程序中实现 的推动，过去几年见证了软件包管理器范围和成功的重大演变。其中大多数工具是对其的抽象层或“前端”

“前端”到之前描述的低层包管理工具。与大多数其他基于 DEB 的发行版一样，Ubuntu 使用 `apt-get`、`Aptitude`、`dselect` 以及图形化前端 `Synaptic`。

由于跟踪和编目依赖关系的能力或许是任何包管理系统最重要的一方面，这些高级工具的主要功能一直是在现有包工具之上添加功能类别，并以一次处理多个包的方式操作包。这些工具中的每一个都包含额外的数据库，这些数据库不仅描述了已安装的包，还描述了可通过存储在本地、CD 或（在当今几乎所有情况下）网络上的包存档作为安装候选的包。

这些系统可以自动理清依赖关系和顺序，下载包（包括依赖项），先安装依赖项，然后使用上一节详述的低层工具安装和配置所讨论的包。

同样，这些高级工具也可用于卸载包。例如，如果用户想要卸载一个共享库，系统会提示一个屏幕，描述后果，列出因卸载后其依赖项将不再存在于系统中而必须卸载的包。涉及更改依赖关系（例如被替换的包）的升级也可以由此系统处理。

此类系统的真正潜力在包的依赖关系随时间变化或多个包可作为直接替代品时显现。需要发送邮件能力的包可以仅依赖于其他包“提供”的虚拟包。新版本的包可以与其他包冲突，并声明“替换”其他包，或提供原始包的功能。例如，如果多个包合并为一个包，使得另外三个包过时，高级包系统应能跟踪变化的依赖信息，并在升级时做出正确决策。沿着这些思路，大多数高级包管理工具使用包依赖项中声明的数据，让用户能够对系统上的每个包进行策略性的“智能升级”，升级到可用包的最新版本。

对一些用户来说更令人兴奋的是，可以跟踪 `GNU/Linux` 操作系统的开发中版本，并每天升级到所有软件的最新版本。包管理器能够找出安全升级路径并据此处理。在这些升级过程中，ABI 和 API 版本变化也可以自动处理，因为系统会拒绝全面升级某个库，直到系统上所有依赖于包含该共享库的包的包能够同时升级为止。系统无需长期保留或跟踪共享库的多个版本。

## Debian 包

正如本书前面提到的，Ubuntu 项目基于 Debian GNU/Linux 发行版。在众多其他技术遗产中，Ubuntu 继承了 Debian 包系统。事实上，许多早期参与的 Ubuntu 核心开发者会将 Debian 的打包系统视为 Debian 被证明是一个如此有吸引力的出发点、并且相对于其他 GNU/Linux 发行版具有主要吸引力的原因。因此，包管理的几乎所有方面——从格式到工具——在 Ubuntu 和 Debian 上都是相同的。在许多情况下，未经修改的 Debian 包可以直接安装在 Ubuntu 上。在几乎所有情况下，未经修改的 Debian 源代码包都可以在 Ubuntu 上构建。因此，我们的第一步是深入检查一个 Ubuntu DEB，以理解包的结构及其实现前面章节所描述功能的方式。

## 源代码包

`DEB` 源代码包通常以三文件或两文件格式清晰表达，但也可能包含由更多文件组成的源代码包。这意味着包本身包含多个文件，下载“一个源代码包”实际上可能涉及下载少量不同的文件。源代码包大致可分为原生 `DEB` 包和非原生 `DEB` 包。原生 `DEB` 是一种软件，其上游版本与 `DEB` 包之间没有区别。在大多数情况下，原生包是 Ubuntu、Debian 或其他基于 Debian 的发行版所特有的。换句话说，原生包无需任何更改即可创建包。`DEB` 源代码包始终由“原始”源代码组成。

archive in the form of a gzip-compressed GNU tar file and a DSC file that will list the contents of the package and can be considered the “core” of a source package. An example DSC for a program called most that I maintain looks like this:

```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA1

Format: 1.0
Source: most
Binary: most
Architecture: any
Version: 5.0.0a-1
Maintainer: Benjamin Mako Hill <mako@debian.org>
Standards-Version: 3.7.3
Build-Depends: debhelper (>= 4), libslang2-dev
Files:
  3f02131b67f61716f6fe1f65205da48b 155233 most_5.0.0a.orig.tar.gz
  07e3eb05ad5524fe6d885f5cdc2eb902 20160 most_5.0.0a-1.diff.gz

-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.6 (GNU/Linux)

iD8DBQFH4IOAiCl1LWBlWeYRAj0AKCrLCfuZA7b8JcvYTFYeuHrF7r34wCfVTBS
/jGUfIrELNq173sM9CorZA4=
=/Cia
-----END PGP SIGNATURE-----
```

该文件使用 `GnuPG` 或 `PGP` 密钥签名，以确保文件的完整性和作者的身份。如果你用 `GPG` 检查此签名，你会看到它是由我的 `GPG` 密钥签名的。`DSC` 文件还包含有关源格式版本的信息（在本例中为“旧”格式 1.0）、源包的名称、包的版本（分为上游源的版本和最终 − 之后的包版本）、维护者的姓名和电子邮件、软件将运行的架构、软件所创建的策略版本（标记为“standards”）、构建包必须存在的软件，以及由文件大小和 MD5 哈希标识的此源包包含的其他文件列表。

在原生 `DEB` 中，只会有一个压缩的 `tar`（`tar.gz`）文件。在此非原生包中，会有额外的文件代表对包的所有更改。这样可以清楚地看到 `DEB` 打包者所做的所有更改。这有时是出于许可原因而做的，但通常只是为了让用户能够清楚地看到打包者做了什么以及更改了什么。这也使包维护者如果出现错误时能够轻松地了解问题所在。对包所做的更改通常以 `gzip` 压缩的 `diff` 文件表示，该文件表达了包源与原始源之间的所有差异。在上一页的示例中，它列为 `most 5.0.0a-1.diff.gz`。在 `DEB` 源代码包格式的新版本中，还允许包含包含对原始源归档的添加或更改的额外 `tar` 文件，只要它们在 `DSC` 文件的文件列表中列出即可。

解压并应用所有必要的补丁后，每个 `DEB` 源包都会解压到一个名为 `packagename-version` 的单个目录中，其中包含一个强制性的 `debian` 子目录。在绝大多数包中，源的几乎所有更改都将在此目录中进行。该目录包含许多文件——我这里没有足够的空间全部介绍。其中最重要的是 `control` 文件和 `rules` 文件。`control` 文件包含 `DSC` 文件中关于源包的大部分信息（该文件使用 `control` 文件数据自动生成）以及描述每个二进制包的额外信息。`control` 文件表达了所有包间关系，包括 `Depends`、`Conflicts`、`Provides`、`Replaces`、`Recommends`、`Suggests` 和 `Enhances`。作为“硬性”要求，前四项最为重要。`Suggests` 和 `Enhances` 很少被任何程序使用。该文件还包含单行和多行描述。以下是示例 `control` 文件（`most` 的 `control`）：

```
Source: most
Section: text
Priority: optional
Maintainer: Benjamin Mako Hill <mako@debian.org>
Standards-Version: 3.7.3
Build-Depends: debhelper (>=4), libslang2-dev

Package: most
Architecture: any
Depends: ${shlibs:Depends}
Description: Pager program similar to more and less
```

长格式描述已从输出中删除，但实际上它跟在最终的描述行之后，并包含缩进一个空格的文本，其中段落由单个“.”分隔。如前所述
