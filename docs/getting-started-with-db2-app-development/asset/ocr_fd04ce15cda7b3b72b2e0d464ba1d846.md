```
zcat DBD-DB2-<x.xx>.tar.gz | tar xvf -
cd DBD-DB2-<x.xx>
export DB2_HOME=/home/db2inst1/sqllib # for example
perl Makefile.PL
make
make test
make install
```

**Listing 9.3 – Install the DBD::DB2 driver from source in Linux/UNIX**

```
#unpack/ unzip the source file DBD-DB2-<x.xx>.tar.gz using winzip
cd DBD-DB2-<x.xx>
perl Makefile.PL
nmake
nmake test
nmake install
```

**Listing 9.4 – Install the DBD::DB2 driver from source in Windows**

# # 9.3 Developing Perl DB2 applications

In this section you will learn how to develop a Perl application that will access DB2 data by calling the Perl DBI API.

# ## 9.3.1 Connecting to a DB2 database

First, enable Perl to load the Perl DBI module that provides the standard DBI APIs used to access a database. This can be done using this line in your application:

```
use DBI;
```

Then, connect to the DB2 database by calling the **DBI->connect** method of the DBI package using this syntax:

```
$dbhndle = DBI->connect($data_source, $userID, $password, \%attr);
```

*Table 9.1* explains some of the parameters of the **DBI->connect** method.

| Name | Description |
| --- | --- |
| $data_source | A database connection string with the format of `\`'dbi:DB2:dbalias'`, where *dbalias* represents one of the following:<br>1) A DB2 Database alias cataloged in your DB2 client, or<br>2) A connection string that includes the database name, host name, port number, protocol, user ID, and password in the format of `'DATABASE=database; HOSTNAME=hostname; PORT=port; PROTOCOL=TCPIP; UID=username; PWD=password'`. This format |