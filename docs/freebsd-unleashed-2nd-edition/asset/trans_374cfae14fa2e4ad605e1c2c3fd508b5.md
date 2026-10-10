

## 第三方模块

Apache 模块化架构的真正威力体现在第三方模块上。这些模块在运行时与其他可用的 Apache 模块链接，提供额外的功能和配置指令——通常是为了让 Apache 能够更高效地处理特定类型的服务器端内容。其中一个流行的模块是 *mod_perl*，它将 Perl 解释器嵌入到 Apache 中，通过消除 Apache 启动子进程并在其中执行 CGI 程序的需要，极大地加速了 Perl CGI 脚本的执行（关于 *mod_perl* 的更多知识，我们将在本章稍后的小节中介绍）。另一个是 *mod_php4*，这是一个让 Apache 能够解析和提供动态 PHP 页面的模块（即微软 ASP 技术在 Unix 中的对应物）。在 */usr/ports/www* 的 ports 集合中，有超过 50 个可用的第三方 Apache 模块；它们都是以 *mod_* 开头的模块。

### 使用 apxs 构建模块

在早期开发第一批第三方模块时，当时动态共享对象（DSO）支持充其量只是实验性的，编译第三方模块意味着手头必须有 Apache 源代码，调整 Apache 源代码和模块源代码中的构建配置文件，并将它们交叉编译成单一的混合二进制文件。虽然在技术上这是一种“模块化”方法（也就是说，这比手动将代码修补到 Apache 源代码本身要好），但它仍然并不容易被大家视为易于处理。每次 Apache 或模块的新版本可用时，仍然需要构建新的可执行文件，并且仍然需要大量的代码修改才能使其正常工作。

*apxs*，即 Apache 扩展工具应运而生。这个位于 */usr/local/sbin* 的支持程序与 Apache 一起构建，利用已编译二进制文件的 DSO 支持（即静态编译的 *mod_so* 模块），提供一个独立的构建框架，该框架完全了解你的 httpd 二进制文件的所有功能。你不再需要保留 Apache 源代码来构建第三方模块；*apxs* 将原始源代码形式或已编译对象中的模块编译并转换为 *.so* 对象，这些对象可以与其余部分一起通过 `LoadModule` 指令加载到 Apache 中。

你很可能永远不需要直接调用 *apxs*；它是 ports 集合中构建工具透明使用的一种编译时工具。就像其他 ports 一样，构建第三方模块所要做的只是进入模块在 */usr/ports/www* 中的目录并输入 *make*。*apxs* 会处理其余的工作。如果发布了 Apache 的新版本，它可以单独构建和安装，而第三方模块将继续工作。同样，如果模块被更新，你只需重新构建并重新安装即可。这是模块化设计的最佳体现。

如果你感兴趣，关于 *apxs* 的更多信息可以在 *man apxs* 页中找到。

#### mod_perl

最受欢迎的第三方模块之一是 mod_perl。虽然 Perl 仍然是 CGI 编程最流行的选择（我们将很快讨论），但执行 Perl 脚本对 Apache 来说意味着相当大的开销。当发出针对 Perl CGI 程序的 HTTP 请求时，Apache 必须启动一个 shell 进程并在其中运行脚本，将结果反馈给客户端。

使用 mod_perl 后，Perl 解释器直接内置于 Apache 中。专用指令将某些文件类型定义为 Apache 可以自己执行的 Perl 脚本；此外，Apache 执行的每个 Perl 脚本都会以编译后的形式保存在内存中以便后续使用。这消除了通常与 CGI 执行相关的启动开销，使服务器端程序的响应速度大大提高。

关于 mod_perl 的更多信息可在 http://perl.apache.org 获取。

#### mod_python

随着 Python 作为 Perl 王位的潜在继承者崛起，成为未来首选的服务器端编程语言，mod_python 为 Apache 带来的 Python 益处与 mod_perl 为 Perl 带来的益处类似。Python 解释器直接提供给 Apache 可执行文件，允许 Apache 运行 Python 程序，而没有通过 CGI 执行所带来的任何开销。

mod_python 的首页位于 www.modpython.org。

#### mod_php

PHP，Unix 上广泛流行的动态页面生成工具，通过 mod_php3 和 mod_php4 模块成为 Apache 的一部分。此模块族启用的指令让 Apache 能够完全本地地提供 .php 文件，执行其嵌入式脚本功能以在将页面最终形式发送到客户端之前生成该形式。当你构建并安装 mod_php4 时，你的 httpd.conf 文件会自动更新，以提供对 .php 和 .phps 文件类型的支持。

关于 PHP 和 mod_php4 的更多信息可在 www.php.net 找到。

还有更多可用的模块，为 Apache 提供了足够扩展的功能，让你忙忙碌碌很长一段时间。Apache 的模块化直到最近才完全确立，而标准化第三方模块的广泛可用性，加上 FreeBSD ports 集合，开启了可扩展 HTTP 服务器管理前所未有的新时代。

## 服务器端包含

Apache 的一个流行功能是处理*服务器端包含*（Server-Side Includes），这些是嵌入到普通 HTML 文件中并在发送到浏览器之前由 Apache 处理的内部 Apache 函数调用。服务器端包含让你能够完成从简单地将环境变量回显到页面，到每次请求页面时导入模块化 HTML 片段或执行服务器端程序等各种操作。

服务器端包含嵌入在所谓的*解析 HTML*（parsed HTML）中，这实际上只是当页面被请求时由 Apache 解析的普通 HTML。Apache 在解析 HTML 中搜索服务器端包含，并在将它们转发给客户端之前依次处理每一个。每个包含具有以下形式：

```
<!--#command attribute=value attribute=value ... -->
```

> **注意**
> 
> 服务器端包含语句的语法至关重要；它必须严格遵循此处所示的形式。起始字符串 `<!--#command` 不能包含空格；否则，Apache 会将该指令视为 HTML 注释并忽略它。
> 
> 你可以使用浏览器的“查看源代码”功能来检查是否有格式错误的服务器端包含语句被 Apache 忽略并原样传递到了浏览器。

在这个通用示例中，`command` 可以是 `include`、`exec`、`config`、`echo` 或几种其他可能性。`attribute=value` 对是设置或读取变量的方式，你可以使用包含自行设置，或从可用的环境变量中读取。

首先，要在 Apache 中启用服务器端包含，请取消 `httpd.conf` 中以下两行的注释（或将其添加到适当的 `.htaccess` 文件中）：

```
AddType text/html .shtml
AddHandler server-parsed .shtml
```

请注意，这些行可能出现在 `httpd.conf` 文件的不同部分。确保它们都出现在同一个“容器”（`<Directory>` 或 `<Location>`）中。这可能很难判断，因为某些容器包含大量注释块和额外文本，这可能使结构变得混乱。

> **说明**
> 
> 在 Apache 2.0 中，`AddHandler` 指令被分离为多个更具体任务的指令；此示例中的第二行变为 `AddOutputFilter` 指令：
> 
> `AddOutputFilter INCLUDES .shtml`

> **提示**
> 
> `.shtml` 扩展名是服务器解析 HTML 文件的广泛接受的 Unix 标准；但是，还有其他变体，例如 `.shtm` 和 `.stm`。若要同时启用这些扩展名以及 `.shtml`，请复制此处显示的指令行并相应地修改副本：
> 
> ```
> AddType text/html .shtml
> AddHandler server-parsed .shtml
> AddType text/html .shtm
> AddHandler server-parsed .shtm
> ```

