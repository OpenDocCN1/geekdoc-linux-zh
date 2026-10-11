
## 28.10 Web Resources 1415

[`www-130.ibm.com/developerworks/webservices`]

IBM 针对面向服务架构 (SOA) 和 Web服务的网站包含了有关 Web 服务技术的文章、下载、演示和讨论论坛。

[`www.w3.org/WSDL/`]

提供了关于 WSDL 的大量文档，包括在 WSDL 框架下对 Web 服务以及相关技术（如 XML、SOAP、HTTP 和 MIME 类型）的深入讨论。

[`www.w3.org/TR/soap`]

提供了关于 SOAP 消息的大量文档，涵盖了在 HTTP 上使用 SOAP 以及 SOAP 服务。

[`www.ws-i.org`]

Web 服务互操作性组织 (Web Services Interoperability Organization) 的网站提供了基于标准的 Web 服务构建详细信息，这些标准促进了互操作性和真正的平台独立。

[`webservices.xml.com/security`]

关于 Web 服务安全和标准安全协议的文章。

## 基于 REST 的 Web 服务

[`en.wikipedia.org/wiki/REST`]

解释表象状态转移 (REST) 的 Wikipedia 资源。

[`www.xfront.com/REST-web-Services.html`]

标题为“以 REST 方式构建 Web 服务”的文章。

[`www.ics.uci.edu/~pubs/dissertation/rest_arch_style.htm`]

最初提出基于 REST 服务的论文。

[`rest.blueox.net/cgi-bin/wiki.p1?ShortSummaryOfRest`]

对 REST 的简单介绍。

[`www.prescod.net/rest`]

链接到许多 REST 资源。

## 总结

### 第 28.1 节简介

- Web 服务是存储在一台计算机上的软件组件，可以通过网络在另一台计算机上的应用程序（或其他软件组件）通过方法调用访问。
- Web 服务使用 XML 和 HTTP 等技术进行通信。
- 简单对象访问协议 (SOAP) 是一种基于 XML 的协议，允许 Web 服务和客户端以平台独立的方式进行通信。
- Web 服务通过标准的、广泛可用的 Web 服务实现业务交易，而不是依赖于专有应用程序。
- Amazon、Google、eBay、PayPal 等许多公司正在利用 Web 服务的优势，通过 Web 服务向合作伙伴提供其服务器端应用程序。
- 通过发布 Web 服务和使用免费 Web 服务，公司可以花费时间开发新应用程序并创建创新的应用程序。
- Netbeans 5.5 和 Java Studio Creator 2（均由 Sun 开发）是许多允许程序员“发布”和/或“消费”Web 服务的工具。

## 第 28 章 JAX-WS Web 服务、Web 2.0 和混合 (Mash-Ups)

### 第 28.2 节 Java Web 服务基础

- Web 服务所在的计算机被称为远程机器或服务器。访问 Web 服务的客户端应用程序通过网络向远程机器发送方法调用，远程机器处理该调用并通过网络返回响应。
- 在 Java 中，Web 服务是以类的形式实现的。表示 Web 服务的类存在于服务器上——它不是客户端应用程序的一部分。
- 创建一个接收客户端请求的 Web 服务被称为“发布”Web 服务；在客户端应用程序中使用 Web 服务则被称为“消费”Web 服务。
- 消费 Web 服务的应用程序由两部分组成：与 Web 服务交互的代理类对象，以及通过调用代理对象上的方法来消费 Web 服务的客户端应用程序。代理对象代表客户端处理与 Web 服务通信的细节。
- 使用 JAX-WS 2.0 创建的 Web 服务的请求和响应通常通过 SOAP 传输。任何能够生成和解析 SOAP 消息的客户端都可以与 Web 服务交互，无论该 Web 服务是用什么语言编写的。

### 第 28.3.1 节在 Netbeans 中创建 Web 项目并添加 Web 服务类

- 当你在 Netbeans 中创建 Web 服务时，你专注于 Web 服务的逻辑，并让 IDE 处理 Web 服务的底层设施。
- 在 Netbeans 中创建 Web 服务，你首先创建一个 Web Application 类型的项目。Netbeans 使用此项目类型用于在浏览器客户端执行的应用程序以及由其他应用程序调用的 Web 服务。
- 当你在 Netbeans 中创建 Web Application 时，IDE 会支持该应用程序的其他文件。

