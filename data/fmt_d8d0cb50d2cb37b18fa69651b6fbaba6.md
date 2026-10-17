
## 5.2.1 HTTP

### HTTP 的优势

使用 HTTP 作为传输具有许多优势，包括：

- HTTP 是一种广泛采用的协议。任何使用 HTTP 的组织都可以通过它来实现 Web 服务。
- HTTP 协议是开放的，许多企业都使用它。
- HTTP 能够自由穿过防火墙。因此，使用 HTTP 传输的障碍更少。

### HTTP 的缺点

HTTP 是一种轻量级协议，最初的设计并不是为了携带应用数据。使用它的某些缺点包括：

- HTTP 协议是无状态的。如果需要状态数据，应用程序必须管理状态。
- HTTP 不可靠。如果需要可靠的数据传输，应用程序必须：
  - 开发一个可靠性框架。
  - 使用更可靠的协议。

## 5.2.2 消息服务

消息中间件是异步方式访问系统的流行选择。消息通信是松耦合的，与远程方法调用（RMI）或远程过程调用（RPC）等紧耦合技术相比，发送者不需要了解接收者的任何信息。要交付的消息由发送者发送到目标位置，接收部分不需要同时可用。当需要 Web 服务以以下方式通信时，消息中间件可能是合适的传输协议：

- 同步，即消息发送者不需要等待回复
- 可靠，即发送者确保消息会被交付

Java 应用程序使用消息件的标准方法是使用 Java 消息服务（JMS）接口。JMS 为 Java 程序员提供了一种创建、发送、接收和读取企业消息的通用方法。JMS 由 Sun Microsystems 开发，IBM、其他企业消息供应商、事务处理供应商和 RDBMS 供应商积极参与。

### IBM JMS 实现

IBM 提供了两种 JMS 实现：

- 包含在 WebSphere Application Server V5.0 中的 JMS 提供程序。它可以用于运行在 WebSphere V5.0 上的应用程序之间的异步通信。
- WebSphere MQ V5.3 包含内置的 JMS 支持，具有增强的性能功能，用于 JMS 应用程序与其他应用程序集成。WebSphere MQ 处理网络接口，确保消息一次且仅交付，处理通信协议，在可用资源之间动态分配负载并在系统问题后进行恢复。IBM WebSphere MQ 适用于大多数流行的操作系统平台。

### JMS 的缺点

尽管 JMS 是一个基于 Java 系统的开放标准，但实际的传输系统必须由软件产品提供。因此，有几个考虑因素，包括：

- 通信的 Web 服务必须能够访问相互通信的 JMS 供应者。通常，这意味着必须安装相同的产品。例如，两个系统都必须安装 IBM WebSphere MQ。
- JMS 是一个基于 Java 的标准，对于非基于 Java 的系统来说并不容易访问。

## 5.2.3 简单邮件传输协议

简单邮件传输协议 (`SMTP`) 是让互联网变得极其流行的协议之一，也是互联网电子邮件的基础。它的目标是在人之间可靠、高效地传输电子邮件。它与其他消息协议（如 IBM WebSphere MQ 或 JMS）不同，后者是专为处理程序之间的信息传输而设计的。

`SMTP` 独立于特定的底层传输子系统，只需要一个可靠的、有序的数据流通道。`SMTP` 的一个重要特性是它能够在跨传输服务环境中中继邮件。它最初于 1982 年由互联网工程任务组 (`IETF`) 作为 RFC 821 发布。自那时，从 RFC 2821 开始的新版 RFC 对原始标准进行了增强，以考虑技术能力。

作为一种广泛使用的标准，`SMTP` 是 SOAP 消息的潜在传输方式。W3C SOAP 1.1 说明文档的作者指出：“SOAP 可以与其他多种协议结合使用；然而，本文中定义的唯一绑定描述了如何将 SOAP 与 HTTP 以及 HTTP 扩展框架结合使用。”W3C SOAP 1.1 说明可以在此处获取：

> http://www.w3.org/TR/soap/

目前大多数实现使用 HTTP 传输 SOAP 消息，但没有理由认为你不能使用其他层，例如 `SMTP`。

### Apache SOAP SMTP 传输

自 WebSphere V4.0 起，Apache SOAP 就被作为 WebSphere SOAP 引擎包含在内。它已被 Apache Axis 和 J2EE Web 服务所取代。

