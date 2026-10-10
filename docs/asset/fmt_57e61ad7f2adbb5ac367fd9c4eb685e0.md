
通过相应的数字选择要编辑的文件。

`(-1` 退出) `(-3` 自动合并所有剩余文件)

`(-5` 自动合并并使用 '`mv -i`' );

```
如果你输入 -1，etc-update 将退出并停止任何后续更改。如果你输入 -3 或 -5，所有配置文件将被用新版本覆盖。因此，选择不应自动更新的第一个配置文件是非常关键的。这只需输入该配置文件左侧列出的数字即可。
```

作为一个示例，我们选择了配置文件 `/etc/perf.conf`：

## 代码列表 3：更新特定的配置文件

```
/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异开始

---

/etc/perf.conf 和 /etc/._cfgg0000_perf.conf 之间的差异结束

1) 用更新版本替换原始文件

2) 更新并保持原始文件不变

3) 交互式合并原始文件与更新版本

4) 再次显示差异
```

你可以看到两个文件之间的差异。如果你认为更新后的配置文件可以无问题使用，输入 `1`。如果你认为更新后的配置文件是不正确的，或没有提供任何有用信息，输入 `2`。如果你想交互式地更新当前文件，输入 `3`。

这里没有必要进一步阐述合并过程。为了完整起见，将列出在交互式合并这两个文件时可以使用命令。你将看到两个文件（原始文件和建议的新文件）以及一个可以输入以下命令的提示符：

## 代码列表 4：交互式合并命令

```
ed    编辑两个版本，每个版本都带有页头。

eeb   编辑使用两个版本。

elf   编辑使用左侧版本。

err   编辑使用右侧版本。

e    编辑当前版本。

i    使用左侧版本。

r    使用右侧版本。

s    使用当前版本。

v    详细信息。

q    退出。
```

## 5. 偏离官方树

### 5.a. 使用 Portage 树子集

排除包/类别

你可以选择性地更新类别/包并忽略其他类别。我们通过让 `rsync` 在合并 `--sync` 时排除类别/包来实现这一点。

你需要在 `/etc.conf` 的 `RSYNC_EXCLUDE` 变量中定义包含排除模式的文件名。

## 代码列表 1：在 etc.conf 中定义排除文件

```
RSYNC_EXCLUDE=/etc/portage/rsync_excludes
```

## 代码列表 2：在 /etc/portage/rsync_excludes 中排除所有游戏

```
games/*
```

注意这可能导致依赖问题，因为允许的包可能依赖于新的排除包。

### 5.b. 添加非官方构建

你可以使用 Portage 使用 Portage 树未提供的构建。创建一个新目录（例如 `/usr/portage`），在其中存储第三方构建。使用与官方 Portage 树相同的目录结构。

然后在 `/etc.conf` 中定义 `PORTDIR_OVERLAY` 并将其指向自定义目录。现在当你使用 Portage 时，它将考虑这些构建，而不会在下次运行 `emerge --sync` 时移除/覆盖这些构建。

处理多个 Overlay

对于想要多个 Overlay、在包进入 Portage 树之前进行测试或仅仅是为了从各种来源使用非官方构建的强力用户，`app-portage-gentookit-build` package sync 是一个帮助你保持 Portage Overlay 更新的工具。每个仓库应该在 `/etc/gentoo/configuration` 目录下有一个 `.rsyncsource` 文件，其中包含仓库位置、名称、ID 等。

假设你有两个额外的仓库，分别名为 `java`（用于开发中的 Java 构建）和 `entapps`（用于为企业内部开发的应用程序）。你可以使用以下命令更新这些仓库：

## 代码列表 3：使用 gensync 更新几个仓库

```
# gensync java entapps
```

### 5.c. 非 Portage 维护的软件

使用 Portage 使用自维护软件

当你想自己安装和维护软件而不使用 Portage 自动化该过程时，即使 Portage 可以提供软件标题。已知案例是内核源码和 NVIDIA 驱动程序。你可以配置 Portage 使其知道某个包是手动安装的。这个过程由 Portage 通过 `/etc/portage/profile/package.provided` 调用并支持。

例如，如果你告知 Portage 关于手动安装的 `vanilla-sources-2.6.11.6`，向 `/etc/portage/profile/package.provided` 添加以下行：

## 6. 构建应用程序

# 6. Emerge 和 Ebuild

`ebuild` 是 Portage 系统的一个低级接口。使用此应用程序，你可以针对指定的 ebuild 执行特定的操作。例如，你可以手动执行单独的合并步骤。

`ebuild` 通常用于开发目的；因此，关于 `ebuild` 的更多信息可以在《开发者手册》（Developers Handbook）中找到。然而，我们将解释 Portage 在特定软件标题的合并过程中是如何调用 `ebuild` 实例的，以及如何调用某些 `ebuild` 允许你执行的配置后步骤。

## 6.b. 手动安装软件

### 获取源码与校验

每当你针对给定的 `ebuild` 调用 `ebuild` 时，它会验证所有涉及文件的校验和是否与附带 `Manifest` 文件或 `files/digest-<name>-<version>` 文件中的值相等。这在获取源码之后发生。

使用 `ebuild` 获取源码，运行：

```
# ebuild path/to/ebuild fetch
```

如果 `ebuild` 的 `mdsum` 与 `Manifest` 文件中列出的不匹配，或者下载的源码与 `files/digest-<package>` 文件中列出的不匹配，你会收到类似下面的错误：

```
!!! File is corrupt or incomplete. (Digests do not match)

>>> our recorded digest: db20421ce35e854346e3ef19e6044e

>>> your file's digest: f10392b7c0b2bc463ad0964260a7d6
```

后续的一行将提到错误的文件。

如果你确定获取的源码和 `ebuild` 本身是有效的，可以使用 `ebuild` 的功能重新生成 `Manifest` 和 `digest-<package>` 文件：

```
# ebuild path/to/ebuild digest
```

### 解包源码

要在 `/var/tmp/portage`（或任何你在 `/etc/make.conf` 中指定的目录）中解包源码，请运行 `ebuild` 的 `unpack` 功能：

```
# ebuild path/to/ebuild unpack
```

这将执行 `ebuild` 的 `src_unpack()` 函数（如果没有定义 `src_unpack()`，则默认执行纯粹解压）。必要的补丁（patches）也是在这一步应用的的。

### 编译源码

合并过程的下一步是编译源码。`ebuid` 的 `compile` 功能通过执行 `ebuild` 中的 `src_compile()` 函数来处理这一步。这这也包括相应的 `configure` 步骤。

```
# ebuild path/to/ebuild compile
```

如果你想更改编译指令，建议编辑 `ebuild` 的 `src_compile()` 函数。不过，你也可以骗过 Portage，使其认为 `ebuild` 已经完成了编译步骤。运行所有必要的命令并在工作目录下创建一个名为 `.compiled` 的空文件：

# 代码列表 6：告知 Portage 编译任务已完成

```
# touch .compiled
```

### 在临时位置安装文件
在下一步，Portage 将将所有必要文件安装在临时位置。该目录将包含所有要在运行系统上合并的文件。你可以通过运行 `ebuild` 的 `install` 功能来实现这一点，该功能会执行 `ebuild` 的 `src_install()` 函数：

# 代码列表 7：安装文件

```
# ebuild path/to/ebuild
```
