
## Pool resources

A Pool resource groups backup media, typically tapes, into sets that are used by specific backup jobs. It may be useful to separate tapes that you use for off-site archival storage from those that you use for nightly incrementals. Each piece of media is assigned to a single Pool, so it’s easy to automatically recycle some tapes and archive others.

```
Pool {
    Name = Full_Pool
    Pool Type = Backup
    Recycle = yes
    AutoPrune = yes
    Storage = T1 4000
    Volume Retention = 365 days
}
```

## Schedule resources

Schedule resources define the timetables for backup jobs. The name, date, and time specification are the only required parameters, but as you can see from the example below, you can sneak in additional parameter values. These values then override the default parameters set in a Job specification.

Below, full backups run on the first Tuesday of each month at 8:10 p.m. The incremental backups use a different tape pool and run every week from Wednesday through Monday at 8:10 p.m.

```
Schedule {
    Name = "Nightly"
    Run = Level=Full Pool=Full_Pool 1st tue at 20:10
    Run = Level=Incremental Pool=Incremental_Pool wed-mon at 20:10
}
```

## Client resources

Client resources identify the computers to be backed up. Each resource has a unique name, IP address, and password; one is required for each client. The catalog for storing backup metadata is also specified. The parameters File Retention and Job Retention specify how long file and job records for this client should be kept in the catalog. If the AutoPrune parameter is set, expired data is deleted from the catalog. Pruning affects only the catalog records and not the actual files stored on backup tapes; recycling of tapes is configured in the Pool resource.

```
Client {
    Name = harp
    Address = 192.168.1.28
    FDPort = 9102
    Catalog = MYSQL
    Password = "TbEpJqrcy"
}
```

## FileSet resources

A FileSet resource defines the files and directories to be included in or excluded from a backup job. Unless you have systems with identical partitioning schemes, you’ll probably need a different fileset for each client. FileSet resources can define multiple Include and Exclude parameters, along with individual Options such as regular expressions. By default, Bacula recursively backs up directories but does not span partitions, so take care to list in separate File parameters all the partitions you want to back up.

In the example below, we enable software compression as well as the signature option, which computes a hash value for each file backed up. These options increase the CPU overhead for backups but can save tape capacity or help identify files that have been modified during a suspected security incident.

```
FileSet {
  Name = "harp"
  Include {
    Options {
      signature=SHA1
      compression=GZIP
    }
    File = "/"
    File = "/boot"
    File = "/var"
  }
  Exclude = { /proc /tmp /journal /fsck }
}
```

## Job resources

A Job resource defines the overall characteristics of a particular backup job by tying together Client, FileSet, Storage, Pool, and Schedule resources. In general, there is one Job definition per client, although you can easily set up multiple jobs if you want to back up different FileSets at different frequencies.

You can supply an (optional) JobDefs resource to set the defaults for all backup jobs. Use of this resource can simplify the per-job configuration data.

```
Job {
  Name = "Harp"
  JobDefs = DefaultJob
  Level = Full
  Write Bootstrap = "/bacula/bootstraps/harp.bsr"
  Client = harp
  FileSet = harp
  Pool = Full_Pool
  Incremental Backup Pool = Incremental_Pool
  Schedule = "Nightly"
  Prefer Mounted Volumes = no
  Max Run Time = 36000
}
```

A "bootstrap" file is a special text file, created by Bacula, that contains information about files to restore. Bootstrap files list the files and volumes needed for a restore job and are incredibly helpful for bare-metal restores. They are not mandatory but are highly recommended.

Bootstrap files are created during restores, or during backups if you have defined the Write Bootstrap parameter for the job. Write Bootstrap tells Bacula where to save the bootstrap information. Bootstrap files are overwritten during full backups and appended to during incremental backups.

## bacula-sd.conf: storage daemon configuration

Storage daemons accept data from file daemons and transfer it to the actual storage media (or vice versa, in the case of a restore). The resources Storage, Device, and Autochanger are defined within the bacula-sd.conf file, along with the common Messages and Director resources.

### The Director resource

The Director resource controls which directors are permitted to contact the storage daemon. The password in the Storage resource of bacula-dir.conf must match the password in the Director resource of bacula-sd.conf.

```
Director {
  Name = bull-dir
  Password = "jIKkrZuE00"
}
```

### The Storage resource

The Storage resource is relatively straightforward. It defines some basic working parameters such as the daemon's network port and working directory.

```
Storage {
  Name = bull-sd
  SDPort = 9103
  WorkingDirectory = "/var/bacula/working"
  Pid Directory = "/var/run"
  Maximum Concurrent Jobs = 2
}
```

### Device resources

Each storage device gets its own Device resource definition. This resource specifies details about the physical backup hardware, be it tape, optical media, or online storage. The details include media type, capabilities, and autochanger information for devices that are managed by a tape changer or media robot.

The example below defines an LTO-3 drive with an automatic tape changer. Note that /dev/nst0 is a non-rewinding device, which is almost invariably what you want. The Name parameter defines a symbolic name that's used to associate the
