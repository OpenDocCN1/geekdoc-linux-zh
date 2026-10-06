

# 334 第三部分 ♦ 在 SUSE Linux 中使用命令行

## 列表 12-7: RPM 头部

| 摘要：Logcheck 系统日志分析器 |
| :--- | :--- |
| 名称 | logcheck |
| 版本 | 1.1.2 |
| 发布 | 2 |
| 供应商 | Craig Rowland <crowlandepsionic.com> |
| 打包员 | Justin Devies <justinpalcmoder.net> |
| 许可证 | GPL |
| 分组 | Applications/System |
| 源 | http://www.palcmoder.net/files/suse-rpm/10/{name}-version.tar.gz |

```
URL:
http://www.palcmoder.net/files/suse-rpm/10
Requires: cnn
Requires: /usr/bin/sendmail
BuildRoot: %tmp/{name}-buildroot
%description
Logcheck 是一个旨在自动运行并检查系统日志是否存在安全违规和异常活动的软件包。
Logcheck 使用了一个名为 logtail 的程序，该程序会记住上次从日志文件中读取的位置，并在后续运行中使用该位置来提供新信息。
```

某些头部选项是自言自语的，例如摘要（Summary）和包名称（Name）。但是，有些还需要进一步的解释。

- 该头部文件最重要的部分之一是版本（version）和发布（release）。
- **Version（版本）**——软件包的主版本号，通常指源版本。
- **Release（发布）**——发布的子版本。这用于对主包进行漏洞修复等更新。
- **Vendor（供应商）**——编写软件的公司或人员名称，而 Packager（打包员）是维护 RPM 包的人员名称。
- **License（许可证）**——软件包/源代码遵循的许可证。在这种情况下，logcheck 根据 GPL 许可证发布。
- **Group（分组）**——维护一个定义的组列表，以控制软件所属的通用部分。分组定义用于告诉用户他们正在安装什么类型的应用程序，并且不会影响 RPM 本身。使用图形用户界面 (GUI) 工具查看 RPM 包时，分组定义用于将应用程序分组到位于以下位置 GROUPS 文件中的标题下：

```
/usr/share/doc/packages/rpm/GROUPS。该文件包含每个组以及其随后的组子部分：
```

- Amusements/Games
- Amusements/Graphics
- Applications/Archiving
- Applications/Communications
- Applications/Databases
- Applications/Editors
- Applications/Emulators
- Applications/Engineering
- Applications/File
- Applications/Internet
- Applications/Multimedia
- Applications/Productivity
- Applications/Publishing
- Applications/System
- Applications/Text
- Development/Debuggers
- Development/Languages
- Development/Libraries
- Development/System
- Development/Tools
- Documentation
- System Environment/Base
- System Environment/Daemons
- System Environment/Kernel
- System Environment/Libraries
- System Environment/Shells
- User Interface/Desktops
- User Interface/X
- User Interface/X Hardware Support

Source（源）——指向 RPM 源文件的位置。这非常重要，因为 RPM 构建过程在准备源分发时会使用此位置。尽管此条目指向网络地址，但最后一部分被用作源 tar 包的文件名，位于 `/usr/src/packages/SOURCES`。

Requires（依赖）——告诉 RPM 此包依赖于 cron RPM 包以及 `/usr/sbin/sendmail` 的存在。

BuildRoot（构建根）——RPM 准备最终 RPM 组成部分实体的位置。

Description（描述）——摘要的详细扩展。它提供了软件包作用的概述，是让最终用户了解软件包提供的功能的好去处。

# RPM 的 %prep 部分

当你定义了 RPM 头部后，需要为编译源码做准备。首先需要发生的事情是解压源分发包。RPM 使用宏 `%setup` 来执行此操作，如下所示：

```
%prep
setup -q
```

`%setup` 宏将源文件解压到 BUILD 目录。`-q` 选项在解压源文件时抑制输出。

# %build 宏

在准备好源码后，你需要为你的系统编译代码。

`%build` 宏允许你告诉 RPM 编译代码。你可以在这里使用任何 shell 命令，可以是配置脚本，也可以是用于 Makefile 的简单 make 命令。在这种情况下，你只是在 `logcheck` 源目录中运行 `make`。

```
%build
make
```

该宏进入源代码目录，并运行你在 `%build` 部分中定义的任何程序。你在命令行上用于编译应用程序的任何内容都可以输入此处。

接下来，你必须创建 `%install` 宏（见列表 12-8）。

## 列表 12-8: logcheck 的 %install 部分

```
%install
rm -rf $RPM_BUILD_ROOT/usr/sbin
mkdir -p $RPM_BUILD_ROOT/etc/logcheck
mkdir -p $RPM_BUILD_ROOT/etc/cron.hourly

install ... ./systems/linux/logcheck.hacking $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck.violations $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck.violations $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/usr/sbin
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/etc/logcheck
install ... ./systems/linux/logcheck $RPM_BUILD_ROOT/etc/logcheck
```

`%install` 宏是最复杂的，因为你必须准备 RPM。

1. 首先，你需要确保 RPM 构建没有完成。
2. 接下来，你需要创建目标目录。
3. 安装过程在实际上与 `cp` 相同。它将文件从一个位置复制到另一个位置。
4. cat 条目是创建文件的一种很好的方法。

# %clean 宏

在创建 RPM 后，会执行 `%clean` 宏。`%clean` 宏用于清理你的系统。与 spec 文件中的其他宏一样，你定义的 `%clean` 宏会在 RPM 构建期间自动执行，在这种情况下，RPM 已经构建完成。

```

rm -rf $RPM_BUILD_ROOT
```

# %files 宏

RPM 需要知道哪些文件归档到二进制 RPM 中。`%files` 宏包含相对于 RPM_BUILD_ROOT 的文件列表。列表 12-9 显示了一个示例。

## 列表 12-9: logcheck 的 %files 宏

```
%files
%defattr(644,root,root,755)
%doc CREDITS* systems/linux/README*
%attr(700,root,root) %dir /etc/logcheck
%attr(600,root,root) %config /etc/logcheck
%attr(700,root,root) %config /etc/cron.hourly/logcheck
%attr(755,root,root) /usr/sbin/logcheck.sh
%attr(755,root,root) /usr/sbin/logtail
```

在该文件中注意的条目如下：

- `%defattr` 宏为所有安装的文件设置权限，在每个文件条目处显式指定。
- 一个重要的 files 宏条目是 `%doc`。它用于指定列出的文件是文档。在 SUSE 中，所有 RPM 文档都存储在 /usr/share/doc/packages/rpmname。任何设置为 `%doc` 类型的文件将安装到 /usr/share/doc/packages/logcheck。
- `%attr` 宏为指定的文件设置权限。在 logcheck 配置文件的案例中，你指定了只有 root 可以访问这些文件。
- `%config` 条目指定指定的文件是配置文件。当 RPM 文件升级时，属于该 RPM 的任何配置文件将被“保留”，以便你可能所做的更改不会丢失。

