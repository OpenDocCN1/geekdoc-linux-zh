
# Measuring Datafile I/O

Measuring the physical I/O performance of the Datafiles in the database can be done using the V$FILESTAT and V$DATAFILE dynamic performance views, the output from STATSPACK and REPORT.TXT, and the output from the OEM Performance Manager GUI tool.

**Oracle Objective**
Diagnose tablespace usage problems

## Using V$FILESTAT, V$DATAFILE, and V$TEMPFILE to Measure Datafile I/O

The V$FILESTAT, V$DATAFILE, and V$TEMPFILE dynamic performance views can be used to monitor the performance of the read and write activity against the individual Datafiles and tablespaces in the database. A description of selected columns from these three views appears in Tables 8.2, 8.3, and 8.4.

**TABLE 8.2** Description of Selected V$FILESTAT Columns

| Column Name | Description |
| :--- | :--- |
| FILE# | The Datafile's internal identifier assigned by Oracle at tablespace creation |
| PHYRDS | Number of physical reads done on that Datafile |
| PHYWRts | Number of physical writes done to that Datafile |
| AVGIOTIM | AVERAGE TIME, IN MILLISECONDS, SPENT PERFORMING I/O on that Datafile |
| MINIOTIM | MINIMUM TIME, IN MILLISECONDS, SPENT PERFORMING I/O on that Datafile |
| MAXIOWTM | Maximum time, in milliseconds, spent writing to that Datafile |
| MAXIORTM | Maximum time, in milliseconds, spent reading from that Datafile |

**TABLE 8.3** Description of Selected V$DATAFILE Columns

| Column Name | Description |
| :--- | :--- |
| FILE# | The Datafile’s internal identifier assigned by Oracle at tablespace creation |
| NAME | The fully qualified path and name of the Datafile |

**TABLE 8.4** Description of Selected V$TEMPFILE Columns

| Column Name | Description |
| :--- | :--- |
| FILE# | The Datafile’s internal identifier assigned by Oracle at tablespace creation |
| NAME | The fully qualified path and name of the Datafile |

Figure 8.1 shows a query on these three views that displays the overall statistics for every Datafile (denoted by D in the first column) and tempfile (denoted by T in the first column) in the database.

**FIGURE 8.1** Performance query on V$FILESTAT, V$DATAFILE, and V$TEMPFILE

```sql
SQL> SELECT s.file#||'D' "FILE#TYPE", d.name "DATAFILE",
  2          s.phyrds, s.phywrts,
  3          s.avgiotm, s.minitiorm,
  4          s.maxiowtm, s.maxiortm
  5    FROM v$filestat s, v$datafile d
  6   WHERE s.file# = d.file#
  7  UNION ALL
  8 SELECT s.file#||'T', t.name "DATAFILE",
  9          s.phyrds, s.phywrts,
 10          s.avgiotm, s.minitiorm,
 11          s.maxiowtm, s.maxiortm
 12   FROM v$filestat s, v$tempfile t
 13  WHERE s.file# = t.file#
 14 ORDER BY 1;
```

FILE#TYPE DATAFILE PHYRDS PHYWRTS AVGIOTM MINIOTIM MAXIOWTM MAXIORTM
10 D:\ORACLE\ORADATA\PROD\SYSTEM01.DBF 956 728 4.82 0 57.30 61.39
20 D:\ORACLE\ORADATA\PROD\TEMP01.DBF 956 735 1.69 0 37.30 61.39
30 D:\ORACLE\ORADATA\PROD\UNDO01.DBF 64 770 11.4 0 57.30 41.09
40 D:\ORACLE\ORADATA\PROD\APPL_IDX01.DBF 31 1202 0.0 0 37.30 61.39
40 D:\ORACLE\ORADATA\PROD\APPL_T101.DBF 2311 13250 9.0 0 57.30 61.34
40 D:\ORACLE\ORADATA\PROD\APPL_T201.DBF 0 12 1.9 0 57.30 61.32
50 D:\ORACLE\ORADATA\PROD\USER01.DBF 1123 62 2.2 0 57.30 61.32
60 D:\ORACLE\ORADATA\PROD\OEM_REPOSITORY1.DBF 2 0 57.32 61.30
70 D:\ORACLE\ORADATA\PROD\WEA01.DBF 4701 0 0 0 38.31 72.71

