
## rmiregistry

### 名称

rmiregistry - 在当前主机的指定端口上启动远程对象注册表。

### 语法

**rmiregistry** [ *port* ]

- **port**
  在当前主机上启动远程对象注册表的**端口**号。

### 描述

**rmiregistry** 命令在当前主机的指定端口上创建并启动一个远程对象注册表。如果省略端口号，则注册表将在端口 1099 上启动。**rmiregistry** 命令不产生输出，通常以后台方式运行，例如：

```
rmiregistry &
```

远程对象注册表是一种引导命名服务，用于同一主机上的 RMI 服务器将远程对象绑定到名称。本地和远程主机上的客户端随后可以查找远程对象并进行远程方法调用。

该注册表通常用于定位应用程序需要调用方法的首个远程对象。该对象随后提供特定于应用程序的支持，以便查找其他对象。

使用 `java.rmi.registry.LocateRegistry` 类的方法可以获取在本地主机或本地主机及端口上运行的注册表。

`java.rmi.Naming` 类的基于 URL 的方法操作注册表，可用于在任何主机和主机上查找远程对象。将简单名称（字符串）绑定到远程对象，将新名称重新绑定到远程对象（覆盖旧绑定），解除远程对象的绑定，以及列出注册表中绑定的 URL。

### 选项

-J
与任何 Java 选项一起使用，将 -J 之后的选项（-J 和选项之间没有空格）传递给 Java 解释器。

### 参见

- `java.rmi.registry.LocateRegistry` 类描述
- `java.rmi.Naming` 类描述

## RNGTEST

### 名称

rngtest - 使用 FIPS 140-2 测试检查数据的随机性

### 语法

```
rngtest [-c n | —blockcount=n] [-b n | —blockstats=n] [-t n | —tidstats=n] [-p | —pipe] [ -? ] [ —help] [-V] [ —version]
```

### 描述

*rngtest* 每次处理 20000 位的块，使用 FIPS 140-2（2001-10-10 勘误表）测试来验证数据块的随机性。

它从 *stdin* 读取输入，并将统计信息输出到 *stderr*，可选地将通过 FIPS 测试的数据块回显到 *stdout*（当以 *管道模式* 运行时）。错误发送到 *stderr*。

启动时，当以 *管道模式* 运行时，*rngtest* 会丢弃数据的前 32 位。它会将接下来的 32 位数据用于引导 FIPS 测试（即使不是以 *管道模式* 运行时也是如此）。这些位不会测试随机性。

当程序退出时，统计信息被转储到 *stderr*。

### 选项

**-p**, **—pipe**
启用 *管道模式*。所有通过 FIPS 测试的数据块都会回显到 *stdout*，并且 *rngtest* 以静默模式运行。

**-c n**, **—blockcount=n** (默认: 0)
处理完 n 个输入块后退出，如果 n 不为零。

**-b n**, **—blockstats=n** (默认: 0)
如果 n 不为零，每 n 个块输出一次统计信息。

**-t n**, **—tidstats=n** (默认: 0)
如果 n 不为零，每 n 秒输出一次统计信息。

**-?**, **—help**
给出所有程序选项的简短摘要。

**-V**, **—version**
打印程序版本

### 统计信息

当 *rngtest* 退出时以及被 *blockstats* 或 *tidstats* 指示时，会将统计信息转储到 *stderr*。

**FIPS 140-2 成功** 和 **FIPS 140-2 失败** 统计被 FIPS 140-2 测试接受或拒绝的 20000 位块的数量。其他统计信息显示 FIPS 140-2 测试中 FIPS 140-2 失败的详细情况。有关更多信息，请参阅 FIPS 140-2 文档（请注意，这些测试是在 FIPS 140-1 和 FIPS 140-2 2001-10-10 勘误表中定义的。它们在 FIPS 140-2 2002-12-03 勘误表中被移除）。

速度统计是针对每个传输或处理的 20000 位块获取的。

### 退出状态

- 如果没有发生错误，并且没有块未通过 FIPS 测试，则为 **0**。
- 如果没有发生错误，但至少有一个块未通过 FIPS 测试，则为 **1**。
- 如果参数存在问题，则为 **10**。
- 如果发生输入/输出错误，则为 **11**。
- 如果发生操作系统或资源匮乏错误，则为 **12**。

### 参见

(4), (8)

FIPS PUB 140-2 加密模块的安全要求，NIST，

### 作者

Henrique de Moraes Holschub <>

## roqet

### 名称

roqet - Rasqal RDF 查询实用工具

### 语法

**roqet [OPTIONS] <query-URI> [base-URI]**

**roqet [OPTIONS]** -e query-string [base-URI]

