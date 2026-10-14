
CouchDB 用于多个软件和 Web 应用程序，包括许多 Facebook 游戏和应用程序、BBC 内部使用以及 Canonical 的云存储 Ubuntu One。

## MongoDB

MongoDB 与 CouchDB 相似之处在于，它们都被设计为 JSON 对象的文档存储器，并且与 Cassandra 不同，它是为复制和高可用性设计的。它由一家名为 10gen 的公司创建并支持，并且较新，首次发布于 2009 年。对于这个开源数据库来说，一个独特的特性是开发者提供商业、企业级支持、培训和咨询。这使得 MongoDB 的采用速度比典型的 NoSQL 产品快得多。

MongoDB 支持分片（sharding），它自动跨服务器划分数据分区，以提高性能和可扩展性。这产生了一种负载和数据平衡的形式，并提供了一种简单添加节点的方法。分片还旨在支持自动故障转移系统，在该系统中节点数据被复制，从而避免了单点故障。

此外，MongoDB 还包含了对索引的支持，其方式比大多数 NoSQL 解决方案更广泛且强大。

## 营销炒作还是卓越设计？

MongoDB 并不是在实验室里设计的。我们根据自己构建大规模、高可用、健壮系统的经验构建了 MongoDB。我们并不是从零开始，而是真正尝试找出哪些地方是坏的并去解决它们。因此，我对 MongoDB 的看法是，如果你取 MySQL 并数据模型从关系型改为基于文档，你将获得许多很棒的功能：用于加速的嵌入文档、可管理性、无模式（schema-less）、水平可扩展性。这意味着宽列存储对于主要用于读取数据的数据库（特别是从非常大的数据存储器读取）往往非常高效。

宽列存储使用类似表的结构，每个表都有定义的模式。与关系型数据库不同，宽列存储不记录表与表之间的关系。它们不是关系型数据库，而更像显示数据存在于多个维度上的映射。它们是为可扩展性和作为分布式系统而设计的。这里讨论了两个宽列存储的示例。另一个示例 Cassandra 在在本章前面已经讨论过，它既属于这一类别，也属于之前的键/值存储类别。

## BaseX

BaseX 由 Christian Grün 于 2005 年在康斯坦茨大学启动，随后于 2007 年使用 BSD 许可证发布。它是一个用于存储文档对象的轻量级数据库。它支持 XPath 和 Xquery 等标准 XML 工具，还包含图形用户界面（GUI）。尽管不像其他选项那样（可能是因为 JSON 相比 XML 的新颖和流行），BaseX 受许多大学和企业的尊重和使用。

## BigTable

宽列存储通常被称为大表存储（big table stores），名称源于最著名的例子之一——Google 的 BigTable。通常，关系型数据库使用行从表中读取数据。然后对数据进行排序以仅找到该行的内容。宽列存储通过从列读取数据改变了这一系统，在读取数据之前先选择属性。这对于输入只读查询更高效。

BigTable 是 Google 的专有产品，仅供 Google 使用。它设计用于与 Google 的 MapReduce 框架协作，该框架被用于在大型计算节点集群中处理海量数据集。BigTable 存储 Google Reader、我的搜索历史、Google Earth、YouTube 和 Gmail 等许多 Google 程序使用的海量数据。BigTable 不向外部开放。

## HBase

HBase 是 Hadoop 使用的数据库。Hadoop 是 Apache 项目的免费软件应用程序，用于在大型计算节点集群中处理大量数据。Hadoop 部分模仿了 Google 的 MapReduce 和 Google 文件系统论文中的信息。HBase 之于 BigTable 就像 Hadoop 之于 MapReduce。HBase 的主要特性是它托管非常大表的能力，或者跨越数百万列的数十亿行规模。它被设计为在通用硬件上托管这些数据。HBase 提供 RESTful Web 服务接口，支持许多格式和编码，并针对实时查询进行了优化。

许多公司正在使用 Hadoop，包括 Amazon、eBay、Facebook、IBM、LinkedIn、Rackspace 和 Yahoo! 等一些知名企业。

# 图数据库

