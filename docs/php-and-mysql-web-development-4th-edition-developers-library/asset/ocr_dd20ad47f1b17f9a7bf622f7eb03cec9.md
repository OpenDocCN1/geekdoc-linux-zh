It’s possible to exclude databases on the master side rather than on the slave side by using the `binlog-ignore-db` option in the master’s option file. This reduces traffic between the master and slave, but also unfortunately causes the binary log to contain no information for the ignored databases. That information is useful for performing recovery on the master after a crash, so database exclusion on the slave side is usually preferable.

After you have replication set up and running, there are several statements that you may find useful for monitoring or controlling the master and the slave. Details about these statements are available in Appendix E. A brief summary follows:

+   * `SHOW SLAVE STATUS` on a slave shows whether replication is running and the current replication coordinates. The coordinates can be used to determine which binary log files from the master are no longer needed.

+   * `PURGE MASTER` on the master expires binary log files. You can use this after issuing a `SHOW SLAVE STATUS` statement on each of the slaves to determine which log files no longer are needed.

+   * The `STOP SLAVE` and `START SLAVE` statements suspend and resume a slave server’s replication-related activity. These statements can be useful for telling the slave to be quiescent while you’re making a backup, for example. (See Section 14.8.4, “Using a Replication Slave for Making Backups.”)

As mentioned earlier, a slave server uses two threads internally to manage replication. The I/O thread talks to the master server, receives updates from it, and writes updates to its relay log. The SQL thread reads the relay log and executes the updates it finds there. You can use `STOP SLAVE` and `START SLAVE` to suspend or resume each thread individually by adding `IO_THREAD` or `SQL_THREAD` to the end of the statement. For example, `STOP SLAVE SQL_THREAD` stops execution by the slave of the updates in the relay log, but enables the slave to continue to read updates from the master and record them in the relay log.

Relay log files are generated in numbered sequence, much like the binary log files. There also is a relay log index file analogous to the binary log index. The default relay log and index files are `HOSTNAME-relay-bin.nnnnnn` and `HOSTNAME-relay-bin.index` in the data directory. The defaults can be changed with the `--relay-log` and `--relay-log-index` server startup options.

# 14.8.3 Binary Logging Formats

Before MySQL 5.1, the server writes data-modification events to the binary log as SQL statements. This is known as statement-based binary logging, and replication based on it is statement-based replication. Beginning with MySQL 5.1.5, an alternative format is available in which the server logs changes to individual data rows. This is row-based logging and replication. Mixed-format logging was added in 5.1.8, for which the server switches between statement-based and row-based logging as it deems best.