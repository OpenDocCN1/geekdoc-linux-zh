
### 7.5.1.4 How Do I Fix a “second device status is active” Error?

Occasionally when you replace a device, the dfsl.dat and dfsc.dat files need to be updated; otherwise, when you attempt to rename the new device back to the old device special file, you will see the following:

```
# dsfmgr -m dsk7 dsk9
dsfmgr: ERROR: second device status is active: dsk9a
```

First, you will need to identify which HWID is associated with dsk9. You will probably already know which it is, because you probably deleted the component when you replaced the device. If you do not know the HWID, however, you can still find it by searching the dfsc.dat file.

```
# grep "dsk 9 a" /etc/dfsc.dat
A: 0 13000b1 59 17 0 b ** /dev/disk/ dsk 9 a
A: 0 13000b2 59 17 0 c ** /dev/rdisk/ dsk 9 a
```

Or try:

```
# awk '/dsk 9 / { print $4 }' </etc/dfsc.dat | uniq
59
```

We printed for the 4th field because it is HWID (see section 7.3). Also, be very careful with the search string; make sure the pattern is: /dsk<space><instance number><space>/ The <space> characters are very important.

The HWID is 59, and this is the one we need to remove from the files. Now that we have the HWID, we can remove it from the dfsl.dat and dfsc.dat files. We will do this using an undocumented switch "-Z" to the dsfmgr command.

```
# dsfmgr -Z rm_hwid 59 0
-dsk9a -dsk9b -dsk9c -dsk9d -dsk9e -dsk9f -dsk9g -dsk9h -dsk9a -dsk9b -dsk9c -dsk9d -dsk9e -dsk9f -dsk9g -dsk9h
```

This will remove the HWID entries from the dfsc.dat and dfsl.dat database files. Alternatively, if you need to remove entries from only one file, you can use the "rm_local_hwid" flag to remove the HWID from the dfsl.dat file or the "rm_cluster_hwid" flag to remove the HWID from the dfsc.dat file.

At this point, the "dsfmgr -m" command should work.

The error will look like this:

```text
# dsmgr -e dsk7 dsk9

dsmgr: ERROR: find device node dsk9  : Device record not found in status database
dsmgr: ERROR: exchange failed: Device record not found in status database
```

Follow the “How Do I Fix a “second device status is active” Error?” procedure (section 7.5.1.4) to resolve the problem.

### 7.5.1.7  How Can I Verify that My Device Special File Databases are Error Free?

```text
# dsmgr -v

dsmgr: verify all datum for system at /

Default File Tree:
    OK.

Device Class Directory Default Database:
    OK.

Device Category to Class Directory Database:
    OK.

Dev directory structure:
    OK.

Device Status Files:
    OK.

Dev Nodes:
    OK.
```

### 7.5.1.8  How Can I Repair Errors in My Device Special File Databases?

Fix database errors or inconsistencies (output not shown). Note this may need to be run a few times to correct errors.

```text
# dsmgr -vF
```

**NOTE:**

The “-o” and “-O” options are used to create the pre-V5 device names that are not supported in a *TruCluster Server* environment.

For more information, see the **dsmgr(8)** reference page as well as the *Tru64 UNIX System Administration* guide.

## 7.5.2  The dn_setup Command

The dn_setup command uses dsmgr to create device special files for the system. This command is run every time the system is rebooted. The dn_setup command can also be used to recreate the devices in /dev and /devices.

To create a tape device when booting from the installation CD to restore the operating system, you can use dn_setup with the “--install_tape” switch. As a general rule, dn_setup should not be used except in those situations where the devices and device databases reach a state where no other command (dsmgr or hwmgr) can clear things up.

Caution should be taken whenever using the dn_setup command with the “--init” or “--clean” options, especially if you are using LSM, because dn_setup will not recreate the LSM devices. See Chapter 14 (“Cluster Logical Storage Manager”) for a detailed discussion.

### 7.5.2.1  How Can I Reinitialize My /dev and /devices Directories?

```sh
# dn_setup -init
```

After executing this command, it is important to run “dsmgr -K” immediately afterward. Furthermore, if you are using LSM, you must also run the following commands:

If the system is in multi-user mode (or in single-user mode with /usr mounted):

```sh
# /usr/sbin/volinstall update
# /sbin/volclt enable
```

If the system is in single-user mode and /usr cannot be mounted (likely because /usr is encapsulated within LSM):
