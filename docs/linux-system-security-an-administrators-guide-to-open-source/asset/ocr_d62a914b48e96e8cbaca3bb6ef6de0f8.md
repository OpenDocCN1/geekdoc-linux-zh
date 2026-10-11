# **Table 14.1** Necessary Scripts Found in the Tripwire Source Tree

| Script | Description |
| --- | --- |
| src/twdb_check.pl | A Perl script that verifies the integrity of the database against the configuration file. It is discussed in *Tripwire Update Mode* on page 402. |
| contrib/CheckConfig | A Bourne-shell script that checks the syntax of the configuration file against the existence of the files and directories referenced therein. It is discussed in *Tripwire Initialize Mode* on page 396. |
| contrib/tw_newinode.pl | A Perl script that corrects captured inode ^ numbers in the database after fsrand, or equivalent, is run. |
| contrib/zencrypt | A sample script using FIFO files with the -cf a option to *tripwire* and incorporating encryption and compression. We will look at examples similar to this in *Routine Tripwire Runs—Compare Mode* on page 399. |


^An inode (index node) is maintained by the filesystem for each file. See the references cited in *System Administration* on page 80 for further details about inodes. The *fsrand* utility is used to randomize the selection of node numbers, making NFS files handles more difficult to guess. It is available on Solaris platforms.

# **Example 14-1** Contents of tripwire-1.2-2.i386.rpm

```
/etc/cron.daily/tripwire.verify
/etc/tw.config
/usr/doc/tripwire-1.2
/usr/doc/tripwire-1.2/ChangeLog
/usr/doc/tripwire-1.2/FAQ
/usr/doc/tripwire-1.2/INTERNALS
/usr/doc/tripwire-1.2/README
/usr/doc/tripwire-1.2/README_FIRST
/usr/doc/tripwire-1.2/Readme
/usr/doc/tripwire-1.2/TOD0
/usr/doc/tripwire-1.2/WHATISNEW
/usr/doc/tripwire-1.2/docs
/usr/doc/tripwire-1.2/docs/README
/usr/doc/tripwire-1.2/docs/sgpdev.txt
/usr/doc/tripwire-1.2/docs/design.doc.ps
/usr/man/man5/tw.config.5
/usr/man/man8/sigen.8
/usr/man/man8/tripwire.8
/usr/sbin/sigen
/usr/sbin/tripwire
/var/spool/tripwire

```

Additionally, the RPM includes an example configuration file /etc/tw.config. It also adds the file /etc/cron.daily/tripwire.verify to automate Tripwire compare-mode runs (see *Routine Tripwire Runs—Compare Mode* on page 399). You will want to change both of these based on the needs of a particular system as discussed in the following sections.