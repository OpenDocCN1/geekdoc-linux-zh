
CouchDB 起于 2005 年，是 Damien Katz 的一个自筹个人项目。2008 年，它交给了 Apache，在那里继续开发。CouchDB 的目标是提供一个适用于 Web 应用程序的数据库。重点是可扩展性和容错性，同时使用廉价硬件（*Couch 是“不可靠商品硬件集群”的缩写*）。这不是一项容易的任务，但一旦成功完成，就能降低成本。

CouchDB 使用 RESTful HTTP API，从一开始就设计为用于 Web 以及为 Web 服务。所有存储的项目都有唯一的资源标识符（URI），完整的创建、读取、更新和删除（CRUD）功能可以直接通过标准 HTTP 调用可用，这使得 CouchDB 非常容易集成到 Web 应用中。这些调用可以从浏览器进行，也可以从命令行使用类似 `cURL` 的工具（`cURL` 可于许多典型的服务器平台，如 Ubuntu）。

CouchDB 的一个优秀特性是它设计时包含了 ACID 兼容性，这与许多 NoSQL 选项不同。这使得使用 CouchDB 处理对一致性更敏感的数据成为可能。

CouchDB 用 Erlang 编写，这是一种专为并发而语言语言。这使得 CouchDB 更适用于并发分布式系统。CouchDB 设计用于存储 JSON 文档对象。

CouchDB 用于多个软件和 Web 应用，包括许多 Facebook 游戏和应用程序、BBC 内部使用、Ubuntu One 以及 Canonical 的云存储。

## MongoDB

MongoDB 与 CouchDB 相似之处在于，它们都被设计为 JSON 对象的文档存储，并且像 Cassandra 一样，专为复制和高可用性而设计。它由名为 10gen 的公司创建并支持，并且较新，首次公开发于 2009 年。这个开源数据库的一个独特特性是，开发者提供商业企业级支持、培训和咨询。这使得 MongoDB 的采用远快于其他 NoSQL 产品。

MongoDB 支持*分片*（sharding），它自动跨服务器对数据进行分区，以提高性能和可扩展性。这产生了一种负载和数据平衡的形式，并提供了一种简单添加节点的方法。分片还旨在支持自动故障转移系统，在该系统中节点数据被复制，从而允许没有单点故障。

此外，MongoDB 对索引的支持比大多数 NoSQL 解决方案更广泛且强大。

## 是营销炒作还是卓越设计？

MongoDB 并不是在真空环境中设计的。它是为了解决开发者在使用关系型数据库时面临的特定问题，特别是处理灵活数据模式的需求以及水平扩展的能力。虽然 NoSQL 技术有很多炒作，但 MongoDB 的设计是基于现代 Web 应用程序开发的实际需求。

使用 JSON 作为数据格式对于已经在代码中使用 JSON 的开发者来说是非常直观的。这减少了在应用程序和数据库之间映射对象的复杂性。此外，MongoDB 对分片和复制的支持使其成为需要扩展的应用程序的强大选择。

然而，记住 MongoDB 并非万灵药。对于某些用例，关系型数据库可能是更好的选择，特别是当复杂的连接和 ACID 兼容性至关重要时。关键在于理解每个工具的优缺点，并为工作选择合适的工具。

## 第 30 章 NoSQL 数据库

HBase 的主要特性是它能够托管极其巨大的表，规模可达数十亿行和百万列。它被设计为运行在通用硬件上。HBase 提供了一个 RESTful 的 Web 接口，支持许多格式和编码，并针对实时查询进行了优化。

许多公司都在使用 Hadoop，包括 Amazon、eBay、Facebook、IBM、LinkedIn、Rackspace 和 Yahoo! 等一些非常著名的巨头。

## 图存储

图存储（Graph stores）或图数据库，字面意思是将数据以图的形式存储。这意味着数据被表示为一系列节点以及它们之间的相互关系。在最简单的情况下，图只有一个节点，所需要的只是该记录及其属性。属性列表可以短到只有几个，也可以长到有几个（可能更多）。

为了不让这种笨拙性日益增加，你必须尽早开始创建新节点，每个节点都有自己的属性以及将每个节点与其他节点连接的显式关系。正是关系组织了节点，因此其结构是灵活的。图看起来像列表、映射、树或完全不同的结构。

图数据库通过遍历（traversals）进行查询。从定义的起始节点开始，通过特定路径遍历，以回答诸如“我的朋友没有选的课程中有哪些？”或“如果服务器 X 有网络连接问题，哪些 Web 服务将受到影响？”在图数据库中，索引仅仅是一种特殊的遍历，通常用于根据它们共享的属性查找特定的节点或关系。

图存储并不十分常见，但深受推崇它的人的喜爱。与本章中其他 NoSQL 数据库类别相比，该类别中可用选项的差异化并不那么大。

## Neo4j

Neo4j 是 NoSQL 世界中大多数人听过的图存储数据库。它既有免费版，也有商业版。它提供了 Java、Python 和 Ruby 的语言绑定。它支持在单机上扩展到具有数十亿个节点/属性的图，并可以扩展到多台机器。它可以作为独立服务器部署，也可以作为一个轻量级数据库与其他软件共存在同一台机器上。

