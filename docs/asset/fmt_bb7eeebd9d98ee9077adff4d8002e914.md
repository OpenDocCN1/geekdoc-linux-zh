
`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

`/lib/libc.so.6` undefined reference to `_dl_runtime_object`

... (remaining 700 lines)

# 第3章 软件配置管理

除了钩子（hook）之外，Netscape（或 Mozilla）还指派了一名“sheriff”（治安官）来监控 Tinderbox 监控第一级平台的整体状态，并确保构建保持“绿色”（即通过测试）。我们最终将担任“sheriff”的责任在各个开发团队之间进行了轮换：某天责任可能落在邮件新闻团队成员身上，另一天则由 IM（即时消息）团队负责，以此类推。一旦出现问题，sheriff 有权关闭所有提交（check-ins）（这通过 Tinderbox 页面顶部的简单消息进行通知），这样做是为了帮助那些正在隔离问题原因的人。sheriff 还有权联系钩子上的任何人，通常通过电子邮件，必要时则通过电话，如果对问题的诊断结果表明被联系的人对代码树变“红”（即构建失败）负有责任。作为 sheriff，我记得曾多次通过电话催促那些让代码树持续“燃烧”并回家过夜的人。并不是所有人都对这项政策感到满意，但它确实让人们在工作时更加谨慎。

简而言之，Tinderbox 在跨平台开发中发挥着重要作用，因为它迫使开发者面对影响提交到仓库的代码可移植性的问题。尽管开发者会尝试在其他平台上提交更改并将代码存入树中，但这并非总是能做到。Tinderbox 像一个后座视角，确保没有任何细节遗漏。当检测到问题时（无论是因为树变红还是第二天 QA 测试失败），可以使用 Tinderbox 作为辅助工具，来确定哪些更改可能是问题的根源。

当然，在所有平台上获得“绿色”构建并不是故事的结束。例如，绿色构建并不能确保该平台实现了跨平台的功能对等。开发者可能实现一个跨平台功能，并为 Mac OS X 提交了完整的实现，而只为 Linux 和 Windows 留了存根实现（stub），Tinderbox 不会指出这一点。Tinderbox 很好地确保平台间共享的代码在处处都能构建，并且没有任何平台可以劫持代码树的稳定性（即让仓库处于一种只有部分支持的平台可以进行清洁构建的状态）。因此，Tinderbox 有助于确保在同时开发多个平台时，跨平台开发列对所有相关平台以相同的速度运行。这有助于确保组织能够在同一时间为所有支持的平台发布产品，这是我们在 Netscape 时追求的目标。然而请记住，Tinderbox 只是一个辅助工具——只有通过仔细测试生成的构建，才能确认产品或功能已实现跨平台对等。

## 第 13 项：使用 CVS 或 Subversion 管理源代码

SCM（软件配置管理）系统的作用正如其名称所示；它帮助你管理源代码和相关资源。为了理解 SCM 的重要性，请思考一下没有它的生活将会是什么样。假设你是一个正在开发新项的开发者，该项目将包含 C++ 源代码文件、一个 Makefile，可能还有一些如图标或图像之类的资源。显然，这些项目必须存在于某处，因此在项目的第一天，你会在本地桌面系统上创建一个目录存放这些文件，并编写几行代码，将结果存储在该目录中。经过几周的黑客式开发（hacking），你创作出了该作品的 0.1 版本，在经过轻度测试后，你决定你的作品已经准备好发布到网上，希望从一小部分社区中获得一些用户反馈。

几周后，你的邮箱积压了来自用户的若干项功能请求，可能还有十几条报告（此外由于你向公众公布了电子邮件，还收到了一堆垃圾邮件）。你忙于实现其中的一些功能并修复最糟糕的漏洞，几几周后，你准备好发布 0.2 版本。这个过程重复了几个月，在你意识到之前，你已经将版本发给了更广泛的受众。

在没有 SCM 系统的情况下，随着版本的推移，当 1.0 版本发布时，问题开始显现。由于没有使用版本控制管理系统，你发布了 1.0 的版本，但并非没有问题。首先，用户开始报告一个糟糕的 bug。如果开发者使用了版本控制管理系统，他可以获取 0.9 版本的源代码，并定位哪些更改导致了 bug 的出现。为了尝试理解问题，你反复查看代码，但在几个小时后你发现并不知道哪些更改导致了 bug。通过源代码管理系统，你唯一的方法是确定哪些更改导致了问题。你面临的第二个问题是请求。事实证明你从 1.0 版本中删除了一个功能，这让很多用户感到愤怒，他们要求将该功能恢复到 1.1 版本中。然而，该代码从很久以前就从源代码中删除了。

# 项目 13：使用 CVS 或 Subversion 管理源代码

通过仅存储更改，你可以轻松检索存储在仓库中的文件的早期版本。更改的日期、执行更改的开发人员名称或 ID，以及开发者随更改一起提供的任何注释，都存储在仓库中。这对开发者问责制的影响是显而易见的；在任何时候，你都可以查询源码管理系统获取更改日志，了解更改何时发生以及由谁执行。这对于定位 bug 的来源以及可能导致这些 bug 的非常有帮助。

将仓库中的更改归因于特定开发者、bug 或功能的能力，直接取决于开发者对项目执行的提交（check-ins）粒度。对仓库进行频繁、微小的更改将增加开发者使用源码控制管理系统识别和隔离更改的能力，并将有助于确保项目中的其他开发者能够及时获取最新更改。一个好的经验是，将每次提交到仓库的更改所修复的 bug 数量限制为一个（除非同一个更改修复了多个相关的 bug）。

由于跨平台可用性和通用用户界面是基本要求，在我写这本书的此时，我看到的 SCM（源码控制管理）系统只有两个选择：CVS 和 SVN。在 Netscape 以及无数其他地方（无论是否开源），CVS 是首选的 SCM。它经受了时间的考验，并且非常强大。它被移植到了几乎任何地方，其用户界面基于命令行。SVN 是 CVS 的一个非常接近的兄弟。在专业项目中使用 SVN 后，我得出的结论是，使用它的 的程序员在处理方法和提供的命令方面与使用 CVS 非常相似，因此任哪一个都是很好的选择。（不过，该 SCM 并非没有自己的怪癖）。在本书中，当我提到 SCM 时，我指的是 CVS，但我也可以很容易地对 SVN 说同样的话。

除了为 Tinderbox 提供拉取源码的位置（见项目 12）以及对 Windows、Mac OS X 和 Linux 的支持外，CVS 对跨平台开发最重要的贡献可能是它创建 diff（或补丁 patch）文件的能力。补丁文件对跨平台开发的影响在项目 14 中详细介绍；在接下来的段落中，我将描述什么是补丁文件，以及如何使用 CVS 创建补丁文件。

diff 或补丁是通过通过执行 `cvs diff` 命令创建的。例如，假设我在 Mozilla 源码树中名为 `nsLabel.h` 的文件中添加了一个方法 `GetAlignment()`。通过输入 `diff`，我可以很容易地识别出我修改的行：

```diff
$ diff
cvs server: Diffing =
Index: nsLabel.h
=============================================
RCS file: /cvroot/mozilla/widget/src/nsLabel.h
retrieving version 1.21
diff -r1.21 nsLabel.h
61a62
> NS_IMETHOD GetAlignment(nsLabelAlignment *aAlignment);
71d71
< GtkJustification GetAlignment();
```

前面的输出告诉我们，`nsLabel.h` 文件的第 61 行附近添加了一行，在第 71 行附近删除了一行。我可以将此输出通过邮件发送给团队中的其他人，并要求他们在提交更改之前对其进行错误检查或提供意见。我还可以查看此补丁，并确保它只包含了我想要提交到仓库的更改。我无法强调 `cvs diff` 作为在在提交前识别无意提交的工具有多么重要。

当更改非常多时，这里显示的默认输出格式很难理解。更好的输出应该显示上下文行，并让哪些行被添加到源文件中、哪些行被删除变得更加明显。`diff` 的 `-u` 参数会导致它生成“统一”的，如下如下：

```diff
$ cvs diff -u
cvs server: Diffing
Index: nslabel.h
=================================================================
RCS file: /cvroot/mozilla/widget/src/gtk/nsLabel.h,v
retrieving revision 1.21
diff -u -r1.21 nslabel.h
--- nslabel.h 28 Sep 2001 20:11:17 -0000 1.21
+++ nslabel.h 1 Feb 2004 02:47:21 -0000
@@ -59,6 +59,7 @@
NS_IMETHOD SetLabel(const nsString &aText);
NS_IMETHOD GetLabel(nsString &aBuffer);
NS_IMETHOD SetAlignment(nsLabelAlignment aAlignment);
+ NS_IMETHOD GetAlignment(nsLabelAlignment *aAlignment);
 NS_IMETHOD PreCreateWidget(nsWidgetData *aInitData)
