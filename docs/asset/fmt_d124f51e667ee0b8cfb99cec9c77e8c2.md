
Create Table `statsbegin_file` Tablespace `tools`

Storage(Initial 10K Next 10K Pctincrease 10 ) As

Select *

From `stats$file_view`

Where 0 = 1;

```
```

Drop Table `statsend_file`;

Create Table `statsend_file` Tablespace `tools`

Storage(Initial 10K Next 10K Pctincrease 10 )As

Select *

From `stats$begin_file`;

```
```

Insert Into `stats$begin_file`

Select *

From `stats$file_view`;

```

在需要分析系统性能的间隔结束后，运行 I/O 脚本捕获间隔结束时的统计信息。I/O 脚本将统计信息存储在 `stat$end_file` 中。列表 22.15 是用于结束 I/O 并获取 I/O 使用报告的脚本。

## 列表 22.15 填充 `statsend_file` 并生成 I/O 使用报告的脚本

```
REM
REM End IO : 在间隔结束时捕获文件 I/O 统计的脚本。
REM
Set Term Off `stats$end_file`
Insert Into `stats$`
Select *
From `stats$file_view`;
```

```
Drop Table `statsfiles`;
Create Table `statsfiles` Tablespace `tools`
Storage(Initial 10K Next 10K Pctincrease 0)As
Select b.ts `table_space`,
b.name `file_name`,
e.pyr-b.pyr `phys_reads`,
e.prbr-b.prbr `phys_blks_rd`,
e.prt-b.prt `phys_rd_time`,
```

```
e.pyw-b.pyw `phys_writes`,
e.pbw-b.pbw `phys_blks_wr`,
e.pwt-b.pwt `phys_wrt_tim`,
(e.st_time -b.st_time)*24*60 `tot_tim`
From `stats$begin_file` b, `stats$end_file`
Where b.name=e.name;
```Drop Table `stats$begin_file`;
Drop Table `stats$end_file`;
Set Term On
Clear Screen
Set Pagesize 24
Set Feedback off
Col `table_space` Format a17
Col `file_name` Format a55
Col `phys_writes` Format 999999 'PHYS_WRS'
Col `phys_reads` Format 99999 'PHYS_RDS'
Col `phys_rd_time` Format 999999 'PHYS_RDT'
Col `phys_wrt_time` Format 999999 'PHYS_WRT'
Col `phys_blks_rd` Format 999999 'BLKS_RD'
Col `phys_blks_wr` Format 999999 'BLKS_WR'
Col `ios_sec` Format 999 'IOS_SEC'
```

```
REM
REM Generate I1
REM
Select `table_space`,
`file_name`,
`phys_reads`,
`phys_writes`,
`phys_blks_rd`,
`phys_blks_wr`,
`phys_rd_time`,
`phys_wrt_time`,
(`phys_reads` + `phys_writes`)/`tot_tim` `ios_sec`
From `stats$files`
Order By `ios_sec`
```

以下是上述 SQL 的输出。

| TABLE_SPACE | PHYS_WRS | BLKS_RD | BLKS_WR | PHYS_RDT | PHYS_WRT | IOS_SEC |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| ARMSLEDUB04_TS | `/u03/ora7/armslivebu.dbf` | 23100 | 34 | 17644 | 106 | 93 |
| ARMSLEDIVEIDX02_TS | `/u11/ora7/armsliveidx07.dbf` | 16886 | | 912 | 68 | |
| ARMSLEDIVEIDX11_TS | `/u14/ora7/armsliveidx19.dbf` | 3461 | 542 | 1288 | 2946 | 16 |
| ARMSLEDUB04_TS | `/u03/ora7/armslivebu03.dbf` | 2521 | 38 | 2131 | 255 | 10 |
| RBS2 | `/db07/ora7/rbs4.dbf` | 1 | 982 | 1 | 7890 | 4 |
| ARMLIVEIDX0_35 | `/db04/ora7/armliveidx0.dbf` | 870 | 51 | 323 | 124 | 4 |
| ARMLIVETMP0_15 | `/db06/ora7/armlivetmp01.dbf` | 866 | 1 | 24729 | 1 | 1402 | 3 |
| ARMLIVEDB2_15 | `/u03/ora7/armslivebu19.dbf` | 157 | 157 | 323 | 32 | 1065 | 2 |
| ARMLIVEDB11_75 | `/u09/ora7/armslivebu16.dbf` | 87 | 331 | 273 | 30 | 1693 | 2 |
| ARMLIVEIDX10_75 | `/u16/ora7/armliveidx17.dbf` | 137 | 25 | 25 | 69 | 66 | 1 |
| SYSTEM | `/u01/ora7/syst1ora7.dbf` | 63 | 23 | 79 | 31 | 204 | 0 |
| SYSTEM | `/u01/ora7/syst2ora7.dbf` | 34 | 37 | 12 | 11 | 90 | 0 |
| ARMLIVEDB02_75 | `/db06/ora7/armliv06.dbf` | 7 | 32 | 7 | 32 | 1 | 203 |

从此 I/O 概览可以看出，系统存在某些 I/O 活动，影响的表空间是 `ARMLIVEDB04_TS`。该表空间的读写速率每秒约为 93。根据磁盘支持的速率，可以确定获得的值是否高。观察到系统中存在高活动后，你现在可以标识产生这些高 I/O 的设备。

你也可以在 UNIX 系统上使用 `sar` 命令获取操作系统层采样概览。列表 22.16 中的 `sar` 命令每 5 秒对磁盘活动进行 3 次采样。

# 文件 I/O（磁盘访问） 399

| | | | | | | |
| c3t4d0 | 7.19 | 0.50 | 9 | 150 | 5.27 | 7.68 |
| c3t5d0 | 0.40 | 0.50 | | 6 | 3.80 | 9.32 |
| c0t6d0 | 0.20 | 0.50 | 0 | 1 | 6.42 | 11.56 |
| c0t5d0 | 72.60 | 1.79 | 186 | 2980 | 8.59 | 5.09 |
| c0t4d0 | 6.20 | 0.50 | 7 | 115 | 5.48 | 8.48 |
| c0t3d0 | 8.60 | 0.50 | 7 | 112 | 5.19 | 13.32 |
| c3d2d0 | 6.20 | 0.50 | 27 | 438 | 5.12 | 2.42 |
| c4t6d1 | 15.40 | 1.52 | 25 | 394 | 9.70 | 16.09 |
| c3t5d0 | 3.60 | 0.50 | 3 | 42 | 4.40 | 14.15 |
| c3t4d0 | 5.00 | 0.50 | | 6 | 5.63 | 7.49 |
| 19:43:15 | 73.20 | 1.86 | 184 | 2947 | 9.44 | 5.38 |
| c0t4d0 | 12.00 | 0.50 | 14 | 221 | 5.05 | 9.26 |
| c0t3d0 | 8.60 | 0.50 | 66 | 99 | 5.31 | 12.99 |
| c3d2d0 | 6.40 | 0.50 | 27 | 435 | 5.31 | 2.33 |
| c4t6d1 | 14.40 | 1.33 | 23 | 365 | 10.21 | 14.72 |
| c4t5d0 | 4.20 | 0.50 | 5 | 51 | 5.38 | 13.08 |
