```
# rm vmunix vmunix.MOLARI vmunix.sys
```

# 12.2.2 Repairing a Broken CDS L

If you accidentally (or otherwise) remove a CDS L, you can repair it with the mkcdsl(8) command.

For example, we accidentally move a new kernel to the root directory out of habit.

```
# mv /sys/MOLARI/vmunix /

```

The kernel is now in the root directory and vmunix is no longer a CDS L.

```
# file /vmunix
/vmunix:
COFF format alpha executable or object module not stripped - version 3.13-14
```

We know that /vmunix is a supposed to be a CDS L, but what if we didn’t know that? Well, we can run the cdslinvchk(8) command, and it should tell us that there is a missing link and what it should be. It should also be noted that the clu_check_config(8) also executes cdslinvchk.

```
# cdslinvchk
Failed CDS L inventory check. See details in /var/adm/cdsl_check_list
```

```
# cat /var/adm/cdsl_check_list
Expected CDS L: /vmunix -> cluster/members/(memb)/boot_partition/vmunix
An administrator or application has replaced this CDS L with:
-rwxr-xr-x 1 root system 21009120 Dec 17 12:00 /vmunix
```

Now that we know what the link should be, we can repair it with the mkcdsl command. We will use the “-b” option to create the CDS L, have it point to the boot_partition, and use the “-c” option to copy the file to the location pointed to by the CDS L.

```
# mkcdsl -bc /vmunix
```

Verify that the procedure was successful.

```
# cdslinvchk
Successful CDS L inventory check
```

For more information on CDS Ls, as well as the cdslinvchk and mkcdsl commands, see chapter 6 and/or the cdslinvchk(8) and mkcdsl(8) reference pages.