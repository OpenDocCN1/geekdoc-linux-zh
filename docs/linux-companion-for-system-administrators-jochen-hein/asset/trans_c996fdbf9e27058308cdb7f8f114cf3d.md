

# 邮件与新闻中的特殊字符 253

注释从第 1 列后开始，第 1 列的命令为激活状态

- 原样字符 160 到 254 的字符按原样显示（现已激活）

列表 9.10 针对编辑器 joe 的适配。

| 额外信息与来源 |
|------|
| 手页 (Man pages): | joe(1) |
| 新闻组: | comp.editors |
| 软件包: | joe23.tar.Z |
| ftp 服务器: | ftp.std.com |
| ftp 路径: | /pub/gnu |
| 大小: | 约 300 KB |

另一个易于处理的旧 DOS 编辑器是 pico。该编辑器从设计初就支持 8 位纯净（8-bit clean）；它位于邮件和新闻阅读器 pine 的归文件中。

## 9.6 邮件和新闻中的特殊字符

在邮件和新闻中，外语言（或任何其他 8 位）字符可以直接发送，前提是传输路径是 8 位纯净的。免费提供的程序 smail 和 sendmail 要么定义上是 8 位的，要么可以相应配置。在当前的 sendmail 版本中，你必须在 `sendmail.cf` 文件中包含 `O7false`。在许多商用操作系统中常见的旧版 sendmail 不是 8 位的，且无法进行适当配置。

今天使用的几乎所有新闻系统都是 8 位纯净的。目前仍在使用（尽管很少）的非 8 位纯净的新闻只有 B-News。因此，可以安全地假设 8 位字符在通过 Usenet 传输时能够保留。

虽然下面的邮件或新闻头文件并不符合 [rfc2045] 中定义的互联网标准，但它实际上是被允许的，并且可以帮助通过不同的邮件和新闻系统不受干扰地传输包含特殊字符的邮件和新闻。系统只需简单地告知消息包含了来自 ISO-8859-1 字符集的 8 位字符文本。

```
Mime-Version: 1.0
Content-Type: text/plain; charset=iso-8859-1
Content-Transfer-Encoding: 8bit
```

如果传输路径不是 8 位纯净的，你可以将特殊字符替换为替换字符或字符序列（这是一种相当过时的方法），或者将其编码交给一个支持 MIME 的¹程序，该程序会以完全对用户透明的方式提供转换。然而，只有当双方都使用支持 MIME 的程序时，此过程才能在没有问题的情况下运行。

MIME 正在迅速成为一种标准，特别是许多 Windows 程序默认创建此类消息。UNIX 下的重要程序也将或少地能够处理 MIME 只是时间问题。

## 9.6.1 邮件阅读器 elm

`elm` 程序是一个简单易用但功能强大的邮件用户代理。首先，elm 必须被正确编译，这在 Slack 分发版中很长一段时间内都没有做对。这允许传入消息中的特殊字符通过内置的分页器（pager）显示。此外，上述头行可以自动包含在发出的邮件中。

```
# elm.rc
# 特殊字符传输
charset = iso-8859-1
displaycharset= iso-8859-1
extencoding = 8bit
pager = builtin
```

然而，elm 也可以与 MIME 实现 metamail 协作，以便也能发送 MIME 消息。

## 9.6.2 邮件和新闻阅读器 pine

邮件和新闻阅读器 pine（Pine Is No longer Elm）是 elm 的进一步开发。Pine 易于使用且支持 MIME。因此，pine 在表示或发送 8 位字符方面没有问题。

## 9.6.3 新闻阅读器 nn

另一个阅读器是程序 nn。`nn` 通过文件 `~/.nn/init` 中的以下条目表示 8 位字符：

```
- data-bits 允许在 nn 中表示8位字符
set data-bits 8
```

## 9.6.4 Emacs/rmail

除了其他功能外，Emacs 编辑器还包含了创建和读取邮件及新闻的模式。邮件模式是 rmail 模式，可以通过直接调用 `Emacs -f rmail` 或在 Emacs 内部使用命令序列 `M-x rmail RET` 启动。

