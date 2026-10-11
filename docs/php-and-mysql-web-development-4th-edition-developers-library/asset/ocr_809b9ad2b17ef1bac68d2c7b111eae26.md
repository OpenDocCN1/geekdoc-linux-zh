# 14.4 Making Database Backups

It's important to back up your databases in case tables are lost or damaged. If a serious sys-tem crash occurs, you want to be able to restore your tables to the state they were in at the time of the crash with as little data loss as possible. Likewise, a user who issues an unwise DROP DATABASE, DROP TABLE, or DELETE statement may show up at your door requesting that you perform data recovery.

Database backups also are useful for copying databases to another server. Most com-monly, a database is transferred to a server running on another host, but you can also transfer data to a different server running on the same host. You might do this if you're testing a server for a new release of MySQL and want to use it with real data from your production server.

Another use for a backup is to set up a replication server, because one of the first steps in setting up a slave server is to take a snapshot of the master server at a specific point in time. The backup serves as this snapshot, and loading it into the slave server brings it up to date with respect to the master server. Thereafter, updates made on the master server are replicated to the slave server through the standard replication protocol. Section 14.8.2, “Establishing a Master-Slave Replication Relationship,” discusses the procedure for setting up replication.

Let’s begin with some general principles that govern backup practices and that will help you decide which techniques to use. Then we'll get to the details of specific backup methods.

There are two general categories of database backups:

+   Text-format backups made by using mysqldump to write table contents into dump files. These files consist of CREATE TABLE and INSERT SQL statements that can be reloaded into the server later to restore the tables.

+   Binary backups made by directly copying the files containing table contents. This type of backup can be made in various ways. For example, you can use a program such as mysqsho photocopy, cp, tar, or rsync.

Each method has its own advantages and disadvantages. Some of the factors to consider are whether you can leave the server running, the time needed to make the backup, portability of the backup, and the scope of what is backed up.

+   mysqldump operates in cooperation with the MySQL server, so you can use it while the server is running. Binary-backup methods involve file copy operations that are done external to the server. Some of these methods require that you stop the server. For those that do not, you still must take steps to ensure that the server does not modify the tables while you copy them.

+   mysqldump is slower than binary-backup techniques because the dump operation involves transferring the information over the network connection between mysqldump and the server. Binary-backup methods operate by copying files at the filesystem level and require no network traffic.