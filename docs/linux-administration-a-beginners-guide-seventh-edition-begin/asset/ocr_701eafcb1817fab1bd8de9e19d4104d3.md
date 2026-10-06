# 216 Linux Administration: A Beginner's Guide

The initctl command can be used to display a listing of all jobs and their states. This example lists all of jobs and their states:

```
root@ubuntu-server:~# initctl list
```

# The /etc/inittab File: Legacy Notes

Although rarely used anymore, the /etc/inittab file contains all the information it needs for starting runlevels. Because initab has been around for a long time, it is likely that you will still come across it on older versions of numerous modern Linux distributions and so we mention it here for legacy reasons.

The format of each line in this file is as follows:

```
id:runlevels:process
```

Table 8-1 explains the significance of each of the four fields of an entry in the /etc/inittab file. Table 8-2 defines some options available for the action field in this file.

| Field | Description |
|---||
| id | A unique sequence of one to four characters that identifies this entry in the /etc/inittab file |
| runlevels | The runlevels at which the process should be invoked. Some events are special enough that they can be trapped at all runlevels (for instance, the CTRL-ALT-DEL combination to reboot). To indicate that an event is applicable to all runlevels, leave this field blank. If you want something to occur at multiple runlevels, simply list all of them in this field. For example, the entry 123 would specify something that runs at runlevels 1, 2, and 3. |
| action | Describes what action should be taken. Options for this field are explained in Table 8-2. |
| process | Names the process (or program) to execute when the runlevel is entered. |

**Table 8-1** /etc/inittab Entries