@@ -68,7 +69,6 @@
protected:
NS_METHOD CreateNative(GtkObject *parentWindow);
GtkJustification GetNativeAlignment();
nsLabelAlignment mAlignment;
```

输出中的区别在于包含了受影响行后的后的行，并使用 `+` 和 `-` 分别指示从源文件中添加或删除的行。这种格式对于所有必须阅读补丁的人来说通常容易得多，这也是我推荐的格式。要通过附加 `-u` 来更改 CVS 生成的上下文数量，可以执行以下命令：

```diff
$ cvs diff -u
cvs server: Diffing
Index: nslabel.h
================================================================
RCS file: /cvroot/mozilla/widget/src/nsLabel.h,v
retrieving version 1.21
diff -u -r1.21 nslabel.h
--- nslabel.h 28 Sep 2001 20:11:17 -0000 1.21
+++ nslabel.h 1 Feb 2004 02:47:21 -0000
@@ -59,6 +59,7 @@
NS_IMETHOD SetLabel(const nsString &aText);
NS_IMETHOD GetLabel(nsString &aBuffer);
NS_IMETHOD SetAlignment(nsLabelAlignment aAlignment);
+ NS_IMETHOD GetAlignment(nsLabelAlignment *aAlignment);
 NS_IMETHOD PreCreateWidget(nsWidgetData *aInitData)