图存储（或图数据库）从字面意思是以“图”的形式存储数据。这意味着数据被表示为一系列节点以及它们之间的关系。在最简单的情况下，图只有一个节点，所有需要记录的就是该记录目及其属性。属性列表可以短到只有一个项，也可以长到几百万项（可能更多）。

与其让这种笨拙结构不断增长，大多数系统会更早地创建节点，每个节点都有自己的属性以及将每个节点与其他节点连接起来的显式关系。正是关系组织了节点，因此其结构是灵活的。图可以像列表、树或完全不同的结构。

图数据库通过遍历进行查询。遍历从定义的节点开始，通过相关节点来回答诸类问题，例如：“我没有选课的朋友中有哪些同学？”或者“如果服务器 X 有网络连接问题，哪些 Web 服务会被中断？”在图数据库中，索引只是特殊类型的遍历，通常用于根据它们共享的属性来查找特定的节点或关系。

图存储并不十分常见，但深受推崇此者的喜爱。与本章中其他 NoSQL 数据库类别的差异化相比，该类别中可用选项的差异化较小。

## Neo4j

Neo4j 是 NoSQL 世界中大多数人听过的图存储。它既有免费版，也有商业版。它提供了 Java、Python 和 Ruby 的语言绑定。它在单台机器上可以扩展到数十亿个节点/关系的图，并可以扩展到多台机器。它可以部署在独立服务器上，也可以作为一个轻量级数据库与同一台机器上的其他软件共存。

## OrientDB

OrientDB 是一个免费并在 Apache 2.0 许可证下发布的数据库。它使用一种名为 MVR-Tree 的不同索引算法，它声称该算法要快得多。你可能记得一个名为 OrientDBMS 的旧版关系型数据库。OrientDB 与之相关并可以使用 SQL 的子集，但它是使用文档/图数据库基础完全重写的。

## HyperGraphDB

HyperGraphDB 是另一个使用 LGPL 许可证的免费选项。它主要为语义网、知识管理和人工智能项目设计。在数学中，超图的定义是对标准图的扩展，允许边指向两个以上的节点。根据 HyperGraphDB 网站的说法，“HyperGraphDB 进一步扩展了这一点，允许边指向其他边，并让每个节点或边都携带一个任意值作为载荷。”HyperGraphDB 似乎侧重于学术领域，因此学生可能对其特别感兴趣；HyperGraphDB 似乎正在尝试一些新的研究想法。

## FlockDB

FlockDB 被 Twitter 用于存储社交图（例如谁关注了谁）以及一些二级索引。它是免费开源的，使用 Apache 2.0 许可证。它比其他图数据库简单，因为它似乎解决的问题较少，是为一种主要用途设计的。FlockDB 是为像 Twitter 这样的在线、低延迟、高吞吐环境设计的；即便如此，它也是用于存储特定类型的数据。

## 参考文献

- [www.oracle.com/us/products/database/berkeley-db/index.html](Berkeley DB 主网站。)

- [http://cassandra.apache.org/](Cassandra 主网站。)

- [www.memcached.org/](Memcached 主网站。)

- [http://redis.io/](Redis 主网站。)

- [http://basho.com/products/riak-s2/](Riak 主网站。)

- [http://couchdb.apache.org/](CouchDB 主网站。)

- [http://mongodb.org/](MongoDB 主网站。)

- [http://basex.org/](BaseX 主网站。)

- [http://research.google.com/archive/bigtable.html](描述 BigTable 的论文。)

- [http://research.google.com/archive/mapreduce.html](描述 MapReduce 的论文。)

- [http://hadoop.apache.org/](Hadoop 主网站。)

- [http://hbase.apache.org/](Hbase（Hadoop 数据库）主网站。)

- [http://research.google.com/archive/gfs.html](描述 Google 文件系统的论文。)

- [http://neo4j.org/](Neo4j 主网站。)

- [http://orientdb.org/](OrientDB 主网站。)

- [http://www.hypergraphdb.org/](HyperGraphDB 主网站。)

- [https://github.com/twitter/flockdb](FlockDB 主网站。)

# 第32章 轻量级目录访问协议 (LDAP)

### 本章内容

- 配置服务器

- 配置客户端

- 管理

- 参考文献
