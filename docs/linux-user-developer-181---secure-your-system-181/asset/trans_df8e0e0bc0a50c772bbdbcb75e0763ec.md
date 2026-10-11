
## 所展示的应用程序将在 Web 浏览器中使用独立的 URL 显示 UNIX 纪元时间

```html
[{<<"content-type">>, <<"text/plain">>}]
<<<<"Hello World and Cowboy!">> ,Req),
(ok, Req2, State).
```

如您所见，这是您定义 /URL 将显示消息的位置。执行 **make** 命令并运行下一条命令：

```bash
$ ./rel/hw_release/bin/hw_release console
```

请注意，可执行文件的完整路径和名称基于项目名称，因此如果您给项目起了不同的名字，您应相应地调整之前的命令。

现在访问 [http://127.0.0.1:1200/](http://127.0.0.1:1200/) 以查看 Web 应用程序的运行效果，或者使用 wget 查看 index.html 文件的内容，它应该是 'Hello World and Cowboy!'。下一节将创建一个支持两个不同 URL 的应用程序，请继续阅读！

## 创建一个简单的 Web 应用程序

所展示的应用程序将在 Web 浏览器中使用独立的 URL 显示 UNIX 纪元时间——该应用程序总共将支持两个 URL，以及第三个捕获其他所有请求的额外 URL。

就像之前那样，您需要创建一个使用 Cowboy 的新 Erlang 项目——项目名称将是 epoch，因此请继续执行 **mkdir epoch**  shell 命令来创建项目的 *root* 目录。

现在，创建一个与前一节中项目类似的项目，然后再继续。如果您遇到困难，请仔细阅读前一节。

因此，在拥有一个仅支持一个 URL 的项目之后，是时候开始修改 epoch 项目的文件了。但是，在此之前，请执行 **make distclean** 以清理任何不必要的文件，并确保 epoch Web 应用程序使用端口号 1300。

![](img/fb76008333fb7aef815b136f9f1afe5f_52_0.png)

**图注** epoch_handler.erl 模块的 Erlang 代码——其最重要的功能是 **handle()** 函数，它允许您在本地机器的浏览器中显示 UNIX 纪元时间。该项目最有趣的部分是定义将由 Cowboy 处理的不同路由的位置：

```erlang
Routes = [[{'_',
    [
        ['/',  root_handler,  []],
        ['epoch', epoch_handler, []],
        ['_', cowboy_static, {priv_file,
        "static/error.html"}]
    }] ]
```

在定义 **Routes** 变量后，您应该编写 **Dispatch = cowboy_router:compile(Routes)** 语句，以便 Cowboy 实际激活这些路由。请注意，路由开头的 '_' 表示 Web 应用程序在任何主机上都能正常工作。第一个路由将捕获 / URL，并且只会显示一条文本消息。第二个路由捕获 **/epoch** URL，并以 UNIX 纪元格式返回当前时间。每次刷新页面时，输出都会更新。最后一个路由将捕获所有不匹配之前任何规则的 URL，它是一个静态规则，在浏览器中显示包含错误信息的 HTML 网页——最后一个路由不需要实现 handler，因为它使用 Cowboy 定义的 **cowboy_static** handler。这里，您只需告诉 Cowboy 在哪里找到您想要显示的 HTML 页面即可。请别忘了创建 **error.html** 页面并将其放入 */priv/static* 目录中；为另外两个路由创建两个模块并实现它们——在这种情况下，这两个规则的实现可以在位于 **src** 目录中的 **root_handler.erl** 和 **epoch_handler.erl** 文件中找到。**root_handler.erl** 实现的 Erlang 代码与前一节中您看到的 **hw_handler.erl** 文件中的 Erlang 代码类似。

图 4 展示了返回 UNIX 纪元时间的 Erlang 函数的实现，该实现可以在 **epoch_handler.erl** 中找到，以及该模块的其余代码。这是一个令人兴奋的 Erlang 函数，原因有很多。第一个原因是，为了在 Erlang 中计算 UNIX 纪元时间，您需要调用 `erlang:timestamp()` 并使用返回的三个值中的前两个来计算 UNIX 纪元时间并将其保存到 `Epoch_time` 变量中。

然后，您构建要发送给 Cowboy `req:reply()` 函数的字符串，并将其存储到 `TextToSend` 变量中。

虽然您在本教程中看到的应用程序是最终版本，但不要试图一次性实现所有内容，因为您的代码很可能包含各种类型的错误——良好的做法是为每个路由创建一个 dummy 函数，该函数将打印一条消息，以确保您的项目路由配置正确，然后开始逐个实现和测试路由。

图 5 展示了 `./src/root_handler.erl` 文件的 Erlang 代码，这应该不会让您感到惊讶。

> “您不需要访问所有目录或编辑包含的每个文件：Erlang.mk 会自动生成其中大多数。”

handler.erl 文件，这应该不会让您感到惊讶。图 6 展示了三个从浏览器访问 Web 应用程序时的输出截图，但您仍然可以使用 wget 和 curl 等命令行工具来测试 Web 应用程序。本教程的引导图片（见第 50 页）展示了 epoch 项目的完整目录结构，但未包含项目文件，以便更好地理解项目背后的复杂性，这些复杂性被隐藏起来以使您的生活更轻松。好事是您不需要访问所有目录或编辑包含的每个文件，因为 Erlang.mk 会自动生成其中大多数。

## 为什么 Web 应用程序很重要？

Web 应用程序很重要，因为它们消耗了大部分互联网流量。这意味着它们必须被开发得 *快速*、*健壮*、*容错* 且 *能够扩展*。虽然 Erlang 符合所有这些要求，但它并不经常被用于创建 Web 应用程序，主要是因为 Web 开发人员不了解 Erlang 和一般的函数式编程。

网站性能越好，访问者越满意，这意味着 Web 应用程序很重要，并且应该仔细开发。此外，良好的 Web 应用程序将需要更少的硬件升级和更少的维护。

最后但同样重要的是，如果您是一位能够创建此类行为良好的应用程序的开发人员，您总是有事可做，并且更容易选择开发您最感兴趣的内容！因此，*行为良好的 Web 应用程序* 将使整个互联网流量更快、更安全。这意味着，如果一家公司的网站使用良好的 Web 应用程序，该公司的网络存在性将更好，更多的访问者将留在其网站上。

## Yawls Web 服务器

Yawls 是另一个特别擅长提供动态内容 Web 应用程序的 Web 服务器。由于它是用 Erlang 编写的，Yawls 在设计上是多线程的，可以非常高效地并发工作。

Yawls 有两种工作模式：*常规* 模式，它作为常规 Web 服务器运行；以及 *嵌入式* 模式，它可以在 Erlang 应用程序中运行。您可以在 [http://yawls.hyber.org/](http://yawls.hyber.org/) 上找到有关 Yawls 的更多信息。

### 关于 MochiWeb

MochiWeb 是一个允许您创建轻量级 HTTP 服务器的 Erlang 库。虽然 Cowboy 比 MochiWeb 更强大，但有时您可能需要更轻量的东西，并考虑使用 MochiWeb。因此，在下一节中，您将学习如何配置 MochiWeb 以提供简单的网页。

您可以通过在 Linux 终端中执行以下命令获取 MochiWeb：

```bash
$ git clone git://github.com/mochi/mochiweb.git
cd mochiweb
Cloning into 'mochiweb'...
remote: Counting objects: 2632, done.
remote: Total 2632 (delta 0), reused 0 (delta 0), pack-reused 2632
Receiving objects: 100% (2632/2632), 1.28 MiB | 603.00 KiB/s, done.
Resolving deltas: 100% (1681/1681), done.
```

![](img/fb76008333fb7aef815b136f9f1afe5f_53_0.png)

**图注** 处理所有 /URL 请求的 root_handler.erl 模块的 Erlang 代码

现在您可以自由使用 MochiWeb！

### 提供 'Hello World!' 页面

本节将展示如何编程 MochiWeb 以提供 'Hello World!' 页面。这个简单的例子将帮助您更好地理解 MochiWeb 的工作原理。您可以通过在 mochiweb 目录内部执行以下命令创建一个名为 hwmochi 的新项目：

```bash
$ make app PROJECT=hwmochi
```

然后，您需要通过执行 cd ./hwmochi 命令进入位于 mochiweb 目录外部的 hwmochi 目录。

![](img/fb76008333fb7aef815b136f9f1afe5f_53_1.png)

**图注** epoch Web 应用程序的三种可能输出——每一种代表开发人员应定义和实现的不同的 Cowboy 路由

