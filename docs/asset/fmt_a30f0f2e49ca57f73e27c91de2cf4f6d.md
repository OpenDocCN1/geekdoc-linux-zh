
`List<Student>` `students` = `database.query(new Predicate() return student.getAge() < 20 && student.getGrade().equals("A")`);

```
这里是 JDBC 的等效代码，如何获取一个 SQL：
```
```java
String param = "String getParam"
String filter = "age < ? and grade ="
Query query = Manager.createQuery(Student.class, filter);
Collection = Collections.executeQuery(query);
```

你看到了什么？第一个是纯粹的，第二个不是。这些字符串就像英语政策中混杂了一点中文——简单地无法理解。原生 Java 的好处是什么？我会给你两个更多的理由。

- 1. 认为年龄是一个数字是错的吗？Db40 会给你一个类型安全的方法 "`age`"。JDBC 不允许你在没有它的情况下运行，所以使用原生解决方案的生产率更高。
- 2. 如何重构——将 "`age`" 改为 "`age`" JavaScript——这在 JDBC 中是一个简单的步骤和示例。如果你使用 JDBC，比如 EQL，并且你给它们命名了，你不需要在源代码中寻找位置，你……

现在，重构增加了收益、更多性能、降低了成本和资源消耗，正如我们所知。那么如何再次提高开发效率呢？

使用 db40，你可以构建并更快领先。你如何做到？

不要误会我，我是指一种解决所有问题的方案，如何构建一个连接到数据库的应用程序。但如果不是，例如在移动应用中，没有位置，所以你需要更少的手，而不是通过 SQL 的复杂性完成所有工作，因为那里没有 db40。

当然，你可以使用 SQL 来获得性能，但不是因为它有更快的、更多的性能以及比 db40 更原生——

LJ: 你能提到一些采用 db40 的公司示例吗？他们是如何使用该产品的，这又是如何……

# 虚拟文件系统即虚拟办公文档

使用 `librbis`、`XML` 和 `XSLT` 来创建虚拟文件系统和文档。**BEN MARTIN**

文件系统可以转换为虚拟办公文档。传统的 Unix 口号“一切皆文件”结合 `xsltf/` 文件系统，允许使用 OpenOffice 透明地编辑关系型数据库以及任意 XML。

`librbis` 文件系统同时呈现了文件和数据。被视为“文件”的边界包括 PostgreSQL、LDAP 和 Firefox，以及标准的 Web 项目，如 HTTP、FTP 和 MIDI。

反向文件系统允许从其他目录合成文档。现有文件的集合允许文件系统显示这些基准（bases）的集。

OpenOffice 现在可以保存该文件。文件文件系统应用反向 XSLT 并更新输入文件系统（在此例中为 PostgreSQL）以反映你的更改。

为了支持这一点，你将拥有两个 XML 文件。第一个样式表将输入文件转换为你感兴趣的格式。第二个 XML 文件（反向样式表）提供反向转换。如果可以从转换的动作中推断出来，则第二个文件应该是可选的。

反向样式表更新每个显式的 URL 或相对路径。反向 XSLT 方法指定反向样式表来更新每个需要更新的文件的属性。这对于 URL 在源和目标中都起作用的 xslltfs 来说非常方便。例如，当你在 OpenOffice 中保存文档时，源 URI 将供反向样式表用于进行更新。

尽管 `librbis` 文件系统与 XML 模型数据之间存在差异，但它们也有许多相似之处。文件的元数据作为扩展属性（EAs）创建，这些属性映射到文件元素中的 XML 元素。文件与 XML 模型数据之间的元素差异在于，元素的顺序不保证能被保留。

反向样式表在概念上类似于对文件应用 diff（差异比较）和 patch（补丁）。反向样式表创建一个更改列表，为每个文件生成一个相对路径，然后应用补丁。反向样式表作为根元素返回一个属性，该属性可以从路径中剥离属性。如果这成立，我们可以创建新文件，其中反向样式表指定的相对路径在当前文件系统中并不存在。

由于与 XML 模型数据的关联，`librbis` 文件系统支持将每个文件视为一个文档对象（Document Object）。可以将任何文件视为 XML 文档，因为文件与 XML 之间的界限往往是模糊的。

反反文件系统可能包含当前文件系统的项目。这不是强制要求的，但如果是的话，翻译在翻译后的文件系统中将完全可用。

许多现代应用程序将其文档作为 XML。文件系统和 XML 可以通过 `librbis` 进行交换，这允许你使用 XML 编辑器编辑文件。使用 XML 编辑器编辑文件的一个缺点是，XML 文件的架构通常与文件的布局不匹配。