**roqet [OPTIONS]** -p sparql-protocol-service-URI [-e query-string] [base-URI]

**roqet [OPTIONS]** -t query results file [base-URI]

### 描述

**roqet** 实用工具允许使用 **Rasqal** RDF 查询库查询 RDF 内容，并以多种格式打印变量绑定、RDF 图或布尔结果的结果。查询从 *query-URI* 读取，如果存在，可选的 *base-URI* 用作查询的基本 URI。

### 主要选项

roqet 使用标准的 GNU 命令行语法，如果 `getopt_long` 函数支持，则长选项以两个破折号（`--`）开头。否则仅可用短选项。

- **-e, --exec QUERY**
  执行参数 *QUERY* 中的查询字符串，而不是从 URI 读取查询（当未提供 *-e* / *--exec* 时）。

- **-i, --input LANGUAGE**
  将输入查询 *LANGUAGE* 设置为受支持的语言之一，包括 ‘sparql’（用于 RDF 的 SPARQL 查询语言，默认）、‘sparql11’ 和 ‘laqrs’。支持的完整语言和子集列表在 *-h* / *--help* 选项的帮助摘要中给出。

- **-p, --protocol SERVICE-URI**
  调用 SPARQL HTTP 协议 *SERVICE-URI* 来执行查询，而不是在本地 Raskal 查询引擎内部执行（当提供 *-e* 或查询字符串时）。

- **-r, --results FORMAT**
  设置查询结果输出 *FORMAT*。

  对于变量绑定，*FORMAT* 的值取决于 Raskal 支持的内容，但包括 ‘simple’（简单文本格式，默认）、‘x’（SPARQL 查询结果 XML 格式）、‘csv’（SPARQL CSV）、‘tsv’（SPARQL TSV）、‘rdfx’ 和 ‘turtle’（RDF 语法格式），以及 ‘json’（结果的 JSON 版本）。

  对于 RDF 图结果，*FORMAT* 的值为 ‘ntriples’（N-Triples，默认）、‘rdfx-abbrev’（RDF/XML 缩写）、‘rdfx’（RDF/XML）、‘turtle’（Turtle）、‘json’（RDF/JSON 资源中心）、‘json-triples’（RDF/JSON 三元组）或 ‘rss-1.0’（RSS 1.0，也是一种 RDF/XML 语法）。

  具体的格式列表取决于构建时包含的内容 (3)，但在带有 -h 的使用消息中给出正确的格式。

- **-R, --results-input-format FORMAT**
  设置查询结果输入 *FORMAT*。

  这用于与 *-t* 配合使用，取值包括 ‘x’（SPARQL 查询结果 XML 格式）、‘csv’（SPARQL CSV）、‘tsv’（SPARQL TSV），以及 ‘turtle’ 和 ‘rdfx’（RDF 语法格式）。

- **-t, --results-input FILE**
  从 *FILE* 读取查询结果。

### 其他选项

- **-c, —count**
  仅统计三元组，不产生其他输出。

- **-d, —dump-query FORMAT**
  以给定的 FORMAT（‘none’（默认）、‘debug’、‘structure’ 或 ‘sparql’ 之一）打印解析后的查询。

- **-D, —data URI**
  添加 RDF 数据源 URI（不是 nad 图）。如果未提供数据源，则查询本身指向数据，例如通过 SPARQL FROM uri 语句。

- **-E, —ignore-errors**
  不打印错误消息，并且不以非 0 状态退出。

- **-f, —feature NAME(=VALUE)**
  将查询功能 NAME 设置为 VALUE，如果省略则为整数 1。已知功能可以通过 -f help 或 —feature help 显示。

- **-F, —format NAME**
  为后续使用 -D / —data 或 -G / —nad 调用的数据图设置数据源格式名称。如果未指定此项，默认情况下由查询引擎猜测。名称是 Raptor 解析器名称。

- **-G, —nad URI**
  添加 RDF 数据源 URI（nad 图）。

- **-h, —help**
  显示选项摘要。

- **-n, —dryrun**
  准备查询但不执行。

- **-q, —quiet**
  不显示额外信息消息。

- **-s, —source URI**
  通过将其添加到查询数据源 URI 列表来添加 RDF 数据源 URI（nad 图）URI。将 FORMAT 设置为 ‘simple’（默认）或 ‘x’（一种实验性 XML 格式）。

- **-v, —version**
  打印 rasqal 库版本并退出。

- **-W, —warnings LEVEL**
  将警告级别设置为 0（不发出任何警告）到 100（显示每个警告）之间的 LEVEL。Rasqal 的默认值在中间（50）。

![](img/b04156a389f578b95caf90c5a4f92a7a_865_0.png)

