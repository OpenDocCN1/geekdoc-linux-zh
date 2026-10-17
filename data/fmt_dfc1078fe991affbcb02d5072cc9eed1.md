
自从 RPM 的第一个版本问世以来，RPM 易用性的一个副作用就是它使人们更容易搞坏东西。因为 RPM 使得卸载包变得如此简单，人们常常欢快地卸载包直到某个东西坏了为止。

通常这种情况只会咬人一次，但如果能避免的话，即使是发生一次也太麻烦了。鉴于此，RPM 开发者赋予了 RPM 以下能力：

- 构建包含其所需能力信息的包。
- 构建包含其提供能力信息的包。
- 将这些提供和所需信息存储在 RPM 数据库中。

此外，他们确保 RPM 能够显示依赖信息，并在用户试图执行可能破坏包依赖要求的行为时警告用户。

有了这些功能，有人无意中卸载包并破坏系统的难度就更大了。

## 14.1. 依赖概览

我们已经暗示了 RPM 依赖处理的底层概念。它基于两个关键因素：

- 包宣传它提供哪些能力。
- 包宣传它需要哪些能力。

通过简单检查这两类信息，你可以避免许多问题。例如，如果一个包需要某个能力，而**没有**任何已安装的包提供该能力，那么这个包无法安装，也不期望能正常工作。

另一方面，如果一个包要被卸载，但它的功能被其他已安装的包所依赖，那么就不能在不导致其他包失败的情况下卸载它。

你可能猜得到，事情并没有那么简单。但是添加依赖信息可以很容易。事实上，在大多数情况下，它是自动的！

## 14.2. 自动依赖

当 RPM 构建一个包时，如果包 `%files` 列表中的任何文件是一个共享库，该库的 soname 会被自动添加到该包提供的能力列表中。soname 是用于确定不同版本库之间兼容性的名称。

请注意，soname 不是文件名。事实上，RPM 依赖处理的任何方面都不是基于文件名的。许多对 RPM 不熟悉的人认为失败的依赖代表缺失的文件。情况并非如此。

请记住，RPM 的依赖处理基于了解包提供了哪些能力以及包需要哪些能力。我们已经看到 RPM 如何自动确定包提供了哪些共享库资源。但它是否自动确定包需要哪些共享库？

是的！RPM 通过在每个包的 `%files` 列表中的每个可执行程序上运行 `ldd` 来实现这一点。由于 `ldd` 提供了每个程序所需的共享库列表，等式的两半都完整了——也就是说，提供共享库的包和需要那些共享库的包都被 RPM 跟踪了。RPM 可以在包安装、升级或卸载时考虑这些信息。

### 14.2.1. 自动依赖脚本

RPM 使用两个脚本来处理自动依赖。它们位于 `/usr/bin`，分别称为 `find-requires` 和 `find-provides`。我们稍后会查看它们，但首先让我们看看为什么会有脚本来做这类事情。将其内置于 RPM 本身岂不是更好？

实际上，为这类事情创建脚本是一个更好的主意。原因是什么？RPM 已经被移植到各种不同操作系统。确定可执行程序需要哪些共享库以及共享库的 sonname 很简单，但具体步骤因操作系统而异。将 RPM 的这一部分放入脚本中使移植 RPM 变得更加容易。

让我们来看看在 Linux 操作系统下 RPM 使用的脚本。

#### 14.2.1.1. `find-requires`：自动确定共享库需求

Linux 的 `find-requires` 脚本非常简单：

```
#!/bin/sh

# note this works for both a.out and ELF executables
ulimit -c 0
filelist='xargs -r file | fgrep executable | cut -d: -f1 '
for f in $filelist; do
    ldd $f | awk '/=>/ { print $1 }' | done; sort -u | xargs -r -n 1 basename | sort -u
```

这个脚本首先创建一个可执行文件列表。然后，对于列表中的每个文件，`ldd` 确定该文件的共享库需求，生成一个 soname 列表。最后，soname 列表通过去除重复项和任何路径进行清理。

