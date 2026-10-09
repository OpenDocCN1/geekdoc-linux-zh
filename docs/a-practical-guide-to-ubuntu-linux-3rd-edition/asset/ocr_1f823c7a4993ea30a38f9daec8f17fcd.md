information about these users and groups. Set **MINUID** to the lowest UID number you want to include in the NIS maps and set **MINGID** to the lowest GID number you want to include.

Ubuntu: 1000/1000

**NFSSNOBODYYID, NFSSNOBODYGID**

Specify the UID and GID, respectively, of the user named **nfsnobody**. NIS does not export values for this user. Set to 0 to export maps for **nfsnobody**.

Ubuntu: 4294967295/4294967295

**MERGE\_PASSWD, MERGE\_GROUP**

When set to TRUE, merge the /etc/shadow and /etc/passwd files and the /etc/gshadow and /etc/group files in the **passwd** and **group** maps, respectively, enabling shadow user passwords and group passwords.

Ubuntu: FALSE/FALSE

# FILE LOCATIONS

The next sections of */var/yp/Makefile* specify standard file locations; you do not normally need to change these entries. This part of the makefile is broken into the following groups:

+   *   **Commands**	Locates awk (mawk) and make and sets a value for umask (page 459)
+   *   **Source directories**	Locates directories that contain NIS source files
+   *   **NIS source files**	Locates NIS source files used to build the NIS database
+   *   **Servers**	Locates the file that lists NIS servers

# THE ALL TARGET

The **ALL** target in */var/yp/Makefile* specifies the maps that **make** is to build for NIS:

```
```
ALL =    passwd group hosts rpc services netid protctols netgrp
#ALL += publickey mail ethers bootparams printcap
#ALL += amd.home auto.master auto.home auto.local
#ALL += timezone locale networks netmasks
```
```

The first line of the **ALL** target lists the maps that **make** builds by default. This line starts with the word **ALL**, followed by an equal sign and a **TAB**. The last three lines are commented out. Uncomment lines or delete or move map names until the list matches your needs.

As your needs change, you can edit the **ALL** target in *Makefile* and run **make** in the */var/yp* directory to modify the list of maps distributed by NIS.

# START THE SERVERS

Restart the master server (page 745) and then the slave servers after completing the preceding steps. On a master server, the **nis** init script starts the **ypserv**, **ypasswd**,