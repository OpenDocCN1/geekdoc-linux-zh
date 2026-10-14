
随着 Web 的发展，动态网站和应用程序越来越多，对于 Web 开发者来说，掌握 JavaScript 变得至关重要。有人产生了一个想法：使用同一种语言编写可以在客户端和服务器端运行的应用程序。这样做的基础性是速度。在 Web 上进行开发需要时间。如果你使用多种编程语言，你就必须学习多种语言，或者雇佣熟悉你所用语言的人。此外，随着越来越多的网站变成完全交互的体验，学习 JavaScript 已经成为许多开发者的必然。因此，JavaScript 现在是客户端和服务器端的首语言——它是 MEAN Web 栈的一个重要组件。

你不需要运行 Linux 就可以使用 MEAN 提供服务。你也可以在 Windows 或 macOS 上运行 MEAN 栈。此外，所有相关内容都是用 JavaScript 编写的。数据库使用了 NoSQL 选项之一 MongoDB，它与 MEAN 栈中的 JSON 数据格式配合得非常好。

无论使用什么操作系统，大多数 MEAN 栈都由四个主要部分组成：

- **MongoDB**——第 29 章“NoSQL 数据库”中讨论的 NoSQL 数据库之一，MongoDB 用于以 JSON 格式存储应用程序的数据。
- **Express.js**——这是一个运行在 Node.js 上的后端 Web 应用程序框架。
- **AngularJS**——它们都是 JavaScript MVC（模型-视图-控制器）框架。Angular 是较新的，是 AngularJS 的完全重写，并在过程中进行了刻意的更改。Angular 提供前端 Web 应用程序框架，允许你在用户浏览器中运行代码。
- **Node.js**——Node.js 是一个事件驱动的服务器端应用程序的执行环境。

无论你的操作系统是什么，大多数 MEAN 栈都建议从各自的网站下载并安装组件，而不是使用操作系统提供的包管理器。每个组件的网站列在这里；请按照提供者的说明按顺序下载并安装软件：

1. 从 www.mongodb.com/download-center 安装 MongoDB。
2. 从 https://nodejs.org/en/ 安装 Node.js。安装时，你也会安装 `npm` 包管理器，接下来你将使用它。
3. 使用命令 `npm install express` 安装 Express.js。
4. 遵循 https://angular.io 的入门指南安装 Angular。

MEAN 应用程序与 LAMP 或传统应用程序相比，真正的不同在于灵活性。你可以在服务器上运行应用程序代码。你可以在用户的浏览器中运行代码。你可以在数据库中运行某些应用程序逻辑，这对于某些类型的分析来说特别有用。

> **注意：** 你可以用 React（来自 Facebook）替换 Angular（最初来自 Google），它们的作用相似。你也可以用其他框架（如 Ember.js 或 Backbone.js）替换它，并且仍然使用 JavaScript 进行所有开发工作。有些人喜欢这种灵活性，但对另一些人来说这令人目不暇接。无论如何，MEAN 开发已经存在，并且不太可能短期内消失。

## 参考文献

- https://help.ubuntu.com/lts/serverguide/lamp-overview.html—Ubuntu 服务器指南中的 LAMP
- www.mongodb.com—MongoDB 官方网站
- https://nodejs.org—Node.js 官方网站
- www.npmjs.com—npm 包管理器主页
- https://express.com—Express 官方网站
- https://angular.io—Angular 官方网站
- https://emberjs.com—Ember.js 官方网站
- http://backbonejs.org—Backbone.js 官方网站
- https://reactjs.org—React，一个用于构建用户界面 JavaScript 库

# 第 25 章 Apache Web 服务器管理

## 本章内容

- 关于 Apache Web 服务器
- 安装 Apache 服务器
- 运行时服务器配置设置
- 文件系统验证与访问控制
- Apache 模块
- 虚拟主机
- 日志
- 参考文献

本章涵盖了 Apache Web 服务器的配置和管理，包括服务器一些主要组件的概述，以及对文本和图形服务器配置的讨论。在本章中，你将学习如何使用命令行启动、停止和重启 Apache。本章从一些介绍信息开始，然后教你安装、配置和使用 Apache。