以下章节展示了两个用途：创建新的虚拟文件系统以及从当前文件系统编辑文档。这通常通过使用自定义文件系统处理器实现。

`xsltfs` 可用于创建一个与应用程序期望格式匹配的翻译文件。例如，你可以将 PostgreSQL 中的表作为数据库，并将该表转换为电子表格文件，然后将其加载到 OpenOffice。

图 2 所示的 `xsltf` 从输入文件创建我们的翻译文件系统。需要注意的是，在这种情况下，输入文件是由 XML 文件生成的。

当考虑到所支持的文件系统时，可能性变得更加有趣。当你对反向样式表进行一些更改后，

翻译后的文件可以像任何其他文件一样通过命令行工具（`fdisk`、`find` 等）使用。`librbis` 中的 `xsltfs/` URL 方案位于大多数其他 URL 之上。

72 | 2007 | www.linuxjournal.com

# 2007年软件开发西部会议与展览

2007年3月19-23日 | 圣塔克拉拉会议中心 | 加利福尼亚州，圣塔克拉拉

提供你所需的所有知识

早鸟优惠
在 2 月23 日前注册
立省高达 $300

周年庆！

# 14 个深度分领域，超过 200 场课程

- 软件业务
- C++
- Java
- .NET
- Ruby
- 建模与设计
- 人员、项目与方法
- 需求与分析
- 安全
- 测试与质量
- Web 2.0
- 服务/SDA
- XML

STROUSSTRUP & STUTTER 论 C++
应广受需求，再次回归：
加入 C++ 创始人 Barnes Stroustrup 和著名 C++ 专家 Herb Stutterun 一起，参加关于 C++ 的为期两天的深度教程。

# 今年新内容：RUBY, WINDOWS VISTA 和 WEB 2.0！
另有：主旨演讲、展会、兴趣小组交流、小组讨论、案例研究、圆桌会议、派对和特别活动

立即登录 WWW.SDEXPO.COM 注册

## 深度

### Listing 1. example.xml
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<root>
  <file size="200GB">
    <file>XML内部的文件系统</file>
    <file myttr="foo">蓝色的东西</file>
  </file>
</root>
```

### Listing 3. 为 example.xml 生成翻译文件系统
```
xsltfs://context/file/example.xml
```

### Listing 2. example.xsl
```xml
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output method="xml" encoding="utf-8"/>
  <xsl:template match="">
    <root>
      <xsl:apply-templates/>
    </root>
  </xsl:template>
  <xsl:template match="file3">
    <file>
      <xsl:value-of select="@url"/>="Content"
    </file>
  </xsl:template>
  <xsl:template match="file7">
    <file>
      <xsl:value-of select="@url"/>="foot"
    </file>
  </xsl:template>
</xsl:stylesheet>
```

### Listing 4. 探索我们的新文件系统
```bash
$ export LIBFERRIS_XLTSFS_SHEETS=/tmp/example
$ cd /tmp/example
$ ls
example.xml  example.xsl
$ cat xsltfs://context/file/example.xml?stylesheet=example.xml
```
输出：
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<root>
  <file name="file3">
    original-url="file:///tmp/example.xml/root/file3">XML内部的文件系统
  </file>
  <file name="file7">
    original-url="file:///tmp/example.xml/root/file7">foot
  </file>
</root>
```

## ASA 电脑
想让您的业务更具效率吗？

由双核 Xeon 处理器驱动的 ASA 服务器提供质量和可靠性，跟上您不断增长的业务。

## 为开源社区提供的硬件系统 - 自 1999 年起
(Linux, FreeBSD, NetBSD, OpenBSD, Solaris 等)

Dempsey/Westwood 服务器起价为：

- 双核 Xeon 500+ 系列
- 4GB DDR3 内存
- 支持高达 64GB FBDIMM
- 120 GB 热插拔驱动器
- 2个集成双 10/1000 局域网

$2399

双 Xeon 服务器起价为：

- 双 Xeon 2.8 GHz 800 FSB。
- 无需配的 iSCSI 或 SAS。
- 10GB SATA 硬盘 - 高达 18TB
- 52 MB RAM
- 硬盘故障 LED 指示灯。

$4139

双 Xeon 800FSB 服务器起价为：

- 双 Xeon 2.8 GHz 800 FSB
- 2TB 存储（最大 32TB）
- 8GB RAM
- 无需配的 NAS 或 iSCSI
- 2 / 10/1000 千兆局域网。

$6699

