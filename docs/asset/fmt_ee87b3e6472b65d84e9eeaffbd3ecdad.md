
SQL*Loader: Release 8.0.3.0 - Production on Wed Mar 10 8:10:23 1999

(c) Copyright 1997 Oracle Corporation. All rights reserved.

提交点到达 - 逻辑记录数 23

# 列表 31.8 load1.ctl-示例1 日志文件内容

SQL*Loader: Release 8.0.3.0 - Production on Wed Mar 10 8:11:03 1999

(c) Copyright 1997 Oracle Corporation. All rights reserved.

+   控制文件: `load1.ctl`

数据文件: `cust.dat`

坏文件: `load1.bad`

丢文件: `load1.dis`

(允许所有丢弃)

加载数量: ALL

跳过数量: 0

允许错误: 50

绑定数组: 64 行，最大 65536 字节

继续: 未指定

所使用的路径: 常规

表 `CUSTOMER`，已从每个逻辑记录加载。

此表生效的插入选项为：INSERT

| 列名 | 位置 | 长度 | 终止 | 数据类型 |
|---|---|---|---|---|
| CUST_NBR | 1:7 | 7 | | CHARACTER |
| CUST_NAME | | 8:27 | 20 | CHARACTER |
| CUST_ADDR1 | | 28:47 | 20 | CHARACTER |
| CUST_CITY | | 48:69 | 20 | CHARACTER |
| CUST_STATE | | 70:79 | 10 | CHARACTER |
| CUST_ZIP | | 88:91 | 12 | CHARACTER |
| CUST_PHONE | | 100:108 | 9 | CHARACTER |
| CUST_BIRTHDAY | | | | DATE-MON-YY |

如果 `CUST_NAME` 为空，则 `CUST_NAME` 为 NULL

如果 `CUST_ADDR1` 为空，则 `CUST_ADDR1` 为 NULL

如果 `CUST_CITY` 为空，则 `CUST_CITY` 为 NULL

如果 `CUST_STATE` 为空，则 `CUST_STATE` 为 NULL

如果 `CUST_ZIP` 为空，则 `CUST_ZIP` 为 NULL

如果 `CUST_PHONE` 为空，则 `CUST_PHONE` 为 NULL

如果 `CUST_BIRTHDAY` 为空，则 `CUST_BIRTHDAY` 为 NULL

记录 2：拒绝 - 表 `CUSTOMER`，列 `CUST_BIRDAY` 错误

ORA-01847: 月份必须在 1 和最后一天之间

* 成功加载 2 行。
* 因数据错误未加载 行。
* 所有 WHEN 子句失败，未加载行。
* 因所有字段为空，未加载行。

# 查看 SQL*Loader 示例

绑定数组分配的空间: 64 行

绑定数组以外的内存空间:

跳过的逻辑记录: 0

读取的逻辑记录: 23

拒绝的逻辑记录: 1

丢弃的逻辑记录: 0

开始于 1999 年 3 月 10 日 8:11:03

结束于 1999 年 3 月 10 日 8:11:03

耗用时间: 00:00:00.21

CPU 时间: 00:00:00.04

示例 1 注：记录 2 因为日期无效被拒绝并写入坏文件 (`load1.bad`)。可以通过对控制文件进行以下更改将坏文件作为输入文件并添加 INTO TABLE 来修复此记录：注意控制文件中的 NULL 子句。空白记录将会失败。

# 示例 2—加载变长度数据

此示例将 `acct.dat` 文件中的数据加载到 customer 表。由于数据是变长度格式，控制文件定义了区分数据项的隔符。

# 列表 31.9 LOAD2.CTL—示例 2 控制文件

```
LOAD DATA
INFILE 'acct.dat'
TO TABLE account
FIELDS TERMINATED BY ',' 可选由 '*' 包围
(cust_nbr, acct_nbr, acct_name)
log=load2.log bad=load2.bad
discard=load2.dis
```

在提示符处为示例 2 调用 SQLLoader 如下：

`$ sqlldr example/expass control=load2.ctl log=load2.log bad=load2.bad`

以下是服务器的响应：

SQL*Loader: Release 8.0.3.0 - Production on Wed Mar 10 8:15:51 1999

(c) Copyright 1997 Oracle Corporation. All rights reserved.

提交点到达 - 逻辑记录数 12

# 列表 31.10 示例 2 日志内容

SQL* Loader: Release 8.0.3.0 - Production on Wed Mar 10 8:16:03 1999

(c) Copyright 1997 Oracle Corporation. All rights reserved.

```
控制文件: load2.ctl
数据文件: acct.dat
坏文件: load2.bad
丢文件: load2.dis
(允许所有丢弃)

加载数量: ALL
跳过数量: 0
允许错误: 50
绑定数组: 64 行，最大 65536 字节
继续: 未指定
所使用的路径: 常规
```

表 `ACCOUNT`，已从每个逻辑记录加载。

此表生效的插入选项为：INSERT

| 列名 | 位置 | 长度 | 包围数据类型 |
| --- | --- | --- | --- |
| CUST_NBR | FIRST | | O(0*) CHARACTER |
| ACCT_NBR | NEXT | | O(0*) CHARACTER |
| ACCT_NAME | NEXT | | O(0*) CHARACTER |

表 `ACCOUNT`:

成功加载 12 行。

- 因数据错误未加载行。
- 所有 WHEN 子句失败，未加载行。
- 因所有字段为空，未加载行。

绑定数组分配的空间:

绑定数组以外的内存空间:

跳过的逻辑记录: 0

读取的逻辑记录: 12

拒绝的逻辑记录: 0

丢弃的逻辑记录: 0

开始于 1999 年 3 月 10 日 8:16:03

结束于 1999 年 3 月 10 日 8:16:28

```
耗用时间: 00:00:00.23
CPU 时间: 00:00:00.04
```

示例 2 注：所有记录成功加载。记住变长度数据必须有隔符来分隔输入数据文件中的数据项。当使用隔符字符数据时，定义每个数据字段的最大长度更有效。在本示例中，控制文件中应使用 `acct_name char(20)`。如果没有定义最大长度，SQL*Loader 将默认使用 255 字节作为长度，这会影响每次执行绑定数组时插入的记录数。

# 示例 3–使用嵌入数据加载

此示例显示数据不必在数据文件中；它可以直接嵌入到控制文件中。BEGINDATA 关键字表示其之后的所有行都是作为此控制文件输入源的数据记录。

# 列表 31.11 LOAD3.CTL–示例 3 控制文件

```
LOAD DATA
INFILE *
APPEND
INTO TABLE account
FIELDS TERMINATED BY ',' 可选由 '*' 包围
(cust_nbr, acct_nbr, acct_name)

BEGINDATA

000324,89073,SAVINGS
000324,89074,CHECKING
000075,111,SAVINGS
001102,600,CHECKING
000068,23368,CHECKING
```

在提示符处为示例 3 调用 SQLLoader 如下：

`$ sqlldr /example/expass control=load3.ctl log=load3.log bad=load3.bad`

`discard=load3.dis`

以下是服务器的响应：

SQL*Loader: Release 8.0.3.0 - Production on Wed Mar 10 8:20:11 1999

(c) Copyright 1997 Oracle Corporation. All rights reserved.

提交点到达 - 逻辑记录数 5

# 列表 31.12 示例 3 日志内容

SQL* Loader: Release 8.0.3.0 - Production on Wed Mar 10 8:21:21 1999

(c) Copyright 1997 Oracle Corporation. All rights reserved.