如果 Emacs 配置得当，只要传输路径是 8 位纯净的，8 位字符就可以没有问题地处理。如果不是如此，可以使用 `mime` 模式，它会在发送之前将消息转换为 MIME 格式。此类消息也可以通过 MetaMail 包在 Emacs 下读取。rmail 的一种可能配置见列表 9.11。

在 Info 系统对 rmail 模式的描述中，可以在 rmail 模式的源码 `/usr/lib/emacs/version/lsp/rmail.el` 中找到一系列有用的注释。

```
(set mail-yarn-prefix " >") ; 带有 " >" 的文本
(set mail-signature t) ; 来自 ".signature" 的签名
(set mail-default-headers
Mime-version: 1.0
Content-Type: text/plain; charset=iso-8859-1
Content-Transfer-Encoding: 8bit\n") 使用 ISO-Latin-1
```

列表 9.11 Emacs/rmail 的配置 (~/.emacs)。

| 额外信息与来源 |
|------|
| Info 系统: 新闻组: | Emacs, advanced features, rmail gnu.emacs gnu.emacs.help |
| 软件包: | emacs-20.2.tar.gz |
| ftp 服务器: | ftp.gnu.org |
| ftp 路径: | /pub/gnu |
| 大小: | 约 12 MB |

## 9.6.5 Emacs/gnus

Emacs 不仅提供邮件阅读器，还提供新闻阅读器 gnus，它允许你在 Emacs 环境内读写新闻。通过 ISO-Latin-1 字符集或结合 mime 模式的 MetaMail 包，可以顺利使用 8 位字符。

与 rmail 模式一样，gnus 模式可以从命令行启动也可以从 Emacs 内部启动。最新版本的 gnus 使用该包来显示和创建 MIME 消息。

| 额外信息与来源 |
|------|
| Info 系统: 新闻组: | Emacs, advanced features, gnus gnu.emacs.help gnu.emacs comp.editors |
| 软件包: | emacs-20.2.tar.gz |
| ftp 服务器: | ftp.gnu.org |
| ftp 路径: | /pub/gnu |
| 大小: | 约 12 MB |

## 9.6.7 程序的适配

本节讨论了不属于任何类别的程序的配置。关于此主题的更多信息可以在各种 HowTos 中找到。

## 程序的适配

### 设备无关

### 9.7.1 less 程序

`less` 程序在安装了相应语言文件并设置环境变量 `CHARSET` 为 `latin1` 的情况下，可以没有问题地显示 8 位字符。

| 额外信息与来源 |
|------|
| 手页: | less(1), less(1) |
| 新闻组: | gnu.utils |
| 软件包: | less-257.tar.gz |
| ftp 服务器: | .org |
| ftp 路径: | /pub/gnu |
| 大小: | 150 KB |

### 9.7.2 groff 程序

`groff` 是一个将 nroff 或 troff 格式的文本转换为输出格式的工具。如果你需要外语言字符，必须在命令行选择 `ascii` 或 `latin1`。输出到 A4 纸格式。

#### A4 纸张格式

如果你需要 A4 纸张格式（297 mm x 210 mm），你需要在启动 groff 之前将 `PAGE` 环境变量设置为 A4。如果 `/usr/lib/groff/font/devps` 包含行长度 84190，则输出为 PostScript。DVI 输出格式的设置没有定义，因此需要手动干预。这也适用于许多其他程序。

| 额外信息与来源 |
|------|
| 手页: | groff (1) |
| 新闻组: | | |
| 软件包: | groff-1.09.tar.gz |
| ftp 服务器: | ftp.gnu |
| ftp 路径: | /pub/gnu |
| 大小: | 840 KB |

### 9.7.3 man 程序

`man` 程序用于格式化和显示在线手册的页面（也称为手页）。在 UNIX 传统中，使用了各种工具来实现这一目标。对于外语言手页，需要考虑几个问题：

- 首先，手页是通过 groff 帮助格式化的。因此，对 groff 及其所属包的调用需要如上述进行适配。
- 随后，文本通过 less 或 more 进行显示。

因此，只有当相关程序配置正确时，手页中的特殊字符才能被正确显示。以下信息适用于 `man-1.4`，这是一种使用消息目录处理多种语言并根据 `LANG` 变量的值显示相应手页的程序。`man-db` 管理已安装手页的列表也适用于这些规范。