## OrientDB

OrientDB 是一个根据 Apache 2.0 许可证发布的免费数据库。它使用一种名为 MVRB-Trec 的不同索引算法，它称这种算法快得多。你可能记得一个名为 OrientDBMS 的旧版关系型数据库。OrientDB 与之相关，可以使用 SQL 的子集，但它是使用文档/图数据基础的完全重写。

## HyperGraphDB

HyperGraphDB 是另一个使用 LGPL 许可证的免费选项。它主要设计用于语义网、知识管理和人工智能项目。在数学中，超图（hypergraph）定义是对标准图的扩展，允许边指向两个以上的节点。根据 HyperGraphDB 网站，“HyperGraphDB 进一步扩展了这一点，允许边指向其他边，并使得每个节点或边都能携带任意值作为负载。”HyperGraphDB 似乎侧重于学术领域，因此学生可能对其特别感兴趣，因为 HyperGraphDB 似乎在尝试新的研究想法。

## FlockDB

FlockDB 被 Twitter 用于存储社交图（例如关注关系）以及用于一些二级索引。它是免费开源的，使用 Apache 2.0 许可证。它比其他图数据库简单，因为它尝试解决的问题较少，是为一种主要用途设计的。FlockDB 为像 Twitter 这样的在线、低延迟、高吞吐量环境设计；即便如此，它也只存储特定类型的数据。

## 参考文献

- `woracle.com/us/products/database/berkeley-db/index.html`—Berkeley DB 主网站。
- `http://cassandra.apache.org/`—Cassandra 主网站。
- `www://memcached.org/`—Memcached 主网站。
- `http://memcached.org/`—MemcachedDB 主网站。
- `http://redis.io/`—Redis 主网站。
- `http://basho.com/products/riak-s2/`—Riak 主网站。
- `http://couchdb.apache.org/`—CouchDB 主网站。
- `http://mongodb.org/`—MongoDB 主网站。
- `http://basex.org/`—BaseX 主网站。
- `http://research.google.com/archive/bigtable.html`—描述 BigTable 的论文。
- `http://research.google.com/archive/mapreduce.html`—描述 MapReduce 的论文。
- `http://hadoop.apache.org/`—Hadoop 主网站。
- `http://hbase.apache.org/`—Hbase（Hadoop 数据库）主网站。
- `http://research.google.com/archive/gfs.html`—描述 Google 文件系统的论文。
- `http://neo4j.org/`—Neo4j 主网站。
- `http://orientdb.org/`—OrientDB 主网站。
- `http://www.hypergraphdb.org/`—HyperGraphDB 主网站。
- `https://github.com/twitter/flockdb`—FlockDB 主网站。

## 第 31 章

轻量级目录访问协议 (LDAP)

## 本章内容

- 配置服务器
- 配置客户端
- 管理

## 参考文献

轻量级目录访问协议（LDAP），发音为 "ell-ldap"，是可以在互联网上获取的技术之一。它的任务非常简单：存储关于用户和设备的信息。

当大多数人将 LDAP 视为一个目录时，会发现这个概念更容易理解。在后台，LDAP 驱动着身份验证、数据分发等等功能。

如果你已经使用了 LDAP 多年，你就会意识到它巨大的力量灵活性。但如果你只是第一次尝试 LDAP，它看起来可能像你能想象到的最糟糕的东西。LDAP 有特定的配置要求，极度缺乏图形化工具，并且有很多缩写需要记忆。好的一方面是，当 LDAP 改进了你的网络体验时，你付出的所有努力都是值得的。在开始之前，你应该阅读整个章节。然后，在执行任何操作之前读取 `/etc/ldap/schema` 中的 README 文件。

### 配置服务器

配置 LDAP 服务器的第一步是安装客户端和服务器应用程序。安装 `slapd` 和 `ldap-util` 包。这样做还会安装另外三个包：`slapinst`、`slap2` 和 `unixodbc`。

默认情况下，Ubuntu 配置 `slapd` 以运行守护进程所需的最小选项。我们将从基础安装一直到其实有用的地方进行所有配置。

现在你需要知道你服务器的完全限定域名（FQDN）。稍后，你将开始编写/修改一些配置文件，这是该过程中至关重要的一部分。示例是 `matthewhelmke.com`。

从 FQDN 中获取域组件，即存储在 DNS 中的域名名称。这缩写为 `dc`。LDAP 将域名的每个部分（用点分隔）连接到域组件。在示例中，有两个 dc 项目：`matthewhelmke`, `com`。

OpenLDAP 现在使用一个包含 `cn=config` 目录树的独立目录来动态配置 `slapd` 守护进程。这允许你在不停止和重启服务的情况下修改模式定义、索引等，而这在早期版本中是必须的。这种配置需要两个文件：一个只有最小配置的后端，和一个使用传统格式的前端，该格式与使用标准的外部程序兼容。

### 创建你的模式

从加载一些预设的模式文件开始。通过预加载某些设置，配置会变得更快更容易。如果你正在构建企业级服务器，请阅读 OpenLDAP 文档并从头开始，这样你就能确切知道服务器在做什么以及为什么。对于示例，使用以下命令将这三个文件加载到目录中：

# 配置服务器
