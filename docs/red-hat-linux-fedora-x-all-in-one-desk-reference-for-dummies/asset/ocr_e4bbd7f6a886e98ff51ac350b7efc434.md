# 546 Using SELinux

You can easily check the context of a file, a user, or a process by using the -Z option with the usual Linux commands such as ls, id, and ps. For example, to see the details of the /etc/passwd file including its security context, type ls -Z /etc/passwd. Here is a typical output of this command (if SELinux is not enabled, you will get an error message):

```
-rw-r--r-- root root system_u:object_r:etc_t    /etc/passwd
```

**Note:** The context is in the form of three colon-separated fields that precede the filename — the first field is the identity, the second field is the role, and the third field is the type.

If you want to know the context of whatever user ID you are currently logged in, type id -Z. For example, here is the output of the id -Z command when you are logged in as root:

```
root:sysadm_r:sysadm_t
```

To see the processes with their security contexts, type ps axZ. Here is a partial listing of output from the ps axZ command (the context appears in the second column):

| PID CONTEXT COMMAND |
|---|---|
| 1 system_u:system_r:init_t | init [5] |
| 2 system_u:system_r:kernel_t | [koftiqd/0] |
| 3 system_u:system_r:kernel_t | [events/0] |
| 4 system_u:system_r:kernel_t | [kblockd/0] |
| 5 system_u:system_r:kernel_t | [pdfhd] |
| 6 system_u:system_r:kernel_t | [pdflush] |
| 7 system_u:system_r:kernel_t | [aio/0] |
| 8 system_u:system_r:kernel_t | [kwaspd0] |
| 9 system_u:system_r:kernel_t | [kserold0] |
| 113 system_u:system_r:kernel_t | [kjournal] |
| 102 system_u:system_r:kernel_t | [khbd0] |
| 240 system_u:system_r:kernel_t | [usb-storage] |
| 241 system_u:system_r:kernel_t | [scsi_eh_0] |
| 770 system_u:system_r:kernel_t | [kjournal] |
| ... lines deleted ... |

To perform some tasks such as system administration with SELinux enabled, you have to assume a specific role. You can assume a new role (provided you have access to that new role) by using the newrole command. For example, to change to the sysadm_r role (the system administrator role), type the following command:

```
newrole -r sysadm_r
```