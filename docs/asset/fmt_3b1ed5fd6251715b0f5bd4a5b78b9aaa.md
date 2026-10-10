
## 注意
`/usr/ports` 的内容在本质上独立于 FreeBSD 操作系统的分支开发结构。新发布的系统副本将包含在系统发布时创建的软件移植快照，但一旦其中的软件移植因新版本移植软件的发布而经过修订，它很快就会过时。如果你将软件移植树同步到中央仓库（我们将在后面讨论），它总是同步到你同步时的最新状态。与软件包不同，软件移植树并没有与每个版本绑定的固定状态。因此，这些示例目录列表可能与系统中的实际情况略有不同。

前几个目录（那些以大写字母开头的目录，利用了 Unix 约定，即大写字母和小写字母按 ASCII 字符集分别按字母顺序排列）是软件移植系统的结构元素，是让系统运行的辅助部分。其余的目录是软件移植类别。进入其中一个目录，你会看到多达数百个不同的软件移植目录，如清单 14.5 所示。

### 清单 14.5 类别（目录）中的软件移植

```
# ls -sF /usr/ports/audio/

total 230

1 Maaite/                  1 mpg123/

5 Makefile                 1 mpg123_el/

11 README.html             1 mpg321/

1 afsf/                    1 mpf20/

1 amp/                     1 mq3/

1 ascd/                    1 musicbox/

1 amix/                    1 musicbrainz/

1 aureal-kmod/             1 mutemix/

1 autozen/                 1 mvx/

1 bladeenc/                1 napster/
```

以这种方式浏览软件移植效率较低，尤其是在较大的类别中。这正是 `README.html` 文件的作用所在。还记得每个软件包的“简短描述”吗？该描述也存储在此文件中，并且在两级目录中都有 `README.html` 文件，几乎每个软件移植目录内部也有。你可以使用本地机器上的任何 Web 浏览器以超文本形式浏览该结构：如果你将机器用作 X-Windows 工作站，可以使用 `Netscape`；如果你是远程登录（如图 14.3 所示），可以使用 `lynx`。

![](img/48eec858cce7dfb89da36a4d40b7daf3_359_0.png)

### 图 14.3 使用 lynx 浏览类别的 README.html 文件。

# FreeBSD 软件移植结构

每个软件移植目录内部都有几个文件，总共不超过几 kilobytes，这些文件完全定义了在 FreeBSD 上干净地编译和安装干净下载的源代码捆绑包所需的所有调整和改进。这些文件在表 14.2 中详细说明。

**表 14.2 软件移植目录中的文件**

| 文件 | 目的 |
| :--- | :--- |
| `Makefile` | 包含构建过程中使用的某些变量以及维护者的联系信息。 |
| `README.html` | 以 HTML 格式包含软件移植的“简短描述”（或注释）。 |
| `distinfo` | 用于验证下载的 tarball 真实性的 MDS 校验和。 |
| `files/` | 在源代码解压缩后应用于源代码的补丁，以及 FreeBSD 特有的支持文件；这些因软件移植而异。 |
| `runme.sh` | |
| `patch-aa` | |
| `patch-ab` | |
| `pkg-comment` | 软件移植的“简短描述”。 |
| `pkg-descr` | 软件移植的“详细描述”，通常包括开发人员分发站的 URL。 |
| `pkg-plist` | “打包清单”，列出所有要安装的文件以及告诉软件移植系统在卸载软件移植时（例如，在移除目录时）要做什么的关键词。 |

`Makefile` 是包含构建、配置、安装和维护软件移植的关键元素的文件。清单 14.6 显示了 `Makefile` 中通常包含的内容。

### 清单 14.6 典型的软件移植 Makefile

```
# New ports collection Makefile for: amp

# Date created: Jun 23 1997

# Whom: Vanilla I. Shu <vanilla@Minje.com.TW>

#

# $FreeBSD: ports/audio/amp/Makefile,v 1.10 2000/04/08 21:23:11 mharo Exp $

#

PORTNAME= amp

PORTVERSION= 0.7.6

CATEGORIES= audio

#MASTER_SITES= ftp://ftp.rasp.fer.hr/pub/mpeg/

# the author's site seems dead.

MASTER_SITES= ftp://ftp.clara.net/pub/unix/Audio/

MAINTAINER=    vanilla@FreeBSD.org

GNU_CONFIGURE= yes

USE_GMAKE=    yes

MAN1=         amp.1

do-install:

	@ ${INSTALL_PROGRAM} ${WRKSRC}/amp ${PREFIX}/bin

	@ ${INSTALL_MAN} ${WRKSRC}/amp.1 ${PREFIX}/man/man1

.include <bsd.port.mk>
```
