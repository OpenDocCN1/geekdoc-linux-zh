
```
lang(fr) %[_datadir/]/locale/fr/LC_MESSAGES/tcsh*
lang(it) %[_datadir/]/locale/it/LC_MESSAGES/tcsh*
lang(ja) %[_datadir/]/locale/ja/LC_MESSAGES/tcsh*
lang(pl) %[_datadir/]/locale/pl/LC_MESSAGES/tcsh*
lang(ru) %[_datadir/]/locale/ru/LC_MESSAGES/tcsh*
lang(uk) %[_datadir/]/locale/uk/LC_MESSAGES/tcsh*
```

此示例标记某些文件仅用于特定语言，例如 `ja` 代表日语文本，`fr` 代表法语文本。

## 验证 `%files` 部分

你可以使用 `%verify` 指令来控制 RPM 在验证软件包时使用的测试。

![](img/9d29d6681c5f42792ea5da4b12142ca2_224_0.png)

`%verify` 指令指定了要包含或不包含的测试。表 10-4 列出了这些测试。

| 表 10–4 软件包验证测试 | | |

|---|---|---|

| Group | 验证文件的组 |

| Maj | 验证文件的主设备号 |

| Md5 | 验证文件的 MD5 校验和 |

| Min | 验证文件的次设备号 |

| Mode | 验证文件的模式（权限） |

| Mtime | 验证文件的最后修改时间 |

| Owner | 验证文件的所有者 |

| Size | 验证文件的大小 |

| Symlink | 验证符号链接 |

使用 `%verify` 指令，你可以命名这些测试，如下：

```
%verify(owner group size) /etc/yp.conf
```

通过 `%verify` 指令，你可以命名测试，如上所示。此示例限制了所有者、组和大小测试（默认是所有测试）。你也可以指定特定的测试：

```
%verify(not owner) /etc/yp.conf
```

## 填充 `%files` 部分

使用 `%f` 指令可以控制 RPM 在验证软件包时使用的测试（注：此处原文逻辑可能略误，通常为 `%verify` 选项）。

（注：此处根据上下文语境翻译，原文后续内容存在部分乱码或重复，已按逻辑梳顺）

...（此处省略原文中重复的 文本，已保留核心逻辑翻译）

你也可以用空格代替逗号。例如：

```
%attr(0700 root root) %dir /var/tux
```

除了使用 `%attr` 设置文件属性外，你还应该使用 `%deattr` 指令来设置包中所有文件的默认属性。例如：

```
%files
%deattr(-,root.root)
/usr/X11R/bin/xtoolwait
/usr/X11R/man/1/xtoolwait.*
```

几乎每个文件都使用 `%deattr` 指令，因为该指令消除了你逐个设置文件属性的大量工作。此外，在创建软件包时，使用 `%deattr` 指令被视为最佳实践。你还可以为特定语言标记文件。例如，来自 `tcsh` shell 包：

```
%files
%deattr(-
```

...（后文由于原文存在重复乱码，已根据高级工程师规范进行清洗处理）

## 第 10 章：处理文件

| 宏 | 用法 |

|--- | --- |

| `%(P:patch_exp)` | 将 `patch_exp` 展开为补丁文件名 |

| `%(S:source_exp)` | 将 `source_exp` 展开为源文件名 |

| `%trace` | 切换调试信息的打印 |

| `%(uncompress:filename)` | 测试文件名是否被压缩。如果是，则解压并包含在给定的上下。如果没有压缩，则调用 `cat` 将文件包含在给定的上下。 |

| `%undefined macro` | 取消给定的宏 |

| `%(warn:message)` | 将消息打印到 `stderr` |

![](img/9d29d6681c5f42792ea5da4b12142ca2_228_0.png)

## 定义新宏

除了内置宏，你还可以定义自己的宏以便于管理包。使用以下语法定义新的 spec 文件宏：

```
%define macro_name value
```

例如：

```
%define major 2
%define minor 2
%define patchlevel 7
```

你可以使用 `%macro_name` 或 `%(macro_name)` 语法使用宏。例如：

```
Version: %(major).%(minor).%(patchlevel)
```

你还可以使用圆括号代替大括号的 `%(command)` 语法来展开运行 shell 命令的结果。例如：

```
%define today %(date)
```

## 为宏指定参数

大多数宏执行简单的文本替换。你还可以向宏传递参数，并在宏内部访问这些参数，这类似于 shell 脚本获取命令行参数的方式。

![](img/9d29d6681c5f42792ea5da4b12142ca2_229_0.png)

通过参数，你可以将宏的普通定义扩展为如下形式：

```
%define macro_name(options) value
```

括号内的任何文本都会传递给 `getopt(3)`，并作为宏的参数。这在宏展开时执行。你还可以使用 `%macro_name` 语法（不带大括号）向宏传递选项。例如：

```
%foo 1 2 3
```

此示例将参数 1、2 和 3 传递给宏 `foo`。在宏内部，你可以使用类似脚本的语法通过宏来访问参数。表 10-6 列出了这些宏。

| 表 10-6 宏展开内部的宏 |

| 宏 | 持有内容 |

| --- | --- |

| `%0` | 宏的名字 |

| `%*` | 宏的所有参数，除任何已处理的选项外 |

| `%#` | 参数的数量 |

| `%1` | 第一个参数 |

| `%2` | 第二个参数 |

| `%3` | 第三个参数，依此类推还有 `%4`、`%5` 及之后 |

| `%(-p)` | 如果向宏传递了 `-p` 参数，则持有 `-p`；否则留空 |

## 第 10 章：处理 Spec 文件 205

| 宏 | 持有内容 |

|---|---|

| `%[-p*]` | 如果向宏传递了 `-p` 参数，则持有通过 `-p` 参数传递的值；否则留为空 |

| `%[-p:text]` | 如果向宏传递了 `-p` 参数，则持有文本；否则留为空 |

注意，表 10-6 中列出的所有参数在经过 `getopt(3)` 处理后持有剩余的参数。你可以在自定义宏的定义中使用这些宏。你还可以嵌套宏，例如：

```
define mypatch %{I-p:-p%(-p)}
```

如果没有传递 `-p` 参数，此宏将展开为 `patch` 命令。如果你传递了 `-p` 参数（例如 `-p 1`），则该宏将展开为带有 `-p` 参数值的 `-p`：

```
patch -pl
```

![](img/9d29d6681c5f42792ea5da4b12142ca2_230_0.png)

这种语法在 `patch` 命令中被大量使用。

## 创建 XML Spec 文件

RPM spec 文件是包含结构化信息的文本文件。使用 XML 编写 RPM spec 文件是一个自然的演进。`rpmxmlbuild` 工具将从 XML 格式的 spec 文件构建 RPM 包。例如，列表 10-1 包含一个 XML 格式的 spec 文件。

列表 10-1：一个 XML spec 文件

```xml
<?xml version="1.0"?>
<spec distribution="RPM Test" vendor="rpm.org"
name="bash" version="2.05a" release="02test"
copyright="GPL"
url="http://www.gnu.org/software/bash.html">
```

列表 10-1：一个 XML spec 文件（续）

```xml
<source name="${name}-${version}.tar.bz2">
  size="1343025" md5="c29b50db80803e39558a0f6354f4cad"
  path="${name}-${version}">
</source>
```

```xml
<buildrequires>
  <require name="bash" />
  <require name="gcc" />
</buildrequires>
```

```xml
<package>
  <require name="bash" />
  <require name="gcc" />
  <require name="make" />
</package>
```