## 列表 5：example-revsl
```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:stylesheet
  xmlns:xs="http://www.w3.org/1999/XSL/Transform"
  xmlns:original="original"
  xmlns:ferris="libferris"
  exclude-prefixes="ferris"
  <xs:output method="xml"/>
  <xs:template match="">
    <xs:explicit-updates>
      <xs:apply-templates select="templates/"/>
    </xs:explicit-updates>
  </xs:template>
  <xs:template match="*[@name=file3]">
    <xs:context url="original">
      <xs:value-of select="./"/>
    </xs:context>
  </xs:template>
  <xs:template match="*[@name=file7]">
    <xs:attribute name="original">
      <xs:value-of select="./"/>
    </xs:attribute>
  </xs:template>
</xs:template>
```

当我们反转样式表时，事情会变得更有趣，如列表 5 所示。在这种情况下，我们在输入文件的 XML 属性中产生这些更改的地方进行了相当昂贵的修改。拥有隐式的反转 XSL 让您能够根据意愿仅更新原始文件的部分内容。您还可以使用函数从样式表修改数据到输入文件。

既然我们已经反转了反转 XSL，我们可以通过在 xsl 中创建虚拟文件来修改原始 XML 文件的内容，列表 6 所示。

列表 6 中的示例显示了更新虚拟文件的两种方法：更改单个虚拟文件或使用虚拟 XML 文档。更新单个文件的第一方法将样式表维护在虚拟单元中。使用虚拟 XML 文档的第二方法提供了 XSL 编辑选项，类似于 OpenOffice 那种对文档进行更新并重新打印。

URL 非常冗长且复杂。如果您经常编辑这些内容，可能希望暴露对 FUSE 的使用。使用 OpenOffice 编辑虚拟文件需要通过 Linux 内核使用 FUSE 处理虚拟文件。

## 虚拟办公文档
您的定制设备解决方案

如果 xtltfs 的格式广为人知（例如 OpenOffice.document），您可以从 XSL 文件自动创建文件格式。使用 `ferris-stylesheet-to-xtltfs` 来设置您的样式表。使用插件系统来允许新文件。

让我们知道您的需求，我们将为您提供解决方案
此处放置 Logo

| ASA 收藏 | ASA 收藏特惠 |
| :--- | :--- |
| 1 个机架 - 325GB 每月 $76 | 首月免费。 |

### 存储解决方案
IDE, SCSI, Fiber Raid 解决方案
NAS, DAS, SCSI, SATA, SAS
FJB/iSCSI/存储解决方案

### 集群
机架式和台式式节点
HP, Intel, 30cm, Cisco 交换机
Vx, 终端服务器
APC 或通用品牌

所有系统均已安装并带有用户选择的 Linux
ASA 系列—每每月 $75

2354 Calle Del Mundo,
Santa Clara, CA 95054
www.asacomputers.com
邮箱: sales@asacomputers.com
电话: 1-800-REAl-PCS | 真: 408-654-2190

Intel®, Intel Atom®, Intel Inside®, 以及 Intel logo 是 Intel 公司或其分公司在美国和其他国家的商标或注册商标。
价格和可用性可能会更改，恕另另通知。不适用于排版错误。

## 深度

## 列表 6. 通过我们的 XSLT 文件系统更改 XML 文件

## 列表 8. 设置虚拟办公文档以编辑数据库表
```bash
$ bash - psql
ben=# create database lj;
ben=# \c
您现在连接到数据库 "lj"。
lj=# create table msgs (
  id serial primary key,
  num int, msg varchar(200),
  foo varchar(80)
);
lj=# insert msgs values
(default, 7, 'This is msg #1', 'Foo is Bar');
lj=# insert msgs values
(default, 12, 'Second message', 'itski');
lj=# select msgs values
| id | num | msg | foo |
|---|---|---|---|
| 1 | 7 | This is msg #1 | Foo is Bar |
| 2 | 12 | Second message | itski |
```

## 深度解析

### 列表 10. 开发与调试新样式表
```
<context>
<root>
  $ ferris -R --xml-xslt-debug \
    --show-name.content.myattr @example.xml/root
  <xml version="1.0" encoding="UTF-8" standalone="no"?>
  <ferrisis>
  <root name="root">
    url="http://tmp/KK/example.xml/root">
    <file content="myattr" name="file">
      url="http://tmp/KK/example.xml/root/file">
      <file content="filesystem" inside XML?>
        url="http://tmp/KK/example.xml/root/file">
        <file content="Something Blue" name="file">
          url="http://tmp/KK/example.xml/root/file">
      </file>
    </file>
    </root>
  </ferrisis>
$ ferris -R --xml-xslt-debug \
    --show-name.content.myattr \
    example.xml/root > input.xml
$ ferrisXalanTransform -s example.xml -m input.xml
  transform XML input with s=example.xml
  <xml version="1.0" encoding="UTF-8"?>
  <context>
  <original name="root">
