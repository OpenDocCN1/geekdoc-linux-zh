# Chapter 10 Backups

own storage daemon. Want to back up to an off-site location? Install a storage daemon on a server. Need to back up new clients? Install and configure the clients' file daemons. New backup administrator? Install the management console on his or her workstation.

The configuration files are human-readable text files. The sample configuration files included in the Bacula distribution are well documented and are a great starting point for a typical configuration.

Before we begin a more detailed discussion of our example set, first define some key Bacula terms.

+   * "Jobs" are the fundamental unit of Bacula activity. They come in two flavors: backup and restore. A job comprises a client, a fileset, storage pool, and a schedule.
* "Pools" are groups of physical media that store jobs. For example, you might use two pools, one for full backups and another for incrementals.
* "Filesets" are lists of systems and individual files. Files can be explicitly included in or excluded from backup or restore.
* "Messages" are inter-daemon communiqués (log entries, really) regarding the status of daemons and jobs. Messages can also be sent by email and written to log files.

We do not cover all the possible configuration parameters in this chapter. Instead, we begin each section with a general overview and then point out some parameters that we are either particularly useful or hard to grasp.

# Common configuration sections

The Bacula configuration files are composed of sections known generically as “resources.” Each resource is enclosed in curly braces. Some resources appear in multiple configuration files. Comments are introduced with a # sign in all Bacula configuration files.

All four files contain a Director resource:

```
# Sample Bacula director configuration file, /etc/bacula-dir.conf
```

```
Director {
  Name = bull-dir # a canonical name for our Bacula
  DIRPort = 9101
  Query File = "/etc/bacula/query.sql"
  Working Directory = "/var/Bacula/working"
  Pid Directory = "/var/run"
  Maximum Concurrent Jobs = 1
  Password = "zHpScUnHN9"
  Messages = Standard
}
```