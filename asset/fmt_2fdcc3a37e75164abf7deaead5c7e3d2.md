
# 附录 B LOBs, UDFs, UDTs 和关系型扩展

## LOBs

### 大对象—内存考虑

由于存储系统和技术的改进，存储 LOB 数据已成为可能。程序员仍然应该关注如此大量数据的数据移动。例如，如图 B.1 所示，在不需要整个 LOB 的情况下向应用程序移动 2GB 数据将浪费资源。此外，使用应用程序内存处理如此巨大的对象是不可行的。

### 大对象—操作

DB2 为程序员提供了操纵 LOB 数据的机制，以减少对性能的影响。

可以定义定位符变量来表示 LOB 或 LOB 数据的一部分（图 B.2）。定位符变量在应用程序中类似于令牌。令牌的使用允许程序员分部分检索 LOB（大对象），从而减少实际传输到应用程序中的数据量。

![](img/aa524d8157d0abd09e6f87c5b1aeab3b_432_0.png)

- 减少数据传输
- 为了性能推迟评估
- 直接文件传输
- CLI 函数

**图 B.2** 大对象——操作。

DB2 允许对 LOB 数据进行若干操作：

- 检索值或部分值
- 替换值
- 使用 LIKE 谓词
- 使用连接
- 使用标量函数 `SUBSTR`、`POSSTR` 和 `LENGTH`
- 使用 UNION ALL

在优化过程中会考虑 LOB 数据谓词的评估，并且通常会推迟执行以增强性能。在应用其他谓词以减少候选行数之前，将不会访问 LOB 数据。

文件引用变量为应用程序程序员提供了一种直接在文件和数据库之间移动 LOB 数据的方法。使用文件引用变量时无需将数据移动到程序存储中。

# DB2 关系扩展 (Relational Extenders)

Text Extender 产品的主要部分安装在与 DB2 服务器相同的机器上。一个 DB2 服务器实例只能安装一个 Text Extender 服务器实例。

在局域网（LAN）中的 Text Extender 安装非常灵活，可以包括：

- 一个或多个 Text Extender 局域网服务器（位于 AIX、OS/2、Windows NT、SUN-Solaris 或 HP-UX 工作站上）

## 416 | 附录 B：LOB、UDF、UDT 和关系扩展

- AIX、OS/2、Windows NT、Windows 95、Windows 98、Windows 3.1、Sun-Solaris 和 HP-UX 客户端，其可访问一个或多个远程 Text Extender 服务器。
- 包含本地 Text Extender 服务器并可访问远程服务器的 AIX 客户端。

要从客户端运行 Text Extender，必须首先安装 DB2 客户端和一些 Text Extender 工具。这些工具构成了 Text Extender 客户端，尽管在严格意义上它并不是一个客户端。该客户端通过 DB2 客户端连接与 Text Extender 服务器通信。

- 帮助 DB2 用户
- 处理复杂数据类型
- 提高应用程序开发效率
- 降低开发复杂度
- Text Extender
- Image Extender
- Video Extender
- Audio Extender
- XML Extender
- 额外费用：
- Net Search Extender
- Spatial Extender

图 B.3 DB2 关系扩展。

Text Extender 组件包括：

- 用于为文本搜索准备数据库、表和列的管理 CLP
- 构建文本索引并更改文本索引特性
- 设置和更改默认文档属性（如语言、格式和代码页）
- Text Extender UDFs，用于在 SQL 查询中集成全文搜索、检索文档属性以及精炼文本搜索参数
- 用于执行文本搜索、浏览结果文档（包括匹配项高亮）的编程 API (C)

Image Extender（图像扩展）可：

- 像处理传统数据一样存储和查询图像
- 支持 GIF、JPEG、BMP 和 TIFF 等多种图像格式
- 导入和导出带有大小（字节）、格式、高度、宽度和颜色数等属性的图像
- 转换图像的格式

# 附录 B：LOB、UDF、UDT 和关系扩展 | 47

- 基于相关数据或图像属性查询图像
- 生成并显示缩略图
- 图像内容查询 (QBIC) 技术，通过所见内容进行搜索、匹配颜色、匹配纹理和形状

Video Extender（视频扩展）可：