![Figure 8.1 Output](img/832fbc6aca8b6075843ca6f2356c0a8d_411_0.png)

The init.ora parameter TIMED STATISTICS must be set to TRUE; otherwise, the values for the PHYRDS, PHYWRTS, AVGIOTM, MINIOTIM, MAXIOWTM, and MAXIORTM columns will all be zeros.

## Tuning Tablespace and Datafile I/O

For more details on tempfiles, see the section headed “Tuning Sort I/O” later in this chapter.

Using the output in Figure 8.1, you can see that the majority of physical writes are occurring against three Datafiles: app1_idx01.dbf, undo01.dbf, and app1_tab01.dbf, which are the Datafiles for the application indexes, rollback segments, and tables respectively. The majority of physical reads are occurring on the Datafile (readonly01.dbf) that makes up the read-only tablespace. As you’ll see in the next section, the placement of these files on disks relative to one another is an important tuning consideration.

The SYSTEM tablespace Datafiles will frequently experience high read activity because the data dictionary tables that Oracle uses to perform recursive SQL are located in the SYSTEM tablespace. However, excessive write activity to the SYSTEM tablespace may indicate that non-data dictionary segments are stored there.

## Using STATSPACK to Measure Datafile I/O

The output from the STATSPACK feature contains similar information regarding Datafile and tablespace I/O characteristics. Figure 8.2 shows sample output from a STATSPACK report.

![Figure 8.2 Output](img/832fbc6aca8b6075843ca6f2356c0a8d_412_0.png)

The output shown in Figure 8.2 indicates that during the period between the two STATSPACK snapshots, the TEMP tablespace received the most read and write activity. Notice that unlike the output in V$FILESTAT, the STATSPACK output expresses the duration of the read and write activity in both seconds and milliseconds. This information is useful when determining where to physically locate Datafiles on the available disk drives, volume groups, and controllers.

## Using REPORT.TXT to Measure Datafile I/O

The REPORT.TXT file generated by UTLBSTAT.SQL and UTLSTAT.SQL also contains file I/O information at both the tablespace level and Datafile level. Figure 8.3 shows the REPORT.TXT output that displays tablespace I/O statistics. Figure 8.4 shows the section of REPORT.TXT that contains tablespace and Datafile I/O statistics.

**FIGURE 8.3** Sample REPORT.TXT showing tablespace I/O statistics

```sql
SQL> rem sum I/O operations over tablespaces.
SQL> select
  2 table_space,
  3 sum(phys_reads) reads,
  4 sum(phys_blks_rd) blks_read,
  5 sum(phys_rd_time) read_time,
  6 sum(phys_writes) writes,
  7 sum(phys_blks_wr) blks_wr,
  8 sum(phys_wrt_time) write_time,
  9 sum(megabytes_size) megabytes
 10 from stats$xfiles
 11 group by table_space
 12 order by table_space;
```

| TABLE_SPACE | READS | BLKS_READ | READ_TIME | WRITES | BLKS_WRT | WRITE_TIME | MEGABYTES |
| :------------ | :------ | :---------- | :---------- | :------- | :--------- | :----------- | :--------- |
| APPL_IDX | 19 | 19 | 0 | 19 | 19 | 0 | 28 |
| APPL_TAB | 27 | 19 | 0 | 19 | 19 | 0 | 10 |
| ORA_REPOSITORY | 19 | 19 | 0 | 19 | 19 | 0 | 21 |
| SYSTEM | 107 | 107 | 481 | 356 | 356 | 2597 | 341 |
| TOOLS | 19 | 19 | 0 | 19 | 19 | 0 | 28 |
| UNDO | 19 | 19 | 0 | 5499 | 5499 | 69719 | 210 |
| USERS | 648 | 3755 | 2577 | 13946 | 13946 | 144108 | 60 |

