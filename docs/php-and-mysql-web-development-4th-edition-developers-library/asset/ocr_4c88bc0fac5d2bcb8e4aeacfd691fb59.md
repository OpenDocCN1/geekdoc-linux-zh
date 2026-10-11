+   * The BLACKHOLE and EXAMPLE storage engines don’t actually store any data, so they need not create any files.
+   * The FEDERATED engine provides access to tables located at remote MySQL servers. It doesn’t create any data files itself.

The following sections characterize the features and behavior of selected MySQL storage engines. For additional information about how engines represent tables physically, see Section 11.2.3, “Representation of Tables in the Filesystem.”

# ### 2.6.1.3 The MyISAM Storage Engine

The MyISAM storage engine is the default engine in MySQL, unless you have configured your server otherwise. The following list describes some of its features:

+   * MyISAM provides key compression. It uses compression when storing runs of successive similar string index values. MyISAM also can compress runs of similar numeric index values because numeric values are stored with the high byte first. (Index values tend to vary faster in the low-order bytes, so high-order bytes are more subject to compression.) To enable numeric compression, use the `PACK_KEYS=1` option when creating a MyISAM table.
+   * MyISAM provides more features for AUTO_INCREMENT columns than do other storage engines. For more information, see Section 3.4, “Working with Sequences.”
+   * Each MyISAM table has a flag that is set when the table is checked by the server or by the myisamchk program. MyISAM tables also have a flag indicating whether a table was closed properly when last used. The server shuts down abnormally or the machine crashes, the flags can be used to detect tables that need to be checked. To do this automatically, start the server with the `--myisam-recover` option. This causes the server to check the table flags whenever it opens a MyISAM table and perform a table repair if necessary.
+   * MyISAM supports full-text searching through the use of FULLTEXT indexes.
+   * MyISAM supports spatial data types and SPATIAL indexes.

# ### 2.6.1.4 The MERGE Storage Engine

MERGE tables provide a means for grouping a set of MyISAM tables into a single logical unit. Querying a MERGE table in effect queries all the constituent tables. One advantage of this is that you can exceed the maximum table size allowed by the filesystem for individual MyISAM tables.

The tables that make up a MERGE table must all have the same structure. This means the columns in each table must be defined with the same names and types in the same order, and the indexes must be defined in the same way and in the same order. It is allowable to mix compressed and uncompressed tables. (To produce compressed tables, use myisampack; see Appendix F, “MySQL Program Reference.”)