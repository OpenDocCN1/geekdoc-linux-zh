

- 控制在包验证期间检查文件的哪些方面
- 减少创建 %files 列表时的一些繁琐工作

在 %files 列表中，一个或多个指令可以放在同一行中，用一个或多个文件名之前通过空格分隔。因此，如果 %foo 和 %bar 是两个 %files 列表指令，它们可以按以下方式应用于文件 baz：

```
%foo %bar baz
```

现在，是时候来看看驻留在 %files 列表中的指令了。

## 13.6.1. 文件相关指令

RPM 会根据文件类型以不同方式处理文件。然而，RPM 没有自动确定文件类型的方法。因此，包构建者需要负责在 %files 列表中适当地标记文件。这是通过使用以下指令之一来完成的。

请记住，并非每个文件都需要标记。在阅读以下章节时，你会看到指令仅用于特殊情况。在大多数包中，%files 列表中的大多数文件不需要标记。

### 13.6.1.1. %doc 指令

%doc 指令将紧随其后的文件名标记为文档。RPM 在其数据库中跟踪文档文件，以便用户轻松查找有关已安装包的信息。此外，RPM 可以在安装过程中创建包特定的文档目录并将文档复制到其中。是否执行此额外步骤取决于文件是如何指定的。示例如下：

```
%doc  README
%doc /usr/local/foonly/README
```

文件 README 在构建期间存在于软件的顶层目录中，并包含在包文件中。安装包时，RPM 在文档目录中创建一个与包同名的目录（即 <software>-<version>-<release>），并将 README 文件复制到该目录中。新创建的目录和 README 文件在 RPM 数据库中被标记为文档。默认文档目录为 /usr/doc，可通过设置 defaultdocdir rpmrc 文件条目进行更改。有关 rpmrc 文件的更多信息，请参见附录 B。

文件 /usr/local/foonly/README 在构建期间已安装到该目录中，并包含在包文件中。安装包时，README 文件被复制到 /usr/local/foonly 并在 RPM 数据库中标记为文档。

%config 指令用于将指定文件标记为配置文件。当包被卸载以及安装和升级时，RPM 会对配置文件执行额外的处理。这是由于配置文件的性质：它们经常由系统管理员修改，这些修改不应丢失。

%config 指令有一个限制：%config 之后只能跟随一个文件名。这意味着以下示例是指定配置文件的唯一允许方式：

```
%config /usr/local/foonly/README
```
请注意，需要提供文件在安装时的完整路径。

%attr 指令允许对三个关键文件属性进行更精细的控制：

- 文件的权限，或模式
- 文件的用户 ID
- 文件的组 ID

%attr 指令的格式如下：

```
%attr(<mode>, <user>, <group>) file
```

模式以传统的数字格式指定，而用户和组以字符串形式指定，例如 root。这是一个 %attr 指令的示例：

```
%attr(755, root, root) foo.bar
```

这将设置 foo.bar 的权限为 755。文件由用户 root、组 root 拥有。如果某个属性不需要指定（通常是因为文件在安装时已正确设置了该属性），则可以用连字符替换该属性：

```
%attr(755, -, root) foo.bar
```

使用 %attr 指令的主要原因是允许没有 root 权限的用户构建包。执行此操作的技术（以及对 %attr 指令的更详细讨论）可在第 16 章中找到。

RPM 验证其已安装软件完整性的能力令人印象深刻。但有时它有点过于令人印象深刻。毕竟，RPM 可以验证每个文件的多达九个不同方面。%verify 指令可以控制在 RPM 验证时检查这些文件属性中的哪些。以下是这些属性以及 %verify 指令使用的名称：

- 所有者 (`owner`)
- 组 (`group`)
- 模式 (`mode`)
- MD5 校验和 (`md5`)
- 大小 (`size`)
- 主设备号 (`maj`)
- 次设备号 (`min`)
- 符号链接字符串 (`symlink`)
- 修改时间 (`mtime`)

%verify 是如何使用的？例如，假设一个包安装设备文件。由于设备的属主会改变，让 RPM 验证设备文件的属主/组并给出误报是没有意义的。相反，可以使用以下 %verify 指令：

```
%verify(mode md5 size maj min symlink mtime) /dev/tty$0
```

我们省略了 owner 和 group，因为我们宁愿 RPM 不验证那些属性。（对于某些类型的文件，如果验证没有意义，RPM 会自动将文件属性排除在验证之外。在我们的示例中，获取设备文件的 MD5 校验和就是这种情况。）然而，如果你想做的仅仅是防止 RPM 验证一两个属性，你可以使用 %verify 的替代语法：

```
%verify(not owner group) /dev/tty$0
```

这种 %verify 的使用产生的结果与上一个示例中的结果相同。

## 13.6.2. 目录相关指令

虽然本节中的两个指令执行不同的功能，但每个都与目录有关。让我们看看它们做什么。

### 13.6.2.1. %docdir 指令

%docdir 指令用于将一个目录添加到包含文档的目录列表中。RPM 默认将 /usr/doc、/usr/info 和 /usr/man 包含在 %docdir 列表中。

例如，如果以下行是 %files 列表的一部分：

```
%docdir /usr/blather
```

来自 /usr/blather 的任何 %files 列表中的文件，RPM 都会像往常一样将其包含在包中，但也会被自动标记为文档。当包创建自己的文档目录并包含大量文件时，这个指令非常有用。让我们通过在 spec 文件中添加以下行来试一试：

```
%docdir /usr/blather
```

我们的 %files 列表中没有引用包安装在 /usr/blather 目录中的几个文件。构建包后，查看包的文件列表显示如下：

```
# rpm -qlp ../RPMS/i386/blather-1.0-1.i386.rpm
...
```

等等：那里什么都没有，甚至没有 /usr/blather！发生了什么？

问题是 %docdir 只是指示 RPM 将指定目录标记为包含文档。它并没有指示 RPM 将目录中的任何文件打包。要做到这一点，我们需要让 RPM 知道目录中有必须打包的文件。

这样做的一种方法是简单地将文件添加到 %files 列表：

```
%docdir /usr/blather
/usr/blather/INSTALL
```

查看包，我们看到 INSTALL 已被打包：

```
# rpm -qlp ../RPMS/i386/blather-1.0-1.i386.rpm
...
/usr/blather/INSTALL
```

指示 RPM 仅显示文档文件，我们看到 INSTALL 确实已被标记为文档，尽管没有使用 %doc 指令：

```
# rpm -qdqp ../RPMS/i386/blather-1.0-1.i386.rpm
...
/usr/blather/INSTALL
```

当然，如果你费心将每个文件添加到 %files 列表，为每个文件添加 %doc 也不会多花多少力气。因此，要从 %docdir 中获得最大利益的方法是向 %files 列表添加另一行：

```
%docdir /usr/blather
/usr/blather
```

由于第一行指示 RPM 将 /usr/blather 中的任何文件标记为文档，而第二行告诉 RPM 自动打包在 /usr/blather 中发现的任何文件，因此其中的每一个文件都会被打包并标记为文档：

```
# rpm -qdq ../RPMS/i386/blather-1.0-1.i386.rpm
/usr/blather
/usr/blather/COPYING
```

