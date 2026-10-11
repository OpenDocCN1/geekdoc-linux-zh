REPLACE always acts like INSERT, and you cannot use DELETE or UPDATE. Rows are compressed during storage and decompressed during retrieval to save space. The ARCHIVE engine does not support indexing until MySQL 5.1.6, at which point an ARCHIVE table can include an indexed AUTO_INCREMENT column; other columns still cannot be indexed.

+   - The BLACKHOLE engine creates tables for which writes are ignored and reads return nothing.

+   - The CSV engine stores data in comma-separated values format. For each table, it creates a .csv file in the database directory. This is a plain text file in which each table row appears as a single line. The CSV engine does not support indexing.

+   - The EXAMPLE engine is a minimal demonstration of how to get started writing a storage engine. It exists mainly for developers to examine its source code and study the basic concepts involved in hooking a storage engine into the server.

# 2.6.1.11 Storage Engine Portability Characteristics

Any table managed by a given MySQL server is portable to another server in the sense that you can dump it into a text file with mysqldump, move the dump file to the machine where the other server runs, and load the file to re-create the table. Another kind of portability is “binary portability,” which means that you can directly copy the disk files that represent the table to another machine, install them into the corresponding locations under the data directory, and expect the MySQL server there to be able to use the table.

A general condition for binary portability of tables is that the source and destination servers must be feature compatible. For example, the destination server must support the storage engine that manages the tables. If the server does not have the appropriate engine, it cannot access tables created by that engine on the source server.

Some storage engines create tables that are binary portable and some do not. The following list summarizes binary portability for individual engines:

+   - MyISAM and InnoDB tables are stored in machine-independent format and are binary portable, assuming that your processor uses two’s-complement integer arithmetic and IEEE floating-point format. Unless you have some kind of oddball machine, neither of these conditions should present any real issues. In practice, you’re probably most likely to see portability—compromising variation in hardware if you’re using an embedded server built for a special-purpose device, as these devices sometimes use processors that have nonstandard operating characteristics.

+   - MERGE tables are portable if their constituent MyISAM files are portable.

+   - MEMORY tables are not binary portable because their contents are stored in memory, not on disk.

+   - CSV tables are binary portable because their .csv data files are plain text.

+   - BLACKHOLE tables are binary portable because they contain no data.