**FIGURE 8.4** Sample REPORT.TXT showing tablespace and Datafile I/O statistics

```sql
SQL> rem I/O should be spread evenly across drives. A big difference between
SQL> phys_reads and phys_blks_rd implies table scans are going on.
SQL> select table_space, file_name,
  2 phys_reads reads, phys_blks_rd blks_read, phys_rd_time read_time,
  3 phys_writes writes, phys_blks_wr blks_wrt, phys_wrt_time write_time,
  4 megabytes_size megabytes,
  5 round(decode(phys_blks_rd,0,0,phys_rd_time/phys_blks_rd),2) avg_rt,
  6 round(decode(phys_reads,0,0,phys_blks_rd/phys_reads),2) "blocks/rd"
  7 from stats$xfiles
  8 order by table_space, file_name;
```

| TABLE_SPACE | FILE_NAME | READS | BLKS_READ | READ_TIME | WRITES | BLKS_WRT | WRITE_TIME |
| :------------ | :---------- | :------ | :---------- | :---------- | :------- | :--------- | :---------- |
| APPL_IDX | 0:\ORACLE\ORADATA\PROD\APPLIDX01.DBF | 112 | 19 | 0 | 19 | 19 | 0 |
| APPL_TAB | 0:\ORACLE\ORADATA\PROD\APPLT1\APLTAB01.DBF | 19 | 19 | 0 | 19 | 19 | 0 |
| APPL_TAB | 0:\ORACLE\ORADATA\PROD\APPLT2\APLTAB02.DBF | 8 | 8 | 0 | 8 | 8 | 0 |
| ORA_REPOSITORY | 0:\ORACLE\ORADATA\PROD\ORAREPOSITORY.DBF | 19 | 19 | 0 | 19 | 19 | 0 |
| SYSTEM | 0:\ORACLE\ORADATA\PROD\SYSTEM01.DBF | 107 | 107 | 481 | 356 | 356 | 2597 |
| TOOLS | 0:\ORACLE\ORADATA\PROD\TOOLS01.DBF | 19 | 19 | 0 | 19 | 19 | 0 |
| UNDO | 0:\ORACLE\ORADATA\PROD\UNDOTBS01.DBF | 19 | 19 | 0 | 5499 | 5499 | 69719 |
| USERS | 0:\ORACLE\ORADATA\PROD\USERS01.DBF | 648 | 3755 | 2577 | 13946 | 13946 | 144108 |

In Figure 8.3, you can see that the majority of the read and write activity I/O took place on the **APPL_IDX**, **USERS**, and **SYSTEM** tablespaces. You can also see that in some cases, multiple blocks were read and written with a single I/O. For example, the **USERS** tablespace had 648 physical reads performed against it, reading 3,755 blocks. This is approximately five to six database blocks read for every physical read on that tablespace. Tuning this type of multiblock read is discussed in the Datafile and tablespace tuning section later in this chapter. Figure 8.4 shows that I/O on the **APPL_TAB** tablespace was distributed across the tablespace's two Datafiles, **APPL_TAB01.DBF** and **APPL_TAB02.DBF**. However, approximately 70 percent of the I/O was on the **APPL_TAB01.DBF** Datafile. This information can also be useful when tuning Datafile disk I/O.

There is no standard rule as to which Datafiles should be receiving the most or least I/O. In general, however, you should strive to balance the I/O requests across several Datafiles.

## Using Performance Manager to Measure Datafile I/O

The Performance Manager component of the Oracle Enterprise Manager Diagnostics Pack includes several graphical representations of Datafile I/O performance. Figure 8.5 shows a sample Performance Manager screen that displays I/O activity based on time for each Datafile in the database.

![Figure 8.5 Output](img/832fbc6aca8b6075843ca6f2356c0a8d_414_0.png)
