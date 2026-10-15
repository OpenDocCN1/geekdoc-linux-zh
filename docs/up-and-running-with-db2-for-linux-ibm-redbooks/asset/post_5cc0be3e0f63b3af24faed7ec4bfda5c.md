
from the database files. This configuration is commonly used in many production environments.

Here is an example of one possible configuration (Table 2-7). We will be using this system setup throughout the rest of this book.

## Table 2-7 Sample partition setup

| Partition name | Description |
|---|---|
| / | Linux |
| /boot | Linux |
| /swap | Linux Swap space |
| /db2home | For storing the home directories for DB2 users (for example, db2inst1, db2fenc1, dasusr1) |
| /database | For storing the database |
| /db2log1 | Used to storing primary copy of logs |
| /db2log2 | Used to store DB2 mirrored logs |
| /db2temp | For storing DB2 temporary tablespaces |
| /software | Used for storing software. For example, we downloaded the DB2 install image into this directory. |
| /tablespaces | Holds all user tablespaces |

> Note: Mirroring log files helps protect a database from accidental deletion of an active log and data corruption caused by disk error. While this functionality increases the high availability of a system, log mirroring may impact system performance as all log data will be written to both the log path and the mirror log path.

## Log space

By default, DB2 sets the log path to the default database path during database creation. For example, Our default database path is /db2home and our log path is:

```
/db2home/db2inst2/db2inst2/NODE0000/SQL00001/SQLLOGDIR/
```

We recommend that you store both the primary copy of the logs and the mirror logs each on a physically separate disk, preferably one that is also on a different disk controller.

Mirror logs are created using the MIRRORLOGPATH configuration parameter. Log mirroring allows the database to write an identical second copy of log files to a different path.

In Example 2-6, we change the primary log path from the default to /db2log1 and set the mirror log path to /db2log2.

## Example 2-6 db2 logs configuration

```
db2 update db cfg for db_name using NEWLOGPATH /db2log1
db2 update db cfg for db_name using MIRRORLOGPATH /db2log2
```

The procedure of changing the log path is discussed in “Change log path” on page 97.

**Note:** These changes will only take place after you deactivate and activate your database.

## Temp space

DB2 uses system temporary tablespaces for many SQL operations, such as JOIN and SORT. DB2’s temporary tablespace, TEMPSPACE1, is one of the three default tablespaces (SYSCATSPACE, TEMPSPACE1, and USERSPACE1) that gets created during database creation. By default, TEMPSPACE1 gets placed in the database path. For larger systems, we recommend that your temporary tablespaces are located on a separate filesystem and disk. For example, in our system, we created the filesystem /db2temp with mount point /db2temp to store our temporary tablespaces.

In a partitioned database environment, the catalog node should contain all three default table spaces, and the other database partitions should each contain only TEMPSPACE1 and USERSPACE1.

Example 2-7 shows how to create a system temporary tablespace on multiple nodes in the /db2temp filesystem:

## Example 2-7 Create temp tablespace in a different filesystem

```
connect to db_name;

create temporary tablespace TEMPSPACE01 in IBM TEMPGROUP
managed by SYSTEM
using ('/db2temp/$INSTANCE/db_name/n001tmp/tempspace01') on dbpartitionnum (1)
using ('/db2temp/$INSTANCE/db_name/n002tmp/tempspace01') on dbpartitionnum (2)
using ('/db2temp/$INSTANCE/db_name/n003tmp/tempspace01') on dbpartitionnum (3)
using ('/db2temp/$INSTANCE/db_name/n004tmp/tempspace01') on dbpartitionnum (4)
extentsize 32
prefetchsize 128
bufferpool IBMDEFAULTBP
overhead 24.1
transferrate 0.9;

drop tablespace tempspace1;
```

For detailed steps of creating temp tablespaces in a different filesystem, refer to “Reallocate temp and user space1” on page 95.

## 2.2.3 Network configuration for a multiple partitioned installation

If you have a configuration that uses more than one machine for a single database instance, you must configure communications before installing DB2. In this section, we discuss how to set up rsh and NFS.

## Enabling rsh

To run DB2 ESE successfully, the rsh server has to be available on all machines in the partitioned database system. This server spawns a shell on the remote host and allows the user to execute commands. The rsh service is managed by inetd. Prior to enabling rsh, please ensure the rsh server rpm is installed, because many distributions do not install it by default.

## Enabling rsh on SuSE

To enable the rsh server and other related services on SuSE, perform the following steps:

- 1. Log on as root and manually edit the /etc/inetd.conf file. Remove # at the beginning of the line to enable a service, and disable what services you do not need by commenting them out (by adding a # at the beginning of the line). Only uncommented services are available. Example 2-8 provides an excerpt of the /etc/inetd.conf file on SuSE v8. In this example, we have enabled the in.ftpd, in.telnetd, in.rshd, and in.rlogind services, which enables ftp, telnet, rsh, and rlogin on your machine.

_Example 2-8 /etc/inetd.conf file_

```
# /etc/inetd.conf
# These are standard services.
#
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
# ftp stream tcp nowait root /usr/sbin/tcpd vsftpd
#
# If you want telnetd not to "keep-alives" (e.g. if it
# runs over a ISDN uplink), add "-n". See 'man telnetd' for more details.
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
```
