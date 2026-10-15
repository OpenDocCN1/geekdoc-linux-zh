
`if` 条件可以嵌套。也就是说，一个 `if` 条件可以包含另一个 `if` 条件。`if` 条件不需要有 `elif` 或 `else` 部分。如果 `if` 语句中指定的表达式以及后续可选的 `elif` 语句中的表达式都没有为真，则执行 `else` 部分。关键字 `fi` 用于表示 `if` 语句的结束，如果你有嵌套的 `if` 条件，这将非常有用。在这种情况下，你应该能够将 `fi` 与 `if` 匹配，以确保所有 `if` 语句都正确编码。

在以下 `bash` 示例中，变量 `var` 可以具有两个值之一：`Yes` 或 `No`。任何其他值都是无效的。可以按以下方式编码：

```sh
if [ $var = "Yes" ]; then
    echo "Value is Yes"
elif [ $var = "No" ]; then
    echo "Value is No"
else
    echo "Invalid value"
fi
```

# case 语句

`case` 语句用于根据与指定变量匹配的离散值或值范围来执行语句。在大多数情况下，如果你有大量条件，可以使用 `case` 语句代替 `if` 语句。

`bash` 中 `case` 语句的格式如下：

```text
case str in
    str1 | str2)
        Statements;;
    str3, str4)
        Statements;;
    *)
        Statements;;
esac
```

你可以为每个条件指定一系列离散值——例如 `str1`、`str2` 等，或者你可以指定带有通配符的值。最后一个条件应该是 `*`（星号），如果在其他条件都不满足时执行。对于指定的每个条件，直到双分号 (`;;`) 为止的所有相关语句都会被执行。

你可以编写一个脚本，如果提供月份编号作为参数，则回显月份名称。如果你提供的编号不在 1 到 12 之间，则会得到错误消息。脚本如下：

```sh
#!/bin/sh

case $1 in
    01 | 1) echo "Month is January";;
    02 | 2) echo "Month is February";;
    03 | 3) echo "Month is March";;
    04 | 4) echo "Month is April";;
    05 | 5) echo "Month is May";;
    06 | 6) echo "Month is June";;
    07 | 7) echo "Month is July";;
    08 | 8) echo "Month is August";;
    09 | 9) echo "Month is September";;
    10) echo "Month is October";;
    11) echo "Month is November";;
    12) echo "Month is December";;
    *) echo "Invalid parameter";;
esac
```

你需要在每个条件下的语句末尾加上双分号（`;;`）。如果没有这样做，下一个条件下的语句也会被执行。

最后一个条件应该是 `*default*`，如果在其他条件都不满足时执行。对于指定的每个条件，直到 `*break*` 为止的所有相关语句都会被执行。

# break 和 exit 语句

你应该了解另外两个语句：`*break*` 语句和 `*exit*` 语句。

`*break*` 语句可用于终止迭代循环，例如 `*for*`、`*until*` 或 `*repeat*` 命令。

`*exit*` 语句可用于退出 shell 程序。你可以在 `*exit*` 后可选地添加一个数字。如果当前的 shell 程序是由另一个 shell 程序调用的，调用程序可以检查代码（根据 shell 不同，为 `$?` 或 `$status` 变量）并据此做出决定。

# 在 Shell 脚本中使用函数

与其他编程语言一样，shell 程序也支持函数。`*函数*` 是 shell 程序的一部分，用于执行特定过程；你可以在 shell 程序中多次重用同一个函数。函数有助于消除在编写 shell 程序时重复代码的需求。

`bash` 中函数的格式如下：

```text
func() {
    Statements
}
```

你可以如下调用函数：

```text
func param1 param2 param3
```

参数 `param1`、`param2` 等是可选的。你也可以将参数作为单个字符串传递——例如，`$0`。函数可以像解析从命令行作为命令行参数传递给 shell 程序的位置参数一样解析参数，但使用脚本内部传递的值。例如，以下脚本使用了一个名为 `DisplayMonth()` 的函数，该函数显示月份名称或一个

## 参考

- [http://www.gnu.org/software/bash/bash.html](http://www.gnu.org/software/bash/bash.html)— GNU 软件项目中的 Bash 主页。
- [http://www.tldp.org/LDP/abs/html/](http://www.tldp.org/LDP/abs/html/)— Mendel Cooper 的《高级 Bash 脚本指南》。
- [http://www.linuxnewbie.org/nht/intel/shells/basic.html](http://www.linuxnewbie.org/nht/intel/shells/basic.html)— 在该网站学习基本的 shell 命令。
- [http://www.cs.princeton.edu/~jlk/jlk/ksh93/](http://www.cs.princeton.edu/~jlk/jlk/ksh93/)—“The New Korn Shell—ksh93”，由 David G. Korn、Charles J. Northrup 和 Jeffery Korn 撰写的关于 Korn shell 的文章。
- [http://lug.umbc.edu/~mabzug1/bash-httpd.html](http://lug.umbc.edu/~mabzug1/bash-httpd.html)— Bash-httpd 常见问题解答，并附有指向最新版 bash 网络服务器 bash-httpd-0.02 的链接。
- [http://www.tsch.org/](http://www.tsch.org/)— 在此处了解有关 tesh 的更多信息。
- [http://www.zsh.org/](http://www.zsh.org/)— 在此处更详细地考察 zsh。

# 第 34 章

# 高级软件管理

Fedora 预先提供了大量已安装并随时可用的软件包。然而，Fedora 还附带了一个出色的软件包管理工具，名为 `yum`，它允许你快速轻松地下载和安装更多软件包。`yum` 工具（Yellowdog Updater, Modified）自 Fedora 1 版起就已包含在内，并已成为安装和更新应用的首选工具。本章将探讨 `yum` 的工作原理、基本用法以及更高级的软件包和存储库管理，包括使用 Fedora 提供的一些图形界面工具。但在开始之前，我们先看看 RPM，这是 `yum` 利用的底层技术。

## 使用 RPM 进行软件管理

`rpm` 命令使用 RPM 系统来安装、删除（erase）、升级、验证以及构建被称为 RPM 文件的软件存档。这些存档或软件包包含软件包标识（签名）、校验和（通过数学推导得出的验证值）以及软件存档本身，后者可以是源代码形式或二进制形式。RPM 软件包还包含大量额外信息，例如名称、版本和基本描述，并且可以包含用于软件安装、清除或升级的安装前和安装后脚本。

## 本章内容

- 使用 RPM 进行软件管理
- `yum` 入门
- 非交互式运行 `yum`
- 使用 `yum` 移除软件包
- 维护 `yum`
- 使用 `yum` 管理软件包清单
- 配置 `yum`
- 使用 `pirut` 进行软件管理
- 使用 Yum Extender
- 创建本地 `yum` 存储库
- 参考

## 什么是 RPM？

RPM 有着悠久的历史，并与 Fedora 的发起人 Red Hat 紧密相关。RPM 本身可以追溯到早期的 Linux 软件包管理软件——名为 RPM PMS 和 PM，它们是用 Perl 编写的。RPM 出现在 1995 年底发布的 Red Hat Linux 2.0 中，并在 1996 年发布的 Red Hat Linux 3.0.3 (Picaaso) 版本中用 C 语言重写。自那时起，`rpm` 命令就成为 Red Hat 独特软件管理系统的主要特性，该系统基于“纯净源代码”的概念，或者说是使用程序源代码的单个初始存档来构建针对不同系统的软件包并跟踪版本的能力。