## 关于 Apache Web 服务器

Apache 是今天互联网上使用最广泛的 Web 服务器。Apache 名称出现在软件开发期间因为它是一个“补丁式”（patchy）服务器，由针对免费获取的 NCSA HTTPd Web 服务器源代码的补丁制成。在 NCSA HTTPd 项目停止一段时间后，很多人为代码编写了各种补丁来修复漏洞或添加他们想要的功能。大量代码在流传，人们自由分享，但完全没有经过管理。

一段时间后，Brian Behlendorf 和 Cliff Sokolnick 建立了这些补丁的中央仓库，Apache 项目因此而生。该项目仍然涉及一小部分程序员，但欢迎任何人向小组提交补丁，以便可能包含在代码中。

过去几年，人们对 Apache 项目的兴趣激增，部分源于企业级信息服务对开源的新兴兴趣。这也部分归因于微软 Internet 信息 Services (IIS) 致命的安全漏洞；恶意 Web 任务漏洞的存在；以及由于臭名昭著的 Code Red、Blaster 和 Nimda 蠕虫导致的操作系统和网络漏洞。IBM 早期承诺支持并使用 Apache 作为其 Web 服务的基础，并……

[注：提供的文本似乎包含来自 482-483 页的严重 OCR 损坏/乱码。我已经处理了连贯部分，并尽可能清理了重复的 OCR 伪迹。]

其他选项包括 Apache 的静态模块，或者服务器特殊的、内置的独立部分，以及可以与模块一起使用的选项。这些选项被称为配置指令（configuration directives），是控制静态模块如何运行的命令。请注意，Apache 还包含大量的动态模块，即在服务器运行时可以选择性地加载和使用的服务器软件部分。

`-t` 选项用于检查您的配置。在重启服务器之前运行此命令是一个好主意，特别是当你对配置文件进行了更改时。此类测试是非常重要的，因为配置文件的错误可能会导致服务器在尝试重启时关闭。在 Ubuntu 中，`apache2` 的内部用户名设置存在一个 bug，如果你输入以下内容并运行 `sudo apache2`，你会收到此错误：

```
matthewwsymmour:$ sudo apache2 -t
apache2: bad user name ${APACHE_RUN_USER}
```

如果你遇到这种情况，请输入此命令来强制命令使用预期的用户名设置，你将获得正确的输出：

```
matthewwsymmour:$ sudo APACHE_RUN_USER=www-data APACHE_GROUP=www-data
apache2 -t
```

## 运行时服务器配置设置

此时，Apache 服务器将会运行，但你可能想更改某些行为，例如网站文件的默认位置。本节涵盖了配置服务器以按你想要的方式运行的基础知识。

运行时配置存储在单个文件中——`apache2.conf`，它位于 `/etc/apache2` 目录下。你可以使用此配置文件来控制 Apache 的行为，例如服务器的基础配置目录（`/etc/apache2`）、服务器的 PID 文件名称（`/var/run/apache2.pid`）或其响应超时时间（300 秒）。Apache 在启动（或重启）时会从配置文件中读取数据。

## 运行时配置指令

你通过配置指令对服务器进行运行时配置，这些指令是为 `apache2` 守护进程设置选项的命令。指令用于告诉服务器你想要启用的各种选项，例如对服务器至关重要的文件位置、各种配置和操作。Apache 支持近 300 条配置指令，使用以下语法：

```
directive option...
```

每个指令单独占一行。请参阅后续章节以获取指令的某些示例及其使用方法。指令可能只设置一个值（如文件名），也可能启用指定的各种选项。特殊的指令称为节指令（section directives），类似于 HTML 标签。节指令用角括号包围，例如 `<Directory>`。节指令通常包含一组仅适用于该节中指定目录的指令：

```
<Directory somed/in/your/tree>
directive option option
directive option option
</Directory>
```

节始终用匹配的节标签关闭，其格式如下：`</Directory>`。

请注意，节标签与其他任何指令一样，每行指定一个。

> 提示