### 第 28.3.2 节在 Netbeans 中定义 Web 服务

- 默认，使用 JAX-WS API 创建的每个新 Web 服务类都是 POJO（普通 Java 对象）——你不需要实现类或接口来创建 Web 服务。
- 当你编译使用 JAX-WS 2.0 注解的类时，编译器会生成代码框架。
- 表示 Web 服务的类存在于服务器上——它不是客户端应用程序的一部分。
- 创建一个接收客户端请求的 Web 服务被称为“发布”Web 服务；在客户端应用程序中使用 Web 服务则被称为“消费”Web 服务。
- 消费 Web 服务的应用程序由两部分组成：与 Web 服务交互的代理类对象，以及通过调用代理对象上的方法来消费 Web 服务的客户端应用程序。代理对象代表客户端处理与 Web 服务通信的细节。
- 使用 JAX-WS 2.0 创建的 Web 服务的请求和响应通常通过 SOAP 传输。任何能够生成和解析 SOAP 消息的客户端都可以与 Web 服务交互，无论该 Web 服务是用什么语言编写的。

### 第 28.3.3 节从 Netbeans 发布 Web 服务

（注：此处由于原文存在大量重复和 OCR 错误，翻译已根据要求进行了去重并保留了核心逻辑）

## 第 28 章 JAX-WS 服务、Web 2.0 与混合应用 (Mash-Ups)

- Netbeans 使用 WSDL描述来生成客户端代理类和构件。
- 当你指定要使用的 Web 服务时，Netbeans会将该服务的 WSDL 复制到项目中的一个文件中。你可以通过展开项目 `xml-resources` 文件夹下的节点来查看此文件。
- 可以通过右键点击 Netbeans 项目（Projects）选项卡中的 Web 服务节点并选择“刷新（Refresh）”，重新生成客户端构件和 WSDL 文件的副本。
- 你可以通过选择 Netbeans 文件（Files）选项卡并展开项目的 `build` 文件夹来查看由 IDE 生成的客户端构件。

## 第 28.5 节 SOAP

- SOAP 是一种常用的、平台无关的基于 XML 的协议，它便于远程过程调用，通常通过 HTTP 进行。
- 传输请求和响应消息的协议也称为 Web服务的线缆格式（wire format）或线缆协议（wire protocol），因为它定义了信息如何“沿线传输”发送。
- 每个请求和响应都封装在 SOAP 消息（也称为 SOAP 封包，envelope）中，其中包含了 Web 服务处理所需的信息。
- 用于传输请求和响应的格式必须支持应用程序之间传递的所有类型。SOAP 支持原始类型及其包装类，以及日期（Date）、时间（Time）等。SOAP 还可以传输自定义类型的数组和对象。
- 当程序调用 Web 方法时，请求所有相关信息都被封装在 SOAP 消息中发送到服务器。Web 服务处理 SOAP 消息的内容，这些内容指定了要调用的方法及其参数。Web 服务接收并解析请求，调用相应的方法，并通过另一个 SOAP 消息将响应返回给客户端。客户端代理解析响应（其中包含方法调用的结果），并将其返回客户端应用程序。
- SOAP 消息是自动为你生成的。因此，在发布和消费 Web 服务时，你不需要理解 SOAP 或 XML 的细节即可利用它。

## 第 28.6 节 Web 服务中的会话跟踪

- Web 服务维护客户端状态信息可能是有益的，这消除了多次在客户端和 Web 服务之间传递客户端信息的需求。存储会话信息使 Web 服务能够区分不同的客户端。

### 第 28.6.1 节 创建 Blackjack Web 服务

- 要在 Web 服务中使用会话跟踪，必须包含维护状态信息的资源的代码。在过去，你必须编写繁琐的代码来创建这些资源。然而，JAX-WS 通过 `@Resource` 注解为你处理了这些工作。该注解允许 Netbeans 将复杂的代码“注入”到你的类中，让你能够专注于业务逻辑而非支持代码。
- 使用注解来支持你的类被称为依赖注入（dependency injection）。像 `@WebService`、`@WebMethod` 和 `@WebParam` 等注解也执行依赖注入。
- `WebContext` 对象允许你访问并维护特定请求的信息，例如会话状态。创建 `WebContext` 对象的代码是由 `@Resource` 注解注入到类中的。
