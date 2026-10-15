
```
%_prefix /usr
%_exec_prefix %{prefix}
%_bindir %{prefix}/bin
%_sbindir %{prefix}/sbin
%_libeccdir %{prefix}/libexec
%_datadir %{prefix}/share
%_sysconfdir %{prefix}/etc
%_sharedstatedir %{prefix}/com
%_locatadir %{prefix}/var
%_libdir %{prefix}/lib
%_includedir %{prefix}/include
%_oldincludedir /usr/include
%_infodir %{prefix}/info
%_mandir %{prefix}/man
```

# 构建阶段

在提供包信息后，你需要按照第 10 节和第 12 节的定义构建阶段。

# 构建准备

构建准备部分为构建奠定。通常该部分包含一个 `%setup` 命令。例如：

```
%prep
%setup -q
```

## 构建

构建部分描述了如何构建库或应用程序。在大多数情况下，大部分指令位于由 prep 部分创建的 Makefile 中，留下的构建部分如下：

```
%build
%configure
make
```

## 安装

构建完成后，安装部分包含安装库或应用程序的命令。例如：

```
%install
rm -rf %(buildroot)
%makeinstall
```

# 清理

clean 部分通常调用 `make clean` 命令来清理已构建的文件。例如：

```
%clean
rm -rf %(buildroot)
```

# 安装和卸载脚本

RPM 包可以在安装前通过 `%pre` 运行，并在安装后通过 `%post` 运行。你还可以在卸载前通过 `%preun` 运行，并在卸载后通过 `%postun` 运行。例如：

```
%post
/sbin/chkconfig --add ybind
```

```
%preun
if [ "$1" = 0 ]; then
  /sbin/service ybind stop > /dev/null 2>&1
  /sbin/chkconfig --del ybind
fi
exit 0
```

```
%postun
if [ "$1" -ge 1 ]; then
  /sbin/service ybind restart > /dev/null 2>&1
fi
exit 0
```

# 文件标签

`%files` 标签列出了你的包应该安装的文件。例如：

```
%files

%defattr(.root,root)

/usr/X1R6/bin/xtoolwait

/usr/X1R6/man/man1/xtoolwait.*
```

你应该分别用 `%config` 和 `%doc` 标记配置和文档文件。例如：

```
%files

%defattr(.root,root)

/sbin/ypbind

%_mandir/*//*

%config /etc/rc.d/init.d/*

%config /etc/yp.conf

%dir /var/yp

%dir /var/yp/binding

%doc README NEWS
```

# 创建可定位包

你可以通过设置一个或多个 Prefix 标签来制作可定位包。例如：

```
Prefix: /usr

Prefix: /etc
```

此时 `%files` 部分中的每个文件必须以提供的前缀之一开头。借此，安装程序可以使用如下命令轻松地重定位包：

```
# rpm --relocate /etc=/usr/etc file_name.rpm
```

# 变更日志

变更日志通常出现在 spec 文件的末尾。它记录了每个重大变更的消息。例如：

```
%changelog
* Fri Jun 21 2002 Bob Marley <marley@redhat.com>
  - automated rebuild

* Tue May 08 2001 Peter Tosh <tosh@redhat.com> 1.3-1
  - updated to 1.3
```

# 附录 C

# RPM 功能演进

尽管 RPM 实现在版本之间很大程度上兼容，但 RPM 打包人员必须记住 RPM 是一个仍在不断进化的程序，开发者在每个版本中都会为其添加功能。在生成 RPM 包文件时，打包人员必须考虑使用最终 RPM 包文件的受众。他们必须决定该包将与哪些版本的 RPM 使用，并仅使用所目标 RPM 版本中最旧版本中已实现的最小公约数功能。作为快速参考，请记住这里提到的 RPM 特性以及引入它们的 RPM 版本。在考虑这些 RPM 的修订版时，感兴趣的主要发布版本是 RPM 2.5、RPM 3.0.5、RPM 4.0.4 和 RPM 4.1。

