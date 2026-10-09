# ## Choosing an Installation Method

AIX can be installed using one of three methods: complete overwrite install, preservation install, or migration install. A complete overwrite install is used to install AIX on new computers or to overwrite a previous installation of the operating system without saving anything in the previous installation. A preservation install will attempt to preserve existing user directories in the root volume group (rootvg) by overwriting only the /, /usr, /var, and /tmp filesystems. As I will explain later in the chapter, a much safer strategy is to keep any user or local data in filesystems that do not reside in rootvg. The migration install option is used to retain the root volume group layout and system configuration files. This is the default installation option for AIX 5L version 5.1.

With any of these installation methods, you need to make sure that you have a good **mksysb**, or **sysback**, **rootvg** backup image. You may need to go back and retrieve a font file, or something, if you have a heavily customized system. Application fonts are the only things that I have ever lost with a migration upgrade. Having the backup tape makes it very easy to put the lost files back in place.

For an easy way out of a bad installation or upgrade, you should consider using the Alternate Disk Installation utility. Alternate Disk Install allows you to clone **rootvg** to an alternate set of disks. This technique can give you an easy way to recover from a failed migration (see “Using Alternate Disk Install,” later in this chapter).

# ## APPLY and COMMIT

Before installing new software or undertaking maintenance on an existing system, you need to have a back-out strategy in the event that problems occur during or after the installation. The AIX default is to add new software and maintenance to the system using the **COMMIT** option as opposed to the **APPLY** state. The **APPLY** option keeps a history file and a backup copy of each object replaced by the software update. If you are not happy with the update, you can **REJECT** the filesets and restore the previous version. When using **SMIT** to install software updates, set the **COMMIT Software?** options to No and the **Save Replaced?** option to Yes. These two **SMIT** options are mutually exclusive, meaning they must have opposite values. The command-line options are listed here:

```
#   installp -qa -d /usr/sys/install.images -X all    APPLY updates
#   installp -rB -X all                  REJECT updates
```

Once satisfied with the update, you can **COMMIT** the update to remove the backup copy of the previous version.

```
#   installp -c -g -X all              COMMIT updates

or

#   smitty install_commit              SMIT FastPath
```