
`roqet [OPTIONS] <query-URI> [base-URI]`

`roqet [OPTIONS]` -e `query-string` `[base-URI]`

`roqet [OPTIONS]` -p `sparql-protocol-service-URI` `[-e query-string] [base-URI]`

`roqet [OPTIONS]` -t `query results file` `[base-URI]`

### 描述

`roqet` 实用工具允许使用 `Rasqal` RDF 查询库查询 RDF 内容，并以多种格式打印变量绑定、RDF 图或布尔结果的结果。查询从 `query-URI` 读取，如果存在，可选的 `base-URI` 用作查询的基本 URI。

### 主要选项

`roqet` 使用标准的 GNU 命令行语法，如果 `getopt_long` 函数支持，则长选项以两个破折号（`--`）开头。否则仅可用短选项。

- `-e`, `--exec QUERY`

  执行参数 `QUERY` 中的查询字符串，而不是从 URI 读取查询（当未提供 `-e` / `--exec` 时）。

- `-i`, `--input LANGUAGE`

  将输入查询 `LANGUAGE` 设置为受支持的语言之一，包括 `'sparql'`（用于 RDF 的 SPARQL 查询语言，默认）、`'sparql11'` 和 `'laqrs'`。支持的完整语言和子集列表在 `-h` / `--help` 选项的帮助摘要中给出。

- `-p`, `--protocol SERVICE-URI`

  调用 SPARQL HTTP 协议 `SERVICE-URI` 来执行查询，而不是在本地 Raskal 查询引擎内部执行（当提供 `-e` 或查询字符串时）。

- `-r`, `--results FORMAT`

  设置查询结果输出 `FORMAT`。

  对于变量绑定，`FORMAT` 的值取决于 Raskal 支持的内容，但包括 `'simple'`（简单文本格式，默认）、`'x'`（SPARQL 查询结果 XML 格式）、`'csv'`（SPARQL CSV）、`'tsv'`（SPARQL TSV）、`'rdfx'` 和 `'turtle'`（RDF 语法格式），以及 `'json'`（结果的 JSON 版本）。

  对于 RDF 图结果，`FORMAT` 的值为 `'ntriples'`（N-Triples，默认）、`'rdfx-abbrev'`（RDF/XML 缩写）、`'rdfx'`（RDF/XML）、`'turtle'`（Turtle）、`'json'`（RDF/JSON 资源中心）、`'json-triples'`（RDF/JSON 三元组）或 `'rss-1.0'`（RSS 1.0，也是一种 RDF/XML 语法）。

  具体的格式列表取决于构建时包含的内容 `(3)`，但在带有 `-h` 的使用消息中给出正确的格式。

- `-R`, `--results-input-format FORMAT`

  设置查询结果输入 `FORMAT`。

  这用于与 `-t` 配合使用，取值包括 `'x'`（SPARQL 查询结果 XML 格式）、`'csv'`（SPARQL CSV）、`'tsv'`（SPARQL TSV），以及 `'turtle'` 和 `'rdfx'`（RDF 语法格式）。

- `-t`, `--results-input FILE`

  从 `FILE` 读取查询结果。

### 其他选项

- `-c`, `—count`

  仅统计三元组，不产生其他输出。

- `-d`, `—dump-query FORMAT`

  以给定的 `FORMAT`（`'none'`（默认）、`'debug'`、`'structure'` 或 `'sparql'` 之一）打印解析后的查询。

- `-D`, `—data URI`

  添加 RDF 数据源 URI（不是 nad 图）。如果未提供数据源，则查询本身指向数据，例如通过 SPARQL `FROM uri` 语句。

- `-E`, `—ignore-errors`

  不打印错误消息，并且不以非 0 状态退出。

- `-f`, `—feature NAME(=VALUE)`

  将查询功能 `NAME` 设置为 `VALUE`，如果省略则为整数 1。已知功能可以通过 `-f help` 或 `—feature help` 显示。