#### 14.2.1.2. `find-provides`：自动确定共享库 Sonames

Linux 的 `find-provides` 脚本稍微复杂一些，但仍然相当直接：

```
#!/bin/bash

# This script reads filenames from STDIN and outputs any relevant
# provides information that needs to be included in the package.

filelist=$(grep "\.so" | grep -v "^/lib/ld.so" | xargs file -L 2>/dev/null | grep 'ELF.*shared object' | cut -d: -f1)

for f in $filelist; do
    soname=$(objdump -p $f | awk '/SONAME/ {print $2}')
    if [ "$soname" != "" ]; then
        if [ ! -L $f ]; then
            echo $soname
        fi
    else
        echo ${f##*/}
    fi
done | sort -u
```

首先，创建一个共享库列表。然后，对于列表中的每个文件，提取并清理 soname，并去除重复项。

### 14.2.2. 自动依赖：示例

让我们以一个广泛使用的程序 `ls`（目录列出器）为例。在 Red Hat Linux 系统中，`ls` 是 `fileutils` 包的一部分，并安装在 `/bin` 中。让我们在 `fileutils` 包构建过程中扮演 RPM 的角色，并对 `/bin/ls` 运行 `find-requires`。我们将看到以下内容：

```
# find-requires
/bin/ls
<ctrl-d>
libc.so.5
#
```

`find-requires` 脚本返回了 `libc.so.5`。因此，RPM 在构建 `fileutils` 包时应添加对 `libc.so.5` 的需求。我们可以通过使用 RPM 的 `--requires` 选项来显示 `fileutils` 的需求，从而验证 RPM 确实添加了 `ls` 对 `libc.so.5` 的需求：

```
# rpm -q --requires fileutils
libc.so.5
#
```

好的，这是等式的第一部分：RPM 自动检测包的共享库需求。现在让我们看看等式的第二部分：RPM 检测提供共享库的包。由于 `libc` 包（除其他外）包含共享库 `/lib/libc.so.5.3.12`，RPM 将获取其 soname。我们可以使用 `find-provides` 打印库的 soname 来模拟这种情况：

```
# find-provides
/lib/libc.so.5.3.12
```

### 14.2.3. `autoreprov` 标签：禁用自动依赖处理

好的，`/lib/libc.so.5.3.12` 的 soname 是 `libc.so.5`。让我们看看 `libc` 软件包是否确实提供了 `libc.so.5` 这个 soname：

```
# rpm -q --provides libc
libm.so.5
libc.so.5
#
```

是的，就在这里，还有包含在该软件包中的另一个库的 soname。通过这种方式，RPM 可以确保，只要安装了提供 `libc.so.5` 的 `libc` 软件包，任何需要 `libc.so.5` 的软件包都能拥有一个兼容的库。

在大多数情况下，自动依赖足以满足需求。然而，在某些情况下，软件包构建者必须手动向软件包添加依赖信息。幸运的是，RPM 对手动依赖的处理方式既简单又灵活。

有时，可能不希望使用 RPM 的自动依赖处理。在这种情况下，可以使用 `autoreprov` 标签来禁用它。此标签接受 yes/no 或 0/1 的值。例如，要禁用自动依赖处理，可以使用以下行：

```
AutoReqProv: no
```

## 14.3. 手动依赖

你可能已经注意到，我们一直使用 `requires` 和 `provides` 这两个词来描述软件包之间的依赖关系。事实证明，这些正是用于在 spec 文件中手动添加依赖信息的确切单词。让我们看看第一个标签：`requires`。

### 14.3.1. `requires` 标签

在讨论软件包具体需要什么是的时候，我们一直故意含糊其辞。虽然我们使用了 *capabilities*（功能）一词，但实际上，手动依赖要求总是以软件包的形式表示的。例如，如果软件包 `foo` 需要安装软件包 `bar`，则只需在 `foo` 的 spec 文件中添加以下行：

```
Requires: bar
```
