
The resource registry history database is used to track the failure history of a resource. This database, like the resource registry database, is binary in format, so the best approach to getting information from the database is to use the caa_stat command. Resource failure history can be retrieved using the "-v" option.

```
# caa_stat -v nicUP
NAME=nicUP
TYPE=network
FAILURE_THRESHOLD=2
FAILURE_COUNT=0 on molari
FAILURE_COUNT=0 on sheridan
TARGET=ONLINE on molari
TARGET=ONLINE on sheridan
STATE=ONLINE on molari
STATE=ONLINE on Sheridan
```

As with the resource registry database (if you're a CT²S² that is), you can dump the resource registry history database using the caa_dbConvert command.

```
# /usr/sbin/cluster/caa_dbConvert DUMP caa.his.binaryDB /tmp/caa.his.txt
```

Here is an excerpt of the convert database showing the information for the nicUP resource.

```
__RESOURCE__,nicUP
2_FAILURE_HISTORY,1018678401 1018682922
_
```

You can see that the last two times the nicUP resource failed as follows:

```
# perl -e 'foreach $i (1018678401,1018682922)
> { printf ("%s\n", scalar localtime $i) };'
Sat Apr 13 02:13:21 2002
Sat Apr 13 03:28:42 2002
```

## 23.3.5 Directory Layout

Figure 23.2 shows the various locations where the majority of CAA-related directories and files are located. Note that we have not included each and every file or directory location. For an exhaustive list you can use the find(1) command.

```
# find / -name "*[Cc] [Aa] [Aa]*"
```

If you happen to have a cluster that is running a patched version of V5.1A, you will see a hybrid directory layout containing some of the files seen in V5.1B. This is due to the work that was done by the CAA Engineering group in support of the "Compaq Database Utility with Oracle® Real Application Clusters".

## V5.0A, V5.1, & V5.1A

![](img/a0df85c2e542a8d6c913113908553aa4_670_0.png)

## V5.1B

![](img/a0df85c2e542a8d6c913113908553aa4_670_1.png)

Figure 23-2: CAA Directories and Files

Note that the log subdirectory under /var/cluster/caa is obsolete and should no longer be used.

## 23.3.6 CAA Commands

CAA has a command-line interface as well as a graphical user interface (GUI). The easiest way to determine what CAA commands are available (or really what CAA information is available), you can simply use the man(1) command with the "-k" option (or the apropos(1) command).

```
# man -k caa
```

Another option is to use the sman script that we wrote. The sman command is essentially a section-based "man -k" command that also formats the output. The advantage of sman is that you can narrow your search criteria to only the sections in which you are interested. For example, if you only want commands, you can limit your search to sections 1 and 8.

```
# sman [18] caa
```

| Section | Reference Page | Description |
|---|---|---|
| 8 | caa_balance | Finds the optimal member for an application resource and relocates the resource to that member if it is not currently placed there. |
| 8 | caa_profile | Creates, validates, deletes, and updates a Cluster Application Availability (CAA) resource profile |
| 8 | caa_register | Registers a resource with Cluster Application Availability (CAA) |
| 8 | caa_relocate | Relocates an application resource from one cluster member to another |
| 1 | caa_report | reports availability statistics for application resources |
| 8 | caa_start | Starts resources that have been registered with Cluster Application Availability (CAA). |
| 1 | caa_stat | Provides status on Cluster Application Availability (CAA) resources within a cluster. |
| 8 | caa_stop | Stops a Cluster Application Availability (CAA) application resource |
| 8 | caa_unregister | Unregisters a Cluster Application Availability (CAA) resource. |
| 8 | caad | Cluster Application Availability (CAA) daemon |

Using the "all" keyword will search all man sections.

```
# sman all caa
Section  Reference Page  Description
-------- --------------- ------------------------------------------------
4         caa             Cluster Application Availability (CAA)
                          information
```

The good news with CAA is that the commands you will be using all start with "caa_". All you need to remember is the action you want to perform.

Note that the GUI does not show up in the output of "man -k" or "sman". This is because the GUI is a sysman(8) application plug-in. Use the "sysman -list" command to find the list of sysman accelerators.

```
# sysman -list | grep -i caa
| Cluster Application Availability (CAA) Management [caa]
```

To manage CAA with sysman using the "caa" accelerator.

```
# sysman caa
```

# NOTE:

The caa_balance(8) and caa_report(1) commands were added in V5.1B.

## 23.4 Resources
