BINARY and VARBINARY are binary types that store bytes and have no character set or collation. Comparisons are based on numeric byte values.

The rules for handling of padding for BINARY values are as follows:

+   - As of MySQL 5.0.15, short values are padded with 0x00 bytes. Nothing is stripped on retrieval.
+   - Before MySQL 5.0.15, short values are padded with spaces. Trailing spaces are stripped on retrieval.

For VARBINARY, no padding occurs when values are stored and no stripping occurs for retrieval.

# 3.2.5.3 The BLOB and TEXT Data Types

A “BLOB” is a binary large object—basically, a container that can hold anything you want to toss into it, and that you can make about as big as you want. In MySQL, the BLOB type is really a family of types (TINYBLOB, BLOB, MEDIUMBLOB, LONGBLOB). These types are identical except in the maximum amount of information they can hold (see Table 3.10). BLOB columns store binary strings. They are useful for storing data that may grow very large or that may vary widely in size from row to row. Some examples are compressed data, encrypted data, images, and sounds.

MySQL also has a family of TEXT types (TINYTEXT, TEXT, MEDIUMTEXT, LONGTEXT). These are similar to the corresponding BLOB types, except that TEXT types store non-binary strings rather than binary strings. That is, text store characters rather than bytes, and are associated with a character set and collation. This results in the general differences between binary and non-binary strings that were described earlier in Section 3.1.2, “String Values.” For example, in comparison operations, BLOB values are compared in byte units and TEXT values are compared in character units using the column collation.

BLOB or TEXT columns sometimes can be indexed, depending on the storage engine you're using:

+   - The MyISAM and InnoDB storage engines support BLOB and TEXT indexing.
+   However, you must specify a prefix size to be used for the index. This avoids creating index entries that might be huge and thereby defeat any benefits to be gained by that index. The exception is that prefixes are not used for FULLTEXT indexes on TEXT columns. FULLTEXT searches are based on the entire content of the indexed columns, so any prefix you specify is ignored.
+   - MEMORY tables do not support BLOB and TEXT indexes because the MEMORY engine does not support BLOB or TEXT columns at all.

BLOB or TEXT columns may require special care:

+   - Due to the typical large variation in the size of BLOB and TEXT values, tables containing them are subject to high rates of fragmentation if many deletes and updates are done. If you're using a MyISAM table to store BLOB or TEXT values, you can run