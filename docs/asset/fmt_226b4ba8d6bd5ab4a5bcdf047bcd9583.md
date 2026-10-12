
在这种，名为 `baz` 的文件是一个版本 3 格式 `RPM` 文件，包含了 `vlock` 包的 1.0 版本 2，该包为 Intel x86 架构构建。

# 附录 B

## rpmrc 文件

`rpmrc` 文件用于控制 `RPM` 的操作。文件的条目对 `RPM` 的几乎每个方面都有影响。在这里，我们详细描述 `rpmrc` 文件，以及显示 `RPM` 如何解释这些文件的命令。

### B.1 使用 --showrc 选项

稍后我们将看到，`RPM` 可以读取多个 `rpmrc` 文件，每个文件可以包含近三十种条目。这使得很难确定 `RPM` 实际上在使用什么。幸运的是，有一个选项可以理清这些情况。`--showrc` 显示 `RPM` 将使用的值。输出分为两个部分：

1. 架构和操作系统值。
2. `rpmrc` 值。

架构和操作系统值定义了 `RPM` 运行的架构和操作系统。这些值也定义了构建和安装包的环境。它们还定义了哪些架构和操作系统之间是兼容的。以下是 `--showrc` 输出的一个示例：

```
# rpm --showrc
ARCHITECTURE AND OS:
  build arch      : i386
  build os        : Linux
```

### B.2 rpmrc 文件的不同位置

3. 在用户登录目录下的名为 `.rpmrc` 的文件中。
4. 如果命令行上存在 `--rcfile` 选项，则在由该选项指定的文件中。

前三个文件按照列出的顺序读取，因此如果每个文件中都存在某个 `rpmrc` 条目，则最后读取的条目值将由 `RPM` 使用。这意味着，例如，用户登录目录下 `.rpmrc` 中的条目将始终覆盖 `/etc/rpmrc` 中的相同条目。同样地，`/etc/rpmrc` 中的条目将始终覆盖 `/usr/lib/rpmrc` 中的相同条目。

如果使用了 `--rcfile` 选项，则只读取 `/usr/lib/rpmrc` 和 `--rcfile` 选项之后的文件，按此顺序读取。`/usr/lib/rpmrc` 文件总是会被首先读取。这一点无法更改。

让我们来看这些每一个文件，从 `/usr/lib/rpmrc` 开始。

#### B.2.1 /usr/lib/rpmrc

`/usr/lib/rpmrc` 文件总是会被读取。它包含了 `RPM` 用于设置某些默认值的信息。**此文件绝不应修改！** 这样做可能会导致 `RPM` 运行异常。

在这一严厉的警告之后，我们应该注意，查看它是完全没问题的。实际上它如下：

```
############################################################
# 默认值，通常在 /etc/rpmrc 中覆盖

dbpath: /var/lib/rpm
topdir: /var/src/redhat
tmppath: /var/tmp
cpiobin: cpio
defaultcodir: /var/doc
```

```
############################################################
# 请将新条目发送至 rpm-list@redhat.com

############################################################
# 各种平台的 RPM_OPT_FLAGS 值
```

```
optflags: i386 -O2 -m486 -fnc-strength-reduce
optflags: alpha -O2
optflags: sparc -O2
optflags: m68k -O2 -fomit-frame-pointer
```

```
############################################################
```

##### 规范架构名称与数字

```
arch_canon: i1986: i1986 1

arch_canon: i1886: i1886 1

arch_canon: i1786: i1786 1

arch_canon: i1686: i1686 1

arch_canon: i1586: i1586 1

arch_canon: i1486: i1486 1

arch_canon: i1386: i1386 1

arch_canon: alpha: alpha 2

arch_canon: sparc: sparc 3

sun4: sparc 3

sun4m: sparc 3

arch_canon: sun4c: sparc 3

# 这是一个真正的 MIPS 占位符

arch_canon: mips: mips 4

arch_canon: ppc: ppc 5

# 这是一个真正的 68000 占位符

arch_canon: m68k: m68k 6

# 这里错了。我们真的在这里需要通配符 :-(

arch_canon: IP: sgi 7

arch_canon: IP22: sgi 7

arch_canon: 9000/712: hppa1.1 9

arch_canon: sun4u: usparc 10
```

```
############################################################

# 规范操作系统名称与数字

os_canon: Linux: Linux 1

os_canon: IRIX: IRIX 2

# 这里错了

os_canon: Sun05: solaris 3

os_canon: Sun0S4: Sun0S 4

os_canon: AmigaOS: AmigaOS 5

os_canon: AIX: AIX 5

os_canon: HP-UX: hpux10 6

os_canon: OSF1: osf1 7

os_canon: FreeBSD: FreeBSD 8
```

```
############################################################

# 对于给 uname().machine，默认构建架构

buildarchtranslate osfmach3_i986: i1386

buildarchtranslate osfmach3_i886: i1886

buildarchtranslate osfmach3_i786: i1786

buildarchtranslate osfmach3_i686: i1686

buildarchtranslate osfmach3_i586: i1586

buildarchtranslate osfmach3_i486: i1486

buildarchtranslate osfmach3_i386: i1386

buildarchtranslate osfmach3_ppc: ppc
```

```
############################################################

# 架构兼容性

arch_compat: alpha: axp

arch_compat: i986: i1886

arch_compat: i886: i1786

arch_compat: i786: i1686

arch_compat: i686: i1586

arch_compat: i586: i1486

arch_compat: i486: i1386

arch_compat: osfmach3_i986: i1986

arch_compat: osfmach3_i886: i1886

arch_compat: osfmach3_i786: i1786

arch_compat: osfmach3_i686: i1686

arch_compat: osfmach3_i586: i1586

arch_compat: osfmach3_i486: i1486

arch_compat: osfmach3_i386: i1386

arch_compat: osfmach3_ppc: ppc
```

内容很多，对吧？除了前五行指示重要目录的位置外，该文件的其余部分包含了与 `RPM` 架构和操作系统相关的条目。正如你所想象的，这里的任何修改可能都没有意义，请将任何修改留给 `RPM` 开发者。

#### B.2.2 /etc/rpmrc

接下来是 `/etc/rpmrc`。与 `/usr/lib/rpmrc` 不同，`/etc/rpmrc` 文件允许修改和添加。事实上，`/etc/rpmrc` 默认并不创建，因此其内容完全由决定。它是存放系统级或全局性 `rpm` 条目的完美位置。

`vendor` 条目是包含在 `/etc/rpmrc` 中的良好示例。在大多数情况下，特定的系统专门为一个供应商构建包。在这种情况下，`/etc/rpmrc` 中的 `vendor` 条目是最好的。

层级结构中是用户登录目录下的名为 `.rpmrc` 的文件。

#### B.2.3 用户登录目录下的 .rpmrc
