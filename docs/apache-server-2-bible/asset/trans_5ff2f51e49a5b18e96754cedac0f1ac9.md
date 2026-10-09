
服务于该请求。此外，该模块现在还能利用一些仅适用于 Windows 的原生函数调用，这使得它在 Windows 平台上的性能优于早期版本的 Apache 服务器。

## I/O 过滤

Apache 2.0 现在提供了分层 I/O 架构。这意味着一个模块的输出可以成为另一个模块的输入。这种过滤效果非常有趣。例如，由 CGI 脚本生成的输出（由 `mod_cgi` 模块处理）现在可以传递给负责 SSIs 的 `mod_include` 模块。换句话说，CGI 脚本可以生成包含 SSI 标记的输出，这些标记可以在最终输出发送到 Web 浏览器之前进行处理。未来还将出现许多其他 I/O 过滤的应用。

## 新的 CGI 守护进程

由于许多 MPM 模块都使用线程，当线程接收到此类请求时，执行 CGI 脚本会变得更加繁琐。`mod_cgi` 模块仍然可以工作，但对于线程化的 MPM 来说并非最优方案，因此增加了 `mod_cgid`。`mod_cgid` 模块创建一个守护进程，该进程生成 CGI 进程，并与线程更高效地交互。图 1-1 展示了对名为 `myscript.pl` 的脚本的 CGI 请求是如何被处理的。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_39_0.png)

以下是 CGI 脚本的执行方式：

- 当 CGI 请求到达子进程内的线程时，该线程会将请求传递给 CGI 守护进程。
- CGI 守护进程生成 CGI 脚本，并将 CGI 脚本生成的数据输出到子进程中的线程。
- 线程将数据返回给 Web 浏览器。

当主 Apache 服务器启动时，它也会启动 CGI 守护进程并建立套接字连接。因此，当创建一个新的子进程时，它会继承该套接字连接，从而无需为每个请求单独创建到 CGI 守护进程的连接。整个过程改善了线程环境下的 CGI 执行效率。

# Apache 可移植运行时

为了践行 Apache 团队打造世界上最受欢迎的 Web 服务器的愿景，人们认识到 Apache 2.0 需要解决可移植性问题。在本次版本发布之前，Apache 一直在内部处理可移植性问题，这使得代码库难以管理。因此，Apache 团队引入了 Apache 可移植运行时（APR）。APR 的目的是为平台特定的函数提供单一的 C 接口，从而只需编写一次代码。

这使得 Apache 能够更原生地运行在 Windows、BeOS、Amiga 和 OS/2 等平台上。得益于 APR，许多程序（如 ApacheBench）也能在这些平台上运行。

# 理解 Apache 许可证

像 Apache、Perl（实用提取和报告语言）和 Linux（一种基于 x86 的类 Unix 操作系统）这样的免费软件，由于 Netscape 决定通过其 Mozilla 项目免费提供 Netscape Communicator（最受欢迎的 Web 浏览器之一），因此获得了大量媒体关注。不幸的是，像 Apache、Perl 和 Linux 这样的免费软件并不共享相同的许可协议，因此媒体将这些软件包归入同一许可类别造成了一定的混乱。

所有免费软件的初衷都是真正地为所有人免费提供。然而，各个软件许可证存在一些法律限制。例如，Linux 由 GNU 通用公共许可证（GPL）使其免费，该许可证要求对 Linux 所做的任何更改都必须公开。另一方面，Apache 并不要求任何人将所做的更改公开。

简而言之，可以将 Apache 视为由 Apache 团队发布的受版权保护的免费软件。它既不属于公共领域，也不是共享软件。还要注意，Apache 不受 GPL 覆盖。为便于阅读，Apache 软件许可证文件列在列表 1-1 中。

**列表 1-1：Apache 软件许可证**

```
/* ------------------------------------------------------------------ * The Apache Software License, Version 1.1 * Copyright (c) 2000-2001 The Apache Software Foundation. All rights reserved. * Redistribution and use in source and binary forms, with or without * modification, are permitted provided that the following conditions * are met: * 1. Redistributions of source code must retain the above copyright * notice, this list of conditions and the following disclaimer. * 2. Redistributions in binary form must reproduce the above copyright * notice, this list of conditions and the following disclaimer in * the documentation and/or other materials provided with the * distribution. * 3. The end-user documentation included with the redistribution, * if any, must include the following acknowledgment: * "This product includes software developed by the * Apache Software Foundation (http://www.apache.org/)." * Alternately, this acknowledgment may appear in the software itself, * if and wherever such third-party acknowledgments normally appear. * 4. The names "Apache" and "Apache Software Foundation" must * not be used to endorse or promote products derived from this * software without prior written permission. For written * permission, please contact apache@apache.org. * 5. Products derived from this software may not be called "Apache", * nor may "Apache" appear in their name, without prior written * permission of the Apache Software Foundation. * THIS SOFTWARE IS PROVIDED "AS IS" AND ANY EXPRESS OR IMPLIED * WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES * OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE * DISCLAIMED. IN NO EVENT SHALL THE APACHE SOFTWARE FOUNDATION OR * ITS CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, * SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT * LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF * USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND * ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, * OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT * OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF * SUCH DAMAGE. *
 * ------------------------------------------------------- * 
 * This software consists of voluntary contributions made by many 
 * individuals on behalf of the Apache Software Foundation.  For more
 * information on the Apache Software Foundation, please see 
 * <http://www.apache.org/>.
 * 
 * Portions of this software are based upon public domain software 
 * originally written at the National Center for Supercomputing Applications,
 * University of Illinois, Urbana-Champaign.
 */
```

# 获取和安装 Apache

![](img/e11fcbd2818a3495ac70085e5d8d1c26_43_0.png)

# 第 2 章

![](img/e11fcbd2818a3495ac70085e5d8d1c26_43_1.png)

## 本章内容

- 寻找最新的 Apache 源码
- Apache 的系统要求
- 下载软件
- 编译源码
- 在系统上安装二进制文件
- 跟进 Apache 的最新发展

![](img/e11fcbd2818a3495ac70085e5d8d1c26_43_2.png)

虽然编译自己的 Apache 二进制文件可能看起来有些麻烦，但这是值得付出的努力。随着您对 Apache 变得更加熟悉，您会发现它是唯一提供几乎所有（甚至更多）完整商业服务器功能的 Web 服务器，同时它还允许您查看这些功能在源码中是如何实现的。我觉得 Apache 的这一点非常迷人。

然而，对于非 C 程序员但依然需要强大且免费的 Web 服务器的人群来说，处理大量的 ANSI C 代码可能并不是什么爱好。幸运的是，您无需担心——Apache 既有源码版本，也有预编译的二进制包版本。本章将讨论从源码和预编译二进制文件安装 Apache 的方法。

## Apache 的官方来源

每当从互联网获取免费软件（源码或二进制文件）时，请确保您不是从一个未知的 Web 或 FTP 站点获取的。我所说的“未知”可以通过一个例子来更好地理解。假设您想获取由 Sun Microsystems 开发的基于 Java 的免费 Web 浏览器软件。您需要能够进行某种真实性检查，这在互联网上通常比较困难；因此，您应该坚持使用广泛认可的站点。例如，您不希望从一个主机名像 `dialup-666.someforeignisp.net.ch` 这样的 FTP 站点获取它；相反，您最好去 `java.sun.com` 网站上的某个地方寻找，因为您无法确定 `666.someforeignisp.net.ch` 是否已彻底检查该软件是否存在任何隐藏危险。您明白我的意思了。

