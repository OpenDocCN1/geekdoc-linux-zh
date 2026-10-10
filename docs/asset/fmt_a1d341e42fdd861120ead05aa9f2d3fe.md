
```
Code List 1: 2004.3 配置的累积 USE 变量
（此示例是 base, default-linux, default-linux/x86 和 default-linux/x86/2004.3 设置的总和）
use86 oss avx build-fonts ctype encode f77
usekde sdl glip python gnome lib+ matt mad
usemod mikft mreq nis obgovnis opennis pdfrib python
qt quicktime release sdl svga truetype x xml znz xv*)
```

### 2b. 使用 USE-flags

#### 声明 USE-flags

如所示，此变量包含了许多关键词。不要修改任何 `make.files` 来声明符合需求的 `USE` 变量：此文件中的更改将在更新时可见！

要更改此默认设置，你需要向 `USE` 变量添加或移除关键字。这是通过在 `/etc/make.conf` 中全局定义 `USE` 变量来实现。在该变量中，你可以添加额外的 `USE-flags`，或者移除不需要的 `USE-flags`。后者通过在关键字前加上减号 `-` 实现。

例如，为了支持 KDE 和 Qt 添加对 ipad 支持，可以在 `/etc/make.conf` 中定义以下 `USE`：

![](img/c0231913cf632f51d9b75da531c717e6_51_0.png)

有时你只想为某个（或几个）应用程序声明特定的 `USE` flag，而不是全局范围。要实现这一点，你需要创建 `/etc/portage/` 目录（如果不存在）并编辑 `/etc/portage/package.use`。

例如，如果你不想在全局启用 `kerdb` 支持，但想为 `mysql` 启用，你可以执行：

```
Code List 3: /etc/portage.use example

dev-db/mysql kerdb
```

当然，你可以显式地禁用某个应用程序的 `USE` flag。例如，如果你不想在 PHP 中支持 java：

```
Code List 4: /etc/portage/package.use 2nd example

dev-php/php-java-
```

## 声明临时 USE-flags

有时你只想设置一次某个特定的 `USE` 设置。与其编辑两次 `/etc/make.conf`（为了执行和撤销 `USE` 更改），你只需将 `USE` 变量声明为环境变量。记住，当你重新合并或更新此应用程序时（无论是显式地还是作为系统更新的一部分），你的更改将会生效：

例如，我们将在安装 `mozilla` 期间临时从 `USE` 设置中移除 `java`。

```
Code List 5: Using USE as environment variable

USE="-java*" emerge mozilla
```

## 自动 USE Flags

软件包安装后，如果你没有显式禁用，已安装的 `USE` flags 将自动为你启用。要查看带有 flag 的包列表，请检查你的配置中的 `/etc/make.profile.defaults` 和 `use.defaults` 文件。

```
Code List 6: A snippet from /etc/make.profile.defaults

gnome gnome-base/gnome

gtk x11-libs/gtk+

dqt x11-libs/qt

kde kde-base/kdebase

motif x11-libs/motif
```

## 优先级

当然，存在某种优于 `USE` 设置的优先级。你不希望在声明了 `USE="-java"` 后，发现由于某个优先级更高的设置，java 仍然被使用。`USE` 设置按优先级排序（第一个优先级最低）：

1. 配置文件中 `make.defaults` 文件中的默认 `USE` 设置
2. 如果安装了来自 `profile.defaults` 的包，则继承的 `USE` 设置
3. `/etc/make.conf` 中的用户自定义 `USE` 设置
4. `/etc/portage/package.use` 中的用户自定义 `USE` 设置
5. 环境变量中的 `USE` 设置

要查看 Portage 看到的最终 `USE` 设置，运行 `emerge --info`。这将列出所有相关变量（包括 `USE` 变量）以及 Portage 所使用的内容。

```
Code List 7: Running emerge --info

# emerge --info
```

## 使你的系统适配新的 USE Flags

如果你更改了 `USE` flags 并希望更新整个系统以使用新的 `USE` flags，请使用 `--newuse` 选项：

```
### Code Listing 8: Rebuilding your entire system

# emerge --update --deep --newuse
```

接下来，运行 Portage 的 `declean` 来移除在你的“旧”系统上合并、但已由于新的 `USE` flags 变得过时的条件依赖。

**警告：** 运行 `emerge --depclean` 是一个危险的操作，应该小心处理。双重检查提供的“过时”包列表，以确保不会删除你需要的包。在接后的示例中，我们为 `declean` 添加了 `-p` 选项，仅列出包而不删除它们。

```
### Code Listing 9: Removing obsolete packages

# emerge --depclean
```

当 `declean` 完成后，运行 `revdev-rebuild` 来重新构建与可能被移除的包提供的共享对象动态链接的应用程序。`revdev-rebuild` 是 `gentoolkit` 包的一部分；不要忘记安装它。

```
### Code Listing 10: Running revdev-rebuild

# revdev-rebuild
```

完成完成后，你的系统将使用新的 `USE` flag 设置。

### 2.c. 特定包的 USE-flags

**查看可用的 USE-flags**

让我们以 `mozilla` 为例：它监听哪些 `USE-flags`？要找到答案，我们使用 `--pretend` 和 `--verbose` 选项进行合并：

```
### Code Listing 11: Using the used USE-flags

# emerge --pretend --verbose mozilla

These are the packages that I would merge, in order:

Calculating dependencies ...done

[build] R //www/mozilla-1.7.2-2 USE='crypt gnome java mozsvg ssl

truetype xtprint -xdap -ipv6 -lapad mozcalendar -mozdevel -nozcompose

nozoirc -moznall -nozoft -postgres -xineama 0 KB
```

`emerge` 不是完成此项工作的唯一工具。事实上，我们有一个专门查询包信息的工具称为 `query`，它位于 `gentoolkit` 包中。首先，安装 `gentoolkit`：

```
### Code Listing 12: Installing gentoolkit

# emerge gentoolkit
```

现在运行参数来查看特定包的 `USE-flags`。例如，对于 `gnumeric` 包：

```
### Code Listing 13: Using query to view used USE-flags

# query use gnumeric

[ Colour : set theme ]

[ Legend

- (U) Col 1 Current USE flags

 (I) Col 2 Installed with USE flags ]
```

```
U I [ Found these variables in : app-office/numeric-1.2

libda : Adds Data Access (CORBA wrapper) support for gnumeric

gomedeb : unknown

+ + python : support/bindings for the Python language

+ + bonobo : Adds support for gnome-base/bonobo (Gnome CORBA interfaces)
```
