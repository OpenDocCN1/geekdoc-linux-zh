
在处理每个参数 URL 时，服务器将每个参数化 URL 发送到相应的数据库服务器，服务器返回一个或多个 SQL 查询的结果。每个结果集都经过格式化并插入 HTML 文档（您的自定义主页）中。在处理完所有的可配置组件后，生成的 HTML 文档作为您的自定义主页呈现给您。

如果没有个性化编辑，将创建并呈现默认网页。

## 现代进展

数据库和应用程序技术的发展给数据库带来了许多根本性变化，其中许多对开源数据库尤为重要。

## 开放标准时代

过去，软件行业的每个有意义的标准都是某个特定供应商事实上的市场胜利。这在数据库领域尤其如此，供应商试图通过自己的专有功能来锁定客户，以确保可预测的市场基础。SQL 等开放数据库标准的出现是一个漫长、充满争吵且非常有政治色彩的过程，直到最近，DBMS 供应商才致力于实现 SQL 兼容性。在不同部门或不同应用程序中使用不同数据库产品的组织经常发现自己面临严重的维护和互操作性问题。

幸运的是，开发者和终端用户的需求营造了一种氛围，使厂商面临着创建和遵循行业范围内标准的压力。SQL 持续发展，对象数据库也已经出现了相关标准。XML（可扩展标记语言）和 Java 等技术从一开始就受到机构的推动（尽管伴随着大量的政治斗争，尤其是 Java 领域），它们现在正在改变数据库技术和实践。

开放标准对最近的“开源”这一现象也大有裨益。在专有标准时代，开源解决方案（OSS）开发者通常必须猜测或通过逆向工程来实现与商业工具的协议互操作性，这极大地减慢了开发过程。有了开放标准，OSS 开发者有了一个文档良好的编程目标，他们可以专注于更有趣的问题。几乎每个成功的 OSS 项目都享到了核心行业标准的益处。

- Linux 遵循 POSIX 操作系统标准，该标准由 ANSI 管理。
- Apache 实现了 HTTP（超文本传输协议），该协议由 IETF 标准化。
- Mozilla 实现了 HTML 和 CSS（级联样式表），这是世界维网联盟（W3C）建议的规范。
- XFree86 实现了 X11 显示标准，该标准由 The Open Group 维护。
- GNOME 和 KDE 都使用基于 CORBA（公共对象请求代理架构）的分布式编程工具，这是 OMG 的标准。
- 当然，PostgreSQL 和 MySQL 实现了 ANSI SQL 以及 Java 数据库连接（JDBC）。

开放标准通过提高生产力和缩短开发周期，让包括厂商在内的所有人受益。如果没有在大多数 Linux 数据库中使用的这些标准，就不可能在一本书中对七种产品进行深度介绍。

## 可扩展标记语言

XML 作为一种通用文档和数据的标准格式，作为 HTML 的替代品赢得了大量媒体关注，因为它能够在互联网上实现更好的搜索、分类和链接，但对于数据库用户来说，它的意义远不止此。

XML 的重要性在于，有这么多厂商和开发者已经接受了它作为一种数据格式。这为软件组件之间的互操作提供了巨大的推动，使得许多以前需要定制、专用软件完成的工作现在可以通过现成工具完成。

许多数据库正在转向支持 XML，以便用户能够以丰富的格式在数据库中存储文档，并提供在软件组件之间传输结构化数据的方法。这种应用被称为序列化。我们在示例中使用的关系型数据库的一种可能的 XML 序列化如下：

```xml
<xml version="1.0"?>
<Database>
  <Table name="Employee">
    <Row>
      <Column name="id" type="int4">101</Column>
      <Column name="name" type="string">Manny Vegas</Column>
      <Column name="birthday" type="datetime">1950-05-10</Column>
      <Column name="dept" type="int4">12</Column>
    </Row>
    <Row>
      <Column name="id" type="int4">102</Column>
      <Column name="name" type="string">Carla Wong</Column>
      <Column name="birthday" type="datetime">1961-12-02</Column>
      <Column name="dept" type="int4">15</Column>
    </Row>
    <Row>
      <Column name="id" type="int4">103</Column>
      <Column name="name" type="string">Arnold Page</Column>
      <Column name="birthday" type="datetime">1965-08-21</Column>
      <Column name="dept" type="int4">15</Column>
    </Row>
  </Table>
  <Table name="Department">
    <Row>
      <Column name="id" type="int4">12</Column>
      <Column name="name" type="string">Accounting</Column>
      <Column name="city" type="string">Miami</Column>
    </Row>
    <Row>
      <Column name="id" type="int4">12</Column>
      <Column name="name" type="string">Human Resources</Column>
      <Column name="city" type="string">Gainesville</Column>
    </Row>
  </Table>
</Database>
```

高级关系型或对象数据库生成的数据的自然视图可能像这样：

```xml
<?xml version="1.0"?>
<company name="Penguin Inc">
  <employee id="101">
    <name>Manny Vegas</name>
    <birthday>1950-05-10</birthday>
    <dept>12</dept>
  </employee>
  <employee id="102">
    <name>Carla Wong</name>
    <birthday>1961-12-02</birthday>
    <dept>15</dept>
  </employee>
  <employee id="103">
    <name>Arnold Page</name>
    <birthday>1965-08-21</birthday>
    <dept>15</dept>
  </employee>
  <department id="12">
    <name>Accounting</name>
    <city>Miami</city>
  </department>
  <department id="15">
    <name>Human Resources</name>
    <city>Gainesville</city>
  </department>
</company>
```

关系模型发展出了两套用于操作关系的系统：关系代数和关系演算法。代数是规范性的——也就是说，它描述了你可以在关系上执行的操作。关系演算法是描述性的——也就是说，它定义了一个视图，而不涉及其如何构建的详细细节。

演算法和代数是等价的——其中一种语言的任何语句都可以转换为另一种语言的等价语句。演算法和代数都是查询语言的基础；如果一种语言可以在不使用循环的情况下表达关系代数中可以表达的任何表达式，那么这种语言就是相对完备的。

关系模型使用 NULL 来处理属性值未知的情况。保证 NULL 不等于任何域中的任何值；因此，将任何值与 NULL 比较的结果始终为假。从逻辑上讲，NULL 既不是 TRUE 也不是 FALSE；因此，关系语言中的语句必须使用三值逻辑进行求值。

数据库必须保护其结构以及所包含数据的完整性。结构完整性确保每个外键都指向一个存在的行。数据完整性意味着确保数据不包含不可能的值，而这种不可能性部分是由关系中的其他其他数据决定的。

在抽象的关系模型与其软件实现之间存在着差距。E. F. Codd 定义了 12 条规则，用于衡量一个系统到底多是关系数据库管理系统。

我们将关系数据库与层次型、网络型和面向对象的数据库进行了比较。Linux 数据库中这些技术有许多变体，我们将在后面的章节中讨论，但大多数属于 ORDBMS（对象关系数据库管理系统）类别。

新技术和发展不断改变数据库世界，Linux 用户无疑是行业进步的受益者。

接下来，我们将讨论你可能需要用 Linux DBMS 管理的数据分类，并尝试根据你的特定需求建议一种策略。
