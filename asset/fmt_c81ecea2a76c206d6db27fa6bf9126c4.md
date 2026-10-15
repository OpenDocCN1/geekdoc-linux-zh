
## 总结

共享内存是可用的最快的进程间通信（IPC），优于所有其他 IPC 机制。然而，使用系统调用来创建和操作共享内存是非常复杂的。将共享内存功能开发并封装到类中可以得到像本章所示易于使用的类。
在进程之间协调共享内存的使用需要像互斥锁（`mutex`）这样的同步对象。在第18章互斥锁类功能的基础上，创建了一个新类来处理多个进程带来的额外需求。在构建新的互斥锁类之后，共享内存类添加了互斥锁属性以同步访问。
到此，Linux 高级开发章节结束。通过使用本章以及前三个章节中描述的信息和示例，开发者可以创建极其复杂的 Kylix 应用，充分利用 Linux 某些最强大的操作系统特性。

## 第 6 章

## Kylix 2 开发

## 企业级应用

第 21 章—互联网应用 — NetCLX
第 22 章—WebSnap 简介
第 23 章—高级 WebSnap
第 24 章—Web 服务
第 25 章—使用 VisiBroker 4.5 进行 Kylix CORBA 开发

## 互联网应用 — NetCLX

### 简介

使用 Kylix 最有趣的方面之一是设计者将看似复杂的内容抽象为一个名为 `WebBroker` 的易于使用的框架。在查看 Kylix 如何让互联网应用的开发变得快速、简单且强大时，这一点尤为明显。

创建这些应用程序不仅容易，而且是跨平台的。`WebBroker` 应用可以移动到 Windows 平台，并转换为 ISAPI、NSAPI、WinCGI 和 CGI ，而无需进行重大修改。同样，现有的 Windows `WebBroker` 应用也可以轻松地移植到 Linux。当然，必须小心避免任何特定于平台的代码。

本章假设读者对互联网术语和技术有基本的了解。如果你不熟悉这些或需要复习，请参见附录 C，“互联网技术简介”。此外，假设 Apache 已安装、配置了共享对象支持并正在正常运行。如果没有，请咨询你的 Linux 发行版附带的文档或访问 `http://www.apache.org`。

> 提示：Apache 必须配置为运行 DSO。默认情况下，大多数发行版编译 Apache 时并未包含 DSO 支持。判断你的发行版是否编译了 DSO 支持的最简单方法是执行以下命令：
`find / -print | grep libhttpd`
如果你发现了 `libhttpd.so`，那么可能 Apache 已经带有 DSO 支持进行了编译。如果没有，请参阅《Delphi Magazine》2001 年 5 月刊中关于 Apache 共享模块的文章。在本文写作时，该文章可以在线获取：`http://www.TheDelphiMagazine.com/Samples/1222/1222.htm`。
Borland 还提供了一个白皮书，地址为：`http://www.borland.com/kylix/papers/apache_development.pdf`。

## 第 21 章：互联网应用 — NetCLX

### 互联网应用的类型

Kylix 支持两种创建互联网应用的方法：通用网关接口 (`CGI`) 和 Apache 共享对象 (`DSO`)。`CGI` 应用是目前生成动态内容最常用的方法。

#### CGI – 通用网关接口

所有 `CGI` 应用都必须符合通用网关接口规范。Web 服务器与 `CGI` 应用之间的通信通过四种方式实现：环境变量、命令行、标准输入和输出。有关 `CGI` 应用细节的更多信息，请访问 `http://hohoo.ncsa.uiuc.edu/cgi/overview.html`。

使用 `CGI` 应用的优点是它们不受限于特定的 Web 服务器。几乎每个 Web 服务器都支持 `CGI` 应用。最大的优势是每当发出请求时，都会创建一个进程来处理请求。反复启动应用程序是一个耗时的操作。

#### DSO – 动态共享对象

`DSO` 应用是标准的 Linux 共享对象库（共享对象库更多信息请见第8 章），在需要时为 Apache 提供若干功能。有关实现 Apache `DSO` 所需详细信息，请访问 `http://www.apache.org`。

使用 Apache `DSO` 的主要优势是避免频繁启动应用程序。Apache 将共享对象库加载到内存中，然后调用 `DSO` 中暴露的函数。这大大减少了处理请求所需的时间。

> 提示：Kylix 的互联网应用功能仅适用于 Kylix 1 开发者版、Kylix 2 专业版和 Kylix 2 企业版。如果你拥有 Kylix 1 桌面版或任何版本的 Kylix 开放版，Bob Swann 有一个名为 `DrBobCGI` 的跨平台工具用于编写 `CGI` 应用（访问 `http://www.drbob42.com/tools/drbobcgi.htm`）。

编写时当前的 Apache 版本为 1.3.20。Apache 是一个多进程应用程序，通过产生子进程来处理单个请求。因此，多个 `DSO` 之间的任何通信都需要形式的进程间通信（有关 IPC 的更多信息请见第 17 到 20 章）。

当 Apache 2.0 版本可用时，可以通过派生子进程来处理单个请求。

### WebBroker 架构

由于 `CGI` 和 `DSO` 应用的功能相似，Kylix 团队将公共区域抽象为类。

### 高级项目架构

在最高层级，互联网应用是 `TWebApplication` 的后类。

#### TWebApplication

在最高层级，互联网应用是 `TWebApplication` 的后类，定义在 `WebBroker`。除了构造函数和析构函数外，还声明了三个方法：`Initialize`、`CreateForm` 和 `Run`。

`CGI` 应用定义为 `TCGIApplication`，它是 `TWebApplication` 的子类并定义在 `CGIApp` 中。同样，`DSO` 应用在 `ApacheApp` 中定义为 `TApacheApplication`。

通过 `File | New | Server Application` 创建互联网应用后，检查源码。下面是一个 `CGI` 应用的示例：

```pascal
program Project1;

{$APPTYPE CONSOLE}

uses
  WebBroker,
  CGIApp,
// TWebModule
Unit1 in 'Unit1.pas' (TWebModule: TWebModule);

{$R *}

begin
  Application.Initialize;
  Application.CreateForm(TWebModule, TWebModule);
  Application.Run;
end.
```

## 第 21 章：互联网应用 — NetCLX

一个 `DSO` 应用如下：

```pascal
library Project1;

uses
  WebBroker,
  HTTP,
  WebApp,
// TWebModule
Unit in 'Unit1.pas' (WebModule: TWebModule);
```

```pascal
exports
  apache_module name 'Project1_module';
```

```pascal
begin
  Application.Initialize;
  Application.CreateForm(TWebModule, TWebModule);
  Application.Run;
end.
```
