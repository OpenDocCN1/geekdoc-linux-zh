```
`# tripwire --update-policy /etc/tripwire/twpol.txt`
```

You will be prompted for your site and local passphrases. After that, a new policy will be built. You can then rebuild the checksum database with the `tripwire --init` command. The "No such file" error messages should not appear this time.

# Checking file integrity

After the checksum database is built, you should periodically run Tripwire in integrity-checking mode. Integrity-checking mode will recompute the checksum for each file and check it against the checksum stored in the database, printing a warning message for any files that have changed. Use the `--check` parameter to do this:

```
`# tripwire --check`
```

Normally, no error messages will be reported. If, however, a file has been modified, you may receive a message that indicates that a cracker has gotten into your system and modified some of the operating system files, such as the `telnetd` program. The `telnetd` program may have been replaced with a version containing a backdoor through your security. It is critical that you replace any altered programs with the original versions from your Linux install CD or from a valid Linux distribution FTP site. Also, remove your system from the Internet while you do a thorough audit of your security logs, closing any revealed security holes.

Tripwire may report file changes that are not the result of a break-in. This most often happens when you have upgraded your operating system or installed software patches. Your best strategy is to run a Tripwire check just before installing any upgrades or patches. Assuming that there are no errors, proceed with the upgrade or patch, then use the `tripwire` command to update the checksum database. It is not necessary to completely rebuild the database; you may run Tripwire in update mode to rebuild only the checksums of those files that changed.

# Updating the database

To run Tripwire in update mode, invoke it with the `--update` parameter.

```
`# tripwire --update`
```

This will recalculate the checksums for any files that have changed since the last update and save those changes to the database. This is much less time-consuming than totally rebuilding the checksum database with the `tripwire --init` command.

> **TIP:** You can greatly improve the security of Tripwire by running it from a read-only media such as a CD-ROM, or at least from a media that is only mounted when Tripwire is run. Also, storing the checksum database on a removable media that is mounted only when needed is another way of improving Tripwire security.

I store my Tripwire executable and database on a CD-R writable CD-ROM drive. You will, of course, need to specify the different file paths when running the `tripwire` command. The `-d`