In general, queries that incorporate V$SYSSTAT will show statistics for the entire instance since the time it was started. By joining this view to the other relevant views, you get the overall picture of performance in the database. Alternatively, queries that incorporate V$SESSTAT will show statistics for a particular session. These queries are better suited for examining the performance of an individual operation or process.

![](bbox=[0.18, 0.25, 0.25, 0.31])

A complete description of all the V$ views can be found in Chapter 3, “Dynamic Performance (V$) Views,” in the *Oracle9i Database Reference Release 1 (9.0.1)* (Part Number A90190-01).

# # DBA Views Commonly Used in Performance Tuning

There are approximately 170 DBA data dictionary views in an Oracle9i database. The tables underlying these views are the physical tables that make up the Oracle data dictionary. Like the X$ virtual tables underlying the V$ views, these tables are also generally undocumented and have only mildly meaningful names like `OBJ$` and `FILE$`. However, in most cases, the DBA views themselves will provide the information you need to begin performance tuning. Table 2.5 contains a partial listing of some of the DBA views that are used when you undertake performance tuning on a database.

**TABLE 2.5 Sample of Static Dictionary Views**

| View Name | View Description |
| :--- | :--- |
| DBA_TABLES | Table storage, row, and block information |
| DBA_INDEXES | Index storage, row, and block information |
| INDEX_STATS | Index depth and dispersion information |
| DBA_DATA_FILES | Datafile location, naming, and size information |
| DBA_SEGMENTS | General information about any space consuming segment in the database |
| DBA_HISTOGRAMS | Table and index histogram definition information |