
## 9.2 Installing Prerequisites

You need to install Perl 5.8 or later.

On Linux/UNIX/Mac OS X, Perl is normally shipped as a standard component of the OS installation.

On Windows, you can download the ActiveState’s free Perl binary distribution ActivePerl from <http://www.activestate.com/activeperl/>. ActivePerl is also available for free on Linux/UNIX. You can download the binaries from the website <http://www.activestate.com/activeperl/downloads/> and install Perl by running the Windows Installer on Windows or `install.sh` on Linux/UNIX.

Alternatively, you can download the source code of Perl interpreter from <http://dev.perl.org/> and then use appropriate C compilers to generate the Perl binaries for your platform. Refer to the above Web site for details about building and installing Perl from source.

After installation, you can check the version of Perl by running `perl -v`. If the version is lower than 5.8, you need to upgrade to 5.8 or later.

### 1. Install the Perl DBI module

This is a prerequisite for any RDBMS including DB2 with its DBD::DB2 driver module.

If you are using ActivePerl distribution and have internet access, you can install a binary version of the DBI module through ActivePerl’s *Perl Package Manager* by issuing the following command:

```bash
ppm install DBI
```

The Perl Package Manager will download the DBI module and install it automatically.

Alternatively if you have internet access, you can run the following to build and install the DBI module from the source:

```bash
perl -MCPAN -e "install DBI"
```

The above command will download the DBI source code, then build and install it automatically through the CPAN module. Note that you need a C compiler for building the source. For details about the CPAN module, refer to <http://www.perl.com/doc/manual/html/lib/CPAN.html>.

If you don’t have internet access, you can download the latest release of Perl DBI module source code from <http://search.cpan.org/~timb/DBI> at a later time, and then build the source and install the DBI module following the instructions shown in *Listing 9.1* for Linux/UNIX and *Listing 9.2* for Windows. You need a C compiler for building the source.

**Listing 9.1 – Install Perl DBI module from source on Linux/UNIX**

```bash
# the source is DBI-<x.xxx>.tar.gz, where x.xxx means version.
zcat DBI-<x.xxx>.tar.gz | tar xvf -
cd DBI-<x.xxx>
perl Makefile.PL
make
make test
make install
```

**Listing 9.2 – Install Perl DBI module from source on Windows**

```bash
# unpack/unzip the source file DBI-<x.xxx>.tar.gz using winzip
cd DBI-<x.xxx>
perl Makefile.PL
nmake
nmake test
nmake install
```

**Note:**

For more information about the Perl DBI API, visit http://search.cpan.org/~timb/DBI/DBI.pm

### 2. Install an IBM DB2 data server client

After installing all the above software, you will be able to install the Perl DB2 driver DBD::DB2. This is discussed in the next sections.

## 9.2.1 Perl adapters and drivers

At the time of writing, the latest release of the DBD::DB2 driver module is 1.78. For more information about the DBD::DB2 driver, visit http://www.ibm.com/db2/perl/ and http://search.cpan.org/~ibmtordb2/.

If you are using ActivePerl distribution on Windows and have the internet connection, you can install the DBD::DB2 module through ActivePerl's Perl Package Manager by issuing the following command:

For Perl version 5.8:

```bash
ppm install http://theoryx5.uwinnipeg.ca/ppms/DBD-DB2.ppd
```

For Perl Version 5.10:

```bash
ppm install http://cpan.uwinnipeg.ca/PPMpackages/10xx/DBD-DB2.ppd
```

Alternatively you can build and install the driver from source. You will need a C compiler. Download the latest release of DBD::DB2 module source from http://www.cpan.org/authors/id/I/IB/IBMTORDb2 and follow the instructions in Listing 9.3 (for Linux/UNIX) and Listing 9.4 (for Windows).

**Listing 9.3 – Install the DBD::DB2 driver from source in Linux/UNIX**

```bash
# the source is DBD-DB2-<x.xx>.tar.gz, where x.xx means version...
zcat DBD-DB2-<x.xx>.tar.gz | tar xvf -
cd DBD-DB2-<x.xx>
export DB2_HOME=/home/db2inst1/sqllib # for example
perl Makefile.PL
make
make test
make install
```

**Listing 9.4 – Install the DBD::DB2 driver from source in Windows**

```bash
# unpack/unzip the source file DBD-DB2-<x.xx>.tar.gz using winzip
cd DBD-DB2-<x.xx>
perl Makefile.PL
nmake
nmake test
nmake install
```

## 9.3 Developing Perl DB2 applications

In this section you will learn how to develop a Perl application that will access DB2 data by calling the Perl DBI API.

### 9.3.1 Connecting to a DB2 database

First, enable Perl to load the Perl DBI module that provides the standard DBI APIs used to access a database. This can be done using this line in your application:

```perl
use DBI;
```

Then, connect to the DB2 database by calling the **DBI->connect** method of the DBI package using this syntax:

```perl
$dbhndle = DBI->connect($data_source, $userID, $password, \%attr);
```

*Table 9.1* explains some of the parameters of the **DBI->connect** method.

| Name | Description |
| :--- | :--- |
| `$data_source` | A database connection string with the format of `'dbi:DB2:dbalias'`, where *dbalias* represents one of the following:<br>1) A DB2 Database alias cataloged in your DB2 client, or<br>2) A connection string that includes the database name, host name, port number, protocol, user ID, and password in the format of `'DATABASE=database; HOSTNAME=hostname; PORT=port; PROTOCOL=TCPIP; UID=username; PWD=password'`. This format can be used for connecting to a remote database via TCP/IP directly without first cataloging it on the client |
| `$userID` | The user ID used to connect to the database, it’s optional if **username** is specified in **$data_source** connection string |
| `$password` | The password for the user ID to connect to the database, it’s optional if **password** is specified in **$data_source** connection string |
| `\%attr` | Optional, a reference to the list of database connection attributes |

**Table 9.1 - Parameters for the DBI->connect method**

The **DBI->connect** method will automatically load the DBD::DB2 module if it was not loaded earlier, and return a database handle if the connection succeeds. The database handle will be used for all future function calls made on the DB connection.

For example, to connect to the **SAMPLE** database, make the connection as shown in *Listing 9.5*:

**Listing 9.5 - Connect to SAMPLE database cataloged on the client**

```perl
use DBI;
my $dbhandle = DBI->connect("dbi:DB2:sample", "db2admin", "password", {AutoCommit=>0});
```

In the above listing, the database user ID is **db2admin**, the **password** is **password** and the **AutoCommit** connection attribute is set off, which means it is turned off. This means you can explicitly issue a commit or rollback for a transaction for this connection. By default **AutoCommit** is on. After successful execution, the **DBI->connect** returns a database handle in the variable **$dbhandle**.

If the **SAMPLE** database is a remote database on a machine **host2** where the instance is listening to port 50000 and it has not been cataloged in your client, you can make a connection to it via TCP/IP directly as shown in *Listing 9.6*:

**Listing 9.6 - Connect to the remote SAMPLE database via TCP/IP directly**

```perl
use DBI;
my $dbhandle = DBI->connect("dbi:DB2:DATABASE=sample; HOSTNAME=host2; PORT=50000; PROTOCOL=TCP/IP;UID=db2admin;PWD=password", {AutoCommit=>0});
```

### 9.3.2 Retrieving data

After connecting to the database, you can issue **SELECT** SQL statements to retrieve data from the database.

If the **SELECT** statement is not known at the time the application is written, refer to *section 9.3.4* on how to run a SQL that contains variable inputs or parameter markers.

If the **SELECT** statement is known, follow the steps below:

1. Connect to the database by calling the **DBI->connect** method.