- `-F`, `—format NAME`

  为后续使用 `-D` / `—data` 或 `-G` / `—nad` 调用的数据图设置数据源格式名称。如果未指定此项，默认情况下由查询引擎猜测。名称是 Raptor 解析器名称。

- `-G`, `—nad URI`

  添加 RDF 数据源 URI（nad 图）。

- `-h`, `—help`

  显示选项摘要。

- `-n`, `—dryrun`

  准备查询但不执行。

- `-q`, `—quiet`

  不显示额外信息消息。

- `-s`, `—source URI`

  通过将其添加到查询数据源 URI 列表来添加 RDF 数据源 URI（nad 图）URI。将 `FORMAT` 设置为 `'simple'`（默认）或 `'x'`（一种实验性 XML 格式）。

- `-v`, `—version`

  打印 `rasqal` 库版本并退出。

- `-W`, `—warnings LEVEL`

  将警告级别设置为 0（不发出任何警告）到 100（显示每个警告）之间的 `LEVEL`。Rasqal 的默认值在中间（50）。

![](img/b04156a389f578b95caf90c5a4f92a7a_865_0.png)

### 示例

```
roqet sparql-query-file.rq
```

运行包含在本地文件 `sparql-query-file.rq` 中的 SPARQL 查询。所使用的数据将在查询文件的 `FROM` 语句中描述。

```
roqet -q -i sparql
```

运行位于 Web 上 URI 处的 SPARQL 查询，且无额外消息（安静模式，-q）。

```
roqet -q query-file.rq
```

从本地文件 `query-file.rq` 运行查询（默认语言为 SPARQL），但使用基本 URI 解析任何相对 URI。

```
roqet -q -i sparql -r x
```

运行位于 Web 上 URI 处的 SPARQL 查询，并将结果格式化为 SPARQL 查询结果 XML 格式，且无额外消息。

```
roqet -i sparql -e ‘SELECT * WHERE { ?s ?p ?o }’-D stuff.rdf
```

针对文件 `stuff.rdf` 中的数据运行在命令行中给出的 SPARQL 查询。文件类型将被猜测，且可能为 RDF/XML 格式。

```
roqet -t result.srx -r ht
```

读取以 SPARQL 查询结果 XML 格式（默认）存储的 SPARQL 查询结果，并以 HTML 格式打印。

```
roqet -t result.ttl -R turtle -r csv
```

读取以 RDF/Turtle 格式存储的 SPARQL 查询结果，并以 CSV 格式打印。

### 符合性

*SPARQL 1.1 查询语言*，Steve Harris 和 Andy Seaborne（编辑），W3C 推荐标准，2013年3月21日

*SPARQL 查询结果 XML 格式（第二版）*，Sandro Hawke（第二版编辑），Jeen Broekstra 和 Dave Beckett（编辑），W3C 推荐标准，2013年3月21日。

### 参见

`(3),(3)`

### 更改记录

### 作者

Dave Beckett -

### RPCCLIENT

### 名称

`rpcclient` - 用于执行客户端侧 MS-RPC 功能的工具

### 概要

```
rpcclient [-Aauthfile] [-c<commandstring>] [-dddebuglevel] [-llogdir] [-N] [-s<sconconfigfile>] [-Uusername[%password]] [-Wworkgroup] [-IdestinationIP] {server}
```

### 描述

该工具是 s 套件的一部分。

`rpcclient` 最初是一个用于测试 s 自身中 MS-RPC 功能的实用工具。它已经过几个开发阶段，并达到了稳定状态。如今，许多系统管理员围绕它编写脚本，以从他们的 UNIX 工作站管理 Windows NT 客户端。

### 选项

- `server`

  要连接的服务器的 NetBIOS 名称。服务器可以是任何 SMB/CIFS 服务器。名称使用 s 中的 `name resolve order` [] 行进行解析。

- `-c|—command=<command string>`

  执行以分号分隔的命令（如下所列）

- `-I|—dest-ip IP-address`