RPM 2.5 不再被广泛使用；只有在打算 RPM 包使用绝对的 RPM 版本进行安装时，才应该针对 RPM 2.5。

RPM 3.0.5 是 RPM 3.x 系列的最后一个发布版本。它是随 Red Hat Linux 6.2 及其他版本发放的 RPM。它仍然被其他供应商广泛使用。例如，Cobalt 发行版使用基于 RPM 3.0.5 的 RPM 实现版本。（Red Hat Linux 通过错误修复升级到了 RPM 4）。

RPM 4.0.4 用于 Red Hat Linux 的 7.x 版本，而 RPM 4.1 首次随 Red Hat Linux 8 发布。目标为 RPM 3.0.5 的包应该兼容几乎所有仍在使用的 RPM 实现。针对 RPM 3.0.4 或 RPM 4.1 的包将仅与较新的实现工作。

RPM 2.5 是最旧的 RPM 版本，从想象力来说，它仍然可能被使用。在 RPM 2.5 中，大多数基本功能已经到位，还包含了触发器（triggers）以及 RPM 文件中的国际化 Summary:Description 和 Group 标签。RPM 2.5 也是第一个使用版本 3 格式的 RPM 版本。

RPM 2.5.3 为 RPM 头增加了 Epoch 支持，实现了 `RPM_EPOCH`。

RPM 2.5.4 引入了 `%license` 和 `%readme` 类型，可在 RPM spec 文件指定许可证和 README 文件。

RPM 2.5.6 增加了 RPM spec 文件中使用 `Epoch:` 关键字的支持，允许为你的包强制 Epoch。`Epoch:` 替换了语义相似的旧关键字 `Serial:`。

RPM 2.5.7 强制了以前隐含的 RPM spec 文件 Version 或 Release 字段的标准。

RPM 2.9 引入了使用 GPG（GNU Privacy Guard）进行签名和验证 RPM 包的支持。

RPM 2.91 允许使用 `Provides:` 指令定义提供文件的绝对路径。在 RPM 2.91 之前，`Provides` 只能用于列出功能，不能用于类似 `Provides: /path/to/file` 的语句。

RPM 3.0.2 首次允许使用多个 `Provides:` 行，消除了在 spec 文件中将所有提供的功能合并到同一行的需求。

RPM 3.0.3 增加了对版本依赖的支持。在 RPM 3.0.3 之前，spec 文件可以指示包需要另一个包或提供特定功能，但无法指示所需包的可接受版本或功能的版本。

RPM 3.4 为 RPM 增加了 CompressedFileNames 支持。在 RPM 3.4 之前，RPM 打包了包内归档文件的绝对路径。包头包含如下语句：

```
fileName #0: /usr/bin/ar
fileName #1: /usr/bin/as
fileName #2: /usr/bin/gasp
fileName #3: /usr/bin/gprof
```

有了 CompressedFileNames 支持，RPM 包头存储的是目录，而不仅仅是目录内文件的文件名。对于具有多个文件的目录，包文件头包含如下语句：

```
dirName #0: /usr/bin
baseName dirIndex
#0      ar          0
#1      as          0
#2      gasp        0
#3      gprof       0
```

每个文件条目持有目录内的文件名，以及一个指向目录条目的索引号。由于包通常包含同一目录下的大量文件，CompressedFileNames 支持在处理包安装时可以节省大量内存。

RPM 3.0.5 为 RPM 增加了 PayloadBzip2 支持，允许 RPM 包文件的数据负载使用 bzip2 而不是 gzip。尽管 RPM 现在支持 RPM 文件的 bzip2 压缩，但该功能在实践中很少使用，因为安装 bzip2 压缩的 RPM 包比安装 gzip 压缩的 RPM 包需要更多的内存和时间。RPM 3.0.5 还增加了处理现有 RPM 版本 4 文件格式的支持；但 RPM 3.0.5 生成的包只能是版本 3 文件。
