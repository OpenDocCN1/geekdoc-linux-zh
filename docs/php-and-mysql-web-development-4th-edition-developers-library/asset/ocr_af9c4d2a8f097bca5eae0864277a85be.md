# 14.6.2 Using mysqlcheck to Check and Repair Tables

The mysqlcheck program provides a command-line interface to the CHECK TABLE and REPAIR TABLE statements. It connects to the server and issues the appropriate statements for you based on the options you specify. Therefore, mysqlcheck can check or repair tables for the same storage engines as CHECK TABLE and REPAIR TABLE.

Typically, you invoke mysqlcheck with a database name, optionally followed by one or more table names. With just a database name, mysqlcheck checks all the tables in the database:

```
% mysqlcheck sampdb
```

With table names following the database name, mysqlcheck checks only those tables:

```
% mysqlcheck sampdb president member
```

If you specify the --databases option, all following arguments are interpreted as database names and mysqlcheck checks all the tables in each database:

```
% mysqlcheck --databases sampdb test
```

If you specify --all-databases, mysqlcheck checks all tables in all databases. No database or table name arguments are needed:

```
% mysqlcheck --all-databases
```

mysqlcheck is more convenient than issuing the CHECK TABLE and REPAIR TABLE statements directly, because those statements require that you explicitly name each table to be checked or repaired. With mysqlcheck, it’s much easier to check all tables in a database: It looks up the names of the tables in the database for you and constructs statements that name the appropriate tables.

By default, mysqlcheck checks tables using a medium check, but supports options that enable explicit selection of the type of operation to perform. The following table shows some mysqlcheck options and the CHECK TABLE options to which they correspond. (As with CHECK TABLE, these options apply to MyISAM tables but may not be used by other storage engines.)

| mysqlcheck Option | CHECK TABLE Option |
|:------------------|:-------------------|
| --check-only-changed | CHANGED |
| --extend | EXTENDED |
| --fast | FAST |
| --medium-check | MEDIUM |
| --quick | QUICK |