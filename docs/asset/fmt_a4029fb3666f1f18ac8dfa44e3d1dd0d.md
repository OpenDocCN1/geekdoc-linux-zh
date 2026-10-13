
`sendmail-doc` 软件包会在你系统的 `/usr/share/sendmail` 目录下安装多个文档文件。你可以在 PostScript 文件 `/usr/doc/sendmail/doc/op/op-ps` 中找到《Sendmail 安装与操作指南》。运行 ghostview 时，选择 Main Menu:Graphics:More Graphics Applications:PDF Viewer，然后打开该文件。

现在你已经处理好了准备工作，可以学习如何重新生成 `sendmail.cf` 文件了。

## 使用 M4 宏处理器

`m4` 宏处理器用于用于生成 `sendmail.cf` 配置文件，该文件随 Red Hat Linux 中的 `sendmail` 包一起。主宏文件 `sendmail.mc` 包含在 `sendmail` 包中，但该文件需要 `sendmail-cf` 包中的其他 m4 宏。为了处理 `sendmail.mc` 文件，你需要如上一节所示安装 `sendmail-cf` 软件包。本节将向你介绍 m4 宏处理器。

宏是某些操作或长字符字符串的符号化名称。像 `m4` 这样的宏处理器通常读取其输入文件并将其复制到输出，在此过程中处理宏。宏的处理通常涉及执行某些操作并生成某些输出。由于宏在输出中生成的文本比宏本身本身多得多，因此宏的处理是——

`m4` 宏处理器是 UNIX 宏处理器的 GNU 实现。本节仅描述了几个简单的 m4 宏，但 `m4` 的功能比这里展示的简单示例多得多。它本质上是一种用于生成配置文件的脚本语言。你可以在 shell 提示符下输入命令 `info m4` 来阅读关于 m4 的在线手册。第 23 节描述了如何使用 `info` 读取在线帮助。

> 注意 `m4` 是基于流的（类似于第 8 节描述的 `sed` 编辑器）。它将输入字符复制到输出，并展开任何宏。`m4` 宏处理器没有行的概念，因此它会在输出中创建换行符。这就是为什么你在大多数 m4 宏文件中看到 `dnl` 这个词；`dnl` 是一个代表“删除换行”的 m4 宏。`dnl` 宏删除从 `dnl` 开始到下一个换行符的所有字符。输出中的换行符不会造成危害；它们只是创建了不必要的空行。`sendmail` 宏包使用 `dnl` 来避免配置文件中出现此类空行。由于 `dnl` 基本上删除了行尾之前的所有内容，m4 宏文件还使用 `dnl` 作为注释行的前缀。

为了查看 m4 的用法，请考虑以下 m4 宏文件，它定义了两个宏——`hello` 和 `bye`，并在格式信中使用它们：

```
dnl

# File: ex.m4

dnl

# m4 宏的简单示例

dnl

define('hello', 'Dear Sir/Madam')dnl

define('bye').

dnl-Sincerely,

Customer Service'*dnl

dnl Now type the letter and use the macros

hello.

This is to inform you that we received your recent inquiry.

We will respond to your question soon.

bye
```

使用你喜欢的文本编辑器输入这段文本，并将其保存为名为 `.m4` 的文件。你可以为宏文件命名任何名称，但习惯上使用 `.m4` 扩展表示 m4 文件。

在使用 m4 处理宏文件之前，请注意上述示例说明的以下关键点：

- 使用 `dnl` 宏开始所有注释行（例如示例中的前四行）。
- 用 `dnl` 宏结束每个宏定义。否则，当 `m4` 处理文件时，会为每个宏定义产生一个空行。
- 使用内置命令 `define` 定义一个新宏。宏名和值都括在一对左右单引号（`''`）之间。注意，你不能使用普通引号来包围宏名和定义。

现在使用 m4 处理宏文件 `ex.m4`：

```
m4 ex.m4
```

Dear Sir/Madam,This is to inform you that we received your recent inquiry.
We will respond to your question soon.

Sincerely,
Customer Service

如果你想将输出重定向到名为 `letter` 的文件，可以使用：

```
m4 ex.m4 > letter
```

Dear Sir/Madam,This is to inform you that we received your recent inquiry.

We will respond to your question soon.

Sincerely,

Customer Service

使用你喜欢的文本编辑器输入这段文本，并将其保存为文件 `letter`.

This is to inform you that we received your recent inquiry.
We will respond to your question soon.

Sincerely,
Customer Service

如果你想在不展开宏的情况下使用 `hello` 或 `bye`，可以这样做：

```
m4 -s ex.m4
```

hello.This is to inform you that we received your recent inquiry.

We will respond to your question soon.

bye.Sincerely,

Customer Service

`sendmail` 宏包使用 `dnl` 来避免配置文件中出现此类空行。由于 `dnl` 基本上删除了行尾之前的所有内容，m4 宏文件还使用 `dnl` 作为注释行的前缀。`sendmail-cf` 软件包在 `/usr/share/sendmail-cf` 目录下安装生成新 sendmail 配置文件所需的所有文件。正如你在接下来的节中学学到的，`sendmail.cf` 文件是由许多 m4 宏文件生成的。这些宏文件组织在 `/usr/share/sendmail-cf/` 下的若干子目录中。你可以读取 `/usr/share/sendmail-cf` 中的 `README` 来了解更多关于创建 sendmail 配置文件的信息。

当你准备好后，也可以从 `sendmail-doc` 软件包安装 sendmail 文档。使用以下命令安装该 RPM：

```
rpm -ivh sendmail-doc*
```

`sendmail-doc` 软件包会在你系统的 `/usr/share/sendmail` 目录下安装多个文档文件。你可以在 PostScript 文件 `/usr/doc/sendmail/doc/op/op-ps` 中找到《Sendmail 安装与操作指南》。运行 ghostview 时，选择 Main Menu:Graphics:More Graphics Applications:PDF Viewer，然后打开该文件 `/usr/share/sendmail/doc/op/op-ps`。

现在你已经处理好了准备工作，可以学习如何重新生成 `sendmail.cf` 文件。

## 使用 M4 宏处理器

`m4` 宏处理器用于生成 `sendmail.cf` 配置文件，该文件随 Red Hat Linux 中的 `sendmail` 包一起。主宏文件 `sendmail.mc` 包含在 `sendmail` 包中，但该文件需要 `sendmail-cf` 包中的其他 m4 宏。为了处理 `sendmail.mc` 文件，你需要如上一节所示安装 `sendmail-cf` 软件包。本节将向你介绍 m4 宏处理器。

宏是某些操作或长字符字符串的符号化名称。像 `m4` 这样的宏处理器通常读取其输入文件并将其复制到输出，在此过程中处理宏。宏的处理通常涉及执行某些操作并生成某些输出。由于宏在输出中生成的文本比宏本身多得多，因此宏的处理是——

`m4` 宏处理器是 UNIX 宏处理器的 GNU 实现。本节仅描述了几个简单的 m4 宏，但 `m4` 的功能比这里展示的简单示例多得多。它本质上是一种用于生成配置文件的脚本语言。你可以在 shell 提示符下输入命令 `info m4` 来阅读关于 m4 的在线手册。第 23 节描述了如何使用 `info` 读取在线帮助。
