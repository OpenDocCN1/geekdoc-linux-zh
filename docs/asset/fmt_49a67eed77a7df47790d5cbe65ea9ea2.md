
`4 rows selected.`

# 执行简单的导出和导入操作 431

# 473 使用导出和导入的指南

# 474 考试要点

描述 TSPIT 概念。表空间点映像恢复（TSPIT）是在使用物理恢复属性恢复单个数据文件时，向克隆数据库导出元数据的操作。这主要用于大型数据库，因为对于这些数据库来说，完全恢复会非常耗时。

描述与 TSPIT 相关的参数。`TRANSPORT_TABLESPACE` 和 `DATAFILES` 参数是传输表空间功能特有的。

## 关键术语

在参加考试之前，请确保你熟悉以下术语：

- 块损坏 (block corruption)
- 常规路径导出 (conventional-path export)
- 直接路径导出 (direct-path export)
- 转储文件 (dump file)
- 导出实用 (Export utility)
- 导入工具 (Import utility)
- 逻辑备份 (logical backup)
- `PARFILE`
- 物理备份 (physical backup)
- 表空间点映像恢复 (TSPIT)

## 复习习题

- 1. 哪种类型的数据库工具执行逻辑备份？
  A. 导出 (Export)
  B. 导入 (Import)
  C. 冷备份 (Cold backup)
  D. 热备份 (Hot backup)

- 2. 哪种类型的数据库工具将转储文件读入数据库？
  A. 导出 (Export)
  B. 导入 (Import)
  C. SQL*Loader
  D. Forms

- 3. 默认的转储文件名称是什么？
  A. export.dmp
  B. expdata.dmp
  C. expdata.dmp
  D. export_data.dmp

- 4. 检查以下导出命令并确定错误的语法处。
  `exp users=ar/trar2 conventional=false tables=ra_customer_deductions`
  
  A. 第一行错误。
  B. 第二行错误。
  C. 第三行错误。
  D. 第四行错误。

- 5. 使用 TSPITR 需要哪些类型的备份？（选择所有适用项）
  A. 逻辑 (Logical)
  B. 物理 (Physical)
  C. 导入 (Import)
  D. 导出 (Export)

- 6. 读取参数文件的参数名称是什么？
  A. PARAMETER FILE
  B. PARFILE
  C. PARAFILE
  D. PAR-FILE

- 7. 使用 TSPITR 时，另一个数据库称为什么？
  A. 二级数据库 (Secondary database)
  B. 恢复数据库 (Recovery database)
  C. 克隆数据库 (Cloned database)
  D. 备份数据库 (Backup database)

- 8. 专门用于 TSPITR 的参数名称是什么？
  A. DATABASE
  B. TRANSPORT_TABLESPACE
  C. CONTROL
  D. COMPRESS

- 9. 哪种导出类型最快？
  A. 完全 (Complete)
  B. 累积 (Cumulative)
  C. 直接路径 (Direct-path)
  D. 常规路径 (Conventional-path)

- 10. 使用导出和导入工具并为大型数据库对象设计的复杂恢复方法是什么？
  A. 全量导出 (Full Export)
  B. Full=Y
  C. TPSTIR
  D. TSPITR

- 11. 哪种导出命令可以与数据库重组结合使用以提高性能？
  A. COMPRESS_EXTENT=Y
  B. COMPRESS_EXT=Y
  C. COMPRESS=Y
  D. COMPEXT=Y

- 12. 关于导出和导入工具，以下哪项是正确的陈述？
  A. 它们不能用于升级数据库。
  B. 它们可以用于升级数据库。
  C. 只有导出工具可以升级数据库。
  D. 只有导入工具可以升级数据库。

- 13. 关于在不使用任何导出关键字选项的情况下使用导出工具处理表，以下哪项是正确的陈述？
  A. 导出工具将数据加载到数据库。
  B. 导入工具从数据库中提取数据。
  C. 导出工具对表执行全选择，然后将数据转储到二进制文件中。
  D. 导出工具对表执行全选择，然后将数据转储到 ASCII 文件。

- 14. 哪一个导出关键字选项可以选择表的子集？
  A. SUBSET
  B. SELECT
  C. WHERE
  D. QUERY

- 15. 下面哪一个导出关键字选项执行完全数据库导出？
  A. ALL=Y
  B. COMPLETE=Y
  C. TOTAL=Y
  D. FULL=Y

## 复习习题答案