- 像处理传统数据一样存储和查询视频片段
- 导入和导出带有帧率、压缩格式和视频轨道数等属性的视频片段
- 基于相关数据或视频属性（如名称、编号、描述、视频格式和最后更新时间）查询视频片段
- 播放视频片段
- 在应用程序中创建 SQL 语句查询新闻数据库中的视频片段
- 选择主题，列出所选片段的播放时间，并允许应用程序用户播放片段
- 当录像机切换视角时，根据场景切换检测自动将视频片段分割成镜头（shots）

Audio Extender（音频扩展）可：

- 像处理传统数据一样存储和查询音频片段
- 导入和导出带有音频通道、传输时间和采样率等属性的音频片段
- 基于相关数据或音频属性（如名称、编号、描述、音频格式和最后更新时间）查询音频片段
- 播放音频片段

通过 XML Extender，您的应用程序可以：

- 将整个 XML 文档作为列数据存储在应用程序表中，或作为本地文件存储，同时将所需的 XML 元素或属性值提取到侧表中进行搜索。使用 XML 方法，您可以：
  - 对提取到侧表并索引的 SQL 通用数据类型的 XML 元素或属性进行快速搜索
  - 更新 XML 元素的内容或 XML 属性的值
  - 使用 SQL 查询动态提取 XML 元素或属性
  - 在插入和更新期间验证 XML 文档
  - 使用 Text Extender 执行结构搜索
- 使用 XML 集合存储和访问方法，使用一个或多个关系表组合或分解 XML 文档的内容。

Net Search Extender：

- 包含一个 DB2 存储过程，为 Net.Data、Java 或 CLI 应用程序添加快速全文检索功能。
- 为应用程序程序员提供多种搜索功能，如模糊搜索、词干提取、布尔操作符和分段搜索。

# Spatial Extender（空间扩展）可：

- 创建地理信息系统：空间数据的复合体
- 将空间数据与普通数据集成以允许运行查询
- 为这些表存储并索引空间数据（坐标信息）

管理支持表提供了支持，这些表包含关于图像、音频和视频的数据。这些表中的信息通常被称为元数据（metadata）。例如，扩展器维护图像的宽度、高度和颜色数，以及最后一次更新对象的人员。

管理支持表也可以以 BLOB 格式包含对象的内容，或者通过文件引用对象。

# 附录 B：LOBs、UDFs、UDTs 和关系扩展器 | 419

镜头目录（shot catalog）用于存储视频片段中镜头的数据。镜头目录可以存储在数据库或文件中。

# 用户定义唯一类型和用户定义函数

本节介绍了创建用户定义唯一类型和用户定义函数的层概述。

## 用户定义类型——必要性

- 需要为语句建立上下文
- DB2 强制类型检查

在业务世界中，数据类型不仅限于 `INTEGER` 或 `CHARACTER` 等数据类型。安装环境需要能够专门反映数据用途的数据类型。例如，图 B.4 描述了这样的情况：如果不应用单位，“限速为 100”这一语句是歧义的。每小时 100 英里**不等于**每小时 100 公里。

通过允许安装环境为数据库管理器定义数据类型，应用程序中就不需要强制类型检查的代码。数据库管理器将执行强数据类型检查，从而不允许无效的比较。这些数据类型被称为用户定义类型（UDTs）。

强数据类型对数据的即时访问也很有价值。使用查询工具的用户可能会尝试比较每小时英里和每小时公里等内容，而没有意识到自己的错误。数据库管理器可以防止此类比较。

## 用户定义类型——定义

需要 `IMPLICIT_SCHEMA` 权限或 `CREATEIN` 权限来使用与当前语句授权 ID 匹配的架构名创建唯一数据类型。要在另一个架构中创建唯一类型，需要 `SYSADM` 或 `DBADM` 或 `CREATEIN` 权限。

`CREATE DISTINCT TYPE` 语句允许安装任意数量由数据库管理器处理的数据类型。见图 B.5。

```
CREATE DISTINCT TYPE KPH AS INTEGER

WITH COMPARISONS

CREATE DISTINCT TYPE MPH AS INTEGER

WITH COMPARISONS

CREATE TABLE SPEED_LIMITS

(ROUTE_NUM SMALLINT,

CANADA_SL KPH NOT NULL,

US_SL MPH NOT NULL)

SELECT ROUTE_NUM FROM SPEED_LIMITS

WHERE CANADA_SL > KPH(80)

SELECT ROUTE_NUM FROM SPEED_LIMITS

WHERE CANADA_SL > US_SL
```
