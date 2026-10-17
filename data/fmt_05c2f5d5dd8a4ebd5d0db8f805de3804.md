
| `shadmrg.aix`<br>`shadmrg.sv` | 这些 Bourne-shell 脚本用于将 `passwd` 和 `shadow` 文件合并为一个文件。`shadmrg.sv` 脚本适用于 System V 风格文件（如 Red Hat），而 `shadmrg.aix` 适用于 IBM AIX 系统。 |

![](img/7933c44717ab0711177ea7153f959fc5_358_0.png)

## 构建 CRACK

构建 `Crack` 有很多不同的方法。例如，如果您使用 `MD5` 或 `bigcrypt` 作为您的密码哈希方案，您需要在编译程序之前对源代码树进行修改。`Crack` 没有配置工具，因此如果除标准 UNIX 密码之外的其他标准 `/etc/passwd` 和 `/etc/shadow` 配置中有内容，您将不得不阅读文档（想象一下）。我们将查看构建用于标准 UNIX 哈希密码、`MD5` 哈希密码和 `bigcrypt` 哈希密码的 `Crack`。

如果您要针对这些不同的密码方案运行 `Crack`，您将希望为每一个创建构建目录。例如，使用 `/usr/src/c50a` 作为 UNIX，`/usr/src/c50aMD5` 作为 `MD5`，等等。如果您还将在不同的操作系统和/或架构上运行 `Crack`，建议在每个系统上手动构建 `Crack`（至少是第一次），以便您可以排查可能出现的问题。一旦编译完成，您可以将完整的源代码树加可执行文件放在单个服务器（如安全服务器）的适当子目录中，然后使整个发行版通过 `NFS` 可访问。当您在网络模式下运行 `Crack` 时（参见第 328 页的 *Running Crack over the Network*），这特别方便。

## 为 Linux 修改 Crack

在我们查看 `MD5` 等特殊案例之前，必须对 `crack` 脚本本身进行修改。当您编辑 `crack` 时，您将找到示例 12-1 中显示的代码行（换行是由于格式限制）。只需将示例 12-1 中的行更改为示例 12-2 中显示的内容（换行是由于格式限制）。示例 12-2 中的修改反映了选择 `gcc` 而不是 `cc` 作为编译器，选择 `gcc` 的 `cFLAGS` 而不是 `cc` 的 `cFlags`，并取消注释带有 `-lcrypt` 的行，以便将该库纳入编译过程。

现在您已准备好为 Linux 密码猜测进行编译。如果您要为 `MD5` 或 `bigcrypt` 构建 `Crack`，请在第一次运行 `Crack` 之前按照第 319 页的 *Modifying Crack for MD5* 和第 319 页的 *Modifying Crack for Bigcrypt* 中的步骤进行操作；否则请转到第 320 页的 *Compiling Crack Itself* 部分。

### 示例 12-1 Crack 中的默认编译器和库规格

```text
# vanilla unix cc
CC=cc
CFLAGS="-g -O $C5FLAGS"
#LIBS=-lcrypt # uncomment only if necessary to use stdlib crypt(), e.g.: NetBSD MD5
# gcc 2.7.2
CC=gcc
#CFLAGS="-g -O2 -Wall $C5FLAGS"
#LIBS=-lcrypt # uncomment only if necessary to use stdlib crypt(), eg: NetBSD MD5
```

### 示例 12-2 Linux 的修改版编译器和库规格

```text
# vanilla unix cc
#CC=cc
#CFLAGS="-g -O $C5FLAGS"
#LIBS=-lcrypt # uncomment only if necessary to use stdlib crypt(), eg: NetBSD MD5
# gcc 2.7.2
CC=gcc
CFLAGS="-g -O2 -Wall $C5FLAGS"
LIBS=-lcrypt # uncomment only if necessary to use stdlib crypt(), eg: NetBSD MD5
```

## 为 MD5 修改 Crack

为了准备 `Crack` 进行 `MD5` 猜测，您需要对源代码树进行一些简单的更改。步骤概述在示例 12-3 中。

### 示例 12-3 准备 MD5 破解所需的步骤

```text
# cd /usr/src/c50aMD5/src
# mv libdes libdes.orig
# cd util
# cp elcid.c elcid.c.orig
# cp elcid.c.bsd elcid.c
```

就是这样！您现在已准备好编译。

### 注意

变量 `PLAINTEXTSIZE` 在 `elcid.c` 文件中定义。对于 `MD5`（在文件 `elcid.c.bsd` 中），它被设置为 16。这意味着将猜测的最大明文密码长度为 16 个字符。您可以将其增加到 32，但这会付出巨大的性能代价。什么是巨大的？仅考虑字母数字字符（a-z, A-Z, 0-9）——这代表 26 个小写字母加上 26 个大写字母加上 10 个数字字符，总共 62 个字符。因此，16 个字符的字母数字密码的总可能性为 `$62^{16}$` 或 `$4.77 \times 10^{29}$`，而 32 个字符的密码的总可能性为 `$62^{32}$` 或 `$2.27 \times 10^{57}$`，这是一个大得多的数字。

若要进一步增加变量 `PLAINTEXTSIZE`，需要对源代码进行额外的修改。

## 为 Bigcrypt 修改 Crack

如果您有使用 `bigcrypt` 的系统，您需要做更多的工作。首先，您必须在系统上加载 `libc-crypt`。如果您运行的是 Red Hat 5.2 或更高版本，它已经在那里了。否则，您需要从以下站点之一获取副本：

- `ftp://prep.ai.mit.edu/gnu/`
- `http://www.redhat.com/`

并安装它。我们假设 `bigcrypt` 版本的源目录为 `/usr/src/c50aARC/src`。一旦你安装了 `libc-crypt`，就需要编辑 `/usr/src/c50aARC/src/util/ecild.c`，并修改两行代码（它们彼此接近，但并不相邻）：

```
#define PLAINTEXTSIZE    8
...
#undef CRYPT16
```

修改为：

```
#define PLAINTEXTSIZE    16
...
#define CRYPT16
```

现在，你准备好进行编译了。

## 为 crypt (3) 准备 Crack

对于标准的 `crypt(3)` 哈希密码，你实际上不需要做任何操作；然而，`Crack` 的发行版包含了 `1ibdes`，这是由 Eric Young 编写的一个高度优化的哈希引擎。你的 Linux 系统很可能附带了来自 GNU 社区的 `libcrypt`（Red Hat 5.2/6.0 的情况就是这样）。如果你希望使用 `1ibdes`，只需切换到 `src/libdes` 子目录并执行 `make`。如果你打算使用 `Crack7`（见第 330 页的 `Crack7`），这一步是必需的。

## 编译和链接 Crack

一旦你完成了“第 318 页 Linux 下的 Crack 修改”部分中给出的必要预备步骤，以及 `MD5` 和/或 `Bigcrypt` 概述的步骤，你就可以编译和链接组成 `Crack` 的各个程序了。

`Crack` 可以带有多个不同的选项来调用。事实证明，如果你调用 `Crack` 开始处理密码文件，它会编译和链接所有尚未构建的必要程序。一旦你确定它可以在特定平台上正确构建，这可能很有用；然而，在第一次运行时，你可能希望采取逐步的方法。编译和链接破解引擎以及字典的离散步骤在接下来两个部分中概述。

## 编译 Crack 本身

你基本上已经完成了所有工作。要编译和链接组成 `Crack` 的各种程序，只需执行 `crack -makeonly`。示例 12-4 提供了一个说明。就这么简单！接下来，你需要构建字典。

### 示例 12-4 执行 Crack -makeonly