Apache SOAP 分发包含了允许使用电子邮件处理 SOAP 请求的类。它结合了 `SMTP` 和 `POP` 使用。一个名为 `SMTP2HTTPBridge` 的类必须在服务器上一个独立的 JVM 中运行。正如名称所示，该类充当桥接器，在 HTTP 和 `SMTP` 之间映射请求。严格来说，这并不是一个独立的 `SMTP` 传输；它实际上做的是将电子邮件 SOAP 消息转换为 HTTP SOAP 消息。

### SMTP 和 J2EE Web 服务

XML 消息 Java API (`JAXM`) 可选包允许应用程序使用 Java API 发送和接收面向文档的 XML 消息。`JAXM` 实现了带有附件的消息的 SOAP 1.1，使开发者能够专注于为应用程序构建、发送、接收和分解消息，而不是编写低级通信例程。规范确保了通过支持多种通信基础设施和关键网络传输（包括但不限于 HTTP(S) 和 `SMTP`）可以完成消息投递。然而，尚未找到关于其实现的参考。

`JAXM` 增加了对插件 ebXML 等更高级消息协议的支持。`JAXM` 并不是像 JMS 那样功能全的消息 API。

J2EE 还提供了一个邮件 API。JavaMail 1.3.1 API 定义了一组抽象类，用于模拟电子邮件系统。该 API 提供了一个与平台无关且协议无关的框架，用于构建基于 Java 技术的电子邮件和消息应用程序。JavaMail API 实现为 Java 平台可选包，并作为 J2EE 的一部分可用。参考实现包含了核心 Mail 包以及 IMAP、POP3 和 `SMTP` 服务提供者。

### 在何处可以找到更多信息

有关 `SMTP` 的信息，请参阅：

- SOAP 协议：

http://www.w3.org/TR/SOAP/

- Apache SOAP：

http://xml.apache.org/SOAP/

- `SMTP`:

http://www.ietf.org

## 5.2.4 HTTPR

可靠 HTTP (`HTTP`) 是一种提出的用于在服务器和客户端之间提供 HTTP 数据包可靠交付的协议，但它已被撤回，转而采用 OASIS 演进中的 WS-ReliableMessaging 标准。`HTTP` 提案通过为 HTTP 添加扩展来提供可靠性，而在后续章节中详细介绍的 WS-ReliableMessaging 则在信封层级提供可靠性。

## 5.2.5 传输的新兴标准

目前 Web 服务常用的传输协议由 HTTP 主导，原因见第 111 页“HTTP 的优势”中的讨论。然而，对于企业在业务关键处理上开发 Web 服务，需要更可靠的传输协议。本节讨论了该领域的一些新兴工作。

### WS-ReliableMessaging

正如第 113 页“JMS 的缺点”中所述，目前的可靠消息传输机制要求连接双方使用相同的基础设施，如 IBM WebSphere MQ。WS-ReliableMessaging 草案标准的开发旨在为不同传输基础设施之间的互操作性提供一个框架。

该草案标准由 IBM、BEA 和 TIBCO 于 2003 年 3 月发布。标准定义的协议提供了四种交付保证描述，通信中的伙伴必须实现这些描述：

- AtMostOnce（最多一次）
- AtLeastOnce（至少一次）
- ExactlyOnce（恰好一次）
- InOrder（有序）

WS-ReliableMessaging 草案标准使用 WS-Policy（见第 144 页 5.8“策略”）相关标准作为确定可靠消息交换中伙伴能力和要求的框架。作者还强烈建议使用 WS-Security 和相关标准来保护通信（见第 151 页 5.9.4“安全新兴标准”）。

### 在何处可以找到更多信息

有关 WS-ReliableMessaging 的更多信息，请参阅：

```
http://www.ibm.com/developerworks/webservices/library/ws-rm/
http://www.ibm.com/developerworks/webservices/library/ws-rmimp/
```

### BEEP

阻塞扩展交换协议 (`BEEP`) 是一种通用的应用程序协议框架，用于 TCP/IP 连接上的点对点异步交互。与 HTTP 不同，`BEEP` 没有服务器或客户端的概念，而是在请求者向提供者发起连接请求时，发起一个基于消息的通信会话。

`BEEP` 由互联网工程任务组 (`IETF`) 标准，提供了一个协议框架来管理点对点连接、身份验证、消息传输和错误处理。但这一切是有代价的，因此 `BEEP` 本身不依赖于归类为一次性的 DNS 查询或像 NFS 那样紧密耦合的 RPC 协议。使用 `BEEP` 的合适环境是你需要一个以下应用程序协议框架时：

- 连接导向：任何基于 `BEEP` 的通信都预计在每次交互时启动并断开。换句话说，`BEEP` 期望你的应用程序连接、执行所需任务并断开。
