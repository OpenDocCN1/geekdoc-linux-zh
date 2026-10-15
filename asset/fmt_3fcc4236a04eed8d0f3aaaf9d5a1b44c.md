
你可能感兴趣的大多数第三方仓库都包含非开源软件。例如，如果你想为 Linux 安装 Adobe Flash 插件，可以从 Adobe 下载 YUM 仓库软件包，然后你可以使用 `yum` 命令安装 Flash 插件，并在可用更新时通过运行 `yum update` 命令获取更新。

## 使用 yum 命令管理软件

`yum` 命令有几十个子命令可供你处理系统上的 RPM 软件包。以下章节提供了一些实用的 `yum` 命令行示例，用于搜索、安装、查询和更新与你的系统相关的软件包。后续章节还包含了一个描述如何使用 `yum` 命令删除软件包的章节。

描述 YUM 仓库内容的元数据会在你第一次运行命令时从你启用的每个仓库中下载。默认情况下，90 分钟后会再次下载。元数据越大，下载所需的时间越长。你可以通过增加过期时间（在 `/etc/yum.conf` 中）或禁用不需要的仓库来减少此类下载。你甚至可以根据 RPM 数据库验证软件包，查看是否有人篡改了已安装的组件。

## 搜索软件包

使用不同的搜索命令，你可以根据关键词或其他属性查找软件包。假设你想尝试不同的软件包，但不记得想要的名字了。你可以开始使用 `search` 命令在名称中查找术语：

```
# yum search editor
eclipse-editor.x864 : Eclipse-based
emacs.x86_64 : GNU
```

要获取该软件包的信息，使用 `info` 子命令：

```
# yum info emacs
Name : emacs
Arch : x86_64
Epoch : 1
Version : 24.4
Release : 3.fc21
Size : 30 M
Repo : updates
Summary : GNU Emacs
URL : http://www.gnu.org/software/emacs
License : GPL3
Description : Emacs 是一种强大的、可定制的、自文档的编辑语言 (elisp)，具有读取邮件、新闻等功能。
```

## 第 10 章：获取和管理软件

`list` 子命令可以用不同的方式列出软件包名称。配合软件包基础名称，查找软件包的版本和仓库。你可以列出可用或已安装的软件包，也可以列出所有软件包。

```
# yum list emacs
emacs.1:24-3.fc21
# yum list available
rpm-admin.1.35-2.fedora
rpm-admin-console.noarch 1.35-2.fedora
rpm-admin-console-doc.noarch 1.8-7.fedora
```

```
# yum list installed
Installed Packages
GConf2.3.2-16.fc21 @koji-0/$releasever
LibRaw.0.16-0.fc21 @koji-0/$releasever
```

如果你找到了一个软件包，但想查看它依赖哪些组件，可以使用 `deplist` 子命令。通过 `deplist`，你可以看到组件（依赖），也可以看到提供该组件的软件包（提供）。如果没有软件包可以提供依赖项，但你想知道是什么组件以便搜索其他仓库，那么 `deplist` 就会很有帮助。考虑以下示例：

```
# yum deplist emacs | less
package: emacs.x86_64 1:24.4-3.fc21
dependency: /bin/sh
provider: bash.x86_64 4.4.33-1.fc21
provider: /usr/bin/alternatives
provider: chconfig.x86_64 1.3.63-1.fc21
provider: dejavu-sans-mono-fonts
provider: dejavu-sans-mono-fonts.noarch 2.34-4.fc21
```

## 安装和删除软件包

`install` 子命令允许安装一个或多个软件包以及任何所需的依赖包。通过 `yum install`，可以搜索多个仓库来满足所需的依赖。考虑以下 `yum install` 的示例：

```
# yum install emacs
...
```

### 第三部分：成为 Linux 系统管理员

| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| 安装中: | | | | |
| emacs | x86_64 | 1:24.3-fc21 | updates | 3.0 M |
| 安装依赖项: | | | | |
| ImageMagick-libs | x86_64 | 6.8.10-5.fc21 | fedora | 2.0 M |
| emacs-common | x86_64 | 1:24.3-fc21 | updates | 37 M |
| libXaw | x86_64 | 1.0.12-fc21 | fedora | 190 k |
| liblockfile | x86_64 | 1.08-16.fc21 | updates | 27 k |
| libotf | x86_64 | 0.9.13-5.fc21 | fedora | 96 k |

### 事务摘要

安装 1 个软件包 (+5 个相关依赖包)

总下载大小：42 M
安装大小：109 MB [y/N]: y

你可以看到 `emacs` 需要安装 `emacs-common` 以及其他几个软件包；所有包都已排队等待安装。这六个软件包共需下载 26MB，但在安装后占用 9MB 空间。在执行操作时，你可以在命令行中加上 `-y`（紧跟在 `yum` 命令之后），这样就可以避免手动按 `y` 来安装软件包。我个人倾向于在同意事务之前之前查看所有即将安装的软件包。

如果你不小心删除了已安装软件包的组件，可以重新安装该软件包。如果你尝试普通安装，系统会响应“无事可做 (nothing to do)”。相反，你必须使用 `reinstall` 子命令。例如，假设你安装了 `zsh` 软件包，然后不小心删除了 `/bin/zsh`。可以通过以下操作恢复丢失的组件：

```bash
# yum reinstall zsh
```

你可以使用 `erase` 命令删除单个软件包。例如，要删除 `emacs` 软件包，你可以输入：

```bash
# yum erase emacs
```

依赖关系已解决=============================================
| 软件包 | 架构 | 版本 | 存储库 | 大小 |
|---|---|---|---|---|
| 正在移除: | | | | |
| ============================================================= | | | |
| emacs | x86_64 | 1:24.3-fc21 | @updates | 14 M |

### 事务摘要

移除 1 个软件包

安装大小：14 MB 是否确定 [y/N]: y

注意，在安装 `emacs` 时安装了六个软件包，但使用 `erase` 子命令只删除了 `emacs` 包本身。尽管 `emacs` 要求安装 `emacs-common`，但 `emacs-common` 并不依赖于 `emacs`，因此可以留在系统中而不破坏依赖关系。运行 `yum remove emacs-common` 将会同时移除这两个软件包。

移除已安装软件包组的另一种方法是使用 `history` 子命令。通过 `history`，你可以查看你的 `yum` 活动并撤销整个事务。换句话说，可以使用 `history` 子命令的 `undo` 选项来卸载你安装的所有软件包。例如：

```bash
# yum history
ID | 登录用户 | 日期和时间 | 动作 | 更改
96 | Chris Neagus <cneus> | 2016-12-10 06:25 | 安装 | 2
# yum history info 96
事务 ID : 96
命令行 : install emacs
```

```bash
# yum undo 96
撤销事务 96，源自 2014年12月14日 06:25:41
Dep-Install emacs-common-1:24.4-3.fc21.x86_64 @updates
Dep-Install libXaw-1.0.12-4.fc21.x86_64 @fedora
```
