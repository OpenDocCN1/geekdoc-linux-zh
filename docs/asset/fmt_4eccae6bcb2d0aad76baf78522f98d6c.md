
应用层和数据库层可以根据系统的工作负载以多种不同的方式拆分。应用层可以在多个系统上运行，以达到所需的性能。最好只在一个平台上使用应用层，以简化维护，因为只需要应用一组补丁。数据库层可以是独立系统，也可以是根据需求配置的 RAC 集群。也可以在同一个系统上运行应用层和数据库层。

## 桌面层（Desktop Tier）

桌面层（或客户端层）是一个 [Java Archive](https://en.wikipedia.org/wiki/Java_Archive)（JAR）文件集合，它被下载并在客户端浏览器中运行。JAR 文件由应用层下载到客户端系统的 [Oracle JInitiator](https://en.wikipedia.org/wiki/Oracle_JInitiator)（由 [Oracle Java 虚拟机](https://en.wikipedia.org/wiki/Oracle_Java_Machine)（JVM）提供）运行。在 Netscape 浏览器中，这实现为一个插件；在 Microsoft Internet Explorer 浏览器中，它实现为 [ActiveX](https://en.wikipedia.org/wiki/ActiveX) 组件。Oracle 依赖自己的 JVM，因为依赖他人的组件并不安全。

## 应用层（Application Tier）

应用层是最复杂的层。这里驻留着 Web 服务器（基于 [Apache web 服务器](https://httpd.apache.org/)）、Forms 服务器、并发处理服务器、报表服务器和管理服务器。该层还可能包含可选的 Discoverer 服务器。通常，所有这些组件都驻留在同一个系统上，但也可以拆分。如果拆分，并发处理服务器和管理服务器通常与数据库层运行在同一个系统上。让我们看看不同的组件及其在整个图中的位置。

### Web 服务器（Web Server）

Oracle HTTP 服务器基于 [Apache web 服务器](https://httpd.apache.org/)，但经过 Oracle 修改以更好地与 Oracle 应用层和 Oracle 数据库服务器集成。Web 服务器包括 Apache web 服务器、Web 监听器（Web Listener）、Java Servlet 引擎（JServ）和 [JavaServer Pages](https://en.wikipedia.org/wiki/JavaServer_Pages)（JSP）。如果可能，Web 服务器本身处理请求。但对于高级处理，Web 监听器将请求传递给 Java Servlet 引擎，该引擎根据需要联系数据库服务器。

### Forms 服务器（Forms Server）

Forms 服务器支持 Oracle E-Business Suite 的 forms。这是传统的 [Oracle Forms](https://en.wikipedia.org/wiki/Oracle_Forms)，而非基于 HTML 的应用程序（formerly known as Self-Service）。Forms 服务器是一个 Oracle 9i 组件，提供桌面客户端与 Oracle 数据库服务器之间的通信，显示客户端屏幕并根据用户操作初始化数据库中的更改。

Oracle E-Business Suite 支持使用 [Socket](https://en.wikipedia.org/wiki/Socket) 模式用于内网用户，[HTTPS](https://en.wikipedia.org/wiki/HTTPS) 用于互联网用户，以及 [HTTP](https://en.wikipedia.org/wiki/HTTP) 模式用于基于 Forms 的通信。Forms 监听器 Servlet 允许您通过 HTTP 和 HTTPS 运行 Oracle Forms 应用程序。它为每个客户端创建一个 Forms 服务器运行时进程，以便通过 Web 服务器进行通信。由于 HTTP 协议比套接字更“健谈”，Forms 监听器 Servlet 会使网络流量增加大约 40%。但它提供了重新建立丢失网络连接、需要更少的机器和端口暴露在防火墙外以及允许更健壮和安全地通过 Internet 部署的好处。

### 报表服务器（Reports Server）

报表服务器用于创建[商业智能系统](https://en.wikipedia.org/wiki/Business_intelligence_system)（Business Intelligence System）的报表。使用报表服务（reports services），而不是允许报表非计划运行。使用报表服务，您可以调整和管理报表处理，这可能非常消耗资源。当有大量的用户时，报表服务可以根据需要拆分到几个报表服务器上。其中一个报表服务器被指定为主报表服务器（master reports server），它接收初始请求并将其分配给其他报表服务器之一。

### 并发处理服务器（Concurrent Processing Server）

当自助服务（Self-Service）和 Oracle Forms 应用程序在前台运行用户请求时，数据密集型操作在后台作为批处理作业运行。并发处理服务器负责运行这些批处理作业。这个专门的服务器确保资源密集型并发处理操作不会干扰交互式操作。在 Oracle RAC 环境中，并发处理服务器配置为在集群的不同节点上定义不同的队列，以便将并发处理分散到不同的集群节点上。这被称为并行并发处理（parallel concurrent processing）。在 Linux RAC 环境中使用并行并发处理正变得非常流行。

### 管理服务器（Admin Server）

管理（Administration）服务器用于维护 Oracle 数据库中的数据模型。在 Oracle RAC 集群中，管理服务器仅在一个节点上运行，但配置为主节点不可用时故障转移到另一个节点。管理服务器用于升级 Oracle E-Business Suite、应用补丁以及维护数据库中的数据。

### Discoverer 服务器（Discoverer Server）

Oracle Discoverer 服务器是一个旨在帮助分析服务和即时查询处理的工具。它也用于执行业务预测，是一个业务分析工具。Oracle Discoverer 服务器是一个可选组件，可能不会在所有情况下部署。

## 数据库层

数据库层是实际数据存储的位置，可以是 Oracle8i、Oracle9i 或 Oracle 10g 数据库服务器。为了本书的目的，我们将假设指的是 Oracle10g 数据库服务器。数据库层不仅存储所有业务数据，还存储定义应用层的元数据。事实上，每当您运行 `AutoConfig` (`adautocfg`) 实用程序来配置 Oracle E-Business Suite 时，许多元数据表作为该过程的一部分会被更新。

## Linux 上可用的模块

Linux 上的 Oracle E-Business Suite 功能完整，并且 Oracle E-Business Suite 中可用的所有模块在 Linux 平台上均可用。E-Business Suite 的所有层（包括数据库应用程序和客户端）都可以在 Linux 上运行。Oracle 已承诺支持 Linux 平台，并完全支持 x86 平台上的 32 位 Linux，从而履行了该承诺。如需了解非 x86 32 位硬件平台上 Linux 操作系统对 E-Business Suite 的支持，请访问 Oracle MetaLink。

## 在 Linux 上使用 Oracle E-Business Suite

Oracle E-Business Suite 在 Linux 上的功能与其他平台没有区别。由于 Linux 平台比其他平台成本更低，应用层更可能由多个 Linux 系统组成，以实现冗余和性能优化。此外，许多 Linux E-Business Suite 配置利用 Oracle RAC 集群作为数据库层。

## RAC 环境中的 E-Business Suite

通过配置并行并发处理，Oracle E-Business Suite 可以配置为在 RAC 环境中工作。这允许并发管理器在 RAC 集群中的所有节点上运行，从而在这些节点之间分配工作负载。并行并发处理允许您为每个处理队列指定主要和次要位置。这使得 E-Business Suite 处理活动能够按照您选择的方式在集群节点之间分布。集群中的工作负载分布既不是自动的，也不是透明的。您必须选择并发处理队列的分布方式及其运行位置。

如前所述，Oracle E-Business Suite 可以配置为在 RAC 环境中运行，但这并非一项简单的配置任务。需要进行多项调优步骤，并且必须进行精细调整，以便能够以最优方式运行。

## 在 Linux 上安装和配置 E-Business Suite
