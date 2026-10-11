The MySQL server supports multiple storage engines and is highly configurable in terms of which engines to make available. General storage engine characteristics are discussed in Chapter 2, “Using SQL to Manage Data.” The following discussion describes how to configure which engines your server uses. It also provides specific configuration information for the MyISAM, InnoDB, and Falcon storage engines.

# 12.7.1 Selecting Which Storage Engines a Server Supports

The MySQL server provides flexible control over which storage engines are available:

+   - If you build MySQL from source, you can determine which of the optional storage engines to build.
+   - For any server, whether or not you compile it yourself, you can selectively enable or disable at startup some of the optional storage engines that are built. You might disable engines that you don't need so as to reduce server memory requirements. (Keep in mind that if you disable an engine, you cannot access any tables that might already have been created by it.)
+   - You can find out at runtime which engines are available, and which one is the default engine.

Table 12.7 shows the options to use with *configure* to include or exclude each engine when building MySQL from source. Some engines, if built, can be disabled with an option to *mysqld* at startup time if you do not want to use them. Falcon requires MySQL 6.0 or higher. The *--skip-archive* option requires MySQL 5.1 or higher.

| Engine | Configuration Options | Runtime Options |
|---|---|---|
| ARCHIVE | --with-archive-storage-engine, --without-archive-storage-engine | --skip-archive |
| BLACKHOLE | --with-blackhole-storage-engine, --without-blackhole-storage-engine |  |
| CSV | --with-csv-storage-engine, --without-csv-storage-engine |  |
| EXAMPLE | --with-example-storage-engine, --without-example-storage-engine |  |
| Falcon | --with-falcon-storage-engine, --without-falcon-storage-engine | --skip-falcon |
| FEDERATED | --with-federated-storage-engine, --without-federated-storage-engine |  |
| InnoDB | --with-innodb, | --skip-innodb |