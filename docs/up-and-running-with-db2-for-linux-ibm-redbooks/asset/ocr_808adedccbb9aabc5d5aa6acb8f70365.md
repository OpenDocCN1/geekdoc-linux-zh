index is made available. While the new index is being made available all access to the table is prohibited.

You can reduce the need of index reorganization via a variety of means, for example, setting PCTFREE for indexes, or enabling the online index defragmentation by setting MINPCTUSED (it will trigger online index leaf page merging when specific conditions are matched). This means it may reduce the likelihood of causing index page splits when future activities such as inserts happen on the table.

The default behavior of the REORG INDEXES command is ALLOW NO ACCESS, which places an exclusive lock on the table during the reorganization process. But you can also specify ALLOW READ ACCESS or ALLOW WRITE ACCESS to permit other transactions to read from or update the table.

# 5.2.3 Statistics information collection

The RUNSTATS command can be issued from any database partition in the db2nodes.cfg file. It can be used to update the catalogs on the catalog database partition. In a partitioned database, the RUNSTATS command collects the statistics on only a single node. If the database partition from which the RUNSTATS command is executed has a part of the table, then the command will execute on that database partition directly. Otherwise, the command executes on the first database partition in the database partition group across which the table is partitioned.

It is possible to perform read or write operations to the table where RUNSTATS is taking place by using different RUNSTATS command parameters. For example, ALLOW READ ACCESS specifies that other users can have read-only access to the table while statistics are calculated and ALLOW WRITE ACCESS specifies that other users can read from and write to the table while statistics are calculated.

> Note: Because reorganizing a table usually takes more time than running statistics, you might execute RUNSTATS to refresh the current statistics for your data and rebind your applications. If refreshed statistics do not improve performance, then reorganization may help.

# 5.2.4 Packages rebinding

The command REBIND enables the user to take advantage of a change in the system without a need for the original bind file. It is likely that a particular SQL statement can take advantage of a newly created index. The REBIND command can be used to recreate the package. REBIND can also be used to recreate