# Chapter 10 Backups

The final Bacula component is the catalog, the relational database in which Bacula stores information about every file and volume that is backed up. The catalog makes Bacula fast and efficient during a restore because the entire backup history is available-online; Bacula knows what storage volumes need to restore a particular file before it reads a single tape. Bacula currently supports three different databases: MySQL, PostgreSQL, and SQLite. The catalog database does not need to reside on the same server as the director.

An additional, optional component is the Bacula Rescue CD-ROM. This component is a separately downloadable package that creates individualized, bootable rescue CDs for Linux systems to use for “bare metal” recovery. The CDs contain a statically linked copy of the system's file daemon as well as customized scripts that configure information about the system's disks, kernel, and network interfaces. If a Linux system has a catastrophic failure, use its rescue CD to boot the fresh system, partition the disk, and connect to the Bacula director to perform a full system restore over the network.

# Setting up Bacula

Because of Bacula's complexity, advanced feature set, and modular design, there are many ways to use a site-wide backup scheme. In this section we walk through a basic Bacula configuration.

In general, six steps get Bacula up and running:

+   * Install a supported third-party database and the Bacula daemons.
* Configure the Bacula daemons.
* Install and configure the client file daemon.
* Start the Bacula daemons.
* Add media to media pools with the Bacula console.
* Perform a test backup and restore.

A minimal setup consists of a single backup server machine and one more clients. The clients run only a file daemon. The remaining four Bacula components (director daemon, storage daemon, catalog, and console) all run on the server. In larger environments it's advisable to distribute the server-side Bacula components among several machines, but the minimal setup works great for backing up to a few dozen systems.

# Installing the database and Bacula daemons

It's important to run the (major) version of Bacula on every system. In the past, some major releases have been incompatible with one another.

Before you install Bacula, you must first install the back-end database for your catalog. For sites backing up just a few systems, SQLite provides the easiest installation. If you are backing up more systems, it's advisable to use a more scalable database. Our experience with MySQL in this role has been positive, and we as-sum MySQL in the following examples.