- 1. 导出工具执行 Oracle 数据库的逻辑备份。
- 2. 导入工具负责读取转储文件。
- 3. `expdata.dmp` 是默认的转储文件名。
- 4. 常规路径导出是默认的。`conventional=false` 行是无效语法。
- 5. A, B。TSPITR 同时执行逻辑和物理数据库备份，而导出是逻辑备份。导入不是备份；它是恢复工具。
- 6. B. `PARFILE` 是指定参数文件的参数。
- 7. C. 克隆数据库是使用 TSPITR 另一个数据库。
- 8. B. `TRANSPORT_TABLESPACE` 参数专门用于 TSPITR。它用于识别需要恢复的表。
- 9. C. 直接路径导出最快。完全和累积导出取决于数据。
- 10. D. 表空间点映像恢复 (TSPITR) 是一种使用导出和导入工具并为大型数据库对象设计的方法。
- 11. C. `COMPRESS=Y` 可以与数据库重组结合使用以提高性能。
- 12. B. 它们可以用于升级数据库。
- 13. C. 导出工具对表执行全选择，然后将数据转储到二进制文件中。
- 14. D. `QUERY` 关键字可以选择表的子集。
- 15. D. `FULL=Y` 执行完全数据库导出。

# 使用 SQL*Loader

`SQL*Loader` 是一个 Oracle 实用程序，设计用于从一个数据库加载或传输外部数据到另一个数据库。`SQL*Loader` 用于与数据库交互的其他非 Oracle 系统进行夜间提取。它已成为 Oracle 数据库构建或刷新数据仓库或数据市（Data Marts）的首选工具。这种新颖受欢迎源于它在处理 Oracle 和非 Oracle 源的大型数据集时的快速速度和多功能。

由于 `SQL*Loader` 的解析能力，它可以处理各种格式的外部文件。由于这种多功能性，你可以使用 `SQL*Loader` 执行以下操作：

- 在同一个加载会话中从多个数据文件或输入文件加载数据。
- 在同一个加载会话中将数据加载到多个表中。
- 将多个输入记录合并为一个逻辑记录进行加载。
- 指定数据的字符集。
- 接受固定长度或变长度的输入字段。
- 选择性加载数据（你可以根据记录的值加载记录）。
- 在加载前使用 SQL 函数对数据进行处理。
- 在指定的列中生成唯一的序列的键值。
- 使用操作系统的文件系统访问数据文件。
- 从磁盘、磁带或命名管道加载数据。
- 向表中追加数据并替换表中现有数据。
- 通过跳过缓冲区缓存将数据直接加载到数据块。
- 使用辅助数据文件加载大型二进制对象（LOBs）和集合。

在使用 `SQL*Loader` 时，你需要熟悉三种主要的文件结构：控制文件；日志文件（包括错误日志、丢弃日志和常规日志）；以及输入数据或数据文件。这些文件结构将在本节中详细讨论。

# 使用 SQL*Loader 447

`SQL*Loader` 还使用三种方法将数据加载到数据库——常规加载、直接路径加载和外部路径加载——并在并行模式下使用其他三种方法来进一步提高性能——并行加载、结合直接路径加载的段间并发以及结合直接路径加载的段内并发。这两组方法在接下来的几页中也得到了讨论。

# 控制文件、日志文件和输入数据或数据文件

`SQL*Loader` 的三个主要组件是控制文件、日志文件、输入数据（或数据文件）。*控制文件*是数据加载背后的逻辑，决定了如何加载加载哪些数据。*日志文件*包括错误日志、丢弃日志和常规日志。*错误日志（bad log）*记录被 Oracle 数据库拒绝的记录，或者由于格式无效、键违反或缺少必要字段而被拒绝的记录。*丢弃日志（discard log）*包含在加载过程中被丢弃或不符合控制文件加载标准的记录。*常规日志（general log）*包含加载过程的详细摘要。*数据文件*（或输入数据）是要加载的原始数据。图 15.1 显示了此利用日志、数据文件和控制文件的 `SQL*Loader` 过程。

# 图 15.1 SQL*Loader 输入和输出文件

![](img/4d4ebf1b63c52ce2a364aa79830c39e0_486_0.png)

Copyright ©2002 SYBEX, Inc., Alameda, CA www.syb.com

## 控制文件

控制文件是 `SQL*Loader` 中一个相当详细的组件，负责加载过程中的大部分功能。控制文件作用正如其名；它控制着 `SQL*Loader` 过程。控制文件在 `SQL*Loader` 过程中执行以下功能：

- 指示你找到数据
- 提供数据格式
- 存放配置和设置信息
- 告诉你好如何处理数据

实际加载的数据可以保留在文件中，但这应仅用于样本或测试加载。下面的示例显示了一个不包含输入数据的控制文件；使用 `INFILE` 参数指定的外部文件（invoice_header.dat）来引用这些输入数据。左侧的行号用于标识我们将要详细讨论的行。

```
```
