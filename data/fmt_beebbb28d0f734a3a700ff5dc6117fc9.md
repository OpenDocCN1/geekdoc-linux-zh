
  `--sharedstatedir=/usr/com` \
  `--mandir=/usr/share/man` \
  `--infadir=/usr/share/info`

![](img/9d29d6681c5f42792ea5da4b12142ca2_216_0.png)

构建软件的大部分工作应该保留在它们所属的 `Makefile` 中。spec 文件中的命令应该调用 `Makefile` 中定义的目标 `targets`。不要在你的 RPM spec 文件中放置过多逻辑，因为这会使你计划打包的应用程序或库的测试变得困难。

如果你打算支持可重定位包，在第 11 章中介绍，你可能需要向 `configure` 脚本传递一个 `--prefix` 选项。例如：

```
%build

./configure --prefix=$RPM_BUILD_ROOT/usr

make
```

你可以根据需要向 `configure` 脚本传递其他选项来编译应用程序。

# 安装软件

`%install` 部分应该安装在 `%build` 节中构建的软件。如果你的 `Makefile` 包含了安装它的所有指令，你可以按照如下方式定义一个 `%install` 节：

```
%install

make install PREFIX=$RPM_BUILD_ROOT/usr
```

在大多数情况下，你需要向 `make` 或 `install` 或另一个命令传递某些参数，将所有文件安装到 buildroot 目录，如此示例中使用 `$RPM_BUILD_ROOT` 环境变量。你需要查看 `Makefile` 内部以确定 `make` 变量应该是 `PREFIX`、`prefix` 还是其他。

有时，你需要调用 `install` 命令而不是 `make` 来执行安装。例如：

```
%install

install -m755 myapp $RPM_BUILD_ROOT/usr/bin/myapp
```

此示例使用了假设的应用程序名称 `myapp`。
许多包使用 `%makeinstall` 宏，它会运行 `make` 命令。例如：

```
%install

rm -rf $RPM_BUILD_ROOT

%makeinstall
```

此示例还清理了 buildroot 中的文件。使用 `rpm --eval` 命令可以查看 `%makeinstall` 宏是如何展开的。例如：

```
$ rpm --eval '%makeinstall'

make \
  prefix=/usr \
  exec_prefix=/usr \
  bindir=/usr/bin \
  sbindir=/usr/sbin \
  sysconfdir=/etc \
  datadir=/usr/share \
  includedir=/usr/include \
  libdir=/usr/lib \
  libexecdir=/usr/libexec \
  localstatedir=/var \
  sharedstatedir=/usr/com/com \
  mandir=/usr/share/man \
  infodir=/usr/share/info \
  install
```

RPM 4.2 在 `%install` 之后添加了一个 `%check` 节。

# 构建后的清理工作

`%check` 部分负责清理构建和安装，移除编译的文件以及作为构建一部分创建的文件。如果你使用了之前讨论过的 buildroot，你可以提供如下所示的 `%clean` 节：

```
%clean
rm -rf $RPM_BUILD_ROOT
```

# 定义安装脚本

除了前述用于控制软件包构建的节外，你还可以在 RPM spec 文件中定义更多脚本。RPM 支持在安装前运行的脚本 `%pre` 和在安装后运行的脚本 `%post`。当包被删除或卸载时，同样的概念也适用于这些情况。`%preun` 脚本在卸载之前运行，`%postun` 脚本在卸载之后运行。

> 第 11 章涵盖了触发器 `triggers`，另一种在包安装或删除时运行的脚本形式。

以对应脚本的 RPM 节标记开始你的脚本，例如用于安装前的脚本 `%pre`。然后，放置你想要运行的 shell 命令。例如，以下是 ybind 网络包的 `%post`、`%preun` 和 `%postun` 脚本：

```
%post
/sbin/chkconfig --add ybind
```

# 第 11 部分：创建 RPM

```
%preun
if [ "$1" = 0 ]; then
  /sbin/service ybind stop > /dev/null 2>&1
  /sbin/chkconfig --del ybind
fi
```

```
%post
if [ "$1" -ne 0 ]; then
  /sbin/service ybind start > /dev/null 2>&1
fi
```

*(注：由于原始文本后半部分存在大量重复和乱码字符，此处已根据指令要求对有效逻辑进行了翻译和整理。)*

## 第 10 章：使用 Spec 文件

![](img/9d29d6681c5f42792ea5da4b12142ca2_222_0.png)

除了标记的目录外，标准的 Linux 文档目录如 `/usr/man` 被自动假认为文档目录。

与 `%doc` 指令类似，`%config` 指令将文件标记为配置。例如：

```
%files
/sbin/ypbind
%config /etc/rc.d/init.d/*
%config /etc/yp.conf
%doc README NEWS
```

`%config` 指令有一个特殊选项 `noreplace` 不替换，告诉 RPM 不要覆盖或替换配置文件。例如：

```
%files
/sbin/ypbind
%config /etc/rc.d/init.d/*
%config(noreplace) /etc/yp.conf
%doc README NEWS
```

使用此选项可以帮助保护本地修改。如果你使用 `%config(noreplace)`，该文件将不会覆盖已修改的现有文件。如果磁盘上的文件未被修改，则 `rpm` 命令将覆盖该文件。但如果文件已被修改，`rpm` 命令将带有 `.rpmnew` 额外扩展名复制新文件。

同样，`%config(missing)` 意味着文件在磁盘上不存在。你可以将此修饰符用于由 `%ghost` 脚本创建但在删除包时需要被删除的文件或链接。

另一个特殊修饰符 `%ghost` 告诉 `rpm` 命令不要将文件包含在包中。你可以使用此名称为程序在安装时创建的文件提取所需的属性。例如，你可能希望确保程序的日志文件具有某些属性。

## 设置文件属性

当你的软件包安装时，你可以控制文件属性以及包含在包中的文件。这非常有用，因为大多数软件包都是由 root 用户安装的，而你不希望 root 用户拥有这些文件。`xattr` 属性允许你控制特定文件的权限。格式为：

```
%attr(mode, user, group) filename
```

### 例如：

```
%attr(0644, root, root) /etc/yp.conf
```

此示例将文件权限设置为 644，用户和组组设置为 root。如果你不需要指定值，可以使用连字符 `-` 保持该文件的设置不变。例如：

```
%attr(-, root, -) /etc/yp.conf
```

请注意，你可以连续组合多个指令。例如：

```
%config %attr(-, root, -) /etc/yp.conf
```

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
