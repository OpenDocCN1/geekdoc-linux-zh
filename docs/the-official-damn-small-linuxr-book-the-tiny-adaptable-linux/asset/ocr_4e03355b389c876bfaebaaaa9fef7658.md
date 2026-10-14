The following prompt appears, asking whether to format the target partition:

```
For INSTALL answer y to format, for UPGRADE answer n.
Format the target partition (y/..)? y
```

```
Last chance to exit before destroying all data on
Formatting target partition.
Setting up system image on target partition.
Setting up grub
```

4. When doing an installation, you want to format (y). Later, when you want to upgrade to a new version of DSL, you would not format the partition (n).

# NOTE

Upgrading a Frugal installation is as easy as running the installation script again. Because Frugal implies running from the untouched compressed image, all of your extensions and backup of configurations are unaffected during an upgrade. Only three system files are copied to the target media.

The last prompt of the Frugal Grub installation is to accommodate existing Windows installations. Because Frugal Grub installs into the master boot record, you must notify the script to add an entry for Windows. This includes all versions of Windows through Windows XP.

# NOTE

Later, in the “Poorman’s—An Easy Way to Try DSL” section, I will discuss the Poorman’s installation, which allows DSL to be installed within an existing Windows partition.

```
Do you have Windows installed on the first partition (y/..)?
Grub Installation Completed.
```

5. Type y if you have Windows installed on your first partition and you want to be able to choose to boot Windows or DSL from the Grub boot prompt. Type n if there is no Windows partition.