@@ -68,7 +69,6 @@
protected:
NS_METHOD CreateNative(GtkObject *parentWindow);
GtkJustification GetNativeAlignment();
nsLabelAlignment mAlignment;
```

### 设置与使用 CVS

为了启动 CVS 服务，你需要从 `http://ftp.gnu.org/gnu/cvs/source/stable/` 下载 CVS 的源码。在解包文件后，进入根目录（在我的情况下是 `cvs-1.22`），并输入以下命令进行构建和安装：

```bash
$ ./configure
$ make
$ install
```

接下来仍然以 root 身份登录，你需要执行一些工作以便服务器每次重启时都执行。第一步是检查 `/etc/services` 中是否存在如下条目：

```text
cvpserver 2401/tcp    # CVS client/server operations
cvpserver 2401/udp    # CVS client/server operations
```

如果这些行不存在，请按所示添加到 `/etc/services`。接下来，你需要在 `/etc/xinetd.d` 中创建一个名为 `cvpserver` 的文件，内容如下：

```
cvpserver
socket_type = stream
protocol = tcp
wait = no
user = root
passenv = PATH
server = /usr/bin/cvs
server_args = -f --allow-root=/usr/cvroot pserver
```

确保该文件的权限为 `-rw-r---`，所有者为 root。这可能是默认设置，但检查一下没坏。

如果你还没有运行桌面图形界面 (GUI)，启动它，并从 Red Hat 开始菜单选择系统设置、用户和组来启动 Red Hat 用户管理器。

在显示的对话框中，点击“添加组”按钮并添加名为 `cvsadmin` 的组。接下来，点击“添加用户”按钮，添加名为 `cvsuser` 的用户。系统会要求你提供密码；输入一个你能记住的密码，完成后退出 Red Hat 用户管理器。

回到终端，仍然以 root 身份，执行以下命令：

```bash
# cd /usr
mkdir cvsroot
chmod 775 cvsroot
chown cvsuser cvsroot
chgrp cvsadmin cvsroot
```
