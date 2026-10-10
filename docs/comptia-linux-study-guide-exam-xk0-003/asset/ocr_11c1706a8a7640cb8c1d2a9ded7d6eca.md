Many distributions ship with Tripwire, but it may not be installed by default. The utility is controlled through two configuration files: *tw.cfg* and *tw.pol*, which often reside in */etc/tripwire*. The *tw.cfg* file controls overall configuration options, such as where *tw.pol* resides, how Tripwire sends reports to the system administrator, and so on. The *tw.pol* file includes information on the files it’s to include in its database, among other things. Both files are binary files created from text-mode files called *twcfg.txt* and *twpol.txt*, respectively. You may need to edit *twpol.txt* to eliminate references to files you don’t have on your system and to add information on files you do have but that the default file doesn’t reference. Use the *twinstalt.sh* program (which often resides in */etc/tripwire*) to generate the binary configuration files and other critical database files. This utility will ask you to set a pair of passphrases, which are like passwords but are typically longer, to control access to the Tripwire utilities. You’ll then need to enter these passphrases to have the utility do its encoding work.

Once you’ve generated the basic setup files, type `tripwire --init` to have it generate initial checksums and hashes on all the files it’s configured to monitor. This process is likely to take a few minutes. Thereafter, typing `tripwire --check` will check the current state of the system against the database, and typing `tripwire --update` will update the database (say, in case you upgrade a package). The `--init` and `--update` operations require you to enter the passphrase, but `--check` doesn’t. Therefore, you can include an automated Trip-wire check in a cron job.

![](bbox=[0.13, 0.48, 0.25, 0.56])

> Tripwire is best installed and initialized on a completely fresh system, before connecting the computer to the Internet but after all programs have been configured. Although it’s possible to install it on a system that’s been up and running for some time, if that computer has already been compromised without your knowledge, Tripwire won’t detect that fact.

# Generating Checksums Manually

If Tripwire is overkill, you can deploy a manual check for changes to files by using checksum programs, which generate short strings that are likely to be unique. Both *md5sum* and *sha1sum* create such checksums, although they generate different checksums:

```
$ md5sum /etc/passwd
f7ba3e97209ca5c4c8040276db5dc329 /etc/passwd
$ sha1sum /etc/passwd
3fc1d2e5d4ec5bf09d12beaf5a013cbf7fd5af1 /etc/passwd
```

If you keep checksums of critical files, you can easily spot changes to them—if the checksum value has changed, then the file has changed. The key to such comparisons is to take a set of checksums before the computer could have been compromised; to do any good, a checksum must have a comparison value. If the file might change legitimately, such as */etc/passwd*, remember to take a new checksum after you make any legitimate changes.