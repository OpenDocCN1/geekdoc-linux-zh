| Column 1 | Column 2 | Column 3 |
|---|---|---|
| Database | Database alias/name of the database to which the Rails project connects | Yes |
| Username | User ID used to connect to the DB2 database | Yes |
| Password | Password for the user ID specified | Yes |
| Schema | The collection of named objects. The schema provides a way to group objects logically within the database. | Optional. If the schema is missing from database.yml, this attribute is set to the authorization ID of the current session user. |
| Application | Application name. Only applicable when working with DB2 Connect™ software to work with DB2 for i5/OS and DB2 for z/OS. | Optional |
| Account | A character string used to identify the client accounting string. Only applicable when working with DB2 Connect software to work with DB2 for i5/OS and DB2 for z/OS. | Optional |
| Workstation | A character string used to identify the client workstation name. Only applicable when working with DB2 Connect software to work with DB2 for i5/OS and DB2 for z/OS. | Optional |
| Host | Host name of the remote server where the database resides | The optional connection attributes `host` and `port` associated with remote TCP/IP connections are only required when DB2 catalog information is not available and no data source has registered in the db2cli.ini configuration file for DB2 CLI. This type of setup is possible while using the IBM Driver for ODBC and CLI instead of a complete DB2 Client installed locally. |